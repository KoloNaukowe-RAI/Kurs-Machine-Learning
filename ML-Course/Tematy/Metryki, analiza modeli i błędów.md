### <span style="color:#4caf50;">Sprawdzian krzyżowy (Cross-Validation)</span> 🔄
> Proces ten polega na podzieleniu zbioru danych na <span style="color:#ff5722;">*k*</span> równych części (*folds*).

1. Model jest trenowany na <span style="color:#ff5722;">*k-1*</span> częściach, a testowany na jednej z pozostałych.
2. Procedura jest powtarzana <span style="color:#ff5722;">*k*</span> razy, za każdym razem wybierając inny podzbiór jako zbiór testowy.
3. Wynik końcowy to średnia ze wszystkich <span style="color:#ff5722;">*k*</span> iteracji.

- Zmniejsza ryzyko <span style="color:#d32f2f;">**overfittingu**</span> poprzez sprawdzanie modelu na różnych partiach danych.

W Scikit-learn implementuje to funkcja `cross_val_score` z opcją `KFold` do określenia liczby podziałów (k).

---

### **<span style="color:#1e88e5;">Przeszukiwanie siatki (Grid Search)</span>** 🔍

**GridSearchCV** to metoda doboru hiperparametrów w `Scikit-learn`, która testuje wszystkie kombinacje zadanych wartości hiperparametrów, aby znaleźć najlepszą.

### <span style="color:#1e88e5;">Jak działa GridSearchCV?</span> ⚙️
1. **Zdefiniowanie siatki**: Użytkownik definiuje wartości hiperparametrów. Przykład dla `RandomForestClassifier`:
   - `n_estimators`: [100, 200, 300]
   - `max_depth`: [5, 10, 15]
   
2. **Przegląd kombinacji**: Model trenowany jest dla każdej kombinacji hiperparametrów, a wydajność oceniana na zbiorze walidacyjnym. Używa się walidacji krzyżowej (`cv`).

3. **Ocena**: Wyniki dla każdej kombinacji są mierzone za pomocą zdefiniowanej metryki, np. `accuracy` czy `F1-score`.

4. **Wybór najlepszego zestawu**: Po przetestowaniu wszystkich kombinacji, zestaw hiperparametrów o najlepszym wyniku zostaje wybrany.

W Scikit-learn implementowane przez `GridSearchCV`.

```python
from sklearn.model_selection import GridSearchCV, train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_iris

# Załadowanie danych
data = load_iris()
X, y = data.data, data.target

# Podział na dane treningowe i testowe
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Definicja hiperparametrów
param_grid = {
    'n_estimators': [100, 200, 300],
    'max_depth': [5, 10, 15]
}

# Model Random Forest
model = RandomForestClassifier()

# Grid Search z walidacją krzyżową (5-fold) na danych treningowych
grid_search = GridSearchCV(model, param_grid, cv=5, scoring='accuracy')
grid_search.fit(X_train, y_train)

# Najlepsze parametry
print(f"Najlepsze parametry: {grid_search.best_params_}")

# Ocena na zbiorze testowym
test_accuracy = grid_search.score(X_test, y_test)
print(f"Dokładność na zbiorze testowym: {test_accuracy:.2f}")

#Wynik
#Najlepsze parametry: {'max_depth': 10, 'n_estimators': 300}
#Dokładność na zbiorze testowym: 0.98

```
### <span style="color:#1e88e5;">Przeszukiwanie losowe (Random Search)</span> 🎲

**RandomizedSearchCV** to alternatywa dla Grid Search, która nie przeszukuje wszystkich możliwych kombinacji, a jedynie losowo wybrane próbki z przestrzeni hiperparametrów.

### <span style="color:#1e88e5;">Jak działa RandomizedSearchCV?</span> ⚙️
1. **Zdefiniowanie zakresu**: Użytkownik definiuje zakresy wartości dla hiperparametrów.
2. **Losowy wybór**: Algorytm losowo wybiera kombinacje wartości do przetestowania (zamiast sprawdzać wszystkie).
3. **Ocena**: Kombinacje oceniane są na zbiorze walidacyjnym, a wyniki mierzone według wybranej metryki.
4. **Wybór najlepszego zestawu**: Najlepsza kombinacja zostaje wybrana do trenowania finalnego modelu.

