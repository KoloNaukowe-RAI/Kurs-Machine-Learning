![[datavis.png]]

Omówienie najpopularniejszych bibliotek do wizualizacji danych:

| Biblioteka     | Opis                                                                           | Cechy                                                                                                                                                                                                                                                                 | Przykładowe zastosowania                      |
| -------------- | ------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| **Matplotlib** | Podstawowa biblioteka do tworzenia wykresów w Pythonie                         | - dobrze integruje się z Numpy i Pandas<br><br>- Umożliwia dostosowywanie wykresów, w tym zmiana kolorów, stylów linii, rozmiarów markerów oraz dodawanie tytułów i etykiet.<br><br>- Obsługuje subplots <br><br>- Możliwość zapisywania wykresów w różnych formatach | Wykresy liniowe, słupkowe, kołowe, histogramy |
| **Seaborn**    | Biblioteka oparta na Matplotlib, ułatwiająca tworzenie wykresów statystycznych | - Umożliwia tworzenie wykresów macierzowych, takich jak heatmapy i pairploty, do analizy korelacji i rozkładów.<br><br>- posiada wbudowane style i palety kolorów<br><br>- dobrze integruje się z danymi  Pandas                                                      | Wykresy pudełkowe, heatmapy, histogramy       |
| **Plotly**     | Biblioteka do tworzenia interaktywnych wykresów                                | - Interaktywność (zoomowanie, najeżdżanie, kliknięcia)<br><br>- Szeroki zakres typów wykresów (w tym mapy i wykresy 3D)<br><br>- Sprawdza się w aplikacjach webowych i notebookach Jupyter                                                                            | Wykresy interaktywne, wykresy 3D, mapy        |
Szczegółowe dokumentacje:

