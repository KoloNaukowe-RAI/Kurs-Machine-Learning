# Rodzaje regresji

Istnieją różne rodzaje regresji, które różnią się rodzajem zależności między zmiennymi, które modelują. Najczęściej występujące to:

- **Regresja liniowa:** Podstawowy rodzaj regresji, w którym założeniem jest liniowa zależność zmiennych (czyli można ją przedstawić za pomocą prostej), np. droga i czas w ruchu jednostajnym prostoliniowym,
- **Regresja wielomianowa:** Służy do modelowania bardziej złożonych zależności, których nie można opisać przy pomocy prostej, np. wzrost człowieka i wiek,
- **Regresja logistyczna:** Służy do przewidywania wartości binarnych (tak/nie, 0/1), np. czy stwierdzenie czy uda się przejechać drogę o danej długości bez tankowania,
- **Regresja drzewiasta:** Buduje model w postaci drzewa decyzyjnego, co pozwala na interpretację wyników, np. predykcja ceny domu, gdzie każdy węzeł jest pytaniem o jedną z cech (metraż, wiek, etc.).

Aby łatwiej było zrozumieć różnice, poniżej znajdują się przykładowe wykresy z wrysowanymi poszczególnymi typami regresji

![[regression_types.png]]

A na grafice poniżej widoczna jest wizualizacja drzewa decyzyjnego z przykładu powyżej, gdzie widać jak parametru `x` wpływa na wartość przewidywaną przez drzewo. Taki "schodkowy" przebieg regresji wynika z głębokości drzewa równej zaledwie `max_depth=3`, więc max 8 wartości na wyjściu.

![[decission_tree_regression_plot.png]]

# Co dalej?

Przejdź do kolejnego zagadnienia ([[Implementacja regresji przy pomocy Scikit-learn]]) lub kliknij [[Regresja liniowa (i nie tylko)|tutaj]], aby wrócić do strony głównej tematu.