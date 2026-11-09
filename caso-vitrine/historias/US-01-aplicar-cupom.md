# US-01 — Aplicar cupom de desconto no checkout

**Como** cliente da Vitrine, **quero** informar um cupom de desconto no checkout **para** pagar menos pelo meu pedido.

Time: Checkout · Prioridade: alta

## Regras de negócio

- **R1.** O cupom é um código de 6 a 12 caracteres, formado por letras e números.
- **R2.** Cada cupom concede desconto percentual, entre 5% e 50%, ou desconto de valor fixo em reais.
- **R3.** O desconto incide sobre o valor dos produtos. O frete não recebe desconto.
- **R4.** Cada cupom tem data de validade. Depois dela, o cupom é recusado com a mensagem "Cupom expirado".
- **R5.** Alguns cupons exigem um valor mínimo de pedido.
- **R6.** Só um cupom pode ser aplicado por pedido.

## Critérios de aceite

- **CA1.** Dado um carrinho com R$ 200,00 em produtos e frete de R$ 20,00, quando aplico o cupom BEMVINDO10 (10%), então o desconto é de R$ 20,00 e o total do pedido é R$ 200,00.
- **CA2.** Dado um cupom com validade vencida, quando aplico, então vejo a mensagem "Cupom expirado" e o total não muda.
- **CA3.** Dado um pedido com um cupom aplicado, quando aplico outro cupom válido, então o novo cupom substitui o anterior.

## Fora do escopo

Criação e gestão de cupons pelo time de marketing.
