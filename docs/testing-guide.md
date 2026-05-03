# Email di Test per Validazione Workflow

Usa queste 9 email per testare il workflow prima di attivarlo in produzione.

## 📧 Come Usare Queste Email di Test

1. **NON attivare il workflow** ancora
2. **Invia queste 9 email** al tuo account Gmail da un altro indirizzo
3. Assicurati che arrivino in **INBOX** e siano **UNREAD**
4. Esegui il workflow **manualmente** in n8n (bottone "Execute Workflow")
5. Verifica che ogni email riceva la **label corretta**

---

## ✅ Test Set 1: Alta Priorità

Queste email dovrebbero ricevere la label **"Alta Priorità"**

### Email Test #1 - Richiesta Urgente con Scadenza

```
Da: capo@company.com
A: tuo-email@gmail.com
Subject: URGENTE: Richiesta approvazione contratto entro venerdì

Body:
Buongiorno,

Ho bisogno della tua approvazione urgente sul contratto allegato con il cliente XYZ.
La scadenza è venerdì 2 febbraio alle 18:00.

Questo è un cliente molto importante e non possiamo permetterci ritardi.
Per favore confermami appena possibile.

Grazie,
Marco
```

**Perché "Alta Priorità"**: Contiene "URGENTE", scadenza temporale specifica, richiesta diretta di azione

---

### Email Test #2 - Domanda che Richiede Risposta

```
Da: cliente@example.com
A: tuo-email@gmail.com
Subject: Domanda importante sul progetto ABC

Body:
Ciao,

Puoi per favore chiarirmi questa questione tecnica sul progetto ABC?
Il cliente sta aspettando una risposta entro oggi pomeriggio.

Nello specifico, vorrei sapere se possiamo implementare la funzionalità X
con il budget attuale, oppure serve un'integrazione aggiuntiva.

Fammi sapere appena puoi, grazie!

Laura
```

**Perché "Alta Priorità"**: Domanda diretta, richiede input specifico, scadenza implicita (oggi)

---

### Email Test #3 - Action Item con Deadline

```
Da: hr@company.com
A: tuo-email@gmail.com
Subject: Action Item: Completa il form feedback entro domani mattina

Body:
Gentile collega,

Ti ricordiamo che devi completare obbligatoriamente il form di feedback
sul corso di formazione entro domani mattina alle 10:00.

Link al form: [link]

Questa è una deadline critica per motivi amministrativi.
Non saranno accettati invii tardivi.

Cordiali saluti,
Ufficio HR
```

**Perché "Alta Priorità"**: Action item esplicito, deadline precisa, richiesta obbligatoria

---

## 💰 Test Set 2: Finanza e Fatturazione

Queste email dovrebbero ricevere la label **"Finanza e Fatturazione"**

### Email Test #4 - Fattura in Scadenza

```
Da: amministrazione@fornitore.it
A: tuo-email@gmail.com
Subject: Fattura #FT-2024-001 - Pagamento in Scadenza

Body:
Gentile Cliente,

La informiamo che la fattura allegata (FT-2024-001) è in scadenza.

Dettagli fattura:
- Numero: FT-2024-001
- Data emissione: 15/01/2024
- Importo: €1,500.00 + IVA
- Scadenza: 31/01/2024

Le chiediamo cortesemente di procedere al pagamento entro la scadenza
per evitare interessi di mora.

Coordinate bancarie:
IBAN: IT12 3456 7890 1234 5678 9012
Causale: FT-2024-001

Distinti saluti,
Amministrazione
```

**Perché "Finanza e Fatturazione"**: Contiene "Fattura", "Pagamento", importo specifico, IBAN

---

### Email Test #5 - Conferma Pagamento

```
Da: payments@paymentgateway.com
A: tuo-email@gmail.com
Subject: Conferma pagamento ricevuto - €250.00

Body:
Ciao,

Il tuo pagamento è stato ricevuto correttamente.

Dettagli transazione:
- Importo: €250.00
- Data: 30/01/2024 ore 14:35
- Metodo: Carta **** 1234
- ID Transazione: TRX-789456123
- Merchant: Software Subscription Inc.

Grazie per la tua puntualità nel pagamento.
La ricevuta completa è disponibile nel tuo account.

Cordiali saluti,
Team Pagamenti
```

**Perché "Finanza e Fatturazione"**: Conferma pagamento, importo specifico, dettagli transazione

---

### Email Test #6 - Estratto Conto Bancario

```
Da: noreply@bancaonline.it
A: tuo-email@gmail.com
Subject: Estratto conto bancario mensile disponibile - Gennaio 2024

Body:
Gentile Cliente,

Il tuo estratto conto mensile di Gennaio 2024 è ora disponibile.

Riepilogo del periodo:
- Saldo iniziale: €5,450.00
- Entrate: €3,200.00
- Uscite: €2,890.00
- Saldo finale: €5,760.00

Puoi consultare i dettagli completi accedendo al tuo account online
nell'area "Estratti Conto".

Per qualsiasi chiarimento contatta il servizio clienti.

Cordiali saluti,
Banca Online S.p.A.
```

