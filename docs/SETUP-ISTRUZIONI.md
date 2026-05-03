# Istruzioni Setup: Gmail Auto-Categorizzazione

## 📋 Checklist Rapida

Prima di iniziare, avrai bisogno di:
- [ ] Istanza n8n attiva (locale o cloud)
- [ ] Account Gmail con accesso alle impostazioni
- [ ] API Key OpenAI
- [ ] 10-15 minuti di tempo

---

## Passo 1: Creazione Label Gmail (5 minuti)

### 1.1 Accedi a Gmail

Vai su [Gmail](https://mail.google.com) e accedi al tuo account.

### 1.2 Crea le 3 Etichette

1. Click sull'icona **⚙️ Impostazioni** in alto a destra
2. Seleziona **"Visualizza tutte le impostazioni"**
3. Vai alla tab **"Etichette"**
4. Scorri fino alla sezione **"Etichette"**
5. Click su **"Crea nuova etichetta"**

Crea queste 3 etichette (rispetta maiuscole/minuscole!):

#### Etichetta 1: Alta Priorità
- Nome: `Alta Priorità`
- Colore consigliato: **Rosso** 🔴
- Descrizione: Email urgenti che richiedono risposta immediata

#### Etichetta 2: Finanza e Fatturazione
- Nome: `Finanza e Fatturazione`
- Colore consigliato: **Verde** 🟢
- Descrizione: Fatture, pagamenti, documenti finanziari

#### Etichetta 3: Promozione
- Nome: `Promozione`
- Colore consigliato: **Arancione** 🟠
- Descrizione: Marketing, newsletter, offerte

### 1.3 Verifica Creazione

Dopo aver creato le label:
1. Vai alla tua inbox Gmail
2. Nella barra laterale sinistra, verifica che le 3 label appaiano
3. **Annota i nomi ESATTI** (case-sensitive!)

✅ **Checkpoint**: Dovresti vedere le 3 label nella sidebar di Gmail

---

## Passo 2: Setup Credenziali n8n (10 minuti)

### 2.1 Configurare Gmail OAuth2 in n8n

1. **Apri n8n** (nel browser)
   - Locale: `http://localhost:5678`
   - Cloud: `https://[tua-istanza].app.n8n.cloud`

2. **Vai a Credentials**
   - Click sull'icona utente in basso a sinistra
   - Seleziona **"Credentials"**

3. **Crea credenziali Gmail**
   - Click **"Add Credential"**
   - Cerca e seleziona **"Gmail OAuth2"**
   - Click **"Connect my account"**
   - Segui il flusso OAuth di Google:
     - Seleziona il tuo account Gmail
     - Autorizza n8n ad accedere a Gmail
     - **IMPORTANTE**: Assicurati di dare questi permessi:
       - ✅ Lettura email (`gmail.readonly`)
       - ✅ Modifica label (`gmail.modify`)

4. **Salva credenziali**
   - Dai un nome descrittivo: es. "Gmail Personal"
   - Click **"Save"**
   - **Annota l'ID delle credenziali** (lo troverai nell'URL o nei dettagli)

### 2.2 Configurare OpenAI API Key in n8n

