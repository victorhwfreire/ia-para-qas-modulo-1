# Caso Vitrine

A Vitrine é uma loja online fictícia, criada para o curso IA para QA. Nenhum conteúdo desta pasta vem de cliente ou de projeto real.

## A loja

- Loja online de casa e decoração, com site e app para Android e iOS.
- Meios de pagamento: cartão de crédito, Pix e boleto.
- Status de um pedido, nesta ordem: **Aguardando pagamento → Pago → Em separação → Enviado → Entregue**. Um pedido também pode passar para **Cancelado**.
- Cupons de desconto são criados pelo time de marketing e aplicados pelo cliente no checkout.

## Conteúdo

| Arquivo | O que tem | Usado em |
|---|---|---|
| [historias/US-01-aplicar-cupom.md](historias/US-01-aplicar-cupom.md) | Aplicar cupom de desconto no checkout | E1, demonstração |
| [historias/US-02-cancelar-pedido.md](historias/US-02-cancelar-pedido.md) | Cancelar pedido pelo app | a partir do E2 |
| [bugs/BUG-101.md](bugs/BUG-101.md) | Cupom percentual também desconta o frete | E1, demonstração; E2 |
| [bugs/](bugs/) BUG-102 a BUG-108 | Oito bugs de cupom e de cancelamento, com o BUG-101, para triagem | E2, demonstração e laboratório |
| [bugs/BUG-109.md](bugs/BUG-109.md) | Cupom aceito abaixo do valor mínimo | E2, triagem pelo terminal |
| [criterios-de-severidade.md](criterios-de-severidade.md) | Como a Vitrine classifica a severidade de um bug | E1, E2 e E3 |
| [prompts/triagem.md](prompts/triagem.md) | Prompt versionado da triagem de bugs | E2 |
| [prompts/formulacoes/](prompts/formulacoes/F1.md) F1 a F4 | Quatro formulações da mesma tarefa: derivar casos de teste da US-02 | E3, laboratório 1 |
| [casos-de-teste/CT-US01.md](casos-de-teste/CT-US01.md) | Casos de teste da US-01 escritos por um colega, enviados para revisão | E3, laboratório 2 |
| `.claude/settings.json` | Desliga a memória automática do Claude Code neste projeto, para que as comparações com e sem instruções sejam justas | E3 em diante |

O caso cresce a cada encontro: os próximos acrescentam casos de teste, bugs e as instruções do projeto.
