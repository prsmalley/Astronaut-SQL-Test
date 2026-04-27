# Astronaut SQL Test

A small SQL project that explores NASA's astronaut yearbook data. The script creates a table of astronauts, loads in their info (birth date, education, missions, hours in space, etc.), and runs a series of queries to answer questions like:

- Who has the most hours in space?
- How do astronauts compare by experience level?
- Is there a pattern between flight hours and how long astronauts lived?

Data source: [Kaggle - NASA Astronaut Yearbook](https://www.kaggle.com/nasa/astronaut-yearbook)

## The File

- **`AstronautQuery.sql`** — The full script. It creates the `astronauts` table, inserts every astronaut's record, and ends with a set of analysis queries (totals, averages, experience-level classification, and a risk profile breakdown using `CASE` and `AND/OR`).

You can run it locally with SQLite:

```bash
sqlite3 :memory: < AstronautQuery.sql
```

## GitHub Actions (CI/CD)

Two workflows run automatically every time code is pushed or a pull request is opened. They live in `.github/workflows/`.

### 1. Lint SQL (`lint.yml`)

This is a **style checker** for SQL. It uses a tool called `sqlfluff` to scan the `.sql` files and flag formatting issues — things like inconsistent capitalization, weird spacing, or non-standard syntax. It keeps the code tidy and easier to read.

If the lint fails, the check shows up red on GitHub so problems are caught before merging.

### 2. Test SQL (`test.yml`)

This is a **smoke test** that proves the script actually works. It:

1. Spins up a fresh Ubuntu machine.
2. Loads `AstronautQuery.sql` into an in-memory SQLite database.
3. Saves the query output to a file.
4. Checks that expected results (like the words `Elite` and `Died in Mission` from the classification queries) actually appear in the output.
5. Uploads the output as an artifact you can download from the GitHub Actions run.

If the SQL has a syntax error or a query breaks, this workflow fails and tells you something's wrong.

### Why this matters

Together these two workflows form a tiny **CI/CD pipeline**: every change is automatically linted and tested before it gets merged. That way the `master` branch always stays in a working state.
