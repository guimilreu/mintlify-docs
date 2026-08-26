# Documentação da API SocialSell

Site Mintlify da API pública v1. Páginas são MDX com frontmatter YAML; a configuração vive em `docs.json`.

- `mint dev` — preview local
- `mint broken-links` — checagem de links

## Idioma e voz

- **Tudo em pt-BR.** Títulos, corpo, tabelas e comentários de exemplo.
- **Títulos em Title Case** ("Enviar mensagem", "Limites e cotas"), como o restante do site.
- Segunda pessoa ("você"), voz ativa, uma ideia por frase.
- Nomes de campo, código, rota e arquivo em `código`. Elementos de interface em **negrito**.

## Vocabulário obrigatório

| Use | Nunca use |
|---|---|
| **WhatsApp Oficial** (canal via Meta Cloud API) | "Cloud API" sozinho como nome de canal |
| **WhatsApp por QR Code** (canal não-oficial) | **Evolution**, "não-oficial", "fork" |
| **modelo** (mensagem aprovada pela Meta) | "template" no corpo do texto — o campo da API é `template_name`, esse mantém |
| **número** do WhatsApp | "instância", exceto quando for o nome literal do campo |
| **funil** | "pipeline" no corpo do texto — o recurso na API é `/pipelines` |
| **disparo** | "broadcast" no corpo do texto |
| **Desenvolvedores** (aba do painel) | "Developers" |

`Evolution` é o nome de um projeto de terceiro e não aparece em documentação pública da SocialSell em nenhuma hipótese.

## Regra de ouro: a doc segue o código

Todo exemplo publicado precisa funcionar **como está escrito**. Antes de documentar um endpoint:

1. Leia o router em `server/routes/public/v1/`
2. Leia o schema Zod, quando houver — é ele que define obrigatoriedade, enums e limites
3. Leia o formatter da resposta, não o model — o shape público quase nunca é o do banco
4. Valide o exemplo contra o schema real antes de publicar

Campo que a doc promete e o código não entrega é bug de documentação, não licença poética.

## Referência de webhooks é gerada

`webhooks/events.mdx` é **gerado** a partir de `server/services/publicApi/webhookEvents.js`.

- **Nunca edite esse arquivo à mão.**
- Depois de mexer no catálogo: `node scripts/ops/generate-webhook-docs.js --write`
- `npm run test:webhooks` falha se o arquivo ficar para trás

## Estrutura de uma página de endpoint

Nesta ordem, omitindo o que não se aplica:

1. Frontmatter (`title`, `description`)
2. `## Endpoint` com método e caminho
3. Escopo necessário, e restrição de plano quando houver
4. Pré-condições de status, em `<Note>` ou `<Warning>`
5. Parâmetros de query ou corpo, em tabela
6. Exemplo `curl` completo e executável
7. Exemplo de resposta real
8. Tabela do objeto de resposta
9. `## Erros` — tabela com código, status e descrição

Toda página de endpoint termina com a tabela de erros. Erro não documentado é erro que o integrador descobre em produção.

## Convenções de exemplo

- `request_id` no formato real: `req_` + 16 caracteres hexadecimais
- IDs no formato ObjectId de 24 caracteres hex
- Chave de API sempre como `sk_live_...`, nunca um valor plausível
- Datas em ISO 8601 com fuso UTC
- Valores monetários em reais

## O que não documentar

- Rotas internas do painel (`/api/...` fora de `/api/v1`)
- Módulo de administração
- Detalhes de implementação: nome de coleção, índice, fila, provedor de infraestrutura
