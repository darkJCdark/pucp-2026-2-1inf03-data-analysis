# 1INF03 – Análisis de Datos (PUCP 2026-2) · Resumen de teoría

> Consolidado a partir del sílabo, las diapositivas (S1–S6), tus notas de clase (`Clase N.txt`), las transcripciones de las sesiones S1–S6 y los notebooks del repositorio.
> **Cobertura:** semanas 1 a 6 (KDD, Steps 1–7a). Las semanas 7–15 aún no tienen material en el repositorio.
> Los apartados marcados **(complemento)** son definiciones estándar que no aparecen textualmente en el material; el resto proviene del curso.

- **Docente:** Carmen Stéfany Neciosup Vera · **Créditos:** 3.5 · **Requisito:** 1INF24 Inteligencia Artificial
- **Metodología:** clases expositivas (teoría) + laboratorios en Python/R. El curso se desarrolla sobre un proyecto real con una institución aliada (Tarea Académica).
- **Evaluación:** `Nota final = (30·Pb + 30·Ta + 20·Ex1 + 20·Ex2) / 100` (Pb: 3 prácticas, Ta: 3 tareas académicas, Ex: 2 exámenes).
- **IA generativa:** su uso debe declararse y citarse; el docente puede pedir el reporte de prompts como anexo. No hacerlo es falta de ética académica.
- **Plagio:** nota cero.
- **Bibliografía obligatoria:** Knaflic (*Storytelling with Data*), Larose & Larose (*Data Mining and Predictive Analytics*), Fayyad et al. 1996 (*Advances in KDD and Data Mining*), Marz (*Big Data*), Duda/Hart/Stork (*Pattern Classification*).

### Unidades del programa analítico

| Unidad | Tema | Horas |
|---|---|---|
| 1 | Introducción a KDD | 3 |
| 2 | Selección y pre-procesamiento de datos | 6 |
| 3 | Transformación de datos (incluye reducción de dimensionalidad) | 9 |
| 4 | Minería de datos (predicción/descripción; clasificación, regresión, clustering; reglas de asociación y patrones secuenciales) | 15 |
| 5 | Visualización e interpretación de resultados | 9 |

---

## 1. Fundamentos: dato → información → conocimiento

- **Variable:** característica medible u observable de un individuo u objeto (peso, edad, créditos matriculados). Es un concepto, todavía sin valores.
- **Población:** todos los individuos de interés (p. ej. todos los alumnos del curso este año).
- **Muestra (tamaño *n*):** subconjunto sobre el que se mide.
- **Variable aleatoria:** cuando la variable "aterriza" en una muestra de tamaño *n* se vuelve un vector de *n* posiciones (aún sin valores). Es "aleatoria" porque su valor depende del azar del individuo observado.
- **Dato:** el valor concreto que toma el vector de la variable aleatoria en la muestra. Es una representación simbólica; por sí solo **no contiene información**.
- **Información:** los datos resumidos/procesados bajo una hipótesis.
- **Conocimiento:** la información genera un razonamiento que permite **tomar decisiones**.

> Idea fuerza: los gerentes no necesitan más datos, necesitan menos ruido y mejor información. "Un problema correctamente planteado está parcialmente resuelto" (Ackoff, 1967).

---

## 2. Metodología KDD (Knowledge Discovery in Databases)

### 2.1 Definiciones

- **Fayyad, Piatetsky-Shapiro & Smyth (1996):** proceso **no trivial** de identificar patrones en los datos que sean **válidos, novedosos, potencialmente útiles y finalmente comprensibles**.
- **Fayyad (1997):** campo de la IA en rápido crecimiento que combina aprendizaje de máquina, reconocimiento de patrones, estadística, bases de datos y visualización para extraer conocimiento de datos de bajo nivel.
- **Molina (2001):** extracción no trivial de información implícita y potencialmente útil desde un gran volumen de datos.

### 2.2 Los 9 pasos (en el curso: 9 pasos ↔ 9 notebooks)

Los pasos son secuenciales, pero **siempre se puede regresar** a uno anterior si algo no cuadra.

| # | Paso | Esencia | Output en el curso |
|---|---|---|---|
| 1 | Entendimiento del dominio y objetivos (KDD goals) | Entender el negocio, los datos y el objetivo desde el punto de vista del cliente | **Ficha técnica** del proyecto (Excel) |
| 2 | Creación del *target dataset*: selección y entendimiento | Elegir qué datos y variables usar; explorarlos | Reporte de selección + descripción de variables |
| 3 | Limpieza y pre-procesamiento | Ruido, duplicados, vacíos, atípicos | **Reporte de pre-procesamiento** |
| 4 | Reducción y proyección de datos | Transformar variables y/o reducir dimensiones | Archivo con las "p" componentes/factores + variables transformadas |
| 5 | Elegir la **tarea** de minería de datos | Emparejar los objetivos KDD con el tipo de tarea (clasificación, regresión, clustering, etc.) | Decisión documentada |
| 6 | Elegir el/los **algoritmo(s)** y parámetros | Según la tarea y el tipo de variable | Lista de técnicas (recomendado: **mínimo 3** para comparar) |
| 7 | **Minería de datos** | Entrenar modelos, ajustar hiperparámetros (paso que suele demorar) | Modelos entrenados |
| 8 | Interpretación de patrones | Visualización; puede volver a pasos anteriores. Se interpreta internamente antes de exponerlo al negocio | Hallazgos |
| 9 | Consolidación del conocimiento | Documentar y reportar en **términos del negocio** | Informe final |

