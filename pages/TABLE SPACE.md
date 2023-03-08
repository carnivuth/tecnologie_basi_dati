- DONE aggiungere definizione
  :LOGBOOK:
  CLOCK: [2023-03-01 Wed 11:45:51]--[2023-03-01 Wed 11:45:52] =>  00:00:01
  :END:
- il tablespace è uno spazio logico che puo contenere 1 o piu tabelle
- possibile specificare parametri
- sono minimo 3
	- USER TABLES
	- CATALOGS (metainformazioni per il DB)
	- TEMPORARY TABLES (necessari per lo swap delle pagine tra memoria centrale e disco)
- [[tipologie di tablespace]]
- il tablespace è diviso in [[CONTAINER]]
- ORGANIZZAZIONE DEI FILE
	- per semplicità si considerano
		- record di lunghezza fissa
		- costo delle operazioni come numero di I/O operation condotte assumendo che il caricamento di una pagina sia un unica I/O operation
		- STIMA DEL COSTO DELLE OPERAZIONI
			- le operazioni interessanti sono
				- ricerca per chiave
				  id:: 30b627f4-65be-4a0f-896b-03e36d69e9e1
				- ricerca per range
				  id:: 7b6cdc6d-baf3-4a1a-83f7-7720b9276cf4
				- inserimento di un record
				- eliminazione di un record
				  id:: f24aed1c-ffca-40d0-9921-2370d5a1642d
				- aggiornamento di un attributo in un record
				  id:: f4e40e86-1149-4a56-9d40-db088c43e031
			-
	- HEAP FILE
	  id:: 63ff4567-cdb6-48fa-a823-d6bb8bf62a9c
		- i dati vengono inseriti senza particolare ordine
	- SEQUENTIAL FILE
	  id:: 63ff461e-09e6-4ad9-8172-b9461cfe0adc
	- all'interno dei catalog vengono memorizzate
		- tabella
		- numero di pagine della tabella
		- id della tabella
		- nome dei campi