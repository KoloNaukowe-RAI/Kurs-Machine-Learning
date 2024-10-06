# Funkcje w języku Python

Funkcje w Pythonie umożliwiają podzielenie kodu na moduły, które można ponownie wykorzystywać. Tworzy się je za pomocą instrukcji `def` i ciała funkcji jak w poniższym przykładzie:

```Python
def nazwa_funkcji(argumenty):
	# tutaj co w funkcji się dzieje
	return wynik
```

gdzie:
- `def` - słowo kluczowe inicjujące definicję funkcji,
- `nazwa_funkcji` - unikalna nazwa funkcji,
- `argumenty` - opcjonalna lista argumentów, które funkcja przyjmuje (można opcjonalnie zdefiniować typ i wartość domyślną elementów),
- `return` - opcjonalne słowo kluczowe, zwracające wartość z funkcji;
a wywołanie funkcji wygląda następująco:
```Python
# W przypadku funkcji zwracającej wartość
zmienna = nazwa_funkcji(argumenty)

# W przypadku funkcji, która nic nie zwraca (np. ma wyświetlić w konsoli odpowiedź, ale nie zwrócić wyniku)
nazwa_funkcji(argumenty)
```

Przykłady tworzenia funkcji:
```Python
def oblicz_sume_kwadratow(x, y):
	result = x**2+y**2
	return result

# Przykład funkcji ze zdefiniowanymi typami danych dla argumentów i zwracanej wartości
def oblicz_kwadrat_sumy(x: float, y: float) ->float:
	return (x+y)**2

# Przykład funkcji z wartością domyślną elementu
def oblicz_roznice_kwadratow(x, y=0.0):
	return x**2 - y**2

# Przykład funkcji z docstrings ("dokumentacją" funkcji)
def oblicz_kwadrat_roznicy(x, y):
  """Oblicza kwadrat różnicy dwóch liczb.

  Args:
    x: Pierwsza liczba.
    y: Druga liczba.

  Returns:
    Kwadrat różnicy liczb x i y.
  """
  return (x-y)**2
```

Możliwe jest też zwracanie więcej niż 1 wartości, np:

```Python
import datetime

def pobierz_aktualna_date():
  """Zwraca aktualną datę w postaci roku, miesiąca i dnia."""
  dzisiaj = datetime.date.today()
  return dzisiaj.year, dzisiaj.month, dzisiaj.day

# Wywołanie funkcji i przypisanie zwróconych wartości do zmiennych
rok, miesiac, dzien = pobierz_aktualna_date()

print(f"Dzisiaj jest {dzien} {miesiac} {rok}.")
```
# Klasy w Pythonie

Klasy są podstawowym elementem programowania obiektowego w Pythonie. Służą one do reprezentacji obiektów/pojęć w świecie rzeczywistym. Definicja klasy wygląda następująco:

```Python
class NazwaKlasy:
    def __init__(self, argumenty_init):
	    self.atrybuty_do_inicjalizacji = argumenty_init
	def metoda(self, argument_metody):
		self.atrybuty_do_modyfikacji = argumenty_metody
```

gdzie:
- `class` - słowo kluczowe inicjujące definicję klasy,
- `NazwaKlasy` - unikalna nazwa klasy,
- `atrybuty` - zmienne związane z obiektami tej klasy (np. kolor, rozmiar),
- `metody` - funkcje związane z obiektami tej klasy (np. poruszanie się, rysowanie).
a utworzenie obiektu danej funkcji wygląda następująco:
```Python
zmienna = NazwaKlasy(argumenty)
```

Przykład tworzenia klasy:

```Python
class Pies:
    def __init__(self, imie, rasa):  
    # wewnątrz init inicjalizujemy wszystkie atrybuty klasy
        self.imie = imie
        self.rasa = rasa
        self.szczek = "Chał chał!"

	def zmien_imie(self, dzwiek):
		self.szczek = dzwiek

    def szczekaj(self):
        print(self.szczek)

moj_pies = Pies("Reksio", "Jamnik")
moj_pies.szczekaj()
# Dostęp do imienia psa
print(moj_pies.imie)
```

Python nie ma mechanizmu ścisłej prywatności artybutów tak jak np. C++, ale wykorzystanie `__` na początku nazwy pozwala na oznaczenie artybutu jako prywatny, do którego należy odwoływać się przez metodę danej klasy:
```Python
class Osoba:
    def __init__(self, imie, pesel):
        self.imie = imie
        self.__pesel = pesel  # Prywatny atrybut

    def pobierz_pesel(self):
        return self.__pesel
```

![[PythonFruitClass.png]]
Źródło: [^meme1]
# Co dalej

Przejdź do kolejnego zagadnienia ([[Używanie bibliotek]]) lub kliknij [[Wstęp do języka Python|tutaj]], aby wrócić do strony głównej tematu.
# Źródła:
[^meme1]: https://programmerhumor.io/python-memes/python-is-easy-they-say/