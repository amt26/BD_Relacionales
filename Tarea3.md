**Modelo Relacional**

1. Encuesta(Id_Encuesta,Id_Encuestado,Id_Ubicación,Periodo_Encuesta)
2. Encuestado(Id_Encuestado,Id_Ubicación,Género,Edad,Fecha_Nacimiento,Ocupación,Grado_Estudio,Número_Mudanza)
3. Ubicación(Id_Ubicación,Localidad,Municipio,Estado)
4. Resultado(Id_Resultado,Id_Encuesta,Id_Encuestado,Percepción_Seguridad_Pública,Confianza_Administración_Pública,Percepción_Inseguridad_Pública,Percepción_Incivilidades_Entorno)

**Diagrama Relacional**
```mermaid
erDiagram
    Encuesta {
        Texto Id_Encuesta
        Texto Id_Encuestado
        Texto Id_Ubicacion
        Texto Periodo_Encuesta
    }

    Encuestado {
        Texto Id_Encuestado
        Texto Id_Ubicacion
        Numerico Genero
        Numerico Edad
        Fecha Fecha_Nacimiento
        Texto Ocupacion
        Texto Grado_Estudio
        Texto Numero_Mudanza
    }

    Ubicacion {
        Texto Id_Ubicacion
        Texto Localidad
        Texto Municipio
        Texto Estado
    }

    Resultado {
        Texto Id_Resultado
        Texto Id_Encuesta
        Texto Id_Encuestado
        Numerico Percepcion_Seguridad_Publica
        Texto Confianza_Administracion_Publica
        Numerico Percepcion_Inseguridad_Publica
        Numerico Percepcion_Incivilidades_Entorno
    }

Encuesta ||--o{ Encuestado: Pertenece
Ubicacion ||--o{ Encuesta: Pertenece
Encuesta ||--o{ Resultado: Pertenece
Encuestado ||--o{ Resultado: Pertenece
Ubicacion ||--o{ Encuestado: Pertenece
```

**Operadores Algebra Lineal**
1. Proyección: conocer la ocupación de los encuestados:

    $\prod_{Encuestado}$(Ocupacion)

2. Selección: extraer el id_encuestado para aquellos encuestados que tienen como sexo el valor de 1 (masculino):

     $\prod_{Id_Encuestado}$ ($\sigma_{Sexo = "1"}$(Encuestado))

3. Proyección: extraer el Id_encuesta de los encuestados cuya edad es menor a 27

     $\prod_{Encuesta.Id_Encuesta}$ ($\sigma_{Edad < 27}$(Encuestado))

4. Selección: extraer el resultado de la encuesta para un encuestado en especifico: 

     $\prod_{Id_Resultado}$ ($\sigma_{Id_Encuestado = "100071.026"}$(Resultado))