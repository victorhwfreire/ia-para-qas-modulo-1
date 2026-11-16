# Encontro 4 — Laboratórios

**Objetivo:** medir quanto do que a IA gerou e executou sobrevive à revisão de um QA.

**Hoje a aula é toda prática**, com Marlon e Eric Araujo:

- **Laboratórios 1 e 2 (sem IA):** vocês escrevem uma rubrica e avaliam às cegas as saídas do E3 dos colegas.
- **Rodada de testes (no Google Chrome):** o Claude in Chrome executa casos de teste numa loja de homologação, e vocês conferem o que ele disse.

---

## Antes da aula

### Até domingo, 15/11, 23h59 — enviar as suas saídas do E3

No canal da turma, numa pasta com o seu nome, envie estes três arquivos da sua pasta `saidas/`:

- `e3-F1-a.md`
- `e3-F4-a.md`
- `e3-F1-com-claude-md-a.md`

Confira que eles não têm o seu nome no texto. Quem não enviar avalia normalmente, só não terá saída avaliada.

### Segunda, 16/11, antes da aula — receber os seus códigos

Você recebe no canal saídas com códigos (por exemplo `S07.md`) e a lista dos **três códigos** que você vai avaliar. Você não sabe de quem são nem como foram pedidas. Copie esses três arquivos para uma pasta `avaliacao/` dentro da sua pasta do caso.

Copie também o [registro](registro.md) para dentro da pasta do caso, com o nome `registro-e4.md`, e preencha lá.

### Até 20h33 — instalar o Claude in Chrome

1. Use o **Google Chrome de computador**. A extensão não roda em outros navegadores Chromium nem no celular.
2. Instale a extensão **Claude in Chrome** pela Chrome Web Store e entre com a sua conta paga (Pro ou superior).
3. Teste: o ícone da extensão, na barra do Chrome, abre um painel ao lado da página.

Sem a extensão funcionando? Faça a rodada em dupla com quem tem.

---

## Laboratório 1 — Rubrica (19:05–19:30)

Em dupla. Sem IA.

### Passo 1 — Escrever · 12 min

A partir do [modelo](modelo-rubrica.md) e da ficha do E3, escrevam uma rubrica para **casos de teste derivados de uma história de usuário**: 4 ou 5 critérios, níveis 0, 1 e 2, e a evidência que justifica cada nível. Cada nível diz o que se vê na saída.

### Passo 2 — Calibrar · 10 min

Cada pessoa da dupla aplica a rubrica à [amostra de calibração](amostra-calibracao.md), **sozinha e sem conversar**. Anote no registro. Depois comparem as notas critério a critério.

### Passo 3 — Ajustar · 3 min

Reescrevam o critério em que as notas mais divergiram. Salvem a rubrica como `rubrica.md` na raiz da pasta do caso.

- **Bloco de Notas (Windows):** em **Salvar como**, escolha **Todos os arquivos (\*.\*)** no tipo, para o nome não virar `rubrica.md.txt`.
- **TextEdit (macOS):** antes de salvar, use **Formatar** → **Converter em Texto Simples**.

---

## Laboratório 2 — Avaliação cega (19:30–20:13)

Sem IA. Para **cada** uma das suas três saídas, 12 minutos:

1. Aplique a rubrica: um nível por critério, com a evidência.
2. Marque cada caso de teste: **A** (aceito sem mudança), **C** (aceito com correção) ou **R** (rejeitado).
3. Anote os minutos que levou para revisar e quantos minutos você levaria para escrever aqueles casos à mão.

Depois, no registro, calcule para cada saída:

- **Aproveitamento direto** = A ÷ total de casos
- **Aproveitamento com correção** = (A + C) ÷ total de casos
- **Ganho real** = minutos à mão − minutos de revisão e correção

Lance no painel uma linha por código.

---

## Rodada de testes com o Claude in Chrome (20:45–21:42)

Em dupla. O Claude executa casos de teste numa loja; vocês decidem se cada caso passou.

**A loja:** https://victorhwfreire.github.io/ia-para-qas-modulo-1/loja-vitrine/

É a loja Vitrine em homologação: fictícia, sem pagamento. O botão “Esvaziar carrinho” também remove a entrega e o cupom. A régua é a US-01 (`caso-vitrine/historias/US-01-aplicar-cupom.md`).

### Passo 1 — Preparar · 10 min

1. Abra a loja no Chrome.
2. Abra o Claude in Chrome pelo ícone da extensão. O painel abre ao lado da página.
3. No seletor do campo de mensagem, escolha o modo **Perguntar antes de agir**. Não use o modo **Agir sem perguntar**.

### Passo 2 — Executar · 25 min

Cole no painel o pedido abaixo, **sem mudar nada**:

