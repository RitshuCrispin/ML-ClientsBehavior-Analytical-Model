# ML Client's Behavior Analytical Model
Modelo ML de clasificación que analiza el comportamiento de clientes para recomendar un plan de servicio de telefonía. Para encontrar el mejor modelo se calcula la métrica de exactitud en diferentes hiper parámetros en los modelos de clasificación Decision Tree Classifier, Random Forest Classifier y Logistic Regression.

# Descripcion del proyecto <a id='project_description'></a>
La compañía móvil Megaline no está satisfecha al ver que muchos de sus clientes utilizan planes heredados. Quieren desarrollar un modelo que pueda analizar el comportamiento de los clientes y recomendar uno de los nuevos planes de Megaline: Smart o Ultra.

Tienes acceso a los datos de comportamiento de los suscriptores que ya se han cambiado a los planes nuevos (del proyecto del curso de Análisis estadístico de datos). Para esta tarea de clasificación debes crear un modelo que escoja el plan correcto. Como ya hiciste el paso de procesar los datos, puedes lanzarte directo a crear el modelo.

## Objetivo: <a id='objective'></a>

Desarrollar un modelo que pueda analizar el comportamiento de los clientes y recomendar uno de los nuevos planes de Megaline: Smart o Ultra. El modelo debe ser con la mayor *exactitud* posible. En este proyecto, el umbral de *exactitud* es 0.75. Usaremos el dataset para comprobar la *exactitud*.


## Conclusiones <a id='end'></a>
 
1. En la etapa de inicializacion del proyecto, se revisaron los datos entregados donde se observo que los datos se encontraban listos sin necesitar de algun tipo de procesamiento que realizar.
2. Seguidamente, se prepararon los datos identificando las variables: features y target. 
3. Luego de ello, se segmentaron los datos en diferentes conjuntos con 3 tamaños con el fin de tener 3 datasets: entrenamiento, validacion y prueba; la distribucion fue de 0.6, 0.2 y 0.2, respectivamente.
4. Se entrenaron y probaron 3 modelos de clasificacion para encontrar el modelo con la mayor exactitud posible, los resultados de las pruebas fueron los siguientes:
- Arboles de decision: 78.85% de exactitud.
- Bosques de aleatoriedad: 78.7% de exactitud.
- Regresion logistica: 69% de exactitud.
5. Finalmente, el modelo con mayor exactitud identificado fue: **Arboles de decision.**
