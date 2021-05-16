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
