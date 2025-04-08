# PostgreSQL/TimescaleDB Corruption Checker

A simple command-line tool to check PostgreSQL and TimescaleDB database
connections and verify database health.

## Features

- Connect to PostgreSQL/TimescaleDB databases
- PSQL-like command-line interface
- Support for .pgpass files for password management
- Support for standard PostgreSQL connection parameters

## Installation

### Using Deno

```bash
deno install -A -n pg-corruption-checker jsr:@langpavel/pg-corruption-checker
```

### From Source

```bash
git clone https://github.com/langpavel/pg-corruption-checker.git
cd pg-corruption-checker
deno task run --help
```

### As a Library

```typescript
import { check } from "@langpavel/pg-corruption-checker";

// Check with connection string
const result1 = await check("postgres://user:pass@localhost:5432/dbname");

// Check with options object
const result2 = await check({
  host: "localhost",
  port: 5432,
  database: "mydb",
  username: "user",
  password: "pass"
});
```

## Usage

```
Usage:
  deno run --allow-net --allow-env --allow-read jsr:@langpavel/pg-corruption-checker [OPTIONS] [DBNAME]

Connection options:
  -h, --host=HOSTNAME      Database server host
  -p, --port=PORT          Database server port
  -d, --dbname=DBNAME      Database name (can also be provided as positional argument)
  -U, --username=USERNAME  Database user name
  -W, --password=PASSWORD  Database password (can be loaded from ~/.pgpass)
  -c, --connection=STRING  Connection string (overrides other options)

Other options:
  --help                   Show this help message
  -v, --version            Show program version

Password management:
  If no password is provided, the tool will try to load it from
  the ~/.pgpass file, following the same rules as psql.

Examples:
  deno run -A jsr:@langpavel/pg-corruption-checker -h localhost -p 5432 -U postgres mydb
  deno run -A jsr:@langpavel/pg-corruption-checker -h localhost -U postgres -d mydb
```

## License

MIT
