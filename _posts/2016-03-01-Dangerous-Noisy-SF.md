---
layout: post
title: Two Data Visualization Question about San Francisco
categories: assignment
tags: [documentation,sample]
image:
  feature: sf.jpg
  teaser: sf-teaser.jpg
  credit: 
  creditlink: ""
---

This is one interesting question from STA141B assignment. This assignment was done using Python sqlite3, basemap, matplotlib and pandas. You may learn other questions in this homework from this [link](https://wurl2013.github.io/STA141Btest/attachment/assignment6.html).

#  Which part of San Francisco is Most Dangerous (and what time)?

## Data Description and Processing
The dataset *crime* was collected from [SF openData](https://data.sfgov.org/). It contains crime case dating back to August 2015. It recorded case number, category, description, time, district, resolution, address, longitude and latitude.  
The information in the database is imported into pandas dataframe using `pd.read_sql_query()`.

## Data Visualization and Conclusion
### Dangerous Part in SF
To find out which part of San Francisco is most dangerous, I mapped a heatmap of the crime number. As the plot below show, Southern dstrict is the most dangerous place in SF. The crime number is almost 200000. Also, by using the barplot, the crime number in Southern district is much higher than other districts in SF.

<img src="https://wurl2013.github.io/STA141Btest/images/crimeSF1.png" width="660px" height = "900px" align="middle"/>
<img src="https://wurl2013.github.io/STA141Btest/images/crimeSF2.png" width="60%" align="middle"/>

### Dangerous Time in SF
As for most dangerous time in SF, I ploted the histogram of crime case time. From the histogram, it is clear that the most dangerous time in a day is around 6pm. Crime case number starts to increase from 5am and increases until 18-19pm, then drops.

<img src="https://wurl2013.github.io/STA141Btest/images/crimeSF3.png" width=60%  align="middle"/>

# Are noise complaints and mobile food vendors related?

## Data Description and Processing
Two datasets The method of data processing and visualization is similar as described above. The datasets used in this part are *noise* and *mobile_food_location*. Noise contains caseID, Type, Address, Neighborhood, DateTime, Latitude and Longitude of each noise complaint case. Mobile_food_location contains locationid, LocationDescription, Address, Latitude and Longitude of each vendor.

## Data Visualization and Conlcusion
The noise complaints are not very much related with mobile food vendors.
The barplot of noise complaints type shows that only few complaints is about mobile food vendors. Also, from the heatmap marking the noise number and vendors, we can see that the density of noise complaints are not very high associated with the distribution of vendors, especially in southern part of the city. Though in the areas where there are a lot of complaints, the number of vendors is large. However, it is not the opposite, in areas where there is a lot of vendors, the density of complaints are not always high. So the association between them is not very high.

<img src="https://wurl2013.github.io/STA141Btest/images/noiseSF1.png" width="660px" height = "900px" align="middle"/>

<img src="https://wurl2013.github.io/STA141Btest/images/noiseSF2.png" width=60%  align="middle"/>

