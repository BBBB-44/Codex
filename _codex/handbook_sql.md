---
---


# summary 
- [Schema explorer](#schema-explorer)
- [Create table](#create-table)
- [Create View](#create-view)
- [Stored procedures](#stored-procedures)


## Schema explorer 

```
SELECT 
    TABLE_NAME, 
    COLUMN_NAME, 
    DATA_TYPE, 
    CHARACTER_MAXIMUM_LENGTH,
    IS_NULLABLE,
    COLUMN_KEY,
    COLUMN_DEFAULT
FROM 
    information_schema.COLUMNS
WHERE 
    TABLE_SCHEMA = DATABASE()
ORDER BY 
    TABLE_NAME, ORDINAL_POSITION;
```
 

## Create Table 

 
```
CREATE TABLE table_name ( 
  column1 datatype constraint, 
  column2 datatype constraint, 
  column3 datatype constraint, 
  .... 
); 

 

 

 

View 

## Create View 

 

CREATE VIEW view_name AS 

SELECT column1, column2 

FROM table_name 

WHERE condition; 
```
 

Create view from multiple table 

```
CREATE VIEW view_name AS 

SELECT * FROM table_name 

UNION ALL 

SELECT * FROM table_name 

UNION ALL 

SELECT * FROM table_name 

UNION ALL 

SELECT * FROM table_name 

UNION ALL 

SELECT * FROM table_name 

UNION ALL 

SELECT * FROM table_name; 
```
 

 

Create view join to another view 
```
CREATE VIEW view_name AS 

SELECT 

    v.nom, 

    t.nbPoints AS total_points 

FROM table_name t 

JOIN view_name_2 v 

    ON t.noJoueur = v.noJoueur; 
```
 

## Stored procedures 

 

 

 

Create stored procedure with input params 

```
DELIMITER // 

CREATE PROCEDURE psResultatsJoueurs( 

    IN noJoueur INT, 

    IN noTournoi INT, 

    IN anneeTournoi INT 

) 

BEGIN 

    SELECT 

        noJoueur, 

        noTournoi, 

        anneeTournoi, 

        nombrePoints, 

        gains 

    FROM tblResultat 

    WHERE noJoueur = noJoueur 

      AND noTournoi = noTournoi 

      AND anneeTournoi = anneeTournoi; 

END // 
DELIMITER ; 
```
