---
id: indici
tags: ["data access"]
aliases: 
index: 3
---

# Quando la struttura del file non e sufficiente: Indici

[L'organizzazione dei file](gestione_disco.md#Organizzazione%20dei%20file) da sola non e sufficiente, in molti casi sia [Heap file](gestione_disco.md#Heap%20file) che [Sequential file](gestione_disco.md#Sequential%20file) hanno i loro limiti, per esempio la ricerca nel primo caso e costosa e nel secondo e efficiente solo se effettuata sul campo di ordinamento del file

Per questo si introducono gli **indici**, strutture dati ausiliarie per facilitare l'accesso ai dati in fase di ricerca per uno specifico termine di ricerca

>[!TIP] il vantaggio sta nel fatto che l'indice e più piccolo -> ricerca più veloce

![](Pasted%20image%2020250130171838.png)

Da un punto di vista logico un indice e una collezione di coppie $(k_i,p_i)$ dove:
- $k$ e il valore di un attributo su cui l'indice e costruito
- $p$ e un RID (*massimo un PID*)  della tupla con il dato valore

esistono 2 tipologie principali di indici

## Indici ordinati

Le coppie sono ordinate per l'attributo chiave

## Indici hash

Viene utilizzata una funzione di hash per trovare la posizione di una data entry dato il valore della chiave

>[!WARNING] non il massimo per le ricerche a range

Ci sono inoltre diverse nomenclature applicate agli indici

- **clustered/unclustered** un indice si dice clustered se e costruito sull'attributo con cui e ordinato il data file
- **primary/secondary** se costruito su un attributo `unique` (tutto ciò che può essere chiave primaria)
- **dense/sparse** il numero di coppie nell'indice e uguale al numero di entry nel data file
- **single level/multi level** un indice multi livello e composto da indici sparsi che indicizzano altri indici (*possibili n livelli*)

## E nel disco? come rappresentare gli indici

Gli indici esattamente come il data file sono strutture dati che vanno caricate dal disco in memoria centrale, e necessario di conseguenza rappresentarle in maniera efficiente per non perdere i vantaggi di ricerca del indice.

## La soluzione B-tree

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

[PREVIOUS](pages/gestione_disco.md)
