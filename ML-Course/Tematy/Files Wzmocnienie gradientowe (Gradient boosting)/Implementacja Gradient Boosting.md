# Jakie biblioteki do wzmocnienia gradientowego?

Gradient Boosting został zaimplementowany w 3 popularnych bibliotekach:
- Scikit-Learn,
- xgboost,
- LightGBM.

Wszystkie 3 implementacje mają podobny interfejs i umożliwiają zastosowanie do regresji i klasyfikacji, co ułatwia pracę. Występują między nimi następujące różnice:
 - Scikit-Learn udostępnia prosty w użyciu algorytm,
 - xgboost udostępnia więcej zaawansowanych hiperparametrów i możliwości tuningu, co może prowadzić do lepszej dokładności, a także dzięki lepszej optymalizacji i rownoległości jest bardziej wydajny do dużych zbiorów danych,
 - LightGBM jest wydajny dla dużych zestawów danych o wielu wymiarach dzięki budowania drzewa na poziomie liści (zamiast poziomu drzewa) i dzielenia danych na histogramy zamiast dzielenia danych na każdą możliwą wartość.

Ze względu na lepszą optymalizację korzystniej jest korzystać z xgboost lub LightGBM, a wybór jednej z tych bibliotek zależy od preferencji oraz konkretnego przypadku datasetu.
# Gradient Boosting dla regresji

Poniżej znajduje się kod, w którym na wygenerowanym zbiorze danych zastosowano modele Gradient Boostingu z bibliotek Scikit-Learn, xgboost i LightGBM:

```Python
from sklearn.ensemble import GradientBoostingRegressor
from sklearn.model_selection import train_test_split
from sklearn.datasets import make_regression
import xgboost as xgb 
import lightgbm as lgb

# Generowanie przykładowego zbioru danych
X, y = make_regression(n_samples=1000, n_features=10, noise=0.1)

# Podział na zbiory treningowe i testowe
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Utworzenie i trenowanie modelu oraz predykacja przy pomocy Sklearn
model_sklearn = GradientBoostingRegressor(n_estimators=100, learning_rate=0.1, max_depth=3, random_state=42)

model_sklearn.fit(X_train, y_train)

y_pred_sklearn = model_sklearn.predict(X_test)

# Utworzenie i trenowanie modelu oraz predykacja przy pomocy xgboost
model_xgb = xgb.XGBRegressor(n_estimators=100, learning_rate=0.1, max_depth=3, random_state=42)

model_xgb.fit(X_train, y_train)

y_pred_xgb = model_xgb.predict(X_test)

# Utworzenie i trenowanie modelu oraz predykacja przy pomocy LightGBM
model_lgb = lgb.LGBMRegressor(n_estimators=100, learning_rate=0.1, max_depth=3, random_state=42)

model_lgb.fit(X_train, y_train)

y_pred_lgb = model_lgb.predict(X_test)
```

# Gradient Boosting dla klasyfikacji

Poniżej znajduje się kod, w którym na wygenerowanym zbiorze danych zastosowano modele Gradient Boostingu z bibliotek Scikit-Learn, xgboost i LightGBM:

```Python
from sklearn.ensemble import GradientBoostingClassifier
from sklearn.model_selection import train_test_split
from sklearn.datasets import make_classification
import xgboost as xgb
import lightgbm as lgb

# Generowanie przykładowego zbioru danych
X, y = make_classification(n_samples=1000, n_features=10, n_classes=2, random_state=42)

# Podział na zbiory treningowe i testowe
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Utworzenie i trenowanie modelu oraz predykacja przy pomocy Sklearn
model_sklearn = GradientBoostingClassifier(n_estimators=100, learning_rate=0.1, max_depth=3, random_state=42)

model_sklearn.fit(X_train, y_train)

y_pred_sklearn = model_sklearn.predict(X_test)

# Utworzenie i trenowanie modelu oraz predykacja przy pomocy xgboost
model_xgb = xgb.XGBClassifier(n_estimators=100, learning_rate=0.1, max_depth=3, random_state=42)

model_xgb.fit(X_train, y_train)

y_pred_xgb = model_xgb.predict(X_test)

# Utworzenie i trenowanie modelu oraz predykacja przy pomocy LightGBM
model_lgb = lgb.LGBMClassifier(n_estimators=100, learning_rate=0.1, max_depth=3, random_state=42) 

model_lgb.fit(X_train, y_train)

y_pred_lgb = model_lgb.predict(X_test)

```
# Co dalej?

Kliknij [[Wzmocnienie gradientowe (Gradient boosting)|tutaj]], aby wrócić do strony głównej tematu. Możesz stamtąd przejść do wykonania zadań przygotowanych w Jupyter Notebook.