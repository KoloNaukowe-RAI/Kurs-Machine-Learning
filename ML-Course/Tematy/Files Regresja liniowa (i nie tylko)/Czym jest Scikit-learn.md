# Jedna biblioteka praktycznie do wszystkiego

Scikit-learn jest jedną z najczęściej wybieranych bibliotek do projektów uczenia maszynowego, zarówno przez początkujących, jak i zaawansowanych użytkowników, co zawdzięcza swojej elastyczności, wszechstronności i prostocie użycia. Zapewnia narzędzia do budowy i trenowania modeli, a także do analizy danych i zapewnia kompatybilność z innymi narzędziami do analizy danych dostępnych w Pythonie. 

Link do oficjalnej strony [scikit-learn](https://scikit-learn.org/).

![[scikit-learn-logo.png]]
Źródło: [^sci]

# Jakie są możliwości Scikit-learn?

Bibliotekę sklearn możemy wykorzystać do:
 - pobierania datasetów, przetwarzania danych i ich wstępnej obróbki,
 - implementacji algorytmów uczenia maszynowego:
	 - klasyfikacji (np. Decision Tree, Random Forest, Gradient Boosting),
	 - regresji (np. Linear Regression, Ridge Regression),
	 - klasteryzacji (np. K-means, DBSCAN),
- optymalizacja hiperparametrów (przy pomocy Grid Search lub Random Search) i walidacja modeli (zaimplementowane są różne metryki jak cross-validation, F1, accuracy)
- tworzenie pipeline'ów (połączenie kilku kroków przetwarzania), aby pomóc w lepszym zorganizowaniu budowania modeli i ich walidacji.

# Uniwersalne funkcje

W scikit-learn dostępne jest kilka funkcji, które mogą być wykorzystane przy różnych modelach i procesach uczenia maszynowego, co ułatwia korzystanie z tej biblioteki. Poniżej znajduje się kilka przykładów:
- podział danych na zbiór treningowy i testowy (jako `X` oznaczone są cechy, a jako `y` etykiety)
```Python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```
 - trening modelu na danych `X_train` i etykietach `y_train`:
 ```Python
model.fit(X_train, y_train)
```
- przewidywanie etykiet dla nowych danych `X_test`:
```Python
model.predict(X_test)
```
- obliczenie oceny modelu (np. dla klasyfikacji oblicza dokładność, a dla regresji błąd):
```Python
model.score(X_test, y_test)
```
- jednoczesne dopasowanie do danych i transformacja (np. przy skalowaniu lub uzupełnianiu brakujących wartości):
```Python
scaler.fit_transform(training_data)
```
- sama transformacja (np. dla danych testowych, gdzie chcemy wykorzystać to samo skalowanie co dla danych treningowych):
```Python
scaler.transform(test_data)
```
- przeprowadzenie walidacji krzyżowej:
```Python
cross_val_score(model, X_train, y_train, cv=5)
```
- optymalizacja hiperparametrów:
```Python
# param_grid jest słownikiem i dla drzewa decyzyjnego może wyglądać następująco:
param_grid = {'max_depth': [None, 10, 20, 30], 
			  'min_samples_split': [2, 10, 20], 
			  'min_samples_leaf': [1, 5, 10], 
			  'max_features': [None, 'sqrt', 'log2']}
# a przeszukiwanie przy pomocy przeszukiwania po siatce hiperparemetrów
GridSearchCV(model(), param_grid, cv=5)
```
- wczytywanie danych:
```Python
from sklearn import datasets
# Wczytanie datasetu Iris
iris = datasets.load_iris()

# Dostępne są inne datasety, do których dostęp jest za pomocą datasets.load_nazwa(), np.
digits = datasets.load_digits()
wine = datasets.load_wine()

# Możliwe jest też pobieranie datasetów z OpenML, np.
mnist = datasets.fetch_openml('mnist_784', version=1)
```

# Przy okazji - skąd brać datasety?

Utworzenie samemu zbioru danych jest czasochłonne i wymaga następnie przetworzenia danych, co ponownie może być czasochłonne i dodatkowo skomplikowane. Istnieją strony, na których użytkownicy mogą wstawić datasety, aby inni mogli z nich publicznie korzystać. Najpopularniejsze z nich to:
- [Kaggle](https://www.kaggle.com/datasets)
- [OpenML](https://openml.org/search?type=data)
Ponadto na Kaggle odbywają się cyklicznie konkursy (z dużymi pulami nagród), w których można spróbować swoich sił.
# Co dalej?

Przejdź do kolejnego zagadnienia ([[Implementacja regresji przy pomocy Scikit-learn]]) lub kliknij [[Regresja liniowa (i nie tylko)|tutaj]], aby wrócić do strony głównej tematu.

# Źródła:
[^sci]: https://github.com/scikit-learn/scikit-learn/tree/main/doc/logos