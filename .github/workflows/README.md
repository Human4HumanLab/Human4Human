# Human 4 Human — workflow con OpenRouter

Questa cartella riproduce il flusso descritto nel PDF del corso:
- `piano.yml`: issue `fase:piano`, solo commento con il piano;
- `implementa.yml`: issue `fase:implementazione`, implementazione e PR draft;
- `test.yml`: PR `fase:test`, solo test e commit/push sul branch;
- `revisione.yml`: PR `ready_for_review`, revisione read-only e commento;
- `agente.yml`: commenti `@claude` da OWNER/MEMBER/COLLABORATOR;
- `ci.yml`: build/test Maven, senza agente e senza secret.

## Unica separazione funzionale aggiunta: scelta dei modelli

I modelli sono centralizzati in `.claude/models.json`. Ogni workflow legge la chiave del proprio ruolo e passa il valore a Claude Code con `--model`. Modificare quel JSON cambia il modello senza modificare il workflow.

Chiavi: `planner`, `implementer`, `tester`, `reviewer`, `general`.

Sostituire i valori segnaposto con gli ID modello esatti pubblicati su OpenRouter. Per Claude Code, OpenRouter dichiara compatibilità garantita con provider Anthropic first-party; selezionarlo come provider prioritario. Vedi https://openrouter.ai/docs/guides/coding-agents/claude-code-integration.

## OpenRouter

Creare il secret GitHub `OPENROUTER_API_KEY`. Nei job Claude:
- `anthropic_api_key` riceve il secret per superare il controllo di avvio dell'action;
- `ANTHROPIC_BASE_URL` punta a `https://openrouter.ai/api`;
- `ANTHROPIC_AUTH_TOKEN` usa la stessa chiave come Bearer token.

La CI non usa chiavi né agenti.

## Configurazione iniziale GitHub

Creare le label:
```bash
gh label create task-agente --color 0E8A16 --description "Task svolto con agenti"
gh label create fase:piano --color FBCA04 --description "Avvia l'agente pianificatore"
gh label create fase:implementazione --color 1D76DB --description "Piano approvato: avvia l'implementazione"
gh label create fase:test --color 5319E7 --description "Avvia l'agente tester sulla PR"
```

Impostare il secret:
```bash
gh secret set OPENROUTER_API_KEY
```

In Settings > Actions > General:
- Workflow permissions: Read repository contents and packages;
- abilitare Allow GitHub Actions to create and approve pull requests.

## Stack H4H e Java

`AGENTS.md` registra lo stack dichiarato per H4H (Java, Spring Boot, Thymeleaf, Spring Data JPA, Maven). I workflow mantengono Java 17 come nel materiale del professore; se la versione approvata nel `pom.xml` sarà diversa, allineare `setup-java` e CI in un'unica modifica esplicita.

## Differenze tecniche indispensabili rispetto al PDF

1. Il secret si chiama `OPENROUTER_API_KEY` al posto di `ANTHROPIC_API_KEY`.
2. I job Claude impostano l'endpoint OpenRouter e il token Bearer come richiesto dalla guida OpenRouter per GitHub Action.
3. Ogni workflow Claude ha un piccolo step `jq` che legge il modello dal file `.claude/models.json`; trigger, prompt, permessi, timeout, limiti, strumenti e azioni restano quelli del tutorial.
4. Non è stata aggiunta integrazione YouTrack.

Il PDF usa l'app GitHub Claude per l'identità `claude[bot]`; la chiave OpenRouter sostituisce solo la credenziale di accesso al modello e non installa automaticamente la GitHub App. Seguire il passo di installazione della GitHub App se si vuole mantenere quell'identità e il relativo flusso di autenticazione. Non confondere la chiave API con il token GitHub `github.token`.

## Da completare prima dell'attivazione

- Sostituire gli username di esempio in `CODEOWNERS`.
- Inserire gli ID modello reali in `.claude/models.json`.
- Allineare Java 17 alla versione effettiva del progetto.
- Popolare RAD, SDD, modelli e test frame H4H.
- Configurare ruleset `main` con required approval e status check `build`.
