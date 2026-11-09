# Modelo de rubrica

Copie a tabela para um arquivo `rubrica.md` na raiz da pasta do caso e preencha. O exemplo é de **outro artefato** (resumo de bug), só para mostrar o nível de detalhe esperado; a sua rubrica é para **casos de teste derivados de uma história de usuário**.

**Quatro regras para escrever:**

1. **Cada nível diz o que se vê na saída.** “Bom” e “ruim” não são níveis.
2. **Um critério mede uma coisa só.** Se dois critérios sobem e descem juntos, junte-os.
3. **Nenhum critério premia tamanho.** Mais casos não é melhor.
4. **Escreva antes de olhar as saídas que vai avaliar.**

## Exemplo, de outro artefato

| Critério | 0 | 1 | 2 |
|---|---|---|---|
| Fidelidade do resumo de bug | O resumo afirma algo que o relato não diz | O resumo é fiel, mas omite o resultado obtido ou o esperado | O resumo traz o resultado obtido e o esperado, sem acrescentar nada |

## A sua rubrica

```markdown
# Rubrica — casos de teste derivados de uma história de usuário

| Critério | 0 | 1 | 2 |
|---|---|---|---|
| [critério 1] | [o que se vê na saída] | [o que se vê na saída] | [o que se vê na saída] |
| [critério 2] | | | |
| [critério 3] | | | |
| [critério 4] | | | |
| [critério 5, opcional] | | | |

Nota total: soma dos níveis.
```
