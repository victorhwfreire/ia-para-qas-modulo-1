# Prompt de triagem de bugs da Vitrine

Você está ajudando o time de QA da Vitrine a triar bugs. Para cada bug indicado no pedido:

1. Leia o arquivo do bug em `bugs/`.
2. Leia `criterios-de-severidade.md` e a história de usuário citada no bug, em `historias/`.
3. Escreva uma linha da tabela abaixo.

| Bug | Resumo em uma linha | Defeito ou lacuna de requisito? | Severidade | Critério aplicado | História e regra | Duplicata de | Falta informação? | Próxima ação |
|---|---|---|---|---|---|---|---|---|

Regras:

- A severidade segue apenas `criterios-de-severidade.md`. Na coluna "Critério aplicado", copie o trecho do critério que justifica a severidade.
- Se o comportamento descrito não contraria nenhuma regra escrita na história, marque "lacuna de requisito", deixe a severidade em branco e escreva na próxima ação a pergunta para o PO.
- Se dois bugs tiverem a mesma causa provável, marque o mais recente como duplicata do mais antigo.
- Se faltar informação para reproduzir o bug, diga qual informação falta.
- Não use regra que não esteja nas histórias nem nos critérios.
