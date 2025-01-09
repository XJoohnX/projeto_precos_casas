
# Previsão de Preços de Imóveis com Machine Learning

## Contexto e Objetivo

O objetivo deste projeto é desenvolver um modelo preditivo robusto para estimar o valor de imóveis com base em suas características. Este projeto foca exclusivamente na construção e avaliação do modelo preditivo, sem explorar em profundidade as relações entre as variáveis. Futuras análises podem incluir a compreensão mais detalhada dessas relações. 

A previsão de preços imobiliários é fundamental para investidores, compradores e vendedores, permitindo uma tomada de decisão mais informada e estratégica no mercado imobiliário. Utilizando dados detalhados sobre imóveis, o projeto emprega um modelo de Machine Learning, o **Random Forest Regressor**, para atingir alta precisão e confiabilidade.

---

## Tabela de Conteúdo

1. [Descrição dos Dados](#descrição-dos-dados)
2. [Pré-processamento](#pré-processamento)
3. [Modelagem](#modelagem)
4. [Avaliação do Modelo](#avaliação-do-modelo)
5. [Resultados](#resultados)
6. [Tecnologias Utilizadas](#tecnologias-utilizadas)
7. [Conclusão](#conclusão)
8. [Recomendações para Próximos Passos](#recomendações-para-próximos-passos)

---

## Descrição dos Dados

O conjunto de dados contém **53.826 registros** e **28 colunas**, incluindo:

- **Preço do imóvel** (`valor`)
- **IPTU** (`iptu`)
- **Condomínio** (`condominio`)
- **Área total** (`area_total`)
- **Área útil** (`area_util`)
- Informações categóricas: tipo de anúncio, tipo de unidade, tipo de uso, zona, bairro.
- Características adicionais dos imóveis, como:
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

**Valores faltantes**: Algumas colunas, como `area_total`, `suites` e `vaga`, possuem valores nulos. Esses valores foram tratados adequadamente durante o pré-processamento.

---

## Pré-processamento

### Transformação de Características

- Expansão das características dos imóveis em colunas binárias utilizando `str.get_dummies()`.
- Remoção de linhas onde todas as características eram iguais a zero.
- Separação da coluna `caracteristicas` em várias colunas binárias.

### Tratamento de Dados

- Conversão de colunas numéricas para o tipo `float`.
- Remoção de colunas irrelevantes (ex.: `bairro`).
- Substituição de valores nulos por médias ou estratégias apropriadas.

### Escalonamento

- Aplicação do **RobustScaler** para normalizar variáveis numéricas (`area_total`, `area_util`, `valor`).
  - Ajuste robusto a outliers, utilizando mediana e intervalo interquartil.
  - Melhor estabilidade e desempenho no modelo **Random Forest Regressor**.

---

## Modelagem

### Algoritmo Escolhido

Utilizou-se o **Random Forest Regressor** devido à sua capacidade de lidar com dados complexos e mistos.

### Divisão de Dados

- **Conjunto de treino**: 70%
- **Conjunto de teste**: 30%
- Utilizou-se `train_test_split` para a divisão.

### Transformação da Variável Alvo

- Aplicação de transformação logarítmica na variável alvo (`valor`) para lidar com a ampla variabilidade nos preços (R$15.000 a R$13.900.000).

---

## Avaliação do Modelo

### Resultados Antes da Transformação

- **MSE**: 284.357.683.697,01
- **RMSE**: 533.251,99
- **R²**: 0,8804

### Resultados Após a Transformação

- **MSE**: 0,0627
- **RMSE**: 0,25
- **R²**: 0,9131

A transformação logarítmica garantiu uma distribuição mais uniforme, reduzindo a influência de valores extremos e melhorando significativamente o desempenho do modelo.

---

## Resultados

### Importância das Features

| **Feature**        | **Importância** |
|---------------------|-----------------|
| Área útil           | 0.61            |
| Condomínio          | 0.17            |
| IPTU               | 0.06            |
| Zona - Zona Sul     | 0.04            |
| Vaga               | 0.03            |
| Suítes             | 0.02            |
| Andar              | 0.01            |
| Banheiros          | 0.01            |
| Quartos            | 0.01            |

- **Área útil** foi a variável mais significativa, seguida por **Condomínio** e **IPTU**.
- Características como **Piscina** e **Academia** não demonstraram impacto relevante no modelo.

---

## Tecnologias Utilizadas

- **Python**
- **Pandas**
- **Matplotlib**
- **Seaborn**
- **Scikit-learn**
- **NumPy**

---

## Conclusão

Este projeto demonstrou que é possível prever com alta precisão o preço de imóveis utilizando o **Random Forest Regressor**. Com a aplicação de técnicas de pré-processamento e transformação de variáveis, o modelo atingiu um **R² de 0,9131**, indicando um excelente ajuste.

---

## Recomendações para Próximos Passos

### Análise de Variáveis

- Explorar como as variáveis independentes se relacionam entre si e com a variável alvo.
- Investigar padrões e interações adicionais.

### Testes com Outros Modelos

- Experimentar técnicas como **Gradient Boosting** ou **XGBoost** para comparar desempenho.

### Validação Contínua

- Monitorar o modelo com novos conjuntos de dados para garantir consistência e adaptabilidade ao longo do tempo.
