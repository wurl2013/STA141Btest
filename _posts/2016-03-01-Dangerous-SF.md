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


<p><strong>1.2.2</strong>-Which parts of the city are the most dangerous (and at what times)?</p>


</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[56]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="n">Crime</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_sql_query</span><span class="p">(</span><span class="s2">&quot;select * from crime&quot;</span><span class="p">,</span><span class="n">conn0</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>
