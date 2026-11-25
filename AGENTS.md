# Human 4 Human — istruzioni condivise

> File iniziale del repository agentico. Completare i dettagli funzionali e architetturali usando RAD, SDD e modelli H4H prima di avviare task di implementazione.

## Contesto
Il progetto è Human 4 Human (H4H). La specifica funzionale e le decisioni architetturali sono quelle documentate nel repository: gli agenti non devono sostituirle con assunzioni proprie.

## Stack
- Java
- Spring Boot
- Thymeleaf
- Spring Data JPA
- Maven

Le versioni effettive devono essere quelle dichiarate nel `pom.xml` e nella documentazione di progetto. Non introdurre dipendenze o versioni non approvate.

## Comandi
- Build e verifica: `mvn -B verify`
- Eseguire test mirati quando opportuno, senza dichiarare superati test non eseguiti.

## Regole
### Sempre
- Leggere `AGENTS.md`, l'issue e solo i documenti indicati nella sezione **Specifica** dell'issue.
- Usare i nomi, i tipi, le firme, i flussi e i vincoli definiti nei documenti H4H.
- Rispettare lo scope e i criteri di accettazione dell'issue.
- Segnalare nel commento o nella PR requisiti mancanti, contraddizioni e assunzioni.
- Lasciare traccia delle decisioni e dei risultati nell'issue o nella PR GitHub.

### Chiedi prima
- Quando la specifica è incompleta o contraddittoria.
- Quando serve modificare modelli, requisiti, schema dati o architettura.
- Quando occorre ampliare lo scope o introdurre una dipendenza non già prevista.

### Mai
- Inventare requisiti, classi, endpoint, schermate, regole di dominio o dipendenze.
- Modificare i documenti di specifica senza approvazione.
- Inserire segreti o credenziali nel repository o nei log.
- Effettuare merge o approvare autonomamente una pull request.

## Quando un task è finito
- Implementazione: piano approvato, modifiche nello scope, `mvn -q verify` eseguito, PR in bozza aperta con `Closes #N`.
- Test: un test per ogni frame indicato, `mvn -q verify` eseguito, commit e push sul branch della PR; gli eventuali frame falliti sono commentati senza correggere il codice applicativo.
- Revisione: commento con le differenze rispetto ai modelli, senza modifiche ai file.
- Il merge resta una decisione umana, subordinata alle regole del repository.

## Documenti di riferimento
Usare i percorsi effettivi del repository H4H indicati nell'issue. Non assumere che i documenti di esempio del professore (`PrenotaAula`) siano specifiche di H4H.
