# ATP Tennis Professionals | Big Data Management & SQL

**Academic group project · MySQL · Data cleaning · Database design · SQL analytics**

## Project overview
Developed a relational database from historical professional tennis records as part of the **Big Data Management** course in the MSc in Data Science at ISCTE. The project covered data import, extensive cleaning and transformation, relational modelling, integrity constraints and analytical SQL queries.

The underlying records span **28 March 1973 to 14 February 2022**. The objective was to move from a large, relatively unstructured dataset to a consistent database suitable for reliable statistical analysis and efficient querying.

This was an **academic group project**. Collaborators' names are intentionally omitted from this public portfolio.

## 1. Data import and technical environment
- Used a **Docker-based environment** with MongoDB and MySQL.
- Imported the original ATP player data into **MongoDB**, then loaded a CSV representation into **MySQL** for transformation.
- Used **phpMyAdmin** to inspect data, execute SQL operations and validate the resulting tables.
- Kept the original source columns during preparation, creating derived fields for cleaned or normalised information.

## 2. Data preparation and identifier design

### Player identifiers
Using player names as identifiers was unreliable because different players could share the same name. The team compared distinct player names with distinct player profile links and selected **LinkPlayer** as the identifying source. A numeric **PlayerID** was then assigned using SQL's `DENSE_RANK()` window function.

### Tournament identifiers
Tournament names could recur across editions and could be associated with different characteristics. A numeric **TournamentID** was therefore generated from the combination of **tournament name and date**, avoiding accidental merging of distinct tournament editions. The analysis identified **22,233 distinct tournament identifiers** before subsequent date filtering.

### Date normalisation
The source date field sometimes contained both start and end dates in text form. We:
- Split date ranges into **Start_Date** and **End_Date**.
- Converted formats such as `YYYY.MM.DD` into MySQL `DATE` values using `REPLACE()`, `SUBSTRING_INDEX()` and `STR_TO_DATE()`.
- Handled absent or invalid date components with `NULL`.
- Added a date-range flag to distinguish records inside and outside the target period.

### Result and match cleaning
- Standardised win/loss information into a derived **ResultStatus** field.
- Trimmed text and replaced empty strings with `NULL` where appropriate.
- Addressed the problem of the **same match appearing twice**, once from each player's perspective.
- Created a **Unique_Matches** indicator to exclude mirrored losses when both players were represented in the player table, while retaining records involving opponents outside that table and records without a recorded result.
- Added indexes to support the relevant lookups.

## 3. Relational database design
The cleaned dataset was structured into four connected tables:

| Table | Purpose |
| --- | --- |
| **Player** | Player identifiers, names, characteristics and standardised country information |
| **Tournament** | Tournament identifiers, surfaces, dates, locations and prizes |
| **Matches** | Unique match records, player/tournament references, scores and results |
| **Countries** | Standardised country names and ISO codes |

### Geographic normalisation
Birthplace and tournament-location fields contained mixed naming conventions, abbreviations and city/state names. Country names were cleaned and matched to an external **Countries** reference table to obtain ISO codes.

The report records **9,960 players**, with substantial missing birthplace information, and reports ISO mapping for **95.2% of the relevant cleaned birthplace records**. For tournament locations, it reports ISO matches for **21,698 records (97.62%)**. These percentages reflect the report's stated validation results, not a claim that every original record was complete.

### Data integrity
Primary keys and foreign keys were defined to connect matches to players and tournaments and to link country codes. The model used **ON DELETE RESTRICT** to protect historical references and **ON UPDATE CASCADE** to propagate identifier changes consistently.

## 4. Validation and scale
Validation queries checked identifier mappings, transformed date fields, date-range flags, country-code matches and the match-deduplication logic.

The report documents a reduction from **1,308,335 source match rows** to **696,595 records** in the final Matches table after deduplication and filtering — approximately **53% fewer rows**. This reduction reflects the chosen representation of unique matches and the filtering rules; it is not a generic measure of missing or erroneous data.

## 5. Analytical SQL queries
The final database supported several multi-table analytical questions:

1. **Country-level summaries:** counts of players, tournaments and matches associated with countries.
2. **Top 10 win percentages:** ranked players by win rate, using a minimum-match threshold based on average participation to reduce distortions from very small samples.
3. **Left-handed Grand Slam players:** calculated win percentages for left-handed players in Australian Open, Roland Garros, Wimbledon and US Open, accounting for the winner and opponent perspectives.
4. **Hard-court performance:** identified the five players with the highest numbers of wins on hard surfaces.

These queries required filtering, aggregation, joins and careful handling of the single-record-per-match representation.

## Outcome and skills demonstrated
The project transformed historical tennis records into a cleaner, relationally structured database, with explicit validation of key transformations and SQL queries designed to answer performance questions.

**Technologies:** MySQL · SQL · MongoDB · Docker · phpMyAdmin

**Methods:** Data cleaning · Data normalisation · Window functions · Indexing · Primary/foreign keys · Referential integrity · Deduplication · Relational database design · Joins and aggregation · Analytical SQL

## Access to the full project
> **Full project available upon request.** The worked SQL script is retained privately and can be shared for professional or recruitment review.

The original academic report, large database dump and collaborators' identifying information are not published in this repository.
