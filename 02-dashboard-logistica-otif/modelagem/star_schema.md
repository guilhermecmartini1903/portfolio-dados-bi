# Modelagem Dimensional — Torre de Controle Logística

Modelo **Star Schema** projetado para cruzar indicadores de pontualidade (OTD), completude (In Full) e desvios operacionais por transportadora, CD de origem e cliente.

```text
               +-------------------+
               |    dCalendario    |
               +-------------------+
               | PK: data          |
               | ano               |
               | mes_ano           |
               +---------+---------+
                         | 1
                         |
                         | N
+--------------+   1   +-v-----------------+   N   1 +-------------------+
|  dWarehouse  +------>|     fEntregas     |<--------+  dTransportadora  |
+--------------+       +-------------------+         +-------------------+
| PK: id_cd    |       | PK: num_nf        |         | PK: id_transp     |
| nome_cd      |       | FK: data_fat      |         | nome_transp       |
| uf_origem    |       | FK: id_cd         |         +-------------------+
+--------------+       | FK: id_transp     |
                       | FK: id_cliente    |
                       | qtd_volumes       |
                       | valor_nf          |
                       | flag_on_time      |
                       | flag_in_full      |
                       | status_desvio     |
                       +---------+---------+
                                 | N
                                 |
                                 | 1
                       +---------v---------+
                       |     dCliente      |
                       +-------------------+
                       | PK: id_cliente    |
                       | nome_cliente      |
                       | regiao            |
                       +-------------------+