Aclaraciones del docente:

- *Target data set* **no** es la variable objetivo: es el conjunto de datos con el que se trabajará. De 100 variables, muchas pueden ser IDs o etiquetas y solo 10 servir para modelar. Las *samples* son las filas.
- KDD del curso tiene **entrega final, no despliegue**.
- Pasos 5–7 = **Data Mining**. El paso 5 es "elegir qué puerta abrir"; el 6 es elegir la herramienta dentro de esa puerta; el 7 es entrenar.

### 2.3 Métodos de minería de datos: descripción vs. predicción

- En KDD, la **descripción** suele importar más que la predicción (a diferencia de ML/reconocimiento de patrones, donde predecir suele ser el objetivo principal).
- **No siempre un modelo predictivo es la mejor solución:** a veces describir la casuística (resumen estadístico o gráfico) es lo adecuado.
- Descripción → resumen estadístico/gráfico, clustering. Predicción → clasificación y regresión.

### 2.4 Otras metodologías

| Metodología | Fases | Notas |
|---|---|---|
| **CRISP-DM** (*Cross Industry Standard Process for Data Mining*) | 1 Comprensión del negocio · 2 Comprensión de los datos · 3 Preparación · 4 Modelado · 5 Evaluación · 6 **Despliegue** | Sí incluye despliegue (p. ej. modelo que corre en el día a día de una empresa). |
| **SEMMA** (SAS Institute) | Sampling · Explore · Modify · Model · Assess | Asume que ya se entendió el negocio/los datos; 5 fases. |

---

## 3. Step 1 – Entendimiento del negocio

Se hace una primera reunión con los dueños de los datos: **ellos** explican el problema, los datos (todas las columnas) y qué esperan recibir; el analista escucha. Si se quiere un modelo predictivo, se necesita la **variable objetivo**.

### 3.1 Planteamiento del problema

Criterios (Kerlinger & Lee, 2002):

1. Debe expresar una **relación entre dos o más variables**.
2. Debe formularse **como pregunta**, clara y sin ambigüedad.
3. Debe permitir una **prueba empírica** o recolección de datos.

### 3.2 Definir objetivos

- **Objetivos del negocio:** ¿qué se desea lograr? ¿cómo ayuda al negocio? ¿áreas interesadas/experto de datos? ¿qué características lo hacen factible? ¿qué esperan recibir (etiqueta vs. probabilidad de riesgo)? ¿cómo usarán el resultado? ¿de cuánto tiempo disponemos?
- **Objetivos de análisis de datos:** *traducción* de los objetivos del negocio (no son lo mismo). Incluye definir **métricas/criterios de evaluación** desde el inicio (métricas del negocio ≠ métricas para entrenar el modelo), un **plan de análisis** (tiempos, hitos, responsables, avances) y **validar cada paso con el negocio**.

### 3.3 Delimitar la población de análisis

Se delimita **en espacio y en tiempo**; el modelo solo servirá para las características de esa población.

- **Criterios de inclusión:** quiénes entran.
- **Criterios de exclusión:** características que no deben tener.
- **Criterios de eliminación:** quienes cumplían la inclusión pero se retiran por hallazgos durante el análisis.

### 3.4 Recursos y limitaciones

| Recursos | Limitaciones |
|---|---|
| **Personas:** especialistas del negocio, líder analítico, analistas de datos, ingeniería de datos (suele ser el dueño de los datos; entrega la tabla final al analista). **Datos:** fuentes, dueños, calidad esperada. **Herramientas:** software, entornos de pre-procesamiento, entrenamiento y despliegue. | **Negocio:** capacidad operativa, poder de acción, normativas (datos sensibles). **Datos:** acceso a todos los datos/toda la población; hay datos usables para entrenar pero no disponibles a futuro. **Tiempo:** tiempo de análisis y de despliegue (el despliegue es aparte del modelo). Conviene dejarlas claras **desde que se acepta el proyecto**. |

**Output del Step 1:** Ficha Técnica del Proyecto de Análisis de Datos.

---

## 4. Step 2 – Selección y entendimiento de los datos

Dos subpasos: **2.1 Selección** (qué datos/variables entran) y **2.2 Entendimiento** (exploración/descripción).

### 4.1 Tipos de datos

Estructurados (filas/columnas) y no estructurados (texto, imágenes; almacenamiento en bases documentales).

