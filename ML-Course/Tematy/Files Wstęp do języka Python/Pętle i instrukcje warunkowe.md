# Pętle w języku Python

Pętle w Pythonie służą do wielokrotnego wykonywania bloku kodu, tak długo jak dany warunek jest spełniony. Są wykorzystywane przy powtarzalnych zadaniach. Python oferuje dwa główne typy pętli: `for` i `while`.

W obu pętlach możliwe jest wykorzystanie dodatkowych funkcji:
- `break` - przerwanie wykonania pętli,
- `continue` - przejście do następnej iteracji pętli (dalsza część obecnej iteracji się nie wykona).
## Pętla `while`

Pętla `while` wykonuje się tak długo, jak długo określony warunek jest prawdziwy.

```Python
count = 0
while count < 5:
    print(count)
    count += 1
```

## Pętla `for`

Pętla `for` służy do iterowania po sekwencjach:

```Python
# Iterowanie po zakresie liczb
for i in range(5):
    print(i)

# Iterowanie po liście
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```

Możliwe jest również wykorzystanie funkcji `enumerate(zmienna)`, aby podczas iterowania po sekwencji mieć również informację o indeksie elementu:

```Python
fruits = ["apple", "banana", "cherry"]

for index, fruit in enumerate(fruits):
    print(f"Owoc na pozycji {index}: {fruit}")


# enumerate można też wykorzystać do utworzenia słownika
my_dict = dict(enumerate(fruits)) 
print(my_dict) # Wynik: {0: 'apple', 1: 'banana', 2: 'cherry'}
```

# Wykorzystanie pętli do wyrażeń listowych (list comprehension)

Za pomocą pętli w Pythonie można w bardzo zwięzły i czytelny sposób tworzyć lub modyfikować listy:

```Python
# Przykład 1
numbers = [1, 2, 3, 4, 5] 
squares = [x**2 for x in numbers] 
print(squares) # Wynik: [1, 4, 9, 16, 25]

# Przykład 2
words = ["apple", "banana", "cherry", "eagle"]
vowels = "aeiou" 
filtered_words = [word for word in words if word[0] in vowels] print(filtered_words) # Wynik: ['apple', 'eagle']

# `for word in words`: Iteruje po każdym słowie w liście `words`.
# `if word[0] in vowels`: Sprawdza, czy pierwsza litera słowa jest samogłoską.
# Jeśli warunek jest spełniony, słowo jest dodawane do nowej listy `filtered_words`
```
# Instrukcje warunkowe

Instrukcje warunkowe pozwalają na wykonanie określonych fragmentów kodu w zależności od spełnienia określonych warunków/kryteriów. Wyróżnić można następujące instrukcje:
- `if` - podstawowy (pierwszy) warunek do sprawdzenia,
- `elif` - sprawdzenie kolejnego warunku, jeżeli poprzednie nie były spełnione,
- `else` - wykonanie w przypadku, gdy żaden wcześniejszy warunek nie został spełniony.

Dostępne są następujące operatory porównania
- `==` - równe,
- `!=` - różne,
- `<` - mniejsze niż,
- `<=` - mniejsze lub równe,
- `>` - większe niż,
- `>=` - większe lub równe;
oraz następujące operatory logiczne
- `and` - oba warunki muszą być spełnione,
- `or` - przynajmniej jeden warunek musi być spełniony,
- `not` - negacja warunku.

Przykłady:

```Python
# Przykład 1
liczba = 10

if liczba > 0:
    print("Liczba jest dodatnia.")
elif liczba < 0:
    print("Liczba jest ujemna.")
else:
    print("Liczba jest równa zero.")


# Przykład 2
x = 10
y = 5

if x > 5 and y < 10:
	print("Oba warunki są spełnione.")
elif x > 5 and not y < 10:
	print("X jest wiekszy niz 5, a y nie jest wiekszy niz 10.")
```
# Co dalej?
Przejdź do kolejnego zagadnienia ([[Funkcje i klasy]]) lub kliknij [[Wstęp do języka Python|tutaj]], aby wrócić do strony głównej tematu.