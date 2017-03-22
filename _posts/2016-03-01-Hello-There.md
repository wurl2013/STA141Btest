---
layout: post
title: Dangerous San Francisco
categories: assignment
tags: [documentation,sample]
image:
  feature: cluster.png
  teaser: cluster-teaser.png
  credit: 
  creditlink: ""
---

This is one interesting question from STA141B assignment. This assignment was done using Python sqlite3, basemap, and pandas. You may learn other questions in this homework from this [jupyter notebook](https://wurl2013.github.io/STA141Btest/attachment/assignment6.ipynb).

#  Which part of San Francisco is Most Dangerous (and what time)?

## Data Description and Processing
The database *noise* was collected from [SF openData](https://data.sfgov.org/). It contains noise complaints dating back to August 2015. It recorded case number, category, description, time, district, resolution, address, longitute and latitute.  
The information in the database is imported into pandas dataframe using `pd.read_sql_query()`.

## Data Visualization
To find out which part of San Francisco is most dangerous, I mapped 
