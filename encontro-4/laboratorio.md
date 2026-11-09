# Encontro 4 — Laboratórios

**Objetivo:** medir quanto do que a IA gerou sobrevive a uma revisão de QA sênior, e a que custo.

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

---

## Laboratório 1 — Rubrica (19:09–19:34)

Em dupla.

### Passo 1 — Escrever · 12 min

A partir do [modelo](modelo-rubrica.md) e da ficha do E3, escrevam uma rubrica para **casos de teste derivados de uma história de usuário**: 4 ou 5 critérios, níveis 0, 1 e 2, e a evidência que justifica cada nível.

### Passo 2 — Calibrar · 10 min

Cada pessoa da dupla aplica a rubrica à [amostra de calibração](amostra-calibracao.md), **sozinha e sem conversar**. Anote no registro. Depois comparem as notas critério a critério.

### Passo 3 — Ajustar · 3 min

Reescrevam o critério em que as notas mais divergiram. Salvem a rubrica como `rubrica.md` na raiz da pasta do caso.

---

## Laboratório 2 — Avaliação cega (19:37–20:20)

Para **cada** uma das suas três saídas, 12 minutos:

1. Aplique a rubrica: um nível por critério, com a evidência.
2. Marque cada caso de teste: **A** (aceito sem mudança), **C** (aceito com correção) ou **R** (rejeitado).
3. Anote os minutos que levou para revisar e quantos minutos você levaria para escrever aqueles casos à mão.

Depois, no registro, calcule para cada saída:

- **Aproveitamento direto** = A ÷ total de casos
- **Aproveitamento com correção** = (A + C) ÷ total de casos
- **Ganho real** = minutos à mão − minutos de revisão e correção

Lance no painel uma linha por código.

---

## Laboratório 3 — O Claude Code como juiz (20:43–21:05)

Troque `S03`, `S11` e `S17` pelos seus três códigos.

### Passo 1 — Juiz · 8 min

**Windows (PowerShell):**

```powershell
[Console]::OutputEncoding = [Text.Encoding]::UTF8
foreach ($c in 'S03','S11','S17') {
  claude -p "Leia rubrica.md e avalie a saída avaliacao/$c.md com essa rubrica. Para cada critério, dê o nível e cite o trecho da saída que o justifica. Responda só com uma tabela: critério, nível, trecho." --allowedTools Read | Out-File -Encoding utf8 "saidas/e4-juiz-$c.md"
}
```

**macOS ou Linux:**

```bash
for c in S03 S11 S17; do
  claude -p "Leia rubrica.md e avalie a saída avaliacao/$c.md com essa rubrica. Para cada critério, dê o nível e cite o trecho da saída que o justifica. Responda só com uma tabela: critério, nível, trecho." --allowedTools Read > "saidas/e4-juiz-$c.md"
done
```

### Passo 2 — Concordância · 7 min

No registro, compare critério a critério o nível do juiz com o seu. Conte as concordâncias. Onde discordaram, quem tem a melhor evidência?

### Passo 3 — Teste de posição · 7 min

Escolha duas das suas saídas. Pergunte qual é melhor; depois troque a ordem e pergunte de novo:

```bash
claude -p "Leia rubrica.md e as saídas avaliacao/S03.md (saída A) e avaliacao/S11.md (saída B). Usando a rubrica, qual é melhor? Responda só com A ou B e uma frase." --allowedTools Read
claude -p "Leia rubrica.md e as saídas avaliacao/S11.md (saída A) e avaliacao/S03.md (saída B). Usando a rubrica, qual é melhor? Responda só com A ou B e uma frase." --allowedTools Read
```

Se ele escolheu o **mesmo arquivo** nas duas vezes, foi consistente. Se escolheu a **mesma posição** (A e A, ou B e B), apareceu o viés de posição.

---

## Laboratório 4 — A mesma triagem com dois modelos (21:08–21:30)

### Passo 1 — Rodar · 8 min

**Windows (PowerShell):**

```powershell
[Console]::OutputEncoding = [Text.Encoding]::UTF8
$tri = 'Faça a triagem de bugs/BUG-102.md, bugs/BUG-107.md e bugs/BUG-108.md seguindo prompts/triagem.md. Mostre só a tabela.'
foreach ($m in 'haiku','sonnet') {
  $t = Measure-Command { claude -p $tri --model $m --allowedTools Read --output-format json | Out-File -Encoding utf8 "saidas/e4-modelo-$m.json" }
  "{0}: {1:N0} s" -f $m, $t.TotalSeconds
}
```

**macOS ou Linux:**

```bash
tri='Faça a triagem de bugs/BUG-102.md, bugs/BUG-107.md e bugs/BUG-108.md seguindo prompts/triagem.md. Mostre só a tabela.'
for m in haiku sonnet; do
  ini=$(date +%s)
  claude -p "$tri" --model "$m" --allowedTools Read --output-format json > "saidas/e4-modelo-$m.json"
  echo "$m: $(( $(date +%s) - ini )) s"
done
```

Anote os segundos de cada modelo. Com tempo sobrando, acrescente `opus` à lista.

### Passo 2 — Custo e resultado · 4 min

**Windows (PowerShell):**

```powershell
foreach ($m in 'haiku','sonnet') {
  $r = Get-Content "saidas/e4-modelo-$m.json" -Raw | ConvertFrom-Json
  "== $m · custo estimado: US$ $($r.total_cost_usd)"
  $r.result
}
```

**macOS ou Linux:**

```bash
for m in haiku sonnet; do
  python3 -c "import json,sys; d=json.load(open(sys.argv[1], encoding='utf-8-sig')); print('==', sys.argv[2], '· custo estimado: US$', d.get('total_cost_usd')); print(d.get('result'))" "saidas/e4-modelo-$m.json" "$m"
done
```

O custo é uma **estimativa** calculada pelo Claude Code e pode diferir da cobrança real.

### Passo 3 — Qualidade · 7 min

Compare as três linhas de cada modelo com a **sua triagem revisada do E2** (`triagem/relatorio.md`). Quantas você aceitaria sem mudança? Quem não fez o E2 compara com a triagem revisada de um colega.

### Passo 4 — Painel · 3 min

Lance: modelo, segundos, custo estimado e linhas aceitas.

---

## Antes de sair

```bash
git add .
git commit -m "e4"
```

Responda o formulário de feedback do módulo, no canal da turma.

## Para aprofundar

- Zheng, L. et al. [Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena](https://arxiv.org/abs/2306.05685). NeurIPS 2023.
- [Execução programática do Claude Code](https://code.claude.com/docs/en/headless): `claude -p`, saída em JSON e custo estimado.
- [Configuração de modelo no Claude Code](https://code.claude.com/docs/en/model-config): `--model` e `/model`.
