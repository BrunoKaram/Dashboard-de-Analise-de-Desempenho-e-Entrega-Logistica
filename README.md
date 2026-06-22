<p align="center">
  <img src="Imagens/Página%201%20Análise%20de%20Vendas%20e%20Mercado.png" width="900">
</p>

<h1 align="center">
📊 Dashboard de Análise de Desempenho e Entrega Logística
</h1>

<p align="center">
Business Intelligence • Excel • Power Query • Power Pivot • DAX
</p>

> Solução de Business Intelligence desenvolvida em Excel 2016 utilizando Power Query, Power Pivot e DAX.

---

# 🎯 Objetivo do Projeto

Este ecossistema de Business Intelligence foi desenvolvido para analisar gargalos logísticos, padrões de consumo e a saúde financeira de uma operação global de vendas.

O foco central é identificar a causa raiz de atrasos e fornecer uma visão limpa da eficiência operacional, eliminando ruídos causados por falhas sistêmicas de registro [Conversation History].

---

# 🏗️ Arquitetura de Dados (Star Schema)

O projeto utiliza uma modelagem dimensional para garantir performance e integridade dos dados.

## Modelo de Dados

![O Modelo de Dados (Star Schema)](<Imagens/O%20Modelo%20de%20Dados%20(Star%20Schema).png>)

### Tabela Fato

| Tabela                 | Descrição                                                                       |
| ---------------------- | ------------------------------------------------------------------------------- |
| **F_Vendas_Logistica** | Centraliza métricas de vendas, lucro, quantidades e o status de atraso (label). |

### Tabelas Dimensão

| Tabela           | Descrição                                                             |
| ---------------- | --------------------------------------------------------------------- |
| **D_Clientes**   | Atributos dos consumidores (Segmento) e localização da loja.          |
| **D_Produtos**   | Catálogo detalhado por Departamentos e Categorias.                    |
| **D_Destino**    | Geografia completa da entrega (Mercado, Região, País e Cidade).       |
| **D_Calendario** | Inteligência temporal (Ano, Mês, Nome do Mês) criada via Power Query. |

---

# 🛠️ Engenharia de Dados: Colunas Adicionadas

Para viabilizar as análises, foram criadas colunas calculadas via DAX no Power Pivot:

### 📅 lead_time_days

Calcula a diferença bruta entre `shipping_date` e `order_date` [Conversation History].

### ✅ lead_time_days_Positive

Corrige erros de cálculo onde a data de envio era anterior à do pedido, garantindo que o cálculo de média ignore valores negativos [Conversation History].

### 📊 Shipping_Range

Categoriza os dias de envio em "buckets" (0-2 dias, 3-5 dias, etc.) para a criação do Histograma [Conversation History].

### 🔍 Data_Quality_Detail (Status de Qualidade)

#### Por que criamos?

Identificamos discrepâncias críticas na base, como recordes de 1430 dias de atraso e -1429 dias de antecipação [Conversation History].

Sem esta coluna, a média geral de 57,4 dias estaria severamente distorcida [Conversation History].

#### Função

Atua como um "Slicer de Auditoria", permitindo ao gestor escolher entre ver a **"Realidade Operacional" (dados limpos)** ou os **"Erros de Sistema" (para correção pela equipe de TI)** [Conversation History].

---

# 📐 Medidas DAX Principais

Implementadas para garantir precisão transacional (evitando contagem duplicada de itens):

![Medidas DAX](Imagens/Medidas%20DAX%20.png)

### Total de Pedidos Únicos

```DAX
=DISTINCTCOUNT(F_Vendas_Logistica[order_id])
```

### Média Geral de Dias de Envio

```DAX
=AVERAGE(F_Vendas_Logistica[lead_time_days_Positive])
```

### Taxa Geral de Atraso

Proporção de pedidos onde:

```DAX
label = 1
```

### Volume Total de Itens

```DAX
=SUM(F_Vendas_Logistica[order_item_quantity])
```

### Total de Entregas (Linhas)

```DAX
=COUNTROWS(F_Vendas_Logistica)
```

---

# 🖥️ Estrutura do Dashboard

---

# 📈 Página 1: Análise de Vendas e Mercado

**Foco:** Desempenho Comercial.

- Tendência de Vendas por Mês (Linha): Identifica sazonalidade e picos de demanda.
- Popularidade por Departamento (Barras): Revela quais setores (ex: Footwear, Apparel) geram mais receita.
- Distribuição por Segmento de Cliente (Pizza): Analisa o peso de consumidores Corporate vs Consumer.
- Top 10 Cidades de Destino (Barras): Foca os esforços comerciais nos mercados mais ativos.

![Página 1 - Análise de Vendas e Mercado](Imagens/Página%201%20Análise%20de%20Vendas%20e%20Mercado.png)

---

# 🚚 Página 2: Fatores de Atraso e Logística

**Foco:** Identificação de Gargalos.

- Taxa de Atraso por País (Barras): Identifica quais nações possuem problemas alfandegários ou de infraestrutura.
- Atraso por Departamento/Categoria (Barras): Mostra se produtos específicos (ex: móveis pesados) atrasam mais que itens leves.
- Atraso por Status do Pedido (Pizza): Identifica se o atraso ocorre na separação (Processing) ou no envio (Shipping).
- Atrasos por Segmento e Pagamento (Barras): Revela correlação entre métodos de pagamento lentos (ex: Boleto/Transferência) e atrasos no despacho.

![Página 2 - Fatores de Atraso e Logística](Imagens/Página%202%20Fatores%20de%20Atraso%20e%20Logística.png)

---

# ⏱️ Página 3: Detalhamento dos Dias de Envio (Lead Time)

**Foco:** Eficiência de Transporte.

- Média de Dias por Modo de Envio (Barras): Valida se o frete First Class está sendo entregue mais rápido que o Standard.
- Histograma de Frequência (Barras): Visualiza a "mancha" de entregas, provando que a maioria é rápida e a média é alta apenas por outliers [Conversation History].
- Top Cidades com Maior Lead Time (Barras): Localiza geograficamente as rotas mais ineficientes.

![Página 3 - Detalhamento dos Dias de Envio (Lead Time)](<Imagens/Página%203%20Detalhamento%20dos%20Dias%20de%20Envio%20(Lead%20Time).png>)

---

# 📦 Página 4: Análise de Pedidos e Comportamento

**Foco:** Operação e Fraude.

- Status do Pedido (Rosca): Monitoramento crítico de saúde, destacando pedidos cancelados ou com Suspeita de Fraude (SUSPECTED_FRAUD) [1, 23, Conversation History].
- Preferência de Pagamento (Barras): Ajuda na negociação de taxas com operadoras de cartão e bancos [1, 19, Conversation History].
- Média de Itens por Pedido (Cartão): Indica o comportamento do carrinho de compras e eficiência de cross-selling [Conversation History].

![Página 4 - Análise de Pedidos e Comportamento](Imagens/Página%204%20Análise%20de%20Pedidos%20e%20Comportamento.png)

---

# 🚀 Principais Diferenciais do Projeto

- Modelagem dimensional (Star Schema)
- ETL utilizando Power Query
- Métricas desenvolvidas em DAX
- Auditoria de qualidade dos dados
- Identificação de gargalos logísticos
- Análise operacional e financeira integrada
- Dashboard executivo com 4 páginas analíticas
