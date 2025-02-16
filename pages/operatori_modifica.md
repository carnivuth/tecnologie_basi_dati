---
id: operatori_modifica
tags: []
aliases: 
index: 16
---

# Operatori di modifica

Le operazioni che scatenano operatori di modifica sono `INSERT` `UPDATE` e `DELETE` ma **solo le ultime due necessitano di un percorso di accesso ai dati**

Il costo di queste operazioni e diviso in tre componenti:

- costo di accesso ai dati
- costo di modifica
- costo di aggiornamento di [indici](indici.md)

## Costo di inserimento

In caso di inserimento in [file non ordinato](gestione_disco.md#Heap%20file) e necessario considerare il costo di aggiunta in fondo al file  e di modifica degli indici:

- $2*Nindici$ se si fanno le modifiche in maniera indipendente
- $2*\Phi(KI,L)$ se si ordinano i record per valore di chiave

## Costo della eliminazione

In caso di eliminazione il costo di modifica dei dati dipende da come si accede ai dati 

- scansione ordinata $\Phi(E,P)$ con $E = f*N$ (*fare riferimento a [questa sezione](operatori_relazionali.md#Stime%20di%20costo%20di%20un%20operatore)*) 
- scansione disordinata $EK*\Phi(N/NK,EP)$ con $EK = f*NK$ (*in caso di indici un-clustered*)

Il costo di modifica conseguente degli indici e stimabile come segue

- $2*f*N$ se le eliminazioni sono indipendenti
- $2\Phi(KD,L)$ se si ordinano i record per valore della chiave

## Costo dell'aggiornamento: la sindrome di Halloween

In caso di query di update come segue

```sql
UPDATE Somelier
SET livello =livello +1
WHERE livello BETWEEN 3 AND 5
```

Si hanno situazioni in cui il db aggiorna dei record più volte se viene utilizzato un indice che ha nella chiave l'attributo di modifica

>[!TIP] in DB2 il problema di Halloween non si presenta in quanto i RID vengono ordinati e modificati e solo dopo si aggiornano gli indici

I costi sono gli stessi della [eliminazione](#Costo%20della%20eliminazione)

### Update della clustering key

In caso di aggiornamenti ai valori della chiave di un indice e necessario preservare l'ordinamento dei dati, 
>[!WARNING] DB2 ci prova ma ammette la presenza di indici **più o meno clustered**, rendendo necessarie operazioni di riorganizzazione quando il clustering risulta fortemente deteriorato

>[!TIP] In  un database oracle il clustering dei dati equivale ad usare un [b+tree](b+tree.md) per organizzare i dati e gli altri indici hanno come valori delle foglie dei RID logici (*i valori della primary key*) che aggiunge un livello di indirezione

[PREVIOUS](pages/group_by.md) [NEXT](pages/ottimizzazione_interrogazioni.md)
