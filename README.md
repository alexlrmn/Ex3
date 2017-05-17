---
title: "310657051_201543915"
author: "Alex&Liad"
date: "May 5, 2017"
output: rmarkdown::github_document
---

# EX3 - Data collection & Network Analysis

# Question 1

## Preperations:
```{r}
install.packages('igraph')
library(igraph)

#Loading the data
connections.data <- read.csv('ga_edgelist.csv', header = T)
graph_connections <- graph.data.frame(connections.data,directed = F)

#Feel the data
graph_connections
```
![Caption for the graph_connections.](/images/graph_connections.JPG)

```r
#First look at the grapth
plot(graph_connections)
```

![Caption for the grapth_plot.](/images/graph_plot.JPG)

## a.

### i. Betweeness 

This chunk consists the results for Betweeness

```{r}
bet <-betweenness(graph_connections)
max_bet <- max(bet)
ind_max_bet<-which.max(bet)
bet
max_bet
ind_max_bet
```

> Sloan is the actor with the highest betweeness (115.3667)


![Caption for the highest betweeness.](/images/sloan_betweeness.JPG)


### ii. Closeness

This chunk consists the results for Closeness

```{r}
close <-closeness(graph_connections)
max_close <- max(close)
ind_max_close<-which.max(close)
close
max_close
ind_max_close
```

> Torres is the actor with the highest Closeness (0.003194888)


![Caption for the highest closeness.](/images/torres_closeness.JPG)

### iii. Eigencetor

This chunk consists the results for Eigencetor

```{r}
eigen<-eigen_centrality(graph_connections)
max_eigen<-max(eigen$vector)
ind_max_eigen<-which.max(eigen$vector)
eigen$vector
max_eigen
ind_max_eigen
```

> Karev is the actor with the highest eigencetor


![Caption for the highest eigencetor.](/images/karev_eigencetor.JPG)

## b.

### First Algorithm: Girvan-Newman
#### i. Community 1 - Girvan-Newman community detection

This chunk consists the creation of the first community detection algorithm

```{r}
set.seed(123)
GrivNewm <-  edge.betweenness.community(graph_connections)
comGN <- membership(GrivNewm)
plot(graph_connections, vertex.size=5,vertex.color=comGN, asp=FALSE)
```
![Caption for the Girvan-Newman community detection algorithm.](/images/community1_girvan-newman.JPG)


#### ii. Community 1 - Number of communities

This chunk consists the number of communities and their size

```{r}
table(comGN)
```

> Number of communities detected is 7, size of each community:


![Caption for the Girvan-Newman community detection algorithm size of each community.](/images/community1_girvan-newman_size.JPG)

#### iii. Community 1 - Modularity

This chunk consists the Modularity rate

```{r}
GrivNewm$modularity
max(GrivNewm$modularity)
which.max(GrivNewm$modularity)
```

> The highest modularity value achieved is:


![Caption for the Girvan-Newman community detection algorithm modularity.](/images/community1_girvan-newman_modularity.JPG)

### Second algorithm: Walktrap
#### i. Community 2 - walktrap community detection

This chunk consists the creation of the second community detection algorithm

```{r}
set.seed(123)
walktrap <- walktrap.community(graph_connections)
comWT <- membership(walktrap)
plot(graph_connections, vertex.size=5,vertex.color=comWT, asp=FALSE)
```


![Caption for the walktrap community detection algorithm.](/images/community2_walktrap.JPG)

#### ii. Community 2 - Number of communities

This chunk consists the number of communities and their size

```{r}
table(comWT)
```


> Number of communities detected is 7, size of each community:


![Caption for the walktrap community detection algorithm.](/images/community2_walktrap_size.JPG)

#### iii. Community 2 - Modularity

This chunk consists the Modularity rate

```{r}
walktrap$modularity
max(walktrap$modularity)
which.max(walktrap$modularity)
```
> The highest modularity value achieved is:


![Caption for the Girvan-Newman community detection algorithm modularity.](/images/community2_walktrap_modularity.JPG)


# Question 2
## Network of games between football clubs
Thanks for www.football-data.org for the data

