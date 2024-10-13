# Normalizacja

Normalizacja polega na przekształceniu danych tak, aby mieściły się w określonym zakresie (zwykle od 0 do 1). Jest to przydatne, gdy dane mają bardzo różne skale, a chcemy by na wejściu algorytmu wartości mieściły się w określonym przedziale.

Wzór na normalizację:
$$
x_{norm}= \frac{x - x_{min}}{x_{max} - x_{min}}​​
$$
gdzie:
- $x$ to oryginalna wartość,
- $x_{min}$​ to minimalna wartość w danym zbiorze,
- $x_{max}$ to maksymalna wartość w danym zbiorze.

Przeprowadzenie normalizacji w języku Python możliwe jest przy pomocy biblioteki Scikit-Learn

```Python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
df_normalized = scaler.fit_transform(df)  # Normalizacja całego DataFrame
df_normalized = pd.DataFrame(df_normalized, columns=df.columns)

```

# Standaryzacja

Standaryzacja polega na przekształceniu danych tak, aby miały średnią równą 0 i odchylenie standardowe równe 1. Jest to przydatne, gdy chcemy, aby różne cechy miały porównywalny wpływ na model (niektóre algorytmy jak regresja liniowa czy SVM są bardzo wrażliwe na skalę danych). 

Formuła standaryzacji:
$$
z= \frac{x - \mu}{\sigma}​
$$
gdzie:
- $x$ to oryginalna wartość,
- $\mu$ to średnia wartość cechy,
- $\sigma$ to odchylenie standardowe cechy (pierwiastek wariancji).

Zastosowanie standaryzacji w języku Python możliwe jest przy pomocy biblioteki Scikit-Learn
```Python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
df_standardized = scaler.fit_transform(df)  # Standaryzacja całego DataFrame
df_standardized = pd.DataFrame(df_standardized, columns=df.columns)
```

> [!error] > Należy pamiętać, że po podzieleniu datasetu na zbiór treningowy, walidacyjny i testowy należy wykorzystywać ten sam `imputer` i `skalery` dla wszystkich zbiorów. Oznacza to, że należy wykorzystać `fit` lub `fit_transform` przy zbiorze treningowym, a dla pozostałych wykorzystywać samo `transform`.
# Co dalej?
Przejdź do kolejnego zagadnienia ([[Inżynieria cech]]) lub kliknij [[Przygotowanie danych i inżynieria cech|tutaj]], aby wrócić do strony głównej tematu.