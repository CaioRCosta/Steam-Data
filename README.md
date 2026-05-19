# Steam Data Insights: Uma Análise Orientada a Dados do Mercado de Games

## Objetivo do Projeto
Este projeto investiga os fatores que impulsionam o sucesso, a retenção e a monetização no ecossistema da Steam. Guiado pela metodologia CRISP-DM (Cross-Industry Standard Process for Data Mining) e utilizando um conjunto de dados com mais de 120.000 títulos, aplicou-se técnicas de Ciência de Dados e Aprendizado de Máquina para desmistificar suposições comuns do mercado por meio de evidências empíricas.

## Stack Tecnológico e Mapeamento da Metodologia CRISP-DM
O ciclo de vida do projeto foi governado pelas fases do framework CRISP-DM, garantindo o alinhamento entre as necessidades do negócio e as decisões de engenharia de dados:

1. **Entendimento do Negócio:** Formulação de hipóteses comerciais sobre a elasticidade do preço, o impacto real da localização global, a percepção de valor de conteúdos adicionais e as dinâmicas de retenção de utilizadores.
2. **Entendimento e Preparação dos Dados:** Análise exploratória inicial e execução de um pipeline de ETL para limpeza de valores nulos, conversão de tipos de dados e engenharia de atributos sobre mais de 120.000 registos.
3. **Modelagem e Avaliação:** Aplicação de modelos estatísticos de regressão e algoritmos de agrupamento espacial para segmentar o catálogo da plataforma e validar as hipóteses de negócio levantadas.

### Tecnologias Utilizadas
* Linguagem: Python
* ETL e Manipulação de Dados: Pandas
* Visualização Analítica: Seaborn e Matplotlib
* Aprendizado de Máquina: Scikit-Learn

## Estrutura do Pipeline e Insights de Negócio

### Módulo 1: Preparação de Dados e Engenharia de Atributos (ETL)
Fase inicial dedicada à ingestão, filtragem e tratamento de inconsistências nas variáveis críticas do ecossistema Steam. Foram calculadas novas métricas de engajamento, como o volume total de revisões e a percentagem real de aprovação de cada título, gerando uma base consolidada para as análises subsequentes.

### Módulo 2: Localização (Quantidade de Idiomas)
A análise mapeou como a quantidade de idiomas suportados influencia a taxa de aprovação dos utilizadores. Identificou-se um ponto ideal (sweet spot) entre 7 e 9 idiomas, correspondente ao pacote de localização global básico. Oferecer suporte a um volume excessivo de línguas não demonstrou crescimento linear de satisfação, indicando possíveis problemas de controlo de qualidade em traduções muito amplas.

<div align="center">
  <img src="images/idiomas_sucesso.png" alt="Impacto da Quantidade de Idiomas na Aprovação" width="800">
</div>

### Módulo 3: O Impacto Comercial dos Idiomas (Filtro de Qualidade)
Aprofundando a localização, avaliou-se o retorno financeiro mediano estimado para cada idioma individualmente. O resultado apontou que o Inglês apresenta a menor mediana de revisões da plataforma, por ser o padrão de projetos de baixo orçamento que acumulam pouca tração. Em contrapartida, idiomas como Polonês, Italiano, Chinês Tradicional e Português (Brasil) lideram o ranking. Essa presença funciona como um indicador de qualidade: apenas estúdios com orçamento estruturado e planeamento de mercado investem na localização para mercados específicos, o que se correlaciona a volumes de vendas significativamente maiores.

<div align="center">
  <img src="images/idiomas_vendas.png" alt="Mediana de Vendas por Idioma" width="800">
</div>

### Módulo 4: A Ilusão da Média vs. A Realidade da Mediana (Tempo de Jogo)
Demonstrou-se estatisticamente o risco de avaliar a retenção de utilizadores utilizando apenas a média. Gêneros Casuais apresentam uma média inflada artificialmente por títulos no estilo "idle" ou contas mantidas ativas exclusivamente para o comércio de cartas colecionáveis da plataforma. A análise da Mediana revelou o comportamento do consumidor padrão: géneros densos como RPG e Estratégia lideram o engajamento real, exigindo e sustentando a atenção orgânica do público após o período inicial.

<div align="center">
  <img src="images/retencao_media_mediana.png" alt="Média vs Mediana de Tempo Jogado por Gênero" width="800">
</div>

### Módulo 5: Crítica Especializada vs. A Voz da Comunidade
O cruzamento das avaliações do Metacritic com a aprovação dos utilizadores via regressão linear demonstrou uma convergência geral na indústria. No entanto, o modelo identificou duas categorias de exceções comerciais relevantes:
* Cult Classics: Jogos com receção mediana pela mídia especializada, mas que atingem patamares de 90%+ de aprovação por comunidades de nicho altamente engajadas.
* Review Bombing: Títulos aclamados pela crítica que sofrem rejeição massiva do público consumidor devido a problemas técnicos no lançamento ou políticas predatórias de monetização pós-lançamento.

<div align="center">
  <img src="images/metacritic_comunidade.png" alt="Metacritic vs Aprovação dos Jogadores" width="800">
</div>

### Módulo 6.1: Elasticidade de Preço e Percepção de Valor
A distribuição do Pico de Jogadores Simultâneos (Peak CCU) sob escala logarítmica confirmou que títulos gratuitos concentram picos de acessos em massa. Contudo, jogos precificados em faixas premium (entre 60 e 80 USD) mantêm volumes elevados de utilizadores ativos de maneira consistente. A barreira de preço elevado não inibe o engajamento de mercado, desde que o escopo e a entrega do produto justifiquem o investimento do consumidor, como ocorre no padrão de títulos AAA.

<div align="center">
  <img src="images/preco_pico.png" alt="Preço vs Pico de Jogadores" width="800">
</div>

### Módulo 6.2: O Paradoxo das DLCs na Taxa de Aprovação
Contrariando a hipótese de que pacotes de conteúdo adicional geram insatisfação por custos extras, os dados mostraram uma tendência de crescimento na aprovação proporcional ao volume de DLCs disponíveis. O fenómeno evidencia um Viés de Sobrevivência (Survivor Bias): estúdios realizam investimentos recorrentes de expansão de conteúdo exclusivamente em propriedades intelectuais que já possuem aceitação consolidada e uma comunidade ativa de compradores.

<div align="center">
  <img src="images/dlc_aprovacao.png" alt="O Efeito das DLCs na Aprovação" width="800">
</div>

### Módulo 7: Aprendizado de Máquina Não Supervisionado (Clustering com DBSCAN)
Para segmentar a dinâmica de mercado sem a interferência de grandes distorções, aplicou-se o algoritmo DBSCAN focado em densidade. O modelo mapeou as variáveis de recepção e alcance, isolando com precisão os fenómenos de vendas e grandes sucessos no Cluster -1 (Outliers). A validação por meio de Boxplots confirmou que a maior parte do catálogo da plataforma opera em margens muito estreitas de engajamento, enquanto um grupo seleto rompe o padrão estatístico tradicional.

<div align="center">
  <img src="images/dbscan_clustering.png" alt="Boxplots do Clustering com DBSCAN" width="800">
</div>
