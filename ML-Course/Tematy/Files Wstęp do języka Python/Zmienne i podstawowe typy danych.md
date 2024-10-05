
# Podstawowe typy danych w języku Python

**Typ danych** określa rodzaj informacji, którą możemy przechowywać w zmiennej. Python jest językiem dynamicznie typowanym, co oznacza, że nie musimy jawnie deklarować typu zmiennej przed jej użyciem. Interpreter automatycznie rozpoznaje typ na podstawie przypisanej wartości.

| Typ    | Opis                      | Przykład          |
| ------ | ------------------------- | ----------------- |
| int    | Liczba całkowita          | `5`, `-123`       |
| float  | Liczba zmiennoprzecinkowa | `1.05`, `-345.12` |
| string | Ciąg znaków               | `"ABCD"`          |
| bool   | Wartość logiczna          | `True, False`     |
Przykłady tworzenia zmiennych poszczególnych typów (do przypisania służy `=`):
```Python
i = 37       # int
f = 92.13    # float
s = "Hello!" # string
b = True     # bool
```

Do sprawdzania typu zmiennej służy funkcja `type(zmienna)`:

```Python
a = 13.23
print(type(a)) # <class 'float'>
```

Ze względu na dynamiczne typowanie, w Pythonie możliwe jest nadpisywanie typu danych, np:

```Python
x = 5.93
x = "Hello"
```

Możliwa jest również konwersja typów przy pomocy funkcji `int(zmienna)`, `float(zmienna)` lub `str(zmienna)`:
```Python
num = 927.27
num_as_str = str(num)
print(num_as_str)      # "927.27"
```

![[PythonDataTypes.png]]
Źródło: [^meme1]

# Operatory

## Dla zmiennych liczbowych

W języku Python dostępne są następujące operatory arytmetyczne do zmiennych liczbowych.

| Operator | Opis                                                |
| -------- | --------------------------------------------------- |
| `+`      | dodawanie                                           |
| `-`      | odejmowanie                                         |
| `*`      | mnożenie                                            |
| `/`      | dzielenie                                           |
| `//`     | dzielenie całkowite (zwraca część całkowitą wyniku) |
| `%`      | modulo (zwraca resztę z dzielenia)                  |
| `**`     | potęgowanie                                         |
Możliwe jest również wykorzystanie skróconych przypisań, co jest przydatne przy zmianie wartości, a służą do tego `+=`, `-=`, `*=`, `/=`, `%=`, `**=`.

## Dla zmiennych typu string

Dla ciągów znaków nie można bezpośrednio zastosować tych samych operatorów arytmetycznych. Konieczna jest wpierw konwersja stringa na liczbę przy użyciu `int(zmienna)` lub `float(zmienna)`. Stringi są niemutowalne, więc nie można zmienić pojedynczych znaków, a trzeba utworzyć nowy string.

Funkcje/operatory dostępne do wykorzystania ze stringami:


| Funkcja/Operator                 | Opis działania                                     | Przykład                                                | Wynik przykładu                |
| -------------------------------- | -------------------------------------------------- | ------------------------------------------------------- | ------------------------------ |
| `+`                              | Łączy stringi w jeden dłuższy                      | `a = "AB"+"CD"`                                         | `"ABCD"`                       |
| `*`                              | Powtarza string określoną liczbę razy              | `b = "ok" * 3`                                          | `"okokok"`                     |
| `[]`                             | Dostęp do znaków/podciągów w stringu               | `c = "Pies"   d = c[0]   e = c[2:3]`                    | `d = "P"  e = "es"`            |
| `==`, `!=`, `<`, `>`, `<=`, `>=` | Operatory porównania                               | `f = ("Pies" > "Koń")`                                  | `False`                        |
| `in`, `not in`                   | Sprawdza, czy dany podciąg występuje w stringu     | `g = "Mam 2 psy"   h = "psy" in g`                      | `True`                         |
| `len(zmienna)`                   | Zwraca długość stringa (ilość znaków)              | `i = len("abc")`                                        | `3`                            |
| `zmienna.upper()`                | Konwertuje wszystkie litery na wielkie             | `j = "Abc"    j.upper()`                                | `"ABC"`                        |
| `zmienna.lower()`                | Konwertuje wszystkie litery na małe                | `k = "EdF"    k.lower()`                                | `"edf"`                        |
| `zmienna.find(substring)`        | Zwraca indeks pierwszego wystąpienia podciągu      | `l = "Mam 2 psy"   l.find("Mam")`                       | `0`                            |
| `zmienna.replace(old, new)`      | Zastępuje wszystkie wystąpienia `old` na `new`     | `m = "Mam 2 psy. Mam 1 kota"   m.replace("Mam","Masz")` | `"Masz 2 psy. Masz 1 kota"`    |
| `zmienna.split(separator)`       | Dzieli string na listę podciągów według separatora | `n = "Mam 2 psy. Mam 1 kota"   n.split(".")`            | `['Mam 2 psy', ' Mam 1 kota']` |
# Co dalej
Przejdź do kolejnego zagadnienia ([[Listy, krotki, zbiory i słowniki]]) lub kliknij [[Wstęp do języka Python|tutaj]], aby wrócić do strony głównej tematu.
# Źródła:
[^meme1]: https://programmerhumor.io/python-memes/im-a-python-programmer-2/