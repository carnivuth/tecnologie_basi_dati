- il filesistem offre servizi facendo assunzioni sull'utilizzo della memoria da parte delle applicazioni che ne fanno uso
- queste assunzioni non valgono per un DBMS
- per un DBMS è necessario sfruttare le relazioni fra le informazioni in fase di memorizzazione delle stesse per rendere le query di estrazione piu veloci
	- esempi
		- se due relazioni sono collegate da un JOIN salvare in container contigui è una buona idea
		- se in una relazione sono presenti dati BLOB salvarli in un altro container è una buona idea
- **IL FILESYSTEM NON È A CONOSCENZA DI QUESTE NECESSITÀ DEL DBMS**