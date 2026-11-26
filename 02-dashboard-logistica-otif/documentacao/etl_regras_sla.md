# Documentação de ETL e Regras de SLA Logístico

Tratamentos e regras de negócio aplicadas no Power Query para a Torre de Controle de Transportes:

1. **Cálculo de Lead Time e SLA:** Criação de coluna condicional comparando `data_entrega` com `data_previsao` para classificar automaticamente cada embarque em `On Time` (`<= previsão`) ou `Atraso` (`> previsão`).
2. **Validação de Completude (`In Full`):** Comparação entre `qtd_entregue` e `qtd_pedida` para identificar cortes de pedido, faltas ou avarias no transporte.
3. **Padronização de Ocorrências:** Agrupamento de códigos de ocorrência de transporte (ex.: reentrega, recusa, avaria, atraso de coleta) na dimensão binária `Normal` vs. `Desvio Operacional`.
4. **Normalização Geográfica e de Parceiros:** Padronização dos nomes das transportadoras, centros de distribuição (`Warehouse Origem`) e macrorregiões do Brasil.
