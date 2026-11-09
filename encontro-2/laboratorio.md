# Encontro 2 — Laboratórios

**Objetivo:** pôr o Claude Code para fazer uma triagem de bugs de ponta a ponta e aceitar o resultado só com base em evidência.

**Regra da noite:** o Claude Code fica no modo **Manual** o tempo todo. Ele lê sozinho, mas pede licença antes de editar arquivo ou rodar comando. Leia cada pedido antes de responder. No Claude Desktop, o modo se escolhe no seletor abaixo da caixa de prompt.

---

## Laboratório 1 — Instalar, entrar e abrir o caso (19:38–20:13)

### Passo 1 — Conferir · 10 min

```bash
claude --version
claude doctor
```

Abra o Claude Desktop e confira que aparece a aba **Code**. Se não instalou em casa, siga agora o [guia de instalação](instalacao.md).

### Passo 2 — Entrar · 8 min

No Claude Desktop, entre com a conta da turma. No terminal:

```bash
claude
```

Faça o login no navegador com a mesma conta. Depois, `/exit`.

### Passo 3 — Preparar o caso · 7 min

1. Copie a pasta `caso-vitrine` do canal da turma para uma pasta local, **fora** de OneDrive, iCloud ou Google Drive. Por exemplo: `C:\cursos\caso-vitrine` no Windows ou `~/cursos/caso-vitrine` no macOS e no Linux.
2. No terminal, dentro dessa pasta:

```bash
git init
git add .
git commit -m "caso inicial"
```

Se o Git pedir nome e e-mail, rode os dois comandos abaixo com os seus dados e repita o `git commit`:

```bash
git config --global user.name "Seu Nome"
git config --global user.email "voce@exemplo.com"
```

### Passo 4 — Primeira sessão · 10 min

No Claude Desktop, aba **Code**:

1. Na linha abaixo da caixa de prompt, escolha o ambiente **Local** e, no seletor de pasta, **Open folder…**: abra a pasta do caso. Deixe a opção **Worktree** desligada (é o padrão), para o agente trabalhar na própria pasta.
2. Pergunte: `Em três frases, do que trata este projeto?` Antes de ler a resposta, olhe **quais arquivos ele leu**.
3. Digite `/context` e veja o que está ocupando a janela.
4. Abra o seletor de modo, abaixo da caixa de prompt, e veja os modos. Deixe em **Manual**. No Desktop, `Shift+Tab` não troca o modo.
5. Abra o terminal integrado do Desktop com `` Ctrl+` `` e rode `git status`: nada mudou, porque ele só leu.

---

## Laboratório 2 — Triagem dos bugs da Vitrine (20:43–21:38)

### Passo 1 — Sem IA · 10 min

Leia `criterios-de-severidade.md`, `bugs/BUG-102.md`, `bugs/BUG-107.md` e as histórias que eles citam. Faça a triagem desses dois bugs **à mão**, no [registro](registro.md). Essa triagem é a sua régua para revisar a do agente.

### Passo 2 — No Claude Desktop · 15 min

Na aba Code, com a pasta do caso aberta e o modo **Manual**, peça:

```text
Faça a triagem de bugs/BUG-101.md a bugs/BUG-108.md seguindo prompts/triagem.md e grave o resultado em triagem/relatorio.md.
```

1. Enquanto ele trabalha, veja quais arquivos ele lê.
2. Quando ele pedir para criar o arquivo, **leia o diff** antes de aceitar.
3. No terminal integrado do Desktop (`` Ctrl+` ``), rode `git status` e confira o que mudou na pasta. Se o arquivo não aparecer, confira se a opção Worktree ficou desligada.

### Passo 3 — Revisar · 18 min

Para cada linha de `triagem/relatorio.md`, faça as cinco perguntas:

1. **Resumo:** é fiel ao que o bug descreve?
2. **Defeito ou lacuna:** existe uma regra escrita na história que o comportamento contraria?
3. **Severidade:** o trecho do critério citado é o que se aplica?
4. **Duplicata:** tem a mesma causa de outro bug?
5. **Informação:** dá para reproduzir com o que está escrito?

Passou em todas: **aceito**. Precisa de ajuste pontual: **corrijo**, editando o próprio arquivo. Errou no fundo: **rejeito**. Anote no registro. Comece pelo BUG-102 e pelo BUG-107, comparando com a sua triagem à mão.

### Passo 4 — No terminal · 8 min

Chegou um bug novo, o BUG-109. No terminal integrado do Desktop ou num terminal comum (no Windows, o PowerShell), dentro da pasta do caso, rode **duas vezes**:

```bash
claude -p 'Faça a triagem de bugs/BUG-109.md seguindo prompts/triagem.md. Mostre a linha da tabela na tela e não grave nenhum arquivo.' --allowedTools Read
```

Compare as duas respostas no registro. Depois, `git status`: nada deve ter mudado.

### Passo 5 — Painel · 4 min

Lance no painel da turma: linhas aceitas, corrigidas e rejeitadas, e a severidade do BUG-109 nas duas execuções.

---

## Se terminar antes

Na aba Code do Desktop, mude o seletor de modo para **Plan** e peça: `Faça um plano para reproduzir o BUG-106 e liste as informações que faltam no relato.` Leia o plano e **não** aprove a execução.

## Antes de sair

Salve a triagem revisada e o registro no Git. Eles voltam no encontro 4.

```bash
git add .
git commit -m "triagem revisada"
```
