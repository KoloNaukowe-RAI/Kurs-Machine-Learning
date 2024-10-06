# Język interpretowany

Python jest językiem interpretowanym, więc do korzystania z niego nie jest wymagany kompilator (wykorzystywany jest interpreter). Innymi przykładami tego typu języków są Bash, PHP lub JavaScript. Oznacza to, że skrypt jest przechowywany w formie kodu i interpretowany przy każdym uruchomieniu, a nie konwertowany na kod maszynowy jednorazowo [^interp].

# Składnia

![[PythonWhere.png]]
Źródło: [^meme2]

Tak jak na obrazku powyżej, programując w Pythonie na końcu linii nie stawia się średnika. Dla tych, którym w C++ się o tym zapomina, może być to ułatwienie, ale dla osób, które pisały "kilka linijek w jednej linijce" i oddzielały je średnikami to będzie wymagało przestawienia.

Na obrazku powyżej wspomniane były też klamry, bo ich też nie ma (więcej o tym jak wyglądają pętle i instrukcje warunkowe będzie dalej). Ale jeśli nie ma klamr, to skąd interpreter ma wiedzieć, które linie kodu są wewnątrz if'a, a które już poza? I tutaj przechodzimy do kolejnego obrazka...

![[NoIndent.png]]
Źródło: [^meme1]

# Wcięcia

Programując w C++ wcięcia zwiększają jedynie czytelność kodu dla programisty i można je pomijać. W przypadku Pythona wcięcia muszą być **identyczne**, żeby interpreter dobrze przetworzył kod. Wydaje mi się, że najlepiej jest to pokazać na przykładzie, więc taki znajduje się poniżej.

```Python
for i in range(3): 
	for j in range(3):
		result = i*10+j
		print(result)
	print("Wykonam się po skończeniu się pętli z j")
print("Wykonam się po skończeniu się pętli z i")
```

Nie wchodzimy na razie w szczegóły pętli i jak działa `in range`, ale wynikiem byłoby:

```
0
1
2
Wykonam się po skończeniu się pętli z j
10
11
12
Wykonam się po skończeniu się pętli z j
20
21
22
Wykonam się po skończeniu się pętli z j
Wykonam się po skończeniu się pętli z i
```

Czyli jak widać wpierw w pętli wewnętrznej (z podwójnym wcięciem) jest dodawanie, a następnie wypisywanie w konsoli wyniku. Po wykonaniu się pętli wewnętrznej, w konsoli pojawia się odpowiednia wiadomość (zwrócę uwagę, że `for j in range(3):` i `print("Wykonam się po skończeniu się pętli z j")`również mają identyczne wcięcia, bo są wewnątrz pętli ze zmienną `i`). Gdy pętla zewnętrzna wykona się odpowiednią ilość razy to w konsoli również pojawia się odpowiednia wiadomość.

W przykładzie użyłem tabulatora do robienia wcięć, ale równie dobrze można używać spacji - jedynie wcięcie musi mieć zawsze równą wielkość!

# Komentarze

W Pythonie komentarze dodaje się po `#`, np:
```Python
# Ta linia to komentarz
print("Hello world!") # A tu komentarz w linii z kodem
```

Możliwe są również komentarze wieloliniowe poprzez umieszczenie ich wewnątrz ` ``` ``` `. Ten drugi jest przydatny np. do przygotowania opisu funkcji, gdzie można w ten sposób opisać czym jest każda zmienna.

# Co dalej?

Przejdź do kolejnego zagadnienia ([[Zmienne i podstawowe typy danych]]) lub kliknij [[Wstęp do języka Python|tutaj]], aby wrócić do strony głównej tematu.
# Źródła:
[^interp]: https://en.wikipedia.org/wiki/Interpreter_(computing)
[^meme1]: https://programmerhumor.io/programming-memes/no-offence-python-from-one-python-lover-to-others/
[^meme2]: https://programmerhumor.io/python-memes/after-using-only-c-and-c-for-years-python-felt-kinda-strange/