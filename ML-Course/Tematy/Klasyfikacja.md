W zbiorze danych występuje 70 tys. obrazów, a każdy z nich opisany jest 784 cechami. Wynika to faktu, że każdy obraz ma 28x28 pikseli, a każda cecha opisuje natężenie szarości danego piksela
(przyjmuje wartość od 0 do 255)

```python
import tensorflow as tf  
import matplotlib.pyplot as plt  
  
mnist = tf.keras.datasets.mnist  
(train_images, train_labels), (test_images, test_labels) = mnist.load_data()  
  
X = train_images.reshape(60000, 28*28)   
y = train_labels  
  
print("Rozmiar danych X (zbiór uczący):", X.shape)  
print("Rozmiar danych y (etykiety):", y.shape)  
  
def plot_digit(image):  
    image = image.reshape(28, 28) 
    plt.imshow(image, cmap='binary')  
    plt.axis('off')  
    plt.show()  
  
# Wyświetlenie przykładów  
for i in range(5):  
    print(f"Przykład {i + 1}: Cyfra {y[i]}")  
    plot_digit(X[i])  
  
# Podział na zbiory: uczący (60 tys.) i testowy (10 tys.)  
X_train = X[:60000]  
y_train = y[:60000]  
  
X_test = test_images.reshape(10000, 28*28)  
y_test = test_labels  
  
print("Rozmiar danych uczących X_train:", X_train.shape)  
print("Rozmiar danych testowych X_test:", X_test.shape)

```

Przykładowe dane przedstawione są poniżej:
![[picture_1.png]]
![[picture_4.png]]
![[picture_9.png]]

>Rozmiar danych X (zbiór uczący): (60000, 784)
>Rozmiar danych y (etykiety): (60000,)

W powyższym przykładzie aby sprawdzić jak wyglądają cyfry przechowywane w zestawie danych wybraliśmy wektor cech danej próbki i przekształciliśmy go w macierz o rozmiarze 28x28, którą wyświetliliśmy za pomocą funkcji imshow(). Do uzyskania mapy w skali szarości wykorzystaliśmy parametr cmap='binary'. 


1. Uczenie klasyfikatora binarnego 
Na początku uprościmy sobie zadanie i spróbujemy identyfikować jedną cyfrę na przykład 5. Jest to przykład klasyfikatora binarnego, który ma zdolność do rozpoznawania jednej z dwóch klas: piątek i niepiątek. Zadanie to rozpoczniemy od stworzenia wektorów docelowych dla tego zadania klasyfikującego.
```python
X_test = test_images.reshape(10000, 28 * 28)    
y_test = test_labels  
  
y_train_binary = (y_train == 5).astype(np.int8)  # 1 dla cyfry 5, 0 dla innych  
y_test_binary = (y_test == 5).astype(np.int8)  
  

sgd_clf = SGDClassifier(random_state=42)  
sgd_clf.fit(X_train, y_train_binary)  
  

y_pred = sgd_clf.predict(X_test)  
  
accuracy = accuracy_score(y_test_binary, y_pred)  
print(f'Dokładność klasyfikatora: {accuracy:.2f}')  
  
print("Przykładowe predykcje (1 oznacza cyfrę 5):")  
print("Predykcje:", y_pred[:10])  
print("Prawdziwe etykiety:", y_test_binary[:10])  
  
```
>Dokładność klasyfikatora: 0.95
>Przykładowe predykcje (1 oznacza cyfrę 5):
>Predykcje: [0 0 0 0 0 0 0 0 0 0]
>Prawdziwe etykiety: [0 0 0 0 0 0 0 0 1 0]

W przykładzie wykorzystano klasyfikator stochastycznego spadku wzdłuż gradientu w tym celu skorzystano z klasy SGDClassifier. Klasyfikator ten sprawdza się w przypadku przetwarzania bardzo dużych zbiorów danych. Wynika to faktu, że klasyfikator ten przetwarza poszczególne przykłady uczące się niezależnie od siebie, po jednym naraz.

2. Miary wydajności:
 Dobrym sposobem oceny modelu jest wykorzystanie sprawdzianu krzyżowego. Zastosujemy funkcję cross_val_score() do oceny naszego modelu SGDClassifier za pomocą metody sprawdzianu krzyżowego, wygenerujemy trzy podzbiory.

 🚨 Ważna Uwaga

>[!important]
> Kroswalidacja k-krotna oznacza rozdzielenie zestawu uczącego się na k podzbiorów ( w naszym przypadku na 3), następnie wyuczany jest model k razy. W każdej iteracji, jeden z podzbiorów jest używany jako zestaw testowy, podczas gdy pozostałe k-1 podzbiory są używane do treningu modelu.

```python
from sklearn.model_selection import cross_val_score  

cross_val_scores = cross_val_score(sgd_clf, X_train, y_train_binary, cv=3, scoring="accuracy")  
print(f'Dokładność (kroswalidacja SGD): {cross_val_scores}')
```

>  [0.95035 0.96035 0.9604 ]

Jednak ten sposób oceny nie sprawdza się tak dobrze w przypadku gdy niektóre klasy występują znacznie częściej od pozostałych tzw. klasy wypaczone.

Innym sposobem oceny wydajności klasyfikatora jest  macierz pomyłek.

```

            Przewidywana
                1      0
              +----+----+
         1    | TP | FN |
Rzeczywista   +----+----+
         0    | FP | TN |
              +----+----+

```
   
Macierz pomyłek pozwala zrozumieć, w jaki sposób model popełnia błędy:

