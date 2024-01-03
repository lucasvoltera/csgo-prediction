# csgo-prediction

## Introdução

O Counter-Strike: Global Offensive (CS:GO) é um jogo de tiro em primeira pessoa lançado em 2012, notório nos esportes eletrônicos, onde duas equipes, Terroristas e Contra-Terroristas, priorizam táticas e estratégias. O cenário competitivo destaca-se em torneios como o Major Championship, impulsionando os esportes eletrônicos. O uso do Aprendizado de Máquina (AM) nas estatísticas, como abates e assistências, inova a análise estratégica, antecipando com precisão desfechos de partidas.

## Objetivos

O principal objetivo é criar modelos de AM capazes de prever se um jogador vencerá ou perderá uma partida de CS:GO com base em suas estatísticas individuais. Objetivos específicos incluem:

* Conduzir uma análise exploratória para identificar as variáveis mais relevantes na predição de vitórias ou derrotas nas partidas.
* Aplicar e comparar diferentes métodos de redução de dimensionalidade para melhorar o desempenho dos modelos.

## Material e Metodologia

Os dados foram fornecidos pela Gamers Club, totalizando mais de 180.000 amostras, cada uma representando um jogador em uma partida de CS:GO entre 2021 e 2022. A metodologia KDD (Knowledge Discovery in Databases) foi adotada, envolvendo etapas como seleção, limpeza, transformação, modelagem e interpretação.


## Análise Exploratória

Na análise exploratória do projeto, foram aplicadas técnicas de Aprendizado de Máquina (AM) utilizando Random Forest e Logistic Regression para identificar variáveis cruciais na predição de vitórias em partidas de CS:GO. Os modelos revelaram diferentes variáveis como significativas: Random Forest destacou taxa de sobrevivência, DPR e KAST, enquanto Logistic Regression priorizou rounds sobrevividos, mortes, assistências e trocas de armas. A análise também revelou a importância das variáveis relacionadas à quantidade de mortes na predição da vitória.

![rf](https://github.com/lucasvoltera/csgo-prediction/assets/62965997/c1f83a60-2cdc-48da-b130-7c25c14f438f)

![lr](https://github.com/lucasvoltera/csgo-prediction/assets/62965997/e5a9cd0e-f67d-4ab5-8800-420a94c61f4e)



Com base nas variáveis mais relevantes, foram conduzidas duas análises adicionais. A primeira explorou a relação entre DPR e KPR, evidenciando que jogadores com estratégias cautelosas, focadas em objetivos e comunicação, têm maior probabilidade de vitória. A segunda analisou a conexão entre taxa de sobrevivência e KAST, destacando que jogadores vitoriosos apresentaram maior taxa de sobrevivência e contribuição ao time, evidenciando a importância de estratégias além da simples eliminação de adversários. Essas descobertas ressaltam a complexidade tática do CS:GO, onde o estilo de jogo impacta diretamente os resultados das partidas.

## Pré-Processamento

O conjunto de dados apresenta equilíbrio notável, com 90.178 amostras (49,3%) indicando vitória e 92.620 amostras (50,7%) de não vitória. Não foi necessário balanceamento de classes devido a essa distribuição equitativa. Durante a análise, identificaram-se 681 amostras com valores ausentes, as quais foram removidas. Não foram encontradas duplicatas. A variável categórica do mapa foi convertida usando "One-Hot Encoding". O tratamento de outliers envolveu o método Z-score, removendo 1191 amostras. O conjunto final de 180.926 amostras foi normalizado pelo método Min-Max antes de ser submetido aos algoritmos de Aprendizado de Máquina, assegurando uniformidade nos pesos e preservando relações proporcionais.

## Redução de Dimensionalidade

Foram criados dois conjuntos adicionais a partir dos dados pré-processados, com diferentes métodos de redução de dimensionalidade. No primeiro, foram escolhidas as 10 variáveis mais relevantes pelo modelo Random Forest. No segundo, a redução foi feita via Análise de Componentes Principais (PCA), selecionando 10 componentes principais.

![pca_analysis](https://github.com/lucasvoltera/csgo-prediction/assets/62965997/b6b27e7a-3701-461a-8be5-11a879267d7c)


## Modelagem 

A previsão de vitórias envolveu técnicas de Aprendizado de Máquina em três conjuntos de dados distintos: os dados pré-processados, os dados com 10 variáveis selecionadas e os dados transformados por PCA, com 10 componentes principais. Algoritmos como Logistic Regression, Random Forest, K-Nearest-Neighbors (KNN), XGBoost, Naive Bayes e Neural Network foram aplicados, dividindo cada conjunto em 80% para treino e 20% para teste. A otimização dos modelos incluiu a extração de métricas relevantes e a utilização do GridSearch para encontrar a melhor combinação de hiperparâmetros, visando melhorar o desempenho preditivo. Segue-se a tabela de acurácia de cada modelo em cada conjunto de dados

| Modelo             | Dados Pré-processados | Dados com Variáveis Selecionadas | Dados Transformados por PCA |
|--------------------|------------------------|----------------------------------|------------------------------|
| Logistic Regression | 0.8                   | 0.78                             | 0.79                         |
| Random Forest       | 0.8                   | 0.78                             | 0.78                         |
| KNN                | 0.77                   | 0.78                             | 0.77                         |
| XGBoost            | 0.8                    | 0.79                             | 0.78                         |
| Naive Bayes        | 0.73                   | 0.76                             | 0.76                         |
| Neural Network     | 0.79                   | 0.79                             | 0.79                         

## Discussão dos modelos

Dentre os modelos analisados nos dados pré-processados, Logistic Regression (C=0.00483), XGBoost (n_estimators=100) e Random Forest (n_estimators=2000) destacaram-se, atingindo 80% de acurácia. O Logistic Regression foi preferencial devido à eficiência computacional e manteve resultados robustos. Nos conjuntos de dados selecionados e transformados por PCA, os modelos não superaram o desempenho dos dados pré-processados. Vale ressaltar que, devido à complexidade centrada no desempenho em equipe, o desafio de prever resultados em CS é evidente. Situações onde uma equipe vence apesar do desempenho individual abaixo do esperado ou perde mesmo com desempenho excepcional são comuns, complicando a tarefa dos modelos. Isso destaca a importância da colaboração e do desempenho coletivo, mesmo em falhas de previsão, para uma compreensão mais completa do jogo.


## Recomendações Futuras

Para futuros trabalhos, sugere-se explorar novas técnicas de pré-processamento, avaliar algoritmos alternativos e investigar estratégias de otimização para aprimorar a previsão de vitórias com este conjunto de dados.
