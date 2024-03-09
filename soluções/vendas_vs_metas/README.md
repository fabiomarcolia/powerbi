
# Modelo de Soluções para aprendizado em Power BI

Este repositório contém modelos de dados no Power BI com o objetivo de compartilhar com a comunidade conhecimento e contribuir com a aprendizagem de criação de Soluções de Business Intelligence para Tomada de Decisão.

## Modelos Disponíveis

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
