## Revisión de Inconsistencias

-----
Antes de cargar la información a las tablas de la base de datos que estoy trabajando les realize una previa limpieza para asegurarme que no tuvieran alguna inconsistencia. De las 4 tablas que uso, en 3 de ellas no encontre alguna inconsistencia pero para la tabla **Encuestado** encontre personas que tienen una edad de **0**.

Para validar si mi variable **Edad** tiene valores vacios, 0 o edades mayores a 100 realice la siguiente consulta 

```sql
/*Validar si hay edades 0, vacias o mayores a 100*/
SELECT e.Edad, COUNT(*) AS Frecuencia
FROM encuestado e 
WHERE e.Edad = 0 OR e.Edad >= 100 OR e.Edad IS NULL
GROUP BY e.Edad;
```

Dandome como resultado la siguiente tabla:

| Edad 	| Frecuencia |
|---	|---	|
| 0	    |  6 	|

Una vez identificado el problema en la variable **Edad** lo siguiente es calcular la edad utilizando la fecha de nacimiento y el día de hoy:

```sql
/*Calcular la edad para clientes que tienen edad 0*/
UPDATE encuestado
SET Edad = DATEDIFF(CURDATE(), fecha_nacimiento) / 365.25
WHERE edad = 0;
```