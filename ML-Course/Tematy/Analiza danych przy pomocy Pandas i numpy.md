Pandas to biblioteka w języku Python, stworzona z myślą o łatwiej i efektywnej analizie danych. Możliwości biblioteki Pandas:
>
>1. **Wczytywanie i zapisywanie danych w różnych formatach:**  CSV, Excel, JSON i SQL
>2. **Przekształcanie i czyszczenie danych** 
>3. **Analiza statystyczna
>4. Wizualizacja danych

>[!important]
>Pandas pozwala na szybkie, elastyczne i intuicyjne operacje na danych, zarówno jednowymiarowych (Series), jak i wielowymiarowych (DataFrame).
>
>DataFrame przypomina dwuwymiarową tablicę NumPy, ale ma etykiety kolumn i wierszy, a każda kolumna może zawierać różne typy danych. Wyodrębniając pojedynczą kolumnę lub wiersz z DataFrame, otrzymujemy jednowymiarowy obiekt Series, który przypomina jednowymiarową tablicę NumPy z etykietami.

![[series_pandas.png]]

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

| Metody          | Opis                                                                                                                               |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `df.tail()`     | Wyświetla ostatnich 5 wierszy z DataFrame, aby szybko przejrzeć końcówkę danych. <br>                                              |
| `df.info()`<br> | Zwraca szczegółowe informacje o strukturze DataFrame, w tym liczbie wierszy, kolumn, typach danych i brakujących wartościach. <br> |
| `df.describe()` | Generuje podstawowe statystyki opisowe (np. średnia, odchylenie standardowe, min, max) dla danych numerycznych w DataFrame. <br>   |
| `df.shape`      | Zwraca krotkę z liczbą wierszy i kolumn w DataFrame. <br>                                                                          |
| `df.dtypes`     | Wyświetla typ danych każdej kolumny w DataFrame, co pomaga zrozumieć strukturę danych.                                             |
| `df.columns`    | Wyświetla listę nazw kolumn, ułatwiając szybkie sprawdzenie, jakie dane są dostępne w DataFrame. <br>                              |

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

>[!important]
>
>W zastosowaniach statystycznych dane niedostępne mogą być danymi, które nie istnieją, lub danymi które istnieją, ale nie zostały zaobserwowane (np. z powodu problemu wynikającego ze sposobu zbierania danych).
>
>Podczas oczyszczania danych przed przeprowadzeniem ich analizy często warto przeprowadzić analizę samych brakujących wartości. 

| Argument   | Opis                                                                                                                                                                              |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **dropna** | Filtruje etykiety osi na podstawie występowania brakujących danych; możliwe jest zdefiniowanie zmiennych wartości progowych określających liczbę tolerowanych brakujących danych. |
| **fillna** | Wypełnia brakujące dane jakimiś wartościami lub robi to za pomocą metody interpolacji, takiej jak np. "ffill" lub "bfill".                                                        |
| **isna**   | Zwraca wartości logiczne określające miejsce występowania brakujących wartości.                                                                                                   |
| **notna**  | Negacja isna. Zwraca True, jeżeli wartość istnieje, a False w przeciwnym wypadku.                                                                                                 |


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

### Statystyka opisowa 

Statystyka opisowa pozwala na podsumowanie zbiorów danych za pomocą miar ilościowych. Dla przykładu prostą statystyką opisową jest liczba punktów danych. Innymi popularnymi przykładami są średnie, mediany lub dominanty. Obiekty DataFrame i Series zapewniają wygodny dostęp do statystyk opisowych za pomocą metod takich jak sum, mean i count.

| Metoda       | Opis                                                                  |
| ------------ | --------------------------------------------------------------------- |
| `mean()`     | Oblicza średnią dla kolumn numerycznych.                              |
| `sum()`      | Sumuje wartości w kolumnach.                                          |
| `std()`      | Oblicza odchylenie standardowe.                                       |
| `describe()` | Zwraca szczegółowe podsumowanie statystyczne dla kolumn numerycznych. |
| `groupby()`  | Grupuje dane na podstawie wskazanej kolumny.                          |
| `agg()`      | Pozwala zastosować różne funkcje agregujące (np. `mean`, `sum`).      |


