# Modelando um Dashboard de E-commerce com Power BI Utilizando Fórmulas DAX

## Resumo do Projeto
O projeto consistiu na modelagem e estruturação de um diagrama condicional para análise de dados financeiros. Foram criadas diversas tabelas dimensionais e uma tabela fato a partir da base "Sample Financials". As principais etapas envolveram a agregação de dados, a exclusão de informações redundantes e a criação de chaves primárias para relacionamentos eficientes entre as tabelas. Além disso, utilizamos funções DAX para gerar uma tabela de datas estruturada, garantindo uma análise temporal precisa.

## 1. Duplicação da Tabela "Sample Financials"
A primeira etapa do projeto consistiu na duplicação da tabela "Sample Financials" para garantir a preservação dos dados originais e possibilitar a modelagem das tabelas dimensionais e de fatos.

## 2. Criação da Tabela "d_produtos"
Nesta etapa, foi criada a tabela "d_produtos" por meio de agregações que consolidaram informações relevantes dos produtos. As colunas incluídas foram:
- "Média de Unidades Vendidas"
- "Média do Valor de Vendas"
- "Mediana do Valor de Vendas"
- "Valor Máximo de Venda"
- "Valor Mínimo de Venda"

Além disso, foi criado um índice para referência única de cada produto, renomeado para "ID_Produto".

## 3. Criação da Tabela "d_descontos"
Para estruturar a tabela "d_descontos", foram realizadas as seguintes operações:
- Criação de uma coluna condicional contendo o nome e código de cada produto, renomeada para "ID_Produto"
- Exclusão de registros duplicados
- Remoção das colunas irrelevantes, mantendo apenas "Discounts" e "Discount Band"

## 4. Criação da Tabela "d_produtos_detalhes"
A tabela "d_produtos_detalhes" foi estruturada para conter informações detalhadas dos produtos:
- Criação de uma coluna condicional com o nome e código de cada produto, renomeada para "ID_Produto"
- Remoção de registros duplicados
- Exclusão das colunas desnecessárias, mantendo apenas:
  - "Produto"
  - "Discount Band"
  - "Sale Price"
  - "Units Sold"
  - "Manufacturing Price"
  - "Sales"

## 5. Criação da Tabela "d_detalhes"
A tabela "d_detalhes" foi estruturada para conter colunas que não estavam presentes nas outras tabelas dimensionais. Foi realizada a criação de uma coluna condicional contendo o nome e código de cada produto, renomeada para "ID_Produto".

## 6. Criação da Tabela Fato "f_vendas"
A tabela fato "f_vendas" foi construída através das seguintes etapas:
- Exclusão de registros duplicados
- Remoção das colunas irrelevantes, mantendo apenas:
  - "Produto"
  - "Units Sold"
  - "Sale Price"
  - "Discount Band"
  - "Segment"
  - "Country"
  - "Sales"
  - "Profit"
  - "Date"
- Criação de um índice como referência de código das vendas, renomeado para "SK_ID"
- Criação de uma coluna condicional do nome e código de cada produto, renomeada para "ID_Produto", para estabelecer relações com as tabelas dimensionais

## 7. Criação da Tabela de Datas com DAX
Para estruturar a tabela de datas, utilizamos a função DAX `CALENDARAUTO` para criar a "Table Date" contendo todas as datas presentes nos registros.

Outras funções DAX utilizadas:
- `YEAR` para criar a coluna "Year"
- `MONTH` para criar a coluna "Month Number"
- `WEEKNUM` para criar a coluna "Week Number"
- `WEEKDAY` para criar a coluna "Day of the Week" (número do dia da semana)
- `FORMAT` para criar a coluna "Day of the Week 2" (nome do dia da semana)

Para garantir a conectividade entre "Table Date" e "f_vendas":
- Modificamos o tipo de formato da coluna "Date" para "Short Date" em ambas as tabelas
- Excluímos a coluna "Year" da tabela "f_vendas"
- Criamos a coluna "Month Name" na "Table Date", com a informação do nome do mês da "f_vendas", utilizando a combinação das funções `DATE` e `FORMAT` para exibição com três caracteres (ex: Jan, Feb, Mar)
- Excluímos a coluna "Month Name" da tabela "f_vendas"

Com essa estruturação, garantimos a organização eficiente dos dados, permitindo a construção de um modelo de dados bem-relacionado e otimizado para análise.

