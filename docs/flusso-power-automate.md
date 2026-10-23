# Flusso Power Automate – «BuddyBot - Crea ticket IT»

Flusso dell'agente richiamato dal topic «Richiesta PC – Ticket IT». Registra un ticket IT nel file `Ticket_IT.xlsx` su SharePoint e restituisce il numero del ticket all'agente.

```text
Quando un agente chiama il flusso (Nome, Reparto, Descrizione)
  → Componi «ID Ticket»
  → Excel Online (Business) – Aggiungi una riga in una tabella
  → Respond to the agent (NumeroTicket)
```

## Input e output

| Tipo | Nome | Formato | Valore passato dal topic |
|---|---|---|---|
| Input | Nome | Testo | `User.DisplayName` (variabile di sistema) |
| Input | Reparto | Testo | `Text(Topic.varReparto)` (formula Power Fx: la variabile è di tipo scelta, il flusso vuole testo) |
| Input | Descrizione | Testo | `varDescrizione` |
| Output | NumeroTicket | Testo | Output dell'azione «ID Ticket» |

## Espressioni

**ID Ticket** (azione Componi), ad esempio `TCK-261021-170106`:

```text
concat('TCK-', formatDateTime(convertFromUtc(utcNow(), 'W. Europe Standard Time'), 'yyMMdd-HHmmss'))
```

**Data apertura** (colonna Excel):

```text
formatDateTime(convertFromUtc(utcNow(), 'W. Europe Standard Time'), 'dd/MM/yyyy HH:mm')
```

## Azione «Aggiungi una riga in una tabella»

Posizione: sito del progetto → raccolta **Ticket IT** → file `Ticket_IT.xlsx` → tabella **TabellaTicket**. Il modello del file è in [`demo-data/Ticket_IT.xlsx`](../demo-data/Ticket_IT.xlsx).

| Colonna Excel | Valore | Come si inserisce |
|---|---|---|
| Formato datetime | (vuoto) | — |
| ID Ticket | Output di «ID Ticket» | contenuto dinamico |
| Data apertura | espressione `formatDateTime(...)` | fx |
| Nome | Nome (trigger) | contenuto dinamico |
| Reparto | Reparto (trigger) | contenuto dinamico |
| Descrizione | Descrizione (trigger) | contenuto dinamico |
| Stato | Aperto | testo |

## Note

- Il connettore Excel di Power Automate lavora solo su **tabelle Excel con un nome**: la tabella e le colonne non vanno rinominate.
- Il file dei ticket sta in una raccolta separata dalla fonte di conoscenza, così nomi e richieste dei colleghi non finiscono nelle risposte dell'agente.
- L'agente può usare solo flussi **pubblicati**.
- Il flusso usa le **credenziali dell'autore** (avviso mostrato alla pubblicazione dell'agente). Per una demo con un solo utente è accettabile; in produzione servirebbe un account di servizio con permessi minimi sul solo file dei ticket.
