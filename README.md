## **Introdução e Contexto do Projeto**

O mercado imobiliário europeu tem sido um dos temas mais discutidos nos últimos anos, com uma percepção geral de que os preços dos imóveis estão aumentando rapidamente, enquanto os salários não acompanham esse crescimento.

Em Portugal, por exemplo, os preços dos imóveis subiram de forma significativa, tornando a compra e o aluguel cada vez menos acessíveis. O objetivo deste projeto é realizar uma análise comparativa entre Portugal e outros países europeus para identificar quais tiveram os maiores aumentos nos preços dos imóveis e como isso impacta a acessibilidade habitacional.

Foram utilizadas duas métricas principais obtidas no portal da União Europeia:

- **House Price Index (HPI - Índice de Preço das Casas, Deflacionado)**: Indica a evolução dos preços dos imóveis ao longo do tempo, já ajustado pela inflação.
- **House Price to Income Ratio (PTIR - Preço dos Imóveis em Relação à Renda)**: Mede a acessibilidade habitacional, ou seja, quão caro está o imóvel em relação à renda das pessoas.

## **Decisão de Exclusão da Tabela de Inflação**

Inicialmente, consideramos a possibilidade de analisar a inflação separadamente, mas optamos por não utilizar a tabela de inflação (`tec00118 - Inflation Rate`) pelos seguintes motivos:

- O **House Price Index (HPI)** já é ajustado pela inflação, o que significa que a variação nos preços dos imóveis já reflete os efeitos inflacionários ao longo do tempo.
- O estudo busca uma análise mais direta e objetiva, sem aprofundar em cálculos complexos relacionados à inflação acumulativa.
- O foco do projeto é comparar o crescimento do mercado imobiliário e a acessibilidade habitacional, não a inflação em si.

## **Estrutura dos Dados e Considerações Importantes**

### **Tabelas Utilizadas**

Foram selecionadas duas tabelas principais do portal da União Europeia:

|**Tabela**|**Código**|**Métrica Principal**|**Descrição**|
|---|---|---|---|
|House Price Index (Deflated)|`tipsho10`|HPI (House Price Index)|Índice de preços de imóveis, já ajustado pela inflação. Mede a evolução dos preços das casas a partir de um referencial.|
|House Price to Income Ratio|`tipsho60`|PTIR (Price-to-Income Ratio)|Mede a acessibilidade habitacional. Quanto maior o índice, mais difícil comprar um imóvel em relação à renda.|

Ambas as tabelas iniciam em **2015 com um valor referencial de 100**.

Esse valor de **100 em 2015** significa que todas as variações a partir desse ano são relativas a essa base.

- Se o índice for **110 em 2020**, significa que os preços subiram **10% desde 2015**.
- Se o índice for **95 em 2020**, significa que os preços caíram **5% desde 2015**.

É importante analisar se o índice de referência (100) é global ou ajustado para cada país, pois isso pode afetar a forma como interpretamos a evolução dos preços.

### **Criação de Tabelas Auxiliares**

Para garantir um modelo de dados eficiente e seguro no Power BI, foram criadas duas tabelas auxiliares:

- **Tabela de Países (`Countries`)**: Contém a lista única de países para evitar inconsistências nos dados.
- **Tabela de Anos (`Years`)**: Criada como tabela de calendário para facilitar os relacionamentos entre os dados.

Essas tabelas permitem criar relacionamentos **One-to-Many**, garantindo filtros mais eficientes e cálculos mais precisos. Sempre utilizamos os campos das tabelas de Países e Anos para relacionamentos, pois isso evita erros ao filtrar os gráficos.

## **Dashboards e Visualizações**

O projeto foi dividido em duas análises principais, refletindo as métricas essenciais para entender o mercado imobiliário europeu.

### **1️⃣ Evolução dos Preços dos Imóveis na Europa**

Objetivo: Identificar quais países tiveram o maior aumento no preço dos imóveis desde 2015.

#### **Visualizações**

- **Gráfico de Linha: Evolução do House Price Index (HPI) por País**
    - Mostra como os preços dos imóveis cresceram ou diminuíram ao longo dos anos.
- **Mapa de Calor (Heatmap): Variação do HPI por País**
    - Identifica quais países tiveram os maiores aumentos de preços.
- **Gráfico de Barras: Top 5 Países com Maior e Menor Crescimento no HPI**
    - Destaque para os países com maior e menor valorização imobiliária.

Métrica de Referência: Média do HPI na União Europeia como linha de comparação nos gráficos.

### **2️⃣ Acessibilidade Habitacional na Europa**

Objetivo: Descobrir quais países têm o mercado imobiliário mais caro em relação à renda da população.

#### **Visualizações**

- **Gráfico de Barras Horizontais: Países com Maior e Menor PTIR**
    - Destaca os países onde é mais difícil e mais fácil comprar um imóvel.
- **Gráfico de Linha: Evolução do PTIR ao Longo do Tempo**
    - Exibe a tendência de acessibilidade ao longo dos anos.
- **Gráfico Comparativo: Crescimento do HPI vs. Crescimento do PTIR**
    - Mostra se os aumentos nos preços dos imóveis impactaram diretamente a acessibilidade.

Métrica de Referência: Média da União Europeia como linha de comparação.

## **Métricas e Cálculos DAX**

Algumas measures principais foram criadas para facilitar a análise:

### **HPI Growth (Crescimento do House Price Index)**

DAX

CopyEdit

`HPI_Growth =  VAR FirstYear = MIN('tipsho10'[Year]) VAR LastYear = MAX('tipsho10'[Year]) RETURN     CALCULATE(AVERAGE('tipsho10'[HPI]), 'tipsho10'[Year] = LastYear) -      CALCULATE(AVERAGE('tipsho10'[HPI]), 'tipsho10'[Year] = FirstYear)`

Essa medida calcula o crescimento percentual do HPI desde 2015 para cada país.

## **Considerações Finais e Próximos Passos**

A análise revelou insights importantes sobre a crise de acessibilidade habitacional na Europa.

- Alguns países tiveram valorização extrema dos imóveis, enquanto outros mantiveram preços mais estáveis.
- A acessibilidade habitacional deteriorou-se em várias regiões, tornando difícil para a população adquirir imóveis.

### **Próximos Passos:**

1. Investigar as causas do aumento dos preços nos três países com maior crescimento imobiliário.
2. Analisar possíveis quedas futuras nos preços, considerando fatores econômicos e mudanças no mercado de trabalho (ex: home office pós-COVID).

Este projeto oferece uma análise objetiva do mercado imobiliário europeu, fornecendo insights valiosos sobre preços e acessibilidade habitacional.

### **Links**

- **GitHub Repository:** [Adicionar link]
- **Power BI Public Report:** [Adicionar link]
