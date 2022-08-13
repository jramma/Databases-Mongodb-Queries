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

5. Mostrar restaurantes que están en el Bronx

>> db.restaurantes.find({borough:"Bronx"}).pretty()

6. Los 5 primeros que están en el Bronx