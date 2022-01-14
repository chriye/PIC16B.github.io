---
layout: post
title: Data visualization tutorial
---

In this post, we'll show some examples of constructing data visualizaiton.

# Introduction

Matplotlib, seaborn, and plotly are methods that we can use to construct data visualization. Here, we'll just focus on plotly.

## Let's get started!!
### Set up

1. Download Anaconda navigator.
2. Open Anaconda app, click on environments and search for plotly.
3. Download the plotly packages
4. Go back to the home page, open the jupyter notebook

### Ready to plot!!

#### Step 1: Load the data set and clean up the data

Since there're useless columns in the data, so we want to clean it up before plotting. And the data set that we use here is Palmer Penguins

```python
import pandas as pd
# url for the data set
url = "https://raw.githubusercontent.com/PhilChodrow/PIC16B/master/datasets/palmer_penguins.csv"
# read the data set and sign it to penguins variable
penguins = pd.read_csv(url)
# simplified the species name
penguins["Species"] = penguins["Species"].str.split().str.get(0)
# delete the row the Sex is .
penguins = penguins[penguins["Sex"] != "."]
# select the column that I 
cols = ["Species", "Island", "Sex", "Culmen Length (mm)", "Culmen Depth (mm)", "Flipper Length (mm)", "Body Mass (g)"]
penguins = penguins[cols]
```



#### Step 2. Import packages to plot

In order to made a super cool plot, we need plotly packages.

```python
from plotly import express as px
import plotly.io as pio
```

### *Scatter plot*

When we made the scatter plot, we need to specifies the data set that we want to plot, and the data for x-axis, y-axis.

```python
# made the scatter plot
fig = px.scatter(data_frame = penguins, 
                 x = "Culmen Length (mm)", # x-axis 
                 y = "Culmen Depth (mm)", # y-axis
                 title = "Culmen Length vs Culmen Depth scatter plot",
                 color = "Species", # color of data points
                 width = 500, # size of the plot
                 height = 300)

# show the plot
fig.show()

# save the plot
from plotly.io import write_html
write_html(fig, "scatter_plot.html")
```

{% include scatter_plot.html %}

### *Historgram*

Here we only need to specifies the data set and the data for x-axis.

```python
# made the histogram plot
fig = px.histogram(penguins,
                   x = "Culmen Length (mm)",
                   title = "Culmen Length histogram",
                   color = "Species",
                   nbins = 30, # number of bins
                   width = 600, # size
                   height = 300)

# show the plot
fig.show()

# save the plot
from plotly.io import write_html
write_html(fig, "hist_plot.html")
```
{% include hist_plot.html %}

