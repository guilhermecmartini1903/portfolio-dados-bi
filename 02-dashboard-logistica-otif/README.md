# Caso 02 — Torre de Controle de Transportes: Monitoramento Logístico e OTIF

> **Navegação Interativa (Power BI):** [Acessar Portfólio Publicado](https://app.powerbi.com/view?r=eyJrIjoiN2I2ZDgwYzYtZTRkZC00YTNkLTllNzAtYzg2OTQ5NTRkYjM1IiwidCI6IjVjZWYyNWRiLTAyYmYtNDQ0ZS04YzVkLWI3ZjA0NzZkZTc1NyJ9)

## 1. Contexto e Problema de Negócio
Na operação de distribuição, acompanhar apenas o volume faturado não garante eficiência na ponta. A **Torre de Controle de Transportes** foi estruturada para responder a três perguntas operacionais entre **2021 e 2022**:
1. Qual é o nível real de serviço entregue ao cliente final (**OTIF — On Time In Full**)?
2. Quais transportadoras estão puxando os índices de atraso (**OTD — On Time Delivery**)?
3. Qual o impacto financeiro e volumétrico dos **desvios operacionais** nas entregas e quais clientes concentram maior movimentação?

---

## 2. Origem dos Dados
* **Fonte:** Base operacional de embarques e notas fiscais de transporte (dataset fictício de logística e cadeia de suprimentos cobrindo o período de **01/01/2021 a 27/12/2022**, totalizando `2,73 mil` notas fiscais, `9 mil` volumes transportados e `R$ 6 Mi` em faturamento transportado).
* **Nota de transparência:** Projeto desenvolvido originalmente para monitoramento de KPIs logísticos no Power BI; a estrutura dimensional abaixo reflete a organização das entidades e regras aplicadas no painel.

---

## 3. Tratamento e Preparação dos Dados (Power Query / DAX)
* **Padronização de datas e status de entrega:** Tratamento das datas de faturamento, previsão de entrega e entrega efetiva para classificar cada nota fiscal como *On Time* ou *Atraso*.
* **Categorização de ocorrências:** Agrupamento de ocorrências de transporte para separar entregas regulares de **Desvios Operacionais**.
* **Padronização geográfica e de parceiros:** Normalização dos nomes das transportadoras, *Warehouses* de origem, clientes embarcadores e macrorregiões (*Centro-Oeste, Nordeste, Norte, Sudeste e Sul*).
* **Medidas DAX de SLA:**
  * Cálculo percentual de **OTIF (`% In Full`)** e **OTD (`% On Time` vs. `% Atraso`)** por transportadora e ao longo do tempo.
  * Contagem distinta de Notas Fiscais, soma de Volumes e representatividade percentual dos desvios operacionais.

---

## 4. Modelagem Dimensional
O modelo segue o padrão **Star Schema**, centralizando os registros de notas fiscais/embarques na tabela fato e conectando-a às dimensões operacionais:

* **Tabela Fato (`fEntregas`):**
  * **Granularidade:** Nota Fiscal / conhecimento de transporte emitido.
  * **Métricas:** Quantidade de Notas Fiscais (`2,73 mil`), Quantidade de Volumes (`9 mil`), Valor Faturado (`R$ 6 Mi`), Indicador On Time (`0/1`), Indicador In Full (`0/1`) e Flag de Desvio Operacional.
* **Tabelas Dimensão:**
  * `dCalendario`: Data de faturamento, Ano (2021 e 2022) e Mês/Ano.
  * `dTransportadora`: ID e Nome da Transportadora (*Cargo Centro Oeste, Gaúcha Transportes, Paulistana, RodoNordeste, RodoCarioca, entre outras*).
  * `dWarehouse`: Unidade/Armazém de origem da carga.
  * `dCliente`: Cliente destinatário e Região geográfica.

```text
               [ dCalendario ]
                      |
                      | (1:N)
                      v
[ dWarehouse ] --(1:N)--> [ fEntregas ] <--(1:N)-- [ dTransportadora ]
                      ^
                      | (1:N)
                      |
                 [ dCliente]
