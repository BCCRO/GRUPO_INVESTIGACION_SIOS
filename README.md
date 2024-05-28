# Análisis de Sentimientos y Frecuencia de Palabras
## Descripción :bookmark_tabs:
Este proyecto realiza un análisis de sentimientos y de frecuencia de palabras en las respuestas de una serie de entrevistas realizadas a estudiantes de la Universidad Distrital Francisco José de Caldas. Las entrevistas están centradas en la ética y la responsabilidad social en el contexto universitario y profesional. El análisis incluye la generación de gráficos de word cloud, gráficos de barras y gráficos de torta para visualizar los resultados.
## Requisitos :dart:
* Python 3.12.3
* `pandas`
* `matplotlib`
* `nltk`
* `wordcloud`
## Funcionalidades :rocket:
* Análisis de Sentimientos: Utiliza la herramienta [VADER de NLTK](https://www.nltk.org/api/nltk.sentiment.vader.html) para evaluar la positividad, negatividad o neutralidad de las respuestas.
```python
  # Inicializar el analizador de sentimientos de VADER
  sid = SentimentIntensityAnalyzer()

  for respuesta in respuestas:
    # Análisis de sentimientos
    scores = sid.polarity_scores(str(respuesta))
    sentimientos.append(scores['compound'])
```
* Frecuencia de Palabras: Cuenta la frecuencia de las palabras más utilizadas en las respuestas, excluyendo las palabras comunes ["stopwords"](https://www.nltk.org/search.html?q=stopwords).
```python
  from nltk.corpus import stopwords
  # Obtener lista de stopwords en español
  stop_words = set(stopwords.words('spanish'))

  for respuesta in respuestas:
      # Tokenización y eliminación de stopwords
      palabras = nltk.word_tokenize(str(respuesta).lower())
      palabras_filtradas = [palabra for palabra in palabras if palabra.isalnum() and palabra not in stop_words]
      palabras_clave.update(palabras_filtradas)
```
* Visualización: Genera word clouds y gráficos de barras para mostrar las palabras más frecuentes, y gráficos de torta y barras para la distribución de sentimientos.
```python
  # Generar word cloud de las palabras mas frecuentes
  wordcloud = WordCloud(width=800, height=400, background_color='white').generate_from_frequencies(datos['palabras_clave'])
  plt.figure(figsize=(10, 6))
  plt.imshow(wordcloud, interpolation='bilinear')
  plt.title(f"Word Cloud de las palabras más frecuentes - Pregunta: {columna}")
  plt.axis('off')
  plt.show()

  # Generar grafico de barras de las palabras mas frecuentes por pregunta
  palabras = [item[0] for item in datos['palabras_clave'].most_common(10)]
  frecuencias = [item[1] for item in datos['palabras_clave'].most_common(10)]

  plt.figure(figsize=(12, 6))
  plt.bar(palabras, frecuencias, color='#00BFBF')
  plt.title(f"Frecuencia de las palabras más comunes - Pregunta: {columna}")
  plt.xlabel('Palabras')
  plt.ylabel('Frecuencia')
  plt.xticks(rotation=45)
  plt.show()
```
## Instalación y Ejecución :hammer_and_wrench:
1. Clonar el repositorio.
` git clone`




