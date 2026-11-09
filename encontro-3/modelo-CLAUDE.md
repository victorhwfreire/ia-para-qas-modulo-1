# Modelo de CLAUDE.md para o projeto Vitrine

Copie as seções abaixo para um arquivo `CLAUDE.md` na raiz da pasta do caso e substitua cada pergunta pela sua resposta, em frases curtas. Apague as perguntas.

**Três regras para escrever:**

1. **Só o que vale para toda tarefa.** Regra da US-02 é da tarefa, não do projeto: ela fica na história.
2. **Específico, não genérico.** “Seja preciso” não muda nada; “todo resultado esperado aponta a regra de onde vem” muda.
3. **Curto.** Até 40 linhas: o arquivo entra na janela em toda chamada.

---

```markdown
# Vitrine — instruções para o agente de QA

## O projeto
- [O que é a Vitrine, em uma linha?]
- [Que informações do domínio o agente precisa ter sempre à mão? Ex.: meios de pagamento, status do pedido.]
- [Onde fica cada tipo de arquivo no projeto?]

## Fonte de verdade
- [O que conta como regra de negócio, e o que não conta?]
- [O que fazer quando a história não define um comportamento?]
- [Com base em que se classifica a severidade de um bug?]

## Formato
- [Em que formato você quer casos de teste? Quais colunas, em que ordem?]
- [Como a origem de cada resultado esperado deve aparecer?]
- [Outras convenções: idioma, valores em reais, o que vem depois da tabela.]

## Ao revisar casos de teste
- [Contra o que cada caso deve ser conferido?]
- [Que tipos de problema o agente deve apontar?]

## Não fazer
- [Que arquivos o agente não deve alterar?]
- [Que dados nunca devem ser usados?]
```
