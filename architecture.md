# Architecture Specification
### The CLARIAH Structured Data Hub


#### History
Predicate | Object
--------- | --------------
Status    | **DRAFT**
Version:  | 0.1
Date:     |
Author:   | Rinke Hoekstra


## Introduction

The CLARIAH Structured Data Hub is at its core, a Linked Data repository for data of interest to the Social History domain.

The data largely consists of statistics (e.g. census data), and is typically *tabular* in nature, i.e. it is described as tables, and contains both numbers and strings. The strings are often *names* that are used to denote entities that may be referred to from multiple datasets. Examples are *places* and *occupations*. Such names are called *codes* if they are defined in standardized *code lists*.

The aim of the Structured Data Hub is to be a platform that allows the storage and publication of this data in a way that datasets are *connected* through shared *names*.



For this domain, we distinguish three levels of description: **micro** data of individual persons, **macro** data, aggregated at municipal, provincial and country levels, and **meso** data, aggregated at a level in between micro and macro (e.g. organisations such as corporations).

#### Micro Data
In its normalized form cross-sectional micro data is captured in a table where the different variables are column headers, and each described entity (typically a person) forms a record along a single row.

For example:

Family name | Occupation | Age        | Gender
----------- | ---------- | ---------- | ------
Zijdeman    | researcher | 38         | m
...         | ...        | ...        | ...

In terms of variables and codes:

Variable A | Variable B | Variable C | Variable D
---------- | ---------- | ---------- | ----------
string     | code       | number     | code

Some micro data is longitudinal in nature, meaning that variables/events are dated. Such data can have a number of forms. One is a subject-date-event structure.

Subject  | Date | Event
---------|------|------
Zijdeman | 1977 | Born
...      | .... | ...

If on the other hand this is organised by source, it can take a slightly different form:

Subject | Date | Variable  | Value
--------|------|-----------|-------
Zijdeman| 1980 | Age       | 3
Zijdeman| 1980 | Occupation| Lemonade salesman
Zijdeman| 2000 | Age       | 23
Zijdeman| 2000 | Occupation| Formula one driver
...     | ...  | ...       | ...

Alternatively, longitudinal data can take the form of a relational database. For example:

Births:

Key|Subject | Date | location
---|--------|------|----------
1  |Zijdeman| 1977 | Emmeloord
...|...     | ...  | ...

Occupations:

Key|Subject | Date | Occupation
---|--------|------|-----------
1  |Zijdeman| 2015 | Researcher
...|...     | ...  | ...

Here the example is a relational database organised by concept (births, occupations), but alternatively it can be organised by source (birth certificates, marriages certificates etc.).

Finally, a word on the relations between individuals in the databases. Cross-sectional micro-data shows this by first nesting each individual in a household and then by specifying the link of each individual in the household to a central person in that household, usually the household head. Longitudinal data may sometimes specify the household at a given data, in which case it can take a similar form. Some datasets are built to follow links between individuals over time: son-father-grandfather-etc., but no clear formats exist for this.

#### Meso Data

...

#### Macro data

Macro data organised in long-form tables consists of at least three column headers, one identifying the geographical area, another identifying the time period, and a finally one specifying the variable of interest.

Country | Year | GDPpc
--------|------|------
NLD     | 2005 | 40867
...     | ...  | ...

## Services

## Example queries

### QQT pilot
Below is a simplified example from the QQT-pilot. The relevant unit of observation here are children older than the mandatory schooling and younger than a predetermined cutoff age (16). The desired output of the query is therefore a table with each row representing such a child and each column representing the variables of interest. Note that the unit of observations could be a number of things: events, households, families, streets

This is a simplified version of the actual queries for the analysis as a number of variables are left out and the data cleaning is left out. Example: in the eventual analysis we only want to distinguish male and female since the small number of observations for unknown/unspecified can give problems in the estimation. Some complications are between square brackes [].
* Select enrolment, age, sex, location, household ID for children between 14 and 16 [age thresholds come from a separate macro-dataset on mandatory schooling laws]
* Count number of siblings[brothers, sisters, extended family members], servants in household of child
* [rank age of child (determine birthorder of child in household)]
* Select age, occupation, literacy, religion of father (household head)
* Select age, occupation, literacy, religion of mother (spouse)
* Select per capita GDP for country-year [or other macro data]
* Join the results

hhid |name |relate  |age|sex   |literacy  |enrol         |year|country|...
-----|-----|--------|---|------|----------|--------------|----|-------|---
1    |john |head    |49 |male  |literate  |not enrolled  |1870| USA   |...
1    |mary |spouse  |47 |female|illiterate|not enrolled  |1870| USA   |...
1    |harry|son     |18 |male  |illiterate|not enrolled  |1870| USA   |...
1    |jim  |son     |15 |male  |illiterate|not enrolled  |1870| USA   |...
1    |susan|daughter|12 |female|literate  |enrolled      |1870| USA   |...
1    |ben  |son     |10 |male  |illiterate|enrolled      |1870| USA   |...
1    |gary |servant |23 |male  |illiterate|not enrolled  |1870| USA   |...
2    |bob  |head    |51 |male  |literate  |not enrolled  |1870| USA   |...
2    |meg  |spouse  |53 |female|literate  |not enrolled  |1870| USA   |...
2    |eve  |daughter|15 |female|literate  |enrolled      |1870| USA   |...
2    |iris |daughter|15 |female|literate  |enrolled      |1870| USA   |...
2    |hank |brother |47 |female|literate  |enrolled      |1870| USA   |...
...  |...  |...     |...|...   |...       |...           |... | ...   |...


loc|year| gdppc
---|----|-------
USA|1870| 2444
USA|1871| ...
...|... | ...

hhid|literate|nsib|n_extd|rank|age|male|father_age|father_literate|...|year|GDPpc|...
----|--------|----|------|----|---|----|----------|---------------|---|----|-----|---
1   |0       |3   |0     |2   |15 |1   |49        |1              |...|1870|2444 |...
2   |1       |1   |1     |1   |14 |0   |51        |1              |...|1870|2444 |...
2   |1       |1   |1     |1   |14 |0   |51        |1              |...|1870|2444 |...
... |...     |... |...   |... |...|....|...       |...            |...|1870|2444 |...
