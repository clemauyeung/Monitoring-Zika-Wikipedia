# Monitoring Disease Outbreak on Wikipedia: A Study on the Zika Virus Page in English, Spanish, and Portuguese

The goal of this project was to understand Zika virus's prevalence in North, Central, and South America by investigating people's behaviors on Wikipedia. Specifically, I collected revision and page view data on the virus's Wikipedia page in three languages: English, Spanish, and Portuguese. These languages dominate the affected regions, and I compared the page data between the different language editions of the Wikipedia page to inform whether disease prevalence could be predicted using Wikipedia data.

## Project Objectives

The objective is to use data science to answer the following research questions:

* How do Wikipedia usage differ among English, Spanish, and Portuguese page for Zika virus?
* How do revisions and page views relate to each other within the same language Wikipedia for the Zika virus page?
* How does WHO declaring Zika as a disease of concern in February 2016 affect revisions and page views?

## Process

* Revision and page view data were retrieved from MediaWiki API
* The data was collected via a Python program I wrote
* The JSON data from the Wikipedia pages were exported to a CSV file
* The data was analyzed and visualized in Tableau

## Data

* [English Wikipedia page on Zika](https://en.wikipedia.org/wiki/Zika_virus)
* [Spanish Wikipedia page on Zika](https://es.wikipedia.org/wiki/Virus_del_Zika) 
* [Portuguese Wikipedia page on Zika](https://pt.wikipedia.org/wiki/Vírus_da_zica)

## Metrics

|Goal |Signal |Metric |
|:----|:------|:------|
| People accessed the page to look for information |  Number of people who accessed the page and when | Page views |
| People added new content to the page | Number of people who edited the page | Revisions |