**Perché "Finanza e Fatturazione"**: Estratto conto, operazioni bancarie, saldi finanziari

---

## 🎁 Test Set 3: Promozione

Queste email dovrebbero ricevere la label **"Promozione"**

### Email Test #7 - Newsletter Marketing

```
Da: newsletter@techcompany.com
A: tuo-email@gmail.com
Subject: Newsletter Gennaio - Le nostre ultime novità di prodotto 🚀

Body:
Ciao!

Benvenuto alla newsletter di gennaio! Ecco le ultime novità dal nostro team.

🎉 NUOVI PRODOTTI LANCIATI:
- Software XYZ v2.0 con AI integrata
- Dashboard Analytics Pro
- Mobile App rinnovata

📚 ARTICOLI DEL MESE:
- Come ottimizzare il tuo workflow
- 5 trucchi per aumentare la produttività
- Case study: Cliente ABC aumenta ROI del 300%

👀 PROSSIMI EVENTI:
- Webinar gratuito: 15 febbraio
- Conferenza annuale: 20-22 marzo
- Workshop online: ogni martedì

Scopri di più sul nostro blog!

A presto,
Team Tech Company

---
Non vuoi più ricevere queste email? [Unsubscribe]
```

**Perché "Promozione"**: Newsletter tipica, contenuti marketing, link unsubscribe

---

### Email Test #8 - Offerta Promozionale

```
Da: sales@onlinecourse.com
A: tuo-email@gmail.com
Subject: ⚡ Offerta Lampo: 50% di sconto su TUTTI i corsi - Solo 48 ore!

Body:
🎓 NON PERDERE QUESTA OPPORTUNITÀ!

Per le prossime 48 ore SOLTANTO, tutti i nostri corsi online sono
scontati del 50%. È l'occasione perfetta per investire sulla tua formazione!

💥 OFFERTA VALIDA SU:
✓ Corso Python per Beginners (era €99, ora €49.50)
✓ Master in Digital Marketing (era €299, ora €149.50)
✓ Web Development Bootcamp (era €499, ora €249.50)
✓ Data Science con AI (era €399, ora €199.50)

⏰ SCADENZA: 2 febbraio ore 23:59

👉 USA IL CODICE: WINTER50

Non rimandare, i posti sono limitati!

[ACQUISTA ORA]

Il Team di Online Course
```

**Perché "Promozione"**: Offerta sconto, linguaggio marketing aggressivo, call-to-action

---

### Email Test #9 - Invito Evento Marketing

```
Da: events@businesscommunity.com
A: tuo-email@gmail.com
Subject: Ti aspettiamo al nostro Webinar Gratuito: "Produttività e AI nel 2024"

Body:
Ciao!

Sei invitato al nostro prossimo webinar GRATUITO:

🎯 TITOLO: "Come l'AI sta rivoluzionando la produttività aziendale nel 2024"

📅 QUANDO: Giovedì 8 febbraio 2024, ore 15:00-16:30
💻 DOVE: Online (riceverai il link dopo registrazione)
🎁 BONUS: Tutti i partecipanti riceveranno un eBook gratuito!

COSA IMPARERAI:
→ Strumenti AI per automatizzare task ripetitivi
→ Come integrare ChatGPT nel tuo workflow
→ Case study di aziende che hanno aumentato la produttività del 40%
→ Q&A con esperti del settore

I POSTI SONO LIMITATI!

[REGISTRATI GRATUITAMENTE ORA]

Non vediamo l'ora di vederti!

Team Business Community

P.S. Invita un collega e ricevi un ulteriore bonus esclusivo!

---
Business Community Inc. | www.businesscommunity.com
```

**Perché "Promozione"**: Invito evento, marketing focused, incentivi e bonus

---

## 📊 Checklist Validazione

Dopo aver eseguito il workflow con queste 9 email, verifica:

### ✅ Risultati Attesi

- [ ] **Email #1**: Label "Alta Priorità" ✓
- [ ] **Email #2**: Label "Alta Priorità" ✓
- [ ] **Email #3**: Label "Alta Priorità" ✓
- [ ] **Email #4**: Label "Finanza e Fatturazione" ✓
- [ ] **Email #5**: Label "Finanza e Fatturazione" ✓
- [ ] **Email #6**: Label "Finanza e Fatturazione" ✓
- [ ] **Email #7**: Label "Promozione" ✓
- [ ] **Email #8**: Label "Promozione" ✓
- [ ] **Email #9**: Label "Promozione" ✓

### ✅ Criteri di Successo

