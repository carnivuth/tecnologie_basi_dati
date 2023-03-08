- indici hash
	- non ottimali per ricerca con range
- indici ordinati
	- strutturati ad albero binario bilanciato
	- ottimi per ricerche range
- INDICE CLUSTERED
	- costruito sullo stesso attributo su cui è ordinato il file
	- è possibile un solo indice clustered per file
- INDICE PRIMARIO
	- se costruito su un attributo unique
- INDICE SECONDARIO
	- costruito su un attributo non unique
	- strutturato a insieme di liste
	-
- INDICE DENSO
	- numero di puntatori pari a numero di record
	- tutti gli elementi sono indicizzati
- INDICE SPARSO
	- non tutti  i record sono indicizzati
	- possibile solo per indici clustered(di solito indice per pagina)
- INDICE MULTILIVELLO
	- struttura dati fatta da indici che indici che indicizzano altri indici
		- essendo che gli indici sono ordinati gli indici di questo tipo sono sparsi
		- creando cosi una struttura ad albero
		- ottimizzazione del caricamento degli indici in memoria