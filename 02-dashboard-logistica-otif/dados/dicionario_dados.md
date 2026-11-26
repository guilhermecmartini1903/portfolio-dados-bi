# Dicionário de Dados — Torre de Controle Logística

Base de acompanhamento de notas fiscais, prazos de entrega (SLA) e ocorrências operacionais (2021 a 2022).

| Tabela | Coluna | Tipo | Descrição |
| :--- | :--- | :--- | :--- |
| `fEntregas` | `num_nf` | VARCHAR | Número da Nota Fiscal emitida |
| `fEntregas` | `data_faturamento` | DATE | Data de emissão e expedição da carga |
| `fEntregas` | `data_previsao` | DATE | Data limite acordada em SLA com a transportadora |
| `fEntregas` | `data_entrega` | DATE | Data real da baixa/entrega no cliente |
| `fEntregas` | `qtd_volumes` | INT | Quantidade de volumes físicos embarcados |
| `fEntregas` | `qtd_pedida` | INT | Quantidade de unidades solicitadas no pedido |
| `fEntregas` | `qtd_entregue` | INT | Quantidade efetivamente entregue sem avaria/falta |
| `fEntregas` | `valor_nf` | DECIMAL | Valor financeiro da mercadoria transportada (R$) |
| `fEntregas` | `status_desvio` | VARCHAR | Classificação operacional (`Normal` ou `Desvio Operacional`) |
| `dTransportadora` | `transportadora` | VARCHAR | Parceiro logístico responsável pelo frete |
| `dWarehouse` | `warehouse_origem` | VARCHAR | Centro de distribuição de origem da carga |
| `dCliente` | `regiao` | VARCHAR | Macrorregião de destino (Centro-Oeste, Nordeste, Norte, Sudeste, Sul) |
