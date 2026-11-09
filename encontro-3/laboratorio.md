# Encontro 3 — Laboratórios

**Objetivo:** medir o que muda a saída de uma tarefa de QA: a formulação do pedido ou o contexto que o agente já tem.

**Regras do experimento:**

- Cada `claude -p` é uma chamada nova, sem memória das anteriores.
- Só o arquivo do pedido muda entre as execuções; o comando é sempre o mesmo.
- Cada formulação roda duas vezes, porque uma execução só não é evidência (E1).

---

## Antes da aula: atualizar o caso

Copie do canal da turma para dentro da sua pasta `caso-vitrine` os arquivos novos:

- `prompts/formulacoes/` (F1.md a F4.md)
- `casos-de-teste/CT-US01.md`
- `.claude/settings.json`

A pasta `.claude` começa com ponto e pode não aparecer no explorador de arquivos. Se faltar, crie num editor de texto um arquivo novo com o nome `.claude/settings.json` e este conteúdo:

```json
{
  "autoMemoryEnabled": false
}
```

Ele desliga a memória automática do Claude Code neste projeto. Sem isso, o agente guarda anotações entre sessões e a comparação deixa de ser justa. Depois:

```bash
git add .
git commit -m "arquivos do E3"
```

---

## Laboratório 1 — Quatro formulações (19:20–20:25)

### Passo 1 — Sem IA · 8 min

Leia `historias/US-02-cancelar-pedido.md`. No registro, liste as regras e os critérios de aceite (são 8 itens) e as lacunas que você enxerga. Essa é a sua régua.

### Passo 2 — Rodar · 17 min

Dentro da pasta do caso, rode o laço abaixo. Ele executa F1, F2, F3 e F4 duas vezes cada e grava cada resposta em `saidas/`. Enquanto roda, abra F1 a F4 e anote no registro o que muda de um para o outro.

**Windows (PowerShell):**

```powershell
[Console]::OutputEncoding = [Text.Encoding]::UTF8
New-Item -ItemType Directory -Force saidas | Out-Null
foreach ($f in 'F1','F2','F3','F4') {
  foreach ($r in 'a','b') {
    claude -p "Leia prompts/formulacoes/$f.md e execute exatamente o pedido escrito nele." --allowedTools Read | Out-File -Encoding utf8 "saidas/e3-$f-$r.md"
  }
}
```

**macOS ou Linux:**

```bash
mkdir -p saidas
for f in F1 F2 F3 F4; do
  for r in a b; do
    claude -p "Leia prompts/formulacoes/$f.md e execute exatamente o pedido escrito nele." --allowedTools Read > "saidas/e3-$f-$r.md"
  done
done
```

### Passo 3 — Comparar · 30 min

Preencha no registro a ficha para cada uma das oito saídas:

| Medida | Como contar |
|---|---|
| Casos | Quantos casos de teste a saída tem. |
| Com origem | Quantos citam a regra ou o critério de onde vem o resultado esperado. |
| Inventados | Quantos dependem de regra que a US-02 não tem. Use a chave do E1: sustentado, inferido ou inventado. |
| Perguntas ao PO | Quantas lacunas viraram pergunta em vez de suposição. |
| Cobertura | Quantos dos 8 itens (R1 a R5, CA1 a CA3) aparecem em pelo menos um caso. |
| Aproveitável | Dá para usar sem retrabalho? Sim ou não. |
| Minutos de revisão | Quanto tempo você levou para conferir a saída. |

Sem tempo para as oito, compare uma execução de cada formulação e anote em uma linha a diferença entre as execuções `a` e `b`.

### Passo 4 — Painel · 5 min

Lance no painel da turma os números de cada saída.

### Passo 5 — Concluir · 5 min

No registro: o que, nas formulações, vale para **qualquer** tarefa da Vitrine e não só para derivar casos da US-02? Essa lista é a matéria-prima do laboratório 2.

---

## Laboratório 2 — Instruções do projeto (20:59–21:44)

### Passo 1 — Escrever · 15 min

Crie o arquivo `CLAUDE.md` na raiz da pasta do caso, a partir do [modelo](modelo-CLAUDE.md) e da sua conclusão do passo 5. Até 40 linhas.

### Passo 2 — Conferir · 5 min

```bash
git add .
git commit -m "CLAUDE.md"
claude
```

Dentro da sessão, digite `/context all` e procure o `CLAUDE.md` na lista **Memory files**. Se não aparecer, ele não está na janela: confira o nome e se ele está na raiz da pasta. Saia com `/exit`.

### Passo 3 — F1 com o arquivo · 15 min

Rode o F1, o pedido mais simples, duas vezes, agora com o `CLAUDE.md`:

**Windows (PowerShell):**

```powershell
foreach ($r in 'a','b') {
  claude -p "Leia prompts/formulacoes/F1.md e execute exatamente o pedido escrito nele." --allowedTools Read | Out-File -Encoding utf8 "saidas/e3-F1-com-claude-md-$r.md"
}
```

**macOS ou Linux:**

```bash
for r in a b; do
  claude -p "Leia prompts/formulacoes/F1.md e execute exatamente o pedido escrito nele." --allowedTools Read > "saidas/e3-F1-com-claude-md-$r.md"
done
```

Preencha a mesma ficha e compare com o F1 e com o F4 do laboratório 1.

### Passo 4 — Outra tarefa · 8 min

O arquivo `casos-de-teste/CT-US01.md` tem casos de teste da US-01 escritos por um colega. Peça a revisão numa linha só:

**Windows (PowerShell):**

```powershell
claude -p "Revise os casos de teste de casos-de-teste/CT-US01.md." --allowedTools Read | Out-File -Encoding utf8 saidas/e3-revisao-CT-US01.md
```

**macOS ou Linux:**

```bash
claude -p "Revise os casos de teste de casos-de-teste/CT-US01.md." --allowedTools Read > saidas/e3-revisao-CT-US01.md
```

Conte quantos problemas o agente apontou. Depois abra o CT-US01 e confira você mesmo, contra a US-01: o que ele achou e o que deixou passar?

### Passo 5 — Painel · 2 min

Lance os números do F1 com o arquivo e da revisão do CT-US01.

---

## Antes de sair

```bash
git add .
git commit -m "e3"
```

Até domingo, 15/11, 23h59, envie no canal da turma, numa pasta com o seu nome, três arquivos de `saidas/`: `e3-F1-a.md`, `e3-F4-a.md` e `e3-F1-com-claude-md-a.md`. Eles são avaliados às cegas pelos colegas no encontro 4. A triagem revisada do E2 também volta no E4.

## Para aprofundar

- [Prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices), guia da Anthropic.
- [Como o Claude Code lembra do projeto](https://code.claude.com/docs/en/memory): `CLAUDE.md`, memória automática e `/context all`.
