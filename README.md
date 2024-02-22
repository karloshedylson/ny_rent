# LH_CD_Karlos_Hedylson_Sousa_Silva

---
#### Sobre o dataset:
> Temos um conjunto de dados com 48.894 linhas e 16 colunas, que será utilizado para desenvolver uma estratégia de precificação para uma plataforma de aluguel temporário na cidade de Nova York. Como estamos fazendo uma previsão do preços, este é um problema de **regressão**.

> #### Análise:
> Além das análises desenvolvidas no Juypter Notebook: [NewYork_RentPrediction.ipynb](https://github.com/karloshedylson/ny_rent/blob/main/NewYork_RentPrediction.ipynb), também fizemos um documento em [.PDF](https://github.com/karloshedylson/ny_rent/blob/main/NewYork_RentPrediction.pdf) para auxiliar no entendimento do processo.

#### Modelo escolhido:
> Testamos diferentes modelos de regressão como Linear, Ridge, Lasso, Decision Tree e Random Forest, e avaliando todos com base no R2 Score. Após os testes, identificamos que o modelo de **Random Forest Regression** demonstrou ser o mais eficaz pois obteve um R²-train (0.929) e um R²-test (0.532).

>  Modelo (.pkl) desenvolvido:  [RFRegressor_NewYork.pkl](https://github.com/karloshedylson/ny_rent/blob/main/RFRegressor_NewYork.pkl)


> #### Requisitos:
> **Arquivo de requisitos** com todos os pacotes utilizados: [requirements.txt](https://github.com/karloshedylson/ny_rent/blob/main/requirements.txt)

---

#### Testando o Modelo:

Para testar o Modelo, recomendo utilizar o seguinte código:

``` py
git clone https://github.com/karloshedylson/ny_rent.git
cd ny_rent

# imports:
import pandas as pd
import joblib

def transform_test(data):
    X_test = {
        'nome': [data.get('nome')],
        'room_type': [data.get('room_type')],
        'bairro': [data.get('bairro')],
        'bairro_group': [data.get('bairro_group')],
        'minimo_noites': [data.get('minimo_noites')],
        'numero_de_reviews': [data.get('numero_de_reviews')],
        'reviews_por_mes': [data.get('reviews_por_mes')],
        'calculado_host_listings_count': [data.get('calculado_host_listings_count')],
        'disponibilidade_365': [data.get('disponibilidade_365')]
    }
    return pd.DataFrame(X_test)

model = joblib.load('RFRegressor_NewYork.pkl')

teste = transform_test({
   'id': 2595,
   'nome': 'Skylit Midtown Castle',
   'host_id': 2845,
   'host_name': 'Jennifer',
   'bairro_group': 'Manhattan',
   'bairro': 'Midtown',
   'latitude': 40.75362,
   'longitude': -73.98377,
   'room_type': 'Entire home/apt',
   'price': 225,
   'minimo_noites': 1,
   'numero_de_reviews': 45,
   'ultima_review': '2019-05-21',
   'reviews_por_mes': 0.38,
   'calculado_host_listings_count': 2,
   'disponibilidade_365': 355
})

prediction = model.predict(teste)
print(prediction)
```