### 4.2 Tipos de variables

| Clasificación | Tipos | Detalle |
|---|---|---|
| **Por naturaleza** | Cualitativa | Categorías; no se pueden promediar. Aunque se codifiquen 1, 2, 3 siguen siendo texto/categoría. |
| | Cuantitativa | Discreta (conteos) o continua |
| **Por escala de medida** | Nominal (cualitativa) | Lista de categorías sin relación entre ellas |
| | Ordinal (cualitativa) | Nominal con jerarquía interna; se puede etiquetar 1,2,3,4 pero **no se opera** (no hay promedio) |
| | De intervalo (cuantitativa) | El cero es **relativo** (depende del instrumento). Ej.: temperatura |
| | De razón (cuantitativa) | El cero es **absoluto** (ausencia de la variable). Ej.: número de hijos |

Advertencia: según el tipo de variable cambia el coeficiente de correlación y la medida de resumen a usar. En Python, `string ≠ object ≠ category`.

### 4.3 Medidas de resumen – variables cualitativas

Frecuencia absoluta (conteo), frecuencia relativa/proporción (conteo/total), porcentaje (proporción × 100 %) y **moda**. Gráficos: barras y pie/dona (las barras no se usan para cuantitativas discretas).

### 4.4 Medidas de resumen – variables cuantitativas

Se describe una variable con **cuatro "brazos"** más un gráfico. **Mínimo se reporta una medida de tendencia central + una de dispersión** (cubre ~90–95 % de la descripción).

| Brazo | Qué mide | Medidas |
|---|---|---|
| **Tendencia central / posición** | Centro y ubicación | Media (punto de equilibrio), mediana (divide 50/50), moda (cresta más alta), cuantiles |
| **Dispersión** | Cuánto se alejan los datos de un punto y entre sí; complementa a la tendencia central | Rango (máx − mín), rango intercuartil, varianza, desviación estándar, coeficiente de variación |
| **Asimetría** (deformación horizontal) | Simetría izquierda-derecha | Coeficiente de asimetría (AS) |
| **Curtosis / apuntamiento** (deformación vertical) | Qué tan apuntada o aplastada está respecto a la normal | Coeficiente de curtosis |

**Cuantiles.** Un cuantil no es el bloque sino la **línea que divide**. Con 100 % de datos: 3 cuartiles, 9 deciles, 99 percentiles. Equivalencia de la mediana: `Q2 = D5 = P50`.

**Mediana:** ordenar los datos; si *n* es impar, el valor central; si es par, el promedio de los dos centrales.

**Rango intercuartil (RIC):** `Q3 − Q1`, es el rango del **50 % central** de los datos (no confundir con el rango general).

**Varianza y desviación estándar.**

| | Población | Muestra |
|---|---|---|
| Media | μ = Σx / N | x̄ = Σx / n |
| Varianza | σ² = Σ(x−μ)² / N | s² = Σ(x−x̄)² / (n−1) |
| Desv. estándar | σ | s |

- El divisor **n−1** en la muestra hace al estimador **insesgado** (converge al valor poblacional).
- Interpretación: la varianza es el **promedio de las distancias al cuadrado**; la desviación estándar es, en términos prácticos, "en promedio cuánto se alejan los datos de la media". La varianza está en **unidades al cuadrado** (años², soles²), por eso para explicar se usa la desviación estándar.
- Ejemplo: x̄ = 22 años, s = 2 años, s² = 4 años².

**Coeficiente de variación:** `CV = s / x̄`. Elimina las unidades: sirve para **comparar dispersión** entre variables con distintas unidades (años vs. soles) o con la misma unidad pero distinta media. Comparar `s` directamente sería erróneo.

| Variable | x̄ | s | CV |
|---|---|---|---|
| Ingresos (Z) | 15 000 soles | 780 soles | 0.052 |
| Edad (Y) | 22 años | 3 años | 0.136 |

→ La edad tiene **mayor** dispersión relativa aunque `s_Z > s_Y`. Además ayuda a decidir qué variables meter a una segmentación (una variable muy dispersa puede meter ruido).

**Parejas compatibles ("match") de resumen:**

- **Media ↔ desviación estándar**
- **Mediana ↔ rango intercuartil**

No se mezclan entre sí. Esto se reutiliza al detectar atípicos y al transformar variables.

**Asimetría (AS).**

- `AS = 0`: simétrica; `AS < 0`: cola larga hacia el infinito negativo; `AS > 0`: cola hacia el infinito positivo. El signo se nombra por **hacia dónde se estira la cola**, no por dónde está la cresta.
- En la normal (única distribución con media = mediana = moda) las tres coinciden. Con asimetría: la **media** es la más sensible (se mueve hacia la cola), la **moda** "le da la contra" (se mueve al lado opuesto) y la **mediana** se mueve poco → es la medida **más robusta a atípicos**.

**Curtosis (referencia = normal):** mesocúrtica (como la normal), leptocúrtica (más apuntada), platicúrtica (más aplastada).

