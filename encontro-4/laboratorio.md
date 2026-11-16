# Encontro 4 — Laboratórios

**Objetivo:** medir quanto do que a IA gerou sobrevive a uma revisão de QA sênior, e a que custo.

**Onde:** tudo na aba **Code** do **Claude Desktop**, como no E3. Hoje também não há terminal.

**Regras dos laboratórios com IA (3 e 4):**

- **Uma sessão nova para cada pedido:** botão **+ New** na barra lateral, ou Ctrl+N (Cmd+N no macOS). Uma conversa já usada muda o que o agente tem na janela.
- **Modelo:** no laboratório 3, **Sonnet 5.5**; no laboratório 4, o modelo que o passo pedir. Escolha no seletor de modelo, abaixo da caixa de prompt (Ctrl+Shift+I no Windows, Cmd+Shift+I no macOS). Confira o seletor em cada sessão nova.
- **Modo Manual.** Quando o agente pedir para gravar em `saidas/`, leia e aprove. Se pedir qualquer outra coisa, como rodar um comando ou editar outro arquivo, rejeite.

---

## Antes da aula

### Até domingo, 15/11, 23h59 — enviar as suas saídas do E3

No canal da turma, numa pasta com o seu nome, envie estes três arquivos da sua pasta `saidas/`:

- `e3-F1-a.md`
- `e3-F4-a.md`
- `e3-F1-com-claude-md-a.md`

Confira que eles não têm o seu nome no texto. Quem não enviar avalia normalmente, só não terá saída avaliada.

### Segunda, 16/11, antes da aula — receber os seus códigos

O professor publica no canal saídas com códigos (por exemplo `S07.md`) e manda a você a lista dos **três códigos** que você vai avaliar. Você não sabe de quem são nem como foram pedidas. Copie esses três arquivos para uma pasta `avaliacao/` dentro da sua pasta do caso.

Copie também o [registro](registro.md) para dentro da pasta do caso, com o nome `registro-e4.md`, e preencha lá.

---

## Laboratório 1 — Rubrica (19:14–19:39)

Em dupla. Sem IA.

### Passo 1 — Escrever · 12 min

A partir do [modelo](modelo-rubrica.md) e da ficha do E3, escrevam uma rubrica para **casos de teste derivados de uma história de usuário**: 4 ou 5 critérios, níveis 0, 1 e 2, e a evidência que justifica cada nível.

### Passo 2 — Calibrar · 10 min

Cada pessoa da dupla aplica a rubrica à [amostra de calibração](amostra-calibracao.md), **sozinha e sem conversar**. Anote no registro. Depois comparem as notas critério a critério.

### Passo 3 — Ajustar · 3 min

Reescrevam o critério em que as notas mais divergiram. Salvem a rubrica como `rubrica.md` na raiz da pasta do caso.

- **Bloco de Notas (Windows):** em **Salvar como**, escolha **Todos os arquivos (\*.\*)** no tipo, para o nome não virar `rubrica.md.txt`.
- **TextEdit (macOS):** antes de salvar, use **Formatar** → **Converter em Texto Simples**.

---

## Laboratório 2 — Avaliação cega (19:44–20:27)

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

## Laboratório 3 — O Claude Code como juiz (21:01–21:18)

Sonnet 5.5. Troque `S03`, `S11` e `S17` pelos seus três códigos.

### Passo 1 — Juiz · 7 min

Para cada código, abra uma **sessão nova** na pasta do caso e cole **uma** linha abaixo. Pode deixar as três sessões rodando ao mesmo tempo.

