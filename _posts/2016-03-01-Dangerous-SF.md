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

This is one interesting question from STA141B assignment. This assignment was done using Python sqlite3, basemap, matplotlib and pandas. You may learn other questions in this homework from this [jupyter notebook](https://wurl2013.github.io/STA141Btest/attachment/assignment6.ipynb).

#  Which part of San Francisco is Most Dangerous (and what time)?

## Data Description and Processing
The database *noise* was collected from [SF openData](https://data.sfgov.org/). It contains noise complaints dating back to August 2015. It recorded case number, category, description, time, district, resolution, address, longitute and latitute.  
The information in the database is imported into pandas dataframe using `pd.read_sql_query()`.

## Data Visualization
### Dangerous Part in SF
To find out which part of San Francisco is most dangerous, I mapped a heatmap of the crime number. As the plot below show, Southern dstrict is the most dangerous place in SF. The crime number is almost 200000. Also, by using the barplot, the crime number in Southern district is much higher than other districts in SF.

### Dangerous Time in SF
As for most dangerous time in SF, I ploted the histogram of crime case time. From the histogram, it is clear that the most dangerous time in a day is around 6pm. Crime case number starts to increase from 5am and increases until 18-19pm, then drops.