- [Matplotlib Documentation](https://matplotlib.org/stable/contents.html)
- [Seaborn Documentation](https://seaborn.pydata.org/)
- [Plotly Documentation](https://plotly.com/python/)


**Przykładowy wykres przy pomocy biblioteki matplotlib:**

```python
import matplotlib.pyplot as plt
import pandas as pd


data = {
    'Miesiąc': ['Styczeń', 'Luty', 'Marzec', 'Kwiecień', 'Maj', 'Czerwiec', 'Lipiec', 'Sierpień', 'Wrzesień', 'Październik', 'Listopad', 'Grudzień'],
    'Przychody (tys. USD)': [9500, 9800, 10200, 10300, 11000, 11500, 12000, 12500, 11500, 11000, 10500, 9900]
}

df = pd.DataFrame(data)

plt.figure(figsize=(12, 6))
plt.plot(df['Miesiąc'], df['Przychody (tys. USD)'], marker='o', linestyle='-', color='teal')
plt.title('Miesięczne przychody spółki w 2023 roku')
plt.xlabel('Miesiąc')
plt.ylabel('Przychody (tys. USD)')
plt.xticks(rotation=45)
plt.grid(True)
plt.tight_layout()
plt.show()


```
\
**Przykładowy wykres słupkowy przy pomocy biblioteki seaborn:**
```python
import seaborn as sns 
import pandas as pd

data = { 
		'Miasto': ['Warszawa', 'Kraków', 'Gdańsk', 'Wrocław', 'Poznań', 'Szczecin', 'Olsztyn'], 
	    'Cena': [800, 750, 700, 680, 650, 620, 570, 490] 
	    }
	    
df = pd.DataFrame(data)

sns.barplot(x='Miasto', y='Cena', data=df, palette='viridis') 
plt.title('Cena mieszkań w różnych miastach') 
plt.xlabel('Miasto')
plt.ylabel('Cena mieszkania (w tys. PLN)') 
plt.show()


```

**Przykładowy wykres kołowy przy pomocy biblioteki seaborn:**
```python
import seaborn as sns  
import pandas as pd  
import matplotlib.pyplot as plt  
  
  
data = {  
    'Kategoria': ['Narzędzia', 'Oświetlenie', 'Farby i lakiery', 'Ogrodnictwo', 'Meble'],  
    'Udział': [30, 20, 25, 15, 10]  
}  
  
df = pd.DataFrame(data)  
  
plt.figure(figsize=(8, 8))  
plt.pie(df['Udział'], labels=df['Kategoria'], autopct='%1.1f%%', colors=sns.color_palette('Set1'))  
plt.title('Udział kategorii produktów w sprzedaży w sklepie OBI')  
plt.show()



```

**Przykładowe wykresy przy pomocy biblioteki Plotly:**

```python 
# wykres kołowy 

import plotly.express as px  
import pandas as pd  

data = {  
    'Producent': ['Apple', 'Samsung', 'Huawei', 'Xiaomi', 'Oppo'],  
    'Udział': [40, 30, 15, 10, 5]  
}  
  
df = pd.DataFrame(data)  
  
fig = px.pie(df, values='Udział', names='Producent', title='Udział rynkowy producentów telefonów')  
fig.update_traces(textinfo='percent+label')  
fig.show()

```

```python 
# wykres słupkowy  
import plotly.graph_objects as go  
import pandas as pd  
  

data = {  
    'Kraj': ['USA', 'Chiny', 'Japonia', 'Wielka Brytania', 'Australia'],  
    'Złote': [15, 12, 10, 8, 7],  
    'Srebrne': [10, 11, 9, 8, 6],  
    'Brązowe': [10, 7, 8, 6, 6]  
}  
  
df = pd.DataFrame(data)  
fig = go.Figure()  
  

fig.add_trace(go.Bar(  
    x=df['Kraj'],  
    y=df['Złote'],  
    name='Złote',  
    marker_color='gold'  
))  
  
fig.add_trace(go.Bar(  
    x=df['Kraj'],  
    y=df['Srebrne'],  
    name='Srebrne',  
    marker_color='silver'  
))  
  
fig.add_trace(go.Bar(  
    x=df['Kraj'],  
    y=df['Brązowe'],  
    name='Brązowe',  
    marker_color='#cd7f32'  
))  
   
fig.update_layout(  
    title='Liczba medali dla Top 5 Krajów na Igrzyskach Olimpijskich w Paryżu 2024',  
    xaxis_title='Kraj',  
    yaxis_title='Liczba Medali',  
    barmode='group',    
template='plotly_white'  
)  
  
fig.show()
```

```python 

import plotly.graph_objects as go  
import pandas as pd  
  

data = {  
    'Data': ['2024-07-01', '2024-07-15', '2024-08-01', '2024-08-15', '2024-09-01'],  
    'Manchester City': [10, 12, 15, 18, 20],  
    'Real Madryt': [8, 10, 12, 14, 17],  
    'Bayern Monachium': [9, 11, 14, 16, 19],  
    'Paris Saint-Germain': [7, 9, 13, 15, 18],  
    'Liverpool': [6, 8, 11, 13, 16]  
}  
  
df = pd.DataFrame(data)  
df['Data'] = pd.to_datetime(df['Data'])  
  
  
fig = go.Figure()  
  
for team in df.columns[1:]:  
    fig.add_trace(go.Scatter(  
        x=df['Data'],  
        y=df[team],  
        mode='lines+markers',  
        name=team,  
        text=df[team],  
        textposition='top center'  
    ))  

fig.update_layout(  
    title='Zmiana punktacji Drużyn UEFA w ciągu kilku tygodni',  
    xaxis_title='Data',  
    yaxis_title='Punkty',  
    legend_title='Drużyna',  
    template='plotly_dark',  
    xaxis=dict(  
        tickformat='%Y-%m-%d',  
        tickvals=df['Data'],  
        ticktext=[date.strftime('%b %d') for date in df['Data']]  
    )  
)  
  
fig.show()
```