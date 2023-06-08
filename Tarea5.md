## Insertado de Datos
```sql
/*Crear la base de datos ENSU*/
DROP DATABASE IF EXISTS ENSU;
CREATE DATABASE ENSU;

/*Usar la base de datos ENSU*/
USE ENSU;

/*Creando la tabla Ubicacion*/
DROP TABLE	IF EXISTS Ubicacion;
CREATE TABLE Ubicacion(
    Id_Ubicacion INT AUTO_INCREMENT PRIMARY KEY,
    Localidad VARCHAR(40),
    Municipio VARCHAR(34),
    Estado VARCHAR(31)
);

/*Creando la tabla Encuestado*/
DROP TABLE	IF EXISTS Encuestado;
CREATE TABLE Encuestado(
    Id_Encuestado INT AUTO_INCREMENT PRIMARY KEY,
    Genero INT(2),
    Edad INT(2),
    Fecha_Nacimiento DATE,
    Ocupacion VARCHAR(10),
    Grado_Estudio VARCHAR(2),
    Numero_Mudanza VARCHAR(2),
    Id_Ubicacion  INT REFERENCES Ubicacion (Id_Ubicacion)
);

/*Creando la tabla Encuesta*/
DROP TABLE	IF EXISTS Encuesta;
CREATE TABLE Encuesta(
    Id_Encuesta INT AUTO_INCREMENT PRIMARY KEY,
    Periodo_Encuesta VARCHAR(10),
	Id_Encuestado INT REFERENCES Encuestado (Id_Encuestado)
);

/*Creando la tabla Resultado*/
DROP TABLE	IF EXISTS Resultado;
CREATE TABLE Resultado(
    Id_Resultado INT AUTO_INCREMENT PRIMARY KEY,
    Percepcion_Seguridad_Publica INT(2),
    Confianza_Administración_Publica VARCHAR(2),
    Percepcion_Inseguridad_Publica INT(2),
    Percepcion_Incivilidades_Entorno INT(2),
    Id_Encuesta INT REFERENCES Encuesta (Id_Encuesta)
);

/*Insertar datos: Ubicacion*/
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Ubicacion.csv'
	INTO TABLE Ubicacion
	FIELDS TERMINATED BY ',' ENCLOSED BY '"'
	LINES TERMINATED BY '\n'
	IGNORE 1 LINES
	(Id_Ubicacion,Localidad,Municipio,Estado);

/*Insertar datos: Encuestado*/
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Encuestado.csv'
	INTO TABLE Encuestado
	FIELDS TERMINATED BY ',' ENCLOSED BY '"'
	LINES TERMINATED BY '\n'
	IGNORE 1 LINES
	(Id_Encuestado,Genero,Edad,Fecha_Nacimiento,Ocupacion,Grado_Estudio,Numero_Mudanza,Id_Ubicacion);

/*Insertar datos: Encuesta*/
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Encuesta.csv'
	INTO TABLE Encuesta
	FIELDS TERMINATED BY ',' ENCLOSED BY '"'
	LINES TERMINATED BY '\n'
	IGNORE 1 LINES
	(Id_Encuesta,Id_Encuestado,Periodo_Encuesta);

/*Insertar datos: Resultado*/
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Resultado.csv'
	INTO TABLE Resultado
	FIELDS TERMINATED BY ',' ENCLOSED BY '"'
	LINES TERMINATED BY '\n'
	IGNORE 1 LINES
	(Id_Resultado,Percepcion_Seguridad_Publica,Confianza_Administración_Publica,Percepcion_Inseguridad_Publica,Percepcion_Incivilidades_Entorno,Id_Encuesta);
```

## Dificultades

    1. Al tratar de conectarme a MySQL desde el Símbolo del Sistema (CMD) para poder realizar la inserción de datos, se me
    complica el lograr entender como puedo realizar esto desde el CMD, para solucionar esto decidí insertar los datos
    utilizando la sentencia "LOAD DATA INFILE".

    2. Al intentar importar archivos con la sentencia "LOAD DATA INFILE" me marcaba un error que hace referencia a que MySQL
    está configurado con la opción "--secure-file-priv" habilitada. Así que para solucionar esto tuve que mover los archivos a
    la ubicación obtenida con el siguiente código: "SHOW VARIABLES LIKE 'secure_file_priv';"

## Autoevaluación
A pesar de tener dificultades para entender el uso de CMD para lograr hacer sentencias de MySQL logre utilizar otro camino para poder dar una solución al problema planteado. Solo queda seguir practicando el uso del CMD por ello, considero que merezco una calificación 8.5/10.0.