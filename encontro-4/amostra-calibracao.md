# Amostra de calibração — casos de teste da US-02

**Saída construída pelo professor para calibrar rubricas; não foi gerada por um modelo.** Tem problemas conhecidos, de propósito. Use-a só no passo 2 do laboratório 1: cada pessoa da dupla avalia sozinha e depois as duas comparam as notas.

Pedido que teria gerado esta saída: derivar os casos de teste funcionais da US-02, citando a origem de cada resultado esperado.

| ID | Pré-condição | Ação | Resultado esperado | Origem | Tipo |
|---|---|---|---|---|---|
| CT-01 | Pedido com status "Aguardando pagamento" | Cliente toca em "Cancelar pedido", escolhe um motivo e confirma | Status muda para "Cancelado"; nenhum estorno é gerado | US-02 R1, CA1 | positivo |
| CT-02 | Pedido "Pago" com cartão de crédito | Cliente cancela, escolhendo um motivo | Estorno solicitado no mesmo cartão | US-02 R3, CA2 | positivo |
| CT-03 | Pedido com status "Em separação" | Cliente abre a tela do pedido | O botão "Cancelar pedido" não aparece | US-02 R2, CA3 | negativo |
| CT-04 | Pedido "Pago" com Pix | Cliente cancela, escolhendo um motivo | Estorno via Pix em até 7 dias úteis | US-02 R3 | positivo |
| CT-05 | Pedido "Pago" | Cliente toca em "Cancelar pedido" e não escolhe motivo | O botão de confirmar fica desabilitado | US-02 R4 | negativo |
| CT-06 | Pedido "Pago" em que foi usado um cupom | Cliente cancela o pedido | O cupom volta a valer para uma nova compra | | positivo |
| CT-07 | Pedido com status "Enviado" | Cliente liga para a central de atendimento | A central cancela o pedido | US-02 R2 | positivo |
| CT-08 | Pedido "Pago" com cartão de crédito | Cliente cancela, escolhendo um motivo | Status muda para "Cancelado" | US-02 R5 | positivo |

**Perguntas ao PO**

1. Como estornar um pedido pago com boleto?
2. O valor do frete também é estornado?
