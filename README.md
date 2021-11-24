# Blotli Style Guide <!-- omit in toc -->

Welcome to the master style guide for Blotli.

## Copyright <!-- omit in toc -->

© Jake Knerr at Blotli.

## Table of Contents <a id="toc" name="toc"></a> <!-- omit in toc -->

- [Style vs. Design](#style-vs-design)
- [Background](#background)
  - [Terms](#terms)
  - [English Language](#english-language)
  - [Code Examples](#code-examples)
- [Assets](#assets)
- [CSS and HTML](#css-and-html)
- [Directories, Folder Structure](#directories-folder-structure)
- [Github](#github)
- [JavaScript](#javascript)
- [NPM](#npm)
- [SQL](#sql)
- [URLs](#urls)
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

#### Prefer the following terms when describing rules

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

> Why? Blotli is located in the United States.

### Code Examples

#### When illustrating the incorrect versus the correct way of coding, prefer the following language:

- **discouraged / preferred** (weaker)
- **avoid / good** (stronger)

**[⬆ Table of Contents](#toc)**

---

## Assets

#### Asset files' (images, sounds, documents, binaries, etc.) names use lowercase and kebab-case.

```
// avoid
Report.PDF
dingDong.wav
RUN.exe
photoMASSIVE.ImG

// good
report.pdf;
ding-dong.wav;
run.exe;
photo-massive.img;
```

**[⬆ Table of Contents](#toc)**

---

## CSS and HTML

See [CHESS](https://github.com/blotli/chess).

**[⬆ Table of Contents](#toc)**

---

## Directories, Folder Structure

#### Directories names use lowercase and kebab-case.

> Why? This convention provides maximum compatibility across platforms.

```
// avoid
/Jake's Folder/

// good
/jakes-folder/
```

**[⬆ Table of Contents](#toc)**

---

## Github

#### Repository names are all lowercase.

**[⬆ Table of Contents](#toc)**

---

## JavaScript

See [Blotli JavaScript Style Guide](#).

**[⬆ Table of Contents](#toc)**

---

## NPM

#### Package names are all lowercase.

**[⬆ Table of Contents](#toc)**

---

## SQL

#### Use a 80 character column width.

#### Use public ids that are unguessable.

#### Database table and column names use lowercase and snake_case.

```sql
# avoid
Big_Database: Table_name: Field_One, field_Two
primarytable: Field1, fieldtwo

# good
big_database: table_name: field_one, field_two
primary_table: field_1, field_two
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

#### Prefer to place one SQL keyword per line and horizontally align all the keywords at the same syntactic level.

> Why? This makes the query easy to read.

```sql
# preferred
   SELECT channels.*,
          COUNT(messages.id) as messages_count,
          (SELECT COUNT(channels_users.id)
            FROM channels_users
            WHERE channels_users.channel_id = channels.id) as user_count
     FROM channels
     JOIN channels_users
       ON channels.id = channels_users.channel_id
      AND channels_users.user_id = ?
LEFT JOIN messages
       ON messages.channel_id = channels.id
 GROUP BY channels.id
```

#### Prefer to wrap overflowing queries but do not indent.

```sql
# preferred
SELECT id, long_column_name, event_longer_table_name,
       absurdly_long_table_name, gigantic_table_name,
       ridiculously_long_table name
  FROM channels
```

**[⬆ Table of Contents](#toc)**

---

## URLs

#### Prefer lowercase snake_case for API URLs. For all other HTTP URLs, prefer lowercase kebab-case.

```
// discouraged
http://xyz.com/getDocs.html

// preferred
http://xyz.com/get-docs.html

// discouraged
http://rest.api.com/multi-TIER-docs

// preferred
http://rest.api.com/multi_tier_docs
```

**[⬆ Table of Contents](#toc)**

---

## Miscellaneous

### Design Patterns

- [Gang of Four (GoF) Design Patterns in JavaScript](https://github.com/blotli/gof-design-patterns-js)
- [View Component Design Pattern](https://github.com/blotli/view-component-design-pattern)

**[⬆ Table of Contents](#toc)**

---
