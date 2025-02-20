---
id: r-tree
tags: ["r-tree vs b+tree","minimum bounding box","MBB","search with r-tree"]
aliases: 
index: 21
---

# R-tree

Gli r-tree sono alberi paginati e bilanciati dove ogni nodo corrisponde a una regione triangolare detta minimal bounding box (*MMB*) che contiene tutte le regioni figlie

L'utilizzo dello storage da parte di un nodo varia dal $100\%$ a un valore minimo inferiore al $50\%$ (*parametro tunabile*)

Le foglie dell'albero sono entry nella forma  `(key, RID)`, dove il valore di chiave contiene le coordinate
>[!NOTE] possibile contenere anche oggetti con un estensione spaziale

I nodi interni dell'albero si presentano nella forma `(MBB, PID)`, dove la chiave sono le coordinate della minimal bounding box

![](Pasted%20image%2020250216184643.png)

## Concetto di MBB

La minima bounding box e definita come la regione hyper-rettangolare minima che contiene un set di punti $m$

![](Pasted%20image%2020250216184057.png)

Per definirla e sufficiente conoscere le coordinate di due vertici opposti

## R-tree vs [b+tree](b+tree.md)


| B+tree                                                 | R-tree                                                                 |
| ------------------------------------------------------ | ---------------------------------------------------------------------- |
| bilanciato e paginato                                  | bilanciato e paginato                                                  |
| i dati sono contenuti nelle foglie                     | i dati sono contenuti nelle foglie                                     |
| le foglie sono ordinate                                | non esiste l'ordine                                                    |
| i dati sono organizzati in intervalli monodimensionali | i dati sono organizzati in intervalli multidimensionali                |
| la ricerca puntuale segue un solo percorso dell'albero | la ricerca puntuale può seguire strade diverse all'interno dell'albero |

## Ricerca con r-tree

La ricerca con un r-tree consiste nel trovare tutti i punti che fanno parte della bounding box della query di ricerca

![](Pasted%20image%2020250218100138.png)

Per implementare la ricerca e necessario implementare le API previste dalla specifica [GiST](GiST.md)

- `Consistent(E,q)` ritorna true solo se `E` e `q` hanno intersezione non nulla
- `Union(P)` l'output e la MMB che contiene tutte le entry
-  `Penalty(E1,E2)` Se il punto si trova dentro la bounding box la penalty e `0` altrimenti e data dal aumento di dimensione della bounding box stessa
- `Picksplit(P)` in output vengono fornite le entry e l'output e un set di due bounding box con cardinalità inferiore, lo split viene deciso minimizzando l'area complessiva delle due [MBB](#Concetto%20di%20MBB)
>[!WARNING] minimizzare la somma complessiva e un problema Np-hard  

[PREVIOUS](pages/indici_multidimensionali.md) [NEXT](pages/top_k_queries.md)