1. **Ottieni API Key da OpenAI**
   - Vai su [platform.openai.com/api-keys](https://platform.openai.com/api-keys)
   - Fai login con il tuo account OpenAI
   - Click **"Create new secret key"**
   - Dai un nome: es. "n8n Gmail Categorization"
   - **COPIA LA CHIAVE** (la vedrai solo una volta!)

2. **Aggiungi credenziali in n8n**
   - In n8n, vai a **Credentials** → **"Add Credential"**
   - Cerca e seleziona **"OpenAI API"**
   - Incolla la tua API Key nel campo **"API Key"**
   - Dai un nome: es. "OpenAI Personal"
   - Click **"Save"**

✅ **Checkpoint**: Dovresti avere 2 credenziali salvate in n8n (Gmail + OpenAI)

---

## Passo 3: Importare Workflow in n8n (3 minuti)

### 3.1 Importare il File JSON

1. **Apri n8n** nel browser
2. Vai alla sezione **"Workflows"** (icona in alto a sinistra)
3. Click su **"Add Workflow"** → **"Import from File"**
4. Seleziona il file: `gmail-categorization-workflow.json`
5. Il workflow verrà caricato con tutti i nodi configurati

### 3.2 Assegnare Credenziali ai Nodi

Il workflow importato avrà placeholder per le credenziali. Devi assegnarle:

#### Nodo: "Gmail Trigger"
1. Click sul nodo
2. Nella sezione **"Credential to connect with"**
3. Seleziona le tue credenziali Gmail OAuth2
4. Click fuori per salvare

#### Nodo: "Get Message Content"
1. Click sul nodo
2. Seleziona le stesse credenziali Gmail OAuth2
3. Click fuori per salvare

#### Nodo: "Get All Gmail Labels"
1. Click sul nodo
2. Seleziona le stesse credenziali Gmail OAuth2
3. Click fuori per salvare

#### Nodo: "Add Label to Message"
1. Click sul nodo
2. Seleziona le stesse credenziali Gmail OAuth2
3. Click fuori per salvare

#### Nodo: "OpenAI GPT-4o-mini"
1. Click sul nodo
2. Nella sezione **"Credential to connect with"**
3. Seleziona le tue credenziali OpenAI API
4. Click fuori per salvare

### 3.3 Salvare il Workflow

1. Click su **"Save"** in alto a destra
2. Dai un nome al workflow: es. "Gmail Auto-Categorizzazione"
3. Il workflow è ora pronto!

✅ **Checkpoint**: Workflow importato, credenziali assegnate, salvato

---

## Passo 4: Testing del Workflow (15 minuti)

### 4.1 Preparare Email di Test

**IMPORTANTE**: NON attivare ancora il workflow!

Invia 9 email di test al tuo account Gmail da un altro indirizzo (o usa un servizio come [Mailtrap](https://mailtrap.io) per test):

#### Test Set 1: Alta Priorità (3 email)

**Email 1:**
- **Subject**: URGENTE: Richiesta approvazione contratto
- **Body**: Buongiorno, ho bisogno della tua approvazione sul contratto allegato entro venerdì. È molto urgente. Grazie!

**Email 2:**
- **Subject**: Domanda importante sul progetto XYZ
- **Body**: Ciao, puoi per favore chiarirmi questa questione sul progetto? Il cliente sta aspettando una risposta oggi.

**Email 3:**
- **Subject**: Action Item: Completa il form entro domani
- **Body**: Ti ricordo che devi completare il form di feedback entro domani mattina. È una deadline critica.

#### Test Set 2: Finanza e Fatturazione (3 email)

**Email 4:**
- **Subject**: Fattura #FT-2024-001 - Pagamento in Scadenza
- **Body**: Gentile cliente, la informiamo che la fattura allegata è in scadenza. Importo: €1,500.00. Scadenza: 31/01/2024.

**Email 5:**
- **Subject**: Conferma pagamento ricevuto
- **Body**: Il tuo pagamento di €250.00 è stato ricevuto correttamente. Grazie per la tua puntualità.

**Email 6:**
- **Subject**: Estratto conto bancario mensile disponibile
- **Body**: Il tuo estratto conto di gennaio 2024 è ora disponibile. Accedi al tuo account per visualizzarlo.

#### Test Set 3: Promozione (3 email)

**Email 7:**
- **Subject**: Newsletter mensile - Le nostre novità di prodotto
- **Body**: Ciao! Ecco le ultime novità del nostro catalogo. Scopri i nuovi prodotti lanciati questo mese!

**Email 8:**
- **Subject**: Offerta Speciale: 50% di sconto su tutti i corsi
- **Body**: Non perdere questa opportunità! Solo per questa settimana, tutti i nostri corsi online sono scontati del 50%. Approfitta ora!

**Email 9:**
- **Subject**: Webinar gratuito - Come migliorare la tua produttività
- **Body**: Ti invitiamo al nostro webinar gratuito giovedì prossimo. Registrati ora per riservare il tuo posto!

### 4.2 Eseguire il Test

1. **Verifica che le 9 email siano in Inbox e UNREAD**
2. In n8n, **NON attivare il workflow**
3. Click su **"Execute Workflow"** (bottone play in basso)
4. Il workflow eseguirà manualmente un ciclo
5. Osserva l'esecuzione:
   - Ogni nodo diventerà verde quando completato
   - Se un nodo diventa rosso, c'è un errore

### 4.3 Verificare i Risultati

1. **Torna su Gmail**
2. Aggiorna la pagina
3. **Controlla che ogni email abbia ricevuto una label**:

   ✅ Email 1-3 dovrebbero avere: **Alta Priorità**
   ✅ Email 4-6 dovrebbero avere: **Finanza e Fatturazione**
   ✅ Email 7-9 dovrebbero avere: **Promozione**

4. **Controlla il log di esecuzione in n8n**:
   - Click su **"Executions"** nella sidebar
   - Verifica l'ultima esecuzione
   - Tutti i nodi dovrebbero essere ✅ verdi

### 4.4 Criteri di Successo

- [ ] 9/9 email hanno ricevuto una label
- [ ] Almeno 8/9 (89%+) hanno la label CORRETTA
- [ ] Nessun errore nel log di esecuzione n8n
- [ ] Email rimaste in Inbox (non archiviate)
- [ ] Tempo esecuzione < 10 secondi per email

**Se il test ha successo** → Procedi al Passo 5
**Se il test fallisce** → Vedi sezione Troubleshooting sotto

---

## Passo 5: Attivazione Produzione (2 minuti)

### 5.1 Attivare il Workflow

1. In n8n, apri il workflow
2. Toggle **"Active"** in alto a destra (da OFF a ON)
3. Il workflow inizierà a monitorare Gmail ogni 5 minuti

### 5.2 Monitoraggio Prima Settimana

**Giorni 1-3: Monitoraggio Intensivo**
- Controlla manualmente 10 email random/giorno
- Verifica che le label siano corrette
- Annota eventuali errori di categorizzazione

**Giorni 4-7: Monitoraggio Ridotto**
- Controlla 5 email random/giorno
- Se accuratezza ≥ 90%, tutto ok!

### 5.3 Metriche da Tracciare

Apri un foglio Excel/Google Sheets e traccia:

| Data | Email Processate | Corrette | Errate | Accuratezza % | Note |
|------|------------------|----------|--------|---------------|------|
| 01/02| 25               | 23       | 2      | 92%           | Ok   |
| 02/02| ...              | ...      | ...    | ...           | ...  |

**Target**: Accuratezza ≥ 85% costante

✅ **Checkpoint**: Workflow attivo e funzionante in produzione!

---

## 🎉 Completato!

Il tuo workflow è ora attivo e categorizza automaticamente le email ogni 5 minuti!

### Cosa Succede Ora

1. Ogni 5 minuti, n8n controlla nuove email
2. Per ogni email unread in INBOX:
   - ChatGPT analizza subject, mittente, contenuto
   - Assegna UNA categoria
   - Applica label Gmail corrispondente
3. Email rimane in Inbox con la label applicata
4. Puoi filtrare per label nella sidebar Gmail

### Prossimi Passi Consigliati

- **Settimana 1**: Monitora accuratezza quotidianamente
- **Settimana 2**: Se accuratezza < 85%, affina il prompt
- **Mese 1**: Traccia costi OpenAI (dovrebbe essere ~$0.17 per 1000 email)
- **Futuro**: Considera di aggiungere auto-archiviazione per "Promozione"

---

## Troubleshooting

### ❌ Errore: "Label non trovata"

**Problema**: Il nodo "Merge Category to Label ID" non produce output

**Causa**: Le label Gmail non esistono o il nome non corrisponde

**Soluzione**:
1. Vai su Gmail → Verifica che le 3 label esistano
2. Controlla lo spelling ESATTO (case-sensitive!)
3. Il nome deve essere identico a quello nel JSON schema:
   - `Alta Priorità` (non "alta priorità" o "Alta priorità")
   - `Finanza e Fatturazione` (non "Finanza e fatturazione")
   - `Promozione` (non "promozione")
4. Se hai scritto il nome in modo diverso:
   - Opzione A: Rinomina la label in Gmail
   - Opzione B: Modifica il JSON schema nel nodo "JSON Parser"

### ❌ Errore: "OpenAI API error"

**Problema**: Errore nel nodo "OpenAI GPT-4o-mini"

**Possibili Cause e Soluzioni**:

**Causa 1: API Key non valida**
- Verifica la API Key in n8n Credentials
- Genera una nuova key su platform.openai.com
- Aggiorna le credenziali in n8n

**Causa 2: Credito OpenAI esaurito**
- Vai su [platform.openai.com/account/billing](https://platform.openai.com/account/billing)
- Verifica il saldo disponibile
- Aggiungi credito se necessario

**Causa 3: Rate limit superato**
- Aspetta 1 minuto e riprova
- Se persiste, riduci la frequenza di polling (da 5 min a 10 min)

### ❌ Errore: "Gmail API quota exceeded"

**Problema**: Troppe chiamate API Gmail

**Soluzione**:
- Gmail quota giornaliera: 1 miliardo di unità (molto alto)
- Polling ogni 5 min usa ~288 chiamate/giorno (ben sotto il limite)
- Se vedi questo errore, potrebbe essere un bug temporaneo di Google
- Aspetta 1 ora e riprova

### ❌ Email non viene processata

**Problema**: Email arriva ma non riceve label

**Checklist Debug**:
1. [ ] L'email è in INBOX? (non in altre cartelle)
2. [ ] L'email è UNREAD? (il workflow processa solo unread)
3. [ ] Il workflow è ATTIVO? (toggle ON)
4. [ ] Sono passati almeno 5 minuti? (polling interval)
5. [ ] Controlla "Executions" in n8n - ci sono errori?

**Se tutte le risposte sono Sì ma email non processata**:
- Click su "Execute Workflow" manualmente
- Guarda quale nodo fallisce
- Leggi il messaggio di errore specifico

### ❌ Categorizzazione Errata

**Problema**: Email marketing riceve "Alta Priorità" invece di "Promozione"

**Causa**: Prompt ambiguo o caso edge non previsto

**Soluzione**:
1. **Raccogli esempi**: Annota 5-10 email categorizzate male
2. **Identifica pattern**: C'è un pattern comune? (es. tutte da stesso mittente)
3. **Affina prompt**:
   - Apri il nodo "Assign Category"
   - Modifica il prompt aggiungendo esempi specifici
   - Esempio: Se newsletter da "newsletter@company.com" vengono categorizzate male, aggiungi:
     ```
     - Email da domini contenenti "newsletter" → SEMPRE Promozione
     ```
4. **Testa modifiche**: Esegui manualmente il workflow con email problematiche
5. **Salva e monitora**: Se migliorato, salva e monitora per 2-3 giorni

**Alternativa**: Abbassa temperatura da 0.3 a 0.2 per output più deterministico

### ❌ Workflow Lento

**Problema**: Esecuzione impiega > 30 secondi per email

**Possibili Cause**:
- OpenAI API latenza (picco di traffico)
- Gmail API latency
- Connessione internet lenta

**Soluzioni**:
- Verifica stato OpenAI: [status.openai.com](https://status.openai.com)
- Controlla la tua connessione internet
- Se problema persiste, considera aumentare timeout nei nodi

---

## Ottimizzazioni Avanzate

### Modifica Frequenza Polling

**Per controllare più frequentemente** (ogni 1 minuto):
1. Apri nodo "Gmail Trigger"
2. In "Poll Times" → cambia `value: 5` in `value: 1`
3. Salva

**Per controllare meno frequentemente** (ogni 15 minuti):
1. Cambia `value: 5` in `value: 15`

### Aggiungere Auto-Archiviazione

Se vuoi archiviare automaticamente le email "Promozione":

1. Aggiungi un nodo **"IF"** dopo "Set Category Value"
2. Condizione: `{{ $json.category === "Promozione" }}`
3. Se True → aggiungi nodo Gmail "Remove from Inbox"
4. Se False → continua con il flusso normale

### Aggiungere Notifiche

Per ricevere notifica quando arriva email "Alta Priorità":

1. Aggiungi nodo **"IF"** dopo label applicata
2. Condizione: `{{ $json.category === "Alta Priorità" }}`
3. Se True → aggiungi nodo Slack/Telegram/Email
4. Invia notifica con subject e mittente

### Logging in Google Sheets

Per tracciare tutte le categorizzazioni:

1. Aggiungi nodo **"Google Sheets"** dopo "Set Category Value"
2. Operazione: "Append Row"
3. Valori da inserire:
   - Data/Ora: `{{ $now }}`
   - Subject: `{{ $('Get Message Content').item.json.subject }}`
   - From: `{{ $('Get Message Content').item.json.from }}`
   - Categoria: `{{ $json.category }}`

---

## Costi e Budget

### Stima Costi Mensili

**OpenAI GPT-4o-mini**:
- Costo per email: ~$0.00015
- 1,000 email/mese: $0.15
- 5,000 email/mese: $0.75
- 10,000 email/mese: $1.50

**Gmail API**: Gratuito (ben dentro quota limits)

**n8n**:
- Self-hosted: $0 (solo costi server)
- n8n Cloud: Da $20/mese (include 2,500 executions)

### Monitoraggio Costi

**OpenAI Dashboard**:
- Vai su [platform.openai.com/usage](https://platform.openai.com/usage)
- Controlla "Usage" per tracciare spesa giornaliera
- Imposta alert se superi soglia

**n8n Dashboard**:
- Vai su "Executions" per vedere quante volte il workflow è eseguito
- Ogni esecuzione = 1 email processata

---

## Risorse Aggiuntive

### Link Utili

- [Documentazione n8n](https://docs.n8n.io)
- [Forum Community n8n](https://community.n8n.io)
- [Documentazione OpenAI GPT-4o-mini](https://platform.openai.com/docs/models/gpt-4o-mini)
- [Gmail API Quotas](https://developers.google.com/gmail/api/reference/quota)

### Supporto

Se hai problemi:
1. Controlla prima questa guida
2. Cerca nel [forum n8n](https://community.n8n.io)
3. Contatta me per assistenza personalizzata

---

## Versione e Changelog

- **v1.0** (31/01/2026): Setup iniziale con 3 categorie
- Basato su Template n8n #4680
- Ottimizzato per GPT-4o-mini cost-effectiveness

---

**🎊 Congratulazioni! La tua inbox Gmail è ora intelligente e auto-organizzata!**
