# Cel projektu

Celem projektu jest predykcja jacy zawodnicy zagrają w meczu NBA All-Star Game 2025, wraz z ilością punktów, które zdobędą. 

NBA All-Star Game, czyli Mecz Gwiazd NBA, jest rozgrywany co roku od sezonu 1950/1951 w lutym/marcu (czyli trochę za połową sezonu). 24 zawodnicy są wybierani przez kibiców, media i koszykarzy, więc ważna jest zarówno rozpoznawalność, ale też wyniki na boisku. Głosujący wybierają po 3 atakujących (Forwards) i 2 rozgrywających (Guards) z każdej konferencji - strona do głosowania dostępna jest tutaj: https://vote.nba.com/en .

>[!IMPORTANT]
>W tym roku nastąpiła zmiana formatu: https://www.nba.com/news/2025-nba-all-star-game-new-format, i zamiast 1 meczu, rozgrywany jest miniturniej, w którym zagrają 3 drużyny po 8 zawodników (wybrani na podstawie głosowania) i drużyna złożona z młodych zawodników - nas interesuje tylko tych 24 zawodników, którzy są wybierani. Dodatkowo mecze rozgrywane są aż jedna z drużyn zdobędzie lub przekroczy 40 punktów.

>[!WARNING]
>Ze względu na zmieniony format, w którym część koszykarzy zagra 1, a część 2 mecze, przyjmijmy, że predykujemy średnią liczbę punktów zdobytych przez koszykarza (w ten sposób nie ma wpływu to czy zagra w finale czy nie). Wcześniej rozgrywane były mecze podzielone na 4 kwarty, przez co zawodnicy zdobywali dużo więcej punktów, a więc należy końcowe predykcje przeskalować, aby suma punktów była sensowna (max. punktów to `39 + (42 + 42)/2 + (42 + 39)/2 = 121.5`, ale może być to mniej).

**W przypadku jakichkolwiek pytań lub wątpliwości zachęcam do zadawania pytań. Jeżeli są to pytania ogólne co do tego jak działa mecz gwiazd, czym są dane statystyki lub coś związanego z koszykówką, to najlepiej zadać je na wspólnym czacie, żeby każdy mógł się dowiedzieć, a jak pytanie konkretnie o kod to wtedy można na priv.**
# Dane

