# Comandos y CRUD

- Mostrar las bases de datos

        $ show dbs

- Crear o Utilizar una base de datos
        
        $ use [nombre db]

Apesar de que cuando se crea una base de datos se ve con el comando show dbs, esta no se materializa hasta que tenga una coleccion con documentos.

- Visualizar que base de datos esta en uso

        $ db

- Crear una coleccion, al igual que crear una base
de datos primero debe tener un contenido , por lo que se materializa encuento se inserta un documento

## INSERT - Insertar Documentos

- Insertar un documento. Hay dos formas de hacerlo
    - Insertar un documento

            $ db.collection.insertOne({"campo":"valor"})

    - Insertar muchos documentos

            $ db.collection.insertMany(
            [ <document 1> , <document 2>, ... ])  
    

## SELECT - Consultas 

Puede encontrar toda la documentacion en https://docs.mongodb.com/manual/tutorial/query-documents/

- Select todos
``` javascript
// SELECT * FROM inventory
db.inventory.find( {} )

db.users.find( 
    {age:{$gt: 18}},  // Criterio de busqueda
    {name:1,address:1} // Proyeccion
).limit(5) // cursor modificador

/* la Proyeccion determina que campos se 
quiren mostrar.
Por defecto trae todos los campos
Para indicar que traiga los especificos se  debe usar el nombre del campo con valor 1
    {campo:1}

el _id simpre es retornado, para quie no sea asi el valor debe ser 0    
*/
```

- Select segun igualdad
``` javascript
// SELECT * FROM inventory WHERE status = "D"
db.inventory.find( { status: "D" } )
```

- Especificar Condicion usando operadores
``` javascript
// SELECT * FROM inventory WHERE status in ("A", "D")
db.inventory.find( { status: { $in: [ "A", "D" ] } } )
```

- Condicional AND
``` javascript
// SELECT * FROM inventory WHERE status = "A" AND qty < 30
db.inventory.find({status: "A", qty: { $lt: 30 }})
```

- Condicional OR
``` javascript
// SELECT * FROM inventory WHERE status = "A" OR qty < 30
db.inventory.find({$or: 
        [ { status: "A" }, 
          { qty: { $lt: 30 } } // $lt = less than - menor que
        ] 
        } )
```

- Usando AND y OR
``` javascript
// SELECT * FROM inventory WHERE status = "A" AND ( qty < 30 OR item LIKE "p%")
db.inventory.find( {
     status: "A",
     $or: [ { qty: { $lt: 30 } }, { item: /^p/ } ]
} )
```

- Buscar el primer documento, o el primero que cumpla con las condiciones
``` javascript
// SELECT TOP 1 * FROM inventory 
db.collection.findOne()
// O con condicion 
db.collection.findOne(query, projection)
```

## UPDATE - Actualizacion de documentos

- Actulizar un solo(primer) documento que cumpla con el filtro
``` javascript
// UPDATE table SET campo="valor"  WHERE [condicion]
db.collection.updateOne(filter, update, options)

 db.restaurant.updateOne(
      { "name" : "Central Perk Cafe" },
      { $set: { "violations" : 3 } }
   );
```

-  Actualizar multiples documentos dentro de una coleccion basado en un filtro
``` javascript
// Actuliza todos los documentos que cumplan con el filtro
db.restaurant.updateMany(
      { violations: { $gt: 4 } },
      { $set: { "Review" : true } }
   );
```

- Remplazar un documento dentro de una coleccion basado en un filtro.
``` javascript
db.collection.replaceOne(filter, replacement, options)

db.restaurant.replaceOne(
      { "name" : "Central Perk Cafe" },
      { "name" : "Central Pork Cafe", "Borough" : "Manhattan" }
   );
```

## DELETE - Borrado de documentos

- Borrar un solo (primer) documento que cumpla con un filtro
``` javascript
db.orders.deleteOne({"_id":ObjectId("563237a41a4d68582c2509da") } );
```

- Borrar todos los documentos que cumplan con un filtro
``` javascript
 db.orders.deleteMany(
       { "client" : "Crude Traders Inc." },
       { w : "majority", wtimeout : 100 }
   );
```