---
title: "Holiday Line Chart Tutorial"
author: "Elyssa Pergola"
date: "2022-11-27"
output:
  pdf_document: default
  theme: cayman
  prettydoc::html_pretty: null
  highlight: github
---
# How To Create A Holiday Line Chart

<p align="center">
<img src="Pics/Tree.png" width="300px" height="300x"/>
</p>

## Tutorial Aims

1. Understand how to create a simple line graph with ggplot2
2. Learn how to make a legend
3. Learn how to label the axes
4. Learn how to change the colors of the graph

## Introduction

What is a line chart? A line chart depicts the changes in values over a certain set of variables on the x-axis. The x-axis is using a measure of time (days, months, years). This is an example of a typical line graph:

<img src="Pics/Generic_Line_Chart.jpg"/> 

---

## Data We Will Use For This Tutorial

Since it is the holiday season, we will be looking at data involving christmas trees. Some people choose to get a real Christmas tree, while other prefer to use a fake one. We will be looking at the total number of trees sold, the number of fake trees sold, and the number of real trees sold throughout the years.  

---

## How To Start

You will need to install the packages that you will be using. You already may have some of these installed, so if you do it is unnecessary to install them again.

Use install.packages() to install a package. We will be using tidyverse, ggplot2, and readr

Then, you will need to load the libraries of these packages.

```{r}
# Libraries
library(tidyverse)
library(ggplot2)
library(readr)
```

Next you will need to load the tree data that we will be using to make the line charts:
```{r}
Tree_Data <- read.csv("Data/Christmas_Tree.csv") # Loading Tree Data
```

--- 

# Make a simple line chart with real trees sold

We will be using a package called ggplot to make our line graphs. This package helps us to visualize data. After ggplot, we will put the data we will be using (Tree_Data). Next we will use aes which is the aesthetic mapping function. This will allow us to say what data we want to put on the x-axis and the y-axis. We will put a plus sign and then geom_line() to make the line graph. 

```{r}
ggplot(Tree_Data, aes(x=Year, y=X._real_trees_sold)) + # Year is on the X-axis, Real trees sold is on the y axis
  geom_line() # Makes it a line chart
```

---

# Add the fake trees line and total trees line

Next, we will add the lines for the fake trees sold and the total tree sold over the years. 

```{r}
ggplot(Tree_Data, aes(x=Year)) +
  geom_line(aes(y = X._real_trees_sold)) + # Line for real trees sold
  geom_line(aes(y = X._fake_trees_sold)) + # Line for fake trees sold
  geom_line(aes(y = total_trees_sold)) # Line for total trees sold
```

---

# Add a title

Next, we will add a title for the graph.

```{r}
ggplot(Tree_Data, aes(x=Year)) +
  geom_line(aes(y = X._real_trees_sold)) + # Line for real trees sold
  geom_line(aes(y = X._fake_trees_sold)) + # Line for fake trees sold
  geom_line(aes(y = total_trees_sold)) + # Line for total trees sold
  ggtitle("Trees Sold Over Time") # Title
```

---

# Add axis labels

Next, we will add appropriate axis labels. 
```{r}
ggplot(Tree_Data, aes(x=Year)) +
  geom_line(aes(y = X._real_trees_sold)) + # Line for real trees sold
  geom_line(aes(y = X._fake_trees_sold)) + # Line for fake trees sold
  geom_line(aes(y = total_trees_sold)) + # Line for total trees sold
  ggtitle("Trees Sold Over Time") + # Title
  labs(y = "Number of Trees Sold", x = "Year") # Y and x labels
```

---

## Adding Colors To The Lines
In order to differentiate what the different lines are showing, we will want to make the lines different colors. In honor of the holiday season, we will be using Christmas colors: gold, green, and red. 

In order to find the colors I wanted, I just googled colors to use in ggplot in R. This is the link I found: http://sape.inf.usi.ch/quick-reference/ggplot2/colour

Here are some of the color options:
<img src="Pics/Colors.jpg"/> 

You can also install other color packages: https://www.datanovia.com/en/blog/top-r-color-palettes-to-know-for-great-data-visualization/

---

## Adding a Legend

Now, we will add a legend so that we understand what line is for what part of the data (real trees, fake, trees, or total trees). 

```{r}
ggplot(Tree_Data, aes(x=Year)) +
  geom_line(aes(y = X._real_trees_sold, color = "Real Trees Sold")) + # Line for real trees sold
  geom_line(aes(y = X._fake_trees_sold, color = "Fake Trees Sold")) + # Line for fake trees sold
  geom_line(aes(y = total_trees_sold, color = "Total Trees Sold")) + # Line for total trees sold
  ggtitle("Trees Sold Over Time") + # Title
  scale_colour_manual("", breaks = c("Real Trees Sold", "Fake Trees Sold", "Total Trees Sold"), # Making the Legend
  values = c("forestgreen", "red", "goldenrod1")) + # Assigning colors to each of the lines
  labs(y = "Number of Trees Sold", x = "Year") # Y and x labels
```

---

## Try To Make a Line Graph By Yourself

Now, it is time to try to make a line graph by yourself. Sally needs your help. She wants to see how the number of presents she got during the holidays has changed over the years. When she behaves better, she gets more presents. This year, she wants to get more presents than she ever has! Help her make a line graph of the presents she has gotten over the years. She also has a special request of making the graph pink (since it is her favorite color). She also wants x and y axis labels and a title!

Use the data: Gift_Data.csv

<p align="center">
<img src="Pics/Present.jpg" width="300px" height="300x"/>
</p>


### Solution?

<details>
  <summary>Click For Answer</summary>
```{r}
Gift_Data <- read.csv("Data/Gift_Data.csv")

ggplot(Gift_Data, aes(x=Year)) + # Year is on the X-axis
  geom_line(aes(y=Number_of_Presents_Sally_Got), color = "pink") + # Makes it a line chart and makes it pink
  labs(y = "Number of Presents Sally Got", x = "Year") + # X and y labels
  ggtitle("Number of Presents Sally Got For Christmas Over Time") # Title
```
  
## Extra Resources To Check Out About Line Graphs

1. https://www.data-to-viz.com/graph/line.html

2. https://r-graph-gallery.com/line-chart-ggplot2.html

3. http://www.sthda.com/english/wiki/ggplot2-line-plot-quick-start-guide-r-software-and-data-visualization

### My Sources

1. https://chartio.com/learn/charts/line-chart-complete-guide/

2. https://www.geeksforgeeks.org/add-legend-for-multiple-lines-in-r-using-ggplot2/

3. https://www.datanovia.com/en/blog/top-r-color-palettes-to-know-for-great-data-visualization/

4. https://www.geeksforgeeks.org/add-legend-for-multiple-lines-in-r-using-ggplot2/

5. https://stackoverflow.com/questions/10349206/add-legend-to-ggplot2-line-plot

6. https://app.getguru.com/card/iMM777jT/Creating-Collapsible-Sections-in-Markdown

7. https://codinhood.com/nano/git/center-images-text-github-readme

8. https://prettydoc.statr.me/
