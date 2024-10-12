# Uzupełnianie brakujących wartości

Jeżeli brakuje danych - dana wartość może być pusta, ale może być wstawiona jakaś wartość domyślna (np. w kolumnie `wzrost` mogłyby być wpisane wartości `0`, które od razu widać, że nie mają sensu) - można podjąć następujące kroki:
- poddać się (to nie w naszym stylu),
- usunąć kolumnę - warto zrobić jeżeli w danej kolumnie brakuje wielu danych, których nie ma jak uzupełnić lub są to dane, które nie są użyteczne,
```Python
# Przykładowe dane z brakującymi wartościami
data = {'A': [1, 2, None, 4, 5],
        'B': [None, 2, 3, None, 5],
        'C': [1, None, None, 4, 5]}

# Tworzenie DataFrame
df = pd.DataFrame(data)

df_without_cols = df.drop(columns=['column_name_1', 'column_name_2'])
```
- uzupełnić kolumnę przy pomocy określonej wartości (np. średniej wartości w danej kolumnie, najczęściej występującej wartości w danej kolumnie lub mediany wartości tej kolumny) lub wykorzystać regresję, aby na podstawie danych z innych kolumn uzupełnić te brakujące miejsca.
```Python
from sklearn.impute import SimpleImputer

# Wykorzystamy DataFrame z poprzedniego fragmentu kodu
# Wypełnianie wartością średnią
imputer_mean = SimpleImputer(strategy='mean')
df_imputed_mean = pd.DataFrame(imputer_mean.fit_transform(df), columns=df.columns)

#Wypełnianie medianą
imputer_median = SimpleImputer(strategy='median') 
df_imputed_median = pd.DataFrame(imputer_median.fit_transform(df), columns=df.columns)

# Wypełnianie najczęstszą wartością
imputer_most_frequent = SimpleImputer(strategy='most_frequent') df_imputed_most_frequent = pd.DataFrame(imputer_most_frequent.fit_transform(df), columns=df.columns)

# Wypełnianie stałą wartością podaną przez użytkownika
imputer_constant = SimpleImputer(strategy='constant', fill_value=5) df_imputed_constant = pd.DataFrame(imputer_constant.fit_transform(df), columns=df.columns)

# Metody korzystające z regresji
from sklearn.experimental import enable_iterative_imputer 
from sklearn.impute import IterativeImputer, KNNImputer

# Wypenianie przy pomocy regresji wielokrotnej
iter_imputer = IterativeImputer()
df_iter_imputed = pd.DataFrame(iter_imputer.fit_transform(df), columns=df.columns)

# Wypełnianie za pomocą k-Najbliższych sąsiadów
knn_imputer = KNNImputer(n_neighbors=3)
df_knn_imputed = pd.DataFrame(knn_imputer.fit_transform(df), columns=df.columns)
```

> [!error] > Należy pamiętać, że po podzieleniu datasetu na zbiór treningowy, walidacyjny i testowy należy wykorzystywać ten sam `imputer` i `skalery` dla wszystkich zbiorów. Oznacza to, że należy wykorzystać `fit` lub `fit_transform` przy zbiorze treningowym, a dla pozostałych wykorzystywać samo `transform`.
# Co dalej?
Przejdź do kolejnego zagadnienia ([[Normalizacja i standaryzacja]]) lub kliknij [[Przygotowanie danych i inżynieria cech|tutaj]], aby wrócić do strony głównej tematu.