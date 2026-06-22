# 📊 Dashboard de Análise de Desempenho e Entrega Logística

Solução de BI de Ponta a Ponta com Excel 2016 (Power Query & Power Pivot)
🎯 Objetivo do Projeto
Este ecossistema de Business Intelligence foi desenvolvido para analisar gargalos logísticos, padrões de consumo e a saúde financeira de uma operação global de vendas
. O foco central é identificar a causa raiz de atrasos e fornecer uma visão limpa da eficiência operacional, eliminando ruídos causados por falhas sistêmicas de registro [Conversation History].
🏗️ Arquitetura de Dados (Star Schema)
O projeto utiliza uma modelagem dimensional para garantir performance e integridade dos dados
:
F_Vendas_Logistica (Fato): Centraliza métricas de vendas, lucro, quantidades e o status de atraso (label)
.
D_Clientes: Atributos dos consumidores (Segmento) e localização da loja
.
D_Produtos: Catálogo detalhado por Departamentos e Categorias
.
D_Destino: Geografia completa da entrega (Mercado, Região, País e Cidade)
.
D_Calendario: Inteligência temporal (Ano, Mês, Nome do Mês) criada via Power Query
.
🛠️ Engenharia de Dados: Colunas Adicionadas
Para viabilizar as análises, foram criadas colunas calculadas via DAX no Power Pivot:
lead_time_days: Calcula a diferença bruta entre shipping_date e order_date [Conversation History].
lead_time_days_Positive: Corrige erros de cálculo onde a data de envio era anterior à do pedido, garantindo que o cálculo de média ignore valores negativos [Conversation History].
Shipping_Range: Categoriza os dias de envio em "buckets" (0-2 dias, 3-5 dias, etc.) para a criação do Histograma [Conversation History].
Data_Quality_Detail (Status de Qualidade):
Por que criamos: Identificamos discrepâncias críticas na base, como recordes de 1430 dias de atraso e -1429 dias de antecipação [Conversation History]. Sem esta coluna, a média geral de 57,4 dias estaria severamente distorcida [Conversation History].
Função: Atua como um "Slicer de Auditoria", permitindo ao gestor escolher entre ver a "Realidade Operacional" (dados limpos) ou os "Erros de Sistema" (para correção pela equipe de TI) [Conversation History].
📐 Medidas DAX Principais
Implementadas para garantir precisão transacional (evitando contagem duplicada de itens):
Total de Pedidos Únicos: =DISTINCTCOUNT(F_Vendas_Logistica[order_id]) [Conversation History].
Média Geral de Dias de Envio: =AVERAGE(F_Vendas_Logistica[lead_time_days_Positive]) [Conversation History].
Taxa Geral de Atraso: Proporção de pedidos onde label = 1
.
Volume Total de Itens: =SUM(F_Vendas_Logistica[order_item_quantity]) [Conversation History].
Total de Entregas (Linhas): =COUNTROWS(F_Vendas_Logistica) [Conversation History].
🖥️ Estrutura do Dashboard (4 Páginas)
Página 1: Análise de Vendas e Mercado
Foco: Desempenho Comercial.
Tendência de Vendas por Mês (Linha): Identifica sazonalidade e picos de demanda
.
Popularidade por Departamento (Barras): Revela quais setores (ex: Footwear, Apparel) geram mais receita
.
Distribuição por Segmento de Cliente (Pizza): Analisa o peso de consumidores Corporate vs Consumer
.
Top 10 Cidades de Destino (Barras): Foca os esforços comerciais nos mercados mais ativos
.
Página 2: Fatores de Atraso e Logística
Foco: Identificação de Gargalos.
Taxa de Atraso por País (Barras): Identifica quais nações possuem problemas alfandegários ou de infraestrutura
.
Atraso por Departamento/Categoria (Barras): Mostra se produtos específicos (ex: móveis pesados) atrasam mais que itens leves
.
Atraso por Status do Pedido (Pizza): Identifica se o atraso ocorre na separação (Processing) ou no envio (Shipping)
.
Atrasos por Segmento e Pagamento (Barras): Revela correlação entre métodos de pagamento lentos (ex: Boleto/Transferência) e atrasos no despacho
.
Página 3: Detalhamento dos Dias de Envio (Lead Time)
Foco: Eficiência de Transporte.
Média de Dias por Modo de Envio (Barras): Valida se o frete First Class está sendo entregue mais rápido que o Standard
.
Histograma de Frequência (Barras): Visualiza a "mancha" de entregas, provando que a maioria é rápida e a média é alta apenas por outliers [Conversation History].
Top Cidades com Maior Lead Time (Barras): Localiza geograficamente as rotas mais ineficientes
.
Página 4: Análise de Pedidos e Comportamento
Foco: Operação e Fraude.
Status do Pedido (Rosca): Monitoramento crítico de saúde, destacando pedidos cancelados ou com Suspeita de Fraude (SUSPECTED_FRAUD) [1, 23, Conversation History].
Preferência de Pagamento (Barras): Ajuda na negociação de taxas com operadoras de cartão e bancos [1, 19, Conversation History].
Média de Itens por Pedido (Cartão): Indica o comportamento do carrinho de compras e eficiência de cross-selling [Conversation History].
🚀 Sugestão de Melhoria Sênior
Para um design verdadeiramente "Clean", utilize uma Barra Lateral de Slicers (Segmentadores) sincronizados [Conversation History]. Garanta que o filtro de Status de Qualidade esteja presente em todas as páginas para que o usuário nunca tome decisões baseadas nos dados "sujos" de 1430 dias de atraso [Conversation History].
Desenvolvido por [Seu Nome] Especialista em BI & Analytics
