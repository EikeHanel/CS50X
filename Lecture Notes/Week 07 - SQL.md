# SQL
- **Notes:** https://cs50.harvard.edu/x/2024/notes/7/
- SQL is a language specifically for databases!

## 1. flat-file database
- Like a .txt file containing the data, separated by a **delimiter**
- **Delimiter**:
  - CSV - Comma-separated values
      - First row is a **header**

## 1.1 csv with python
- Printing data
    ```py
    import csv

    with open("favorites.csv", "r") as file:
        reader = csv.DictReader(file)
        for row in reader:
            print(row["language"])
    ```
- Counting entries:
    ```py
    import csv

    with open("favorites.csv", "r") as file:
        reader = csv.reader(file)
        scratch, c, python = 0, 0, 0

        for row in reader:
            fav = row[1]
            if fav == "Scratch":
                scratch += 1
            elif fav == "C":
                c += 1
            elif fav == "Python":
                python += 1
    print(f"Scratch: {scratch}\nC: {c}\nPython: {python}")
    ```
- A better way to Count entries:
    ```py
    import csv

    with open("favorites.csv", "r") as file:
        reader = csv.DictReader(file)
        counts = {}

        for row in reader:
            fav = row["language"]
            if fav in counts:
                counts[fav] += 1
            else:
                counts[fav] = 1

    for fav in sorted(counts, key=counts.get, reverse=True):
        print(f"{fav}: {counts[fav]}")
    ```
- Still a better way to Count:
    ```py
    import csv
    from collections import Counter

    with open("favorites.csv", "r") as file:
        reader = csv.DictReader(file)
        counts = {}

        for row in reader:
            fav = row["language"]
            counts[fav] += 1

    for fav, count in counts.most_common():
        print(f"{fav}: {count}")
    ```

## 2. relational database
- "3D" database
  - Multiple sheets possible
- SQL is a "CRUD" language
  - CREATE, INSERT
  - READ, SELECT
  - UPDATE
  - DELETE, DROP
  - This makes the language relatively small in keywords/arguments

- Data type
  - .sqlite

### 2.1 Create and update a table with sqlite3
- **Terminal command**:
    ```
    Week-07/ $ sqlite3 favorites.db
    Are you sure you want to create favorites.db? [y/N] y
    sqlite> .mode csv
    sqlite> .import favorites.csv favorites
    sqlite> .quit
    ```
    - Week-07/ $ sqlite3 favorites.db
      - Creates the empty .db file
    - sqlite> .mode csv
      - changes the mode to csv
    - sqlite> .import favorites.csv favorites
      - imports "favorites.csv" with the table name "favorites"
    - sqlite> .quit
      - quit

### 2.2 Access data via sqlite3
- **Terminal command**:
    ```
    Week-07/ $ sqlite3 favorites.db
    sqlite> .schema
    CREATE TABLE IF NOT EXISTS "favorites"(
    "Timestamp" TEXT, "language" TEXT, "problem" TEXT);
    sqlite> SELECT * FROM favorites;
    sqlite> SELECT language FROM favorites LIMIT 10;
    ```
  - Week-07/ $ sqlite3 favorites.db
    - opens the database
  - sqlite> .schema
    - shows the schema of the database 
  - sqlite> SELECT * FROM favorites;
    - **Semicolon** is back 
    - opens all columns form the table favorites
        ```sql
        +---------------------+----------+----------------+
        |      Timestamp      | language |    problem     |
        +---------------------+----------+----------------+
        | 10/30/2023 13:38:01 | Python   | Hello, World   |
        | 10/30/2023 13:38:03 | Python   | DNA            |
        | 10/30/2023 13:38:03 | Python   | Hello, World   |
        | 10/30/2023 13:38:05 | Scratch  | Scratch        |
        ...
        ...
        ...
        | 10/30/2023 13:41:05 | C        | Inheritance    |
        | 10/30/2023 13:41:09 | C        | Sort           |
        | 10/30/2023 13:41:21 | C        | Sort           |
        +---------------------+----------+----------------+
        ```
  - sqlite> SELECT language FROM favorites LIMIT 10;
    - get the first 10 data points from the language column
        ```sql
        +----------+
        | language |
        +----------+
        | Python   |
        | Python   |
        | Python   |
        | Scratch  |
        | Python   |
        | Python   |
        | Python   |
        | Python   |
        | Python   |
        | Python   |
        +----------+
        ```

### 2.3 SQL keywords
- **AVG**
  - Calculated the average of the specified column

- **COUNT**
  - Count entires, i.e. number of rows

- **DISTINCT**
  - Displayes the unique entires in the column

- **LOWER**
  - Force everything to lower-case

- **MAX**
  - Find max value

- **MIN**
  - Find min value

- **UPPER**
  - Force everything to upper-case
  