## a. Network creation
> We used the API of the site: [www.football-data.org] for information about 50 different football clubs games in the europe league.The information retrieved was in JSON format, we parsed it to get information about each relavent game. From each game we extracted the hosting club, visiting club and the game final score. We ignored games which ended in a draw or there was no information about the score.Each game was saved in a CSV file, the winning team under the winning colomn and the losing team under the losing colomn.The graph created is a directed graph, when the edge points from the winning team to the losing team.

> To collect the data, we wrote a crawler in python. The code is in a file under the name of crawling.py. The crawler creates a CSV file named 'FootballResultsGraph.csv' 

#### API Football Games + creation the directed graph
```{r}
football.data <- read.csv('FootballResultsGraph.csv', header = T)
graph_football <- graph.data.frame(football.data,directed = T)
```

## b. Nodes and edges:
> Each node in the graph represent a football club. Each edge represent a game between two teams, the edge is directed, so the node where the edge comes from is the winnig team and the end of the edge points to the losing team. For each node, the in degree represent the number of games lost by the club, and the out degree represent the number of games won. In total, the grapth contains 195 nodes and 1158 edges.

## c.Graphs

## Feel the data

This chunk consists the graphs data

```{r}
graph_football
```
![Caption for the football graph.](/images/feel_the_graph.JPG)


#plot

This chunk consists the plot of the graph

```{r}
plot(graph_football)
```

![Caption for the football graph.](/images/football_layout.JPG)

Another look at the graph, each nodes size depends on the out degree(number of games won):
```r
V(graph_football1)$size=degree(graph_football1, mode="out")
plot(graph_football)
```

![Caption for the football graph, size.](/images/football_layout_clear.JPG)

Just labels:

```r
tkplot(graph_football,vertex.size=0, edge.arrow.size=0.3)
```

![Caption for the football graph labels.](/images/football_layout_labels.JPG)

## d. Betweeness, closeness and eignecetor

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
> The football club with the highest betweeness value is Manchester City


![Caption for the manchester city betweeness, size.](/images/manchester_city_betweenes.JPG)

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

> The football club with the highest closeness value is Manchester City


![Caption for the manchester city closeness, size.](/images/manchester_city_closeness.JPG)

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

> The football club with the highest eigencetor value is Hamburger SV


![Caption for the hamburger eigencetor, size.](/images/hamburger_eigencetor.JPG)


## First algorithm - Girvan-Newman
### Community 1 - Girvan-Newman community detection

This chunk consists the creation of the first community detection algorithm

```{r}
set.seed(123)
GrivNewm <-  edge.betweenness.community(graph_football)
comGN <- membership(GrivNewm)
plot(graph_football, vertex.size=5,vertex.color=comGN, asp=FALSE)
```

![Caption for football community1, size.](/images/football_community1.JPG)

### Community 1 - Number of communities

This chunk consists the number of communities and their size

```{r}
table(comGN)
```
Number of communities found is 8, with size of:

![Caption for football community1, size.](/images/football_community1_size.JPG)

## Community 1 - Modularity

This chunk consists the Modularity rate

```{r}
GrivNewm$modularity
max(GrivNewm$modularity)
which.max(GrivNewm$modularity)
```

Modularity highest value: 0.6744752

## Second algorithm - Walktrap
### Community 2 - walktrap community detection

This chunk consists the creation of the second community detection algorithm

```{r}
set.seed(123)
walktrap <- walktrap.community(graph_football)
comWT <- membership(walktrap)
plot(graph_football, vertex.size=5,vertex.color=comWT, asp=FALSE)
```

![Caption for football community1, size.](/images/football_community2.JPG)

### Community 2 - Number of communities

This chunk consists the number of communities and their size

```{r}
table(comWT)
```

Number of communities found is 8, with size of:


![Caption for football community1, size.](/images/football_community2_size.JPG)

### Community 2 - Modularity

This chunk consists the Modularity rate

```{r}
walktrap$modularity
max(walktrap$modularity)
which.max(walktrap$modularity)
```
Modularity highest value: 0.7775869

[www.football-data.org]: <www.football-data.org>

