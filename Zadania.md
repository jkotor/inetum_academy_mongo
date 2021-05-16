# Zadania

## Część 0 (proces mongod, linux)
Polecenia
```sh
sudo systemctl status mongod
sudo systemctl start mongod
sudo systemctl stop mongod
mongo
```

## Część 1 (bazy danych i kolekcje)
Polecenia

```
show databases / show dbs
use <baza_danych>
show collections
db.createCollection("<kolekcja>")
db.<kolekcja>.drop()
db.stats()
cls
```
#### Zadanie 1
Wyświetlić istniejące bazy danych, wejść do jednej z systemowych baz danych i wyświetlić istniejące kolekcje. 

Sprawdzić statystyki.

#### Zadanie 2
Utworzyć bazę danych o nazwie "myshop" (lub wybrać inną nazwę). Wejść do bazy danych i utworzyć w niej kolekcję "testowa". Sprawdzić, że kolekcja istnieje.

Usunąć kolekcję "testowa" i sprawdzić, że nie istnieje.

## Część 2 (CRUD na dokumentach)
Polecenia
```
db.<kolekcja>.find()
// db.users.find()
db.<kolekcja>.insert()
// db.users.insert({_id:1, name: "Frodo Baggins"})
db.<kolekcja>.update()
// db.users.update({_id:1}, {name: "Smeagol"})
// operators: $set, $unset
db.<kolekcja>.remove()
// db.users.remove({_id:1})
```

Elementy testowe do bazy danych:
```
{ "_id":1, "item": "journal", "qty": 25, "size": { "h": 14, "w": 21, "uom": "cm" }, "status": "A" }
{ "_id":2, "item": "notebook", "qty": 50, "size": { "h": 8.5, "w": 11, "uom": "in" }, "status": "A" }
{ "_id":3, "item": "paper", "qty": 100, "size": { "h": 8.5, "w": 11, "uom": "in" }, "status": "D" }
{ "_id":4, "item": "planner", "qty": 75, "size": { "h": 22.85, "w": 30, "uom": "cm" }, "status": "D" }
{ "_id":5, "item": "postcard", "qty": 45, "size": { "h": 10, "w": 15.25, "uom": "cm" }, "status": "A" }
```
qty - quantity, h - height, w - width, uom - Units of measurement

#### Zadanie 3
W bazie "myshop" wstawić do nowej kolekcji "inventory" trzy elementy z powyższej listy o identyfikatorach 1, 2, 3. Wyświetlić zawartość kolekcji.

Używając polecenia `insertMany()` wstawić dokumenty o identyfikatorach 4 i 5.

#### Zadanie 4
Spróbować wstawić dokument "planner2" o tym samym identyfikatorze co "planner". 

Usunąć dokument "planner" i wstawić w jego miejsce "planner2". 

#### Zadanie 5
Wstawić nowy dokument do kolekcji bez podawania identyfikatora. (Co się stało?)
Usunąć nowo dodany dokument.

#### Zadanie 6
Zmienić status dokumentu "paper" na "B". Sprawdzić wynik zmiany. (Co się stało?)

#### Zadanie 7
Dodać elementom 1, 2, 3 parametr określający ich wagę (weight) z dowolnymi wartościami. 

Usunąć paramert z wagą z dokumentu 3.

#### Zadanie 8
Skasować wszystkie dokumenty z kolekcji "inventory" jednym poleceniem, sprawdzić wynik. Ponownie wstawić wszystkie 5 dokumentów z następującymi wartościami:

```
{ _id:1, item: "journal", status: "A", size: { h: 14, w: 21, uom: "cm" }, instock: [ { warehouse: "A", qty: 5 } ] }
{ _id:2, item: "notebook", status: "A",  size: { h: 8.5, w: 11, uom: "in" }, instock: [ { warehouse: "C", qty: 5 } ] }
{ _id:3, item: "paper", status: "D", size: { h: 8.5, w: 11, uom: "in" }, instock: [ { warehouse: "A", qty: 60 } ] }
{ _id:4, item: "planner", status: "D", size: { h: 22.85, w: 30, uom: "cm" }, instock: [ { warehouse: "A", qty: 40 } ] }
{ _id:5, item: "postcard", status: "A", size: { h: 10, w: 15.25, uom: "cm" }, instock: [ { warehouse: "B", qty: 15 }, { warehouse: "C", qty: 35 } ] }
```

## Część 3 (wyszukiwanie)
Polecenie `find()`
```
db.<kolekcja>.find({<warunki>})
db.<kolekcja>.find({}, {<projekcja>})
db.<kolekcja>.find({<warunki>}, {<projekcja>})
// db.users.find({name: "Frodo"})
// db.users.find({},{"address":1}) - include
// db.users.find({},{"address":0}) - exclude 
```

#### Zadanie 9
Wyświetlić elementy o statusie "A". 

Wyświetlić elementy znajdujące się w magazynie "A".

#### Zadanie 10 
Operatory `$and, $or, $in`.

Wyświetlić elementy o statusie "A" znajdujące się w magazynie "A".

Wyświetlić elementy o _id: 1, 2, 3.

Wyświetlić elementy o statusie "D" oraz elementy z magazynu "B".

#### Zadanie 11
Wyświetlić wszystkie elementy, ale tylko pola "_id", "item" i "status".

Wyświetlić elementy o statusie "D", ale tylko pola "_id", "item" i "status".

Wyświetlić elementy o statusie "D", ale tylko pola "item" i "status" (ukryć "_id")

Wyświetlić elementy o statusie "A", wszystkie pola bez pól "size" oraz "_id".

#### Zadanie 12
https://docs.mongodb.com/manual/reference/operator/query-comparison/

Wyświetlić elementy, które mają wysokość (h) nie większą niż 10.

Wyświetlić elementy, które mają wysokość (h) nie większą niż 10 i miarą są centymetry.

Wyświetlić elementy, które mają wysokość (h) nie większą niż 10 i miarą są centymetry, na wyjściu tylko "name" i "size".

#### Zadanie 13
https://docs.mongodb.com/manual/reference/operator/query/regex/

Wyświetlić elementy zawierające w nazwie literę p.

Wyświetlić nazwę i status elementów kończących się na "er".
