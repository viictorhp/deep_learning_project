# Análisis de Reseñas Trustpilot — `dice.fm`

Caso práctico de Deep Learning y NLP. Análisis de reseñas de la empresa **dice.fm** (sector *Events & Entertainment*) usando técnicas de procesamiento de lenguaje natural, comparadas con el resto de empresas del sector.

---

## Contexto del proyecto

El rol es el de Data Scientist de **dice.fm**, una plataforma de venta de entradas para eventos musicales y de entretenimiento. El objetivo es analizar la reputación online de la empresa a través de reseñas de Trustpilot y compararla con la competencia del mismo sector para identificar fortalezas, debilidades y áreas de mejora.

---

## Dataset

| Archivo | Descripción |
|---|---|
| `trustpilot-reviews-123k.csv` | Dataset completo — 123.181 reseñas, 1.680 empresas, 22 sectores |
| `emp_100_reviews.xlsx` | 558 empresas con exactamente 100 reseñas cada una |

**Columnas:** `category`, `company`, `description`, `title`, `review`, `stars`

- Empresa analizada: **dice.fm** — 100 reseñas
- Sector: **Events & Entertainment**

---

## Objetivos del análisis

1. ¿Las reseñas de `dice.fm` son mayoritariamente positivas o negativas? ¿Y la competencia?
2. ¿Qué temas tratan principalmente las reseñas?
3. Para cada tema, ¿el sentimiento es positivo o negativo? ¿En qué somos mejores o peores que el sector?
4. Identificar áreas de mejora

---

## Metodología

### Preprocesamiento de texto
Limpieza de URLs, HTML, menciones, hashtags y tokens cortos. Normalización a minúsculas.

### Análisis de Sentimiento
Modelo **DistilBERT** (`distilbert-base-uncased-finetuned-sst-2-english`) — clasificación binaria POSITIVE / NEGATIVE aplicada sobre todas las reseñas del sector.

### Topic Modeling
Vectorización con **TF-IDF** (bigramas) + descomposición **NMF** con 6 componentes, entrenado sobre el sector completo para que los temas sean comparables entre empresas.

### Comparativa con competidores
Ranking por % de reseñas positivas, distribución de temas y gap de sentimiento por tema (dice.fm vs media del sector).

---

## Resultados

*(Por completar tras ejecutar el notebook)*

| Dimensión | dice.fm | Sector |
|---|---|---|
| % Positivo global | — | — |
| Media de estrellas | — | — |
| Tema más frecuente | — | — |
| Mejor tema (gap +) | — | — |
| Peor tema (gap −) | — | — |

---

## Archivos del proyecto

```
NLP_project/
├── Analisis_dice_fm.ipynb          ← Notebook principal
├── requirements.txt                ← Dependencias
├── README.md                       ← Este archivo
├── trustpilot-reviews-123k.csv     ← Dataset principal
├── emp_100_reviews.xlsx            ← Listado de empresas seleccionables
├── Directrices Caso Práctico DL.pdf
├── NLP.pdf
├── 09 Deep Learning.pdf
└── Articulo Medium DL.pdf
```

---

## Entregables

- **Notebook** (`Analisis_dice_fm.ipynb`) — 6 puntos
- **Presentación PowerPoint** — 4 puntos
  - Slide 1: Objetivos e hipótesis
  - Slide 2: Sentimiento positivo y negativo
  - Slide 3: Análisis de topics
  - Slide 4: Sentimiento y topics
  - Slide 5: Conclusiones
