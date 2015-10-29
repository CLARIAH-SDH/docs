# Clariah Structured Data (WP-4) Pilot report

Richard Zijdeman, Auke Rijpma, Rinke Hoekstra
	
| 			|Table of contents							|
|-----------------------|-----------------------------------------------------------------------|
| 1	 		| [Introduction][intro]							|	
| 2 			| [Semantic web embedment] [sem]						|
| 2.1 			| [Linking to existing vocabularies and data][link]			|
| 2.2 			| [Transposing existing data to linked data][transpose]			|
| 2.2.1			| [Level of complexity and approach][complex]				|
| 2.2.2 		| [Level of detail and increase in file sizes][fileSize]			|
| 3 			| [Running a historical semantic web (infra-structure)][historical]	|
| 4 			| [Implications for the CSDH project][implicationsCSDH]			|
| 4.1 			| [Implications for data][implicationsData]				|
| 4.1.1 		| [Micro data][micro]							|
| 4.1.2 		| [Macro data][macro]							|
| 4.1.3 		| [Data format requirements][format]					|
| 4.2 			| [Implications for the working process][implicationsProcess]		|
| 5 			| [References][refs]							|

#1 Introduction [intro]
The Clariah Structured Data Hub project (CSDH) has completed the pilot phase, that ran from February 1st, 2015 to July 1st, 2015. This report evaluates that six month period, in particular the strengths and weaknesses of using semantic technologies to combine and analyze structured datasets in the field of economic and social history.
	The pilot phase consisted of two mini-projects, that were directed by research questions from the field, one on the quality-quantity trade-off (QQT) and one the U-shaped relation between female labour force participation and economic development (USHAPE). The aim of the QQT project was to compare the efficiency of semantic web technology to a more traditional way of linking and analysing datasets. The aim of the USHAPE project was to enrich an existing dataset, with data from the semantic web and analyze the enhanced dataset. In total 14.4 post-doc months were dedicated to both projects, one architect (0.8 fte) and two quantitative researchers from the fields of economic and social  history (0.8 fte each).
	
#2 Semantic web embedment [sem]
##2.1 Linking to existing vocabularies and data [link]
To transpose current datasets to ‘linked data’ and augment historical datasets with data on the semantic web, we first established the extent to which there were so called ‘vocabularies’ for economic and social history.  Such vocabularies contain concise description of characteristics (concepts), e.g. ‘sex’, ‘father’, ‘year’. By declaring that columns from a dataset are (partly) the same to these concepts, we can link those datasets based on concept-similarity. To check for vocabularies relevant to the field of economic and social history we used a LSD-dimensions (Meroño-Peñuela (2014)) a tool for searching items on the semantic web. Unfortunately, only a handful of concepts appeared to be available for our purposes, mostly which are really generic, such as ‘sdmx:sex’ for sex and ‘xsd:gYear’ for Gregorian Year. As these concepts are lacking, it also means that historical data that is available as linked data is scarce, and often only available to specific domains (such as data from the Ships and Sailors project).

> OUTCOME 1: Few concepts and historical data are available for the field of economic and social history.

