# Encontro 2 — Instalar o Claude Code antes da aula

Faça este guia em casa, antes de segunda, 09/11. Leva poucos minutos quando tudo dá certo; se travar, traga anotado o erro que apareceu e resolvemos no começo da aula.

Na aula, você vai usar o Claude Code de dois jeitos: no aplicativo **Claude Desktop**, na aba **Code**, e no **terminal**, com o comando `claude`. São duas instalações.

**Você vai precisar de:** notebook com permissão de instalação, internet e uma conta com acesso ao Claude Code.

## 1. Conta com acesso ao Claude Code

O plano gratuito do claude.ai **não** inclui o Claude Code; servem os planos Pro, Max, Ultra, Team ou Enterprise. A via da turma é:

> **[A coordenação preenche aqui antes de enviar: convite para a organização do curso, ou conta própria Pro ou Max.]**

Se a via for o convite, aceite o e-mail de convite antes da aula.

## 2. Requisitos

- Windows 10 ou mais novo (x64 ou ARM64) ou macOS. No Linux, o Claude Desktop está em versão beta para Ubuntu e Debian.
- 4 GB de RAM ou mais.

## 3. Git

Usamos o Git para ver tudo o que o agente mudar na pasta do projeto.

- Confira com `git --version` num terminal.
- Se não tiver: baixe em [git-scm.com/downloads](https://git-scm.com/downloads). No Windows, instale o Git for Windows.

## 4. Claude Desktop, com a aba Code

1. Baixe e instale o Claude Desktop em [claude.ai/download](https://claude.ai/download).
2. Abra o aplicativo e entre com a conta do passo 1.
3. Confira que aparece a aba **Code**. Ela já traz o Claude Code: não precisa instalar mais nada para usar a aba.

O Claude Desktop **não** instala o comando `claude` no terminal. Faça também o passo 5.

## 5. Claude Code no terminal

Abra um terminal e rode **um** dos comandos abaixo, conforme o seu sistema. São os comandos da documentação oficial; não rode comandos de instalação de outras fontes.

**Windows, no PowerShell** (o prompt começa com `PS C:\`; não precisa ser administrador):

```powershell
irm https://claude.ai/install.ps1 | iex
```

**macOS ou Linux:**

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

O instalador não mostra progresso enquanto baixa. Quando terminar, **feche o terminal e abra um novo**.

## 6. Conferir

```bash
claude --version
```

Deve aparecer um número de versão seguido de `(Claude Code)`. Para um diagnóstico completo:

```bash
claude doctor
```

## 7. Entrar com a sua conta no terminal

```bash
claude
```

Na primeira vez, o Claude Code abre o navegador para o login. Entre com a conta do passo 1. Se o navegador não abrir, tecle `c` para copiar o endereço e cole no navegador. Ao terminar, o terminal mostra `Login successful`. Digite `/exit` para sair.

## Se algo der errado

| Sintoma | O que fazer |
|---|---|
| A aba Code não aparece no Claude Desktop | Confira se entrou com a conta do passo 1; o plano gratuito não tem a aba Code. Atualize o aplicativo. |
| `claude` não é reconhecido no terminal | Feche e abra um terminal novo. Se continuar, rode `claude doctor` e traga a saída para a aula. Lembre que o Claude Desktop não instala esse comando. |
| `'irm' is not recognized` | Você está no CMD, não no PowerShell. Abra o PowerShell e repita. |
| O login diz que a conta não tem acesso | Contas do plano gratuito não acessam o Claude Code. Confira a via do passo 1. |
| A instalação é bloqueada pela política do notebook ou pela rede da empresa | Anote a mensagem e traga; você faz a aula em dupla. |

Referência: documentação do Claude Code: [Claude Desktop](https://code.claude.com/docs/en/desktop-quickstart), [instalação da linha de comando](https://code.claude.com/docs/en/setup) e [autenticação](https://code.claude.com/docs/en/authentication).
