# EX3 - Data collection & Network Analysis

---
title: "310657051_201543915"
author: "Alex&Liad"
date: "May 5, 2017"
output: rmarkdown::github_document
---

# Question 1

## Package and code used:
```{r}
install.packages('igraph')
library(igraph)

#Loading the data
connections.data <- read.csv('ga_edgelist.csv', header = T)
graph_connections <- graph.data.frame(connections.data,directed = F)
graph_connections
```
![Caption for the graph_connections.](/images/graph_connections.jpg)

```r
#First look at the grapth
plot(graph_connections)
```

![Caption for the grapth_plot.](/images/graph_plot.jpg)


## Read the data

This chunk consists the read of the data

```{r}
connections.data <- read.csv('ga_edgelist.csv', header = T)
graph_connections <- graph.data.frame(connections.data,directed = F)

```

## Feel the data

This chunk consists the graph data

```{r}
graph_connections
```

#plot

This chunk consists the plot of the graph

```{r}
plot(graph_connections)
```

## Betweeness 

This chunk consists the results for Betweeness

```{r}
bet <-betweenness(graph_connections)
max_bet <- max(bet)
ind_max_bet<-which.max(bet)
bet
max_bet
ind_max_bet
```

##  Closeness

This chunk consists the results for Closeness

```{r}
close <-closeness(graph_connections)
max_close <- max(close)
ind_max_close<-which.max(close)
close
max_close
ind_max_close
```

## Eigencetor

This chunk consists the results for Eigencetor

```{r}
eigen<-eigen_centrality(graph_connections)
max_eigen<-max(eigen$vector)
ind_max_eigen<-which.max(eigen$vector)
eigen$vector
max_eigen
ind_max_eigen
```


## Community 1 - Girvan-Newman community detection

This chunk consists the creation of the first community detection algorithm

```{r}
set.seed(123)
GrivNewm <-  edge.betweenness.community(graph_connections)
comGN <- membership(GrivNewm)
plot(graph_connections, vertex.size=5,vertex.color=comGN, asp=FALSE)
```

## Community 1 - Number of communities

This chunk consists the number of communities and their size

```{r}
table(comGN)
```

## Community 1 - Modularity

This chunk consists the Modularity rate

```{r}
GrivNewm$modularity
max(GrivNewm$modularity)
which.max(GrivNewm$modularity)
```

## Community 2 - walktrap community detection

This chunk consists the creation of the second community detection algorithm

```{r}
set.seed(123)
walktrap <- walktrap.community(graph_connections)
comWT <- membership(walktrap)
plot(graph_connections, vertex.size=5,vertex.color=comWT, asp=FALSE)
```

## Community 2 - Number of communities

This chunk consists the number of communities and their size

```{r}
table(comWT)
```

## Community 2 - Modularity

This chunk consists the Modularity rate

```{r}
walktrap$modularity
max(walktrap$modularity)
which.max(walktrap$modularity)
```

## API Football Games + creation the directed graph
```{r}
football.data <- read.csv('FootballResultsGraph.csv', header = T)
graph_football <- graph.data.frame(football.data,directed = T)
```

## Feel the data

This chunk consists the graphs data

```{r}
graph_football
```

#plot

This chunk consists the plot of the graph

```{r}
plot(graph_football)
```

## Betweeness

This chunk consists the results for Betweeness

```{r}
bet <-betweenness(graph_football)
max_bet <- max(bet)
ind_max_bet<-which.max(bet)
bet
max_bet
ind_max_bet
```

##  Closeness

This chunk consists the results for Closeness

```{r}
close <-closeness(graph_football)
max_close <- max(close)
ind_max_close<-which.max(close)
close
max_close
ind_max_close
```

## Eigencetor

This chunk consists the results for Eigencetor

```{r}
eigen<-eigen_centrality(graph_football)
max_eigen<-max(eigen$vector)
ind_max_eigen<-which.max(eigen$vector)
eigen$vector
max_eigen
ind_max_eigen
```

## Community 1 - Girvan-Newman community detection

This chunk consists the creation of the first community detection algorithm

```{r}
set.seed(123)
GrivNewm <-  edge.betweenness.community(graph_football)
comGN <- membership(GrivNewm)
plot(graph_football, vertex.size=5,vertex.color=comGN, asp=FALSE)
```

## Community 1 - Number of communities

This chunk consists the number of communities and their size

```{r}
table(comGN)
```

## Community 1 - Modularity

This chunk consists the Modularity rate

```{r}
GrivNewm$modularity
max(GrivNewm$modularity)
which.max(GrivNewm$modularity)
```

## Community 2 - walktrap community detection

This chunk consists the creation of the second community detection algorithm

```{r}
set.seed(123)
walktrap <- walktrap.community(graph_football)
comWT <- membership(walktrap)
plot(graph_football, vertex.size=5,vertex.color=comWT, asp=FALSE)
```

## Community 2 - Number of communities

This chunk consists the number of communities and their size

```{r}
table(comWT)
```

## Community 2 - Modularity

This chunk consists the Modularity rate

```{r}
walktrap$modularity
max(walktrap$modularity)
which.max(walktrap$modularity)
```
