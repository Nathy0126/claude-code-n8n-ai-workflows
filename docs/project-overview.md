# n8n Workflow Builder con Claude Code

## Panoramica

Questo progetto è uno spazio di lavoro dedicato alla creazione di workflow n8n di alta qualità con l'assistenza di Claude. Combinando Claude Code con il server MCP (Model Context Protocol) di n8n e le skill specializzate, puoi creare, modificare e gestire efficacemente automation complesse attraverso conversazioni in linguaggio naturale.

### Vantaggi

- **Sviluppo Rapido**: Costruisci workflow attraverso istruzioni conversazionali
- **Best Practice**: Sfrutta la conoscenza di Claude sui pattern e le best practice di n8n
- **Prevenzione Errori**: Ricevi feedback in tempo reale sul design del workflow
- **Documentazione**: Documenta automaticamente i tuoi workflow mentre li costruisci
- **Testing**: Testa e debugga i workflow in modo interattivo
- **Accesso a 1.084 Nodi**: Database completo di tutti i nodi n8n con documentazione
- **2.709 Template**: Esempi reali di workflow da cui imparare

### ⚠️ Avvertenza Importante

**Non usare mai l'AI direttamente sui workflow di produzione!** Lavora sempre su copie o in ambienti di test. Vedi la sezione [Sicurezza](#️-avvertenza-critica-di-sicurezza) per le best practice complete.

## Prerequisiti

Prima di iniziare, assicurati di avere:

1. **Istanza n8n**: Un'istanza n8n attiva (locale o cloud)
   - Self-hosted: `http://localhost:5678` (default)
   - n8n Cloud: `https://[tua-istanza].app.n8n.cloud`

2. **Accesso API n8n**:
   - API key dalla tua istanza n8n
   - Per generarla: Impostazioni → API n8n → Crea API Key

3. **Claude Code CLI**: Già installato se stai leggendo questo documento

## Istruzioni di Setup

### Passo 1: Configurare il Server MCP di n8n

