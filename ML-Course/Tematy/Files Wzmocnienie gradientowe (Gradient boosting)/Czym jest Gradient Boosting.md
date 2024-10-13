# Definicja i zasada działania

Gradient Boosting iteracyjnie tworzy silny model predykcyjny, poprzez łączenie wyników wielu słabszych modeli (zazwyczaj drzew decyzyjnych), które poprawiają błędy poprzednich modeli. Każdy kolejny model jest trenowany na resztkowych błędach (residuals) poprzedniego modelu. Kluczowa jest optymalizacja funkcji straty za pomocą algorytmu gradientowego, który ma na celu minimalizację błędu między predykcją modelu a rzeczywistymi wartościami.

# Zastosowania

Wzmocnienie gradientowe można stosować w szerokim zakresie problemów związanych z uczeniem maszynowym:
- klasyfikacja: Gradient Boosting jest stosowany tam, gdzie liczy się precyzyjne klasyfikowanie (np. w analizach medycznych lub wykrywaniu oszustw),
- regresja: wzmocnienie gradientowe radzi sobie świetnie z problemami przewidywania wartości nawet w bardzo złożonych i nieliniowych modelach (np. przewidywanie cen nieruchomości czy wartości portfeli inwestycyjnych),
- systemy rekomendacyjne i rankingi (np. w systemach rekomendacji filmów lub innych produktów),
- zawody w uczeniu maszynowym: ze względu na wysoką skuteczność i precyzyjne wyniki, Gradient Boosting jest jedną z najczęściej używanych metod w zawodach Kaggle oraz w zadaniach wymagających maksymalnej dokładności.
# Porównanie z innymi metodami

W porównaniu do regresji liniowej, Gradient Boosting umożliwia modelowanie bardzo złożonych danych, których zależności mogą być nieliniowe, dzięki czemu jest bardziej elastyczny. Pojedyncze drzewa decyzyjne mają skłonności do przeuczania i mogą być niedokładne, a wzmocnienie gradientowe trenuje drzewa w sekwencji, w której każde drzewo poprawia błędy poprzednika. Jest to też różnica z lasem losowym, w którym agregowane jest wiele losowo wygenerowanych drzew, ale te drzewa nie uwzględniają błędów poprzedników, więc Gradient Boosting umożliwia lepszą optymalizację.

# Wady i zalety

- Zalety:
    - wysoka dokładność:  szczególnie gdy dane są złożone to Gradient Boosting często przewyższa inne metody w wielu zadaniach predykcji,
    - elastyczność: umożliwia użycie różnych typów danych (ciągłych i kategorycznych) oraz modelowanie złożonych zależności nieliniowych,
    - dzięki iteracyjnemu procesowi uczy się z błędów poprzednich modeli, co prowadzi do bardziej precyzyjnych predykcji.
- Wady:
    - Gradient Boosting może być wolniejszy w porównaniu z innymi metodami (np. lasami losowymi), ponieważ proces jest iteracyjny i każdy model musi zostać wytrenowany jeden po drugim,
    - jeśli model jest źle skonfigurowany (np. zbyt wiele drzew lub zbyt wysoki learning rate), może łatwo dojść do overfittingu, co skutkuje słabą generalizacją,
    - przy uczeniu modelu ze wzmocnieniem gradientowym należy dostroić wiele parametrów (np. learning rate, liczba drzew), co może być czasochłonne i wymaga doświadczenia.

# Co dalej?

Przejdź do kolejnego zagadnienia ([[Kluczowe pojęcia w Gradient Boosting]]]) lub kliknij [[Wzmocnienie gradientowe (Gradient boosting)|tutaj]], aby wrócić do strony głównej tematu.