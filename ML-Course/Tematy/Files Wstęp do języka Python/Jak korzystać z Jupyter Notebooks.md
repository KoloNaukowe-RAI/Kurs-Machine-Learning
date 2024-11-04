W tym miejscu przedstawione zostaną 3 możliwości uruchomienia Jupyter Notebooks oraz krótki opis tego jak one działają.

# Wgrywanie Notebooków

Przed przejściem do wgrywania zacznijmy od pobierania Notebooków przygotowanych do tego kursu. Przejdź do repozytorium kursu, wejdź w katalog `Tasks` i wybierz, który plik chcesz wybrać (kliknij go dwukrotnie). Po przejściu do podglądu pliku, w górnej prawej części ekranu powinna być widoczna ikonka pobierania (`Download raw file`) i przy jej pomocy można pobrać plik. Należy pamiętać o tym, że do części zadań trzeba pobrać dodatkowo pliki z danymi (z folderu `Dane`).
![[Downloading_from_github.png]]
Inną możliwością jest użycie `git clone <adres_url_repozytorium>`, który pobierze całe repozytorium z GitHuba i w ten sposób można przejść do folderu, który nas interesuje.
## Sposób #1 Google Colab

### 1. Wejść na stronę https://colab.research.google.com/ i zalogować się

### 2. Powinno wyświetlić się okienko "Otwórz notatnik", gdzie można wybrać pomiędzy wgrywaniem nowego Notebooka lub edycją tego, który mamy na dysku Google.
![[GoogleColab2.png]]

#### 2.1. Jeżeli nie otworzyło się okienko tylko przykładowy Notebook to możemy to okienko wywołać poprzez wybranie `Plik > Prześlij notatnik`.
![[GoogleColab1.png]]

### 3. Połączyć się do środowiska można na kilka sposobów: kliknąć "Połącz" w prawej części paska, kliknąć wewnątrz `[]` przy komórce z kodem (zmieni się na przycisk start) lub wybrać `Środowisko wykonawcze > Uruchom Zaznaczony Kod`.
![[GoogleColab3.png]]
### 4.  Aby wgrać plik z danymi należy wybrać ikonkę z folderem i przeciągnąć plik w wolne miejsce na pasku, który się pojawił.
![[GoogleColab4.png]]

## Sposób #2 Kaggle

### 1. Utworzyć konto na Kaggle: https://www.kaggle.com/ (można zalogować się przy pomocy konta Google). Jedna ważna sprawa - po utworzeniu konta nie można zmienić nicku.

### 2. Należy utworzyć nowy Notebook korzystając z przycisku `Create`, a następnie `New Notebook`.
![[Kaggle1.png]]

### 3. Z paska na górze strony wybrać `File > Import Notebook`.
![[Kaggle2.png]]

### 4. Po prawej stronie pojawi się miejsce na wgranie pliku, a po wrzuceniu notatnika z dysku należy na dole strony kliknąć `Import`.
![[Kaggle3.png]]

### 5. Aby wgrać plik należy z paska po prawej stronie w części Input wybrać `Upload`, a następnie `New Dataset`. Ponownie wyskoczy analogiczne okno jak w punkcie 4., gdzie można dodać plik z danymi.
![[Kaggle4.png]]

## Sposób #3 Visual Studio Code

### 1. Pobrać i zainstalować:
- Visual Studio Code z oficjalnej strony: https://code.visualstudio.com/ 
- Pythona ze strony: https://www.python.org/downloads/ (w chwili tworzenia kursu polecam korzystać z Pythona 3.11)
### 2. Należy zainstalować rozszerzenie Jupyter (extension id: ms-toolsai.jupyter) oraz Python (extension id: ms-python.python) dla Visual Studio Code. 

### 3. Następnie należy otworzyć folder, w którym znajdują się nasze Notebooki
![[vscode1.png]]

### 4. Teraz należy dodać kernel, aby umożliwić intepretację kodu:
W przypadku, gdy nie mieliśmy wcześniej utworzonego środowiska:
`Python Environments > Create Python Environment + Venv + Python 3.xx`
![[vscode2.png]]
![[vscode3.png]]
Jeżeli środowisko wcześniej utworzyliśmy to można zamiast `Create Python Environment` można je wybrać z listy 
![[vscode4.png]]

### 5. Jak chodzi o dane to musimy się upewnić, że jest do nich odpowiednia ścieżka. Notebooki do tego kursu zostały utworzone z myślą o wykorzystaniu Google Colab, gdzie Notebook jest w tym samym folderze co dane. Upewnij się, że również w taki sposób masz zapisane dane lub zmień ścieżkę w odpowiednich komórkach kodu.

### 6. W przypadku korzystania z Notebooków na własnym komputerze konieczne będzie doinstalowanie dodatkowych bibliotek (kernele dostępne w rozwiązaniach chmurowych mają od razu najpopularniejsze biblioteki zainstalowane). Można to zrobić przy pomocy 
```Python
!pip install <nazwa_biblioteki>
```
możesz też skorzystać z przygotowanego pliku `requirements.txt`
```
!pip install -r requirements.txt
```

# Jak pracować z Notebookami?

Na rysunku poniżej zaznaczono elementy widoczne w notatniku:
<div style="color: orange;"> <b>Komórka z tekstem</b> </div>
<div style="color: blue;"> <b>Komórka z kodem</b> </div>
<div style="color: green;"> <b>Pole do wpisywania kodu</b> </div>
<div style="color: yellow;"> <b>Przycisk do uruchomienia komórki z kodem</b> </div>
<div style="color: pink;"> <b>Wyjście komórki z kodem</b> </div>

![[notebook1.png]]

Notebooki umożliwiają uruchamianie jedynie fragmentów kodu, przez co dobrze nadają się do realizacji ćwiczeń, które rozwiązuje się krok po kroku i gdzie przygotowuje się coś, co wykorzysta się później, dzięki zapamiętywaniu wartości zmiennych (są one resetowane przy rezetowaniu środowiska). Powoduje to, że nie ma konieczności wykonywania długich obliczeń za każdym uruchomieniem skryptu.

# Co dalej?

Kliknij [[Wstęp do języka Python|tutaj]], aby wrócić do strony głównej tematu. Możesz stamtąd przejść do wykonania zadań przygotowanych w Jupyter Notebook.