### 4.5 Detección de atípicos (sistema de alertas naive)

| | Diagrama de cajas (mediana + RIC) | Distribución normal / Z-score (media + s) |
|---|---|---|
| Umbral inferior | `Q1 − 1.5·RIC` | `x̄ − 3·s` |
| Umbral superior | `Q3 + 1.5·RIC` | `x̄ + 3·s` |
| Usar cuando | Distribución **asimétrica** (y también funciona en simétricas) | Distribución **simétrica / pseudonormal** |

- Los límites de la fórmula son **teóricos**; el límite **real** de la caja se ajusta hasta el último dato que existe dentro del umbral. Todo registro fuera del límite real dispara la alerta.
- ¿Por qué 1.5 y 3? En la normal estándar (μ = 0, σ² = 1), ±1.5 abarca casi el 95 % y ±3 casi el 99 %; lo que queda fuera de ±3 es "recontra atípico".
- Si hay que quedarse con **un solo método**, el de la mediana (cajas) funciona bien en ambos escenarios.
- Ejemplo del docente: máquina que llena botellas de 500 ml; se fijan umbrales para alertar cuando se descalibra.

**Output del Step 2:** reporte de selección y descripción de variables (cuali y cuanti).

---

## 5. Step 3 – Pre-procesamiento: limpieza de datos

Suele ser el paso que más demora y depende del contexto. Siempre analizar **variable por variable** antes de tratar de forma masiva.

### 5.1 Datos duplicados

- **Completos:** filas idénticas en todas las columnas → `df.duplicated()`.
- **Parciales:** duplicadas solo en columnas clave (p. ej. ID y fecha) → `df.duplicated(subset=['ID','fecha'])`.

### 5.2 Datos vacíos (*empty*)

Celdas aparentemente vacías pueden ser `" "` (espacio), `""` (cadena vacía) o `NA/NaN`. Un espacio a veces significa una **categoría nueva**; si no tiene interpretación, se convierte a `NaN`. Hay que entender **por qué** hay vacíos: no todos se tratan igual.

### 5.3 Datos faltantes (*missing*): mecanismos

| Mecanismo | Definición | Preocupación | Tratamientos |
|---|---|---|---|
| **MCAR** (*Missing Completely at Random*) | Falta completamente al azar; sin relación con otras variables ni con el valor perdido. Sin patrón en filas ni columnas (p. ej. falló el instrumento). | Ninguna | Eliminar filas/columnas; **imputación simple/univariada** (media, mediana, moda) |
| **MAR** (*Missing at Random*) | Depende de **otras variables observadas**, pero no del valor que falta. | Poca | **Variable flag** (columna 0/1 que indica el vacío), imputación **condicional**, **multivariada** (KNN-imputer, modelos predictivos), modelos bayesianos o EM |
| **MNAR** (*Missing Not at Random*) | El dato falta **por su propio valor** (no observable). Ej.: por ser menor de edad no da sus datos. | Mucha; no hay forma directa de recuperarlo | Columna flag, recuperar de **fuentes externas**, **Heckman imputation**, mejorar la recolección |

**Buenas prácticas de imputación:**

- Imputación **univariada** usa una sola variable (media/mediana); **condicional/bivariada** usa la media por grupo de otra variable (p. ej. media de ingresos para <30 y ≥30 años); **multivariada** usa varias variables (KNN, iterativa/MICE, MissForest).
- Establecer un **máximo de vacíos** para imputar (el docente usa 15 %, como máximo 20 %; depende de la distribución). Medirlo por **columna** (para imputarla) y por **fila** (para decidir si la fila se queda).
- **Comparar la distribución antes vs. después** de imputar: si aparece una "joroba" en el centro (típico de imputar mucha media/mediana), el método está mal elegido.
- `ffill/bfill` (imputar con el valor anterior/siguiente) solo si el orden de las filas es aleatorio; si la tabla está ordenada por otra variable, se introduce sesgo.
- **KNN imputer:** para cada fila con vacío busca los *k* perfiles más parecidos (por distancias, en el resto de variables) y toma sus valores. **Iterativo:** predice el valor faltante usando **todas** las demás columnas.
- Guardar separadas las variables numéricas y categóricas (**manteniendo el orden de las filas**) para poder reunirlas. Cada paso debería generar su propio output diferenciado.
- Para categóricas: imputar con la moda o **crear una nueva categoría** ("Desconocido").

### 5.4 Datos atípicos (*outliers*)

- Distorsionan modelos (p. ej. sesgan una regresión lineal). Hay que descubrirlos antes de modelar; en el caso multivariado el efecto es menos evidente. No todo dato extremo es un error: puede ser una observación con sentido.

**Opciones de tratamiento:**

