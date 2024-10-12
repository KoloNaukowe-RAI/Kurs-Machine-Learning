# Sprawdzenie danych

Pierwszym co należy zrobić przed przystąpieniem do uczenia implementacji algorytmów uczenia maszynowego jest przejrzenie datasetu. Korzystając z poznanych wcześniej bibliotek możemy użyć następujących komend:
- sprawdzenie liczby brakujących wartości w poszczególnych kolumnach:
```Python
print(pandas_dataframe.isnull().sum())
```
- obliczenie korelacji pomiędzy poszczególnymi kolumnami i wyświetlenie ich w formie macierzy korelacji:
```Python
# Wyliczenie macierzy korelacji
corr = pandas_dataframe.corr()

# Przygotowanie wykresu i wyświetlenie go (wymaga importowania seaborn i matplotlib)
plt.figure()
sns.heatmap(corr, annot=True, cmap='coolwarm', fmt=".2f")

plt.title('Correlation Matrix')
plt.show()
```
-  sprawdzić jakie unikalne wartości przyjmują dane w określonej kolumnie:
```Python
pandas_dataframe['column_name'].unique()
```
- wyświetlić dane numeryczne w formie histogramu:
```Python
pandas_dataframe['column_name'].plot.hist(bins=5, color='red', edgecolor='black')
```

# Usuwanie wartości odstających

Wartości odstające, zwane również outliers, to wartości, które znacznie różnią się od reszty danych. W rezultacie mogą one niekorzystnie wpływać na wyniki analizy danych i modele uczenia maszynowego poprzez:
- znaczne wpływanie na średnią, wariancję i inne statystyki opisowe,
- wprowadzanie szumu do modeli,
- prowadzenie do błędnych wniosków z analizy danych.

W jaki sposób można sobie poradzić, jeżeli w danych występują wartości odstające:
- usunięcie outlierów (np. jeżeli wynikają z błędu pomiaru lub wpisania danych i nie da się ich przybliżyć do reszty danych),
- winsoryzacja - zamiana wartości odstających na wartości graniczne pewnego przedziału (np. na wartości 95 percentyla),
- zamiana wartości odstających medianą (dzięki temu mniej wpływają na rozkład),
- wykorzystać normalizację, standaryzację lub podział danych na przedziały (o tym na dalszych podstronach).

## Jak identyfikować wartości odstające?

Najprostszą metodą identyfikacji wartości odstających jest użycie reguły rozstępu międzykwartylowego (IQR)[^1].

- IQR (Interquartile Range): Różnica między trzecim kwartylem (75 percentyl) a pierwszym kwartylem (25 percentyl).
- Outliery są wartościami, które są poniżej $Q1−1.5\cdot IQR$ lub powyżej $Q3+1.5 \cdot IQR$.

Implementacja identyfikacji wartości odstających i winsoryzacji oraz filtrowania znajduje się poniżej:
```Python
import pandas as pd
import numpy as np

# Utworzenie dataframe
data = {'Wartość': [10, 12, 14, 15, 100, 13, 14, 16, 12, 13, 11, 110]}
df = pd.DataFrame(data)

# 1. Obliczenie Q1 (pierwszego kwartylu) i Q3 (trzeciego kwartylu)
Q1 = df['Wartość'].quantile(0.25)
Q3 = df['Wartość'].quantile(0.75)
IQR = Q3 - Q1  # Rozstęp międzykwartylowy

# 2. Definiowanie granic dla wartości odstających
lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

# 3. Usunięcie danych odstających
df_no_outliers = df[(df['Wartość'] >= lower_bound) & (df['Wartość'] <= 
		upper_bound)]

# 4. Winsoryzacja - zastępowanie outlierów wartościami granicznymi 
df_winsorized = df.copy() 
df_winsorized['Wartość'] = np.where(df_winsorized['Wartość'] > upper_bound, 
		upper_bound, np.where(df_winsorized['Wartość'] < lower_bound, 
		lower_bound, df_winsorized['Wartość']))
```
# Co dalej?
Przejdź do kolejnego zagadnienia ([[Brakujące dane]]) lub kliknij [[Przygotowanie danych i inżynieria cech|tutaj]], aby wrócić do strony głównej tematu.

# Źródła:
[^1]: https://en.wikipedia.org/wiki/Interquartile_range