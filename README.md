# MongoDB

## Insert Data
- Flights
```
db.flightData.insertMany([   {     "departureAirport": "MUC",     "arrivalAirport": "SFO",     "aircraft": "Airbus A380",     "distance": 12000,     "intercontinental": true   },   {     "departureAirport": "LHR",     "arrivalAirport": "TXL",     "aircraft": "Airbus A320",     "distance": 950,     "intercontinental": false   } ])
```
- Passengers
```
db.passengers.insertMany([   {     "name": "Max Schwarzmueller",     "age": 29   },   {     "name": "Manu Lorenz",     "age": 30   },   {     "name": "Chris Hayton",     "age": 35   },   {     "name": "Sandeep Kumar",     "age": 28   },   {     "name": "Maria Jones",     "age": 30   },   {     "name": "Alexandra Maier",     "age": 27   },   {     "name": "Dr. Phil Evans",     "age": 47   },   {     "name": "Sandra Brugge",     "age": 33   },   {     "name": "Elisabeth Mayr",     "age": 29   },   {     "name": "Frank Cube",     "age": 41   },   {     "name": "Karandeep Alun",     "age": 48   },   {     "name": "Michaela Drayer",     "age": 39   },   {     "name": "Bernd Hoftstadt",     "age": 22   },   {     "name": "Scott Tolib",     "age": 44   },   {     "name": "Freddy Melver",     "age": 41   },   {     "name": "Alexis Bohed",     "age": 35   },   {     "name": "Melanie Palace",     "age": 27   },   {     "name": "Armin Glutch",     "age": 35   },   {     "name": "Klaus Arber",     "age": 53   },   {     "name": "Albert Twostone",     "age": 68   },   {     "name": "Gordon Black",     "age": 38   } ])
```


## Fetch Data
```
db.flightData.find({intercontinental: true}).pretty()
```
```
db.flightData.find({distance: {$gt: 900}}).pretty()
```
```
db.flightData.findOne({distance: {$gt: 1000}}).pretty()
```
- Find all elements filtered 
  ```
  db.passengers.find().toArray()
  ```
- Find a cursor for all the elements filtered
  ```
  db.passengers.find().forEach((passengerData) => {printjson(passengerData)}
  ```
- Find the value of a given key inside filtered element
  ```
  db.passengers.findOne({name: "Albert Twostone"}).hobbies
  ```
- Find the entire document that have that key-value match
  ```
  db.passengers.find({hobbies: "sports"}).pretty() 
  ```
- Search for nested fields 
  ```
  db.flightData.find({"status.description": "on-time"}).pretty()
  ```


## Update
- Update only the desiredd field, from the first document filtered
  ```
  db.flightData.updateOne({"_id" : ObjectId("6035701519b36532c7ce02cc")}, {$set: {delayed: true}})
  ```
- Update only the desiredd field, from all documents filtered
  ```
  db.flightData.updateMany({"_id" : ObjectId("6035701519b36532c7ce02cc")}, {$set: {delayed: true}})
  ```
- Update the desired field and delete the remaining others (overwrite object)
  ```
  db.flightData.update({"_id" : ObjectId("6035701519b36532c7ce02cc")}, {delayed: true})
  ```
- If you really want to replace the objetct, better use this command
  ```
  db.flightData.replaceOne({_id: ObjectId("6035701519b36532c7ce02cc")}, {"departureAirport": "MUC", "arrivalAirport": "SFO", "aircraft": "Airbus A380", "distance": 30000, "intercontinental": true })
  ```
- Add fields to all flights, as embedded documents (nested)
  ```
  db.flightData.updateMany({}, {$set: {status: {description: "on-time", lastUpdated: "1 hour ago"}}})
  ```
- Add data as a list, not documents
  ```
  db.passengers.updateOne({name: "Albert Twostone"}, {$set: {hobbies: ["sports", "cooking"]}})
  ```



## Projection
Prevent fetch of unecessary flightData
- Get only passengers id (always included by default) and name 
  ```
  db.passengers.find({}, {name: 1}).pretty()
  ```
- Get only passengers name
  ```
  db.passengers.find({}, {name: 1, _id: 0}).pretty()
  ```
  
  
