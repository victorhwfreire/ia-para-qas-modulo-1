# Casos de teste — US-01, aplicar cupom de desconto

Escritos por um colega do time e enviados para revisão.

| ID | Pré-condição | Ação | Resultado esperado | Origem | Tipo |
|---|---|---|---|---|---|
| CT-01 | Carrinho com R$ 200,00 em produtos e frete de R$ 20,00 | Aplicar o cupom BEMVINDO10 (10%) | Desconto de R$ 20,00; total de R$ 200,00 | US-01 R3, CA1 | positivo |
| CT-02 | Cupom com validade vencida | Aplicar o cupom | Mensagem "Cupom expirado"; total não muda | US-01 R4, CA2 | negativo |
| CT-03 | Carrinho com produtos | Aplicar um cupom com 13 caracteres | Mensagem "Cupom inválido" | US-01 R1 | borda |
| CT-04 | Cliente já usou o cupom BEMVINDO10 em outro pedido | Aplicar BEMVINDO10 de novo, com o mesmo CPF | Cupom recusado: "Cupom já utilizado" | US-01 R6 | negativo |
| CT-05 | Carrinho com R$ 200,00 em produtos e frete de R$ 20,00 | Aplicar um cupom de 10% | Desconto de R$ 22,00; total de R$ 198,00 | US-01 R2 | positivo |
| CT-06 | Pedido com um cupom válido aplicado | Aplicar outro cupom válido | O novo cupom substitui o anterior | US-01 R6, CA3 | positivo |
| CT-07 | Cupom que exige valor mínimo de pedido | Aplicar o cupom | Verificar o comportamento | US-01 R5 | negativo |
| CT-08 | Cupom com data de validade no passado | Tentar aplicar o cupom no checkout | Cupom rejeitado com a mensagem "Cupom expirado" | US-01 R4 | negativo |
