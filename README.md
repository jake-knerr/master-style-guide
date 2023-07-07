# Master Style Guide <!-- omit in toc -->

Welcome to my master style guide.

## Copyright <!-- omit in toc -->

Jake Knerr © Ardisia Labs LLC

## Table of Contents <a id="toc" name="toc"></a> <!-- omit in toc -->

- [Style vs. Design](#style-vs-design)
- [Background](#background)
  - [Terms](#terms)
  - [English Language](#english-language)
  - [Code Examples](#code-examples)
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

- **prefer / discourage** (weaker suggestions)
- **always / avoid** (stronger suggestion)
  - Note, if you are already using the imperative mood, then words like "always" are optional. For example, "Use semicolons" is already imperative, no need for "always."
- **strongly / weakly** (use to adjust the strength of suggestion)
- **acceptable** (permissible)
- **Prefix optional rules with (Optional). Start sentence with "Consider".**
  - (Optional) Consider using ....

### English Language

#### Use Wikipedia's style guide to resolve any style questions.

[Wikipedia:Manual of Style](https://en.wikipedia.org/wiki/Wikipedia:Manual_of_Style)

> Why Wikipedia? Their guide is thorough, free, searchable, and accessible.

#### When choosing a national variety of English, prefer American English.

> Why? I am American.

### Code Examples

#### When illustrating the incorrect versus the correct way of coding, prefer the following language:

- **discouraged / preferred** (weaker)
- **avoid / good** (stronger)

**[⬆ Table of Contents](#toc)**

---

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

#### Divide up apps into feature/domain folders with a file in the root directory named `server` that bootstraps the server.

Optionally, a `.env` file at the root may be useful to store site secrets.

```
.env
/auth
/cars
/client
/customers
server.js
```

#### Common top-level folders:

- `/client` - the client application.
- `/site` - public website.
- `/types` - shared type definitions, enums, classes, and jsdoc definitions that do not fit cleanly into a feature folder.
- `/utils` - shared utils.
- `/validators` - shared validators.

#### Each top-level feature/domain folder prefers these sub-folders:

- `/routes` - post requests should use CRUD prefixes in the url. E.G. `/create-topic`
- `/controllers` - all exported functions use `handleXXX` as a naming scheme.
  - Prefer thin controllers and put business logic in the services.
  - Responses prefer a JSON response with the following signature: `{ok: boolean, error: string|string[]}`;
- `/models` - all exported functions use CRUD prefix names like `readData`, `updateData`, etc. Models are "dumb" and use simple CRUD functions. The services are smart.
  - Models are the gateway to the persistence layer. All SQL/DB code is in model functions.
- `/services` - exported functions are named using `get/set/add/remove` to distinguish them from model functions.
  - Services are the API that each feature uses to communicate with each-other, and they are the gateway to the model. Services are "smart" and models are "dumb". They provide the API for features to interact with one-another.
- `/views` - Templates, static view files, or the src for a SPA.
- `/public` - static files accessible by name.
  - Such files are not in `/views` because these can be accessed without a "view".
  - `/public/assets` - all static non-html files.
- `/validators` - all exported functions use `validateXXX` as a naming scheme. They validate and sanitize data in requests.
  - Validators are middleware used to validate data before it gets to the controllers.
  - They validate the shape of data so typically there are no hits to the database or services.
  - For errors, either throw `400`|`500` for tampering, or errors in an array on the `Request` object for handling by the controllers.
- `/types` - enums, classes, and jsdoc definitions that are specific to the feature, and can be used by other features.
- `/utils` - feature specific utilities.

#### Views and validators are contained within the same feature folder as the routes that use them.

I find it more intuitive for routes, validators, and views to be grouped because they are not shared between different feature modules. However, the service/model layer is shared and should be split up into each's respective feature folder.

```
/* avoid */
/admin
  /services/
    auth.js
/auth
  /views/
    admin-view-auth.ejs

/* good */
/admin
  /views/
    admin-view-auth.ejs
/auth
  /services/
    service-auth.js
```

#### It is permissible to merge the controllers into the routes if it improves code clarity.

I have found that separation of responsibilities between routing and controllers can result in useless complexity.

#### Always validate user submitted data.

Do not allow user tampering to crash the server.

**[⬆ Table of Contents](#toc)**

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
  *,
  FROM
  channels

# good
SELECT
  *,
FROM
  channels
```

#### Prefer to place statements, clauses, and expression keywords on their own line. Indent the remainder of the instructions.

If a clause is a compound clause (for example `JOIN` and `ON` or `ORDER BY` and `DESC`), then place the trailing part of the compound clause on its own line and indented.

> Why? This technique makes spotting the relevant keywords easier and simplifies wrapping line-overflow.

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
  GREATEST(
    minMoney,
    maxMoney
  )
FROM
  channels
WHERE
  id > 10
  AND userName = "Jake"
```

#### For multi-line parenthesis, prefer to place the leading parenthesis above the text it encloses and the trailing parenthesis alone on a new line.

```sql
# preferred
SELECT
  GREATEST(
    minMoney,
    maxMoney
  )
FROM
  channels
WHERE
  id > 10
  AND userName = "Jake"
```

#### Operators are inline. However, if either operand is multi-line then the operator should be placed alone on a newline with the operands left-aligned above and below.

```sql
# good
SELECT
  *
FROM
  users
UNION
SELECT
  *
FROM
  clients

# good
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
