# Documentação de ETL e Tratamento (Power Query)

Etapas aplicadas durante a preparação das bases para o modelo analítico da Lets-Cola:

1. **Padronização de Tipos e Datas:** Conversão explícita de colunas monetárias para número decimal fixo (`Currency`) e datas de faturamento para o tipo `Date` no padrão ISO.
2. **Limpeza de Textos e Categorias:** Aplicação de `Text.Trim` e `Text.Proper` nos nomes de vendedores, supervisores, cidades e grupos de clientes para evitar fragmentação em filtros e rankings.
3. **Tratamento de Nulos:** Substituição de valores nulos em `valor_frete` por `0` (casos de retirada local) e filtragem de registros sem `id_pedido` válido.
4. **Enriquecimento do Catálogo (`dProdutos`):** Validação das URLs de imagens dos 46 produtos e criação da coluna booleana de disponibilidade (`Em Portfólio` vs. `Indisponível`).
5. **Desnormalização Controlada:** Extração de tabelas dimensão únicas (`Remove Duplicates` nas chaves primárias) a partir de planilhas transacionais brutas.
