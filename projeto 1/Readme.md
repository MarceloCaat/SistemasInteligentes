# Regressão Linear Múltipla para Previsão da Produção de Energia em uma Usina de Ciclo Combinado

##  Introdução
Neste projeto, trabalharemos com uma usina termelétrica de ciclo combinado, que utiliza turbinas a gás e a vapor para gerar energia elétrica. A potência elétrica produzida pela usina pode variar de acordo com diferentes condições ambientais e operacionais.

Diante disso, nosso objetivo é desenvolver um modelo de Regressão Linear Múltipla capaz de prever a potência elétrica (PE) gerada pela usina a partir de quatro variáveis independentes: temperatura ambiente (AT), vácuo de escape (V), pressão atmosférica (AP) e umidade relativa (RH).

##  Dataset usado

Foi utilizado o dataset **Combined Cycle Power Plant (CCPP)**, disponibilizado pela UCI Machine Learning Repository.

- **Número de amostras:** 9.568
- **Variáveis independentes:** AT, V, AP e RH
- **Variável-alvo:** PE (produção líquida de energia elétrica, em MW)

**Fonte dos dados:** [UCI Machine Learning Repository - Combined Cycle Power Plant](https://archive.ics.uci.edu/ml/datasets/Combined+Cycle+Power+Plant)

## Pré-processamento dos dados

### Verificação e tratamento de valores
 Foi realizada uma verificação da existência de valores ausentes no conjunto de dados. Como não foram identificados valores ausentes, não eranecessario procedimentos de remoção ou imputação desses valores, Porem foi feito uma metodo de tratamento preventivo.

 Para o tratamento dos dados, utilizamos a **imputação de valores ausentes (SimpleImputer)** como forma de prevenir possíveis problemas com dados incompletos. Foi utilizada a estratégia da mediana para substituir eventuais valores ausentes. Entretanto, como o dataset não apresentou valores ausentes, não foi necessário realizar nenhuma substituição.

Também utilizamos a **padronização (StandardScaler)**, com o objetivo de colocar todas as variáveis independentes em uma mesma escala, fazendo com que apresentem média zero e desvio padrão igual a um. Esse processo evita diferenças de escala entre as variáveis durante o treinamento.

Por fim, utilizamos a **Regressão Linear Múltipla (LinearRegression)** para construir o modelo responsável por estimar a variável dependente (PE), utilizando as quatro variáveis independentes (AT, V, AP e RH).
### Divisão de dados de treinamento e teste
O dataset foi divido em 80% para o treinamento e 20% para o teste

##  Análise de Correlação

Foi utilizada a correlação de Pearson para analisar a relação linear entre as variáveis independentes e a produção de energia elétrica (PE).

### Correlação das variáveis independentes com PE

| **Variável** | **Correlação de Pearson com PE** |
|:---:|---:|
| AT | -0,9481 |
| V | -0,8698 |
| AP | 0,5184 |
| RH | 0,3898 |

Observando a tabela, podemos identificar que as variáveis independentes **AT** e **V** apresentam as correlações negativas mais fortes com a variável dependente **PE**, com valores de -0,9481 e -0,8698, respectivamente. Isso indica uma forte relação inversa: à medida que a temperatura ambiente (AT) e o vácuo de exaustão (V) aumentam, a produção de energia elétrica (PE) tende a diminuir.

Já as variáveis **AP** e **RH** apresentam correlações positivas, de intensidade moderada e mais fraca, respectivamente.


### Correlação entre as Variáveis de Entrada



| **Par de Variáveis** | **Correlação de Pearson** |
|:---|---:|
| AT e V | 0,8441 |
| AT e RH | -0,5425 |
| AT e AP | -0,5075 |
| V e AP | -0,4135 |
| V e RH | -0,3122 |
| AP e RH | 0,0996 |


Foi calculada a correlação de Pearson entre as variáveis independentes (AT, V, AP e RH) para identificar possíveis relações lineares entre elas e verificar indícios de multicolinearidade.

Observando os resultados, nota-se que o par **AT e V** apresenta a maior correlação positiva, com valor de **0,8441**, indicando uma forte associação linear entre essas variáveis. Esse resultado pode ser um indício de multicolinearidade no modelo.

As demais combinações apresentam correlações de menor intensidade. Destaca-se também a baixa correlação entre **AP e RH**, cujo valor é de **0,0996**.

Portanto, os resultados sugerem uma possível relação de multicolinearidade principalmente entre AT e V. Entretanto, a matriz de correlação, isoladamente, não é suficiente para confirmar sua presença. Para uma análise mais precisa, pode-se utilizar o **Fator de Inflação da Variância (VIF)**.

### Construção e Treinamento do Modelo

Nesta etapa, construímos o modelo de Regressão Linear Múltipla utilizando os dados de treinamento. O método `fit()` foi responsável por ajustar o modelo, identificando os coeficientes das variáveis independentes (AT, V, AP e RH), além do intercepto.

Após o treinamento, analisamos os coeficientes obtidos para compreender a influência de cada variável na estimativa da produção de energia elétrica (PE).

Em seguida, utilizamos o método `predict()` para realizar previsões com os dados de teste. Por fim, comparamos os valores reais de produção de energia com os valores previstos pelo modelo, permitindo avaliar o desempenho das estimativas.


### Resultados da Avaliação do Modelo

Após a avaliação do modelo com os dados de teste, obtivemos um coeficiente de determinação (R²) de **0,9301**, indicando que aproximadamente **93,01% da variação da produção de energia elétrica (PE)** é explicada pelo modelo.

O RMSE apresentou um valor de **4,5026 MW**, enquanto o MAE foi de **3,5959 MW**. Esses resultados indicam que as previsões apresentam erros relativamente baixos, com uma diferença absoluta média de aproximadamente 3,60 MW em relação aos valores reais.

De maneira geral, os resultados demonstram que o modelo de Regressão Linear Múltipla apresentou um bom desempenho na previsão da produção de energia elétrica, conseguindo representar grande parte da variação dos dados de teste.

