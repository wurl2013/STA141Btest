---
layout: post
title: “The Next Super Star”
author: Mengxin Ji, Ruolai Wu, Meng Li, Yonglin Jing
#categories: journal
tags: [documentation,sample]
image:
  feature: nbafans.png
  teaser: nbafans-teaser.png
  credit: Death to Stock Photo
  creditlink: ""
---
<style TYPE="text/css">
code.has-jax {font: inherit; font-size: 100%; background: inherit; border: inherit;}
</style>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
    tex2jax: {
        inlineMath: [['$','$'], ['\\(','\\)']],
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'] // removed 'code' entry
    }
});
MathJax.Hub.Queue(function() {
    var all = MathJax.Hub.getAllJax(), i;
    for(i = 0; i < all.length; i += 1) {
        all[i].SourceElement().parentNode.className += ' has-jax';
    }
});
</script>
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>


## _Motivation_

Given the large basis of NBA audiences and increasing pursue for super stars, using past year data to analyze who is the next super star seems to be an interesting and meaningful question.


## _Questions_

Are there any statistical patterns in the players performance? Can we use the pattern to predict the potential stars?

What features do the potential stars and super stars share?

## _Methodology_

Using NBA statistic data, we would like to do some exploratory analysis and data visualization over “all stars” and “potential players” based on their first four seasons data

1. Data Scrapping

2. K-means Cluster

3. PCA and Data Visualization

4. Compare player A and player B


## _Explanation for Choosing the Methodology_

### Data Scrapping
We exploit the data from http://www.basketball-reference.com/ and used lxml module to extract basic statistics data of rookie players of 2013 during recent four seasons and all starts during recent four seasons.

### k-means

We are interested whether there is any statistical patterns in the statistics of the players' performances. To answer this question, we would like to cluster the data and see if the stars and rookie players can be in the same cluster. Basically, we will mainly use clustering to automatically split players into several clusters based on technical data during the seasons. To deal with the data containing 180 variables, we normalized the data.

