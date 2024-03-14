
# Modelo de Soluções para aprendizado em Power BI

Este modelo de dados no Power BI é exemplo projetado para analisar dados de vendas e metas dos vendedores. O modelo integra detalhes do produto, transações de vendas, informações do vendedor e dados temporais para fornecer um ambiente rico para análise e relatórios de vendas.

## Estrutura do Modelo

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

 ## Diagrama do Modelo 
 vendas_vs_metas
/Diagrama_Dados.png

## Dicas Extras

- Certifique-se de que as relações estejam corretamente definidas para a granularidade dos dados.
- Considere adicionar uma tabela de dimensão para clientes, se relevante.
- Inclua categorias de produtos e regiões de vendedores para análises mais detalhadas.
- Mantenha a integridade do modelo, verificando e limpando dados duplicados ou inconsistentes.

## Métricas do Modelo

PS: YoY(Year-over-Year) Significa variação anual de uma métrica

- `Faturamento`:
  ```dax
  Faturamento = SUMX(fVendas, fVendas[QtdItens] * fVendas[PrecoUnitario])
  
- `% Faturamento YoY`:
  ```dax
  % Faturamento YoY = 
  VAR varFaturamentoLY = 
  CALCULATE(
    [Faturamento],
    SAMEPERIODLASTYEAR(dCalendario[Data])
  )
  RETURN
  IF(
    ISBLANK(DIVIDE([Faturamento] - varFaturamentoLY, varFaturamentoLY)),
    "-",
    DIVIDE([Faturamento] - varFaturamentoLY, varFaturamentoLY)
  )

- `% Margem YoY`:
  ```dax
  % Margem YoY = 
  VAR varMargemLY = 
  CALCULATE(
    [Margem Bruta],
    SAMEPERIODLASTYEAR(dCalendario[Data])
  )
  RETURN
  IF(
    ISBLANK(DIVIDE([Margem Bruta] - varMargemLY, varMargemLY)),
    "-",
    DIVIDE([Margem Bruta] - varMargemLY, varMargemLY)
  )

- `% Notas Emitidas YoY`:
  ```dax
  % Notas Emitidas YoY = 
  VAR varQtdVendidaLY = 
  CALCULATE(
    [Notas Emitidas],
    SAMEPERIODLASTYEAR(dCalendario[Data])
  )
  VAR vVar = DIVIDE([Notas Emitidas] - varQtdVendidaLY, varQtdVendidaLY)
  RETURN
  IF(
    ISBLANK(vVar),
    "-",
    vVar
  )
  
- `Custos`:
  ```dax
     Custos = 
     SUMX(
      fVendas, 
      fVendas[QtdItens] * RELATED(dProduto[CustoUnitario])
         )

- `Margem Bruta`:
  ```dax
     Margem Bruta = [Faturamento]-[Custos]

- `QTD de Notas Emitidas`:
  ```dax
     Notas Emitidas = DISTINCTCOUNT(fVendas[NFe]

- `Ticket Médio`:
  ```dax
     Ticket Médio = DIVIDE([Faturamento],[Notas Emitidas])

- `Meta de Faturamento`:
  ```dax
     % Meta Faturamento = 
		DIVIDE(
			[Faturamento], 
			SUM(fMeta[Meta Faturamento])
		)

- `% Meta Margem`:
  ```dax
     % Meta Margem = 
		DIVIDE(
		[Margem Bruta], 
		SUM(fMeta[Meta Margem Bruta]))

- `% Meta Notas Emitidas`:
  ```dax
     % Meta Notas Emitidas = 
		DIVIDE(
		[Notas Emitidas], 
		SUM(fMeta[Meta Notas Emitidas]))

- `Rank de Vendedores`:
  ```dax
	 Rank Vendedor = 
	 RANKX( ALL(dVendedor),[Medida Switch])