```text
Você é analista de QA da Vitrine e vai testar a loja aberta nesta aba. É um ambiente de homologação de uma loja fictícia: não há pagamento e nada é comprado.

Contexto: a regra de negócio é a história US-01, abaixo. Ela é a única fonte de regra.

US-01 · Aplicar cupom de desconto no checkout
R1. O cupom é um código de 6 a 12 caracteres, formado por letras e números.
R2. Cada cupom concede desconto percentual, entre 5% e 50%, ou desconto de valor fixo em reais.
R3. O desconto incide sobre o valor dos produtos. O frete não recebe desconto.
R4. Cada cupom tem data de validade. Depois dela, o cupom é recusado com a mensagem "Cupom expirado".
R5. Alguns cupons exigem um valor mínimo de pedido.
R6. Só um cupom pode ser aplicado por pedido.
CA1. Carrinho com R$ 200,00 em produtos e frete de R$ 20,00, cupom BEMVINDO10 (10%): desconto de R$ 20,00 e total de R$ 200,00.
CA2. Cupom vencido: mensagem "Cupom expirado" e o total não muda.
CA3. Com um cupom aplicado, aplicar outro cupom válido: o novo substitui o anterior.

Tarefa: execute os casos de teste abaixo, um por vez. Antes de cada caso, clique em "Esvaziar carrinho".

CT01 (R3, CA1). Adicione 2 unidades de "Luminária de mesa Aurora". Escolha a entrega "Padrão". Aplique o cupom BEMVINDO10. Esperado: desconto de R$ 20,00 e total de R$ 200,00.
CT02 (R5). Adicione 1 unidade de "Vaso de cerâmica Terra". Escolha a entrega "Econômica". Aplique o cupom MINIMO50 (R$ 10,00 de desconto, exige pedido mínimo de R$ 50,00). Esperado: o cupom é recusado; desconto de R$ 0,00 e total de R$ 45,00.
CT03 (R4, CA2). Adicione 1 unidade de "Luminária de mesa Aurora". Escolha a entrega "Padrão". Aplique o cupom VERAO2025 (validade encerrada em 31/03/2026). Esperado: mensagem "Cupom expirado" e total de R$ 120,00, sem mudança.
CT04 (CA3). Adicione 2 unidades de "Luminária de mesa Aurora". Escolha a entrega "Padrão". Aplique o cupom BEMVINDO10 e, em seguida, o cupom DESC30 (R$ 30,00 de desconto fixo). Esperado: DESC30 substitui BEMVINDO10; desconto de R$ 30,00 e total de R$ 190,00.
CT05 (R1). Adicione 1 unidade de "Luminária de mesa Aurora". Escolha a entrega "Padrão". Aplique o cupom bemvindo10, em letras minúsculas. Esperado: o cupom é aceito, como acontece com BEMVINDO10.
CT06 (R2, R3). Adicione 1 unidade de "Luminária de mesa Aurora". Escolha a entrega "Padrão". Aplique o cupom MINIMO50 (R$ 10,00 de desconto fixo, mínimo de R$ 50,00). Esperado: desconto de R$ 10,00 e total de R$ 110,00.

Restrições:
- Use só a US-01. Não use regra que não esteja escrita nela.
- Se o resultado esperado de um caso depender de algo que a US-01 não define, não marque como falha: marque "Lacuna" e escreva a pergunta para o PO.
- Não vá para pagamento e não mexa em nada fora do carrinho.

Como responder: ao final, uma tabela com as colunas Caso | Status (Passou, Falhou, Lacuna ou Bloqueado) | Esperado | Obtido (copie da tela a mensagem do cupom e os valores de Desconto e Total) | Regra. Depois da tabela, liste os possíveis defeitos com os passos para reproduzir.
```

- O Claude mostra um plano. Leia e aprove se ele só mexe na loja.
- Se ele pedir confirmação para uma ação fora da loja, negue.
- Acompanhe a aba enquanto ele trabalha. Você pode interromper.
- Quando ele terminar, copie para o registro o status e os valores de cada caso.

### Passo 3 — Conferir · 15 min

Para cada caso da tabela do Claude, abra a US-01 e confira:

- O status (Passou, Falhou ou Lacuna) confere com a história?
- Os valores que ele copiou estão na tela? Se tiver dúvida, refaça o caso à mão na loja.

Marque no registro:

- **A:** veredito aceito sem mudança.
- **C:** veredito corrigido (por exemplo, status errado com valores certos).
- **R:** veredito rejeitado (a leitura não confere com a tela).

Lacuna não é bug: ela vira pergunta ao PO. Uma falha só vira bug depois de refeita à mão.

### Passo 4 — Painel · 7 min

**Aproveitamento da execução** = vereditos A ÷ 6. Lance no painel: a dupla, A ÷ 6 e o caso em que vocês mais discordaram do Claude.

---

## Antes de sair

Confira que a pasta do caso tem `rubrica.md` e o `registro-e4.md` preenchido.

Se quiser guardar no Git, peça numa sessão do Claude Desktop na pasta do caso e aprove o comando:

```text
Faça o commit de todos os arquivos com a mensagem "e4".
```

Responda o formulário de feedback do módulo, no canal da turma.

## Para aprofundar

- [Estudo dirigido do encontro 4](estudo-dirigido.pdf): os conceitos da aula e três práticas para fazer depois, no Desktop. O juiz automático e a escolha de modelo, que não entraram na aula, estão nas práticas 2 e 3.
- [Get started with Claude in Chrome](https://support.claude.com/en/articles/12012173-get-started-with-claude-in-chrome), central de ajuda da Anthropic.
- [Claude in Chrome permissions guide](https://support.claude.com/en/articles/12902446-claude-in-chrome-permissions-guide): os modos de permissão.
- Zheng, L. et al. [Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena](https://arxiv.org/abs/2306.05685). NeurIPS 2023.