Explicitly, we use K-means cluster to group similar players based on the first four year players stats. The main idea is that if a fourth year player share the same cluster as star players, then we can conclude they are similar in terms of early career stats and therefore that young player has the potential to become a star player. However, the number of clusters K need to be pre-specified. Thus, it necessary to evaluate the choice of K. There are many metrics and here we use silhouette scores. The silhouette score for each sample is defined as <span class="mrow" id="MathJax-Span-2"><span class="mi" id="MathJax-Span-3" style="font-family: STIXGeneral-Italic;">s</span><span class="mo" id="MathJax-Span-4" style="font-family: STIXGeneral-Regular;">(</span><span class="mi" id="MathJax-Span-5" style="font-family: STIXGeneral-Italic;">i</span><span class="mo" id="MathJax-Span-6" style="font-family: STIXGeneral-Regular;">)</span><span class="mo" id="MathJax-Span-7" style="font-family: STIXGeneral-Regular; padding-left: 0.301em;">=</span><span class="mfrac" id="MathJax-Span-8" style="padding-left: 0.301em;"><span style="display: inline-block; position: relative; width: 3.753em; height: 0px; margin-right: 0.122em; margin-left: 0.122em;"><span style="position: absolute; clip: rect(3.336em 1002.5em 4.289em -999.997em); top: -4.521em; left: 50%; margin-left: -1.247em;"><span class="mrow" id="MathJax-Span-9"><span class="mi" id="MathJax-Span-10" style="font-size: 70.7%; font-family: STIXGeneral-Italic;">b</span><span class="mo" id="MathJax-Span-11" style="font-size: 70.7%; font-family: STIXGeneral-Regular;">(</span><span class="mi" id="MathJax-Span-12" style="font-size: 70.7%; font-family: STIXGeneral-Italic;">i</span><span class="mo" id="MathJax-Span-13" style="font-size: 70.7%; font-family: STIXGeneral-Regular;">)</span><span class="mo" id="MathJax-Span-14" style="font-size: 70.7%; font-family: STIXGeneral-Regular;">−</span><span class="mi" id="MathJax-Span-15" style="font-size: 70.7%; font-family: STIXGeneral-Italic;">a</span><span class="mo" id="MathJax-Span-16" style="font-size: 70.7%; font-family: STIXGeneral-Regular;">(</span><span class="mi" id="MathJax-Span-17" style="font-size: 70.7%; font-family: STIXGeneral-Italic;">i</span><span class="mo" id="MathJax-Span-18" style="font-size: 70.7%; font-family: STIXGeneral-Regular;">)</span></span><span style="display: inline-block; width: 0px; height: 3.991em;"></span></span><span style="position: absolute; clip: rect(3.336em 1003.57em 4.289em -999.997em); top: -3.568em; left: 50%; margin-left: -1.783em;"><span class="mrow" id="MathJax-Span-19"><span class="mo" id="MathJax-Span-20" style="font-size: 70.7%; font-family: STIXGeneral-Regular;">max</span><span class="texatom" id="MathJax-Span-21" style="padding-left: 0.182em;"><span class="mrow" id="MathJax-Span-22"><span class="texatom" id="MathJax-Span-23"><span class="mrow" id="MathJax-Span-24"><span class="mi" id="MathJax-Span-25" style="font-size: 70.7%; font-family: STIXGeneral-Italic;">a</span><span class="mo" id="MathJax-Span-26" style="font-size: 70.7%; font-family: STIXGeneral-Regular;">(</span><span class="mi" id="MathJax-Span-27" style="font-size: 70.7%; font-family: STIXGeneral-Italic;">i</span><span class="mo" id="MathJax-Span-28" style="font-size: 70.7%; font-family: STIXGeneral-Regular;">)</span><span class="mo" id="MathJax-Span-29" style="font-size: 70.7%; font-family: STIXGeneral-Regular;">,</span><span class="mi" id="MathJax-Span-30" style="font-size: 70.7%; font-family: STIXGeneral-Italic;">b</span><span class="mo" id="MathJax-Span-31" style="font-size: 70.7%; font-family: STIXGeneral-Regular;">(</span><span class="mi" id="MathJax-Span-32" style="font-size: 70.7%; font-family: STIXGeneral-Italic;">i</span><span class="mo" id="MathJax-Span-33" style="font-size: 70.7%; font-family: STIXGeneral-Regular;">)</span></span></span></span></span></span><span style="display: inline-block; width: 0px; height: 3.991em;"></span></span><span style="position: absolute; clip: rect(0.836em 1003.75em 1.253em -999.997em); top: -1.307em; left: 0em;"><span style="display: inline-block; overflow: hidden; vertical-align: 0em; border-top: 1.3px solid; width: 3.753em; height: 0px;"></span><span style="display: inline-block; width: 0px; height: 1.074em;"></span></span></span></span></span> where <span class="math" id="MathJax-Span-34" style="width: 1.729em; display: inline-block;"><span style="display: inline-block; position: relative; width: 1.432em; height: 0px; font-size: 120%;"><span style="position: absolute; clip: rect(1.729em 1001.37em 2.92em -999.997em); top: -2.557em; left: 0em;"><span class="mrow" id="MathJax-Span-35"><span class="mi" id="MathJax-Span-36" style="font-family: STIXGeneral-Italic;">a</span><span class="mo" id="MathJax-Span-37" style="font-family: STIXGeneral-Regular;">(</span><span class="mi" id="MathJax-Span-38" style="font-family: STIXGeneral-Italic;">i</span><span class="mo" id="MathJax-Span-39" style="font-family: STIXGeneral-Regular;">)</span></span><span style="display: inline-block; width: 0px; height: 2.562em;"></span></span></span><span style="display: inline-block; overflow: hidden; vertical-align: -0.282em; border-left: 0px solid; width: 0px; height: 1.146em;"></span></span> is the mean distance between a sample and all other points in the same cluster and <span class="math" id="MathJax-Span-34" style="width: 1.729em; display: inline-block;"><span style="display: inline-block; position: relative; width: 1.432em; height: 0px; font-size: 120%;"><span style="position: absolute; clip: rect(1.729em 1001.37em 2.92em -999.997em); top: -2.557em; left: 0em;"><span class="mrow" id="MathJax-Span-35"><span class="mi" id="MathJax-Span-36" style="font-family: STIXGeneral-Italic;">b</span><span class="mo" id="MathJax-Span-37" style="font-family: STIXGeneral-Regular;">(</span><span class="mi" id="MathJax-Span-38" style="font-family: STIXGeneral-Italic;">i</span><span class="mo" id="MathJax-Span-39" style="font-family: STIXGeneral-Regular;">)</span></span><span style="display: inline-block; width: 0px; height: 2.562em;"></span></span></span><span style="display: inline-block; overflow: hidden; vertical-align: -0.282em; border-left: 0px solid; width: 0px; height: 1.146em;"></span></span> is the mean distance between a sample and all other points in the next nearest cluster. So it is clear that <span class="mrow" id="MathJax-Span-41"><span class="mo" id="MathJax-Span-42" style="font-family: STIXGeneral-Regular;">−</span><span class="mn" id="MathJax-Span-43" style="font-family: STIXGeneral-Regular;">1</span><span class="mo" id="MathJax-Span-44" style="font-family: STIXGeneral-Regular; padding-left: 0.301em;">≤</span><span class="mi" id="MathJax-Span-45" style="font-family: STIXGeneral-Italic; padding-left: 0.301em;">s</span><span class="mo" id="MathJax-Span-46" style="font-family: STIXGeneral-Regular;">(</span><span class="mi" id="MathJax-Span-47" style="font-family: STIXGeneral-Italic;">i</span><span class="mo" id="MathJax-Span-48" style="font-family: STIXGeneral-Regular;">)</span><span class="mo" id="MathJax-Span-49" style="font-family: STIXGeneral-Regular; padding-left: 0.301em;">≤</span><span class="mn" id="MathJax-Span-50" style="font-family: STIXGeneral-Regular; padding-left: 0.301em;">1</span></span> where a high value indicates that the object is well matched to its own cluster and poorly matched to neighboring clusters. If most objects have a high value, then the clustering configuration is appropriate. Finally, the Silhouette Coefficient for whole dataset is given as the mean of the silhouette Coefficient for each sample. For the sake of visualization, K-means clustering is run on the dataset for a range of values of k from 2 to 10, and for each value of k the silhouette is calculated. The plot of silhouette scores against different k is shown as follows.

