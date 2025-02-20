---
id: indici_multidimensionali
tags: ["excell","grid","k-d-tree","k-d-B-tree"]
aliases: 
index: 20
---

# Indici $n$-dimensionali

Nati per soddisfare query che coinvolgono molteplici attributi, tra cui

- query puntuali $A_1 = v_1, A_2 = v_2, … , A_n = v_n$ 
- query finestra $l_1 \leq A_1 \leq h_0, l_2 \leq A_2 \leq h_2, … , l_n \leq A_n \leq h_n$
- nearest neighbor query $A_1 \approx v_1, A_2 \approx v_2, … , A_n \approx v_n$ 

## Limiti del [b+tree](b+tree.md)

Supponendo di avere una window query su due attributi $A,B$ del tipo

```sql
SELECT * FROM table as T
WHERE T.A > 10
AND T.A < 20
AND T.B > 10
AND T.B < 20
```

In questo caso e possibile utilizzare un indice [b+tree](b+tree.md) su entrambi gli attributi oppure 2 indici monodimensionali su i due attributi

>[!ERROR] In entrambi i casi si compie del lavoro inutile perché i punti spazialmente vicini non sono posti nelle stesse foglie

## Indicizzamento spaziale

Per affrontare il problema sono state proposte una marea di strutture dati ma il concetto resta lo stesso, **mappare record spazialmente vicini nelle stesse pagine**

## K-d-tree

Struttura mantenuta in memoria centrale non paginata e non bilanciata, dove ogni nodo rappresenta uno split sul valore mediana dell'attributo con la maggiore varianza

![](Pasted%20image%2020250216172340.png)

### K-d-tree ricerca

In caso di ricerca si visitano tutti i rami dell'albero che contengono regioni che si intersecano con la regione definita dalla query

>[!WARNING] dato che l'albero non e bilanciato sono necessarie operazioni di ribilanciamento periodiche

>[!ERROR] le eliminazioni sono estremamente complicate

## Paginando il k-d-tree: k-d-B-tree

E la versione paginata del [K-d-tree](#K-d-tree) dove ogni nodo corrisponde a un iper-rettangolo dello spazio ottenuto come unione delle regioni figlie

![](Pasted%20image%2020250216182013.png)

### K-d-B-tree: overflow

In caso di overflow si partizionano i nodi padri fino a risalire alla root

>[!WARNING] non e sempre possibile mantenere il bilanciamento durante l'operazione di split

## hB-tree

Variante del [k-d-B-tree](#Paginando%20il%20k-d-tree%20k-d-B-tree) in cui le regioni possono contenere *buchi*, questo migliora la situazione in caso di split di un data block la differenza e data dal fatto che un nodo può essere referenziato da più separazioni

![](Pasted%20image%2020250216182500.png)

### hB-tree: split

In caso di split della root i nodi figli vengono splittati come segue

![](Pasted%20image%2020250216182641.png)

## Excell

Tecnica basata su una hash directory fatta a griglia $n$-dimensionale dove ogni cella corrisponde a una datapage **ma non e vero il contrario**, estendendo il concetto di [extendible hashing](indici_hash.md#Extendible%20hashing) al caso multidimensionale.

![](Pasted%20image%2020250216182829.png)

### Excell: split


In caso di split ci sono due casistiche:

- split di una datapage referenziata da due celle della directory, in questo caso e sufficiente aggiornare le referenze della directory
- split di una datapage referenziata da una cella della directory in questo caso si raddoppia la dimensione della griglia

>[!NOTE] tutte le problematiche e considerazioni fatte per l'[extendible hashing](indici_hash.md#Extendible%20hashing) restano valide 


## Grid file

Versione generalizzata del [Excell](#Excell), dove gli intervalli hanno dimensione variabile, 

![](Pasted%20image%2020250216183422.png)

## Mono-dimensional sorting

Si basa sul concetto di linearizzare lo spazio n dimensionale per mezzo delle cosiddette space-filling curves

![](Pasted%20image%2020250216183530.png)

>[!ERROR] In questo caso preservare l'ordine locale risulta quasi impossibile

[PREVIOUS](pages/progetto_fisico_tuning.md) [NEXT](pages/r-tree.md)