| Técnica | Descripción |
|---|---|
| **Trimming** | Eliminar las filas con atípicos |
| **Capping (winsorización)** | Reemplazar el atípico por el **valor límite** de la variable (con IQR o con Z-score). Busca "disimular" el atípico → no abusar; comparar gráfico antes/después y cambiar de tratamiento si el comportamiento cambió |
| **Imputation** | Tratar el atípico como vacío e imputarlo (univariada/multivariada, KNN, MissForest) |
| **Transformation** | Aplicar log o raíz para acercar los extremos |
| **Flag** | Marcar el atípico en una columna indicadora |

Elección del método de detección/capping: **cajas/IQR para asimétricas, Z-score para simétricas** (la media es sensible en asimetría).

### 5.5 Transformaciones de escala

| Transformación | Fórmula | Efecto | Cuándo usarla |
|---|---|---|---|
| **Normalización (Min-Max)** | `(x − mín)/(máx − mín)` | Lleva al rango [0, 1]; conserva la forma pero comprime; "hace cortes" | Modelos basados en **distancias**, variables acotadas en rango |
| **Estandarización (Z)** | `z = (x − x̄)/s` | Media 0 y varianza 1; **no acota** (mantiene la variabilidad; la desviación estándar es una unidad de medida, no un corte). Permite comparar variables de distinta unidad | Cuando importa la variabilidad; distribución ~ simétrica |
| **Estandarización/normalización robusta** | `(x − mediana)/RIC` | Igual idea pero con mediana y RIC | Datos con **atípicos o asimetría** |
| **Logaritmo** | `log(x)` | Acerca los extremos; si se transforma **Y**, se predice el log y luego se aplica la inversa | Distribuciones muy sesgadas |

Reglas prácticas del docente:

- "Normalizar" y "estandarizar" **no son lo mismo**.
- Transformar Y no es lo mismo que transformar X; si se transforma Y, se mantiene hasta el final.
- Si no hay certeza, entrenar varios escenarios (X original, X normalizada, X estandarizada) y comparar.
- **No siempre aplicar una transformación masiva.** Ejemplo (S6): variables en porcentaje 0–100 más una variable "promedio de hogares": solo esta se lleva a Min-Max (ideal con el mínimo/máximo **poblacional**, no solo el de la muestra) y luego se divide todo entre 100. Aplicar Min-Max a todas destruiría el significado de las distancias porcentuales y fallaría al predecir un valor fuera del rango visto.
- Guardar el objeto de transformación (p. ej. con `pickle`) para reutilizarlo al predecir con nuevos datos.

**Output del Step 3:** Reporte de pre-procesamiento.

---

## 6. Step 4 – Transformación y reducción de dimensiones

La reducción de dimensiones es una transformación (columnas). **No es obligatoria.** Son modelos que pertenecen al mundo del data mining, pero aquí se usan como paso previo. **Consecuencia:** se **pierde interpretabilidad** y se reducen las dimensiones consideradas. El output son las nuevas columnas (componentes/factores) junto con las originales que no se modifican.

### 6.1 PCA – Análisis de Componentes Principales

**Idea.** Combina linealmente las columnas para generar **componentes** no correlacionados entre sí, ordenados de mayor a menor variabilidad. En regresión se espera correlación entre Y y las X, pero no entre las X (multicolinealidad); si varias X están correlacionadas, PCA las reemplaza por un nuevo componente que entra al modelo.

**Requisitos y pasos:**

1. **Solo variables numéricas** (las 0/1 pueden incluirse, con cuidado).
2. **Verificar que procede:** prueba de **esfericidad de Bartlett**. H₀: la matriz de correlaciones es la identidad (todas las correlaciones = 0). Si `p-value < 0.05` se rechaza H₀ → tiene sentido reducir. Si `p > 0.05`, no se recomienda PCA. Complementar mirando el **mapa de calor de correlaciones**, siempre con el rango completo de color (−1 a 1, centro 0) para que se interprete bien; eliminar antes las transformaciones redundantes de una misma variable.
3. **Estandarizar** (media 0, varianza 1): si no, las variables con rangos mayores (p. ej. millones vs. años) dominan.
4. Ajustar PCA. Con *n* observaciones y *p* variables se obtienen `min(n−1, p)` componentes.

**Resultados:**

- **Autovectores / cargas (*loadings*):** peso de cada variable en cada componente; dan la **dirección**. Cada componente contiene "un pedacito de todas" las variables.
- **Autovalores / varianza explicada:** variabilidad de cada componente (matriz de varianzas y covarianzas). La suma de la variabilidad original = suma de la final. Se interpretan como **proporción** de la variabilidad total y **proporción acumulada** (sin unidades).
- **Scores (puntajes):** nuevas coordenadas de cada observación en los componentes: combinación lineal de los valores estandarizados con las cargas. Sirven para graficar (p. ej. PC1 vs PC2 coloreando por la variable objetivo).

**¿Cuántos componentes?**

