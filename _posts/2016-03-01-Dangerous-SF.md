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


<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[57]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>IncidntNum</th>
      <th>Category</th>
      <th>Descript</th>
      <th>DayOfWeek</th>
      <th>Datetime</th>
      <th>PdDistrict</th>
      <th>Resolution</th>
      <th>Address</th>
      <th>Lon</th>
      <th>Lat</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>150060275</td>
      <td>NON-CRIMINAL</td>
      <td>LOST PROPERTY</td>
      <td>Monday</td>
      <td>2015-01-19 14:00:00</td>
      <td>MISSION</td>
      <td>NONE</td>
      <td>18TH ST / VALENCIA ST</td>
      <td>-122.421582</td>
      <td>37.761701</td>
    </tr>
    <tr>
      <th>1</th>
      <td>150098210</td>
      <td>ROBBERY</td>
      <td>ROBBERY, BODILY FORCE</td>
      <td>Sunday</td>
      <td>2015-02-01 15:45:00</td>
      <td>TENDERLOIN</td>
      <td>NONE</td>
      <td>300 Block of LEAVENWORTH ST</td>
      <td>-122.414406</td>
      <td>37.784191</td>
    </tr>
    <tr>
      <th>2</th>
      <td>150098210</td>
      <td>ASSAULT</td>
      <td>AGGRAVATED ASSAULT WITH BODILY FORCE</td>
      <td>Sunday</td>
      <td>2015-02-01 15:45:00</td>
      <td>TENDERLOIN</td>
      <td>NONE</td>
      <td>300 Block of LEAVENWORTH ST</td>
      <td>-122.414406</td>
      <td>37.784191</td>
    </tr>
    <tr>
      <th>3</th>
      <td>150098210</td>
      <td>SECONDARY CODES</td>
      <td>DOMESTIC VIOLENCE</td>
      <td>Sunday</td>
      <td>2015-02-01 15:45:00</td>
      <td>TENDERLOIN</td>
      <td>NONE</td>
      <td>300 Block of LEAVENWORTH ST</td>
      <td>-122.414406</td>
      <td>37.784191</td>
    </tr>
    <tr>
      <th>4</th>
      <td>150098226</td>
      <td>VANDALISM</td>
      <td>MALICIOUS MISCHIEF, VANDALISM OF VEHICLES</td>
      <td>Tuesday</td>
      <td>2015-01-27 19:00:00</td>
      <td>NORTHERN</td>
      <td>NONE</td>
      <td>LOMBARD ST / LAGUNA ST</td>
      <td>-122.431119</td>
      <td>37.800469</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[135]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="k">def</span> <span class="nf">draw_sf</span><span class="p">(</span><span class="n">width</span><span class="o">=</span><span class="mf">2e7</span><span class="p">,</span><span class="n">proj</span><span class="o">=</span><span class="s1">&#39;merc&#39;</span><span class="p">):</span>
    <span class="n">figsize</span> <span class="o">=</span> <span class="p">[</span><span class="mi">10</span><span class="p">,</span><span class="mi">10</span><span class="p">];</span> <span class="n">dpi</span><span class="o">=</span><span class="mi">80</span>
    <span class="n">fig</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="n">figsize</span> <span class="o">=</span> <span class="n">figsize</span><span class="p">,</span> <span class="n">dpi</span> <span class="o">=</span> <span class="n">dpi</span><span class="p">)</span>
    <span class="n">ax</span> <span class="o">=</span> <span class="n">fig</span><span class="o">.</span><span class="n">add_subplot</span><span class="p">(</span><span class="mi">111</span><span class="p">)</span>
    <span class="n">bmap</span> <span class="o">=</span> <span class="n">Basemap</span><span class="p">(</span><span class="n">width</span><span class="o">=</span><span class="n">width</span><span class="p">,</span><span class="n">height</span><span class="o">=</span><span class="n">width</span><span class="p">,</span><span class="n">projection</span><span class="o">=</span><span class="n">proj</span><span class="p">,</span>
                   <span class="n">llcrnrlon</span><span class="o">=-</span><span class="mf">122.53</span><span class="p">,</span><span class="n">llcrnrlat</span><span class="o">=</span><span class="mf">37.67</span><span class="p">,</span><span class="n">urcrnrlon</span><span class="o">=-</span><span class="mf">122.33</span><span class="p">,</span><span class="n">urcrnrlat</span><span class="o">=</span><span class="mf">37.85</span><span class="p">,</span>
                   <span class="n">resolution</span><span class="o">=</span><span class="s1">&#39;h&#39;</span><span class="p">,</span> <span class="c1">#f for full</span>
                   <span class="n">lat_0</span> <span class="o">=</span> <span class="mf">37.5</span><span class="p">,</span>
                   <span class="n">lon_0</span><span class="o">=-</span><span class="mf">122.5</span><span class="p">)</span>
    <span class="n">bmap</span><span class="o">.</span><span class="n">drawcoastlines</span><span class="p">()</span>
    <span class="n">bmap</span><span class="o">.</span><span class="n">drawmapboundary</span><span class="p">(</span><span class="n">fill_color</span><span class="o">=</span><span class="s1">&#39;white&#39;</span><span class="p">)</span>
    <span class="c1">#bmap.fillcontinents(color=&#39;white&#39;,lake_color=&#39;white&#39;)</span>
    <span class="n">bmap</span><span class="o">.</span><span class="n">readshapefile</span><span class="p">(</span><span class="s1">&#39;geo_export_772ba198-1646-427d-8190-94c324b75364&#39;</span><span class="p">,</span><span class="s1">&#39;SFFindNeighborhoods&#39;</span><span class="p">)</span>
    <span class="k">return</span> <span class="n">ax</span><span class="p">,</span> <span class="n">fig</span><span class="p">,</span> <span class="n">bmap</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[140]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span></span><span class="n">ax</span><span class="p">,</span> <span class="n">fig</span><span class="p">,</span> <span class="n">bmap</span> <span class="o">=</span> <span class="n">draw_sf</span><span class="p">()</span>

<span class="n">lons</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="n">Crime</span><span class="p">[</span><span class="s1">&#39;Lon&#39;</span><span class="p">])</span>
<span class="n">lats</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="n">Crime</span><span class="p">[</span><span class="s1">&#39;Lat&#39;</span><span class="p">])</span>
<span class="n">x</span><span class="p">,</span><span class="n">y</span> <span class="o">=</span> <span class="n">bmap</span><span class="p">(</span><span class="n">lons</span><span class="p">,</span> <span class="n">lats</span><span class="p">)</span>
<span class="c1">#bmap.plot(x, y, &#39;o&#39;, markersize=5 ,markeredgecolor=&quot;none&quot;, alpha=0.33)</span>

<span class="n">db</span> <span class="o">=</span> <span class="mf">0.003</span> <span class="c1"># bin padding</span>
<span class="n">lon_bins</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">linspace</span><span class="p">(</span><span class="nb">min</span><span class="p">(</span><span class="n">lons</span><span class="p">)</span><span class="o">-</span><span class="n">db</span><span class="p">,</span> <span class="nb">max</span><span class="p">(</span><span class="n">lons</span><span class="p">)</span><span class="o">+</span><span class="n">db</span><span class="p">,</span> <span class="mi">10</span><span class="o">+</span><span class="mi">1</span><span class="p">)</span> <span class="c1"># 10 bins</span>
<span class="n">lat_bins</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">linspace</span><span class="p">(</span><span class="nb">min</span><span class="p">(</span><span class="n">lats</span><span class="p">)</span><span class="o">-</span><span class="n">db</span><span class="p">,</span> <span class="nb">max</span><span class="p">(</span><span class="n">lats</span><span class="p">)</span><span class="o">+</span><span class="n">db</span><span class="p">,</span> <span class="mi">13</span><span class="o">+</span><span class="mi">1</span><span class="p">)</span> <span class="c1"># 13 bins</span>
    
<span class="n">density</span><span class="p">,</span> <span class="n">_</span><span class="p">,</span> <span class="n">_</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">histogram2d</span><span class="p">(</span><span class="n">lats</span><span class="p">,</span> <span class="n">lons</span><span class="p">,</span> <span class="p">[</span><span class="n">lat_bins</span><span class="p">,</span> <span class="n">lon_bins</span><span class="p">])</span>

<span class="c1"># Turn the lon/lat of the bins into 2 dimensional arrays ready</span>
<span class="c1"># for conversion into projected coordinates</span>
<span class="n">lon_bins_2d</span><span class="p">,</span> <span class="n">lat_bins_2d</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">meshgrid</span><span class="p">(</span><span class="n">lon_bins</span><span class="p">,</span> <span class="n">lat_bins</span><span class="p">)</span>

<span class="c1"># convert the bin mesh to map coordinates:</span>
<span class="n">xs</span><span class="p">,</span> <span class="n">ys</span> <span class="o">=</span> <span class="n">bmap</span><span class="p">(</span><span class="n">lon_bins_2d</span><span class="p">,</span> <span class="n">lat_bins_2d</span><span class="p">)</span> <span class="c1"># will be plotted using pcolormesh</span>
<span class="c1"># ######################################################################</span>

<span class="c1"># define custom colormap, white -&gt; nicered, #E6072A = RGB(0.9,0.03,0.16)</span>
<span class="n">cdict</span> <span class="o">=</span> <span class="p">{</span><span class="s1">&#39;red&#39;</span><span class="p">:</span>  <span class="p">(</span> <span class="p">(</span><span class="mf">0.0</span><span class="p">,</span>  <span class="mf">1.0</span><span class="p">,</span>  <span class="mf">1.0</span><span class="p">),</span>
                   <span class="p">(</span><span class="mf">1.0</span><span class="p">,</span>  <span class="mf">0.9</span><span class="p">,</span>  <span class="mf">1.0</span><span class="p">)</span> <span class="p">),</span>
         <span class="s1">&#39;green&#39;</span><span class="p">:(</span> <span class="p">(</span><span class="mf">0.0</span><span class="p">,</span>  <span class="mf">1.0</span><span class="p">,</span>  <span class="mf">1.0</span><span class="p">),</span>
                   <span class="p">(</span><span class="mf">1.0</span><span class="p">,</span>  <span class="mf">0.03</span><span class="p">,</span> <span class="mf">0.0</span><span class="p">)</span> <span class="p">),</span>
         <span class="s1">&#39;blue&#39;</span><span class="p">:</span> <span class="p">(</span> <span class="p">(</span><span class="mf">0.0</span><span class="p">,</span>  <span class="mf">1.0</span><span class="p">,</span>  <span class="mf">1.0</span><span class="p">),</span>
                   <span class="p">(</span><span class="mf">1.0</span><span class="p">,</span>  <span class="mf">0.16</span><span class="p">,</span> <span class="mf">0.0</span><span class="p">)</span> <span class="p">)</span> <span class="p">}</span>
<span class="n">custom_map</span> <span class="o">=</span> <span class="n">LinearSegmentedColormap</span><span class="p">(</span><span class="s1">&#39;custom_map&#39;</span><span class="p">,</span> <span class="n">cdict</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">register_cmap</span><span class="p">(</span><span class="n">cmap</span><span class="o">=</span><span class="n">custom_map</span><span class="p">)</span>


<span class="c1"># add histogram squares and a corresponding colorbar to the map:</span>
<span class="n">plt</span><span class="o">.</span><span class="n">pcolormesh</span><span class="p">(</span><span class="n">xs</span><span class="p">,</span> <span class="n">ys</span><span class="p">,</span> <span class="n">density</span><span class="p">,</span> <span class="n">cmap</span><span class="o">=</span><span class="s2">&quot;custom_map&quot;</span><span class="p">)</span>

<span class="n">cbar</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">colorbar</span><span class="p">(</span><span class="n">orientation</span><span class="o">=</span><span class="s1">&#39;horizontal&#39;</span><span class="p">,</span> <span class="n">shrink</span><span class="o">=</span><span class="mf">0.625</span><span class="p">,</span> <span class="n">aspect</span><span class="o">=</span><span class="mi">20</span><span class="p">,</span> <span class="n">fraction</span><span class="o">=</span><span class="mf">0.2</span><span class="p">,</span><span class="n">pad</span><span class="o">=</span><span class="mf">0.02</span><span class="p">)</span>
<span class="n">cbar</span><span class="o">.</span><span class="n">set_label</span><span class="p">(</span><span class="s1">&#39;Number of Crimes&#39;</span><span class="p">,</span><span class="n">size</span><span class="o">=</span><span class="mi">18</span><span class="p">)</span>
<span class="c1">#plt.clim([0,100])</span>


<span class="n">bmap</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="s1">&#39;o&#39;</span><span class="p">,</span> <span class="n">markersize</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span><span class="c1">#zorder=6, </span>
          <span class="n">markerfacecolor</span><span class="o">=</span><span class="s1">&#39;#424FA4&#39;</span><span class="p">,</span><span class="n">markeredgecolor</span><span class="o">=</span><span class="s2">&quot;none&quot;</span><span class="p">,</span> <span class="n">alpha</span><span class="o">=</span><span class="mf">0.03</span><span class="p">)</span>
 
    
<span class="c1"># http://matplotlib.org/basemap/api/basemap_api.html#mpl_toolkits.basemap.Basemap.drawmapscale</span>
<span class="c1">#bmap.drawmapscale(-119-6, 37-7.2, -119-6, 37-7.2, 500, barstyle=&#39;fancy&#39;, yoffset=20000)</span>

<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Distribution of Crimes in San Francisco&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">annotate</span><span class="p">(</span><span class="s1">&#39;Southern&#39;</span><span class="p">,</span> <span class="n">xy</span><span class="o">=</span><span class="n">bmap</span><span class="o">.</span><span class="n">SFFindNeighborhoods</span><span class="p">[</span><span class="mi">21</span><span class="p">][</span><span class="mi">1</span><span class="p">],</span> 
             <span class="n">color</span> <span class="o">=</span><span class="s1">&#39;black&#39;</span><span class="p">,</span><span class="n">weight</span> <span class="o">=</span> <span class="s1">&#39;black&#39;</span><span class="p">,</span> <span class="n">size</span> <span class="o">=</span> <span class="mi">13</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">=</span><span class="mf">0.7</span><span class="p">)</span>

<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>warning: width and height keywords ignored for Mercator projection</pre>
</div>
</div>
