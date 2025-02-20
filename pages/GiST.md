---
id: GiST
tags: ["implementazione r-tree","implementazione b+tree","GiST"]
aliases: 
index: 6
---

# Implementando i [b+tree](b+tree.md): GiST

Generalized search tree (*[GiST](https://en.wikipedia.org/wiki/GiST)*) e una struttura generalizzata per l'implementazione di indici, che se opportunamente istanziata puo comportarsi da diverse tipologie di albero ([b+tree](b+tree.md), [r-tree](r-tree.md))

La specifica GiST modella le query come predicati e la risoluzione di una query come la ricerca nell'albero del predicato che la soddisfa

Internamente un GiST e composto da una lista linkata di **entries** composte come `<p,ptr>` dove `p` e un predicato e `ptr` un puntatore a un altra entry che soddisfa il suddetto predicato

Le api della specifica si dividono in funzioni di chiave e funzioni d'albero, le seconde richiamano le prime per implementare le operazioni di manipolazione del indice

## Funzioni di chiave

- `Consistent(e,q)` controlla se un data entry e consistent con un dato predicato
- `union(P)` restituisce il predicato che include le entry della lista `P`
- `compress(E)/decompress(E)` comprimono/decomprimono una entry
- `penalty(E1,E2)` restituisce il costo di inserimento della entry `E1` nella entry `E2`, usata come metrica per determinare la politica di inserimento
- `pickSplit` implementa il processo decisionale per determinare dove l'albero viene splittato

## Funzioni d'albero

- `search` implementa la ricerca dato un predicato, utilizza la funzione `consistent`, nel caso di un  [b+tree](b+tree.md) la ricerca termina con il raggiungimento della prima foglia e lo scorrimento della lista (*il dominio di un B+tree e totalmente ordinato*)
- `insert` inserisce un nodo nell'albero (*entra in gioco anche quando ci sono entry orfane*)
- `chooseSubtree` sceglie il sottoalbero piu adatto per l'inserimento di una entry
- `split` divide l'albero a seguito di un bilanciamento
- `delete` elimina una entry dall'albero
- `adjustKeys` aggiusta il valore delle chiavi dei nodi intermedi e controlla che il predicato dei figli corrisponda a quello del padre per mezzo di `union`
- `condenseTree` effettua il reinserimento di entry orfane nell'albero

[PREVIOUS](pages/b+tree.md) [NEXT](pages/indici_hash.md)
