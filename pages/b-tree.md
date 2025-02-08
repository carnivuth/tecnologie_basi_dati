---
id: b-tree
tags: ["indici", "b-tree", "indici ordinati"]
aliases: 
index: 4
---

# La soluzione B-tree

Gli indici B-tree sono strutture dati ad albero bilanciate in cui i singoli nodi rappresentano delle pagine dati, il bilanciamento e mantenuto dalle operazioni di inserimento e update.

Il numero di entries di un nodo e un valore $m$ nell'intervallo $d-2d$ dove $d$ e detto ordine dell'albero

il numero di nodi figli e $m+1$ e oscilla nell'intervallo $d+1 - 2d+1$

### Algoritmo di ricerca di un b-tree

L'algoritmo di ricerca, dato un valore della chiave percorre l'albero prendendo in considerazione il figlio $i$-esimo con tale per cui $k_{i-1}<k<k_i$ 

### Costo di una ricerca in un b-tree

In una ricerca in un b-tree il costo e dato dall'altezza dell'albero + l'accesso al data file

$$
costo = h - 1 + 1
$$
> la root si presume già essere in memoria centrale

Di conseguenza e necessario poter computare l'altezza di un b-tree

Si ha che il numero massimo di nodi di un b-tree e dato quando tutti i nodi hanno $2d+1$ entry di conseguenza si ha che

$$
b_{max} = \sum_{i=0}^{h-1}{(2d+1)^i} = \frac{(2d-1)^h-1}{2d}
$$

Di conseguenza il massimo numero di entry e dato da

$$
N_{max} = 2db_{max} = (2d +1)^h -1
$$

Viceversa il numero minimo di nodi si ha quando tutti escluso la root sono pieni a meta ovvero hanno $d$ entry

$$
b_{min} = 1 + 2\sum_{i=0}^{h-2}{(d+1)^i} = 1+ 2\frac{(d+1)^{h-1}-1}{d}
$$

Di conseguenza il minimo numero di entry e dato da

$$
N_{min} = 1 + d(b_{min}- 1) = 2(d +1)^{h-1} -1
$$

L'altezza dell'albero e di conseguenza inclusa nel range:

$$
\lceil \log_{2d+1}{(N+1)}\rceil \leq h \leq \lfloor \log_{d+1}(\frac{N+1}{2})\rfloor +1
$$

### Limitazioni di un b-tree

Un B-tree risulta inefficente nelle ricerche a range in quanto le entry sono contenute anche nei nodi intermedi, per risolvere questo problema si introducono i B+tree

[PREVIOUS](pages/indici.md) [NEXT](pages/b+tree.md)
