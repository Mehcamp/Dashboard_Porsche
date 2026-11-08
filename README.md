# Painel de Vendas Porsche (HTML + GitHub Pages)

Dashboard interativa em um único arquivo HTML (`index.html`) que responde perguntas de negócio sobre 100 vendas de carros Porsche. Feita como projeto final de um desafio da DIO.

**Endereço da dashboard publicada:** `https://mehcamp.github.io/Dashboard_Porsche/`

## Perguntas de negócio escolhidas

1. **Qual linha de modelo gera mais receita?** Agrupei os 41 modelos em seis linhas (911, 718, Cayenne, Macan, Panamera e Taycan), porque comparar 41 modelos com 1 a 4 vendas cada não diz nada. Por linha, dá para ver onde está o dinheiro: a linha 911 lidera, com cerca de US$ 4,27 milhões (um terço da receita).
2. **Como os clientes pagam?** Mostra a receita e o número de vendas por método de pagamento. Ajuda a entender quais formas de pagamento concentram mais valor: transferência bancária internacional (*wire transfer*) lidera, com 26 vendas.
3. **Carros mais novos custam mais?** Mostra o preço médio por ano do modelo e quantas vendas cada ano tem. Os modelos de 2024 a 2026 têm preço médio bem mais alto que os de 2021 a 2023.

Acima das perguntas ficam os indicadores de topo: número de vendas, receita total, ticket médio e porcentagem de vendas entregues.

## Filtros

Linha, ano do modelo, método de pagamento e estado. Todos os indicadores e gráficos se atualizam juntos, e o botão "Limpar filtros" volta ao estado inicial. Usei **estado** em vez de cidade porque a base tem 79 cidades, quase todas com 1 ou 2 vendas, o que deixaria o filtro inútil.

## Tratamento da base

A planilha tem cada campo em duas versões: o dado cru e o sanitizado. Para a dashboard:

- Mantive apenas as colunas sanitizadas (modelo, ano, preço, método de pagamento, estado e status de entrega) mais o `sale_id`.
- Preço e ano já estavam como números nas colunas sanitizadas.
- Criei a coluna **linha** a partir da primeira palavra do modelo (por exemplo, "Macan GTS" vira "Macan"; "911 Turbo S" vira "911").
- A **data da venda** ficou de fora: 24 das 100 linhas estão como `INVALID` na coluna sanitizada (datas impossíveis como 30/02), então uma análise por mês seria enviesada. A ideia de "evoluir" do desafio, escrever uma segunda regra para recuperar essas datas, ficaria para uma próxima versão.
- Não há dados sensíveis na base embutida: removi nome do cliente e vendedor, que não eram necessários.

## Ferramenta usada e prompt

A dashboard foi gerada com o **Claude** (assistente de IA da Anthropic).  Escolhi o Claude porque ele consegue ler a planilha anexada, testar o resultado com os filtros aplicados antes de eu enviar. Enviei a base e pedi uma dashboard com visual criativo, mas simples. Depois revisei os números e os filtros e ajustei o texto do README com as minhas palavras. Resumo do pedido:

> Crie uma dashboard em HTML, em arquivo único, com a base de vendas da Porsche anexada. Quero três perguntas de negócio respondidas por gráficos, filtros para recortar os dados, indicadores no topo e um visual coerente. Pode ser criativo no design, mas sem complicar.

**O que mudou até a versão final:**
- Troquei o filtro de cidade por estado e criei a "linha" do modelo, pelos motivos acima.
- Os gráficos de barras ficaram estreitos na primeira versão em cards pequenos, então aumentei a largura mínima dos cards.
- Testei a página com filtros combinados (por exemplo, linha 911 com *wire transfer*, que dá 7 vendas e US$ 1,67 milhão) e com um filtro sem resultados, que mostra uma mensagem em vez de quebrar.

**Visual:** fundo escuro, vermelho Porsche para os destaques e dourado para o gráfico de anos, com fonte sem serifa e títulos em caixa alta espaçada. Os gráficos são desenhados com HTML e CSS puros, sem bibliotecas externas.

## Como publicar no GitHub Pages

1. Crie um repositório **público** na sua conta, com nome em minúsculas e sem acento (por exemplo, `dashboard-porsche`).
2. Suba o `index.html` e este `README.md`.
3. Vá em **Settings → Pages**, escolha a branch `main` e a pasta `/ (root)` e salve.
4. Em alguns minutos o endereço estará no ar. Copie-o para o topo deste README.

## Evidências

Print da dashboard e um exemplo de filtro aplicado em `images/` (por exemplo, `dashboard-geral.png` e `filtro-911-wire-transfer.png`).
