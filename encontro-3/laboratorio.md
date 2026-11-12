# Encontro 3 — Laboratórios

**Objetivo:** medir o que muda a saída de uma tarefa de QA: a formulação do pedido ou o contexto que o agente já tem.

**Onde:** tudo na aba **Code** do **Claude Desktop**. Hoje não há terminal.

**Regras do experimento:**

- **Um modelo para a turma toda: Sonnet 5.5.** Escolha no seletor de modelo, abaixo da caixa de prompt (Ctrl+Shift+I no Windows, Cmd+Shift+I no macOS). O padrão costuma ser o Opus: confira o seletor em cada sessão nova.
- **Uma sessão nova por execução:** botão **+ New** na barra lateral, ou Ctrl+N (Cmd+N no macOS). Uma conversa já usada muda o que o agente tem na janela.
- **Só o pedido muda.** O texto que você cola é sempre o mesmo; troca só o nome da formulação e o do arquivo de saída.
- **Modo Manual.** Quando o agente pedir para gravar em `saidas/`, leia e aprove. Se pedir qualquer outra coisa, como rodar um comando ou editar outro arquivo, rejeite.
- **F1 e F4 rodam duas vezes**, porque uma execução só não é evidência (E1).

---

## Antes de começar: abrir e conferir o caso

