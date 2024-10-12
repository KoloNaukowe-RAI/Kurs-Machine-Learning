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

# Co dalej?
Przejdź do kolejnego zagadnienia ([[Brakujące dane]]) lub kliknij [[Przygotowanie danych i inżynieria cech|tutaj]], aby wrócić do strony głównej tematu.
