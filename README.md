# Modelo predictivo de fuga Colombina

En este repositorio se realiza un modelo predictivo de fuga de clientes desde la modificación y la depuración de los datos. El objetivo es predecir los clientes que tienen mayor probabilidad de no volver a comprar ninguno de los productos. Colombina ha establecido que un cliente que no compra durante los últimos dos meses es un cliente fugado.

Para la generación del modelo se crearon las variables:

- recencia: La cual cuenta los días transcurridos desde la ultima fecha de compra hasta 16 de julio del 2022.
- monto: Es el promedio del valor neto en dinero de cada cliente.
- Frecuencia: cuantas veces ha comprado el cliente por Fecha. (se cuenta en cuantas fechas distintas ha comprado cada cliente).
- longitud: fecha max - fecha minima de cada cliente
- periodicidad: Es la desviación estándar de la diferencia de tiempos de compra de cada cliente. Se toma la cantidad de días que han pasado entre cada fecha y a estos se les calcula la desviación estándar.
- portafolio: Se cuenta la cantidad de productos (Material) que ha comprado cada cliente.

Con base a la variable recencia se calcula la variable de respuesta 'fugados', la cual es 1, si los clientes llevan más de 60 días sin comprar y 0 en caso contrario.

Entonces para el modelo se tiene:
y = fugados
x = monto, frecuencia, longitud, periodicidad y portafolio.

Analizando la variable de respuesta, se encontró que esta desbalanceada. El 13% de los datos son clientes fugados.

<table style="display:flex;justify-content:center">
  <tr>
    <th>Cliente</th>
    <th>Cantidad</th>
    <th>Porcentaje</th>
  </tr>
  <tr>
    <td>Fugados</td>
    <td>10,663</td>
    <td>13%</td>
  </tr>
  <tr>
    <td>No fugaods</td>
    <td>69,631</td>
    <td>87%</td>
  </tr>
</table>

Por ende se aplico el método SMOTE para datos desbalanceados. COn el fin de que se amplie la cantidad de datos de clientes fugados.

# Generacion del modelo de fuga

Para la generación del modelo predictivo de fuga, se prueban los siguientes métodos:
* Regresión logística 
* Random Forest
* KNN
* Support Vector Machine (SVM)
* Gaussian Naive Bayes (GNB)
* Xgboost

Para tener menor sesgos en las estimaciones se probó cada método con la validación cruzada kfold. 

Al ejecutar los métodos, el método Xgboost, es el que logra clasificar el modelo de mejor manera, ya que tanto el recall y la precisión son altos, ademas viendo las gráfica de las métricas de clasificación son mejores comparados con los demás modelos. En el tiempo de ajuste del estimador si es un poco más alto con respecto a los demás, sin embargo la diferencia no es tan grande. También se ejecuto el método SVM, sin embargo sus tiempos de ejecución eran muy altos y las métricas no eran muy buenas.

<div style="text-align:center">
  <img src="https://github.com/marcelamu9/modelo_predictivo_fuga_colombina/blob/main/img/boxplot_metricas_clasificacion.png" width="800" title="Métricas de clasificación">
  <img src="https://github.com/marcelamu9/modelo_predictivo_fuga_colombina/blob/main/img/boxplot_tiempos_modelos.png" width="800" title="Tiempos de modelos">
</div>

Al realizar las métricas en los datos de entrenamiento y prueba se encontró que las métricas de precisión y recall son muy buenas en los datos de entrenamiento, sin embargo la precisión no es tan buena en los datos de prueba, la idea en los futuros modelos será aumentar la precisión para identificar correctamente los clientes fugados.

Se realizó el gráfico para medir la importancia de las variables en el modelo, donde se tiene que la variable longitud es la más importante para el modelo y las otras variables tienen poco peso, así que es conveniente en una próximo modelo evaluar otras variables o descartar algunas de las variables ya incluidas.

<div style="text-align:center">
  <img src="https://github.com/marcelamu9/modelo_predictivo_fuga_colombina/blob/main/img/importancia_variables.png" width="800" title="importancia variables">
</div>
<br>


# Como ejecutar el proyecto

```
Después de clonar el proyecto ejecutar 
pip install -r requirements.txt
Esto instalara las librerias del proyecto
```