- **WHERE**
  - Filtering the data
  - sqlite> SELECT COUNT(\*) FROM favorites WHERE language = 'C' AND problem = 'Hello, World';
    ```sql
    +----------+
    | COUNT(*) |
    +----------+
    | 7        |
    +----------+
    ```

- **LIKE**
  - Used to search for a specific pattern within a column
    - % matches zero or more characters
    - _ matches exactly one character
  - sqlite> SELECT name FROM users WHERE name LIKE 'A%';
    ```sql
    +--------+
    | name   |
    +--------+
    | Alice  |
    | Alan   |
    +--------+
    ```

- **ORDER BY**
  - Order by the selected column
  - sqlite> SELECT language, COUNT(\*) FROM favorites GROUP BY language ORDER BY COUNT(\*) DESC;
  - **ASC** - Ascending; **DESC** - Descending Order
    ```sql
    +----------+----------+
    | language | COUNT(*) |
    +----------+----------+
    | Python   | 280      |
    | C        | 78       |
    | Scratch  | 40       |
    +----------+----------+
    ```

- **LIMIT**
  - Limits the output

- **GROUP BY**
  - Groups by the selceted column 
  - sqlite> SELECT language, COUNT(\*) FROM favorites GROUP BY language;
    ```sql
    +----------+----------+
    | language | COUNT(*) |
    +----------+----------+
    | C        | 78       |
    | Python   | 280      |
    | Scratch  | 40       |
    +----------+----------+
    ```

- **AS**
  - "Rename" function
  - sqlite> SELECT language, COUNT(*) AS n FROM favorites GROUP BY language ORDER BY n DESC;
    ```sql
    +----------+-----+
    | language |  n  |
    +----------+-----+
    | Python   | 280 |
    | C        | 78  |
    | Scratch  | 40  |
    +----------+-----+
    ```

### 2.4 Insert/Delete into a table
- **Insert** a row:
  - sqlite> INSERT INTO favorites(language, problem) VALUES('SQL', 'Fiftyville');
  - sqlite> SELECT * FROM favorites;
    ```sql
    | 10/30/2023 13:41:05 | C        | Inheritance    |
    | 10/30/2023 13:41:09 | C        | Sort           |
    | 10/30/2023 13:41:21 | C        | Sort           |
    | NULL                | SQL      | Fiftyville     |
    +---------------------+----------+----------------+
    ```
- **Delete**:
  - **NEVER DO:**
    - sqlite> DELETE FROM favorites;
    - This deletes every datapoint from favorites
- **Delete** a specified row/rows, using **WHERE**
  - sqlite> DELETE FROM favorites WHERE Timestamp IS NULL;
    ```sql
    | 10/30/2023 13:41:05 | C        | Inheritance    |
    | 10/30/2023 13:41:09 | C        | Sort           |
    | 10/30/2023 13:41:21 | C        | Sort           |
    +---------------------+----------+----------------+
    ```

### 2.5 Update
- Update whole table also **DESTRUCTIVE**
  - sqlite> UPDATE favorites SET language = 'SQL', problem = 'Fiftyville';
    ```sql
    +---------------------+----------+------------+
    |      Timestamp      | language |  problem   |
    +---------------------+----------+------------+
    | 10/30/2023 13:38:01 | SQL      | Fiftyville |
    | 10/30/2023 13:38:03 | SQL      | Fiftyville |
    | 10/30/2023 13:38:03 | SQL      | Fiftyville |
    ...
    ...
    ...
    | 10/30/2023 13:41:05 | SQL      | Fiftyville |
    | 10/30/2023 13:41:09 | SQL      | Fiftyville |
    | 10/30/2023 13:41:21 | SQL      | Fiftyville |
    +---------------------+----------+------------+
    ```
- **Always double check what you update/delete**
  

## 3. How a Database stores data (tablewise)
- Assume we want to create a TV-show database:
  - table 1 -> shows
  - table 2 -> people
  - table 3 -> stars
- **shows table**:
    id        | show         
    ----------|--------------
    386676    | The Office   
- **people table**:
    id        | name
    ----------|--------------
    136797    | Steve Carell
    933988    | Rainn Wilson
    1024677   | John Krasinski
    278979    | Jenna Fischer
    1145983   | B.J. Novak
- **star table**:
    show_id   | person_id
    ----------|--------------
    386676    | 136797
    386676    | 933988
    386676    | 1024677
    386676    | 278979
    386676    | 1145983

With this you can relate the show and actors(stars) due to the star table. The star table is associating the show_id with the person_id. This is done because numbers are way more efficiantly to store than strings. Here, "The Office" -> 11 Bytes **while** 386676 -> 4 bytes.
This avoids dublication of data, i.e. Normalizing the data.

## 4. IMDb data
- I could not download the database.
- Video content starts at ~ https://www.youtube.com/watch?v=1RCMYG8RUSE&t=4080

### 4.1 One to One relationship
- Show - Rating
  - Every show has one rating
  - Show has 
    - PRIMARY KEY (id)
  - Rating has
    - FOREIGN KEY (show_id)

