# Metodologia

## 1. Preparação dos dados

Os dados foram criados e organizados no Google Sheets e posteriormente armazenados em um arquivo Excel.

O dataset foi estruturado em quatro tabelas:

- PRODUTOS
- CLIENTES
- PEDIDOS
- ENTREGAS

## 2. Análise com Python

Os dados foram analisados utilizando Python, principalmente com Pandas e Matplotlib.

Foram analisados:

- faturamento total;
- ticket médio;
- produtos mais vendidos;
- faturamento por região;
- quantidade de entregas;
- entregas atrasadas.

Também foram criadas visualizações para apoiar a interpretação dos resultados.

## 3. Modelagem no Power BI

As quatro tabelas foram importadas para o Power BI e relacionadas por suas chaves:

- CLIENTES -> (chave clientes_id) -> PEDIDOS
- PEDIDOS (chave pedido_id) -> ENTREGAS

## 4. Medidas DAX

Foram criadas medidas para calcular o ticket médio, entregas atrasadas e identificar os cinco produtos mais vendidos.

### Ticket Médio

```DAX
TicketMedioPedidos =
DIVIDE(
    SUM(PEDIDOS[valor_total]),
    DISTINCTCOUNT(PEDIDOS[pedido_id])
)
```

### Entregas Atrasadas

```DAX
Entregas Atrasadas =
CALCULATE(
    COUNTROWS(ENTREGAS),
    ENTREGAS[status_entrega] = "Atrasada"
)
```

### Top 5 Produtos

```DAX
Top 5 Produtos =
VAR RankingProduto =
    RANKX(
        ALL(PRODUTOS[produto_nome]),
        CALCULATE(SUM(PEDIDOS[quantidade])),
        ,
        DESC
    )
RETURN
    IF(
        RankingProduto <= 5,
        SUM(PEDIDOS[quantidade])
    )
```

## 5. Dashboard

O dashboard foi desenvolvido em uma única página, contendo quatro indicadores e três visualizações:

### Indicadores

- Faturamento Total
- Total de Pedidos
- Ticket Médio
- Entregas Atrasadas

### Visualizações

- **Top 5 Produtos Mais Vendidos** — gráfico de barras clusterizado
- **Faturamento por Região** — gráfico de colunas clusterizado
- **Status das Entregas** — gráfico de rosca

O dashboard foi organizado com foco em uma apresentação simples e objetiva dos principais resultados da análise.