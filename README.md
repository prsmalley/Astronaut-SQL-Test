# Astronaut SQL Test - Khan Academy Project: Data dig with github actions

A small SQL project that explores NASA's astronaut yearbook data. The script creates a table of astronauts, loads in their info (birth date, education, missions, hours in space, etc.), and runs a series of simple queries to answer questions:

- Who has the most hours in space?
- How do astronauts compare by experience level?
- Is there a pattern between flight hours and how long astronauts lived? (no)

Data source: [Kaggle - NASA Astronaut Yearbook](https://www.kaggle.com/nasa/astronaut-yearbook)

## The File

- **`AstronautQuery.sql`** — Creates the `astronauts` table, inserts every astronaut's record, and ends with a set of analysis queries (totals, averages, experience-level classification, and a risk profile breakdown

Can be run locally with SQLite:

```bash
sqlite3 :memory: < AstronautQuery.sql
```

## GitHub Actions

Two workflows run automatically every time code is pushed or a pull request is opened. 
1. Lint.yml - a standard style checker using sqlfluff to flag formatting issues
2. Test.yml - tests the file in a vm environment using SQLite and saves the output to a file. Searches the file for expected results and uploads.






