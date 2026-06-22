# Dashboard-de-Analise-de-Desempenho-e-Entrega-Logistica
📊 Solução de Business Intelligence com Excel 2016 (Power Query e Power Pivot)
🎯 Objetivo do Projeto
Este projeto visa analisar os gargalos de entrega (atrasos), identificar padrões geográficos e comerciais e entender a saúde financeira das operações globais de uma empresa de logística e vendas
. O desafio central foi extrair inteligência de uma base de dados com inconsistências sistêmicas (outliers de data), transformando-a em um ecossistema de decisão focado em Lead Time e Eficiência Operacional [11, Conversation History].
🏗️ Arquitetura de Dados (Star Schema)
Para garantir a performance e a escalabilidade no Excel 2016, a base foi modelada seguindo o padrão Star Schema (Fato/Dimensão)
:
F_Vendas_Logistica (Fato): Registra métricas como vendas, lucro, quantidades e o status de atraso (label)
.
D_Clientes: Detalhes do perfil (Segmento) e localização da compra
.
D_Produtos: Catálogo detalhado por Departamentos e Categorias
.
D_Destino: Geografia completa da entrega (Mercado, Região e País)
.
D_Calendario: Inteligência temporal criada no Power Query a partir de order_date
.
🛠️ Tecnologias Utilizadas
Excel 2016 "Puro"
.
Power Query (ETL): Tratamento de dados, normalização e criação do modelo relacional
.
Power Pivot (Data Modeling): Criação de medidas DAX e relacionamentos [15, Conversation History].
📈 Estrutura do Dashboard (4 Páginas)
Página 1: Análise de Vendas e Mercado
Foco no desempenho comercial global
.
KPIs: Total de Vendas, Ticket Médio e Total de Pedidos
.
Visuais: Popularidade por Departamento, Distribuição por Segmento de Cliente e Tendência Mensal
.
Página 2: Fatores de Atraso e Logística
Diagnóstico de causa raiz para falhas de entrega
.
KPIs: Taxa Geral de Atraso (proporção de label = 1)
.
Insights: Atrasos por Status do Pedido, Categoria, Departamento e País de destino
.
Página 3: Detalhamento dos Dias de Envio (Lead Time)
Análise granular do tempo de transporte
.
KPIs: Média de Dias de Envio, Recorde de Atraso e Média para pedidos atrasados
.
Análise Operacional: Eficiência por Modo de Envio (shipping_mode) e histograma de frequência de prazos [18, Conversation History].
Página 4: Análise de Pedidos e Comportamento
Saúde do funil de vendas e perfil transacional [1, Conversation History].
KPIs: Total de Pedidos Únicos, Média de Itens por Pedido e Volume de Itens [Conversation History].
Visuais: Volume mensal, Status do Pedido (incluindo Suspeita de Fraude) e Preferência de Pagamento [1, Conversation History].
💡 Diferencial Técnico: Data Quality & Outliers
Um dos maiores valores deste projeto foi o tratamento de Qualidade de Dados. Identificamos registros com 1430 dias de atraso e -1429 dias de antecipação, indicadores de erros sistêmicos [Conversation History].
Foi implementada uma coluna calculada de Status de Qualidade (Data_Quality_Detail) que permite ao usuário filtrar o dashboard entre:
Dados Operacionais: Realidade logística limpa para tomada de decisão.
Erros Sistêmicos: Auditoria para a equipe de TI corrigir a base original [Conversation History].
📂 Como Explorar este Repositório
Dashboard_Logistica_Vendas.xlsx: Arquivo principal com o modelo de dados e visuais.
Scripts_PowerQuery/: Documentação da lógica de ETL aplicada.
Calculos_DAX/: Lista das medidas principais (Total Pedidos Únicos, Taxa de Atraso, etc.).