### 4.2 One to Many relationship
- Show - Genres
  - One show can have many genres!

### 4.3 Many to Many relationship
- Show - Person 
  - A show can have multiple actors
  - An actor can star in multiple shows

## 5. Datatypes + Keywords
- **BLOB**
  - binary large object - basically a file
- **INTEGER**
  - int
- **NUMERIC**
  - dates, times
- **REAL**
  - basically float
- **TEXT**
  - strings

---

- **NOT NULL**
  - must be filled
- **UNIQUE**
  - cant be a duplicate
- **PRIMARY KEY**
  - a unique id for the specific table
- **FOREIGN KEY**
  - the presents of a PRIMARY KEY in a different table 
----
- PRIMARY and FORGEING KEYs can be identified by e.g. calling 
    ```sql
    sqlite>.schema ratings
    CREATE TABLE ratings(
        show_id INTEGER NOT NULL,
        rating REAL NOT NULL,
        votes INTEGER NOT NULL,
        FOREIGN KEY(show_id) REFERENCES shows(id)
    );
    ```
## 6. Nested Queries
- IN - used to check for id == (show_id with rating >= 6.0)
    ```sql
    sqlit> SELECT * FROM shows WHERE id IN
    ...> (SELECT show_id FROM ratings WHERE rating >= 6.0);
    ```
### 6.1 JOIN
- Getting a table with Title and Rating
    ```sql
    SELECT title, rating FROM shows JOIN ratings ON shows.id = ratings.show_id WHERE rating >= 6.0 LIMIT 10;
    ```

### 6.2 JOIN creates tmp duplicates when a One to Many relationship exists
- By making this query
    ```sql
    SELECT * FROM shows JOIN genres ON shows.id = genres.show_id WHERE id = 63881;
    ```
- We get:
    ```
    +-------+-----------+------+----------+---------+-----------+
    |  id   |   title   | year | episodes | show_id |   genre   |
    +-------+-----------+------+----------+---------+-----------+
    | 63881 | Catweazle | 1970 |       26 |   63881 | Adventure |
    | 63881 | Catweazle | 1970 |       26 |   63881 | Comedy    |
    | 63881 | Catweazle | 1970 |       26 |   63881 | Family    |
    +-------+-----------+------+----------+---------+-----------+
    ```

### 6.3 Get everything about "The Office"
- Explaination in steps:
- Finding the correct show id:
    ```sql
    SELECT * FROM shows WHERE title = 'The Office';
    ```
    ```sql
    SELECT * FROM shows WHERE title = 'The Office' AND year = 2005;
    ```
- Getting the person id's starring in "The Office"
    ```sql
    SELECT person_id FROM stars WHERE show_id = 
    (SELECT id FROM shows WHERE title = 'The Office' AND year = 2005);
    ```
- Getting the name through the person_id
    ```sql
    SELECT name FROM people WHERE id IN
     (SELECT person_id FROM stars WHERE show_id = 
      (SELECT id FROM shows WHERE title = 'The Office' AND year = 2005));
    ```

---

- Going the reverse way 
    ```sql
    SELECT title FROM shows WHERE id IN
     (SELECT show_id FROM stars WHERE person_id = 
      (SELECT id FROM people WHERE name = 'Steve Carell'));
    ```

### 6.4 JOIN 3 tables
- Using two JOIN parts
    ```sql
    SELECT title FROM shows
    JOIN stars ON shows.id = stars.show_id
    JOIN people ON stars.person_id = people.id
    WHERE name = 'Steve Carell';
    ```
- A simpler way:
    ```sql
    SELECT title, FROM shows, stars, people
    WHERE shows.id = stars.show_id
    AND people.id = stars.person_id
    AND name = 'Steve Carell';
    ```

## 7. Timing / Index
### 7.1 Timing
- You can time the queries by using: (**Terminal Command**)
    ```
    sqlite> .timer ON
    ```
- This only works with sqlite3 (.'method' command)

- **Example**:
  ```sql
  SELECT * FROM shows WHERE title = 'The Office';
  ```
- Timing Result: 0.044 seconds

### 7.2 Index
- CREATE INDEX name ON table (column, ...);

To increase the speed indexing is used!
- title index
    ```sql
    CREATE INDEX title_index ON shows (title);
    ```
- **Index Example**:
  ```sql
  SELECT * FROM shows WHERE title = 'The Office';
  ```
- Timing Result: 0.000 seconds

This makes the searching so much faster! Saves Money! Because the same server can handle way more people.

When creating an **Index** you create whats called a B-tree. A "short", "fat" tree. Lots of children, with minimal height.



## 8. sqlite3 with Python

```py
from cs50 import SQL

db = SQL("sqlite:///favorites.db")
fav = input("Favorite: ")
rows = db.execute("SELECT COUNT(*) AS n FROM favorites WHERE problem = ?", fav)

row = rows[0]

print(row["n"])
```