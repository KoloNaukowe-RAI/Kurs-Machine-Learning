# Po co używać biblioteki?

Jeżeli będziemy pracowali nad jakimś projektem związanym z ... w sumie praktycznie z czymkolwiek to jest duże prawdopodobieństwo, że ktoś już coś podobnego robił i potrzebował do tego przygotować sobie narzędzia (funkcje, klasy) i stworzył z ich wykorzystaniem bibliotekę, więc możemy ją pobrać i korzystać z tego co ktoś przygotował i zaoszczędzić przy tym czas. Wg [^mgl] istnieje ponad `137.000` bibliotek, ale spokojnie, my będziemy korzystać z kilkunastu (być może kilkudziesięciu, ale to pojedyncze funkcje będą). To jak dużo jest bibliotek dobrze jest widoczne na zrzucie ekranu poniżej.

![[Libraries_in_python.png]]
# Instalowanie bibliotek

Instalowanie bibliotek odbywa się z wykorzystaniem `pip`. Najlepiej odszukać w internecie nazwę interesującej nas biblioteki (bo nie zawsze nazwa przy importowaniu jest jednakowa jak przy instalacji), a następnie w konsoli użyć komendy:
```bash
pip install nazwa_biblioteki
```

W przypadku instalowania wielu bibliotek można to zrobić następująco:
```bash
pip install nazwa_biblioteki1 nazwa_biblioteki2
```

Czasami może być konieczność zainstalowania konkretnej wersji biblioteki (np. aby była kompatybilna z inną biblioteką). Należy wówczas użyć:
```bash
pip install nazwa_biblioteki==wersja
```
lub kombinacji `>`, `<`, `>=` lub `<=`, np.
```bash
pip install numpy<=1.25.2
```
lub
```
pip install "numpy>1.18.5,<=1.25.2"
```

Dobrym zwyczajem jest również tworzenie pliku `requirements.txt`, w którym wypisane są wszystkie wykorzystywane biblioteki (jest to zwykły plik tekstowy, który można zrobić nawet w notatniku). Pozwoli to każdemu komu wyślemy kod na zainstalowanie tych samych bibliotek i tym samym uruchomienie skryptu (bez zainstalowania niestety nie pójdzie). Po utworzeniu pliku `requirements.txt` można łatwo całość zainstalować poleceniem
```bash
pip install -r requirements.txt
```

# Importowanie i korzystanie z bibliotek

Po zainstalowaniu biblioteki, jej zaimportowanie jest proste. Wystarczy w skrypcie wpisać
```Python
import nazwa_biblioteki
```
Możliwe jest również nadanie aliasu (np. jeżeli biblioteka ma długą nazwę) lub zaimportowanie jedynie pewnych składników
```Python
import nazwa_biblioteki as alias_bibl # Importowanie z aliasem

from nazwa_biblioteki import funkcja, klasa # Importowanie wybranych składników
```

> [!TIP]
> Należy zwrócić uwagę na to w jaki sposób importujemy bibliotekę, bo ma to wpływ na dalszy kod (np. po nadaniu aliasu nie możemy odwołać się do biblioteki pod jej standardową nazwą)

Korzystanie z funkcji jest również stosunkowo proste. Załóżmy, że w `bilioteka` są funkcje `funkcja1` i `funkcja2`. Poniżej znajduje się przykład z wszystkimi przedstawionymi powyżej możliwościami importu

```Python
import os # Importowanie biblioteki
import numpy as np # Importowanie biblioteki z aliasem
from pandas import DataFrame, read_csv # Importowanie tylko klasy i funkcji

# Utworzenie DataFrame z biblioteki Pandas przez wczytanie danych z pliku txt
data_frame = read_csv(os.path.join("/path/to/","filename.csv"))
# Konwersja na numpy array (to_numpy() jest metodą DataFrame)
array = data_frame.to_numpy()

# Obliczenie sumy wszystkich elementów wektora
array_sum = np.sum(array)
```
# Co dalej

Kliknij [[Wstęp do języka Python|tutaj]], aby wrócić do strony głównej tematu. Możesz stamtąd przejść do wykonania zadań przygotowanych w Jupyter Notebook.

# Źródła:
[^mgl]: https://www.mygreatlearning.com/blog/open-source-python-libraries/