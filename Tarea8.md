## Creación de vistas
-----------

Esta primera vista nos puede servir para consultar información sobre las características inherentes del encuestado y ver a que encuesta está asociado. Esta vista nos ayuda a tener una mayor rapidez al momento de querer consultar información puntual de los encuestados.

```sql
DROP VIEW IF EXISTS InformacionEncuestado;

CREATE VIEW InformacionEncuestado AS
SELECT e.Id_Encuestado,e.Id_Encuesta,en.Genero,en.Edad,en.Fecha_Nacimiento,en.Ocupacion,en.Grado_Estudio,en.Numero_Mudanza,en.Id_Ubicacion,u.Localidad,u.Municipio,u.Estado
FROM encuesta e 
LEFT JOIN encuestado en
	ON e.Id_Encuestado = en.Id_Encuestado
INNER JOIN ubicacion u
	ON en.Id_Ubicacion = u.Id_Ubicacion
```

----

Para esta vista, se decidió conjuntar la información a nivel encuesta trayendo así el resultado y la ubicación en la cual se realizó. Esta vista nos puede ayudar a obtener información general de los resultados por estado.

```sql
DROP VIEW IF EXISTS ResultadoPorEncuesta;

CREATE VIEW ResultadoPorEncuesta AS
SELECT e.Id_Encuesta, en.Id_Ubicacion,u.Localidad,u.Municipio,u.Estado,r.Percepcion_Seguridad_Publica,r.Confianza_Administración_Publica,r.Percepcion_Inseguridad_Publica,r.Percepcion_Incivilidades_Entorno
FROM encuesta e 
LEFT JOIN encuestado en
	ON e.Id_Encuestado = en.Id_Encuestado
RIGHT JOIN ubicacion u
	ON en.Id_Ubicacion = u.Id_Ubicacion
INNER JOIN resultado r
	ON e.Id_Encuesta = r.Id_Encuesta
```

---------------
## TRIGGER

El siguiente trigger nos permite mantener una vista actualizada cada vez que se agreguen encuestados a la base. Esta vista nos proporciona de manera resumida cuantos encuestados hay por estado.

```sql
CREATE TRIGGER calcular_encuestas_estado
AFTER INSERT ON encuestado
FOR EACH ROW
BEGIN	
	CREATE OR REPLACE VIEW Edo_encuestas AS
	SELECT u.Estado, count(e.Id_Encuestado) AS Total_Encuestas 
	FROM encuestado e 
	LEFT JOIN ubicacion u
		ON e.Id_Ubicacion = u.Id_Ubicacion
	GROUP BY u.Estado
	ORDER BY Total_Encuestas DESC
END;
```