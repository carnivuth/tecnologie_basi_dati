---
id: group_by
tags: ["funzioni aggregate","group by ordinando","group by con hashing", "group by con indice"]
aliases: 
index: 15
---

# Funzioni aggregate

 in caso di funzioni aggregate come
 
```sql
SELECT AVG(eta)
FROM Sommelier S
```

Tutti i record vengono scanditi  e vengono mantenute informazioni aggiuntive

| **Funzione** | Informazione mantenuta    |
| ------------ | ------------------------- |
| **SUM**      | totale dei valori stimati |
| **AVG**      | totale e numero di valori |
| **MIN**      | minimo dei valori         |
| **MAX**      | massimo dei valori        |
| **COUNT**    | numero dei valori         |

# Group by

In caso di raggruppamenti come:

```sql
SELECT S.livello, MIN(età)
FROM Sommelier S
GROUP BY S.livello
```

e necessario partizionare i record e calcolare le funzioni di aggregazione per ogni record, ci sono 3 principali strategie:

## Group by per mezzo di sorting

Una delle possibilità e quella di sfruttare tecniche di ordinamento come quelle viste per la [proiezione](proiezione.md#Proiettare%20[ordinando](sorting.md)), va sommato il costo di calcolo delle funzioni aggregate

## Group by per mezzo di indici

In caso di indici sugli attributi di group by e di calcolo delle funzioni non e necessario accedere al file dati

>[!TIP] in caso di [b+tree](b+tree.md) se gli attributi di raggruppamento sono un prefisso della chiave si può utilizzare l'indice per accedere al file dati in maniera ordinata

## Group by usando hashing

Si costruisce una tabella di hash in memoria centrale in maniera analoga al caso della [proiezione](proiezione.md#Proiettare%20usando%20hashing)

[PREVIOUS](pages/join.md) [NEXT](pages/operatori_modifica.md)
