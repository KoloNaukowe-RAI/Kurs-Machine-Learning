# Jak zaimplementować regresję w Pythonie?

## 1. Importowanie niezbędnych bibliotek

```Python
# Import niezbędnych bibliotek
import numpy as np
from sklearn.datasets import make_regression
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.tree import DecisionTreeRegressor
from sklearn.ensemble import RandomForestRegressor
from sklearn.svm import SVR
from sklearn.metrics import mean_squared_error
```

## 2. Wczytanie zbioru danych (w tym przypadku wygenerowanie)
```Python
X, y = make_regression(n_samples=1000, n_features=10, noise=0.1, random_state=42)
```

## 3. Podział danych na zestaw treningowy i testowy
```Python
# Podział danych na zestaw treningowy i testowy
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

## 4. Trenowanie modeli
```Python
# Regresja liniowa
model_lr = LinearRegression()
model_lr.fit(X_train, y_train)

# Drzewo decyzyjne
model_dt = DecisionTreeRegressor()
model_dt.fit(X_train, y_train)

# Las losowy
model_rf = RandomForestRegressor(n_estimators=100)
model_rf.fit(X_train, y_train)

# SVR
model_svr = SVR()
model_svr.fit(X_train, y_train)
```

## 5. Predykcja na zbiorze testowym
```Python
y_pred_lr = model.predict(X_test)
y_pred_dt = model.predict(X_test)
y_pred_rf = model.predict(X_test)
y_pred_svr = model.predict(X_test)
```

## 6. Obliczenie błędu w celu walidacji modeli
```Python
mse_lr = mean_squared_error(y_test, y_pred_lr)
mse_dt = mean_squared_error(y_test, y_pred_dt)
mse_rf = mean_squared_error(y_test, y_pred_rf)
mse_svr = mean_squared_error(y_test, y_pred_svr)
```

# Implementacja przy pomocy Pipeline
```Python
import numpy as np
from sklearn.datasets import make_regression
from sklearn.model_selection import train_test_split
from sklearn.svm import SVR
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import mean_squared_error
from sklearn.pipeline import Pipeline

X, y = make_regression(n_samples=1000, n_features=10, noise=0.1, random_state=42)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Tworzenie Pipeline dla modelu SVR
pipeline = Pipeline([
    ('scaler', StandardScaler()),  # Skalowanie danych
    ('svr', SVR())                 # Regresor SVR
])

# Trenowanie Pipeline
pipeline.fit(X_train, y_train)

# Predykcja przy użyciu Pipeline
y_pred_pipeline = pipeline.predict(X_test)

# Ocena modelu Pipeline
mse_pipeline = mean_squared_error(y_test, y_pred_pipeline)
```
# Co dalej?

Kliknij [[Regresja liniowa (i nie tylko)|tutaj]], aby wrócić do strony głównej tematu. Możesz stamtąd przejść do wykonania zadań przygotowanych w Jupyter Notebook.