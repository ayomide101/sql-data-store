# 🌍 SQL-Seed-Data Repository

This repository provides a growing collection of ready-to-use SQL files that help developers and database administrators quickly seed their databases with useful reference tables. These include global datasets such as:

- 🌐 Countries
- 🏙️ States and Provinces
- 🛫 Airports
- 📍 Cities
- 📦 Currencies

Each SQL file contains both the **schema definition** (with optimized indexing) and **data inserts** for maximum performance and convenience across most SQL database engines.

---

## 🚀 Features

### ✅ Plug & Play SQL Files
Each `.sql` file is ready to be executed directly in your database environment. Simply run the file using your favorite SQL client or CLI (e.g., `psql`, `mysql`, `sqlite3`, etc.).

### 🔧 Predefined Indexes
To improve query performance, tables come with thoughtfully chosen `PRIMARY KEY` and `KEY` (index) definitions. You don’t need to worry about optimization — it’s already baked in.

### 🏗️ Structured Table Definitions
Tables are created with sensible defaults, proper data types, and constraints like `NOT NULL`, `ENUM`, `AUTO_INCREMENT`, etc., to ensure data integrity and ease of querying.

### 📌 Universal Compatibility
Although syntax might vary slightly across SQL dialects, the structure follows broadly supported standards to ensure compatibility with most popular SQL databases such as MySQL, PostgreSQL, MariaDB, and SQLite (minor adjustments may be required).

---

## 📂 Available Datasets

- `airports.sql`: Worldwide airport directory including heliports, small/medium/large airports
- `countries.sql`: Country data with ISO codes and regions
- `states_provinces.sql`: US States and global provinces with associated countries

## ⚙️ Usage

1. Clone the repository:
```bash
   git clone https://github.com/ayomide101/sql-data-store.git
   cd sql-data-store
```   

## 🧰 Example Usage

To seed your database with airport data:

```bash
mysql -u your_user -p your_database < airports.sql
```

Or in PostgreSQL:
```bash
psql -U youruser -d yourdb -f airports.sql
```

Or, from within a SQL client:

```sql
SOURCE path/to/airports.sql;
```

This will create the `airports` table and populate it with thousands of records, complete with indexing on important fields like `ident` and `country`.

---

## 📄 File Structure

Each SQL file includes:

1. **Table Creation** – A `CREATE TABLE` statement with proper column types and indexing.
2. **Data Inserts** – Thousands of rows of insert statements populated from trusted public data sources.

Sample snippet from `airports.sql`:

```sql
CREATE TABLE IF NOT EXISTS airports (
  autoId INT NOT NULL AUTO_INCREMENT,
  id INT NOT NULL,
  ident VARCHAR(15) NOT NULL,
  type ENUM('heliport', 'small_airport', 'seaplane_base', 'balloonport', 'closed', 'medium_airport', 'large_airport') NOT NULL DEFAULT 'small_airport',
  name VARCHAR(150) NOT NULL,
  location POINT NOT NULL,
  ...
  PRIMARY KEY (id),
  KEY airport_ident (ident),
  KEY airport_country (country)
);

INSERT INTO airports SET id='6523', ident='00A', type='heliport', name='Total RF Heliport', ...;
```

---

## 🛠️ Customization

If you need to:

- Change data types to match your engine
- Add additional indexes for your use case
- Filter or reduce the dataset

Feel free to fork the repo and modify the `.sql` files accordingly.

---

## 📦 Planned Datasets

- 🌍 Timezones
- 🗣 Languages
- 🏢 Company Types
- 🎓 Education Levels
- 💳 Payment Methods

Pull requests are welcome for additional datasets!

---

## 🔍 Query Examples

### 1. Find a specific airport by ICAO code:
```sql
SELECT * FROM airports WHERE icao_code = 'KJFK';
```

### 2. List all airports in Canada:
```sql
SELECT name, municipality FROM airports WHERE iso_country = 'CA';
```

### 3. Full-text search for airports matching "Heathrow":
```sql
SELECT name, municipality FROM airports
WHERE MATCH(name, municipality) AGAINST('Heathrow' IN NATURAL LANGUAGE MODE);
```

### 4. Count airports per country:
```sql
SELECT country, COUNT(*) AS total_airports
FROM airports
GROUP BY country
ORDER BY total_airports DESC;
```

---

## 🤝 Contributing

Want to add a new dataset or improve an existing SQL structure? Please open a pull request or issue with your suggestion. Contributions that include:

- Accurate data
- Well-indexed schema
- Compatible syntax

...are highly appreciated!

---

## 📜 License

This repository is licensed under the GNU GENERAL PUBLIC License.

---

## 🙏 Acknowledgments & Data Sources

This project compiles and structures public domain and openly licensed data for easy use in SQL-based systems.

Data sources include:

- [OpenFlights](https://openflights.org/data.html) — for global airport and airline data
- [Geonames](https://www.geonames.org/) — for cities, countries, and regional geographic data
- [ISO](https://www.iso.org/iso-3166-country-codes.html) — for standardized country and region codes
- [UN/LOCODE](https://unece.org/trade/cefact/unlocode) — for city and port codes
- [Wikipedia](https://en.wikipedia.org/) and government open data portals — for curated data

---

Happy querying! ✨

