# Base de Datos
La base de datos elegida pertenece a un estudio que realiza el INEGI llamado **Encuesta Nacional de Seguridad Pública Urbana (ENSU)**. El objetivo de este estudio es proporcionar información al público en general y proveer elementos para la toma de decisiones de política pública en materia de seguridad.

Esta base de datos cuenta con 3 archivos .csv:
    1. ENSU_CB_0323
    2. ENSU_VIV_0323
    3. ENSU_CS_0323

**ENSU_CB_0323**
Esta tabla contiene preguntas que están enfocadas a obtener información sobre la percepción de la población de 18 años y más sobre la situación de seguridad pública en el ámbito urbano. 

La tabla se compone por un total de 142 variables y 23,778 registros.

**ENSU_VIV_0323**
Aquí podemos encontrar las características generales de la vivienda, así como del hogar principal. Además, capta información sobre los datos del personal operativo y el resultado definitivo de la entrevista.

La tabla se compone por un total de 29 variables y 23,778 registros.

**ENSU_CS_0323**
Contiene información sobre las principales características sociodemográficas de la población residente del hogar principal e identifica a la población de 18 años y más, a esta población se le aplican las preguntas del cuestionario principal de la ENSU.

La tabla se compone por un total de 41 variables y 75,759 registros.

**Identificadores y periodo de tiempo**
Las variables que se van a utilizar para realizar el cruce entre estas 3 tablas son:
    1. ID_VIV (Identificador de vivienda seleccionada): número de identificación único de cada vivienda seleccionada para la encuesta.
    2. ID_PER (Identificador del informante seleccionado): Clave de identificación único de cada informante seleccionado para la encuesta.

Estados dos variables son de tipo character.

El periodo de tiempo el cual se compone esta encuesta es de enero 2023 a marzo del 2023.

# Sistema de gestión de bases de datos (SGBD)
Se eligio el sistema de gestión de bases de datos **MySQL** porqué:
    1. Tiene una gran comunidad de usuarios, lo que significa que podemos encontrar una gran cantidad de recursos y documentación disponibles en línea.

    2. Es posible configurar y optimizar MySQL para manejar grandes cantidades de datos y usuarios concurrentes.
    
    3. Es compatible con una gran variedad de sistemas operativos y lenguajes de programación. Esto nos facilita el poder utilizarlo en una variedad de entornos y para diferentes aplicaciones.
    
    4. Tiene una seguridad sólidas que permiten proteger los datos almacenados en las bases de datos. Esto incluye autenticación de usuarios, encriptación de datos y auditoría de seguridad.
