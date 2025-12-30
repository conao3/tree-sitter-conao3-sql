# tree-sitter-sql

A [tree-sitter](https://tree-sitter.github.io/tree-sitter/) grammar for SQL, with a focus on PostgreSQL syntax.

## Overview

This parser provides accurate syntax highlighting, code navigation, and structural analysis for SQL files. It supports PostgreSQL-compatible DDL statements including `CREATE TABLE` with comprehensive type and constraint coverage.

## Features

- PostgreSQL data types (integers, text, JSON, arrays, timestamps, geometric types, and more)
- Column constraints (NOT NULL, PRIMARY KEY, UNIQUE, CHECK, DEFAULT, REFERENCES)
- Table constraints (PRIMARY KEY, FOREIGN KEY, UNIQUE, CHECK, EXCLUDE)
- Referential actions (CASCADE, SET NULL, SET DEFAULT, RESTRICT, NO ACTION)
- Generated columns (STORED and IDENTITY)
- Expression support including function calls, binary/unary operators, and type casting

## Installation

### Node.js

```bash
npm install tree-sitter-sql
```

### From Source

```bash
git clone https://github.com/conao3/tree-sitter-conao3-sql.git
cd tree-sitter-conao3-sql
npm install
```

## Usage

### Generate the Parser

```bash
tree-sitter generate
```

### Parse a SQL File

```bash
tree-sitter parse example.sql
```

### Node.js Example

```javascript
const Parser = require('tree-sitter');
const SQL = require('tree-sitter-sql');

const parser = new Parser();
parser.setLanguage(SQL);

const sourceCode = `
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email TEXT UNIQUE,
  created_at TIMESTAMP DEFAULT now()
);
`;

const tree = parser.parse(sourceCode);
console.log(tree.rootNode.toString());
```

## Development

### Prerequisites

- Node.js 14+
- tree-sitter CLI

### Testing

```bash
tree-sitter generate
tree-sitter test
```

### Project Structure

```
.
├── grammar.js          # Grammar definition
├── bindings/
│   ├── node/          # Node.js bindings
│   └── rust/          # Rust bindings
├── src/               # Generated parser source
└── queries/           # Syntax highlighting queries
```

## License

Apache-2.0
