
# Guia de Aprendizado do Modelo de Vendas e Metas no Power BI

Este repositório contém um modelo de dados no Power BI projetado para analisar dados de vendas e metas dos vendedores. O modelo integra detalhes do produto, transações de vendas, informações do vendedor e dados temporais para fornecer um ambiente rico para análise e relatórios de vendas.

## Estrutura do Modelo

O modelo consiste nas seguintes tabelas:

- `dProduto`: Contém informações sobre os produtos.
- `dCalendario`: Uma tabela de dimensão de tempo para análise temporal.
- `dVendedor`: Detalha informações sobre os vendedores.
- `fVendas`: Tabela fato que registra as vendas transacionais.
- `fMeta`: Registra as metas de vendas dos vendedores.

## Relacionamentos do Modelo

As tabelas estão relacionadas da seguinte maneira:

- `dProduto` ↔ `fVendas`: Um produto pode estar em várias vendas.
- `dCalendario` ↔ `fVendas`: As vendas são registradas com uma data específica.
- `dVendedor` ↔ `fVendas` e `dVendedor` ↔ `fMeta`: Um vendedor pode ter várias vendas e várias metas.

## Sugestões de Melhorias no Modelo

- Certifique-se de que as relações estejam corretamente definidas para a granularidade dos dados.
- Considere adicionar uma tabela de dimensão para clientes, se relevante.
- Inclua categorias de produtos e regiões de vendedores para análises mais detalhadas.
- Mantenha a integridade do modelo, verificando e limpando dados duplicados ou inconsistentes.

## Métricas e KPIs Sugeridos

Utilize as seguintes métricas DAX para análises:

- `Total de Vendas`:
  ```dax
  Total de Vendas = SUMX(fVendas, fVendas[Quantidade] * fVendas[PrecoUnitario])