Dane zebrałem przy pomocy [nba_api](https://github.com/swar/nba_api), a dostępne są na Kaggle: https://www.kaggle.com/datasets/marcinmc/nba-players-statistics-seasonal-and-matchbymatch. Na Kaggle również znajdują się opisy poszczególnych kolumn, oraz przykład wczytywania danych sezonowych.
>[!IMPORTANT]
>Należy zwrócić uwagę, że w pliku `matches_player_stats.csv` są dostępne statystyki z wszystkich meczów NBA w historii (aż do 01.01.2025) dla wszystkich zawodników, którzy w nich grali. Tych danych jest mnóstwo, więc warto zrobić jakąś filtrację i np. policzyć sumy lub średnie wartości statystyk, które zdobywali zawodnicy w każdym sezonie przed określoną datą lub w określonej liczbie meczów od początku sezonu.

>[!IMPORTANT]
>W pliku `seasonal_stats_with_awards.csv` są statystyki za cały sezon, co oznacza, że zawierają część danych o "przyszłości", bo sezon zasadniczy nie kończy się na All-Star Weekend, a trwa do połowy/końca kwietnia, a większość nagród przyznawanych jest na koniec sezonu. 

Można (a nawet zachęcamy) tworzyć własne kolumny, które mogą pomóc w predykcji - np. ilość występów w Meczu Gwiazd przed danym sezonem, ilość sezonów rozegranych w NBA przed danym sezonem, lub jakieś ciekawe statystyki, jak np. liczba punktów zdobywana w piątki.

Dopuszczalne jest korzystanie z innych źródeł danych (np. dodatkowe dane o zawodniku, ilości głosów w poszczególnych głosowaniach, przyrost obserwujących na Instagramie w poszczególnych latach, czy cokolwiek innego co może okazać się przydatne), pod warunkiem, że dana strona nie zabrania ich wykorzystania.
# Co ma się znaleźć w projekcie?

Projekt musi zawierać:
- predykcję 18 zawodników wraz z liczbą punktów, które zdobędą,
- kod,
- opis.
Dodatkowo konieczne jest:
- podział na zbiór treningowy i testowy (polecamy podzielić sezonami, a nie zawodnikami, bo wtedy możecie wykorzystać tę samą metrykę, która będzie tu wykorzystana),
- zrobienie initial guess (może być to losowe wybranie zawodników i punktów lub zastosowanie jakiegoś prostego modelu),
- przetestowanie i porównanie min. 3 różnych algorytmów,
- przetestowanie i porównanie różnych hiperparametrów dla przynajmniej 1 algorytmu (np. wykorzystując GridSearchCV lub RandomizedSearchCV),
- przetestowanie kilku zestawów cech (kolumn) dla przynajmniej 1 algorytmu i 1 zestawu hiperparametrów.

# Czego nie może być w projekcie?

W projekcie niedozwolone jest ręczne ustawianie jacy zawodnicy będą grać lub ilości punktów (np. wpisanie, że zawodnik A będzie grał, bo w informacjach z internetu jest napisane, że ma najwięcej głosów). Dopuszczalne jest ustawianie warunków, np. "Sprawdziłem, że w All-Star Game zawsze gra zawodnik, który w poprzednim sezonie miał największą liczbę punktów w ostatnim meczu Finałów" - ale taka informacja musi być dodana w opisie (swoją drogą nie wiem czy dany przeze mnie przykład jest prawdziwy).
# Format

Poza predykcją w formacie csv, należy również przesłać kod i opis. Predykcja powinna mieć nagłówek `name, points`, a w kolejnych linijkach powinny znajdować się predykowane imię i nazwisko wraz z ilością punktów (punkty powinny być oddzielone od imienie i nazwiska przecinkiem - korzystając z `to_csv()` z biblioteki `pandas` zostanie to zrobione to w ten sposób automatycznie). Chodzi o coś takiego:

| name     | points |
| -------- | ------ |
| Player A | 10.2   |
| Player B | 5.7    |
Jak chodzi o kod to może on być przygotowany zarówno w Jupyter Notebook, jak i w formie skryptu/skryptów. Proszę o krótkie komentarze w kodzie (np. `#wczytywanie danych`, `#wstepna analiza`, `#funkcja do predykcji`, etc.). 

Co do opisu to nie ma narzuconej formy, w przypadku Jupyter Notebook pewnie najlepiej będzie jakby te opisy pojawiały się pomiędzy poszczególnymi komórkami z kodem, ale może też być zrobione oddzielnie (np. w postaci README w Markdown, pdf z dokumentu Word, czy jak ktoś chce poćwiczyć to w Latexu). Opis ma pokazać ścieżkę rozumowania - "Porównując wykresy zależności zmiennej A i prawdopodobieństwa zagrania w drużynie NBA All-Star i zmiennej B, a prawdopodobieństwo zagrania, zobaczyłem, że na podstawie zmiennej A można więcej wnioskować, więc wybrałem tę kolumnę" (i najlepiej dodać ten wykres) albo "Przetestowałem 5 różnych typów modeli, z czego 2 z nich dawały o wiele lepsze wyniki, więc analizę, które kolumny poprawią wynik przeprowadzałem tylko na tych 2" (tu też warto tabelkę czy wykres dać).

Najlepszą metodą oddania projektu byłoby wrzucenie go na GitHuba, ale jeżeli ktoś nie korzystał nigdy, to może być wszystko podesłane na Facebooku lub Discordzie.

# Deadline

Ze względu na to, że weekend NBA All-Star zaczyna się 14.02, to jest to też ostateczny termin oddania projektu. 

# Metryka

Do oceny predykcji zastosowana zostanie następująca metryka:
- dla zgłoszeń przed 30.01.2025 (data ogłoszenia pełnych zespołów):
$$X = 50\cdot Zaw + 5\cdot Piatka + 20 \cdot Punkty + 10 \cdot MalyBlad$$
- dla zgłoszeń 30.01.2025 lub później:
$$X = 20\cdot Zaw + 5\cdot Piatka + 30 \cdot Punkty + 10 \cdot MalyBlad$$

Gdzie:
$$Zaw = \frac{\text{Liczba dobrze predykowanych zawodnikow}}{\text{Calkowita liczba zawodnikow co zagrali}}\text{,}$$
$$Punkty = \frac{1}{\text{Liczba zaw.}} \sum_{i=1}^{\text{Liczba zaw.}} -|\text{predykcja} - \text{rzeczywiste punkty}|\text{,}$$
- `Piatka` - za każdych 5 dobrze predykowanych zawodników dodawane jest 1 (np. za 4 trafionych `Piatka = 0`, za 5 `Piatka = 1`, za 8 `Piatka = 1`, za 14 `Piatka = 2`, etc.), jest to forma takiego bonusu,
- `MalyBlad` - liczba zawodników, dla których błąd bezwzględny predykcji punktów jest nie większy niż 1.

Nie ma ograniczenia, że model musi zdobyć pewne minimum punktów, ale możemy zrobić potem listę wyników i zobaczyć jakie podejścia były najlepsze.
# Co dalej?

Kliknij [[Index|tutaj]], aby wrócić do strony głównej kursu.

# Źródła:
https://www.nba.com/news/2025-nba-all-star-game-new-format
https://en.wikipedia.org/wiki/NBA_All-Star_Game