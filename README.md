# nosql-mczestkowski
Dataset w formacie json zawiera liste najpopularniejszych filmów z serwisu youtube.com z roku 2017 (w zależności od ilości like'ów).
Dataset zawiera takie dane, jak: url do filmu, nazwa filmu, ilość like'ów, data dodania filmu
Dataset został okrojony do około 2 500 000 rekordów przy liczbie like'ów od 100 000 do 1 000 000.

Link do datasetu: https://drive.google.com/file/d/1tfq60WbX0TrGLghR7bwLzyCL1wh548bU/view?usp=sharing

Informacje o komputerze na którym były wykonywane obliczenia:

| Nazwa                 | Wartość    |
|-----------------------|------------|
| System operacyjny     | Windows 7 x64 |
| Procesor              | Intel Core i5 @3,5 GHz |
| Liczba rdzeni         | 4 |
| Pamięć                | 8 Gb |
| Dysk                  | SSD/HDD |


___________________
#### MongoDB

- wersja: Windows Server 2008 R2 64-bit and later, with SSL support x64

Instalator do pobrania ze [strony](https://www.mongodb.com/download-center#community) 
Po instalacji, do uruchomienia MongoDB nalezy użyć CMD:

 ``` mongod```


___________________
Import danych do bazy:

 ``` mongoimport --db youtube --collection youtube --file dataset.json```
_______________

Przykład wyglądu datasetu z programu robo 3t:
![1](https://i.imgur.com/azPTkro.png)
Przykład agregacji z rosnącą liczbą like'ów
![2](https://i.imgur.com/hUg58lD.png)
Przykład agregacji z malejącą liczbą like'ów
![3](https://i.imgur.com/TT1PjWh.png)
