# ad-teardown-pipeline

Os anúncios ativos de um concorrente, lidos por um modelo de visão e devolvidos como uma análise com
nota.

A maioria das ferramentas de pesquisa de concorrente resume a legenda do anúncio. A legenda é a
parte que o anunciante escreveu pro algoritmo. Este fluxo baixa o criativo de verdade e manda a
imagem pro modelo de visão, então a nota fala do que quem assiste vê nos três primeiros segundos.

## O fluxo

Uma fila no Notion tem uma página por marca, preenchida por um coletor que raspa a Biblioteca de
Anúncios da Meta pelo Apify. Esse coletor é outro workflow e não está neste repo. Este consome a
fila.

**Principal** (8 nós): roda a cada 4 horas, lê as linhas `To do` e chama o sub uma vez por página.
No fim, um resumo e um aviso no Telegram.

**Sub** (22 nós): marca a página como `Analyzing`, lista a pasta da marca no Drive, baixa o contexto
do anúncio e as imagens do criativo, monta o prompt de visão com a rubrica, chama o modelo, grava o
`teardown.txt` de volta na pasta da marca, escreve a análise no corpo da página do Notion e marca
`Done`.

Se a página não tem dado aproveitável, o sub marca `Error` e devolve um erro estruturado, em vez de
derrubar o lote inteiro.

## A rubrica

A nota segue critério fixo, não impressão. Pesos: gancho 40, desenvolvimento 30, chamada pra ação
30, mais aderência ao briefing. A parte do gancho pergunta se o criativo para a rolagem sem som e
sem contexto, porque a maior parte do público assiste no mudo.

A saída tem duas coisas ao mesmo tempo: texto pra uma pessoa ler e um bloco JSON estruturado pra
próxima automação consumir.

O `rubric.pt.md` é a rubrica original. Ela entra no prompt de sistema.

## Números

| | |
|---|---|
| Custo por relatório de concorrente | US$ 0,004 |
| Agenda | a cada 4 horas, sem ninguém olhando |
| Relatórios por marca | 1; rodar de novo sobrescreve em vez de empilhar |

Primeira execução verde do início ao fim: 02/09/2026, com L'Oréal Paris e depois Principia Skincare
Pro. Criativo baixado e avaliado, `teardown.txt` no Drive, análise na página do Notion, status
`Done`.

## Como rodar

O `workflow.json` (principal) e o `subworkflow-teardown.json` (sub) importam em qualquer instância
do n8n. Os dois estão sanitizados: credenciais e ids de banco do Notion, de pasta do Drive e de chat
são marcadores.

1. Importe os dois. Abra o principal e aponte o nó Execute Workflow pra sua cópia do sub.
2. Ligue as credenciais: Notion, Google Drive, OpenRouter e Telegram.
3. Crie o banco do Notion com uma propriedade `Status` com as opções `To do`, `Analyzing`, `Done` e
   `Error`.
4. Preencha o nó `Configuracao` do principal com os ids do seu banco e das pastas.
5. A chamada de visão usa o nó da comunidade do OpenRouter. Numa instância em modo fila, ele precisa
   estar instalado no worker, não só no editor, senão a agenda dispara e o nó não existe.

O `flow.drawio` tem o fluxograma, uma página pro principal e outra pro sub.

## Situação

Rodou na minha instância do n8n, contra anunciantes reais, em setembro de 2026. Nenhum cliente rodou
em produção ainda.

Stack: n8n, Apify (antes do fluxo), OpenRouter (visão), Notion, Google Drive, Telegram.
