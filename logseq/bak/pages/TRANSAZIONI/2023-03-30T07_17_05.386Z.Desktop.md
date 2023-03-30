- operazioni logiche che portano il DB da uno stato consistente ad un altro
- rispettano le proprieta ACID
- #### ATOMICITY
  id:: 64130f84-57f3-4149-b83d-6d42ff423930
	- la transazione non può essere interrotta da altra operazioni
- #### CONCISTENCY
  id:: 64130fb2-5a41-4907-ac7e-523ad2167e28
	- il db alla fine della transazione deve trovarsi in uno stato consistente (i vincoli definiti sul db non devono essere violati)
- #### ISOLATION
  id:: 6421c858-c6de-4b98-a122-c18655fbdcf2
	- l'esecuzione di una transazione non deve interferire con l'esecuzione di un altra
- #### DURABILITY PERCISTANCE
  id:: 6421c858-9048-4a02-bc33-e399ec6df6da
	- le modifiche apportate da una transazione devono essere persistenti
	- necessario decidere il momento corretto in cui salvare le modifiche di una transazione
- ### COMPONENTI DBMS RESPONSABILI DELLE TRANSAZIONI
	- #### TRANSACTION MANAGER
		- responsabile della ((64130f84-57f3-4149-b83d-6d42ff423930))
	- #### LOGGING AND RECOVERING MANAGER
		- responsabile di ((64130fb2-5a41-4907-ac7e-523ad2167e28)) e ((64130f84-57f3-4149-b83d-6d42ff423930))
	- #### CONCURRENCY MANAGER
		- responsabile di ((6421c858-c6de-4b98-a122-c18655fbdcf2))
	- #### DDL COMPILER
		- responsabile della ((6421c858-9048-4a02-bc33-e399ec6df6da))