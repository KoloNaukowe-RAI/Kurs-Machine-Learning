# Kodowanie kolumn

W przypadku kolumn, w którym przechowywane są dane tekstowe, kluczowym krokiem jest zamiana tych wartości na wartości numeryczne przed użyciem w modelu uczenia maszynowego. W zależności od charakteru danych można zastosować różne metody:
- kodowanie etykiet (label encoding) - polega na przypisaniu każdej unikalnej wartości tekstowej w kolumnie liczby całkowitej. Wadą może być jeżeli nie ma naturalnego porządku w kategoriach, bo model może zakładać, że wyższe liczby mają większe znaczenie.
```Python
from sklearn.preprocessing import LabelEncoder

le = LabelEncoder()
df['column_name'] = le.fit_transform(df['column_name']) 
#dla zbioru testowego/walidacyjnego należy enkodera utworzonego na zbiorze treningowym (w tym przypadku df):
test_df['column_name'] = le.transform(test_df['column_name'])
```
- one-hot encoding: tworzy osobne kolumny dla każdej unikalnej wartości tekstowej w kolumnie, a następnie przypisuje wartość 0 lub 1 w tych kolumnach, wskazując, czy dana obserwacja zawiera daną kategorię. Zaletą jest, że nie występuje wiele wartości, które mogłyby mylić model, ale wadą jest utworzenie wielu kolumn (co w przypadku rozbudowanych zbiorów danych może bardzo zwiększyć zapotrzebowanie na pamięć do przechowywania datasetu).
```Python
df = pd.get_dummies(df, columns=['column_name'])
```
- mapowanie wartości: ręczne przypisane liczby do wartości tekstowych, co bywa przydatne w przypadku danych z wyraźnym porządkiem logicznym.
```Python
mapping = {'val_1': 1, 'val_2': 2, 'val_3': 3} 
df['column_name'] = df['column_name'].map(mapping)
```

Przykład jak wygląda zakodowanie kolumny `ocena`, w której przechowywane są wartości: `niska`, `średnia` i `wysoka`:

- Podstawowa kolumna:

| Index | Ocena   |
| ----- | ------- |
| 0     | wysoka  |
| 1     | niska   |
| 2     | średnia |
| 3     | średnia |
| 4     | wysoka  |
- Zakodowana kolumna przy pomocy label encoding (`wysoka` -> 0, `niska` -> 1, `średnia` -> 2)

| Index | Ocena |
| ----- | ----- |
| 0     | 0     |
| 1     | 1     |
| 2     | 2     |
| 3     | 2     |
| 4     | 0     |
- Wykorzystanie one-hot encoding:

| Index | niska | średnia | wysoka |
| ----- | ----- | ------- | ------ |
| 0     | 0     | 0       | 1      |
| 1     | 1     | 0       | 0      |
| 2     | 0     | 1       | 0      |
| 3     | 0     | 1       | 0      |
| 4     | 0     | 0       | 1      |
- Wykorzystanie mapowania `{'niska': 0, 'średnia': 1, 'wysoka': 2}`:

| Index | Ocena |
| ----- | ----- |
| 0     | 2     |
| 1     | 0     |
| 2     | 1     |
| 3     | 1     |
| 4     | 2     |

# Data binning (dyskretyzacja danych)

Data binning jest techniką wstępnej obróbki danych, która polega na grupowaniu ciągłych danych liczbowych w dyskretne przedziały lub "koszyki". W efekcie, zamiast mieć nieskończony zestaw możliwych wartości liczbowych, przekształcamy dane na określoną liczbę przedziałów, co ułatwia analizę i może poprawić działanie niektórych modeli uczenia maszynowego.

Zaletami jest uproszczenie interpretacji (na danych ciągłych może być trudność w analizie datasetu), obsługę nieliniowości, zmniejszenie wpływu szumu (po podziale na koszyki drobne fluktuacje mają mniejsze znaczenie, co pozwala zrozumieć ogólne trendy), oraz ułatwienie modelowania, bo część modeli (np. drzewa decyzyjne) mogą działać lepiej, kiedy dane zamiast być ciągłe to są podzielone na przedziały.

Wyróżnić można następujące rodzaje binningu:
- podział na przedziały o równej szerokości (każdy przedział ma taką samą szerokość, ale liczba elementów w każdym koszyku może się różnić),
- podział na przedziały o równej liczebności (każdy przedział ma taką samą liczbę obserwacji, ale szerokość każdego przedziału zależy od rozkładu danych),
- podział na przedziały ze względu na dane i ich zastosowanie (np. kolumna `wiek` mogłaby zostać podzielona na 3 podzbiory `0-18`, `18-65` i `65+`).

Przykład implementacji każdej z przedstawionych metod znajduje się poniżej:
```Python
import pandas as pd

# Przykładowy DataFrame z kolumną 'Wiek'
data_wiek = {'Wiek': [5, 17, 25, 45, 67, 72, 15, 60, 19, 84]}
df_wiek = pd.DataFrame(data_wiek)

# Przedziały o równej szerokości
df_wiek['Wiek_equal_width'] = pd.cut(df_wiek['Wiek'], bins=3, labels=[0, 1, 2])

# Przedziały o równej liczebności
df_wiek['Wiek_equal_freq'] = pd.qcut(df_wiek['Wiek'], q=3, labels=[0, 1, 2])

# Na podstawie własnych reguł na koszyki 0-18, 18-65 i 65+
bins_business = [0, 18, 65, float('inf')]
labels_business = [0, 1, 2]
df_wiek['Wiek_own_rules'] = pd.cut(df_wiek['Wiek'], bins=bins_business, labels=labels_business)
```
# Tworzenie nowych cech

Czasami w procesie analizy danych nie wystarczy po prostu użyć surowych wartości — warto pomyśleć o tym, jak możemy z istniejących danych wyciągnąć dodatkowe informacje lub wyliczyć bardziej użyteczne cechy, które mogą mieć większe znaczenie dla modelu lub analizy. Tego rodzaju proces, zwany **feature engineering**, może znacznie poprawić wyniki modelu i jakość wniosków. Oto kilka przykładów, jak można wykorzystać istniejące dane do wyciągania dodatkowych informacji:
- wyliczenie wartości średniej: np. posiadając liczbę transakcji sklepu w ciągu miesiąca i jaka była suma transakcji w miesiącu można obliczyć średnią, co może mieć znaczenie przy podawaniu danych do modelu,
- obliczenie procentów/proporcji: np. wyliczenie jaki procent transakcji sklepu to zakupy pieczywa,
- sumowanie wartości z kilku kolumn,
- wyciąganie dodatkowych informacji, np. kolumna przechowująca wartości binarne, które powstają przez sprawdzenie warunku "Czy dany sklep ma minimum 15 transakcji w miesiącu i średnią wartość transakcji powyżej 50pln?",
- wyciąganie cech z kolumn tekstowych, np. długość tekstu, ilość słów, ilość hasztagów, występowanie poszczególnych słów, etc.
# Co dalej?

Kliknij [[Przygotowanie danych i inżynieria cech|tutaj]], aby wrócić do strony głównej tematu. Możesz stamtąd przejść do wykonania zadań przygotowanych w Jupyter Notebook.