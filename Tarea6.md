## Uso de funciones

-----
**Frecuencia**

Para saber como se encuentra distribuida la variable **Genero** se utilizo la funcion **count()** para obtener la frecuencia de cuantos clientes son hombre y cuantos son mujeres.

```sql
/*Distribución de Genero*/
SELECT e.Genero, count(e.Genero) AS Frecuencia
FROM encuestado e
GROUP BY e.Genero
ORDER BY e.Genero;
```
Dandonos como resultado la siguiente tabla, donde el valor de 1 representa a los hombres y el valor de 2 las mujeres:

| Genero 	| Frecuencia    |
|---	|---	|
| 1 	| 497 	|
| 2 	| 503 	|

-------
**Mínimos, Máximos y Rango**

Para obtener la edad minima y maxima de los encuestados se utilizara las funciones **min()** y **max()**.

```sql
/*Minimo y Maximo*/
SELECT min(e.Edad) AS Edad_Min, max(e.Edad) AS Edad_Max, (max(e.Edad) - min(e.Edad)) AS Rango
FROM encuestado e;
```

Resultado de la consulta:

| Edad_Min 	| Edad_Max    | Rango    |
|---	|---	|---	|
| 18 	| 85 	| 67    |

----
**Cuartiles**

```sql
/*Creamos una tabla para agregar la variable Edad y el Número de Renglones*/
DROP TABLE IF EXISTS Cuartiles;
CREATE TABLE Cuartiles(
    NumRenglon INT AUTO_INCREMENT PRIMARY KEY,
    Edad INT(2)
);

/*Agregar la edad de la tabla Encuestado*/
INSERT INTO Cuartiles (Edad)
SELECT Edad
FROM encuestado  
ORDER BY Edad ASC;

/*Cuartil a elegir*/
SET @Cuartil = 0.75;

/* Calculo del Cuartil 3 */
SELECT Edad
FROM cuartiles c 
WHERE NumRenglon = (ROUND((@Cuartil) * ((SELECT count(*) FROM Encuestado e) - 1)));
```

Dando como resultado para el cuartil 3:

| Edad | 
|---	|
| 68 	|

----
**Moda**

Se para el estado de la ubicación de los encuestados.

```sql
/*Moda*/
SELECT e.Id_Ubicacion ,u.Estado, count(1) AS Frecuencia 
FROM encuestado e 
LEFT JOIN ubicacion u 
		ON e.Id_Ubicacion = u.Id_Ubicacion
GROUP BY e.Id_Ubicacion
ORDER BY Frecuencia DESC
LIMIT 1;
```

Dando como resultado el estado que tiene una mayor moda:

| Id_Ubicacion 	| Estado    | Frecuencia    |
|---	|---	|---	|
| 81 	| NUEVO LEON 	| 15    |

-----
**Dificultades**

Las dificultades para la tarea 6 fueron:

    1. Al intentar calcular la moda de los estados de la ubicación de los encuestados, tuve dificultad al momento de pensar y
    plasmar en codito una solución para este problema.

    2. Al realizar la tarea, dejé como ejercicio final el cálculo de los cuartiles ya que, igual que con la moda, tuve
    problemas el intentar plasmar lo que pensaba en código. Para resolver este ejercicio me vi con la necesidad de investigar
    en varios foros de internet para poder encontrar una forma óptima de realizar el ejercicio.