- **Gráfico de codo / sedimentación:** punto de inflexión. Si no hay codo, PCA no aporta.
- **Varianza acumulada:** fijar un umbral (p. ej. aceptar perder ~15–20 %; en el ejemplo se usó 80 %).
- Los componentes ya vienen ordenados: el corte se hace tomando los primeros.
- Si el PC1 explica poca varianza (p. ej. 18 %) y KMO/correlaciones son bajos, los datos no están muy correlacionados y PCA es poco útil.

**Usos:** acelerar modelos complejos, quitar multicolinealidad y **visualizar** (graficar clusters/clases con PC1–PC2 aunque el modelo se haya entrenado con todas las variables).

**Output:** archivo de datos con las "p" componentes principales (quitar las variables originales que las generaron).

### 6.2 EFA – Análisis Factorial Exploratorio

**Idea.** Existen **variables latentes** (no observables, típicas de las ciencias sociales; p. ej. la inteligencia de Spearman, 1904) que mantienen cohesionadas a las variables observadas. El sentido es **inverso** al PCA: cada **variable observada** contiene un pedazo de cada factor, mientras que en PCA cada componente contiene un pedazo de cada variable.

**PCA vs. EFA (analogía de Milli Vanilli):** el PCA es la versión simplificada/generalizada ("fake") que se popularizó; el EFA es el original. Usar **PCA** cuando el objetivo es puramente matemático (reducir dimensiones/tiempo de cómputo, sin interpretar). Usar **EFA** cuando se busca una reducción **interpretable** y darle **nombre** a los factores.

| | PCA | EFA |
|---|---|---|
| Número de componentes/factores | Lo entrega el método (*min(n−1, p)*) | Hay que **indicarlo** antes de entrenar (gráfico de sedimentación) |
| Sentido | Componente = combinación de variables | Variable = combinación de factores latentes |
| Interpretación | No interpretable (puramente matemático) | Interpretable, factores nombrables |

**Pasos del EFA:**

1. **Adecuación muestral:** Bartlett (como en PCA) y **KMO** (Kaiser-Meyer-Olkin). Se desea KMO **≥ 0.5–0.6**; un KMO bajo (p. ej. 0.23) indica que el análisis resumirá poco de la variabilidad. También hay un KMO por variable (para decidir cuáles entran).
2. **Extracción de factores:** el "EFA real" usa **máxima verosimilitud**; el "EFA vía PCA" es la versión simplificada.
3. **Número de factores:** gráfico de sedimentación, **autovalores > 1** (criterio de Kaiser) y/o varianza explicada acumulada.
4. **Rotación** (p. ej. **Varimax**): busca el mejor "punto de observación" para que cada variable cargue en un solo factor. *No manipula los datos*; se rota el ángulo de observación, como al rodear una escultura.
5. **Etiquetado:** conceptualizar y nombrar cada factor según las variables que más cargan en él (mirar valores absolutos; asignar cada variable al factor donde carga más).
6. **Puntuaciones factoriales** (*factor scores*) para usar los factores en los siguientes pasos.

**Comunalidades:** proporción de la varianza de **cada variable** explicada por los factores retenidos (debe estar entre 0 y 1; un valor > 1 es un síntoma de mal ajuste, p. ej. por KMO bajo). Además se reporta la varianza explicada por cada factor.

**Cargas ideales:** contrastes marcados (valor alto en un factor y bajo en el otro).

---

## 7. Steps 5 y 6 – Data Mining task y algoritmos

### 7.1 Step 5: elegir la tarea (matching con el Step 1)

| Enfoque | Definición | Técnicas |
|---|---|---|
| **Predictivo** | Usa variables del conjunto de datos para predecir valores desconocidos o futuros de una variable de interés | Clasificación, regresión, *classifier ensemble* (los ensambles sirven para clasificación y regresión) |
| **Descriptivo** | Cuantifica relaciones entre los datos analizando eventos pasados para obtener información sobre cómo abordar eventos futuros | Reglas de asociación, **clustering**, detección de anomalías, *rough sets* |
| **Optimización** | Encuentra alternativas de mayor rendimiento/rentabilidad **bajo restricciones**, maximizando factores deseados y minimizando los no deseados | Enfoques heurísticos y meta-heurísticos (basados en enjambre, trayectoria, evolutivos/genéticos) |

Notas: no todo problema se resuelve con modelos predictivos o descriptivos; a veces el problema es de **optimización** (ej.: asignar fiscalizadores a contribuyentes riesgosos con restricciones de tiempo, dieta de menor costo para un establo). Optimización no se desarrolla en el curso, pero coexiste con las otras dos ramas.

**Supervisado vs. no supervisado:**

- **Supervisado:** hay variable objetivo Y (clasificación, regresión).
- **No supervisado:** sin Y; se buscan patrones (clustering, reducción de dimensiones, reglas de asociación).
- Otros: aprendizaje por refuerzo (agentes, recompensas), semi-supervisado, transfer learning, etc.

### 7.2 Step 6: elegir el algoritmo

