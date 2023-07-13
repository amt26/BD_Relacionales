## Creación de Funciones
-----------

Para esta primera función elegí calcular la cantidad de elementos que puede tener un arreglo ya que, últimamente me veo en vuelto en la necesidad de estar realizando este cálculo en el ámbito laboral:

```sql
DROP FUNCTION IF EXISTS LargoArreglo;

CREATE FUNCTION LargoArreglo(arr VARCHAR(255))
RETURNS INT DETERMINISTIC
BEGIN
	DECLARE contador INT;
	DECLARE posicion INT;
	DECLARE longitud INT;

	SET contador = 0;
	SET posicion = 1;
	SET longitud = LENGTH(arr);
   
    WHILE posicion <= longitud DO
        IF SUBSTRING(arr, posicion, 1) = ',' THEN
            SET contador = contador + 1;
        END IF;
        SET posicion = posicion + 1;
    END WHILE;

    RETURN contador + 1;
END;
```

---------------------

Para la segunda función, decide crear una que me calcule la correlación de dos variables ya que, en la materia de métodos estadísticos estamos calculando la correlación entre variable utilizando el lenguaje de programación R:

```sql
DROP FUNCTION IF EXISTS CalculoCorrelacion;

CREATE FUNCTION Correlacion(Variable1 VARCHAR(255), Variable2 VARCHAR(255), Base VARCHAR(255))
RETURNS FLOAT
DETERMINISTIC
BEGIN
	DECLARE n INT;
    DECLARE sum_x FLOAT;
    DECLARE sum_y FLOAT;
    DECLARE sum_xy FLOAT;
    DECLARE sum_x2 FLOAT;
    DECLARE sum_y2 FLOAT;
    DECLARE correlacion FLOAT;
    
    SELECT COUNT(*) INTO n FROM Base;
    SELECT SUM(Variable1) INTO sum_x FROM Base;
    SELECT SUM(Variable2) INTO sum_y FROM Base;
    SELECT SUM(Variable1 * Variable2) INTO sum_xy FROM Base;
    SELECT SUM(Variable1 * Variable1) INTO sum_x2 FROM Base;
    SELECT SUM(Variable2 * Variable2) INTO sum_y2 FROM Base;
    
    SET correlacion = (n * sum_xy - sum_x * sum_y) / SQRT((n * sum_x2 - sum_x * sum_x) * (n * sum_y2 - sum_y * sum_y));
    
    RETURN correlacion;
END;
```
