# mintlify-docs — documentação pública da API

Se as regras transversais ainda não estiverem no contexto, ler [`../AGENTS.md`](../AGENTS.md).

Mintlify em MDX com frontmatter YAML; configuração em `docs.json`. Tudo em pt-BR, títulos em Title Case, segunda pessoa, voz ativa e uma ideia por frase. Código/campo/rota em `código`; elementos da UI em **negrito**.

## Vocabulário

| Usar | Não usar no texto público |
|---|---|
| WhatsApp Oficial | “Cloud API” como nome do canal |
| WhatsApp por QR Code | Evolution, não-oficial, fork |
| modelo | template, salvo o campo `template_name` |
| número do WhatsApp | instância, salvo campo literal |
| funil | pipeline, salvo a rota `/pipelines` |
| disparo | broadcast |
| Desenvolvedores | Developers |

## Contrato

- A doc segue o código. Ao criar/alterar contrato ou exemplo de endpoint, conferir router em `../server/routes/public/v1/`, schema Zod e formatter da resposta. Correção editorial não exige reauditar a implementação. Não documentar rota interna, Admin, coleção, índice, fila ou provedor de infraestrutura.
- `webhooks/events.mdx` é gerado de `../server/services/publicApi/webhookEvents.js`: nunca editar à mão. Depois do catálogo, rodar o gerador e `npm run test:webhooks` no `server`.
- Página de endpoint: frontmatter; endpoint; escopo/plano; pré-condições; parâmetros; `curl` executável; resposta real; campos; erros. Sempre terminar com a tabela de erros.
- Exemplos usam `req_` + 16 hex, ObjectId de 24 hex, chave `sk_live_...` não plausível, ISO 8601 UTC e reais.

## Prova

`mint dev` quando MDX/layout precisar de preview; `mint broken-links` quando links ou navegação mudarem. Exemplo novo/alterado se confere contra o contrato real, sem chamar endpoint com efeito externo só para validar documentação.