- Elegir según **objetivo**, **tipo de variable** (numéricas, categóricas, mixtas), **input** y **output** (Y numérica → regresión; Y categórica → clasificación).
- Recomendación del curso: **mínimo 3 algoritmos** y, dentro de cada uno, varios escenarios (hiperparámetros) para compararlos.
- Definir nosotros el tipo de variable en lugar de confiar en que el algoritmo lo identifique solo.

---

## 8. Step 7a – Clustering (Análisis de Conglomerados)

### 8.1 Objetivo y principio

Agrupar observaciones de modo que los grupos sean **homogéneos internamente y heterogéneos entre sí** (minimizar la distancia dentro del grupo, maximizarla entre grupos). Lo contrario (heterogéneos internamente y homogéneos externamente) es un tipo de muestreo, no clustering.

Como todo se basa en distancias, **hay que estandarizar/transformar** las variables para quitar unidades de medida.

### 8.2 Distancias

| Distancia | Idea |
|---|---|
| **Euclidiana** | Línea recta; raíz de la suma de distancias al cuadrado |
| **Manhattan** | Por bloques (como calles de una ciudad) |
| **Minkowski** | Generalización con parámetro *p* (p=1 Manhattan, p=2 Euclidiana) |
| **Chebyshev** | Caso límite p → ∞ (máxima diferencia) |
| **Canberra** | Variante ponderada relativa |
| **Gower** | Sirve para **variables mixtas/nominales** |

También existe la distancia **multivariada** (p. ej. Mahalanobis), útil para detectar atípicos multivariados.

### 8.3 Elección del número de clusters

Es **subjetiva** salvo que se usen métodos estadísticos (análisis de clases latentes) o criterios de negocio/literatura (en estudios de mercado suelen usarse 3–10 segmentos). Consideraciones: que cada cluster tenga suficientes observaciones; el tipo de distancia depende del nicho (psicología, ciencias administrativas, etc.).

### 8.4 Métodos jerárquicos

- Producen un **dendograma** (árbol): las observaciones cercanas se unen primero. Se interpreta con **cortes** horizontales: donde se corta, cada rama que se abre es un cluster. Da flexibilidad para elegir más o menos granularidad sin reentrenar.
- Útil para **respetar jerarquías** existentes (biología: reinos, árboles filogenéticos) y para **detectar atípicos** (un cluster de una sola observación en la primera partición = muy diferente de forma multivariada).
- Requiere la **matriz de distancias**.

| Algoritmo | Tipo | Idea |
|---|---|---|
| **AGNES** (*Agglomerative Nesting*) | Aglomerativo (de abajo hacia arriba) | Cada objeto es un cluster; se unen los más próximos repetidamente |
| **DIANA** (*Divisive Analysis*) | Divisivo (de arriba hacia abajo) | Un solo grupo grande que se va dividiendo |

Ambos usan un coeficiente para saber cuándo detenerse (aglomeración/división). Método de enlace mencionado: **Ward**.

### 8.5 Métodos no jerárquicos (de partición)

Suelen requerir fijar de antemano el número de clusters *k*. Métrica: **suma de distancias al cuadrado dentro de cada cluster**.

| Algoritmo | Centro | Características |
|---|---|---|
| **K-medias (K-means)** | **Centroide** = vector de medias | Rápido y muy usado, pero **sensible a atípicos** y a la **elección inicial** de centroides (óptimo local) → entrenar con distintas inicializaciones |
| **PAM** (*Partitioning Around Medoids*) | **Medoide** (basado en la mediana) | **Robusto a atípicos**; necesita la matriz de disimilaridades completa (costoso en datos grandes) |
| **CLARA** (*Clustering Large Applications*) | Medoides | Aplica PAM sobre **submuestras/bloques** → pensado para conjuntos grandes |
| **FANNY** (*Fuzzy Analysis*) | Grados de pertenencia | **Lógica difusa**: cada observación puede pertenecer a **más de un** cluster (probabilidades); K-means, PAM y CLARA asignan a uno solo |

**Algoritmo K-means:**

1. Elegir *k* centroides iniciales (aleatorios).
2. Asignar cada punto al centroide más cercano.
3. Recalcular cada centroide como el vector de medias del grupo.
4. Repetir 2–3 hasta convergencia o criterio de parada (p. ej. cambios/distancias cuadráticas menores a un umbral, o máximo de iteraciones).

### 8.6 Cómo elegir *k*: codo y silueta

- **Gráfico de codo (inercia):** la **inercia** es la distancia cuadrática media entre cada observación y su centroide más cercano; se busca el punto de inflexión (menor es mejor, pero siempre baja al aumentar *k*).
- **Silueta:** toma valores de −1 a 1; se busca el **mayor**. **(complemento)** `s(i) = (b − a) / max(a, b)`, con *a* la distancia media al propio cluster y *b* la distancia media al cluster vecino más cercano.
  - Se mira la **silueta global** (línea punteada), la **silueta por cluster** y su ancho.
  - Criterios: anchos/tamaños de cluster **homogéneos**, **pocos valores negativos** (posible mala asignación) y **silueta promedio más alta**.
  - Ejemplo del docente: k=2 con silueta global ≈ 0.4 (mejor) vs. k=3 < 0.3; aun así se puede preferir k=3 si el negocio necesita tres segmentos.
  - Codo y silueta son **herramientas complementarias** y a veces poco concluyentes.