Il server MCP di n8n ([n8n-mcp](https://github.com/czlonkowski/n8n-mcp)) permette a Claude di interagire programmaticamente con la tua istanza n8n.

#### Prerequisiti
- Node.js installato (per usare npx)
- Un'istanza n8n in esecuzione (opzionale per solo documentazione)

#### Opzioni di Configurazione

**Opzione A: Solo Documentazione (Senza Credenziali API)**

Se vuoi solo accedere alla documentazione dei nodi n8n senza gestire workflow:

1. **Crea o Aggiorna `.claude/settings.local.json`** nella root del progetto:

   ```json
   {
     "mcpServers": {
       "n8n-mcp": {
         "command": "npx",
         "args": ["n8n-mcp"],
         "env": {
           "MCP_MODE": "stdio",
           "LOG_LEVEL": "error",
           "DISABLE_CONSOLE_OUTPUT": "true"
         }
       }
     },
     "permissions": {
       "allow": [
         "Bash(dir:*)"
       ]
     }
   }
   ```

   Con questa configurazione avrai accesso a:
   - 1.084 nodi n8n (537 core + 547 community)
   - Documentazione completa dei nodi
   - 2.709 template di workflow
   - 2.646 configurazioni pre-estratte
   - Ricerca nodi community

**Opzione B: Gestione Completa Workflow (Con Credenziali API)**

Per creare, modificare ed eseguire workflow sulla tua istanza n8n:

1. **Genera API Key in n8n**:
   - Vai su Impostazioni → API n8n → Crea API Key
   - Copia la chiave generata

2. **Configura `.claude/settings.local.json`**:

   ```json
   {
     "mcpServers": {
       "n8n-mcp": {
         "command": "npx",
         "args": ["n8n-mcp"],
         "env": {
           "MCP_MODE": "stdio",
           "LOG_LEVEL": "error",
           "DISABLE_CONSOLE_OUTPUT": "true",
           "N8N_API_URL": "TUA_URL_ISTANZA_N8N",
           "N8N_API_KEY": "TUA_API_KEY_N8N"
         }
       }
     },
     "permissions": {
       "allow": [
         "Bash(dir:*)"
       ]
     }
   }
   ```

3. **Sostituisci i Placeholder**:
   - `TUA_URL_ISTANZA_N8N`: L'URL della tua istanza n8n
     - Self-hosted locale: `http://localhost:5678`
     - n8n Cloud: `https://[tua-istanza].app.n8n.cloud`
     - Self-hosted remoto: `https://tuo-dominio.com`
   - `TUA_API_KEY_N8N`: La tua API key generata da n8n

4. **Esempio Configurazione Completa**:

   ```json
   {
     "mcpServers": {
       "n8n-mcp": {
         "command": "npx",
         "args": ["n8n-mcp"],
         "env": {
           "MCP_MODE": "stdio",
           "LOG_LEVEL": "error",
           "DISABLE_CONSOLE_OUTPUT": "true",
           "N8N_API_URL": "http://localhost:5678",
           "N8N_API_KEY": "n8n_api_1a2b3c4d5e6f7g8h9i0j"
         }
       }
     },
     "permissions": {
       "allow": [
         "Bash(dir:*)"
       ]
     }
   }
   ```

#### Opzioni Avanzate

Puoi aggiungere queste variabili d'ambiente aggiuntive se necessario:

- `WEBHOOK_SECURITY_MODE`: Imposta a `"moderate"` per webhook localhost
- `N8N_MCP_TELEMETRY_DISABLED`: Imposta a `"true"` per disabilitare telemetria anonima
- `SQLJS_SAVE_INTERVAL_MS`: Intervallo di salvataggio database (in millisecondi)
- `LOG_LEVEL`: Livello di logging (`error`, `warn`, `info`, `debug`)

#### Metodi di Installazione Alternativi

Il metodo `npx n8n-mcp` scarica e esegue il server automaticamente. Se preferisci altri metodi:

**Docker:**

```json
{
  "mcpServers": {
    "n8n-mcp": {
      "command": "docker",
      "args": [
        "run", "-i", "--rm", "--init",
        "-e", "MCP_MODE=stdio",
        "-e", "LOG_LEVEL=error",
        "-e", "DISABLE_CONSOLE_OUTPUT=true",
        "-e", "N8N_API_URL=http://localhost:5678",
        "-e", "N8N_API_KEY=tua-api-key",
        "ghcr.io/czlonkowski/n8n-mcp:latest"
      ]
    }
  }
}
```

**Installazione Locale (Sviluppo):**

```bash
git clone https://github.com/czlonkowski/n8n-mcp.git
cd n8n-mcp
npm install
npm run build
npm run rebuild
npm start
```

#### Riavviare Claude Code

Dopo aver aggiornato la configurazione, riavvia Claude Code per applicare le modifiche:

```bash
# Esci dalla sessione corrente (Ctrl+C o Ctrl+D)
# Avvia una nuova sessione in questa directory
claude-code
```

### Passo 2: Installare le Skill n8n (Fortemente Consigliato)

Le skill ([n8n-skills](https://github.com/czlonkowski/n8n-skills)) sono 7 competenze specializzate che insegnano a Claude come costruire workflow n8n in modo corretto ed efficiente. Si attivano automaticamente quando necessario.

#### Le 7 Skill Disponibili

1. **n8n Expression Syntax** - Insegna la sintassi corretta `{{}}` e accesso alle variabili
2. **n8n MCP Tools Expert** - Guida all'uso efficace degli strumenti n8n-mcp (priorità massima)
3. **n8n Workflow Patterns** - Cinque pattern architetturali comprovati per automazioni
4. **n8n Validation Expert** - Interpreta e risolve errori di validazione
5. **n8n Node Configuration** - Guida alla configurazione nodi consapevole delle operazioni
6. **n8n Code JavaScript** - Scrittura JavaScript efficace nei nodi Code
7. **n8n Code Python** - Coding Python con consapevolezza delle limitazioni della piattaforma

#### Installazione

**Metodo Raccomandato (Claude Code):**

```bash
/plugin install czlonkowski/n8n-skills
```

**Metodi Alternativi:**

- **Via Marketplace**:
  ```bash
  /plugin marketplace add
  # Poi cerca e seleziona n8n-skills
  ```

- **Installazione Manuale**:
  ```bash
  git clone https://github.com/czlonkowski/n8n-skills.git
  cp -r n8n-skills/skills ~/.claude/skills/
  ```

#### Verifica Installazione

```bash
/plugin list
```

Dovresti vedere tutte le 7 skill n8n nella lista.

#### Come Funzionano le Skill

Le skill si attivano automaticamente quando rilevano query pertinenti:

- Domande sulle espressioni → attiva **Expression Syntax**
- Ricerca nodi → attiva **MCP Tools Expert**
- Errori di validazione → attiva **Validation Expert**
- Domande su pattern → attiva **Workflow Patterns**
- Configurazione nodi → attiva **Node Configuration**
- Codice JavaScript → attiva **Code JavaScript**
- Codice Python → attiva **Code Python**

#### Gotchas Critici Risolti

Le skill ti aiutano ad evitare errori comuni:

- ✅ I dati webhook si trovano sotto `$json.body` (non alla radice)
- ✅ Formato corretto ritorno Code node: `[{json: {...}}]`
- ✅ I nodi Python Code non hanno supporto librerie esterne (usa JavaScript nel 95% dei casi)
- ✅ 10+ pattern di Code node testati in produzione
- ✅ Catalogo completo errori con soluzioni

### Passo 3: Verifica del Setup

#### Se Hai Configurato Solo Documentazione

Prova a chiedere:

```
Cerca nodi n8n per inviare email
```

o

```
Mostrami alcuni template di workflow n8n per webhook
```

Claude dovrebbe essere in grado di accedere al database di nodi e template.

#### Se Hai Configurato con Credenziali API

Prova a chiedere:

```
Puoi controllare se riesci a connetterti alla mia istanza n8n e listare i miei workflow?
```

Se ha successo, vedrai una lista dei tuoi workflow esistenti (o una lista vuota se non ne hai ancora creati).

#### Troubleshooting Connessione

Se il server MCP non si carica:
1. Verifica che Node.js sia installato: `node --version` (richiede v18+)
2. Controlla la sintassi JSON in `.claude/settings.local.json`
3. Guarda i log nella console di Claude Code per errori MCP
4. Prova a eseguire manualmente: `npx n8n-mcp` per vedere eventuali errori

## Guida all'Utilizzo

### Creare Nuovi Workflow

Descrivi cosa vuoi costruire in linguaggio naturale. Sii specifico riguardo:

- **Trigger**: Cosa avvia il workflow?
- **Azioni**: Cosa dovrebbe accadere?
- **Trasformazioni dati**: Come devono essere processati i dati?
- **Gestione errori**: Cosa succede se qualcosa fallisce?

**Esempi di Richieste:**

```
Crea un workflow che:
1. Si attiva quando viene aggiunta una nuova riga a Google Sheets
2. Valida l'indirizzo email nella colonna B
3. Invia un'email di benvenuto tramite SendGrid
4. Registra il risultato in un database PostgreSQL
```

```
Costruisci un endpoint webhook che:
- Accetta richieste POST con dati JSON
- Estrae le informazioni del cliente
- Crea o aggiorna un record in Airtable
- Invia una notifica Slack al canale #sales
```

### Modificare Workflow Esistenti

Fai riferimento ai workflow per nome o ID:

```
Modifica il workflow "Onboarding Clienti" per aggiungere un ritardo di 2 ore prima di inviare l'email di benvenuto
```

```
Aggiungi gestione errori al workflow con ID 123 - se la chiamata API fallisce, inviami una notifica Slack
```

### Testare i Workflow

```
Testa il workflow webhook con questi dati di esempio: {"name": "Mario Rossi", "email": "mario@example.com"}
```

```
Esegui manualmente il workflow "Report Giornaliero" e mostrami i risultati
```

## Pattern di Workflow Comuni

### 1. Sincronizzazione Dati tra Servizi

```
Crea un workflow che sincronizza i record di Airtable con PostgreSQL ogni ora
- Fonte: Base Airtable "Clienti"
- Destinazione: Tabella PostgreSQL "customers"
- Abbina i record tramite campo email
- Aggiorna se esiste, inserisci se nuovo
```

### 2. Elaborazione Webhook

```
Costruisci un webhook che elabora gli eventi di pagamento Stripe:
- Valida la firma del webhook
- Estrae i dettagli del pagamento
- Aggiorna il record del cliente nel database
- Invia ricevuta via email tramite SendGrid
- Registra nel canale Slack #pagamenti
```

### 3. Elaborazione Dati Schedulata

```
Crea un workflow giornaliero che:
- Viene eseguito ogni giorno alle 9:00
- Recupera dati da REST API
- Trasforma il JSON per adattarlo al nostro schema
- Carica su Google Sheets
- Invia email di riepilogo al team
```

### 4. Pipeline da Form a CRM

```
Costruisci un workflow che:
- Riceve invii di form tramite webhook
- Valida i campi obbligatori
- Controlla email duplicate nel CRM
- Crea nuovo contatto in HubSpot
- Attiva sequenza email di benvenuto
- Notifica il team vendite se lead score > 75
```

## Best Practice

### Design dei Workflow

1. **Singola Responsabilità**: Ogni workflow dovrebbe gestire un'attività primaria
2. **Gestione Errori**: Aggiungi sempre nodi di gestione errori per operazioni critiche
3. **Logging**: Registra eventi importanti per debugging e monitoraggio
4. **Testing**: Testa i workflow con dati di esempio prima di attivarli
5. **Documentazione**: Usa le note dei workflow per documentare la logica complessa

### Ottimizzazione delle Performance

1. **Operazioni Batch**: Processa più elementi insieme quando possibile
2. **Logica Condizionale**: Usa nodi IF per saltare operazioni non necessarie
3. **Caching**: Memorizza dati acceduti frequentemente per ridurre chiamate API
4. **Rate Limiting**: Rispetta i limiti di rate delle API con nodi di ritardo
5. **Trasformazione Dati**: Processa i dati efficientemente con nodi nativi n8n

### Considerazioni sulla Sicurezza

1. **Credenziali**: Memorizza API key e password nelle credenziali n8n
2. **Validazione**: Valida e sanitizza gli input dei webhook
3. **Autenticazione**: Proteggi gli endpoint webhook con autenticazione
4. **Dati Sensibili**: Fai attenzione con i dati personali (PII)
5. **Controllo Accessi**: Usa i controlli di accesso di n8n per workflow di team

## Strumenti MCP Disponibili

Il server n8n-mcp fornisce accesso a un'ampia gamma di strumenti e risorse:

### Risorse Documentazione (Disponibili Sempre)

Anche senza credenziali API, hai accesso a:

- **1.084 nodi n8n** (537 core + 547 community) con documentazione completa
- **87% copertura documentazione nodi** con descrizioni dettagliate
- **99% copertura proprietà nodi** con tutti i parametri
- **63,6% copertura operazioni nodi** con esempi d'uso
- **2.646 configurazioni pre-estratte** da template reali
- **2.709 template di workflow** con metadata completa
- **265 varianti di tool AI-capable** con documentazione completa
- **Ricerca nodi community** con filtro per fonte

### Strumenti Gestione Workflow (Con Credenziali API)

Quando configuri `N8N_API_URL` e `N8N_API_KEY`, ottieni anche:

- **list_workflows**: Ottieni tutti i workflow dalla tua istanza n8n
- **get_workflow**: Recupera i dettagli di un workflow specifico
- **create_workflow**: Crea nuovi workflow
- **update_workflow**: Modifica workflow esistenti
- **execute_workflow**: Attiva l'esecuzione di un workflow
- **get_execution**: Controlla lo stato e i risultati dell'esecuzione
- **list_credentials**: Visualizza le credenziali disponibili (solo nomi, non valori)

Claude userà automaticamente questi strumenti quando richiedi operazioni sui workflow.

### ⚠️ AVVERTENZA CRITICA DI SICUREZZA

**NON editare MAI i tuoi workflow di produzione direttamente con l'AI!**

Segui sempre queste pratiche di sicurezza:

1. ✅ **Fai una copia** del workflow prima di usare strumenti AI
2. ✅ **Testa in ambiente di sviluppo** prima di passare a produzione
3. ✅ **Esporta backup** dei workflow importanti regolarmente
4. ✅ **Valida i cambiamenti** manualmente prima del deploy in produzione
5. ✅ **Usa un'istanza n8n di test** separata per sperimentare con l'AI

Il server n8n-mcp invia telemetria anonima di utilizzo per migliorare il servizio. Puoi disabilitarla aggiungendo `N8N_MCP_TELEMETRY_DISABLED: "true"` alle variabili d'ambiente.

## Esempi di Interazioni

### Creare un Workflow Semplice

**Tu:**
```
Crea un workflow che mi invia un messaggio Slack giornaliero alle 9:00 con la data di oggi
```

**Claude:**
1. Creerà un nuovo workflow con un Schedule Trigger (cron: 0 9 * * *)
2. Aggiungerà un nodo Date & Time per formattare la data corrente
3. Aggiungerà un nodo Slack configurato per inviare un messaggio
4. Collegherà i nodi appropriatamente
5. Fornirà l'ID del workflow e lo stato di attivazione

### Debugging di un Workflow

**Tu:**
```
Il mio workflow "Sincronizzazione Clienti" sta fallendo. Puoi controllare cosa c'è che non va?
```

**Claude:**
1. Recupererà i dettagli del workflow
2. Controllerà le esecuzioni recenti
3. Identificherà il nodo che fallisce
4. Analizzerà i messaggi di errore
5. Suggerirà correzioni con modifiche di configurazione specifiche

### Costruire Workflow Complessi

**Tu:**
```
Costruisci un workflow di elaborazione ordini e-commerce:
- Webhook riceve dati ordine
- Valida pagamento con Stripe
- Crea ordine in Shopify
- Invia email di conferma
- Aggiungi cliente alla lista Mailchimp
- Registra su Google Sheets
- Notifica team su Slack
```

**Claude:**
1. Farà domande di chiarimento sulla struttura dati e credenziali
2. Creerà il workflow passo dopo passo
3. Configurerà ogni nodo con le impostazioni appropriate
4. Aggiungerà gestione errori nei punti critici
5. Testerà con dati di esempio
6. Fornirà documentazione della logica del workflow

## Risoluzione Problemi

### Problemi di Connessione

**Problema**: "Non riesco a connettermi all'istanza n8n"

**Soluzioni**:
1. Verifica che n8n sia in esecuzione: Visita l'URL di n8n nel browser
2. Controlla che l'API key sia corretta in `.claude/settings.local.json`
3. Assicurati che l'URL base includa il protocollo (`http://` o `https://`)
4. Verifica che il firewall permetta connessioni alla porta n8n
5. Riavvia Claude Code dopo le modifiche alla configurazione

### Errori di Autenticazione

**Problema**: "Non autorizzato" o "API key non valida"

**Soluzioni**:
1. Genera una nuova API key in n8n: Impostazioni → API n8n → Crea API Key
2. Aggiorna `.claude/settings.local.json` con la nuova key
3. Assicurati che l'API key abbia i permessi necessari
4. Controlla spazi extra o virgolette nella configurazione

### Fallimenti nell'Esecuzione dei Workflow

**Problema**: "Esecuzione workflow fallita"

**Soluzioni**:
1. Chiedi a Claude di controllare le esecuzioni recenti: `Mostrami i dettagli dell'errore dell'ultima esecuzione fallita`
2. Rivedi le configurazioni dei nodi per credenziali mancanti
3. Controlla i limiti di rate e le quote delle API
4. Verifica che il formato dati corrisponda allo schema atteso
5. Aggiungi nodi di gestione errori per catturare i fallimenti

### Server MCP Non Caricato

**Problema**: Strumenti MCP n8n non disponibili

**Soluzioni**:
1. Assicurati che `@n8n/mcp-server` sia accessibile via npx
2. Controlla che Node.js sia installato e aggiornato (v18+)
3. Verifica che la sintassi di `.claude/settings.local.json` sia JSON valido
4. Rivedi la console di Claude Code per messaggi di errore del server MCP
5. Prova l'installazione manuale: `npm install -g @n8n/mcp-server`

## Suggerimenti per Costruire Workflow Efficaci

### 1. Inizia Semplice, Itera

Inizia con un workflow base e aggiungi complessità gradualmente. Testa ogni aggiunta prima di passare alla successiva.

```
Prima: Crea webhook base → notifica Slack
Poi: Aggiungi validazione dati
Infine: Aggiungi logging database e gestione errori
```

### 2. Usa Nomi Descrittivi

Dai nomi chiari ai tuoi workflow e nodi:

- ✅ "Sincronizzazione Pagamenti Stripe a CRM"
- ❌ "Workflow 1"

- ✅ "Valida Email Cliente"
- ❌ "Nodo IF"

### 3. Fornisci Contesto

Quando chiedi a Claude di modificare workflow, fornisci contesto:

```
Nel mio workflow "Elaborazione Ordini", il nodo Stripe a volte va in timeout.
Puoi aggiungere un meccanismo di retry con 3 tentativi e backoff esponenziale?
```

### 4. Testa con Dati Reali

Quando possibile, testa i workflow con dati realistici:

```
Testa il workflow con questo record cliente reale dal nostro database:
[incolla dati di esempio]
```

### 5. Chiedi Spiegazioni

Non esitare a chiedere a Claude di spiegare la logica del workflow:

```
Puoi spiegarmi come fluiscono i dati attraverso il workflow "Onboarding Clienti"?
```

## Prossimi Passi

1. **Verifica il setup** chiedendo a Claude di listare i tuoi workflow
2. **Crea il tuo primo workflow** usando uno dei pattern di esempio sopra
3. **Esplora le integrazioni n8n** - chiedi a Claude sui nodi disponibili
4. **Costruisci incrementalmente** - inizia semplice e aggiungi funzionalità
5. **Documenta mentre procedi** - chiedi a Claude di spiegare la logica complessa

## Risorse Aggiuntive

- [Documentazione n8n](https://docs.n8n.io)
- [Forum Community n8n](https://community.n8n.io)
- [Template Workflow n8n](https://n8n.io/workflows)
- [Documentazione Claude Code](https://docs.anthropic.com/claude/docs)
- [Documentazione MCP Server](https://modelcontextprotocol.io)

---

**Pronto per iniziare?** Chiedi a Claude di aiutarti a creare il tuo primo workflow!