```python
import pandas as pd  
  
# Dane z firmy w działach w róznych miastach 
data = {  
    "Miasto": ["Warszawa", "Kraków", "Poznań", "Wrocław", "Gdańsk", "Sopot", "Zakopane", "Łódź"],  
    "Kawa (litry)": [200.5, 300.1, 280.3, 400.4, 310.2, 270.6, 150.3, 320.9],  
    "Brak snu (godziny)": [50, 100, 90, 130, 80, 95, 40, 85],  
    "Dział": ["Produkcja", "HR", "IT", "Produkcja", "Marketing", "IT", "Produkcja", "HR"]  
}  
   
df = pd.DataFrame(data)  
opis = df.describe()  
  
# Grupowanie danych na podstawie działu  
grupa_dzial = df.groupby("Dział").agg({  
    "Kawa (litry)": ["mean", "sum"],  
    "Brak snu (godziny)": ["mean", "sum"]  
})  
  

print("=== Statystyka opisowa dla pracowników  ===\n")  
print(opis)  
  
print("\n=== Średnie spożycie kawy oraz brak snu w różnych działach ===\n")  
print(grupa_dzial)  
  
# Szukamy działu, w którym pracownicy potrzebują najwięcej kawy  
dzial_max_kawa = df.groupby("Dział")["Kawa (litry)"].sum().idxmax()  
  
print(f"\nNajwięcej kawy pije dział: {dzial_max_kawa})

1. 
		Kawa (litry)  Brak snu (godziny)
count       8.000000            8.000000
mean      279.162500           83.750000
std        71.570789           28.643055
min       150.300000           40.000000
25%       255.225000           77.500000
50%       290.250000           87.500000
75%       312.675000           95.000000
max       400.400000          130.000000


2.

				Kawa (litry)        Brak snu (godziny)     
                  mean    sum               mean  sum
Dział                                                
HR              310.50  621.0          92.500000  185
IT              275.45  550.9          92.500000  185
Marketing       310.20  310.2          80.000000   80
Produkcja       250.40  751.2          73.333333  220
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

## Przekształcanie danych za pomocą mapowania

Mapowanie polega na zastąpieniu jednej wartości inną, np. w oparciu o słownik.
#### Mapowanie wartości za pomocą słownika

W przykładzie mamy dane dotyczące produktów mięsnych, a my chcemy dodać kolumnę z informacją o zwierzęciu, z którego pochodzi dany produkt.

```python
import pandas as pd  
  
data = pd.DataFrame({  
    'food': ['bacon', 'pulled pork', 'bacon', 'Pastrami', 'corned beef', 'Bacon', 'pastrami', 'honey ham', 'nova lox'],  
    'ounces': [4, 3, 12, 6, 7.5, 8, 3, 5, 6]  
})  
  
meat_to_animal = {  
    'bacon': 'pig',  
    'pulled pork': 'pig',  
    'pastrami': 'cow',  
    'corned beef': 'cow',  
    'honey ham': 'pig',  
    'nova lox': 'salmon'  
}  
  
# Zmapowanie typu mięsa na zwierzę  
data['animal'] = data['food'].str.lower().map(meat_to_animal)  
print(data)
```

Rezultat:

|     | food        | ounces | animal |
| --- | ----------- | ------ | ------ |
| 0   | bacon       | 4.0    | pig    |
| 1   | pulled pork | 3.0    | pig    |
| 2   | bacon       | 12.0   | pig    |
| 3   | Pastrami    | 6.0    | cow    |
| 4   | corned beef | 7.5    | cow    |
| 5   | Bacon       | 8.0    | pig    |
| 6   | pastrami    | 3.0    | cow    |
| 7   | honey ham   | 5.0    | pig    |
| 8   | nova lox    | 6.0    | salmon |


>[!important]
>**Szeregi czasowe to jedna z kluczowych funkcjonalności Pandas, zwłaszcza gdy pracujemy z danymi finansowymi, meteorologicznymi czy jakimikolwiek danymi zależnymi od czasu**

Zacznijmy od prostego przykładu pracy z datami, które przekształcimy z łańcuchów znaków na znacznik czasu.
### Moduł `datetime`: Podstawowe narzędzia pracy z datami

Moduł **`datetime`** w Pythonie pozwala na tworzenie, manipulowanie i formatowanie dat oraz czasu. Używając go, możemy wykonywać podstawowe operacje na obiektach daty i czasu.

#### Tworzenie daty i czasu

Aby utworzyć obiekt daty w Pythonie, korzystamy z klasy **`datetime`**:
```python
import pandas as pd

# Konwersja daty z tekstu na obiekt Timestamp
date = pd.to_datetime("2021-07-04")
print(date)  # Wynik: 2021-07-04 00:00:00
```

#### Parsowanie daty z tekstu za pomocą `dateutil`

Jeśli mamy daty w formacie tekstowym, możemy użyć modułu **`dateutil`**, który automatycznie rozpoznaje różne formaty dat.

```python
from dateutil import parser

