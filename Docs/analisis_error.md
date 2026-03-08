
_**Análisis de Errores del Modelo de Detección de Objetos (AECO)**_


**_1. Resumen Ejecutivo del Desempeño_**
Tras el análisis de las métricas de validación y las matrices de confusión, se observa que el modelo es capaz de identificar elementos clave en obra, pero presenta retos específicos en la exhaustividad de la detección y en la discriminación de clases con características morfológicas similares.

**_2. Desglose de Errores Principales_**

_A. Predominancia de Falsos Negativos (FN)_
El error más crítico identificado es la tasa de Falsos Negativos, lo que significa que el modelo omite objetos presentes en la escena.

**Impacto:** El sistema no logra marcar elementos existentes, lo que podría derivar en reportes incompletos de avance de obra o inventario.

**Posibles Causas:** * Oclusiones: Elementos parcialmente cubiertos por andamios, maquinaria o personal de obra.

**Variabilidad de Iluminación:** Sombras densas o sobreexposición en tomas exteriores que difuminan los bordes de los objetos.

**Escala:** Dificultad para detectar objetos de dimensiones pequeñas en tomas de gran angular (vistas generales de la losa o fachada).

_B. Confusión de Clases (Errores de Clasificación)_
Se ha detectado que el modelo confunde ciertas categorías entre sí. Esto ocurre principalmente en elementos que comparten texturas o geometrías similares dentro del sector AECO.

**Ejemplos detectados:** Confusión entre tipos de tuberías (hidrosanitarias vs. eléctricas) o entre distintos tipos de herramental de encofrado.

**Causa:** Similitud visual en el set de datos de entrenamiento y falta de características distintivas claras en imágenes de baja resolución.

**_3. Matriz de Confusión y Métricas_**
A continuación, se describen las tendencias observadas en la matriz de salida:

**Precisión:** Relativamente alta (pocos Falsos Positivos), lo que indica que cuando el modelo detecta algo, suele ser correcto.

**Exhaustividad:** Baja, confirmando la tendencia de omitir etiquetas necesarias.

**_4. Plan de Acción y Mejoras_**
Para mitigar los errores actuales, se proponen las siguientes acciones en el próximo ciclo de entrenamiento:

**Aumento de Datos:** Aplicar técnicas de tiling (división de imágenes) para mejorar la detección de objetos pequeños y aumentar la exposición artificial para robustecer el modelo ante sombras.

**Refinamiento del Dataset:** Revisar el etiquetado en Roboflow para asegurar que no existan objetos sin marcar en el set de entrenamiento, lo cual alimenta directamente la generación de Falsos Negativos.

**Ajuste de Hiperparámetros:** Experimentar con un Confidence Threshold más bajo durante la inferencia para capturar más detecciones, evaluando el balance con la precisión.