<img src="https://mengxinji.github.io/STA141B/images/slh.png" alt="" width="60%">


We can see the optimal K is 2. This actually makes sense as the data is comprised of both stats for star players (have been proved later on) and 4th-year rookies. Nevertheless, we want to go deeper in order to find more patterns among similar players. For example, star players can also belong to different groups as they may play in different positions therefore their stats are different. Surprisingly, there is a bump when k = 5 and it turns out to be a reasonable choice of k in terms of interpretation and visualization.

## K-means Cluster Results

Cluster 4 is the largest proportion and cluster 1 is the smallest. The players in cluster 2 are mostly rookie players and all the players in cluster 3 are stars. In cluster 1,4, and 3, there are a few players are rookie players. Such that rookie stars in cluster 1, 4, and 3 may be potential candidates for next stars.



<img src="https://mengxinji.github.io/STA141B/images/pieCL.png" alt="" width="40%"> <img src="https://mengxinji.github.io/STA141B/images/stackCl.png" alt="" width="50%">


## PCA Visualization

Due the large explanatory variables in the NBA stats for evaluating players’ personality and ability, we consider first using principal component analysis to reduce the covariates dimensions through coordinate transformation. We find first two components account for over 75% variance, which is also good for visualization coordinates.

![alt tag](https://mengxinji.github.io/STA141B/images/cluster_plot_r.png)


## Data Analysis

Based on the results of clustering, we would like to analyze why player A and player B are in the same cluster.
James Harden vs. Micheal Cart-Williams Paul Millsap vs. Nerlen Noel
Tony Parker vs. Victor Oladipo

For James Harden vs. Micheal Cart-Williams, We compared their 3 point rate during last four regular seasons.

![alt tag](https://mengxinji.github.io/STA141B/images/James_Michael.png)

For Paul Millsap vs. Nerlen Noel, we compared their BLK during last four regular seasons.

![alt tag](https://mengxinji.github.io/STA141B/images/Millsap_Noel.png)

For Tony Parker vs. Victor Oladipo, we compared their Field Goal% during last four regular seasons.

![alt tag](https://mengxinji.github.io/STA141B/images/Parker_Oladipo.png)


## Conclusion

Ideally, we would exploit an automatic clustering method that can correctly split all players into several clusters, and based on the similar pattern between all stars and potential stars to identify a forthcoming super star!

Besides the plots we showed above, we test several stats of these 3 pairs. most of the stats have similar distribution. Suggesting the rookie players play highly resemble with the star players.

Finally, we can say that this three players Micheal Cart-Williams, Nerlen Noel, Victor Oladipo might become star players in the future.
