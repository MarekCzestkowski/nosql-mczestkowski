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
#### Wyniki 

Wyniki zostały przedstawone w formie tabeli:

|   | opcje | średni wynik (sekundy) | (średni wynik minuty) |
| ------ | ------ | ------ | ------ |
| I | { "w" : 1, "wtimeout" : 0 } | 810 | 12,8 |
| II | { w: 1, j: false } | 789 | 12,5 |
| III | { w: 1, j: true } | 854 | 13,6 |
| IV | { w: 2, j: false } | 654 | 10,2 |
| V | { w: 2, j: true } | 889 | 14,1 |

#### Wnioski

Dwa najlepsze wyniki jakie można zobaczyć to podjeście II i IV. Oba podejścia mają wspólną opcję: 

 ```j: false  ```

co oznacza, że dane zostają zapisane w pamięci. Na kolejnym miejscu znajduje się podejście I które ma tą samą opcję dla j tylko nie podaną gdyż jest ona opcją domyślną. Opcja wtimeout jeśli nie jest większa od I nie ma wpływu na wynik dlatego wyniki II i I niewiele od siebie odbiegają. 

Najgorsze wyniki to podejścia III i V i posiadają opcję:

 ```j: true  ```

co oznacza że dane będą zapisywane w disk journal(On-disk journal).

Natomiast opcja "w" żąda potwierdzenia, że operacja zapisu została rozpropagowana do określonej liczby instancji mongo. Porównując IV i II wydawałoby się że im wyższy numer tym lepszy czas ale porównując II i V można odnieść inne wrażenie jakby zapis(On-disk journal) miał odwrotny wpływ na czas niż zapis(in memory).

Kolejność od najlepszego do najgorszego czasu: **IV, II, I, III, V**.




Przykład wyglądu datasetu z programu robo 3t:
![1](https://i.imgur.com/azPTkro.png)
Przykład agregacji z rosnącą liczbą like'ów
![2](https://i.imgur.com/hUg58lD.png)
Przykład agregacji z malejącą liczbą like'ów
![3](https://i.imgur.com/TT1PjWh.png)
