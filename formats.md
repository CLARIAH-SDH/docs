# List of data formats

## Introduction

The Clariah Structured Data Hub must eventually become a “live” data hub, where users can upload, enrich, use, and download data. It is therefore crucial that the hub can deal with a variety of data formats.

## List of formats

This is a list of formats at some point encountered in the social-economic history "wild".

### Microsoft 
* MS excel (xls/xlsx)
* MS access (mdb/accdb/...)

### Relational database formats
* db
* dbf

### Text based formats
* csv
* tsv
* fwf
* other text: dat/raw/...

### Statistical package formats
* spss
* stata
* rdata
* sas (very rare)

### Web formats
* json
* xml
* html tables

### geographical data
* (esri) shapefiles: shp, dbf etc.

## Prioritisation

What formats should the hub accept?

Excel, csv, stata, and spss are the most common formats.
Relational databases are also commonly used in systematic data collection efforts (which tend to contain some of the most interesting data).

## Requirements data structure

* data should be presented in rows and colums
* one variable name per row or column
* no totals or subtotals
* it is desirable to support relational databases, though direct support of access is difficult; there is an rdb2rdf
* if the data is in a presentation format (both columns and rows are dimensions), then the metadata should contain the variable name