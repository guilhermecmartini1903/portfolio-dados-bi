# Modelagem Dimensional — Star Schema (Lets-Cola)

O modelo relacional separa transações numéricas (`fVendas`) dos atributos descritivos em 4 dimensões principais, com relacionamentos **1:N** (um para muitos) unidirecionais.

```text
                  +-------------------+
                  |    dCalendario    |
                  +-------------------+
                  | PK: data          |
                  | ano               |
                  | mes_ano           |
                  | trimestre         |
                  +---------+---------+
                            | 1
                            |
                            | N
+-----------------+   1   +-v-----------------+   N   1 +-------------------+
|    dClientes    +------>|      fVendas      |<--------+     dProdutos     |
+-----------------+       +-------------------+         +-------------------+
| PK: id_cliente  |       | FK: data_pedido   |         | PK: id_produto    |
| nome_cliente    |       | FK: id_cliente    |         | nome_produto      |
| grupo_cliente   |       | FK: id_produto    |         | categoria         |
| cidade / estado |       | FK: id_vendedor   |         | disponivel        |
+-----------------+       | valor_venda       |         | url_imagem        |
                          | custo_produto     |         +-------------------+
                          | valor_frete       |
                          | qtd_itens         |
                          +---------+---------+
                                    | N
                                    |
                                    | 1
                          +---------v---------+
                          | dEquipeComercial  |
                          +-------------------+
                          | PK: id_vendedor   |
                          | nome_vendedor     |
                          | supervisor        |
                          | unidade_negocio   |
                          +-------------------+
