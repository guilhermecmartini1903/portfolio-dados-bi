# Dicionário de Dados — Lets-Cola Company

Base estruturada para consolidação comercial, financeira e de portfólio (período de 2019 a 2022).

| Tabela | Coluna | Tipo | Descrição |
| :--- | :--- | :--- | :--- |
| `fVendas` | `id_pedido` | INT | Identificador único do pedido faturado |
| `fVendas` | `data_pedido` | DATE | Data de faturamento (chave para `dCalendario`) |
| `fVendas` | `id_cliente` | VARCHAR | Chave estrangeira do cliente (`dClientes`) |
| `fVendas` | `id_produto` | VARCHAR | Chave estrangeira do SKU (`dProdutos`) |
| `fVendas` | `id_vendedor` | VARCHAR | Chave estrangeira da equipe comercial (`dEquipeComercial`) |
| `fVendas` | `valor_venda` | DECIMAL | Receita bruta da linha do pedido (R$) |
| `fVendas` | `custo_produto` | DECIMAL | Custo direto dos produtos vendidos (R$) |
| `fVendas` | `valor_frete` | DECIMAL | Custo logístico alocado ao pedido (R$) |
| `dProdutos` | `categoria` | VARCHAR | Bebidas, Snacks, Matinais, Doces, Chás ou Energéticos |
| `dProdutos` | `disponivel` | BOOLEAN | Status de disponibilidade ativa no portfólio |
| `dClientes` | `grupo_cliente` | VARCHAR | Pequeno Porte, Tradicional, Redes Regionais, Atacados, Atacarejo, Food Services |
| `dEquipeComercial` | `unidade_negocio` | VARCHAR | Diamante, Ametista, Rubi, Esmeralda ou Topázio |
