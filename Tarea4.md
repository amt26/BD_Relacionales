**Base de Datos, Tablas e Insertando de Datos**

```sql
/*Crear la base de datos ENSU*/
CREATE DATABASE ENSU;

/*Usar la base de datos ENSU*/
USE ENSU;

/*Creando la tabla Encuesta*/
CREATE TABLE Encuesta(
    Id_Encuesta INT AUTO_INCREMENT PRIMARY KEY,
    Id_Encuestado INT REFERENCES Encuestado (Id_Encuestado),
    Periodo_Encuesta VARCHAR(10) NOT NULL
);

/*Insertar datos: Encuesta*/
INSERT INTO Encuesta (Id_Encuesta,Id_Encuestado,Periodo_Encuesta) VALUES
(1,1,"01Jan2023"),
(2,2,"01Jan2023"),
(3,3,"01Jan2023"),
(4,4,"01Jan2023"),
(5,5,"01Jan2023");

/*Creando la tabla Encuestado*/
CREATE TABLE Encuestado(
    Id_Encuestado INT AUTO_INCREMENT PRIMARY KEY,
    Id_Ubicacion  INT REFERENCES Ubicacion (Id_Ubicacion),
    Genero INT(2) NOT NULL,
    Edad INT(2) NOT NULL,
    Fecha_Nacimiento DATE NOT NULL,
    Ocupacion INT(10) NOT NULL,
    Grado_Estudio INT(2) NOT NULL,
    Numero_Mudanza INT(2) NOT NULL
);

/*Insertar datos: Encuestado*/
INSERT INTO Encuestado (Id_Encuestado,Id_Ubicacion,Genero,Edad,Fecha_Nacimiento,Ocupacion,Grado_Estudio,Numero_Mudanza) VALUES
(1,1,1,23,'1999-10-26',2,8,1),
(2,2,2,25,'1998-04-26',2,8,1),
(3,3,2,59,'1964-01-27',2,2,3),
(4,4,1,21,'2000-11-14',2,8,1),
(5,5,2,20,'2003-05-11',2,8,1);

/*Creando la tabla Ubicacion*/
CREATE TABLE Ubicacion(
    Id_Ubicacion INT AUTO_INCREMENT PRIMARY KEY,
    Localidad VARCHAR(40) NOT NULL,
    Municipio VARCHAR(34) NOT NULL,
    Estado VARCHAR(31) NOT NULL
);

/*Insertar datos: Ubicacion*/
INSERT INTO Ubicacion (Id_Ubicacion,Localidad,Municipio,Estado) VALUES
(1,"Arboledas","Escobedo","Nuevo Leon"),
(2,"Azteca","Guadalupe","Nuevo Leon"),
(3,"Balcones del Norte","Apodaca","Nuevo Leon"),
(4,"Camino Real","Guadalupe","Nuevo Leon"),
(5,"Camino Real","Guadalupe","Nuevo Leon");

/*Creando la tabla Resultado*/
CREATE TABLE Resultado(
    Id_Resultado INT AUTO_INCREMENT PRIMARY KEY,
    Id_Encuesta INT REFERENCES Encuesta (Id_Encuesta),
    Percepcion_Seguridad_Publica INT(2) NOT NULL,
    Confianza_Administración_Publica INT(2) NOT NULL,
    Percepcion_Inseguridad_Publica INT(2) NOT NULL,
    Percepcion_Incivilidades_Entorno INT(2) NOT NULL
);

/*Insertar datos: Resultado*/
INSERT INTO Resultado (Id_Resultado,Id_Encuesta,Percepcion_Seguridad_Publica,Confianza_Administración_Publica,Percepcion_Inseguridad_Publica,Percepcion_Incivilidades_Entorno) VALUES
(1,1,2,3,1,2),
(2,2,2,3,2,2),
(3,3,3,4,2,1),
(4,4,1,2,2,2),
(5,5,1,3,1,2);
```