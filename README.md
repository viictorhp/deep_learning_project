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
Modelo **DistilBERT multilingüe** (`lxyuan/distilbert-base-multilingual-cased-sentiments-student`) — 3 clases (positive / neutral / negative), compatible con inglés, italiano y francés. Aplicado sobre todas las reseñas del sector.

### Topic Modeling
Vectorización con **TF-IDF** (bigramas, token Unicode) + descomposición **NMF** con 6 componentes, entrenado sobre el sector completo para que los temas sean comparables entre empresas. Se optó por TF-IDF + NMF frente a BERTopic por su mayor robustez con corpus pequeños e interpretabilidad directa de los temas.

### Comparativa con competidores
Ranking por % de reseñas positivas, distribución de temas y gap de sentimiento por tema (dice.fm vs media del sector).

---

## Resultados

### Sentimiento global

| | % Positivo |
|---|---|
| dice.fm | **43.0%** |
| Sector (sin dice.fm) | **46.8%** |

dice.fm se sitúa 3.8 puntos por debajo de la media del sector.

### Distribución de temas (dice.fm)

| Tema | Reseñas | % |
|---|---|---|
| Compra de entradas | 27 | 27% |
| Reembolsos y pagos | 25 | 25% |
| Experiencia y ambiente | 22 | 22% |
| Proceso de compra online | 18 | 18% |
| Servicio al cliente | 7 | 7% |

### Sentimiento por tema — dice.fm vs sector

| Tema | dice.fm | Sector | Gap |
|---|---|---|---|
| Proceso de compra online | 88.9% | 65.1% | **+23.8%** ✅ |
| Compra de entradas | 44.4% | 33.6% | **+10.8%** ✅ |
| Experiencia y ambiente | 50.0% | 65.4% | -15.4% ❌ |
| Reembolsos y pagos | 8.0% | 19.0% | -11.0% ❌ |
| Servicio al cliente | 14.3% | 51.5% | **-37.2%** ❌ |

---

## Conclusiones

dice.fm destaca como plataforma de compra — su app y proceso de reserva están por encima del sector — pero pierde la confianza del usuario en el postventa.

**Fortalezas:**
- Proceso de compra online: +23.8% sobre el sector, principal ventaja competitiva.
- Disponibilidad de entradas: +10.8% sobre el sector.

**Áreas críticas:**
- **Reembolsos y pagos** (25% de las reseñas): solo 8% positivo. Fallos en la gestión de reembolsos y falta de respuesta del soporte son las quejas más frecuentes.
- **Servicio al cliente**: gap de -37.2% con el sector. Los usuarios describen falta de empatía y mala resolución de incidencias.
- **Experiencia en evento**: -15.4% sobre el sector, relacionado con condiciones en venues parcialmente fuera del control de dice.fm.

> La brecha entre la experiencia de compra (valorada positivamente) y la gestión de problemas (reembolsos, atención al cliente) es el principal factor que lastra la posición competitiva de dice.fm.
