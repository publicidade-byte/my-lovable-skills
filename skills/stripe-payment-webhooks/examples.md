# Stripe payment webhook examples

## Full handler skeleton (Deno edge)

```ts
import { createClient } from "npm:@supabase/supabase-js@2";
import Stripe from "npm:stripe@17";

const supabase = createClient(
  Deno.env.get("SUPABASE_URL")!,
  Deno.env.get("SUPABASE_SERVICE_ROLE_KEY")!
);

async function alreadyProcessed(eventId: string) {
  const { data } = await supabase
    .from("stripe_webhook_events")
    .select("id")
    .eq("id", eventId)
    .maybeSingle();
  return !!data;
}

async function markProcessed(event: Stripe.Event) {
  await supabase.from("stripe_webhook_events").insert({
    id: event.id,
    type: event.type,
  });
}

async function upsertSubscription(sub: Stripe.Subscription, userId: string) {
  const priceId = sub.items.data[0]?.price?.id ?? null;
  await supabase.from("subscriptions").upsert({
    user_id: userId,
    stripe_customer_id: sub.customer as string,
    stripe_subscription_id: sub.id,
    status: sub.status,
    price_id: priceId,
    current_period_end: new Date(sub.current_period_end * 1000).toISOString(),
    cancel_at_period_end: sub.cancel_at_period_end,
    updated_at: new Date().toISOString(),
  });
}

Deno.serve(async (req) => {
  if (req.method !== "POST") return new Response("Method not allowed", { status: 405 });

  const stripe = new Stripe(Deno.env.get("STRIPE_SECRET_KEY")!, {
    apiVersion: "2024-11-20.acacia",
    httpClient: Stripe.createFetchHttpClient(),
  });
  const cryptoProvider = Stripe.createSubtleCryptoProvider();
  const body = await req.text();
  const sig = req.headers.get("stripe-signature")!;

  let event: Stripe.Event;
  try {
    event = await stripe.webhooks.constructEventAsync(
      body,
      sig,
      Deno.env.get("STRIPE_WEBHOOK_SECRET")!,
      undefined,
      cryptoProvider,
    );
  } catch (err) {
    console.error("Webhook signature verification failed", err);
    return new Response("Webhook signature verification failed", { status: 400 });
  }

  if (await alreadyProcessed(event.id)) {
    return new Response(JSON.stringify({ received: true, duplicate: true }), { status: 200 });
  }

  try {
    switch (event.type) {
      case "checkout.session.completed": {
        const session = event.data.object as Stripe.Checkout.Session;
        const userId = session.client_reference_id ?? session.metadata?.user_id;
        if (!userId) break;
        if (session.mode === "subscription" && session.subscription) {
          const sub = await stripe.subscriptions.retrieve(session.subscription as string);
          await upsertSubscription(sub, userId);
        }
        break;
      }
      case "customer.subscription.updated":
      case "customer.subscription.deleted": {
        const sub = event.data.object as Stripe.Subscription;
        const { data: row } = await supabase
          .from("subscriptions")
          .select("user_id")
          .eq("stripe_subscription_id", sub.id)
          .maybeSingle();
        if (row?.user_id) await upsertSubscription(sub, row.user_id);
        break;
      }
    }
    await markProcessed(event);
  } catch (e) {
    console.error("Webhook handler error", event.id, e);
    return new Response("Handler failed", { status: 500 });
  }

  return new Response(JSON.stringify({ received: true }), { status: 200 });
});
```

## Create Checkout with metadata (server)

```ts
const session = await stripe.checkout.sessions.create({
  mode: "subscription",
  customer_email: user.email,
  client_reference_id: user.id,
  metadata: { user_id: user.id },
  line_items: [{ price: priceId, quantity: 1 }],
  success_url: `${origin}/billing?success=1`,
  cancel_url: `${origin}/pricing`,
});
```

## Client polling after redirect (optional UX)

```ts
// billing?success=1 — poll until webhook writes subscription (max ~30s)
const { data } = await supabase.from("subscriptions").select("status").eq("user_id", uid).single();
```
