---
id: operatori_relazionali
tags: ["operatori relazionali","operatori logici", "operatori fisici"]
aliases: 
index: 10
---

# Rispondere alle interrogazioni: operatori relazionali

Nei DBMS relazionali le interrogazioni vengono risolte combinando in maniera opportuna un insieme di operatori, di conseguenza e necessario

- implementare in maniera efficiente tali operatori
- saper trovare la miglior combinazione per rispondere in velocita

>[!NOTE] le prestazioni di risposta a una query dipendono da molti fattori tra cui numero di tuple, distribuzione delle stesse, presenza di indici, buffer ecc...

## Tipologie di operatori

Gli operatori si dividono in due categorie

| Operatori logici                                                                                                       | Operatori fisici                                                                                            |
| ---------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| estensione di quelli messi a disposizione dall'algebra relazionale, forniscono un insieme di tuple con certe proprietà | implementazione effettiva degli operatori logici, a questi e possibile associare un **costo di esecuzione** |

## Operatori logici

Gli operatori logici sono i seguenti:

- **ordinamento**
- **selezione**
- **proiezione**
- **join**
- **operatori insiemistici**
- **group by**
- **operatori aggregati**
- **operatori di modifica** (*update, delete, insert*)

## Stime di costo di un operatore

Per poter stimare il costo di un operatore si prendono in considerazione i seguenti parametri (*reperibili dai cataloghi del database*)

- $N(R)$ = numero di record di $R$
- $P(R)$ = numero di pagine di $R$
- $Len(R)$ = lunghezza (in byte) di un record di $R$
- $NK(R.A)$ = numero di valori distinti dell'attributo $R.A$
- $TP(R)$ = numero di tuple per pagina
- $B$ = numero di pagine buffer a disposizione per l'operatore
- $L(IX)$ = numero di pagine foglia dell’indice $IX$

[PREVIOUS](pages/durability_control.md) [NEXT](pages/sorting.md)
