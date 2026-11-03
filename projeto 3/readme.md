## Classificação da Qualidade de Vinhos utilizando k-NN
## Introdução
O objetivo deste projeto é desenvolver um modelo de classificação utilizando o algoritmo k-Nearest Neighbors (k-NN), capaz de classificar os vinhos em três categorias: Ruim, Média e Boa, considerando suas propriedades físico-químicas.
## Dataset
Foi utilizado o dataset Wine Quality – Red, disponibilizado no UCI Machine Learning Repository.

**Dimensões do dataset:** 1.599 amostras e 12 colunas.

**Variáveis independentes:** fixed acidity, volatile acidity, citric acid, residual sugar, chlorides, free sulfur dioxide, total sulfur dioxide, density, pH, sulphates e alcohol.

**Variável-alvo:** quality, que representa a avaliação da qualidade do vinho.

### Agrupamento da Variável-Alvo

A variável original foi agrupada em três categorias:

- **Ruim:** qualidade igual ou inferior a 5 (≤ 5).
- **Média:** qualidade igual a 6 (= 6).
- **Boa:** qualidade igual ou superior a 7 (≥ 7).

### Distribuição das Classes após o Agrupamento

| Classe | Amostras | Percentual |
|:-------|---------:|-----------:|
| Ruim   | 744      | 46,53%     |
| Média  | 837      | 52,35%     |
| Boa    | 18       | 1,13%      |
| **Total** | **1.599** | **100%** |
    
Observa-se um forte desbalanceamento na classe Boa, que representa apenas 1,13% das amostras.

## Pré-processamento dos dados

### Verificação e tratamento de valores

Foi realizada uma análise exploratória do dataset para verificar suas dimensões, os tipos das variáveis e a existência de valores ausentes.

O conjunto de dados apresentou 1.599 registros e 12 colunas. Na verificação de valores ausentes, não foram identificados valores faltantes nas variáveis utilizadas.

### Agrupamento das classes 

A variável original quality, que apresenta valores numéricos de avaliação, foi transformada em uma variável categórica com três classes: Ruim, Média e Boa.

Esse agrupamento foi realizado para simplificar o problema de classificação e permitir uma análise mais abrangente da qualidade dos vinhos.

Entretanto, essa transformação resultou em um desbalanceamento significativo, principalmente pela baixa quantidade de amostras pertencentes à classe Boa.

### Divisão dos dados de treinamento e teste

Os dados foram divididos utilizando a proporção de 80% para treinamento e 20% para teste. ficamos com 1279 amostras para p treinamento e 320 para o teste

### Normalização das variaveis

Foi utilizada a padronização por meio do StandardScaler.

Esse procedimento transforma as variáveis numéricas, ajustando suas escalas para que apresentem média próxima de zero e desvio-padrão próximo de um.

A normalização é especialmente importante para o algoritmo k-NN, pois seu funcionamento depende do cálculo de distâncias entre as amostras.

Como as características físico-químicas possuem unidades e escalas diferentes, a padronização evita que variáveis com valores numericamente maiores tenham influência desproporcional no cálculo das distâncias.

### Tratamento do desbalanceamento das classes

Como o dataset apresenta uma quantidade muito pequena de amostras da classe Boa (1,13%), foi utilizada a técnica SMOTE para gerar amostras sintéticas das classes minoritárias, buscando reduzir o desbalanceamento e melhorar o desempenho da classificação.

## Construção e treinamento do modelo

Foi utilizado o algoritmo k-Nearest Neighbors (k-NN), que classifica uma amostra com base nas classes de seus vizinhos mais próximos.

Para selecionar o melhor valor de k, foram testados os valores 1, 3, 5, 7 e 11, utilizando validação cruzada.

O valor escolhido foi k = 5, pois apresentou o melhor F1-score macro médio de 0.5170, com acurácia média de 72,40%.

### Resultados da Avaliação do Modelo

Após o treinamento, o modelo foi avaliado com as 320 amostras do conjunto de teste.

| Métrica | Valor |
|:--------|------:|
| Acurácia | 73,75% |
| Acurácia balanceada | 58,01% |
| Precisão macro | 53,59% |
| Recall macro | 58,01% |
| F1-score macro | 54,24% |

## Matriz de Confusão

| Classe Real / Prevista | Ruim | Média | Boa |
|:----------------------|-----:|------:|----:|
| Ruim                  | 115  | 32    | 2   |
| Média                 | 37   | 120   | 10  |
| Boa                   | 0    | 3     | 1   |

O modelo apresentou melhor desempenho nas classes **Ruim** e **Média**, com F1-scores de 0.7641 e 0.7453, respectivamente.

Já a classe **Boa** apresentou desempenho inferior, com F1-score de 0.1176, devido à quantidade reduzida de amostras.

A maior confusão ocorreu entre as classes **Ruim** e **Média**, com 69 classificações incorretas entre essas categorias.

 ## Análise Comparativa

| Modelo | Acurácia | F1-macro | Acurácia balanceada |
|:-------|---------:|---------:|--------------------:|
| Referência | 0.7131 | 0.4763 | 0.4786 |
| SMOTE + distância | 0.7240 | 0.5170 | 0.5536 |

A utilização de **SMOTE e distância** apresentou melhorias nas três métricas, principalmente na acurácia balanceada, indicando uma classificação mais equilibrada entre as classes.

## Conclusão 
O algoritmo k-NN apresentou acurácia de 73,75% na classificação da qualidade dos vinhos. O melhor valor de k foi 5, selecionado por meio do F1-score macro.

O modelo apresentou resultados satisfatórios para as classes Ruim e Média, mas teve dificuldade em classificar a classe Boa devido ao desbalanceamento do dataset. Dessa forma, conclui-se que o modelo conseguiu identificar padrões nas características físico-químicas dos vinhos, mas ainda apresenta limitações na classificação das classes minoritárias.