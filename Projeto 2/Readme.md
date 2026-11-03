# Regressão Logística para Previsão de Doenças Cardíacas
## Introdução

## Dataset
Foi utilizado o dataset Heart Disease, disponibilizado pelo UCI Machine Learning Repository.
**Variáveis independentes**: age, sex, cp, trestbps, chol, fbs, restecg, thalach, exang, oldpeak, slope, ca e thal.
**Variável-alvo**: num, transformada em uma variável binária para representar a ausência ou presença de doença cardíaca.
Fonte dos dados: UCI Machine Learning Repository — Heart Disease.

## Pré-processamento dos dados
### Verificação e tratamento de valores
Inicialmente, foi realizada uma análise dos dados para verificar os tipos das variáveis e a existência de valores ausentes. Em seguida, foi utilizado o SimpleImputer para realizar o tratamento de eventuais valores ausentes.

Para as variáveis numéricas, foi utilizada a estratégia da mediana, que substitui os valores ausentes pelo valor central da distribuição observada nos dados de treinamento. Para as variáveis categóricas, foi utilizada a estratégia da categoria mais frequente, substituindo os valores ausentes pela categoria que apresenta maior ocorrência.
### Padronização das variáveis numéricas
Também foi utilizada a padronização por meio do StandardScaler, aplicada às variáveis numéricas, como idade, pressão arterial em repouso, colesterol, frequência cardíaca máxima e oldpeak.

A padronização é importante porque as variáveis possuem escalas diferentes. Ao colocá-las em escalas comparáveis, o procedimento pode favorecer a otimização dos parâmetros da Regressão Logística e tornar a regularização do modelo mais consistente

### Codificação das variáveis categóricas
Para as variáveis categóricas, foi utilizado o One-Hot Encoding, por meio da classe OneHotEncoder.

Esse método transforma as categorias em variáveis indicadoras, representadas por valores binários. Dessa forma, evita-se impor uma relação de ordem numérica entre categorias que não possuem uma hierarquia natural.

As variáveis categóricas utilizadas foram sex, cp, fbs, restecg, exang, slope, ca e thal.

Também foi utilizado o parâmetro handle_unknown="ignore", que permite lidar com categorias presentes nos dados de teste que não tenham sido observadas durante o treinamento.

O pré-processamento numérico e categórico foi organizado por meio de Pipeline e ColumnTransformer, permitindo que cada grupo de variáveis recebesse o tratamento adequado. Os parâmetros das transformações foram ajustados exclusivamente com os dados de treinamento, evitando o vazamento de informações do conjunto de teste.
### Divisão dos dados de treinamento e teste
os dados foram divididos 80% para o treinamento e 20% para teste
## Construção e treinamento do modelo

## Resultados da avaliação do modelo
Após o treinamento, o modelo foi avaliado utilizando os dados de teste. Foram calculadas as métricas de acurácia, precisão, recall, F1-score e AUC-ROC.

| Métrica | Valor |
|---|---:|
| Acurácia (Accuracy) | 0.8852 (88,52%) |
| Precisão (Precision) | 0.8387 (83,87%) |
| Recall | 0.9286 (92,86%) |
| F1-score | 0.8814 (88,14%) |
| AUC-ROC | 0.9665 |

De maneira geral, os resultados demonstram que o modelo apresentou bom desempenho na classificação dos indivíduos do conjunto de teste. Destaca-se o recall de 92,86%, que indica uma elevada proporção de casos positivos identificados, e a AUC-ROC de 0,9665, que demonstra uma forte capacidade de discriminação entre as classes. Apesar disso, a precisão de 83,87% indica que parte das previsões positivas corresponde a falsos positivos.