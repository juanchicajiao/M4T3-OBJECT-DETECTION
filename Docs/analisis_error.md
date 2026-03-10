
# _**Análisis de Errores del Modelo de Detección de Objetos (AECO)**_


## **_1. Resumen de Desempeño_**
Tras el análisis de las métricas de validación y las matrices de confusión, se observa que el modelo es capaz de identificar elementos clave en obra, pero presenta retos específicos en la exhaustividad de la detección y en la discriminación de clases con características morfológicas similares, y sobre todo una predominancia de los FN.

## **_2. Desglose de Errores Principales_**

_A. Predominancia de Falsos Negativos (FN)_
El error más crítico identificado es la tasa de Falsos Negativos, lo que significa que el modelo es "conservador" y omite objetos presentes en la escena, antes que presentar una etiqueta "mal" puesta.

**Impacto:** El sistema no logra marcar elementos existentes, lo que podría derivar en reportes incompletos de avance de obra o inventario.

**Oclusiones:** Elementos parcialmente cubiertos por andamios, maquinaria o personal de obra.

**Escala:** Dificultad para detectar objetos de dimensiones pequeñas en tomas de gran angular.

_B. Confusión de Clases (Errores de Clasificación)_
Se ha detectado que el modelo confunde ciertas categorías entre sí. Es decir marca un objeto pero con la etiqueta equivocada. 

**Ejemplos detectados:** Confusión entre vestimenta y chaleco, o entre una herramienta y un casco

**Causa:** Similitud visual en el set de datos de entrenamiento y falta de características distintivas claras en imágenes de baja resolución.

**Falsos Negativos:**

![FalsoNegativo1](https://github.com/user-attachments/assets/f0d6ef4b-8bb7-4a65-8f46-eb524739e97f)

1. Se identifica el casco pero no al obrero ni al chaleco claramente representados en la imagen

![FalsoNegativo2](https://github.com/user-attachments/assets/cb32f634-478a-4dc7-aaa0-541dc84ed999)

2. No se identifica al segundo obrero en esta imagen. Podría darse por una obstrucción en la figura completa de la persona.

![FalsoNegativo3](https://github.com/user-attachments/assets/bf2fcf6c-826d-43ac-9546-36afb51673df)

3. Se identifica al obrero pero no al chaleco y tampoco la ausencia del casco.

**Falsos Positivos:**

![FalsoPositivo1](https://github.com/user-attachments/assets/23d9891b-306d-4d81-ad8c-fa7280b8e008)

1. Se identifica un casco inexistente en la cabeza del obrero. Se puede originar en una falla de iluminación en esa zona.

![FalsoPositivo3](https://github.com/user-attachments/assets/fc12365a-ad82-4dd1-936e-6531528d1263)

2. En esta imagen se indetifican dos obreros y dos chalecos, cuando en realidad solamente hay un obrero y un chaleco.

![FalsoPositivo2](https://github.com/user-attachments/assets/c8b3c290-de26-4cc5-8c9f-155a85d48252)

3. Similar a la anterior, se identifican dos obreros sin una razón en específico ya que la figura no se interrumpe. 

## **_3. Matriz de Confusión y Métricas_**
A continuación, se describen las tendencias observadas en la matriz de salida:

**Precisión:** Media, en general lo marcado está bien aunque omite partes importantes. No realciona la aparición de una clase con otra como correlación, es decir, identifica el casco pero no al obrero quien lo usa. 

**Exhaustividad:** Baja, confirmando la tendencia de omitir etiquetas necesarias.

## **_4. Plan de Acción y Mejoras_**
Para mitigar los errores actuales, se proponen las siguientes acciones en el próximo ciclo de entrenamiento:

**Aumento de Datos:** Aplicar técnicas de tiling (división de imágenes) para mejorar la detección de objetos pequeños y aumentar la exposición artificial para robustecer el modelo ante variabilidad entre imágenes.

**Refinamiento del Dataset:** Revisar el etiquetado en Roboflow para asegurar que no existan objetos sin marcar en el set de entrenamiento, lo cual alimenta directamente la generación de Falsos Negativos.

**Ajuste de Hiperparámetros:** Experimentar con un Confidence Threshold más bajo durante la inferencia para capturar más detecciones, evaluando el balance con la precisión.
