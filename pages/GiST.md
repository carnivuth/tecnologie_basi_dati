- struttura generalizzata per l'implementazione di indici
- opportunamente istanziata puo comportarsi da diverse tipologie di albero
- concetti base
	- una query è vista come un predicato
	- si accede a un determinato sottoalbero solo se è consistente con il predicato (vi è la possibilità che il sottoalbero contenga record che soddisfano il predicato)
	- l'albero di GiST prevede due tipologie di metodi
		- Key methods
			- specificati dall'implementazione dell'albero
			- #### CONSISTENT(entry,predicate)
			  id:: 6409e8ac-4b6c-4214-82fd-7b0d3f9c4113
				- determina se un sottoalbero è consistente con il predicato
				- questo consente di fare pruning dell'albero, rimuovendo le parti dell'albero che non soddisfano il predicato
				- approccio conservativo nella semantica
					- si afferma che è consistente anche se non si  è in grado di definirlo
			- #### UNION (P)
			  id:: 6411a3cd-6261-45f2-9e1b-2dcc2b47d0f0
				- crea un predicato che fa match con la serie di sottoalberi data in input
			- #### COMPRESS (E)
				- data una entry restituisce una entry con chiave compressa
			- #### DECOMPRESS (E')
				- restituisce la entry con chiave decompressa
			- #### PENALTY()
			  id:: 6411a50e-d55a-42f6-9b6c-bb04409ec1b9
				- TODO inserire definizione
			- #### PICSPLIT(P)
			  id:: 6411a5cf-2bce-4ccf-8495-baceba115bc4
				- dato l'insieme di entry di M +1 vengono restituiti due set di entry con cardinalità > fM
			-
		- Tree methods
			- metodi di gestione dell'albero
			- sono gia implementati nello standard GiST
			- ##### SEARCH
			  id:: 6411a775-8e1c-4189-bc54-7677bd32ed33
				- chiama ((6409e8ac-4b6c-4214-82fd-7b0d3f9c4113))
				- data la radice dell'albero e un predicato p si chiama consistent su i figli
					- se consistent è true allora avviene una chiamata ricorsiva
				- se il dominio è totalmente ordinato
					- search raggiunge la prima foglia consistente con il predicato e scorre a lista le foglie ordinate fintanto che non si raggiunge la prima foglia che non lo rispetta
			- ##### INSERT
			  id:: 6411a77b-c129-4414-8e60-dba8901df881
				- chiama ((6411a780-3d89-44a8-89d1-5f4943ce4c33)) ((6411a785-4067-483c-be2a-827e6c36e191)) ((6411a78a-3b0d-4735-b256-828a4c9fec90))
				- usato per inserire una nuova entry
				- usato anche per inserire entry orfane (quando viene eliminato un nodo e è necessario ripartire i suoi figli)
				-
			- ##### CHOOSESUBTREE
			  id:: 6411a780-3d89-44a8-89d1-5f4943ce4c33
				- chiama ((6411a50e-d55a-42f6-9b6c-bb04409ec1b9))
				- sceglie il sottoalbero  piu adatto per inserire una entry
				- se necessario viene chiamato ((6411a50e-d55a-42f6-9b6c-bb04409ec1b9)) per determinare il sottoalbero migliore e avviene una chiamata ricorsivam
			- ##### SPLIT
			  id:: 6411a785-4067-483c-be2a-827e6c36e191
				- chiama ((6411a5cf-2bce-4ccf-8495-baceba115bc4)) ((6411a3cd-6261-45f2-9e1b-2dcc2b47d0f0))
			- ##### ADJUSTKEYS
			  id:: 6411a78a-3b0d-4735-b256-828a4c9fec90
				- chiama ((6411a3cd-6261-45f2-9e1b-2dcc2b47d0f0))
			- ##### DELETE
				- chiama ((6411a775-8e1c-4189-bc54-7677bd32ed33)) ((6411a79a-8c56-4ddb-8386-486d6bc91a77))
			- ##### CONDENSETREE
			  id:: 6411a79a-8c56-4ddb-8386-486d6bc91a77
				- chiama ((6411a77b-c129-4414-8e60-dba8901df881)) ((6411a78a-3b0d-4735-b256-828a4c9fec90))
			-
		-
	-