# Parsowanie daty z tekstu
date = parser.parse("4th of July, 2021")
print(date)  # Wynik: 2021-07-04 00:00:00
```
### Generowanie zakresu dat

Czasami chcesz stworzyć listę dat, np. wszystkie dni w określonym okresie. Używamy do tego funkcji **`pd.date_range()`**.

 Funkcja pd.date_range przyjmuje datę początkową, datę końcową i opcjonalny kod częstotliwości oraz zwraca regularną sekwencję dat.


```python
# Tworzenie zakresu dat od 1 stycznia do 7 stycznia 2023
date_range = pd.date_range('2023-01-01', '2023-01-07')
print(date_range)
```
### Tworzenie danych z tygodniową częstotliwością

Można łatwo wygenerować daty co tydzień za pomocą funkcji **`pd.date_range()`** z argumentem `freq`.

```python
# Generowanie dat co tydzień, od 1 stycznia 2023, przez 4 tygodnie
weekly_dates = pd.date_range('2023-01-01', periods=4, freq='W')
print(weekly_dates)
```

### Przesuwanie danych w czasie 

W Pandas służy do tego metoda shift, która pozwala przesunąć dane w czasie o określoną liczbę wpisów. W przypadku szeregów czasowych próbkowanych z równomierną częstotliwością metoda ta pozwala na zbadanie trendów w czasie.

```python
import pandas as pd  
  
data = pd.DataFrame({  
    'sales': [300, 320, 310, 330, 340],  
    'date': pd.date_range(start='2023-01-01', periods=5, freq='D')  
}).set_index('date')  

data['previous_day_sales'] = data['sales'].shift(1)  
data['sales_increase'] = data['sales'] > data['previous_day_sales']  
print(data) 

#Wynik 
#           sales  previous_day_sales  sales_increase
#date                                                 
#2023-01-01    300                 NaN           False
#2023-01-02    320               300.0            True
#2023-01-03    310               320.0           False
#2023-01-04    330               310.0            True
#2023-01-05    340               330.0            True
```

### Ruchome okna 

Obliczanie statystyk kroczących jest kolejnym rodzajem operacji specyficznych dla szeregów czasowych, które znajdziemy w Pandas. Statystyki te można obliczyć za pomocą atrybutu rolling obiektów typu Series i DataFrame. Opcja ta pozwala na tworzenie miar statystycznych, takich jak średnia krocząca, suma krocząca czy odchylenie standardowe kroczące.


>[!important]
> Obliczanie statystyk na określonym "ruchomym" oknie danych polega na tym, że przekształcamy dane na podstawie bieżących wartości oraz wcześniejszych obserwacji z określonego przedziału (np. liczby dni, tygodni). 

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Przykładowe dane czasowe (ceny akcji)
dates = pd.date_range(start='2023-01-01', periods=30, freq='D')
prices = np.random.randint(100, 200, size=len(dates))

data = pd.DataFrame({'price': prices}, index=dates)

# 7-dniowa średnia krocząca
data['7_day_mean'] = data['price'].rolling(window=7).mean()

# Wykres
plt.figure(figsize=(10, 6))
plt.plot(data.index, data['price'], label='Cena akcji')
plt.plot(data.index, data['7_day_mean'], label='7-dniowa średnia krocząca', linestyle='--')
plt.title("7-dniowa średnia krocząca cen akcji")
plt.xlabel("Data")
plt.ylabel("Cena akcji")
plt.legend()
plt.grid(True)
plt.show()

```
![[ruchome_okna.png]]
### **Strefy czasowe w Pythonie**

Praca ze strefami czasowymi to wyzwanie w analizie danych czasowych, zwłaszcza jeśli dane pochodzą z różnych lokalizacji. W tym celu można używać biblioteki **`pytz`**, która umożliwia zarządzanie strefami czasowymi.

- **Kluczowe operacje**:
    - Przekształcanie dat pomiędzy strefami czasowymi.
    - Zarządzanie czasem lokalnym i UTC.
    
```python
import pandas as pd  
import pytz  
  
# Dane dotyczące transakcji
data = {'transaction_time': ['2023-01-01 10:00:00', '2023-01-01 14:00:00', '2023-01-02 09:30:00'],  
        'city': ['New York', 'London', 'Tokyo']}  
  
df = pd.DataFrame(data)  
  
# Upewnienie się ze 'transaction_time' jest w formacie datetime  
df['transaction_time'] = pd.to_datetime(df['transaction_time'])  
  
# Nowa kolumna z przypisanymi strefami czasowymi  
df['transaction_time'] = df['transaction_time'].dt.tz_localize('UTC')  # Lokalizacja dat w UTC  
  
# Dostosowanie stref czasowych dla odpowiednich miast  
df.loc[df['city'] == 'New York', 'transaction_time'] = df.loc[df['city'] == 'New York', 'transaction_time'].dt.tz_convert('America/New_York')  
df.loc[df['city'] == 'London', 'transaction_time'] = df.loc[df['city'] == 'London', 'transaction_time'].dt.tz_convert('Europe/London')  
df.loc[df['city'] == 'Tokyo', 'transaction_time'] = df.loc[df['city'] == 'Tokyo', 'transaction_time'].dt.tz_convert('Asia/Tokyo')  
  
print(df) 
#Wynik
#           transaction_time      city
#0 2023-01-01 10:00:00+00:00  New York
#1 2023-01-01 14:00:00+00:00    London
#2 2023-01-02 09:30:00+00:00     Tokyo
```
#### Tworzenie daty z `datetime64`

