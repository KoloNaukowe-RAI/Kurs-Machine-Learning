Pandas to biblioteka w języku Python, stworzona z myślą o łatwiej i efektywnej analizie danych.

Pandas pozwala na szybkie, elastyczne i intuicyjne operacje na danych, zarówno jednowymiarowych (Series), jak i wielowymiarowych (DataFrame).

 [Eksploracja Danych]
 
Możliwości biblioteki Pandas:

1. **Wczytywanie i zapisywanie danych w różnych formatach:**  CSV, Excel, JSON i SQL
2. **Przekształcanie i czyszczenie danych:** 
- Usuwanie wybranych kolumn 
- Wyświetlanie i zliczanie unikalnych wartości w kolumnach 
- Usuwanie brakujących wartości 
- Uzupełnianie brakujących wartości
3. **Analiza statystyczna:** 
- Wyświetlanie podstawowych statystyk opisowych
- Wyświetlanie liczby wierszy i kolumn DataFrame 
- Wyświetlanie typów danych w każdej kolumnie
4. **Wizualizacja danych:** 
- Integracja z bibliotekami do wizualizacji danych (np. Matplotlib, Seaborn)

**Wczytywanie i zapis danych:**

**Wczytywanie danych z pliku  CSV:**
```python 
   import pandas as pd 
   df = pd.read_csv('plik.csv')
```

**Zapis danych jako pliku CSV:**
```python 
   df.to_csv('nowy_plik.csv', index=False)
```

**Wczytywanie danych z pliku Excel:**
```python  
   df = pd.read_excel('plik.xlsx')
```

**Wczytywanie danych z pliku JSON:**
```python 
   df = pd.read_json('plik.json')
```

**Podstawowe Operacje na DataFrame**:

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

- **Wyświetlanie liczby wierszy i kolumn Dataframe:**

```python
print(df.shape)
```

 - **Wyświetlanie typów danych w każdej kolumnie**:
```python
print(df.dtypes)
```

 - **Wyświetlanie kolumn**:
```python
print(df.columns)
```

**Przekształcanie, czyszczenie i transformacje danych**: 

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

**Filtrowanie wierszy, gdzie wartość w kolumnie 'wiek' jest większa niż 25:**
```python
df_filtered = df[df['wiek'] > 25]
```

**Filtrowanie wierszy, gdzie wartość w kolumnie 'wiek' jest większa niż 25 i w kolumnie 'miasto' jest równa 'Poznań':**
```python
df_filtered = df[(df['wiek'] > 25) & (df['miasto'] == 'Poznań')]
```

**Grupowanie danych i obliczanie statystyk dla każdej grupy:**
```python
grouped = df.groupby('nazwa_kolumny').mean()
```

**Sortowanie danych według wybranej kolumny:**
```python
df_sorted = df.sort_values(by='nazwa_kolumny', ascending=True)
```

**Zmian nazw kolumn:**
```python
df.rename(columns={'stara_nazwa': 'nowa_nazwa'}, inplace=True)
```

Numpy to podstawowa biblioteka w języku Python, używana do obliczeń naukowych i analizy danych. Oferuje struktury danych, takie jak tablice wielowymiarowe (ndarray) i funkcje matematyczne.
## Możliwości biblioteki numpy

1. **Tworzenie i manipulowanie tablicami wielowymiarowymi:**
- Tworzenie tablic z list, zakresów, plików 
- Operacje matematyczne na tablicach -
- Indeksowanie i wycinanie tablic
- Zmiana kształtu tablic 
2. **Funkcje matematyczne i statystyczne:**
- Podstawowe operacje matematyczne (dodawanie, odejmowanie, mnożenie, dzielenie)
- Funkcje trygonometryczne 
- Funkcje statystyczne (średnia, mediana, odchylenie standardowe) 
3. **Algebra liniowa:**
- Mnożenie macierzy 
- Wyznacznik macierzy
- Rozwiązywanie układów równań liniowych
- Wartości własne i wektory własne
4. **Generowanie liczb losowych z różnych rozkładów (normalny, jednostajny, itp.) **
5. **Wczytywanie i zapisywanie danych**


**Tworzenie tablicy z samymi zerami:**
```python
a = np.zeros((3, 4)) # 3 wiersze, 4 kolumny
```
\
**Obliczanie średniej:**
```python
a = np.array([1, 2, 3, 4, 5])
mean = np.mean(a)
print(mean)
```
