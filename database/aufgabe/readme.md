# SQL Aufgaben 

## Vorbereitung
1. Öffne die Webseite https://sql.js.org/examples/GUI/
2. Wähle oben rechts __Load DB__ und wähle die Datenbank-Datei __pokedex.db__

Es wird folgenden Abfrage (__Query__) ausgeführt die alle Tabellen in der SQLite Datenbank aufführt

```sql
SELECT `name`, `sql`
FROM `sqlite_master`
WHERE type='table';
```

Die Tabellen sind

|Tabellen Name|Beschreibung|
|--|--|
|pokemon|Die 151 Pokemon der 1. Generation|
|type|Die verschiedenen Pokemon-Typen|
|trainer|Einige bekannte Trainer|
|region|Die Regionen der Welt|
|pokemon_type|Verknüpfungstabelle Pokemon zu Pokemon-Typ|
|trainer_pokemon|Verknüpfungstabelle Trainer zu Pokemon|

## Aufgabe 1: SELECT

Selektiere alle Pokemon in der Datenbank.   
Trage folgende Query links in den Editor und drücke oben rechts auf __Execute__

```sql
SELECT * FROM pokemon
```

Zeige nur die deutschen Namen an

```sql
SELECT name_de FROM pokemon
```

Zeige den Namen vom Pokemon an mit dem Index 1

```sql
SELECT name_de 
FROM pokemon
WHERE id = 1
```

Zeige den Index vom Pokemon 'Smogmog'

```sql
SELECT id
FROM pokemon
WHERE name_de = 'Smogmog'
```


### Jetzt bist du dran 🤔

1. Selektiere das Pokemon mit der ID 2
2. Zeige vom Pokemon mit ID 25 alle Namen an (Deutsch, Englisch und Japanisch)
3. Selektiere alle Trainer (Tabelle _trainer_)

## Aufgabe 2: LIKE

Mit `LIKE` kannst du nach ähnlichen Texteinträgen suchen. Nutze dabei das Prozentzeichen `%` als Plathalter

Zeige alle Pokemon die mit Me anfangen

```sql
SELECT id, name_de
FROM pokemon
WHERE name_de LIKE 'me%'
```

### Jetzt bist du dran 🤔

1. Selektiere alle Pokemon die mit 'D' anfangen
2. Selektiere alle Pokemen die mit 'i' enden. (Tipp: Platzhalter anders setzen)

## Aufgabe 3: COUNT

SQL bietet mehrere Funktionen um Daten zusammenzufassen (_Aggregate_). Eins davon ist `COUNT`. Damit lassen sich die Anzahl der Einträge anzeigen.

Wieviele Pokemon gibt es in der Datenbank?

```sql
SELECT COUNT(*)
FROM pokemon
```

Wieviele haben einen S als Anfangsbuchstaben im Namen?

```sql
SELECT COUNT(*)
FROM pokemon
where name_de LIKE 'S%'
```

### Jetzt bist du dran 🤔

1. Wieviele Pokemon haben L als Anfangsbuchstaben?
2. Wieviele Regionen gibt es?

## Aufgabe 4: INSERT

Mit dem Befehl `INSERT INTO` können wir Daten einfügen.

Es gibt einen neuen Trainer "Tracey Sketchit" den wir anlegen müssen.

```sql
INSERT INTO trainer
VALUES (8, 'Tracey Sketchit', 1)
```
__Hinweis__: Insert wird nur bestätigt. Die Änderung wird nicht direkt angezeigt. 

Zum Prüfen...

```sql
SELECT * FROM trainer
```

Er hat einen "Sichlor" Pokemon

```sql
SELECT * FROM pokemon where name_de = 'Sichlor'
```

```sql
INSERT INTO trainer_pokemon
VALUES (8, 123)
```

Zum prüfen

```sql
select * from trainer_pokemon
```

### Jetzt bist du dran 🤔
1. Füge dich selbst als Trainer in die Datenbank
2. Weise dir beliebige Pokemon zu


## Aufgabe 5: UPDATE

Mit `UPDATE` können wir bestehende Daten anpassen.

"Tracey Sketchit" ist aus der Region Kanto (1) in die Region Alola (7) umgezogen.

```sql
UPDATE trainer
SET regionId = 7
WHERE id = 8
```

__WICHTIG__: Vergiss nicht die `WHERE` Bedingung zu setzen, sonst werden alle Daten verändert. 

__Tipp__: Schreibe immer erst die WHERE, z.B. `UPDATE trainer WHERE id = 8` und dann die `SET`. So kannst du nicht ausversehen einen falschen Befehl absenden.


## Aufgabe 6: LEFT JOIN

In einer relationen Datenbank haben die Tabellen beziehungen. Diese werden mit Schlüssel (_keys_) abgebildet.

In der Tabelle _trainer_ referenziert _regionId_ auf die Tabelle _region_.

```sql
SELECT name, regionId
FROM trainer
```

Um die Name der Region zu erhalten müssen wir die Verknüpfung in der Query mit `LEFT JOIN` aufführen.  
Zudem benennen wir die Tabellen, um leichter auf ihre Elemente zuzugreifen. Hier nennen wir die Tabelle `trainer t`, der Name ist aber beliebig, d.h. `trainer tr` oder `trainer tx` wäre auch möglich.  
Mit `ON` geben wir die Verknüpfung über die Schlüssel an.
Mit `AS` können wir die Spalte einen anderen Namen geben.

Selektion trainer mit region

```sql
SELECT 
    t.name AS Trainer_Name
   ,r.name As Region_Name
FROM trainer t
LEFT JOIN region r 
    ON r.id = t.regionId
```

Alle Trainer aus der Region Kanto

```sql
SELECT 
    t.name
FROM trainer t
LEFT JOIN region r 
    ON r.id = t.regionId
WHERE r.name = 'Kanto'
```

### Jetzt bist du dran 🤔
1. Wieviele Trainer gibt es in der Region außerhalb von Kanto?  
(Tipp: Benutze `<>` für "nicht gleich")


## Aufgabe 7: Verknüpfungstabellen

Im vorherigen Beispiel war die Beziehung __"1 zu 1"__, d.h. 1 Trainer hat genau 1 Region Beziehung.  
Bei __"1 zu n"__ Beziehungen oder __"n zu n"__ Beziehungen, wo es mehrere Verknüpfungen geben kann, brauchen wir Verknüpfungstabellen. 

Pokemon können mehrere Typen angehören, daher gibt es die Verknüfungstabelle `pokemon_type`

```sql
SELECT *
FROM pokemon p
LEFT JOIN pokemon_type pt
    ON pt.pokemonId = p.id
LEFT JOIN type t 
    ON pt.typeId = t.id
```

Welcher Pokemon-Typ ist Bisasam?

```sql
SELECT t.type
FROM pokemon p
LEFT JOIN pokemon_type pt
    ON pt.pokemonId = p.id
LEFT JOIN type t 
    ON pt.typeId = t.id
WHERE p.name_de = 'Bisasam'
```

### Jetzt bist du dran 🤔
1. Welche Pokemon gehören zum Typ __"Gift"__?  
(Tipp: Tausche in der Abfrage oben nur `t.type` mit `p.name_de` und im `WHERE t.type = ...`)




