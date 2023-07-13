## Conexión de R con MySQL

Para poder realizar la conexión de R con MySQL primero tenemos que instalar una paqueteria llamada "RMySQL":

```R
#Instalar el paquete RMySQL para realizar la conexión con R
install.packages("RMySQL")
library(RMySQL)
```

En esta libreria se encuentra una funcion cuyo nombre es "dbConnect" de la cual, nos pide que pongamos nuestro usuario, contraseña, nombre de la base de datos y el host. Para mayor facilidad, esta conexión se le asigna a una variable para futuras operaciones:

```R
# La funcion dbConnect nos permite realizar la conexión con MySQL
conexion <- dbConnect(MySQL(),
                      user = "root",
                      password = "",
                      dbname = "ensu",
                      host = "localhost")
```

Si quieremos validar que tablas son las que se encuentran en nuestra base de datos tenemos que usar la funcion "dbListTables" poniendo como unico parametro la conexión que se realizo en el paso anterior. Para poder extraer la información de una tabla tenemos que agregar la conexión y el nombre de la tabla entre comillas:

```R
#dbListTables nos permite ver los nombres de las tablas de nuestra BD
dbListTables(conexion)

#Para extraer el nombre de la tabla que ocupamos, se necesita poner entre "" el nombre de esta
encuestado <- dbReadTable(conexion, "encuestado")
resultado <- dbReadTable(conexion, "resultado")
encuesta <- dbReadTable(conexion, "encuesta")
ubicacion <- dbReadTable(conexion, "ubicacion")
```

Para el apartado de consultas relevantes, se me hizo de suma importancia obtener la correlacion entre variables, para ello, utilice la funcion corrplot para graficar y la funcion cor para obtener la matriz de correlación:

```R
#Consultas Relevantes
#Calcular la correlación entre variables
library(corrplot)

#Tenemos que asegurarnos que las variables sean de tipo numerico
encuestado$Ocupacion <- as.numeric(encuestado$Ocupacion) 
encuestado$Grado_Estudio <- as.numeric(encuestado$Grado_Estudio)
encuestado$Numero_Mudanza <- as.numeric(encuestado$Numero_Mudanza)

#Graficar la matriz de correlacion 
corrplot(cor(encuestado[!names(encuestado) %in% c("Id_Encuestado","Fecha_Nacimiento","Id_Ubicacion")]),
         method = "number",
         type = "full",
         title = "Matriz de Correlación para Encuestado",
         tl.pos = "n", mar = c(2, 1, 3, 1),
         col = colorRampPalette(c("white", "black"))(100))
```

![Grafico de Correlación](C:\Users\tmoli\OneDrive\Documentos\Angel\Maestria\Materias\2. Bases de datos\COR_Tarea10.jpeg)


En el paso de operaciones de agregación, me di la tarea de crear un ciclo que me de una tabla con los valores de estas operaciones y me grafique el histograma y el boxplot de estos datos. Este ciclo se alimenta de una variable macro que como datos, tomara todas aquellas variables a las cuales se le desee obtener este analisis. 

Para este ejercicio se realizo solo para la variable "Edad" pero en el dado caso que se hubiera querido obtener el analisis para tres variables, el unico cambio que se tendria que realizar es; en los parametros solicitados por el for, en la lista, se tendria que agregar las demas variables por ejemplo: ``` for (variable in c("Edad","Ocupacion","Numero_Mudanza"))```.

```R
# Operaciones de Agregacion
# El siguiente ciclo creara una tabla llamada Analisis_Variable en la cual, contendra difetentes
# operaciones de agregacion.
# Tambien graficara el histograma y el boxplot de esta variable
# Nota: para querer mas de una tabla de analisis se le tiene que agregar al for el nombre
# de las variables que se ocupan, para este ejercicio se realizo solo para 1

for (variable in c("Edad")) {
  eval(parse(text = paste0("Analisis_",variable," <- data.frame(Variable = c(\"Maximo\",
                                         \"Minimo\",
                                         \"Rango\",
                                         \"Media\",
                                         \"Mediana\",
                                         \"Moda\",
                                         \"Q1\",
                                         \"Q2\",
                                         \"Q3\",
                                         \"Varianza\",
                                         \"Desviacion\",
                                         \"Coeficiente de Variación\"),
                            Dato = c(max(encuestado$",variable,"),
                                     min(encuestado$",variable,"),
                                     (max(encuestado$",variable,") - min(encuestado$",variable,")),
                                     mean(encuestado$",variable,"),
                                     median(sort(encuestado$",variable,")),
                                     names(table(encuestado$",variable,"))[table(encuestado$",variable,") == max(table(encuestado$",variable,"))],
                                     quantile(encuestado$",variable,", 0.25),
                                     quantile(encuestado$",variable,", 0.5),
                                     quantile(encuestado$",variable,", 0.75),
                                     round(var(encuestado$",variable,"),3),
                                     round(sqrt(var(encuestado$",variable,")),3),
                                     round(((sd(encuestado$",variable,") / mean(encuestado$",variable,")) * 100),3)))")))
  
  eval(parse(text = paste0("hist(encuestado$",variable,", breaks = \"FD\", main = \"Histograma de ",variable,"\", xlab = \"",variable,"\", ylab = \"Frecuencia\")")))
  eval(parse(text = paste0("boxplot(encuestado$",variable,", main = \"Boxplot de ",variable,"\", ylab = \"",variable,"\")")))
}
```


[def]: :\Users\tmoli\OneDrive\Documentos\Angel\Maestria\Materias\2. Bases de dato