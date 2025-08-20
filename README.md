# Master Style Guide <!-- omit in toc -->

Welcome to my master style guide.

## Copyright <!-- omit in toc -->

Jake Knerr © Ardisia Labs LLC

## Table of Contents <a id="toc" name="toc"></a> <!-- omit in toc -->

- [Style vs. Design](#style-vs-design)
- [Background](#background)
  - [Terms](#terms)
  - [English Language](#english-language)
- [Directories, Folder Structure, File names](#directories-folder-structure-file-names)
- [CSS and HTML](#css-and-html)
- [JavaScript](#javascript)
- [Node](#node)
- [NPM](#npm)
- [SQL](#sql)
- [Github](#github)
- [Front-End Development](#front-end-development)
- [Miscellaneous](#miscellaneous)
  - [Design Patterns](#design-patterns)

## Style vs. Design

Although this guide is called a style guide, it focuses on more than simply aesthetic issues like formatting. It also provides design guidance — styling with a purpose.

When is a rule a style rule? When is a rule a design rule? Like most decisions in artistic endeavors, the difference is a matter of judgment.

#### Style is usually more specific.

For example, "use semicolons after statements" opposed to "use domain-specific language" or "prefer higher-level abstractions."

#### Style is more focused on visuals.

In other words, style is more concerned with how information looks, rather than what it means or represents.

#### Style is more coupled to a particular language than design.

Different languages produce different style guides, but design invokes high-level abstractions that apply to many languages.

#### Style does not trigger side effects.

For example, choosing to put a blank line before a _return_ statement does not trigger code refactoring.

#### Many rules are edge cases that can be classified as style or design (or both) by reasonable developers.

> Why are these distinctions important? It is good practice to question design decisions, to consider different design approaches, and to understand design decisions. It is not essential to spend mental capital on styling decisions.

**[⬆ Table of Contents](#toc)**

---

## Background

### Terms

#### Prefer the following terms when describing rules:

- **discouraged, preferred** (weaker suggestions)
- **avoid, good** (stronger suggestion)
- **weakly / strongly** (use to adjust the strength of suggestion)
- **acceptable** (permissible)
- **Prefix optional rules with (Optional). Start sentence with "Consider".**
  - (Optional) Consider using ....

### English Language

#### Use Wikipedia's style guide to resolve any style questions.

[Wikipedia:Manual of Style](https://en.wikipedia.org/wiki/Wikipedia:Manual_of_Style)

> Why Wikipedia? Their guide is thorough, free, searchable, and accessible.

#### When choosing a national variety of English, prefer American English.

> Why? I am American.

## Directories, Folder Structure, File names

See the naming guide in the [JS guide](https://github.com/jake-knerr/js-style-guide).

**[⬆ Table of Contents](#toc)**

---

## CSS and HTML

See [CHESS](https://github.com/jake-knerr/chess).

**[⬆ Table of Contents](#toc)**

---

## JavaScript

See [JavaScript Style Guide](https://github.com/jake-knerr/js-style-guide).

**[⬆ Table of Contents](#toc)**

---

## Node

See [JavaScript Style Guide](https://github.com/jake-knerr/js-style-guide).

**[⬆ Table of Contents](#toc)**

---

## NPM

#### Package names are all lowercase.

**[⬆ Table of Contents](#toc)**

---

## SQL

#### Use a 80 character column width.

#### Use public ids that are unguessable.

#### Database names, table names, and column names use nouns.

> Why? Because databases store data, which are "things".

#### Database and table names use lower snake-case.

> Why use lowercase? Many databases are configured to require lowercase.

> Why use snake-case? Because it is the SQL standard convention.

#### Column names are named using lower-camel-case.

> Why? The data more easily maps to JSON and JavaScript naming conventions.

#### Definitions Overview

A **statement** is the complete instruction you give to the database. It usually ends with a semicolon (;) and tells the database to do something (query data, insert, update, delete, etc.).

```sql
SELECT * FROM users;
INSERT INTO users (id, name) VALUES (1, 'Alice');
UPDATE users SET name = 'Bob' WHERE id = 1;
DELETE FROM users WHERE id = 1;
```

A **clause** is a building block of a statement.

Think of clauses as keywords that define parts of the statement. A single statement is usually composed of multiple clauses.

```sql
SELECT – defines which columns to return
FROM – defines which table(s) to use
WHERE – filters rows
GROUP BY – groups rows
HAVING – filters groups
ORDER BY – sorts rows
LIMIT – restricts number of results
```

An **expression** is a combination of symbols that evaluates to a value.

Expressions can appear inside clauses.

```sql
Literal: 42, 'Alice'
Column reference: users.name
Arithmetic expression: price * quantity
Logical expression: age > 18 AND active = 1
Function call: COUNT(*), LOWER(name)
Case expression: CASE WHEN score >= 60 THEN 'Pass' ELSE 'Fail' END
```

Example inside a statement:

```sql
SELECT name, price * quantity AS total
FROM orders
WHERE quantity > 10 AND status = 'shipped';
```

An **operator** in SQL is a symbol or keyword that tells the database how to combine, compare, or manipulate values in an expression.

They are the "glue" inside expressions, and they always work on operands (which can be column references, literals, or results of other expressions).

Arithmetic Operators

```sql
+, -, *, /, %
```

Comparison Operators – compare values (return true/false/unknown)

```sql
=, <>, !=, > , < , >= , <=, BETWEEN, AND, LIKE, IN, IS NULL
```

Logical Operators – combine boolean results

```sql
AND, OR, NOT
```

Set Operators – work between result sets (apply between queries, not columns)

```sql
UNION, UNION ALL, INTERSECT, EXCEPT
```

#### SQL keywords are capitalized in queries.

> Why? This creates strong contrast with the lowercase table and column names.

```sql
# avoid
select *
from table;

# good
SELECT *
FROM table;
```

#### Prefer left-alignment at the same syntactic level.

> Why? Left alignment is much easier to maintain than right-alignment. Especially for SQL written in raw strings.

```sql
# discouraged
SELECT *
  FROM channels

# preferred
SELECT *
FROM channels
```

#### Prefer to place clauses on their own line.

> Why? This technique makes it easy to see the keywords, the instructions and simplifies line-wrapping.

```sql
# discouraged
SELECT * FROM channels
JOIN channels_users ON channels.id = channels_users.channel_id AND channels.date = channels_users.date
GROUP BY
  channels.id

# preferred
SELECT *
FROM channels
JOIN channels_users
  ON channels.id = channels_users.channel_id # another clause
  AND channels.date = channels_users.date
GROUP BY channels.id
```

#### Prefer to place solitary expressions on the same line as the clause and place multiple expressions on separate lines.

Functions can be place on a single line if they fit in the column width.

```sql
# discouraged
SELECT id, userName, userLocation,
  GREATEST(
    minMoney,
    maxMoney
  ) AS greatest
FROM
  channels
WHERE id > 10 AND userName = "Jake"

# preferred
SELECT
  id,
  userName,
  userLocation,
  GREATEST (minMoney, maxMoney) AS greatest
FROM channels
WHERE
  id > 10
  AND userName = "Jake"
```

#### When multi-line parenthesis are used, prefer to place the leading parenthesis above the text it encloses and the trailing parenthesis on a new line.

Place a space between adjacent keywords and the parenthesis.

```sql
# discouraged
SELECT
  GREATEST (aReallyLongName, anotherEvenLongerName, wowTheseNamesAreGettingRidiculous) AS greatest

# discouraged
SELECT
  GREATEST (aReallyLongName,
    anotherEvenLongerName, wowTheseNamesAreGettingRidiculous) AS greatest

# preferred
SELECT
  GREATEST (
    aReallyLongName,
    anotherEvenLongerName,
    wowTheseNamesAreGettingRidiculous
  ) AS greatest
```

#### Operators are inline. However, if either operand is multi-line then the operator should be placed alone on a newline with the operands left-aligned above and below.

Prefer to place logical operators at the start of the line.

```sql
# good - UNION is multi-line
SELECT *
FROM users
UNION
SELECT*
FROM clients

# good - LIKE is single line
SELECT *
FROM users
WHERE userName LIKE "%j%"
```

**[⬆ Table of Contents](#toc)**

---

#### Place trailing keywords on the same line.

```sql
# discouraged
ORDER BY jingle
  DESC

#preferred
ORDER BY jingle DESC
```

## Github

#### Repository names are all lowercase.

**[⬆ Table of Contents](#toc)**

---

## Front-End Development

See [Cogent](https://github.com/jake-knerr/cogent).

**[⬆ Table of Contents](#toc)**

---

## Miscellaneous

### Design Patterns

- [Gang of Four (GoF) Design Patterns in JavaScript](https://github.com/jake-knerr/gof-design-patterns-js)

**[⬆ Table of Contents](#toc)**

---
