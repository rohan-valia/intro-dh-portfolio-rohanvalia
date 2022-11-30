---
layout: page
title: Exploring and Analyzing Network Data with Python
description: This lesson uses the NetworkX Python package to analyze statistics regarding British Quakers social network and formulate inferences and conclusions on these network statistics.
---

## Source
[John R. Ladd, Jessica Otis, Christopher N. Warren, and Scott Weingart, "Exploring and Analyzing Network Data with Python," Programming Historian (2021)](https://programminghistorian.org/en/lessons/exploring-and-analyzing-network-data-with-python)

## Reflection
Network analysis involves the process of identifying links and connections between a social network of individuals. Using the NetworkX Python package, this programming historian lesson aims to quantatively analyze the social structure and the strength of the connections between the Quakers in seventeenth century England.

In following the code of this lesson, I was able to effectively understand the various quantative measurements that were used in evaluating the overall network construct and how the NetworkX package was applied. The flow and development of the code made sense, from first diagnosing and unpacking the numerical identities of the two datasets to then applying the NetworkX to create visual and numerical comparisons between the individual Quakers and the subgroups of the overall network. In doing so, I was able to learn how these quantitative metrics, such as degree, centrality, and modularity, can offer various identifiers of the individuals in the network, such as the number of connections an individual has, the strength of their connections, and structurally how these individuals are connected. By following this analysis of the network structure, I was able to understand how communities of individuals can be distinguished and what makes certain communities more tight knit than others, which can be based on the strength and association of the subgroups and individuals.

## Code

```python
import csv
from operator import itemgetter
import networkx as nx
from networkx.algorithms import community
```


```python
with open('quakers_nodelist.csv','r') as nodecsv:
    nodereader = csv.reader(nodecsv)
    nodes = [n for n in nodereader][1:]
    
node_names = [n[0] for n in nodes]

with open('quakers_edgelist.csv', 'r') as edgecsv:
    edgereader = csv.reader(edgecsv)
    edges = [tuple(e) for e in edgereader][1:]
```


```python
print(len(node_names))
```

    119



```python
print(len(edges))
```

    174



```python
G = nx.Graph()

G.add_nodes_from(node_names)
G.add_edges_from(edges)
```


```python
hist_sig_dict = {}
gender_dict = {}
birth_dict = {}
death_dict = {}
id_dict = {}

for node in nodes:
    hist_sig_dict[node[0]] = node[1]
    gender_dict[node[0]] = node[2]
    birth_dict[node[0]] = node[3]
    death_dict[node[0]] = node[4]
    id_dict[node[0]] = node[5]
    
nx.set_node_attributes(G, hist_sig_dict, 'historical_significance')
nx.set_node_attributes(G, gender_dict, 'gender')
nx.set_node_attributes(G, birth_dict, 'birth_year')
nx.set_node_attributes(G, death_dict, 'death_year')
nx.set_node_attributes(G, id_dict, 'sdfb_id')
```


```python
for n in G.nodes():
    print(n, G.nodes[n]['birth_year'])
```

    Joseph Wyeth 1663
    Alexander Skene of Newtyle 1621
    James Logan 1674
    Dorcas Erbery 1656
    Lilias Skene 1626
    William Mucklow 1630
    Thomas Salthouse 1630
    William Dewsbury 1621
    John Audland 1630
    Richard Claridge 1649
    William Bradford 1663
    Fettiplace Bellers 1687
    John Bellers 1654
    Isabel Yeamans 1637
    George Fox the younger 1551
    George Fox 1624
    John Stubbs 1618
    Anne Camm 1627
    John Camm 1605
    Thomas Camm 1640
    Katharine Evans 1618
    Lydia Lancaster 1683
    Samuel Clarridge 1631
    Thomas Lower 1633
    Gervase Benson 1569
    Stephen Crisp 1628
    James Claypoole 1634
    Thomas Holme 1626
    John Freame 1665
    John Swinton 1620
    William Mead 1627
    Henry Pickworth 1673
    John Crook 1616
    Gilbert Latey 1626
    Ellis Hookes 1635
    Joseph Besse 1683
    James Nayler 1618
    Elizabeth Hooten 1562
    George Whitehead 1637
    John Whitehead 1630
    William Crouch 1628
    Benjamin Furly 1636
    Silvanus Bevan 1691
    Robert Rich 1607
    John Whiting 1656
    Christopher Taylor 1614
    Thomas Lawson 1630
    Richard Farnworth 1630
    William Coddington 1601
    Thomas Taylor 1617
    Richard Vickris 1590
    Robert Barclay 1648
    Jane Sowle 1631
    Tace Sowle 1666
    Leonard Fell 1624
    Margaret Fell 1614
    George Bishop 1558
    Elizabeth Leavens 1555
    Thomas Curtis 1602
    Alice Curwen 1619
    Alexander Parker 1628
    John Wilkinson 1652
    Thomas Aldam 1616
    David Barclay of Ury 1610
    David Barclay 1682
    Sir Charles Wager 1666
    George Keith 1638
    James Parnel 1636
    Peter Collinson 1694
    Franciscus Mercurius van Helmont 1614
    William Caton 1636
    Francis Howgill 1618
    Richard Hubberthorne 1628
    William Ames 1552
    William Rogers 1601
    Isaac Norris 1671
    Anthony Sharp 1643
    Mary Fisher 1623
    Anne Conway Viscountess Conway and Killultagh 1631
    Samuel Fisher 1604
    Francis Bugg 1640
    Sarah Gibbons 1634
    William Tomlinson 1650
    Humphrey Norton 1655
    William Gibson 1628
    Gideon Wanton 1693
    John Wanton 1672
    Grace Chamber 1676
    Mary Prince 1569
    John Bartram 1699
    Edward Haistwell 1658
    John ap John 1625
    John Rous 1585
    Anthony Pearson 1627
    Solomon Eccles 1617
    John Burnyeat 1631
    Edward Burrough 1633
    Rebecca Travers 1609
    William Edmundson 1627
    Sarah Cheevers 1608
    Edward Pyott 1560
    Daniel Quare 1648
    John Penington 1655
    Mary Penington 1623
    Charles Marshall 1637
    Humphrey Woolrich 1633
    William Penn 1644
    Mary Pennyman 1630
    Dorothy Waugh 1636
    David Lloyd 1656
    Lewis Morris 1671
    Martha Simmonds 1624
    John Story 1571
    Thomas Story 1670
    Thomas Ellwood 1639
    William Simpson 1627
    Samuel Bownas 1677
    John Perrot 1555
    Hannah Stranger 1656



```python
density = nx.density(G)
print("Network density:", density)
```

    Network density: 0.02478279447372169



```python
fell_whitehead_path = nx.shortest_path(G, source="Margaret Fell", target="George Whitehead")
print("Shortest path between Fell and Whitehead:", fell_whitehead_path)
```

    Shortest path between Fell and Whitehead: ['Margaret Fell', 'George Fox', 'George Whitehead']



```python
print("Length of that path:", len(fell_whitehead_path)-1)
```

    Length of that path: 2



```python
print(nx.is_connected(G))
```

    False



```python
components = nx.connected_components(G)
largest_component = max(components, key=len)
```


```python
subgraph = G.subgraph(largest_component)
diameter = nx.diameter(subgraph)
print("Network diameter of largest component:", diameter)
```

    Network diameter of largest component: 8



```python
triadic_closure = nx.transitivity(G)
print("Triadic closure:", triadic_closure)
```

    Triadic closure: 0.16937799043062202



```python
degree_dict = dict(G.degree(G.nodes()))
nx.set_node_attributes(G, degree_dict, 'degree')
```


```python
print(G.nodes['William Penn'])
```

    {'historical_significance': 'Quaker leader and founder of Pennsylvania', 'gender': 'male', 'birth_year': '1644', 'death_year': '1718', 'sdfb_id': '10009531', 'degree': 18}



```python
sorted_degree = sorted(degree_dict.items(), key=itemgetter(1), reverse=True)
```


```python
print("Top 20 nodes by degree:")
for d in sorted_degree[:20]:
    print(d)
```

    Top 20 nodes by degree:
    ('George Fox', 22)
    ('William Penn', 18)
    ('James Nayler', 16)
    ('George Whitehead', 13)
    ('Margaret Fell', 13)
    ('Benjamin Furly', 10)
    ('Edward Burrough', 9)
    ('George Keith', 8)
    ('Thomas Ellwood', 8)
    ('Francis Howgill', 7)
    ('John Perrot', 7)
    ('John Audland', 6)
    ('Richard Farnworth', 6)
    ('Alexander Parker', 6)
    ('John Story', 6)
    ('John Stubbs', 5)
    ('Thomas Curtis', 5)
    ('John Wilkinson', 5)
    ('William Caton', 5)
    ('Anthony Pearson', 5)



```python
betweenness_dict = nx.betweenness_centrality(G)
eigenvector_dict = nx.eigenvector_centrality(G)

nx.set_node_attributes(G, betweenness_dict, 'betweenness')
nx.set_node_attributes(G, eigenvector_dict, 'eigenvector')
```


```python
sorted_betweenness = sorted(betweenness_dict.items(), key=itemgetter(1), reverse=True)

print("Top 20 nodes by betweenness centrality:")
for b in sorted_betweenness[:20]:
    print(b)
```

    Top 20 nodes by betweenness centrality:
    ('William Penn', 0.23999456006192205)
    ('George Fox', 0.23683257726065216)
    ('George Whitehead', 0.12632024847366005)
    ('Margaret Fell', 0.12106792237170329)
    ('James Nayler', 0.10446026280446098)
    ('Benjamin Furly', 0.06419626175167242)
    ('Thomas Ellwood', 0.046190623885104545)
    ('George Keith', 0.045006564009171565)
    ('John Audland', 0.04164936340077581)
    ('Alexander Parker', 0.03893676140525336)
    ('John Story', 0.028990098622866983)
    ('John Burnyeat', 0.028974117533439564)
    ('John Perrot', 0.02829566854990583)
    ('James Logan', 0.026944806605823553)
    ('Richard Claridge', 0.026944806605823553)
    ('Robert Barclay', 0.026944806605823553)
    ('Elizabeth Leavens', 0.026944806605823553)
    ('Thomas Curtis', 0.026729751729751724)
    ('John Stubbs', 0.024316593960227152)
    ('Mary Penington', 0.02420824624214454)



```python
top_betweenness = sorted_betweenness[:20]

for tb in top_betweenness:
    degree = degree_dict[tb[0]]
    print("Name:", tb[0], "| Betweenness Centrality:", tb[1], "| Degree:", degree)
```

    Name: William Penn | Betweenness Centrality: 0.23999456006192205 | Degree: 18
    Name: George Fox | Betweenness Centrality: 0.23683257726065216 | Degree: 22
    Name: George Whitehead | Betweenness Centrality: 0.12632024847366005 | Degree: 13
    Name: Margaret Fell | Betweenness Centrality: 0.12106792237170329 | Degree: 13
    Name: James Nayler | Betweenness Centrality: 0.10446026280446098 | Degree: 16
    Name: Benjamin Furly | Betweenness Centrality: 0.06419626175167242 | Degree: 10
    Name: Thomas Ellwood | Betweenness Centrality: 0.046190623885104545 | Degree: 8
    Name: George Keith | Betweenness Centrality: 0.045006564009171565 | Degree: 8
    Name: John Audland | Betweenness Centrality: 0.04164936340077581 | Degree: 6
    Name: Alexander Parker | Betweenness Centrality: 0.03893676140525336 | Degree: 6
    Name: John Story | Betweenness Centrality: 0.028990098622866983 | Degree: 6
    Name: John Burnyeat | Betweenness Centrality: 0.028974117533439564 | Degree: 4
    Name: John Perrot | Betweenness Centrality: 0.02829566854990583 | Degree: 7
    Name: James Logan | Betweenness Centrality: 0.026944806605823553 | Degree: 4
    Name: Richard Claridge | Betweenness Centrality: 0.026944806605823553 | Degree: 2
    Name: Robert Barclay | Betweenness Centrality: 0.026944806605823553 | Degree: 3
    Name: Elizabeth Leavens | Betweenness Centrality: 0.026944806605823553 | Degree: 2
    Name: Thomas Curtis | Betweenness Centrality: 0.026729751729751724 | Degree: 5
    Name: John Stubbs | Betweenness Centrality: 0.024316593960227152 | Degree: 5
    Name: Mary Penington | Betweenness Centrality: 0.02420824624214454 | Degree: 4



```python
communities = community.greedy_modularity_communities(G)

modularity_dict = {} 
for i,c in enumerate(communities): 
    for name in c:
        modularity_dict[name] = i 

nx.set_node_attributes(G, modularity_dict, 'modularity')
```


```python
class0 = [n for n in G.nodes() if G.nodes[n]['modularity'] == 0]

class0_eigenvector = {n:G.nodes[n]['eigenvector'] for n in class0}

class0_sorted_by_eigenvector = sorted(class0_eigenvector.items(), key=itemgetter(1), reverse=True)

print("Modularity Class 0 Sorted by Eigenvector Centrality:")
for node in class0_sorted_by_eigenvector[:5]:
    print("Name:", node[0], "| Eigenvector Centrality:", node[1])

```

    Modularity Class 0 Sorted by Eigenvector Centrality:
    Name: James Nayler | Eigenvector Centrality: 0.3352974100447867
    Name: Margaret Fell | Eigenvector Centrality: 0.253170949905681
    Name: Francis Howgill | Eigenvector Centrality: 0.19095393782681047
    Name: Richard Farnworth | Eigenvector Centrality: 0.15368535029296412
    Name: Anthony Pearson | Eigenvector Centrality: 0.11120476725256782



```python
for i,c in enumerate(communities):
    if len(c) > 2:
        print('Class '+str(i)+':', list(c)) 
```

    Class 0: ['Margaret Fell', 'Richard Farnworth', 'William Gibson', 'Robert Rich', 'Martha Simmonds', 'James Nayler', 'Dorcas Erbery', 'Thomas Lower', 'Gervase Benson', 'Thomas Holme', 'Hannah Stranger', 'Thomas Aldam', 'Francis Howgill', 'George Fox the younger', 'William Tomlinson', 'Anthony Pearson', 'Elizabeth Leavens']
    Class 1: ['Edward Haistwell', 'William Bradford', 'David Lloyd', 'Samuel Bownas', 'Joseph Besse', 'Tace Sowle', 'George Keith', 'Anne Conway Viscountess Conway and Killultagh', 'Isaac Norris', 'James Logan', 'Peter Collinson', 'Richard Claridge', 'William Penn', 'John Bartram', 'Jane Sowle', 'Isabel Yeamans', 'Thomas Story']
    Class 2: ['Elizabeth Hooten', 'Edward Burrough', 'William Crouch', 'George Fox', 'Leonard Fell', 'William Mead', 'William Coddington', 'John Crook', 'Ellis Hookes', 'Mary Prince', 'Thomas Salthouse', 'William Mucklow', 'Mary Fisher', 'William Dewsbury', 'John Perrot']
    Class 3: ['Gilbert Latey', 'Alexander Parker', 'Henry Pickworth', 'Sir Charles Wager', 'Francis Bugg', 'Richard Hubberthorne', 'Daniel Quare', 'Lewis Morris', 'Thomas Lawson', 'George Whitehead', 'Silvanus Bevan', 'Rebecca Travers', 'John Whitehead', 'Alice Curwen']
    Class 4: ['Samuel Clarridge', 'Anthony Sharp', 'William Rogers', 'William Edmundson', 'John ap John', 'William Simpson', 'James Claypoole', 'Thomas Ellwood', 'Joseph Wyeth', 'John Penington', 'Thomas Curtis', 'Mary Penington', 'John Burnyeat']
    Class 5: ['Robert Barclay', 'James Parnel', 'Samuel Fisher', 'Franciscus Mercurius van Helmont', 'William Caton', 'William Ames', 'John Swinton', 'Benjamin Furly', 'Stephen Crisp', 'David Barclay of Ury', 'John Stubbs']
    Class 6: ['Anne Camm', 'Charles Marshall', 'Thomas Camm', 'John Camm', 'John Audland', 'Solomon Eccles', 'John Wilkinson', 'Edward Pyott', 'John Story']
    Class 7: ['John Whiting', 'Christopher Taylor', 'Thomas Taylor']



```python
nx.write_gexf(G, 'quaker_network.gexf')
```


```python

```
