# Caso 01 — Lets-Cola Company: Inteligência Comercial, Financeira e de Portfólio

> **Navegação Interativa (Power BI):** [Acessar Portfólio Publicado] https://app.powerbi.com/view?r=eyJrIjoiYjcwZDJlNzEtNWVkZS00N2M2LThiNzItYTlkNmM2NTY2NTYwIiwidCI6IjVjZWYyNWRiLTAyYmYtNDQ0ZS04YzVkLWI3ZjA0NzZkZTc1NyJ9
## 1. Contexto e Problema de Negócio
A **Lets-Cola Company** (cenário analítico de distribuição de bebidas e alimentos) precisava consolidar em um único ambiente executivo três visões críticas de operação entre **2019 e 2022**:
1. **Comercial:** acompanhar o faturamento acumulado, cumprimento de metas, evolução mensal, ranking de vendedores/supervisores e desempenho por grupo de clientes.
2. **Financeiro:** cruzar receita, custos diretos e frete para avaliar margem de lucro, distribuição geográfica das vendas e simular cenários de redução de custos (*What-If*).
3. **Produtos:** entender a representatividade de cada categoria no faturamento e identificar a concentração de receita dentro do mix de 46 produtos ativos.

---

## 2. Origem dos Dados
* **Fonte:** Base histórica estruturada de vendas, produtos, clientes, vendedores e custos operacionais (dataset fictício utilizado em projeto prático de Business Intelligence para simulação de cenário corporativo real, cobrindo o período de **01/01/2019 a 30/12/2022**).
* **Nota de transparência:** Este projeto foi desenvolvido originalmente com foco em visualização executiva e regras DAX; a documentação de modelagem abaixo consolida a estrutura relacional extraída diretamente das entidades e métricas do relatório.

---

## 3. Tratamento e Preparação dos Dados (Power Query / DAX)
* **Padronização temporal e calendário:** Criação/estruturação de tabela calendário (`dCalendario`) para suportar comparativos temporais (`vs. Ano Anterior`), evolução mensal e filtros de intervalo de datas.
* **Normalização de entidades comerciais:** Padronização de grupos de clientes (*Pequeno Porte, Tradicional, Redes Regionais, Atacados, Atacarejo, Food Services*), canais/unidades de negócio e hierarquia comercial (*Supervisor $\rightarrow$ Vendedor*).
* **Tratamento de catálogo e mídia:** Estruturação de 6 categorias de produtos (*Bebidas, Snacks, Matinais, Doces, Chás e Energéticos*) com suporte a URLs de imagens para identificação visual dos itens.
* **Regras de negócio em DAX:**
  * Cálculo de **Receita Bruta/Vendas**, **Custo Total**, **Frete**, **Lucro** e **Margem %**.
  * Comparativos de meta (`vs. meta`) e crescimento anual (`vs. ano anterior`).
  * **Parâmetro de Simulação (What-If):** criação de parâmetro numérico para simular redução percentual nos custos e calcular automaticamente o *saving* financeiro projetado.

---

## 4. Modelagem Dimensional
O modelo segue o padrão de Esquema Estrela, separando os registros transacionais de pedidos das tabelas descritivas de contexto:

* **Tabela Fato (`fVendas`):**
  * **Granularidade:** Item/pedido faturado por data, cliente, produto e vendedor.
  * **Métricas:** Valor de Venda (`R$ 201,52 Mi`), Custo (`R$ 95,47 Mi`), Frete (`R$ 7,85 Mi`), Lucro (`R$ 106,05 Mi`) e Quantidade de Pedidos (`200.566`).
* **Tabelas Dimensão:**
  * `dCalendario`: Data, Ano (2019–2022), Mês/Ano e hierarquias temporais.
  * `dClientes`: ID Cliente, Nome, Grupo de Cliente, Cidade e Estado (base de `9.274` clientes ativos).
  * `dProdutos`: ID Produto, Nome do Produto, Categoria (46 produtos em 6 categorias), Status de Disponibilidade e URL de imagem.
  * `dEquipeComercial`: Vendedor, Supervisor e Unidade de Negócio (*Diamante, Ametista, Rubi, Esmeralda, Topázio*).


                  [ dCalendario ]
                         |
                         | (1:N)
                         v
[ dClientes ] --(1:N)--> [ fVendas ] <--(1:N)-- [ dProdutos ]
                         ^
                         | (1:N)
                         |
               [ dEquipeComercial ]

## 5. Arquivos Técnicos do Projeto
* [Amostra de Dados (CSV)](./dados/amostra_fvendas.csv) e [Dicionário de Dados](./dados/dicionario_dados.md)
* [Modelagem Dimensional (Star Schema)](./modelagem/star_schema.md)
* [Consultas SQL Analíticas](./sql)
* [Medidas DAX](./dax/medidas_principais.dax)
* [Documentação de ETL (Power Query)](./documentacao/etl_power_query.md)
