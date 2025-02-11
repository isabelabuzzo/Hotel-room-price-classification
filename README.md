# 🏨 Hotel Price Classification

Este repositório contém um projeto de classificação de preços médios por quarto de hotel, explorando o dataset *hotel-price*. Os preços foram categorizados em três faixas distintas e, posteriormente, modelos de *machine learning* foram treinados para realizar a classificação, utilizando atributos como número de adultos, crianças, tipo do quarto, entre outros.

## 📊 Dicionário de Dados Inicial

O dataset possui **36.275 linhas** e **19 colunas** e pode ser encontrado em  
[📌 Hotel Reservations Classification Dataset - Kaggle](https://www.kaggle.com/datasets/ahsan81/hotel-reservations-classification-dataset).  

Abaixo, o dicionário dos dados:

- **Booking ID**: Identificador único de cada reserva.  
- **no of adults**: Número de adultos.  
- **no of children**: Número de crianças.  
- **no of weekend nights**: Número de noites de fim de semana reservadas. 
- **no of week nights**: Número de noites da semana reservadas. 
- **type of meal plan**: Tipo de plano de refeição reservado pelo cliente.  
- **required car parking space**: O cliente necessita de uma vaga de estacionamento? *(0 - Não, 1 - Sim)*.  
- **room type reserved**: Tipo de quarto reservado pelo cliente.
- **lead time**: Número de dias entre a data da reserva e a data de chegada.  
- **arrival year**: Ano da data de chegada.  
- **arrival month**: Mês da data de chegada.  
- **arrival date**: Dia do mês da data de chegada.  
- **market segment type**: Designação do segmento de mercado.  
- **repeated guest**: O cliente é um hóspede repetido? *(0 - Não, 1 - Sim)*.  
- **no of previous cancellations**: Número de reservas anteriores canceladas pelo cliente antes da reserva atual.  
- **no of previous bookings not canceled**: Número de reservas anteriores não canceladas pelo cliente.
- **avg price per room**: Preço médio por dia da reserva em euros.
- **no of special requests**: Número total de pedidos especiais feitos pelo cliente.  
- **booking status**: Indicador se a reserva foi cancelada ou não.  


## 🏷️ Classificação

A repartição dos dados em ``avg_price_per_room`` foi feita por meio da função ``qcut``, que dividiu a feature em três intervalos diferentes, preservando ao máximo a quantidade de dados em cada categoria.

- **Label 0**: Preços entre **€0 e €88,00**.
- **Label 1**: Preços entre **€89 e €115,00**.
- **Label 2**: Preços acima de **€115,00**.

## ⚙️ Pré-processamento dos dados

- **Carregamento dos dados**: O dataset foi importado e analisado para verificar sua estrutura e qualidade.
- **Remoção de colunas irrelevantes**: A coluna `Booking_ID` foi excluída, pois continha valores únicos para cada entrada e não agregava informação relevante ao modelo.
- **Verificação de valores nulos**: Nenhuma entrada nula foi identificada.

### Transformação dos atributos categóricos e numéricos

Os atributos foram analisados para verificar distribuição e possíveis relações hierárquicas:

- **Label Encoding** foi aplicado em atributos categóricos **ordinais** (``market_segment_type`` e ``booking_status``).
- **One-Hot Encoding** foi utilizado para atributos categóricos **não ordinais** (``type_of_meal_plan`` e ``room_type_reserved``).

A variável `avg_price_per_room` foi transformada na variável alvo `label_avg_price_per_room`, categorizando os preços nas três faixas mencionadas anteriormente.

### Análise estatística dos atributos

- Foram aplicados testes estatísticos como `f_classif` para selecionar os atributos mais relevantes.
- A seleção final foi baseada em *p-values* inferiores a **0.01** e correlação superior a **0.1**.

## 💡 Modelos de Machine Learning

### 🌲 Random Forest

- Divisão do dataset em treino, validação e teste.
- Treinamento do modelo *Random Forest* com diferentes profundidades.
- Avaliação do modelo utilizando *accuracy_score* e *classification_report*.
- Utilização da matriz de confusão para análise detalhada dos erros de classificação.

### 🚀 XGBoost

- Treinamento do modelo *XGBoost* com diferentes hiperparâmetros (`n_estimators`, `max_depth`, `learning_rate`).
- Monitoramento do desempenho usando `early_stopping_rounds`.
- Avaliação do modelo nos conjuntos de validação e teste.

## Resultados

Para ambos os modelos, foi utilizada *Cross Validation*, com **30%** do dataset destinado à validação e **70%** para treino.

### 🌲 Random Forest

| **Label** | **Precisão** | **Recall** | **F1-score** |
|-----------|------------|-----------|------------|
| 0         | 0.89       | 0.89      | 0.89       |
| 1         | 0.82       | 0.80      | 0.81       |
| 2         | 0.88       | 0.90      | 0.89       |
| **Acurácia** | **0.86**  |           |            |
| **Macro avg** | 0.86    | 0.86      | 0.86       |
| **Weighted avg** | 0.86 | 0.86      | 0.86       |

### 🚀 XGBoost

| **Label** | **Precisão** | **Recall** | **F1-score** |
|-----------|------------|-----------|------------|
| 0         | 0.90       | 0.87      | 0.89       |
| 1         | 0.81       | 0.82      | 0.81       |
| 2         | 0.88       | 0.90      | 0.89       |
| **Acurácia** | **0.87**  |           |            |
| **Macro avg** | 0.87    | 0.86      | 0.86       |
| **Weighted avg** | 0.87 | 0.87      | 0.87       |

## 🛠️ Ferramentas Utilizadas

- **Linguagem**: Python
- **Ambiente**: Jupyter Notebook
- **Bibliotecas**: Pandas, Seaborn, Scikit-learn, Matplotlib, XGBoost

## Conclusão

📌 O modelo *XGBoost* apresentou um desempenho ligeiramente superior ao *Random Forest*, com acurácia de **87%** contra **86%**.

## Possíveis complementos futuros

Responder às seguintes questões:
- Quais as categorias mais importantes e influentes para definir o preço médio por quarto?
- A divisão dos dados é equalitária e representativa?
