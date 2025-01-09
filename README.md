
# Previsão de Preços de Imóveis com Machine Learning


# Contexto e Objetivo

O objetivo deste projeto é desenvolver um modelo preditivo robusto para estimar o valor de imóveis com base em suas características. Este projeto focou exclusivamente na construção e avaliação do modelo preditivo, sem explorar em profundidade as relações entre as variáveis e outros aspectos exploratórios. Futuras análises podem incluir a compreensão mais detalhada dessas relações. A previsão de preços imobiliários é fundamental para investidores, compradores e vendedoras, permitindo uma tomada de decisão...

---

# Tabela de Conteúdo

1. [Descrição dos Dados](#descrição-dos-dados)
2. [Pré-processamento](#pré-processamento)
3. [Modelagem](#modelagem)
4. [Avaliação do Modelo](#avaliação-do-modelo)
5. [Resultados](#resultados)
6. [Tecnologias Utilizadas](#tecnologias-utilizadas)
7. [Conclusão](#conclusão)
8. [Recomendações para Próximos Passos](#recomendações-para-próximos-passos)

---

# Descrição dos Dados

O conjunto de dados contém **53.826 registros** e **28 colunas**, incluindo informações sobre preço do imóvel (`valor`), IPTU (`iptu`), condomínio (`condominio`), área total (`area_total`), área útil (`area_util`), tipo de anúncio, tipo de unidade, tipo de uso, zona, bairro e uma lista de características do imóvel, como:

- Academia
- Animais permitidos
- Churrasqueira
- Condomínio fechado
- Elevador
- Piscina
- Playground
- Portaria 24h
- Portão eletrônico
- Salão de festas

Alguns campos possuem valores faltantes, como `area_total`, `suites` e `vaga`. As características dos imóveis foram transformadas em variáveis dummy para facilitar a análise.

---

# Pré-processamento

As etapas de pré-processamento incluíram:

### Transformação de Características:

- As características dos imóveis foram expandidas em colunas binárias utilizando `str.get_dummies()`.
- Linhas onde todas as características eram iguais a zero foram removidas.
- A coluna `caracteristicas`, que continha uma lista de atributos, foi separada em várias colunas, representando cada atributo como uma variável binária (presente ou ausente). Essa separação permitiu capturar melhor os atributos individuais dos imóveis e sua influência no valor de preço.

### Tratamento de Dados:

- Conversão de colunas numéricas para o tipo float.
- Remoção de colunas irrelevantes, como bairro.
- Substituição de valores nulos por médias ou estratégias apropriadas.

### Escalonamento:

- O **RobustScaler** foi aplicado para normalizar variáveis numéricas, como área total, área útil e preço, utilizando os valores de mediana e intervalo interquartil. Essa técnica permitiu que os dados fossem ajustados de forma robusta a outliers, reduzindo sua influência sem eliminá-los. Na prática, isso resultou em uma distribuição mais uniforme das variáveis, o que melhorou a estabilidade e o desempenho do modelo de Random Forest Regressor.

---

# Modelagem

A modelagem utilizou o **Random Forest Regressor** devido à sua capacidade de lidar com dados complexos e mistos. As etapas incluíram:

### Divisão de Dados:

- Separar os dados em conjunto de treino (70%) e teste (30%) usando `train_test_split`.

### Treinamento do Modelo:

- O modelo foi ajustado para prever a variável alvo `valor`.

---

# Avaliação do Modelo

### Transformação da Variável Alvo:

- A transformação logarítmica foi aplicada na variável alvo `valor` para lidar com a ampla variabilidade nos preços dos imóveis, que variavam de R$15.000 a R$13.900.000. Essa distribuição assimétrica dificultava o aprendizado do modelo devido à presença de valores extremos.

### Resultados Antes da Transformação:

- **Mean Squared Error (MSE):** 284.357.683.697,01
- **Root Mean Squared Error (RMSE):** 533.251,99
- **R² (Coeficiente de Determinação):** 0,8804

### Resultados Após a Transformação:

- **Mean Squared Error (MSE):** 0,0627
- **Root Mean Squared Error (RMSE):** 0,25
- **R² (Coeficiente de Determinação):** 0,9131

A transformação logarítmica garantiu uma distribuição mais uniforme dos dados, reduzindo a influência de valores muito altos ou baixos e permitindo que o modelo capturasse melhor os padrões subjacentes. Isso resultou em predições mais precisas e consistentes, com ganhos significativos de desempenho nas métricas avaliadas.

---

# Resultados

### Desempenho Geral:

- As métricas de desempenho do modelo foram:
  - **Erro Quadrático Médio (MSE):** Mede a diferença média ao quadrado entre os valores reais e previstos.
  - **R² (Coeficiente de Determinação):** Indica a proporção da variância explicada pelo modelo. O valor obtido foi **0,9131**, sugerindo um ajuste ainda mais preciso após a transformação logarítmica.

### Importância das Features:

| **Feature**         | **Importância** |
|----------------------|-----------------|
| Área útil            | 0.61            |
| Condomínio           | 0.17            |
| IPTU                | 0.06            |
| Zona - Zona Sul      | 0.04            |
| Vaga                | 0.03            |
| Suítes              | 0.02            |
| Andar               | 0.01            |
| Banheiros           | 0.01            |
| Quartos             | 0.01            |

A análise das importâncias das features destaca que a **"Área útil"** é a variável mais significativa para o modelo, seguida por **"Condomínio"** e **"IPTU"**. As variáveis relacionadas às zonas geográficas, como **"Zona Sul"**, também apresentaram alguma relevância. Entretanto, diversas características adicionais, como **"Piscina"** e **"Academia"**, não demonstraram impacto relevante no modelo atual. Recomenda-se revisitar essas variáveis em análises futuras para compreender melhor seu papel potencial.

---

# Tecnologias Utilizadas

- Python
- Pandas
- Matplotlib
- Seaborn
- Scikit-learn
- NumPy

---

# Conclusão

Este projeto demonstrou que é possível prever com alta precisão o preço de imóveis utilizando um modelo de **Random Forest Regressor**. No entanto, é recomendado aprofundar as análises para entender melhor como as variáveis independentes se relacionam entre si e com a variável alvo, oferecendo insights mais completos para o mercado imobiliário.

---

# Recomendações para Próximos Passos

## Análise de Variáveis:

- Investigar como as variáveis independentes se relacionam com a variável alvo e entre si.
- Identificar padrões e interações que possam oferecer insights adicionais para o mercado imobiliário.

## Testes com Outros Modelos:

- Explorar outras técnicas de Machine Learning, como **Gradient Boosting** ou **XGBoost**, para comparar o desempenho.

## Validação Contínua:

- Monitorar o modelo em novos conjuntos de dados para garantir a consistência e adaptabilidade ao longo do tempo.
