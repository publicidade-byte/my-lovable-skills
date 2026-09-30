# My Lovable Skills

Pacote reutilizável de skills para projetos de vibe coding com foco em segurança.

Este repositório reúne skills que podem ser usadas em diferentes projetos, com o objetivo de:

- adotar padrões seguros por padrão
- evitar confiar no frontend para decisões de segurança
- aplicar verificações especializadas apenas quando fizer sentido
- separar vulnerabilidades reais de melhorias opcionais
- tornar auditorias de segurança mais fáceis de entender

---

# Security Pack

A skill principal de orquestração é:

`security-pack`

Ela identifica quais skills especializadas são relevantes para o projeto atual.

As skills especializadas são:

- `security-core`
- `supabase-rls-and-auth`
- `server-input-validation`
- `edge-functions-and-webhooks`
- `rate-limiting-edge`
- `audit-logging-backend`
- `lovable-ship-checklist`

---

# O que cada skill faz

## security-pack

É a orquestradora principal de segurança.

Use para:

- identificar quais módulos de segurança são relevantes
- coordenar várias skills
- evitar aplicar controles desnecessários
- organizar a auditoria final

É o ponto de entrada recomendado para tarefas de segurança.

---

## security-core

Framework universal de segurança.

Use para:

- classificação de severidade
- Critical / High / Medium / Low
- recomendações de hardening
- separar controles verificados de não verificados
- reduzir falsos positivos
- avaliar prontidão para produção
- analisar confiança no frontend
- exposição de segredos
- autorização
- IDOR
- estruturação de auditorias

Essa skill deve organizar e classificar os achados das skills especializadas.

---

## supabase-rls-and-auth

Use quando o projeto utiliza Supabase.

Foco em:

- Row Level Security
- `auth.uid()`
- políticas SELECT
- políticas INSERT
- políticas UPDATE
- políticas DELETE
- `anon`
- `authenticated`
- `service_role`
- IDOR
- escalonamento de privilégios
- políticas de Storage
- funções `SECURITY DEFINER`
- fronteiras de autenticação e autorização

---

## server-input-validation

Use quando a aplicação recebe dados controlados pelo usuário.

Foco em:

- validação server-side
- constraints no banco
- schemas Zod
- enums
- IDs
- números
- quantidades
- datas
- arquivos
- valores manipulados no frontend

A validação no frontend não deve ser tratada como única barreira de segurança.

---

## edge-functions-and-webhooks

Use quando o projeto possui:

- Server Functions
- Edge Functions
- rotas de API
- APIs externas
- webhooks
- integrações backend

Foco em:

- autenticação
- autorização
- segredos
- tratamento de erros
- separação cliente/servidor
- verificação de webhooks
- proteção contra replay
- idempotência

Aplique regras específicas de webhook somente quando o projeto realmente utilizar webhooks.

---

## rate-limiting-edge

Use quando endpoints podem sofrer abuso por chamadas repetidas ou automatizadas.

Exemplos:

- login
- signup
- recuperação de senha
- pagamentos
- cupons
- chamadas de IA
- envio de e-mail
- queries caras
- APIs públicas

Os limites devem ser definidos conforme o contexto do produto.

Não criar limites arbitrários sem entender o uso esperado.

---

## audit-logging-backend

Use quando o projeto possui ações sensíveis ou administrativas.

Exemplos:

- ações de admin
- mudanças de papel
- alterações de conta
- eventos de pagamento
- mudanças de configuração
- mudanças de permissão

Nunca registrar:

- senhas
- tokens de autenticação
- chaves privadas
- dados completos de cartão
- segredos privados

---

## lovable-ship-checklist

Use antes do lançamento ou publicação em produção.

Foco em:

- revisão final de segurança
- segredos
- autenticação
- configurações de produção
- tratamento de erros
- acessibilidade
- prontidão para lançamento
- configurações externas ainda não verificadas

Essa skill não deve declarar que uma aplicação está segura para produção apenas com base na análise do repositório.

---

# Uso recomendado

## Auditoria geral de segurança

Comece com:

`security-pack`

Prompt recomendado:

```text
Use a skill security-pack para revisar este projeto.

Identifique quais skills especializadas de segurança são relevantes.

Depois execute a auditoria utilizando apenas os módulos necessários.

Separe:
- Critical
- High
- Medium
- Low
- Hardening
- Controles verificados
- NOT VERIFIED

Não altere o projeto.
