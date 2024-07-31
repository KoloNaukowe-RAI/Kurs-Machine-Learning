Pandas to biblioteka w języku Python, stworzona z myślą o łatwiej i efektywnej analizie danych.

Pandas pozwala na szybkie, elastyczne i intuicyjne operacje na danych, zarówno jednowymiarowych (Series), jak i wielowymiarowych (DataFrame).

 [Eksploracja Danych]
 
 
Pandas obsługuje wczytywanie i zapisywanie danych w różnych formatach (CSV, Excel, SQL, JSON), przekształcanie i czyszczenie danych, analizę statystyczną oraz wizualizację danych.

**Wczytywanie danych z pliku  CSV:**
```python 
   import pandas as pd 
   df = pd.read_csv('plik.csv')
```

**Wczytywanie danych z pliku Excel:**
```python  
   df = pd.read_excel('plik.xlsx')
```

**Wczytywanie danych z pliku JSON:**
```python 
   df = pd.read_json('plik.json')
```

- **Wyświetlanie ostatnich 5 wierszy:**
   ```python 
   print(df.tail()) 
   ```

 - **Wyświetlanie informacji o DataFrame:**
   ```python 
   print(df.info()) 
   ```

- **Wyświetlanie podstawowych statystyk opisowych:**
```python
print(df.describe())
```

 **Wyświetlanie liczby wierszy i kolumn Dataframe:**
```python
print(df.shape)
```

 **Wyświetlanie  typów danych w każdej kolumnie :**
```python
print(df.dtypes)
```

 **Wyświetlanie kolumn**:
```python
print(df.columns)
```

 **Wyświetlanie i zliczanie unikalnych wartości w kolumnie :**
```python
print(df.['nazwa_kolumny'].unique())

print(df.['nazwa_kolumny'].value_counts())
```

 **Usuwanie wybranej kolumny:**
```python
df.drop(columns=['nazwa_kolumny'], inplace=True)
```

**Wyświetlanie brakujących danych:**
```python
print(df.isnull().sum())
```

**Usuwanie brakujących wartości**
```python
df.dropna(inplace=True)
```

**Uzupełnianie brakujących wartości**
```python
df.fillna(0, inplace=True)
```