##2.2 Transposing existing data to linked data [transpose]
The bulk of time spent in the pilot phase was dedicated to transposing historical datasets to linked data. Transposing datasets was already emphasized in the QQT project, but as no data was available for linkage in the USHAPE project, the USHAPE project shifted its aims towards creating linked data too. 
In total five datasets were transposed to linked data. We started with a small dataset on migrants in the city of Utrecht as registered in the 1829 Census. A second dataset used was the USA 1850 census sample (c. 200.000 observations; 17MB) from the North Atlantic Population Project (NAPP) project (https://www.nappdata.org/napp/samples.shtml). The third dataset was the England and Wales 1881 full census. The Historical International Standard Classification of Occupations (HISCO) was the fourth dataset and finally the GDP per Capita dataset from Clio-Infra was converted to linked data. None of these files have been made publicly available as they cannot be distributed without permission.

###2.2.1 Level of complexity and approach [complex]
The conversion of datasets to linked data was an enriching experience as it brought to light a number of issues. A first issue relates to varying levels of complexity of datasets. During the pilot phase a tool was created ‘QBer’, that allows one to create linked data, using a .csv file as input. QBer let’s the user search for existing vocabularies and aids in the creation of new ones. However, when creating triples from the values, writing (Python) scripts to turn the values into linked data proved to be more efficient than QBER. Moreover, in the case where datasets are part of a bigger data source (e.g. Clio-Infra, HISCO, NAPP), one first needs to design and define an underlying data structure to reduce redundancy in the  files. Currently defining the data structure is most feasible by writing scripts, rather than trying to implement it in QBER, although this could be extended in the future.
	Apart from the question what software to use to transpose files (e.g. QBer vs. scripting), the varying degrees of complexity of datasets also requires different levels of knowledge. Defining a data structure with dimensions and measures for example, appears to be a somewhat more advanced topic than transposing values into literals, or linking a variable to an existing concept. This would indicate that we would need varying levels of knowledge when transposing data into linked data and that a tool like QBER would need to be complemented with support.

> OUTCOME 2: Data sets come with varying levels of complexity, requiring various levels of knowledge of RDF and therewith various levels of support to historians.

###2.2.2 Level of detail and increase in file sizes [fileSize]
A second issue we encountered while transposing data into linked data, concerns the ‘level of detail’. One way of linking data is by concatenating columns. That means if one combines datasets based on the columns they have in common, the linked dataset will consist of these columns and the number of rows will be equal to the sum of rows in each of the datasets used in the linkage procedure. 
A more detailed level of linkage is on the value level (as opposed to the column level mentioned above). This requires values to be represented as linked data too and allows for more specific queries. For example, rather than querying just for any datasets that contain columns with a ‘sex’, ‘occupation’ and ‘year’ variable, we could query datasets for ‘women’, ‘butchers’ in 1805.
For our purposes a more detailed level of specification is more suitable as we are often interested in specific parts of a dataset, e.g. a specific period, region or country. However, adding a triple for each value in the dataset has a substantial impact on the size of transposed datasets. For example, from the QQT project we learned that the 17MB US 1850 census increased to a 375MB turtle (ttl) file. The England and Wales dataset was 2.5GB as .csv file and turned into a 121 GB ttl file. While the HISCO files are much more modest in size (ca. 500 KB per .csv file), they increase by similar factors of 20 to 40 times their original size.

> OUTCOME 3: Transposing datasets into RDF seriously increases the size of files, factors of 20 to 40 times are not uncommon.

#3 Running a historical semantic web (infra-structure) [historical]
Once the historical data is transposed to linked data, the data will need to be made available for researchers. Basically, we have distinguished three different ways of doing so, varying in degree of complexity.
	A first option, or ‘flavour’ of a prototype is to transpose only the data model into RDF. The data would resort in a dedicated database, while queries for data selection would be provided. We refer to this flavour as ‘vanilla’. Under the vanilla scheme it would not be possible to query on values of different datasets. A researcher would first need to download all data and then make a selection of the data that is useful for her purposes. Also any analysis on the data would be conducted by the researcher herself.
	A second flavour, ‘chocolate’, entails the provision of the full data in RDF, thus at the value level allowing for queries of specific time periods, regions and populations. Moreover, the chocolate flavour allows for data export facilities, e.g. providing data as .csv, .sps, .dta or Rdata. 
	A third flavour, ‘cherry-on-top’, entails all of the elements of ‘chocolate’, thus full RDF data and data export facilities, but adds tooling on the triple store to it. Basically any tool that appears to be relevant could be build on top-of-it, but in the first instance, we think of three such tools:
‘linked edit rules’, which provides a generic way of cleaning and recoding data among researchers, enhancing replicability of research
basic analysis tools, allowing for correlation testing
basic visualization tools
The additional tools will not be integrated with the database but provided as seperate modules to maintain flexibility.

Currently we are running a chocolate flavour setup on VU machinery. Several test queries were run on a subset of the England and Wales file (600k observations; 15m triples). Most of the queries necessary to obtain the data for the QQT pilot were possible and went sufficiently fast. Additional queries on the bigger dataset are still necessary to properly review the usability of such a system. A challenge we face is that evaluating the feasibility of the chocolate system is depended on data size, which will be increasing all the time, even after the Clariah project has ended.

> OUTCOME 4: We have identified three ways of hosting a historic semantic web, varying in levels of complexity. The chocolate and/ or cherry-on-top flavour appear to be the most worthwhile in terms of usability, but also the more riskful in terms of manageability.
					
#4 Implications for the CSDH project [implicationsCSDH]
##4.1 Implications for data [implicationsData]
###4.1.1 Micro data [micro]
A set of key variables in the dataset or metadata must be present. First is the geographical location. 
At the very least the country must be provided. The datahub should accommodate more detailed geocoding as well: province, municipality, or coordinates. 
The second key variable is time. At the very least the year/decade must be provided; more detailed dates should be accommodated by the hub as well. 
Finally, there should be meaningful identifiers of the observations (household, individual or otherwise).
The following variables are not necessary for the hub to function, but we  think they are important to be able to answer research questions with the data. These variables can also be used to prioritise datasets. These are the variables the hub should accommodate, meaning there is a  basic vocabulary/codebook present to allow the data to be linked to similar datasets. The QQT-pilot identified the following variables as important:

- age
- sex
- household/family relation
- occupation string
- (occupation code)
- enrolment
- literacy
- marital status
- religion
- person id
- household id
- place of birth
-(urban)
-(income)
-(name)

The list of  variables required some elaboration. Occupation strings were vital, though coded occupations make the data processing and analysis much easier. However, coding occupations in multiple large datasets would probably be too time-consuming. Likewise, variables for region and whether the location was urban were important. Such data could in theory be extracted from geocoded observations. However, geocoding of historical data is tricky. For example: it turned out to be very difficult to automatically geocode the Hungarian and Hapsburg regions. Finally, any individual/household-level income data would have been very useful, but such data at the microlevel is very rare.

###4.1.2 Macro data [macro]
At the country-level adding all macro data from clio-infra should be fairly straightforward. See https://www.clio-infra.eu/datasets/indicators. To this the data from e.g. the labour relations hub can also be added. Nonetheless, some priorities are:

- gdp
- real wage
- inflation
- population (by various characteristics if possible for weighting / post- stratification)
- urbanisation
- life expectancy
- inequality
- poverty
- numeracy
- literacy
- average years of education
- enrolment
- polity2

###4.1.3 Data format requirements [format]
As long as the project is running, we should be able to convert most data, provided the original data has some structure and has sufficient documentation. Sufficient documentation means the variables are properly described. If the variables do not cover it, the documentation should also contain information on the sample or population.
The more interesting question is possibly what formats the hub should be able to deal with when users want to upload (or download) their data. While conversion might be tricky, some formats tend to contain highly structured data, so these should be easy to accomodate. Data file for statistical software usually come in highly structured tables with columns representing variables. To an extent, the same holds for relational databases, though they can have complex structures nonetheless. 
Text files and excel allow more freedom in structuring the data. Form requirements therefore need to be determined. They are that the file follows some tabular dataformat: the top row should have variable names, below that each column contains the data for that variable. Each row should contain one observation. The hub could also accommodate a "presentation format" (like clio-infra) where a table represents one variable and rows/columns contain e.g. years/countries. If the data do not meet any of these requirements, users could be led through a data-cleaning workflow.
Searching for useful datasets for the QQT-pilot has led to the following list of common formats in economic and social history.:

- Text based formats: csv, fwf, tsv, and other plain text: dat, raw, etc.. 
- Statistical package formats include: sav (spss), dta (stata), rdata (R ), sas. 
- Common Microsoft formats: MS excel (xls, xlsx), MS access (mdb, accdb, ...). 
- Relational database formats: db, dbf. Geographical data: (esri) shapefiles: shp, dbf etc.. Web formats: json, xml, html tables.
- Excel, csv, fwf, spss, stata, and access are probably the most important of these in economic and social history. 

Data files for statistical software usually come in highly structured tables with columns representing variables. To an extent, the same holds for relational databases, though they can have complex structures nonetheless.  Text files and excel allow more freedom in structuring the data. Form requirements need to be set. They are that the file follows some tabular data format: the top row should have variable names, below that each column contains the data for that variable. Each row should contain one observation. The hub could also accommodate a "presentation format" (like Clio-Infra) where a table represents one variable and rows/columns contain e.g. years/countries. If the data do not meet any of these requirements, users could be led through a data-cleaning workflow.

## 4.2 Implications for the working process [implicationsProcess]
In hindsight the pilot phase has been a plunge into the unknown and for the future requires some adaptation of the strategy chosen. From the part of the historians concepts of RDF and more specific concepts, such as ‘owl’ and ‘qb’ were unknown. At the same time they had to improve on their programming skills in Python which were small to non-existent. It also meant that quite often the architect needed to explain some of the more mundane elements of Python and RDF. Moreover the architect had to come to grips with terminology and characteristics of historical data, while all three had to adapt to a common vocabulary.
	While some of these issues just appear to be related to starting an interdisciplinary project and properly dealt with, some issues are still there and could be solved by training the project members. Even if in the end a tool could be developed that allowed non-initiated to transpose data into linked data, in the meantime many datasets must be transposed and training while time-costly could enhance efficiency in the end.

# 5 References [refs]
Albert Meroño-Peñuela. “LSD Dimensions: Use and Reuse of Linked Statistical Data”. In: *Proceedings of the 19th International Conference on Knowledge Engineering and Knowledge Management*, EKAW 2014. LNCS 8982, Springer. Linköping, Sweden (2014). [pdf](http://www.albertmeronyo.org/wp-content/uploads/2014/10/ekawpd2014_submission_7_A.pdf)
