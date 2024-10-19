# Struktury danych w Python

W Pythonie możemy wyróżnić następujące struktury danych: listy, krotki, zbiory i słowniki.

- **Listy** są najbardziej uniwersalnymi strukturami danych w Pythonie. Są to uporządkowane, mutowalne kolekcje, które mogą zawierać dowolne elementy. Możesz dodawać, usuwać i modyfikować elementy listy.

- **Tuple** (krotki) są podobne do list, ale są niemutowalne, czyli po utworzeniu nie można zmieniać ich elementów. Są często używane do przechowywania danych, które nie powinny być modyfikowane.

- **Sety** (zbiory) są nieuporządkowanymi zbiorami unikalnych elementów. Nie mogą zawierać duplikatów. Sety są używane do sprawdzania przynależności elementów, wykonywania operacji zbiorów (np. przecięcia, sumy) oraz usuwania duplikatów z sekwencji.

- **Słowniki** to struktury danych, które przechowują pary klucz-wartość. Każdy klucz musi być unikalny. Słowniki są używane do szybkiego wyszukiwania wartości na podstawie klucza.

# Przykłady tworzenia poszczególnych struktur

```Python
# List
numbers_list = [1, 2, 3, 4, 2]
mixed_list = [1, "hello", 3.14, True]

# Tuple
numbers_tuple = (1, 2, 3, 4, 2)
mixed_tuple = (1, "hello", 3.14, True)

# Set
numbers_set = {1, 2, 3, 4, 2}   # Przechowa jedynie unikalne wartosci {1,2,3,4} 
mixed_set = {1, "hello", 3.14, True}

# Dictionary
num_as_key = {25: "John", 30: "Jane"}
str_as_key = {"name": "Alice", "age": 28, "city": "London"}
```

# Operacje na poszczególnych strukturach

## List

```Python
# Tworzenie listy
fruits = ["apple", "banana", "cherry"]

# Dodawanie elementu na koniec
fruits.append("orange")
print(fruits)  # Wynik: ['apple', 'banana', 'cherry', 'orange']

# Wstawianie elementu na określone miejsce
fruits.insert(1, "grape")
print(fruits)  # Wynik: ['apple', 'grape', 'banana', 'cherry', 'orange']

# Usuwanie elementu po wartości
fruits.remove("banana")
print(fruits)  # Wynik: ['apple', 'grape', 'cherry', 'orange']

# Usuwanie elementu po indeksie
del fruits[2]
print(fruits)  # Wynik: ['apple', 'grape', 'orange']

# Dostęp do elementu
print(fruits[0])  # Wynik: apple

# Długość listy
print(len(fruits))  # Wynik: 3

# Sortowanie listy (rosnąco)
fruits.sort()
print(fruits)  # Wynik: ['apple', 'grape', 'orange'] (sortowanie alfabetyczne)

# Sortowanie malejąco
fruits.sort(reverse=True)
```

## Tuple

Krotki są niemutowalne, więc nie można dodawać ani usuwać elementów po ich utworzeniu!!! Aby zrobić zmiany można skopiować wartości z już istniejącej tupli do nowej.
```Python
# Tworzenie tuple
numbers = (1, 2, 3)

# Dostęp do elementu
print(numbers[1])  # Wynik: 2

# Długość tuple
print(len(numbers))  # Wynik: 3
```

## Sety

```Python
# Tworzenie setu
my_set = {1, 2, 3, 2}  # Duplikaty są usuwane

# Dodawanie elementu
my_set.add(4)
print(my_set)  # Wynik: {1, 2, 3, 4}

# Usuwanie elementu
my_set.remove(2)
print(my_set)  # Wynik: {1, 3, 4}

# Długość setu
print(len(my_set))  # Wynik: 3

# Operacje na zbiorach (przecięcie, suma, różnica)
set1 = {1, 2, 3}
set2 = {2, 3, 4}
print(set1.union(set2))  # Suma zbiorów: {1, 2, 3, 4}
print(set1.intersection(set2))  # Przecięcie zbiorów: {2, 3}
```

## Słowniki

```Python
# Tworzenie słownika
person = {"name": "John", "age": 30, "city": "New York"}

# Dodawanie pary klucz-wartość
person["country"] = "USA"
print(person)

# Usuwanie pary klucz-wartość
del person["age"]
print(person)

# Dostęp do wartości
print(person["name"])  # Wynik: John

# Długość słownika (liczba par klucz-wartość)
print(len(person))  # Wynik: 2

# Sprawdzenie, czy klucz istnieje
if "city" in person:
    print("Klucz 'city' istnieje")
```

# Co dalej?
Przejdź do kolejnego zagadnienia ([[Pętle i instrukcje warunkowe]]) lub kliknij [[Wstęp do języka Python|tutaj]], aby wrócić do strony głównej tematu.