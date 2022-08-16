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

22. 