1. Na aba Code: **Local** → **Open folder…** → a pasta `caso-vitrine` do repositório da turma. Deixe **Worktree** desligado.
2. Confira que o caso já tem os arquivos do E3:
   - `prompts/formulacoes/` com F1.md a F4.md
   - `casos-de-teste/CT-US01.md`
   - `.claude/settings.json`

   A pasta `.claude` começa com ponto e pode não aparecer no explorador de arquivos. Se faltar algum arquivo, baixe o repositório de novo em [github.com/victorhwfreire/ia-para-qas-modulo-1](https://github.com/victorhwfreire/ia-para-qas-modulo-1) (botão **Code** → **Download ZIP**) e copie o que falta para a sua pasta.

   O `.claude/settings.json` contém:

   ```json
   {
     "autoMemoryEnabled": false
   }
   ```

   Ele desliga a memória automática do Claude Code neste projeto. Sem isso, o agente guarda anotações entre sessões e a comparação deixa de ser justa.
3. Copie o [registro](registro.md) para dentro da pasta do caso com o nome `registro-e3.md` e preencha lá.

---

## Laboratório 1 — Quatro formulações (19:45–20:36)

### Passo 1 — Sem IA · 6 min

Leia `historias/US-02-cancelar-pedido.md`. No registro, liste as regras e os critérios de aceite (são 8 itens) e as lacunas que você enxerga. Essa é a sua régua.

### Passo 2 — Rodar · 15 min

São seis execuções. Para cada uma, abra uma **sessão nova** na pasta do caso, confira o Sonnet 5.5 no seletor e cole **uma** linha abaixo:

```text
Leia prompts/formulacoes/F1.md e execute exatamente o pedido escrito nele. Grave a sua resposta completa, sem resumir, em saidas/e3-F1-a.md.
Leia prompts/formulacoes/F1.md e execute exatamente o pedido escrito nele. Grave a sua resposta completa, sem resumir, em saidas/e3-F1-b.md.
Leia prompts/formulacoes/F2.md e execute exatamente o pedido escrito nele. Grave a sua resposta completa, sem resumir, em saidas/e3-F2-a.md.
Leia prompts/formulacoes/F3.md e execute exatamente o pedido escrito nele. Grave a sua resposta completa, sem resumir, em saidas/e3-F3-a.md.
Leia prompts/formulacoes/F4.md e execute exatamente o pedido escrito nele. Grave a sua resposta completa, sem resumir, em saidas/e3-F4-a.md.
Leia prompts/formulacoes/F4.md e execute exatamente o pedido escrito nele. Grave a sua resposta completa, sem resumir, em saidas/e3-F4-b.md.
```

Pode deixar várias sessões rodando ao mesmo tempo. Na primeira gravação, a pasta `saidas/` ainda não existe: se o agente avisar isso, é esperado. Ele cria a pasta ao gravar; leia o pedido de permissão e aprove.

Enquanto roda, abra F1 a F4 e anote no registro o que muda de um para o outro.

**Se atrasar:** rode primeiro F1-a, F2-a, F3-a e F4-a; F1-b e F4-b, se der tempo.

### Passo 3 — Comparar · 22 min

Preencha no registro a ficha para cada uma das seis saídas:

| Medida | Como contar |
|---|---|
| Casos | Quantos casos de teste a saída tem. |
| Com origem | Quantos citam a regra ou o critério de onde vem o resultado esperado. |
| Inventados | Quantos dependem de regra que a US-02 não tem. Use a chave do E1: sustentado, inferido ou inventado. |
| Perguntas ao PO | Quantas lacunas viraram pergunta em vez de suposição. |
| Cobertura | Quantos dos 8 itens (R1 a R5, CA1 a CA3) aparecem em pelo menos um caso. |
| Aproveitável | Dá para usar sem retrabalho? Sim ou não. |
| Minutos de revisão | Quanto tempo você levou para conferir a saída. |

Sem tempo para as seis, compare uma saída de cada formulação e anote em uma linha a diferença entre F1-a e F1-b.

### Passo 4 — Painel · 4 min

Lance no painel da turma os números de cada saída.

### Passo 5 — Concluir · 4 min

No registro: o que, nas formulações, vale para **qualquer** tarefa da Vitrine e não só para derivar casos da US-02? Essa lista é a matéria-prima do laboratório 2.

---

## Laboratório 2 — Instruções do projeto (21:06–21:46)

### Passo 1 — Escrever · 13 min

Crie o arquivo `CLAUDE.md` na raiz da pasta do caso, a partir do [modelo](modelo-CLAUDE.md) e da sua conclusão do passo 5. Até 40 linhas.

Num editor de texto simples:

- **Bloco de Notas (Windows):** em **Salvar como**, escolha **Todos os arquivos (\*.\*)** no tipo, para o nome não virar `CLAUDE.md.txt`.
- **TextEdit (macOS):** antes de salvar, use **Formatar** → **Converter em Texto Simples**.

### Passo 2 — Conferir · 4 min

Abra uma sessão nova na pasta do caso e digite `/context all`. Procure o `CLAUDE.md` na lista **Memory files**. Se não aparecer, ele não está na janela: confira o nome e se ele está na raiz da pasta.

### Passo 3 — F1 com o arquivo · 13 min

Rode o F1, o pedido mais simples, duas vezes, agora com o `CLAUDE.md`. Cada linha numa sessão nova:

```text
Leia prompts/formulacoes/F1.md e execute exatamente o pedido escrito nele. Grave a sua resposta completa, sem resumir, em saidas/e3-F1-com-claude-md-a.md.
Leia prompts/formulacoes/F1.md e execute exatamente o pedido escrito nele. Grave a sua resposta completa, sem resumir, em saidas/e3-F1-com-claude-md-b.md.
```

Preencha a mesma ficha e compare com o F1 e com o F4 do laboratório 1.

### Passo 4 — Outra tarefa · 8 min

O arquivo `casos-de-teste/CT-US01.md` tem casos de teste da US-01 escritos por um colega. Numa sessão nova, peça a revisão numa linha só:

```text
Revise os casos de teste de casos-de-teste/CT-US01.md. Grave a revisão em saidas/e3-revisao-CT-US01.md.
```

Conte quantos problemas o agente apontou. Depois abra o CT-US01 e confira você mesmo, contra a US-01: o que ele achou e o que deixou passar?

### Passo 5 — Painel · 2 min

Lance os números do F1 com o arquivo e da revisão do CT-US01.

---

## Antes de sair

Confira que a pasta do caso tem `saidas/` com as saídas, o `CLAUDE.md` e o `registro-e3.md`.

Se quiser guardar no Git, peça numa sessão do Desktop na pasta do caso e aprove o comando:

```text
Faça o commit de todos os arquivos com a mensagem "e3".
```

Até domingo, 15/11, 23h59, envie no canal da turma, numa pasta com o seu nome, três arquivos de `saidas/`: `e3-F1-a.md`, `e3-F4-a.md` e `e3-F1-com-claude-md-a.md`. Eles são avaliados às cegas pelos colegas no encontro 4. A triagem revisada do E2 também volta no E4.

## Para aprofundar

- [Estudo dirigido do encontro 3](estudo-dirigido.pdf): os conceitos da aula e três práticas para fazer depois, no Desktop.
- [Prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices), guia da Anthropic.
- [Como o Claude Code lembra do projeto](https://code.claude.com/docs/en/memory): `CLAUDE.md`, memória automática e `/context all`.
- [Claude Code no Desktop](https://code.claude.com/docs/en/desktop): sessões, seletor de modelo e modos de permissão.
- [Why Language Models Hallucinate](https://arxiv.org/abs/2509.04664) (Kalai e outros, 2025): por que o modelo chuta quando não sabe.