```text
Leia rubrica.md e avalie a saída avaliacao/S03.md com essa rubrica. Para cada critério, dê o nível e cite o trecho da saída que o justifica. Responda só com uma tabela: critério, nível, trecho. Grave a tabela em saidas/e4-juiz-S03.md.
Leia rubrica.md e avalie a saída avaliacao/S11.md com essa rubrica. Para cada critério, dê o nível e cite o trecho da saída que o justifica. Responda só com uma tabela: critério, nível, trecho. Grave a tabela em saidas/e4-juiz-S11.md.
Leia rubrica.md e avalie a saída avaliacao/S17.md com essa rubrica. Para cada critério, dê o nível e cite o trecho da saída que o justifica. Responda só com uma tabela: critério, nível, trecho. Grave a tabela em saidas/e4-juiz-S17.md.
```

### Passo 2 — Concordância · 5 min

No registro, compare critério a critério o nível do juiz com o seu. Conte as concordâncias. Onde discordaram, abra a saída: quem tem o trecho que sustenta melhor o nível?

### Passo 3 — Teste de posição · 5 min

Escolha duas das suas saídas. Pergunte qual é melhor; depois troque a ordem e pergunte de novo. **Cada pergunta numa sessão nova:**

```text
Leia rubrica.md e as saídas avaliacao/S03.md (saída A) e avaliacao/S11.md (saída B). Usando a rubrica, qual é melhor? Responda só com A ou B e uma frase.
Leia rubrica.md e as saídas avaliacao/S11.md (saída A) e avaliacao/S03.md (saída B). Usando a rubrica, qual é melhor? Responda só com A ou B e uma frase.
```

Se ele escolheu o **mesmo arquivo** nas duas vezes, foi consistente. Se escolheu a **mesma posição** (A e A, ou B e B), apareceu o viés de posição.

---

## Laboratório 4 — A mesma triagem com dois modelos (21:23–21:38)

### Passo 1 — Rodar · 6 min

Abra **duas sessões novas** na pasta do caso: numa, escolha o **Haiku** no seletor de modelo; na outra, o **Sonnet 5.5**. Cole nas duas o mesmo pedido:

```text
Faça a triagem de bugs/BUG-102.md, bugs/BUG-107.md e bugs/BUG-108.md seguindo prompts/triagem.md. Mostre só a tabela.
```

Use o cronômetro do celular: comece ao apertar Enter e pare quando a tabela terminar. Anote os segundos de cada modelo.

- **O Haiku não aparece no seletor?** Digite `/model haiku` na sessão. Se não funcionar, compare o Sonnet com o **Opus**.
- **Com tempo sobrando:** rode também com o Opus.

### Passo 2 — Qualidade · 6 min

Compare as três linhas de cada modelo com a **sua triagem revisada do E2** (`triagem/relatorio.md`). Quantas você aceitaria sem mudança? Quem não fez o E2 compara com a triagem revisada de um colega.

O custo não aparece no Desktop para quem usa assinatura. Para comparar, use a tabela de preços da API mostrada no slide: o Sonnet custa cerca de 20 vezes o Haiku por token.

### Passo 3 — Painel · 3 min

Lance: modelo, segundos e linhas aceitas.

---

## Antes de sair

Confira que a pasta do caso tem `rubrica.md`, o `registro-e4.md` e, em `saidas/`, as tabelas do juiz.

Se quiser guardar no Git, peça numa sessão do Desktop na pasta do caso e aprove o comando:

```text
Faça o commit de todos os arquivos com a mensagem "e4".
```

Responda o formulário de feedback do módulo, no canal da turma.

## Para aprofundar

- [Estudo dirigido do encontro 4](estudo-dirigido.pdf): os conceitos da aula e três práticas para fazer depois, no Desktop.
- Zheng, L. et al. [Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena](https://arxiv.org/abs/2306.05685). NeurIPS 2023.
- [Configuração de modelo no Claude Code](https://code.claude.com/docs/en/model-config): seletor, `/model` e apelidos `haiku`, `sonnet` e `opus`.
- [Claude Code no Desktop](https://code.claude.com/docs/en/desktop): sessões, seletor de modelo e modos de permissão.
- [Custos no Claude Code](https://code.claude.com/docs/en/costs): o que o `/usage` mostra para quem usa assinatura.