- **Wysokie wartości TP** wskazują, że model dobrze klasyfikuje pozytywne przypadki.
- **Wysokie wartości TN** wskazują na dobry poziom klasyfikacji negatywnych przypadków.
- **Wysokie wartości FP** wskazują, że model często myli negatywne przypadki z pozytywnymi.
- **Wysokie wartości FN** wskazują, że model często przeocza pozytywne przypadki.


```python
from sklearn.metrics import accuracy_score, confusion_matrix 
from sklearn.model_selection import cross_val_predict
import seaborn as sns

# Kroswalidacja z przewidywaniami  
y_pred_cv = cross_val_predict(sgd_clf, X_train, y_train_binary, cv=3)  
accuracy = accuracy_score(y_train_binary, y_pred_cv)  
print(f'Dokładność klasyfikatora (kroswalidacja): {accuracy:.2f}')  
  
confusion_mat = confusion_matrix(y_train_binary, y_pred_cv)  
  
# Wyświetlenie macierzy pomyłek  
plt.figure(figsize=(8, 6))  
sns.heatmap(confusion_mat, annot=True, fmt='d', cmap='Blues', xticklabels=['0', '1'], yticklabels=['0', '1'])  
plt.ylabel('Rzeczywista')  
plt.xlabel('Przewidywana')  
plt.title('Macierz Pomyłek')  
plt.show()
```

> Dokładność klasyfikatora (kroswalidacja): 0.96

![[Macierz.png]]
🚨 Ważna Uwaga

>[!important]
>Każdy rząd macierzy pomyłek reprezentuje klasę rzeczywista. Natomiast kolumna stanowi przewidywaną klasę. Interpretacja 53892 stanowi prawidłowo sklasyfikowane próbki niebędące piątkami tzw. PN, 687 przykładów zostało niewłaściwe uznane za 5, tzw. FP (błąd pierwszego rodzaju). 
W drugim rzędzie zostały umieszczone obrazy zaklasyfikowane jako piątki.
Przy czym 1891 próbek zostało nieprawidłowo sklasyfikowanych jako niebędące piątkami tzw. FN natomiast 3530 zostało prawidłowo zaklasyfikowane jako 5. 

>Nasz doskonały klasyfikator uzyskiwałby wyłącznie przykłady prawdziwe pozytywne i prawdziwe negatywne () na głównej przekątnej miałby niezerowe wartości. 

Jeszcze inne miary:

3. Pełność 

**Pełność** (znana również jako **czułość**) jest to odsetek pozytywnych przykładów prawidłowo rozpoznane przez klasyfikator.
$$ \text{Pełność} = \frac{TP}{TP + FN} $$


- \( TP \ (True Positives) - liczba rzeczywistych pozytywnych przypadków, które zostały poprawnie sklasyfikowane przez model.
- \( FN \ (False Negatives) - liczba rzeczywistych pozytywnych przypadków, które model błędnie sklasyfikował jako negatywne.

4. F1 
Jest to średnia harmoniczna precyzji z pełnością.  Jak to rozumieć?
Standardowa średnia traktuje wszystkie wartości jednakowo, natomiast średnia harmoniczna nadaje większą wagę małym wartością.
 $$ F1 = 2 \cdot \frac{\text{Precyzja} \cdot \text{Pełność}}{\text{Precyzja} + \text{Pełność}} $$ Gdzie: - **Precyzja** (Precision) to miara, która określa, jak wiele z przewidywanych pozytywnych przypadków jest rzeczywiście pozytywnych.
 $$ \text{Precyzja} = \frac{TP}{TP + FP} $$
```python

from sklearn.metrics import precision_score, recall_score, f1_score  

precision = precision_score(y_train_binary, y_pred_cv) 
recall = recall_score(y_train_binary, y_pred_cv) 
f1 = f1_score(y_train_binary, y_pred_cv)

print(f'Precyzja: {precision:.2f}') 
print(f'Pełność: {recall:.2f}') 
print(f'F1-score: {f1:.2f}')
```

>Precyzja: 0.84
>Pełność: 0.65
>F1-score: 0.73

 🚨 Ważna Uwaga Kompromis pomiędzy precyzją a pełnością
 
>[!important]
>Przy czym F1 faworyzuje klasyfikatory mające zbliżone wartości precyzji i pełności. Nie zawsze tego chcemy, przykładowo mając na celu wyuczenie klasyfikatora w określaniu bezpiecznych filmów dla dzieci bardziej zależałoby nam na tym by klasyfikator odrzucał wiele dobrych filmów (mała wartość pełności), ale zapamiętywałby jedynie bezpieczne (duża precyzja). Niekorzystna byłaby relacja odwrotna gdzie model cechowałby się dużo większą pełnością, ale dopuszczałby kilka nieodpowiednich filmów.
Jednak przy trenowaniu klasyfikatora do wykrywania złodziei z zapisu kamer prawdopodobnie nic złego by się nie stało gdyby model miał przykładowo 30% precyzji przy 99% pełności. Wówczas może i byłoby kilka fałszywych alarmów ale niemal wszyscy przestępcy zostaliby złapani.
### Klasyfikacja wieloetykietowa

Do tej pory każdy przykład był przydzielany wyłącznie do jednej klasy. Jednak weźmy przykład rozpoznawania twarzy, co powinien zrobić gdy na zdjęciu jest wiele osób? 
Powinien przydzielić po jednej etykiecie na każdą rozpoznaną twarz. Załóżmy ,że model został wyuczony do rozpoznania grupy przyjaciół na zdjęciu: Tomka, Piotrka i Agnieszki. Po zaprezentowaniu zdjęć Tomka i Piotrka powinien zostać wygenerowany wynik [True, True, False ].

Tego typu system klasyfikujący zdolny do wyznaczania wielu binarnych znaczników nosi nazwę klasyfikacji wieloetykietowej. 