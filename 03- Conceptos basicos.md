# Conceptos basicos

## JSON 
Es un formato con amplia aceptacion por distintas razones

- Es rapido , ligero y flexible.

- Es compatible con practicamente todos los lenguajes y herramientas.

- Se utiliza para la comunicacion y el intercambio de datos modernos.

## BSON
MongoDB al final utiliza un data binario llamado <strong>BSON</strong>
que es la Serializacion binaria de la representacion de datos JSON.
Mas facil de transferir que los archivos de texto.
Ligero,eficiente y facil de recorrer.


## Modelo de datos basado en documentos 

``` json
{
    "_id" : ObjectId("5ad88534e3632e1a35a58d00"),
    "name" : {
        "first" : "Juan",
        "last" : "castillo"
    },
    "address" : [
        {
            "location" : "casa",
            "address" : {
                "street" : "adkjflkjflskj",
                "city" : "asdfsadfd"
            }
        },
        {...}
    ]
}
```

## Descripcion de los elementos 

- ObjectId: es el identificador unico que proporciona mongodb cuando no se le envia uno
explicitamente.  ejemplo : ObjectId("5ad88534e3632e1a35a58d00")
    - los 4 primeros bytes , Marca el tiempo de creacion
    - los 5 bytes siguientes  son un valor unitario
    - los 3 ultimos bytes son un contador autoincremental

- Documento : todo lo que este entre "{..}"

- Campo : "campo" : "valor"

- Matriz o Array : Todos los campos o documentos dentro de "[...]"


## Lenguajes soportados 

Estos son algunos de los lenguajes que tiene Drivers para mongodb

- C
- C++
- C#
- Java
- Php
- Ruby
- Javascript
- R
- Python
- Scala
- Go


## Frameworks soportados

Algunos de los frameworks que trabajan con mongodb 

- Nodejs
- Django
- Spark
- Spring
- ... Entre muchos otros


## Lenguaje de consultas en MongoDB
MongoDB tambien permite hacer consulta atraves del lenguaje que maneja
conocido como MQL (Mongo Query Languaje)


# Varios modelos de datos y funciones de consulta avanzadas 

Mongo permite generar diferentes modelos de datos atraves de las consultas 
tales como :

- Documentos JSON
- Tabular
- Clave-valor
- Texto
- Geoespacial
- Grafos

## Consultas avanzadas 
Tambien se pueden realizar consultas por :
- Puntos
- Rangos
- Datos geoespaciales
- Busqueda por facetas  (categorias)
- Agregaciones
- Sentencias JOIN
- Recorridos de grafos
- Operadores booleanos
