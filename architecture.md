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



For this domain, we distinguish two levels of description: **micro** data of individual persons, and **meso** data, aggregated at municipal and provincial levels.

#### Micro Data
In its normalized form micro data is captured in a table where the different variables are column headers, and each described entity (typically a person) forms a record along a single row.

For example:

Family name | Occupation | Age        | Gender
----------- | ---------- | ---------- | ------
Zijdeman    | researcher | 38         | m
...         | ...        | ...        | ...

In terms of variables and codes:

Variable A | Variable B | Variable C | Variable D
---------- | ---------- | ---------- | ----------
string     | code       | number     | code

#### Meso Data

...


## Services
