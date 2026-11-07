# Olympic History Data Analysis (SQL Server)

A SQL-based data analysis project exploring **120 years of Olympic history** using athlete and athlete-event datasets. The project uses Microsoft SQL Server to answer eight analytical questions about medal counts, athlete achievements, teams, events, and Olympic seasons.

## Project Overview

The dataset is split across two CSV files:

- **`athletes.csv`** — athlete-level information, including athlete ID, name, sex, height, weight, and team.
- **`athlete_events.csv`** — event participation and medal information, including athlete ID, Olympic Games, year, season, city, sport, event, and medal.

The two datasets are connected through `athlete_events.athlete_id = athletes.id`.

## Repository Structure

```text
Project 2 olympic history/
├── athletes.csv
├── athlete_events.csv
├── ATHELETES_SQL.sql
├── ATHELETES_EVENTS_SQL.sql
├── project 2_solutions.sql
└── README.md
```

> The two large SQL files contain the imported table data/scripts supplied with the project. `project 2_solutions.sql` contains the analytical SQL queries.

## Tools & Technologies

- Microsoft SQL Server
- SQL (T-SQL)
- CSV data import
- Common Table Expressions (CTEs)
- Aggregate functions (`COUNT`, `SUM`, `MAX`)
- Window functions (`RANK`, `LAG`, `LEAD`)
- String aggregation (`STRING_AGG`)
- Joins and subqueries

## Database Schema

### `athletes`

| Column | Description |
|---|---|
| `id` | Unique athlete identifier |
| `name` | Athlete name |
| `sex` | Athlete sex |
| `height` | Height |
| `weight` | Weight |
| `team` | Team represented |

### `athlete_events`

| Column | Description |
|---|---|
| `athlete_id` | Athlete identifier; joins to `athletes.id` |
| `games` | Olympic Games edition |
| `year` | Year of the Olympic Games |
| `season` | Summer or Winter |
| `city` | Host city |
| `sport` | Sport |
| `event` | Specific event |
| `medal` | Gold, Silver, Bronze, or `NA` |

## Setup & Run

1. Download or clone this repository.
2. Open SQL Server Management Studio (SSMS) and connect to your SQL Server instance.
3. Create a database for the project, for example:

   ```sql
   CREATE DATABASE OlympicHistory;
   GO
   USE OlympicHistory;
   GO
   ```

4. Import `athletes.csv` and `athlete_events.csv` into the database as tables named **`athletes`** and **`athlete_events`**. You can use the SSMS Import Flat File / Import Data wizard.
5. Check that the imported column names and data types match the schema above. In particular, `id`, `athlete_id`, and `year` should be numeric columns, while descriptive fields should be text.
6. Open and run `project 2_solutions.sql` in SSMS.

The supplied `ATHELETES_SQL.sql` and `ATHELETES_EVENTS_SQL.sql` files may also be used if they contain the table creation and data-loading scripts for your SQL Server setup.

## Analysis Questions

The solution script addresses these eight questions:

1. **Top gold-medal team** — identify the team with the highest number of gold-medal event wins across the dataset.
2. **Silver medals by team** — calculate each team's total silver medals and identify the year in which it won the most silver medals.
3. **Gold-only athlete** — find the athlete with the most gold medals among athletes who never won silver or bronze.
4. **Top gold-medal athlete by year** — find the athlete(s) with the highest gold-medal count in each year; include all tied names as a comma-separated list.
5. **India's first medals** — identify the first year and sport/event in which India won gold, silver, and bronze.
6. **Gold medals in both seasons** — find athletes who won gold medals in both Summer and Winter Olympics.
7. **All three medal types in one year** — find athletes who won gold, silver, and bronze in the same Olympic year.
8. **Three consecutive Summer Olympics wins** — find athletes who won gold in the same event in three consecutive Summer Olympic editions from 2000 onwards.

## SQL Concepts Demonstrated

- Joining related tables using athlete IDs
- Filtering medal records and excluding non-medal values
- Grouping and aggregating data by team, athlete, year, season, and event
- Using CTEs to make multi-step analysis easier to read
- Applying `RANK()` to handle maximum values and ties
- Using `STRING_AGG()` to combine tied athlete names
- Using `LAG()` and `LEAD()` to compare consecutive Olympic editions

## Notes & Validation

- The queries are written for **Microsoft SQL Server (T-SQL)**. Functions such as `STRING_AGG()` require a compatible SQL Server version.
- Confirm how missing medals are represented in the imported data (the supplied solution uses `NA`).
- The supplied solutions use `COUNT(DISTINCT event)` in some team-level calculations. If the intended metric is the **number of individual medals**, review whether `COUNT(*)` or a distinct medal/athlete-event key is more appropriate for the question and dataset.
- Athlete names may not uniquely identify a person. For rigorous athlete-level analysis, consider grouping by athlete ID rather than name, especially where names may be duplicated.
- Question 5 asks for the first medal year and sport; the supplied query also returns the `event` column. Keep or remove that column depending on the required output.
- Review tie handling and duplicate event records against the dataset before treating the results as final.

## Project Objective

This project demonstrates practical SQL skills through a real-world, multi-table sports dataset. It focuses on transforming raw CSV data into meaningful insights using joins, aggregations, CTEs, subqueries, and window functions.

---

**Project:** Olympic History Data Analysis  
**Database:** Microsoft SQL Server  
**Language:** T-SQL