Tworzenie obiektu `datetime64` jest proste – wystarczy podać datę jako łańcuch znaków i określić typ danych:

```python
import numpy as np
# Znacznik czasu na poziomie dnia  
date_day = np.datetime64('2021-07-04', 'D')  
print(date_day)  # Wynik: 2021-07-04  
  
# Znacznik czasu na poziomie minut  
date_minute = np.datetime64('2021-07-04 12:00', 'm')  
print(date_minute)  # Wynik: 2021-07-04T12:00  
  
# Znacznik czasu na poziomie nanosekund  
date_ns = np.datetime64('2021-07-04 12:59:59.50', 'ns')  
print(date_ns)  # Wynik: 2021-07-04T12:59:59.500000000

```

#### Operacje wektorowe na datach

NumPy pozwala na wykonywanie operacji wektorowych na dużych zbiorach dat. Możemy np. dodać dni do istniejącej daty:

```python
import numpy as np

# Tworzenie daty w formacie datetime64
date_np = np.datetime64('2024-19-10')
print(date_np)  # Wynik: 2024-19-10
date_range = date_np + np.arange(12)  
print(date_range)

#wynik 
['2021-07-04' '2021-07-05' '2021-07-06' '2021-07-07' '2021-07-08'
 '2021-07-09' '2021-07-10' '2021-07-11' '2021-07-12' '2021-07-13'
 '2021-07-14' '2021-07-15']
```


> 🛑 **Uwaga: Kiedy używać `datetime64` z NumPy?**
> - <span style="color:red">Kiedy pracujesz z dużymi zbiorami danych czasowych.</span>
> - <span style="color:red">Kiedy potrzebujesz wydajności w operacjach wektorowych na datach (np. dodawanie, odejmowanie dni).</span>
> - <span style="color:red">Kiedy wymagana jest precyzja w nanosekundach lub chcesz skorzystać z szybkich operacji na datach.</span>

### Formatowanie i kody formatów

NumPy i `datetime` oferują różne kody formatu, które można używać do manipulowania wyświetlaniem dat. 

```python
from datetime import datetime

# Wyświetlanie w formacie 'YYYY-MM-DD HH:MM:SS'
formatted_date = datetime.now().strftime('%Y-%m-%d %H:%M:%S')
print(formatted_date) # Wynik 2024-10-19 15:38:34
```

![[tabela_data.png]]

Oprócz `datetime64`, NumPy oferuje typ **`timedelta64`**

Służący do przechowywania czasów trwania lub odstępów czasu dostępny. Jest on wydajniejszym zamiennikiem natywnego typu datetime.timedelta z Pythona, bazującym na typie numpy.timedelta64. 

```python
import numpy as np

# Obliczanie różnicy między datami
date1 = np.datetime64('2023-01-01')
date2 = np.datetime64('2023-01-10')

difference = date2 - date1
print(difference)  # Wynik: 9 days
```


>[!important]
>Na co pozwala biblioteka Numpy?
>1. **Tworzenie i manipulowanie tablicami wielowymiarowymi:**
>- Tworzenie tablic z list, zakresów, plików 
>- Operacje matematyczne na tablicach -
>- Indeksowanie i wycinanie tablic
>- Zmiana kształtu tablic 
>2. **Funkcje matematyczne i statystyczne:**
>- Podstawowe operacje matematyczne (dodawanie, odejmowanie, mnożenie, dzielenie)
>- Funkcje trygonometryczne 
>- Funkcje statystyczne (średnia, mediana, odchylenie standardowe) 
>3. **Algebra liniowa:**
>- Mnożenie macierzy 
>- Wyznacznik macierzy
>- Rozwiązywanie układów równań liniowych
>- Wartości własne i wektory własne
>4. **Generowanie liczb losowych z różnych rozkładów (normalny, jednostajny, itp.) **
>5. **Wczytywanie i zapisywanie danych**

**Tworzenie tablicy z samymi zerami:**
```python
a = np.zeros((3, 4)) # 3 wiersze, 4 kolumny
```

**Obliczanie średniej:**
```python
a = np.array([1, 2, 3, 4, 5])
mean = np.mean(a)
print(mean)
```

# Link do Jupyter Notebook

Ćwiczenia dla tego tematu zostały zebrane [tutaj](https://github.com/KoloNaukowe-RAI/Kurs-Machine-Learning/blob/main/Tasks/Tasks02_Zapoznanie_z_biblioteką_pandas.ipynb).

# Co dalej?

Kliknij [[Index|tutaj]], aby wrócić do strony głównej kursu.