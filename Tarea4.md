**Base de Batos y Tablas**

```sql
/*Crear la base de datos ENSU*/
CREATE DATABASE ENSU;

/*Usar la base de datos ENSU*/
USE ENSU;

/*Creando la tabla Encuesta*/
CREATE TABLE Encuesta(
    Id_Encuesta INT AUTO_INCREMENT PRIMARY KEY,
    Periodo_Encuesta VARCHAR(10) NOT NULL
);

/*Creando la tabla Encuestado*/
CREATE TABLE Encuestado(
    Id_Encuestado INT AUTO_INCREMENT PRIMARY KEY,
    Genero INT(2) NOT NULL,
    Edad INT(2) NOT NULL,
    Fecha_Nacimiento DATE NOT NULL,
    Ocupación VARCHAR(10) NOT NULL,
    Grado_Estudio VARCHAR(2) NOT NULL,
    Numero_Mudanza VARCHAR(2) NOT NULL
);

/*Creando la tabla Ubicacion*/
CREATE TABLE Ubicacion(
    Id_Ubicacion INT AUTO_INCREMENT PRIMARY KEY,
    Localidad VARCHAR(40) NOT NULL,
    Municipio VARCHAR(34) NOT NULL,
    Estado VARCHAR(31) NOT NULL
);

/*Creando la tabla Resultado*/
CREATE TABLE Resultado(
    Id_Resultado INT AUTO_INCREMENT PRIMARY KEY,
    Percepción_Seguridad_Pública INT(2) NOT NULL,
    Confianza_Administración_Pública VARCHAR(2) NOT NULL,
    Percepción_Inseguridad_Pública INT(2) NOT NULL,
    Percepción_Incivilidades_Entorno INT(2) NOT NULL
);
```

**Insertando Datos**