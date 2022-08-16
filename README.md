# Databases-Mongodb-Queries
Dada una base de datos (restaurantes.json) hago una serie de búsquedas posibles:

1. Consulta para mostrar todos los documentos en la colección restaurantes:

>> db.restaurantes.find()

2. Consulta para mostrar el restaurante_id, name, borough y cuisine de la colección restaurantes:

>> db.restaurantes.find( {}, {restaurant_id:1, name:1, borough:1, cuisine:1}).pretty()

*.pretty() es para que se muestre bonito por el shell, no es necesario

3. Lo mismo de antes pero sin mostrar _id:

>> db.restaurantes.find( {}, {restaurant_id:1, name:1, borough:1, cuisine:1, _id:0}).pretty()

4. Mostrar restaurante_id, name, borough y zip code y no mostrar _id:

>> db.restaurantes.find({}, {restaurant_id:1, _id:0, name:1, borough:1, address:{zipcode:1}}).pretty()

*zipcode esta dentro del Array address

5. Mostrar restaurantes que están en el Bronx:

>> db.restaurantes.find({borough:"Bronx"}).pretty()

6. Los 5 primeros que están en el Bronx:

>> db.restaurantes.find({borough:"Bronx"}).pretty().limit(5)

7. Los siguienetes después de los 5 primeros:

>> db.restaurantes.find({borough:"Bronx"}).pretty().skip(5)

8. Restaurantes con un score mayor de 90:

>> db.restaurantes.find({ "grades.score": { $gt: 90 } })

9. Restaurantes con un score mayor de 80 pero menor de 100:

>> db.restaurantes.find({$and:[{"grades.score": { $gt: 80 }} ,{ "grades.score": {$lt: 100}}]})

10. Mostrar lista de restaurantes que se encuentran a una latitud menor de -95.754168:

>> db.restaurantes.find({"address.coord":{$gte:-95.754168}},{id:0})

11. Restaurantes que cuisine no es 'American', cualificación superior a 70 y longitud menor a -65.754168:

>> db.restaurantes.find({$and:[{cuisine:{$ne:"American "}},{"grades.score":{$gt:70}},{"address.coord.1":{$lt:-65.754168}}]})

12. Restaurantes que cuisine no es 'American ', marcador mayor de 70 y longitud menor a -65.754168, sin usar $and:

>> db.restaurantes.find({cuisine:{$ne:"American "},"grades.score":{$gt:70},"address.coord.1":{$lt:-65.754168}})

13. Restaurantes que cuisine no es es 'American ', que obtuvieron un grado 'A' y no pertenecen a Brooklyn. Ordenar resultado por cuisine de forma descendiente.

>> db.restaurantes.find({cuisine:{$ne:"American "},"grades.grade":"A", borough:{$ne:"Brooklyn"}}).sort({cuisine:-1})

14. Buscar los restaurantes que tienen 'Wil' al principio del nombre, filtrar por restaurant_id, name, borough i cuisine:

>> db.restaurantes.find({name:/^Wil/}, {restaurant_id:1, name:1, borough:1, cuisine:1}).pretty()

15. Buscar los restaurantes que tienen 'ces' al final del nombre, filtrar por restaurant_id, name, borough i cuisine:

>> db.restaurantes.find({name:/ces$/}, {restaurant_id:1, name:1, borough:1, cuisine:1}).pretty()

16. Buscar los restaurantes que contengan 'Reg' en el nombre, filtrar por restaurant_id, name, borough i cuisine:

>> db.restaurantes.find({name:/Reg/}, {restaurant_id:1, name:1, borough:1, cuisine:1}).pretty()

17. Restaurantes del Bronx que hayan hecho algún plato chino o americano:

>> db.restaurantes.find({borough:"Bronx", $or:[{cuisine:"American "},{cuisine:"Chinese"}]})

18. Restaurantes que pertenezcan Staten Island , Queens, Bronx, Brooklyn y filtrar por restaurant_id, name, borough y cuisine:

>> db.restaurantes.find({$or:[{borough:"Staten Island"},{borough:"Queens"},{borough:"Bronx"},{borough:"Brooklyn"}]}, {restaurant_id:1, name:1, borough:1, cuisine:1}).pretty()
 