- [ ] 9/9 email hanno ricevuto una label (100% coverage)
- [ ] Almeno 8/9 hanno la label CORRETTA (89%+ accuracy)
- [ ] Nessun errore nel log di esecuzione n8n
- [ ] Ogni email ha UNA SOLA label (non multiple)
- [ ] Email sono rimaste in INBOX (non archiviate)
- [ ] Tempo totale esecuzione < 90 secondi (10 sec/email)

### ❌ Se il Test Fallisce

**Accuratezza < 89% (più di 1 errore)**:
- Identifica quale email è stata categorizzata male
- Leggi il messaggio di errore nel log n8n
- Controlla se il prompt deve essere affinato
- Vedi sezione Troubleshooting in [SETUP-ISTRUZIONI.md](SETUP-ISTRUZIONI.md)

**Email non hanno ricevuto label**:
- Verifica che le 3 label esistano in Gmail
- Controlla lo spelling esatto (case-sensitive!)
- Verifica che le credenziali Gmail siano configurate correttamente

**Errori nel log n8n**:
- Click sul nodo rosso per vedere l'errore specifico
- Errori comuni:
  - "Label not found" → Label Gmail non create o nome errato
  - "OpenAI API error" → API key non valida o credito esaurito
  - "Gmail API error" → Credenziali OAuth2 non configurate

---

## 🎯 Test Avanzati (Opzionale)

Se vuoi testare casi edge più complessi:

### Email Ambigua #10 - Potrebbe essere Alta Priorità O Finanza

```
Da: contabilita@azienda.it
Subject: URGENTE: Fattura cliente mancante - Serve approvazione oggi

Body:
Ciao, manca la fattura del cliente ABC per chiudere il bilancio trimestrale.
È urgente, il commercialista ha bisogno dell'approvazione entro oggi.
Puoi confermare l'importo?
```

**Categorizzazione attesa**: "Alta Priorità" (prevale l'urgenza)
**Alternativa accettabile**: "Finanza e Fatturazione"

### Email Ambigua #11 - Newsletter vs Alta Priorità

```
Da: security@company.com
Subject: Azione richiesta: Aggiorna la tua password per sicurezza

Body:
Per motivi di sicurezza, ti chiediamo di aggiornare la tua password
entro 48 ore. Questo è un messaggio automatico inviato a tutti gli utenti.

[Aggiorna Password]
```

**Categorizzazione attesa**: "Alta Priorità" (richiede azione)
**Alternativa accettabile**: "Promozione" (se interpretato come email di massa)

### Email Ambigua #12 - Marketing vs Finanza

```
Da: billing@softwarecompany.com
Subject: Il tuo piano gratuito sta per scadere - Upgrade ora con 20% sconto!

Body:
Il tuo trial gratuito termina tra 3 giorni. Passa al piano Premium
con il 20% di sconto! Solo per questa settimana.

[Upgrade Ora]
```

**Categorizzazione attesa**: "Promozione" (focus su sconto/marketing)
**Alternativa accettabile**: "Finanza e Fatturazione" (se focus su billing)

---

## 📝 Note per il Testing

### Best Practice

1. **Invia le email in sequenza** (non tutte insieme) per evitare rate limiting
2. **Aspetta 30 secondi tra invii** per permettere a Gmail di processarle
3. **Verifica che arrivino in INBOX** (controlla spam/promotions tabs)
4. **Esegui workflow manualmente** la prima volta (non via trigger automatico)
5. **Salva screenshot** dei risultati per riferimento futuro

### Variazioni per Test Personalizzati

Puoi modificare queste email per testare scenari specifici del tuo dominio:

- Cambia i nomi mittenti con domini reali che ricevi
- Adatta il linguaggio al tuo settore (tech, finance, retail, etc.)
- Aggiungi parole chiave specifiche che vedi nelle tue email reali

### Logging dei Risultati

Crea un foglio per tracciare i risultati:

| Email # | Categoria Attesa | Categoria Assegnata | Corretto? | Note |
|---------|------------------|---------------------|-----------|------|
| 1       | Alta Priorità    | Alta Priorità       | ✅        | Ok   |
| 2       | Alta Priorità    | Alta Priorità       | ✅        | Ok   |
| 3       | Alta Priorità    | Promozione          | ❌        | Fix  |
| ...     | ...              | ...                 | ...       | ...  |

**Calcolo Accuratezza**: `(Corretti / Totali) × 100%`

---

## 🚀 Pronto per Produzione?

Se hai superato questi test con successo (≥ 89% accuratezza), sei pronto per:

1. **Attivare il workflow** in produzione
2. **Monitorare** quotidianamente per la prima settimana
3. **Celebrare** la tua inbox organizzata! 🎉

---

**Versione**: v1.0
**Ultima Modifica**: 31/01/2026
**Compatibile con**: Workflow Gmail Auto-Categorizzazione v1.0
