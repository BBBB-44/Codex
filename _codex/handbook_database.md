---
---


# summary 
- [Schema explorer](#schema-explorer)
- [Create table](#create-table)
- [Create View](#create-view)
- [Stored procedures](#stored-procedures)


Table Architecture
General Principles

DONT Use camelCase for column names, since PostgreSQL convertit par défaut tous les noms de colonnes en minuscules.
Avoid generic id column names. Make identifiers specific to the entity.
bookId
artistId
venueId
eventId
Build the database architecture in English to keep it consistent and scalable.

Use consistent naming conventions across all tables. For example, always use birthDate rather than sometimes birthday and sometimes dateOfBirth.
For translatable fields, add the ISO language abbreviation:
description
descriptionFR
Keep the original/source identifiers whenever available. Do not rely only on internally generated IDs.
wikidataId
wikimediaId
sourceId
Preserve data provenance. The database should retain information about where the data came from and, when possible, the original identifier or source URL, rather than simply copying the data.
Avoid storing information in a single field when it could be useful as a page-generation or filtering variable.
Instead of only address, consider streetAddress, city, province, postalCode, country.
This makes it easier to generate web pages, URLs, slugs, filters, and location-based navigation.
Avoid unnecessary duplication. If the same information can be derived reliably from another table, consider using a relationship rather than duplicating the data.
Use controlled values where consistency matters. For example, don't have Canada, CA, and CAN appearing in different records if they represent the same country.
Prefer structured data over free text when the information will be used for filtering, sorting, searching, or page generation.
IDs, Slugs & URLs
Every entity should have a stable, specific identifier.
Keep source identifiers separate from internal identifiers.
artistId
wikidataId
Use slugs for web-facing URLs, but don't use the slug as the primary identifier.
artistId → stable database identifier
nameSlug → web URL identifier
Slugs should be generated consistently and should not be treated as permanent if the underlying name can change.
Consider whether fields such as city, province, country, profession, etc. should be stored separately specifically because they can become URL/page-generation variables.
Dates & Locations
Establish a consistent format for dates and timestamps from the beginning.
Distinguish between different types of dates when necessary:
birthDate
deathDate
createdAt
updatedAt
Avoid putting multiple pieces of information into one field when they may later need to be queried independently.
For locations, consider separating:
streetAddress
city
province
postalCode
country
Recommended Workflow

Start with the simplest useful structure:

artistId · name · description

Then progressively enrich the schema after testing it with the first 10 records.

These first entries will help reveal:

recurring data patterns;
which fields are actually needed;
edge cases;
normalization requirements;
naming conventions;
translation requirements;
source/provenance requirements;
opportunities for automated page generation;
fields that should be split into separate columns;
relationships between tables.

One additional recommendation: don't try to design the perfect schema before entering real data. The first 10–20 records are essentially a discovery phase. Let the actual data expose the structure, then formalize the schema.

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
