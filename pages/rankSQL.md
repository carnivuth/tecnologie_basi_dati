---
id: rankSQL
tags: []
aliases: 
index: 24
---

# Introdurre il Concetto di rank nei DBMS

Una delle sfide nelle query [top k](top_k_queries.md) e quello  di introdurre nei DBMS il concetto di ranking, come first class citizen, un primo approccio al problema e stato fornito dal progetto RankDB definendo i seguenti concetti:

- splitting e interleaving del ranking degli oggetti
- relazione-rank e il principio di ranking
- rank-algebra pensata per le relazioni-rank

## Relazione rank 

Una relazione rank e definita come segue

>[!CITE] data una relazione $R$ e una funzione di scoring monotona $S(p_1,p_2,...,p_m)$  una relazione rank  $R_P$ si definisce come una relazione dove gli oggetti sono ordinati per valore decrescente di $S_P^+(t)$ dove $S_P^+(t)$ e definito come il massimo possibile score della tupla $t$ 

## Rank algebra

Pensata come estensione per supportare le [Relazioni rank](#Relazione%20rank), introduce l'operatore $\mu$ che applica una preferenza alla relazione rank $R_P$

grazie all'operatore $\mu$ e possibile l'interleaving con altri operatori $\sigma(\mu(R_P))$

![](Pasted%20image%2020250220160711.png)

[PREVIOUS](pages/top_k_join_queries.md) [NEXT](pages/skyline_queries.md)
