# Examples — typed API hooks and forms

## `api/users.ts`

```ts
import { supabase } from "@/lib/supabase";
import type { Database } from "@/types/database";

type User = Database["public"]["Tables"]["users"]["Row"];

export async function fetchUser(userId: string): Promise<User | null> {
  const { data, error } = await supabase
    .from("users")
    .select("*")
    .eq("id", userId)
    .maybeSingle();
  if (error) throw error;
  return data;
}

export async function updateUser(
  userId: string,
  patch: Database["public"]["Tables"]["users"]["Update"]
): Promise<User> {
  const { data, error } = await supabase
    .from("users")
    .update(patch)
    .eq("id", userId)
    .select()
    .single();
  if (error) throw error;
  return data;
}
```

## `hooks/useUser.ts`

```ts
import useSWR from "swr";
import { fetchUser } from "@/api/users";

export function useUser(userId: string | null | undefined) {
  const { data, error, isLoading, mutate } = useSWR(
    userId ? (["user", userId] as const) : null,
    () => fetchUser(userId!)
  );
  return {
    user: data ?? null,
    error,
    isLoading,
    refresh: mutate,
  };
}
```

## Dashboard: three components, one request

```tsx
// All three share the same SWR cache key ["user", id]
function Header() {
  const { user } = useUser(id);
  return <span>{user?.display_name}</span>;
}
function Sidebar() {
  const { user } = useUser(id);
  return <Avatar src={user?.avatar_url} />;
}
function ProfileCard() {
  const { user, isLoading } = useUser(id);
  if (isLoading) return <Skeleton />;
  return <Card>{user?.bio}</Card>;
}
```

## Create flow with mutation + cache update

```tsx
function CreatePostDialog() {
  const { refresh } = usePosts({ authorId: userId });

  async function handleSubmit(values: PostFormValues) {
    await createPost({ ...values, author_id: userId });
    await refresh();
  }

  return <PostForm onSubmit={handleSubmit} />;
}
```

## `schemas/profile.ts` + `components/ProfileForm.tsx`

```ts
import { z } from "zod";

export const profileFormSchema = z.object({
  display_name: z.string().min(1).max(80),
  bio: z.string().max(500).optional(),
  website: z.string().url().optional().or(z.literal("")),
});

export type ProfileFormValues = z.infer<typeof profileFormSchema>;
```

```tsx
const form = useForm<ProfileFormValues>({
  resolver: zodResolver(profileFormSchema),
  defaultValues: { display_name: "", bio: "", website: "" },
});

async function onSubmit(values: ProfileFormValues) {
  await updateUser(userId, values);
  await refreshUser();
}
```

## Invalidating related keys after delete

```ts
import { mutate } from "swr";

async function handleDeletePost(postId: string) {
  await deletePost(postId);
  await mutate(["post-detail", postId], undefined, false);
  await mutate((key) => Array.isArray(key) && key[0] === "posts");
}
```
