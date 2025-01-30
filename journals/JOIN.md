- supponiamo di avere query del tipo
- ![image.png](../assets/image_1681897443350_0.png)
- eseguire il prodotto cartesiano per poi applicare il predicato è **molto inefficente**
- molte possibili varianti
- ## NESTED LOOP JOIN
	- si confronta ogni record di un input con ogni  record dell'altro input
	- ![image.png](../assets/image_1681897585440_0.png)
	- #### COSTO
		- `P(R) + N(R) * P(S) = P(R) + TP(R)*P(R)*P(S)`
		- è conveniente avere come relazione esterna quella con più tuple ma il guadagno sulle prestazioni non è significativo
	- ### PROPRIETÀ
		- l'algoritmo **preserva l'ordine della relazione esterna**
		- può risultare utile per altre operazioni da svolgere nella query
		- ![image.png](../assets/image_1681898140692_0.png)
	- ### VERSIONE PAGINATA
		- ![image.png](../assets/image_1681898218951_0.png)
		- si perde il vantaggio dell'ordinamento ma si riduce di molto il numero di I/O
	- ### SFRUTTANDO IL BUFFER
		- se si avesse un maggior numero di pagine del buffer si possono sfruttare per migliorare le prestazioni
		- si usano B-2 pagine per la relazione esterna
		- 1 per la relazione interna
		- 1 per la pagina di output
		- ![image.png](../assets/image_1681898408366_0.png)
		- ci puo eseere un caso in cui la relazione interna a il maggior numero di buffer ovvero quando si **puo contentere interamente in memoria**
	- ### HASHING PER EFFETTUARE MATCHING
	  id:: 643fc349-19b4-425a-83d5-ff561d5f78f2
		- si può usare una funzione hash su i record della relazione esterna e  su quella esterna
		- ![image.png](../assets/image_1681898782114_0.png)
	- ### INDEX NESTED LOOP JOIN
		- è possibile sfruttare un indice per ridurre il costo delle operazioni di accesso per la relazione interna
		- ![image.png](../assets/image_1681899209967_0.png)
		- ![image.png](../assets/image_1681899225713_0.png)
		- #### COSTO
			- `P(R) + N(R) * (costo indice + dati)`
	- ### JOIN E PUSH DOWN
		- si possono sfruttare operazioni di push down di selezioni per alleggerire l'esecuzione di query di ricerca
		- ```
		  SELECT * FROM SOMELIER S RECENSIONI R
		  WHERE R.SID=S.SID
		  AND R.RIVISTA= "sapore di vino"
		  ```
		- eseguire il push down del filtro può alleggerire di molto l'esecuzione della query
- ## MERGE-SCAN JOIN
  id:: 643fc6bb-0c03-4a7e-9c4e-891a02f16016
	- si basa sul fatto che entrambe le relazioni siano **ordinati sull'attributo di join**
	- usato solo per equi-join
- ## HASH JOIN
	- il vantaggio del ((643fc6bb-0c03-4a7e-9c4e-891a02f16016)) è che viene ridotto il numero di confronti fra i record delle relazioni
	- un altro modo per ottenere questo effetto è quello di usare una funzione hash per partizionare
	- schema identico a quello di una proiezione basata su hasing
	- la fase di matching puo essere utilizzata con un altra funzione hash con lo stesso schema di ((643fc349-19b4-425a-83d5-ff561d5f78f2))
- ## OUTER DEL JOIN
	- ![image.png](../assets/image_1681902524414_0.png)
	- produce in output anche le tuple di una o l'altra relazione che non hanno match (*dandling*)
	- ![image.png](../assets/image_1681902732283_0.png)
	  id:: 643fcc66-10dd-4234-947c-65fb81d6f825

 [NEXT](pages/struttura_database.md)