### <span style="color:#4caf50;">Zalety Random Search:</span>
- **Szybkość**: Przeszukiwanie losowe jest szybsze niż Grid Search, szczególnie przy dużej liczbie parametrów.

W Scikit-learn implementowane przez `RandomizedSearchCV`.

```python
from sklearn.model_selection import RandomizedSearchCV, train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_iris
from scipy.stats import randint
from sklearn.metrics import accuracy_score

# Załadowanie danych
data = load_iris()
X, y = data.data, data.target

# Podział na dane treningowe i testowe
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Definicja zakresów dla hiperparametrów
param_dist = {
    'n_estimators': randint(100, 500),
    'max_depth': randint(5, 20)
}

# Model Random Forest
model = RandomForestClassifier()

# Random Search z walidacją krzyżową (5-fold), 10 losowych próbek
random_search = RandomizedSearchCV(model, param_dist, n_iter=10, cv=5, scoring='accuracy', random_state=42)
random_search.fit(X_train, y_train)

# Najlepsze parametry
print(f"Najlepsze parametry: {random_search.best_params_}")

# Ocena na zbiorze testowym
y_pred = random_search.predict(X_test)
test_accuracy = accuracy_score(y_test, y_pred)
print(f"Dokładność na zbiorze testowym: {test_accuracy:.2f}")

```
---

### <span style="color:#ff5722;">Przykład 🎯</span> dla modelu Random Forest:
#### Grid Search:
- `n_estimators`: [100, 200, 300]
- `max_depth`: [5, 10, 15]  
Przeszukuje wszystkie możliwe kombinacje.

#### Random Search:
- `n_estimators`: od 100 do 500
- `max_depth`: od 5 do 20  
Losowo wybiera próbki z przestrzeni tych wartości do testowania.

### <span style="color:#4caf50;">Etapy analizy błędów</span> 🧠

---

### <span style="color:#1e88e5;"> Macierz pomyłek (Confusion Matrix)</span> 

 Pozwala zobaczyć, jak model klasyfikuje próbki: ile razy poprawnie przewiduje daną klasę, a ile razy pomyli się, klasyfikując próbki do innych klas.
 
>[!important]
> Elementy Confusion Matrix
>- **True Positives (TP)**: poprawne pozytywne predykcje.
>- **True Negatives (TN)**: poprawne negatywne predykcje.
>- **False Positives (FP)**: błędne predykcje klasy pozytywnej (fałszywe alarmy).
>- **False Negatives (FN)**: błędne predykcje klasy negatywnej (pominięcia).

#### Przykład macierzy pomyłek (dla klasyfikacji binarnej):
```
            Predicted Positive   Predicted Negative
Actual Pos          50                    10
Actual Neg          5                     35

- Model poprawnie przewidział 50 pozytywnych przypadków (TP) i 35 negatywnych (TN).
- 5 negatywnych przypadków zostało błędnie przewidzianych jako pozytywne (FP).
- 10 pozytywnych przypadków zostało błędnie sklasyfikowanych jako negatywne (FN).
```

```python
from sklearn.metrics import confusion_matrix, classification_report y_true = [0, 0, 1, 1, 0, 1, 0, 1, 1, 1] # rzeczywiste etykiety 
y_pred = [0, 1, 1, 1, 0, 0, 0, 1, 1, 1] # przewidziane etykiety 

# Macierz pomyłek 
cm = confusion_matrix(y_true, y_pred) print("Macierz pomyłek:") print(cm) 

print("\nRaport klasyfikacji:") 
print(classification_report(y_true, y_pred))


#Macierz pomyłek:
#[[3 1]
 #[1 5]]

#Raport klasyfikacji:
#             precision    recall  f1-score   support

#           0       0.75      0.75      0.75         4
#          1       0.83      0.83      0.83         6

#    accuracy                           0.80        10
#   macro avg       0.79      0.79      0.79        10
#weighted avg       0.80      0.80      0.80        10

```

# Link do Jupyter Notebook

Ćwiczenia dla tego tematu zostały zebrane [tutaj](https://github.com/KoloNaukowe-RAI/Kurs-Machine-Learning/blob/main/Tasks/Tasks08_Metryki_Oceny_Modelu.ipynb).
# Co dalej?

Kliknij [[Index|tutaj]], aby wrócić do strony głównej kursu.