- **Búsqueda de hiperparámetros:** `GridSearchCV` (número de clusters, iteraciones máximas, inicializaciones). Reducir el vector de valores si demora demasiado.

### 8.7 Cierre del paso y datos mixtos

1. Entrenar el modelo con el *k* elegido y asignar la **etiqueta de cluster** a cada observación.
2. **Describir cada cluster** con gráficos y métricas descriptivas (perfil de variables por cluster).
3. Para graficar, se puede usar **PCA solo con fines de visualización** (PC1–PC2), sin cambiar el modelo.
4. Con variables **mixtas** (numéricas + nominales/ordinales), K-means no basta: se usan modelos inclusivos como **K-Prototypes** (`kmodes`), previsto para la siguiente clase.

---

## 9. Steps 8 y 9 – Interpretación y consolidación

- **Paso 8 (interpretación):** en bucle con el paso 7. Se interpreta internamente (métricas, gráficos, perfiles) antes de exponerlo al negocio; puede regresar a cualquier paso. La Unidad 5 del sílabo cubre visualización (análisis exploratorio, técnicas y herramientas) y las presentaciones grupales del proyecto final.
- **Paso 9 (consolidación):** documentar y reportar en términos del negocio, con interpretación numérica en el lenguaje del caso o institución.

---

## 10. Herramientas de Python usadas en el curso

```python
# Step 2 – entendimiento
import pandas as pd, numpy as np, seaborn as sns, matplotlib.pyplot as plt
import pyreadstat                       # lectura de archivos .sav (SPSS)

# Step 3 – limpieza / imputación
df.duplicated(subset=['ID', 'fecha'])
from sklearn.impute import SimpleImputer, KNNImputer
from sklearn.experimental import enable_iterative_imputer
from sklearn.impute import IterativeImputer

# Step 4a – transformaciones
from sklearn.preprocessing import StandardScaler, RobustScaler, MinMaxScaler

# Step 4b – reducción de dimensiones
from sklearn.decomposition import PCA
from factor_analyzer import FactorAnalyzer
from factor_analyzer.factor_analyzer import calculate_kmo, calculate_bartlett_sphericity

# Step 7a – clustering
from sklearn.cluster import KMeans
from sklearn.metrics import silhouette_score, silhouette_samples
from sklearn.model_selection import GridSearchCV
from kmodes.kprototypes import KPrototypes   # datos mixtos
```

---

## 11. Checklist rápido de decisiones

- **¿Media o mediana?** Distribución simétrica → media + desviación estándar; asimétrica/con atípicos → mediana + RIC.
- **¿Cómo detectar atípicos?** Simétrica → Z-score (±3 s); asimétrica → cajas (1.5·RIC).
- **¿Qué hacer con vacíos?** Identificar mecanismo (MCAR/MAR/MNAR) → imputar según corresponda y comparar antes/después; tope de ~15–20 %.
- **¿Qué escala usar?** Rango fijo [0,1] → Min-Max; centrado y comparable → Z; atípicos → robusta; no aplicar de forma masiva sin analizar.
- **¿Reducir dimensiones?** Verificar Bartlett (y KMO si es EFA). Sin interpretación → PCA; con interpretación → EFA.
- **¿Qué tarea?** Predecir (supervisado), describir (no supervisado) u optimizar; luego elegir ≥ 3 algoritmos.
- **¿Clustering?** Estandarizar, elegir distancia adecuada, decidir *k* con codo + silueta + criterio de negocio, describir cada cluster.

---

## 12. Glosario

| Término | Significado |
|---|---|
| KDD | Knowledge Discovery in Databases |
| Target data set | Conjunto de datos seleccionado para el análisis |
| MCAR / MAR / MNAR | Mecanismos de datos faltantes |
| RIC / IQR | Rango intercuartil (Q3 − Q1) |
| Capping | Reemplazar atípicos por valores límite |
| PCA | Análisis de Componentes Principales |
| EFA | Análisis Factorial Exploratorio |
| KMO | Kaiser-Meyer-Olkin, adecuación muestral |
| Comunalidad | Varianza de una variable explicada por los factores |
| Centroide / Medoide | Centro de cluster basado en media / mediana |
| AGNES / DIANA | Jerárquicos aglomerativo / divisivo |
| PAM / CLARA / FANNY | Particionales: medoides / para datos grandes / difuso |

---

### Pendiente por cubrir (sin material aún en el repositorio)

Semanas 7 en adelante: modelos supervisados (clasificación y regresión), reglas de asociación y patrones secuenciales, evaluación de modelos, visualización e interpretación de resultados, y el trabajo con datos no estructurados (texto/imágenes).
