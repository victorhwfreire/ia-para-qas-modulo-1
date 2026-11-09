# US-02 — Cancelar pedido pelo app

**Como** cliente da Vitrine, **quero** cancelar um pedido pelo app **para** não receber uma compra da qual desisti.

Time: Pós-venda · Prioridade: média

## Regras de negócio

- **R1.** O botão "Cancelar pedido" aparece na tela do pedido enquanto ele estiver com status "Aguardando pagamento" ou "Pago".
- **R2.** A partir do status "Em separação", o cancelamento só pode ser pedido à central de atendimento.
- **R3.** Ao cancelar um pedido "Pago", o valor é estornado no mesmo meio de pagamento usado na compra.
- **R4.** Para cancelar, o cliente escolhe um motivo numa lista.
- **R5.** Ao concluir o cancelamento, o status muda para "Cancelado" e o cliente recebe um e-mail de confirmação.

## Critérios de aceite

- **CA1.** Dado um pedido "Aguardando pagamento", quando o cliente cancela, então o status muda para "Cancelado" e nenhum estorno é gerado.
- **CA2.** Dado um pedido "Pago" com cartão de crédito, quando o cliente cancela, então o estorno é solicitado no mesmo cartão.
- **CA3.** Dado um pedido "Em separação", quando o cliente abre a tela do pedido, então o botão "Cancelar pedido" não aparece.
