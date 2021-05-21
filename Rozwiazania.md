#### Zadanie 3

```
db.inventory.insert({ "_id":1, "item": "journal", "qty": 25, "size": { "h": 14, "w": 21, "uom": "cm" }, "status": "A" })
db.inventory.insert({ "_id":2, "item": "notebook", "qty": 50, "size": { "h": 8.5, "w": 11, "uom": "in" }, "status": "A" })
db.inventory.insert({ "_id":3, "item": "paper", "qty": 100, "size": { "h": 8.5, "w": 11, "uom": "in" }, "status": "D" })

db.inventory.find()

db.inventory.insertMany([
    { "_id":4, "item": "planner", "qty": 75, "size": { "h": 22.85, "w": 30, "uom": "cm" }, "status": "D" },
    { "_id":5, "item": "postcard", "qty": 45, "size": { "h": 10, "w": 15.25, "uom": "cm" }, "status": "A" }
])
```

#### Zadanie 4
identyfikator musi być unikalny

#### Zadanie 5
```
db.inventory.insert({item: "new-item"})

db.inventory.remove({_id:ObjectId("60a6db537defcbc9851a93d0")})
```
Powstanie nowy dokument z wygenerowanym id, uzyc to id do skasowania

#### Zadanie 6
```
// źle, bo podmieni cały dokument
db.inventory.update({_id: 3},{status: "B"})
// poprawnie 
db.inventory.update({_id: 3},{$set: {status: "B"}})
```

#### Zadanie 7
```
db.inventory.update({_id: 1},{$set: {weight: {value: 123}}})
db.inventory.update({_id: 2},{$set: {weight: {value: 12, uom: "g"}}})
db.inventory.update({_id: 3},{$set: {weight: {value: 25, uom: "g"}}})

db.inventory.update({_id: 3},{$unset: {weight: ""}})
```
#### Zadanie 8
```
db.inventory.remove({})

//insert tez zadziała jak insertMany()
//db.inventory.insert([.....])
```

#### Zadanie 9
```
db.inventory.find({status:"A"})
db.inventory.find({"instock.warehouse":"A"})
```

#### Zadanie 10
```
db.inventory.find({status:"A", "instock.warehouse":"A"})

db.inventory.find({_id: {$in: [1, 2, 3]}})

db.inventory.find({
    $or: [ {status: "D"},
           {"instock.warehouse":"B"}  
         ]
})
```

#### Zadanie 11
Nie wolno łączyć include i exclude, wyjątek stanowi pole _id.
```
db.inventory.find({},{item:1, status:1})
db.inventory.find({status: "D"},{item:1, status:1})
db.inventory.find({status: "D"},{item:1, status:1, _id:0})
db.inventory.find({status: "A"},{size:0, _id:0})
```

#### Zadanie 12
```
db.inventory.find({"size.h": {$lte: 10}})
db.inventory.find({"size.h": {$lte: 10}, "size.uom": "cm"})
db.inventory.find({"size.h": {$lte: 10}, "size.uom": "cm"}, 
                  {item:1, size:1, _id:0}
)
```

#### Zadanie 13
Drobiazg: ^ dopasowuje początek, $ dopasowuje koniec
```
db.inventory.find({item: /p/})
db.inventory.find({item: /er$/})
```

#### Zadanie 15
```
db.data.find().limit(8)
db.data.find().skip(8).limit(8)
db.data.find().skip(8).limit(8).sort({name:-1})
db.data.find({name: /numer_3/}, {type:0, _id:0}).sort({count:-1})
```

### Bonus
Przykładowa agregacja, składa się z kolejnych kroków (stage'y)
```
db.inventory.aggregate([
  {$match: {item: /p/}}, 
  {$unwind: "$instock"}, 
  {$group: {_id: "$item", 
            sum_qty: {$sum: "$instock.qty"}
           }
  }, 
  {$project: {"item": "$_id", "_id":0, total_quantity: "$sum_qty"}}
])
```

explain na zapytaniu listuje analizę jaką robi mongo
```
db.inventory.find({status:"D"}).explain()
```
Po założeniu indeksu zapytanie będzie lepiej optymalizowane
```
db.inventory.getIndexes()
db.inventory.createIndex({status:1})
db.inventory.find({status:"D"}).explain()

```