19. Restaurantes que NO pertenezcan Staten Island , Queens, Bronx, Brooklyn y filtrar por restaurant_id, name, borough y cuisine:

>> db.restaurantes.find({$nor:[{borough:"Staten Island"},{borough:"Queens"},{borough:"Bronx"},{borough:"Brooklyn"}]}, {restaurant_id:1, name:1, borough:1, cuisine:1}).pretty()

20. Restaurantes que el marcador no sea mayor de 10 y filtrar por restaurant_id, name, borough y cuisine:

>> db.restaurantes.find({"grades.score":{$not:{$gt:10}}}, {restaurant_id:1, name:1, borough:1, cuisine:1}).pretty()

21. Restaurants que preparan pez excepto 'American' y 'Chinees' o que el nombre del restaurante comience por 'Wil'
y filtrar por restaurant_id, name, borough y cuisine:

>> db.restaurantes.find({$nor:[{cuisine:"American "},{cuisine:"Chinees"},{cuisine:"Donuts"},{cuisine:/^Ice/},{name:/^Wil/}]}, {restaurant_id:1, name:1, borough:1, cuisine:1}).pretty()

22. Restaurantes con nota 'A', score 11 y en la fecha ISODate "2014-08-11T00:00:00Z":

>> db.restaurantes.find({$and:[ {"grades.grade":"A"}, {"grades.score":11}, {"grades.date":ISODate ("2014-08-11T00:00:00Z")}]}, {restaurant_id:1, name:1, grades:1})

23. Consultar restaurant_id, name y grades donde los restaurantes, el 2n elemento de variedad de grados contiene un grado de "A" i marcador 9 sobre un ISODate "2014-08-11T00:00:00Z".

>> db.restaurantes.find({ "grades.2.grade":"A", "grades.2.score":9, "grades.2.date":ISODate ("2014-08-11T00:00:00Z")}, {restaurant_id:1, name:1, grades:1})

24. Consulta para encontrar el restaurant_id, name, adreça y ubicació geogràfica pera aquellos restaurantes dónde el segundo elemento del array coord contiene un valor que es más de 42 y menor a 52.

>> db.restaurantes.find({$and:[{"address.coord.1":{$gt:42}},{"address.coord.1":{$lt:52}}]} , {estaurant_id:1, name:1, adreça:1, "address.coord":1} )

25. Consulta para organizar según nombre de los restaurants en ordren ascendente:

>> db.restaurantes.find({},{name:1}).sort({name:1})

26. Consulta para organizar según nombre de los restaurants en ordren descendente:

>> db.restaurantes.find({},{name:1}).sort({name:-1})

27. Escriu una consulta per organitzar el nom de la cuisine en ordre ascendent i pel mateix barri de cuisine. Ordre descendent.

>> db.restaurantes.find({},{name:1, borough:1}).sort({ borough:-1, name:-1})


28. Consulta que muestra todas las direcciones que no tienen calle:

>> db.restaurantes.find({"address.street":{$exists:false}})

29. Consulta que selecciona todos los documentos en la colección de restaurantes donde el valor del campo coord es Double.

>> db.restaurantes.find({"address.coord":{$type:"double"}})


30. Restaurant_id, name y grade para aquellos restaurantes que devuelvan 0 como resto después de dividir el marcador por 7.

>> db.restaurantes.find({$divide:{"grades.score",7},0}, {restaurant_id:1,name:1,"Gradess.grade":1})

31. Name, borough, longitud, altitud y cuisine para aquellos restaurantes que contienen 'mon' como tres letras en algun lugar de su nombre:

>> db.restaurantes.find({name:/m/,name:/o/,name:/n/}, {name:1,borough:1,"address.coord":1,cuisine:1})


32. Name, borough, longitud, latitud y cuisine para aquellos restaurantes que contienen 'Mad' como primeras tres letras de su nombre:

>> db.restaurantes.find({name:/^Mad/}, {name:1,borough:1,"address.coord":1,cuisine:1})
