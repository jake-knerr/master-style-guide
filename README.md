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

#### Column names are named using the same conventions as laid out in the [JavaScript Style Guide](https://github.com/jake-knerr/js-style-guide) for data.

> Why? The data more easily maps to JSON and JavaScript naming conventions.

#### SQL keywords are capitalized in queries.

> Why? This creates strong contrast with the lowercase table and column names.

```sql
# avoid
select *
  from table;

# good
SELECT
  *
FROM
  table;
```

#### Prefer left-alignment at the same syntactic level.

> Why? Left alignment is much easier to maintain than right-alignment. Especially for SQL written in raw strings.

```sql
# discouraged
SELECT
  *
  FROM
  channels

# preferred
SELECT
  *
FROM
  channels
```

#### Prefer to place statements, clauses, and expression keywords on their own line. Indent the remainder of the instruction.

If a clause is a compound clause (for example `JOIN` and `ON` or `ORDER BY` and `DESC`), then place the trailing part of the compound clause on its own line and indented.

> Why? This technique makes it easy to see the keywords, the instructions and simplifies line-wrapping.

```sql
# discouraged
SELECT *,
FROM channels
JOIN channels_users ON channels.id = channels_users.channel_id
GROUP BY channels.id

# preferred
SELECT
  *,
FROM
  channels
JOIN
  channels_users
  ON
    channels.id = channels_users.channel_id
GROUP BY
  channels.id
```

#### Prefer to place each condition and argument on a separate line.

Single argument functions can be on one line.

```sql
# discouraged
SELECT
  id, userName, userLocation, GREATEST(minMoney, maxMoney)
FROM
  channels
WHERE
  id > 10 AND userName = "Jake"

# preferred
SELECT
  id,
  userName,
  userLocation,
  GREATEST (
    minMoney,
    maxMoney
  )
FROM
  channels
WHERE
  id > 10
  AND userName = "Jake"

# acceptable
SELECT
  COUNT(*) AS totalCount
```

#### For multi-line parenthesis, prefer to place the leading parenthesis above the text it encloses and the trailing parenthesis on a new line.

Place a space between adjacent keywords and the parenthesis.

```sql
# preferred
SELECT
  GREATEST (
    minMoney,
    maxMoney
  )
```

#### Operators are inline. However, if either operand is multi-line then the operator should be placed alone on a newline with the operands left-aligned above and below.

Prefer to place logical operators at the start of the line.

```sql
# good - UNION is multi-line
SELECT
  *
FROM
  users
UNION
SELECT
  *
FROM
  clients

# good - LIKE is single line
SELECT
  *
FROM
  users
WHERE
  userName LIKE "%j%"
```

**[⬆ Table of Contents](#toc)**

---

## Github

#### Repository names are all lowercase.

**[⬆ Table of Contents](#toc)**

---

## Miscellaneous

### Design Patterns

- [Gang of Four (GoF) Design Patterns in JavaScript](https://github.com/jake-knerr/gof-design-patterns-js)
- [Cogent](https://github.com/jake-knerr/cogent)

**[⬆ Table of Contents](#toc)**

---
