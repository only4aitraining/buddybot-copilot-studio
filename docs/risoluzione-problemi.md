# Risoluzione dei problemi

Problemi incontrati durante lo sviluppo di BuddyBot e come sono stati risolti.

| Problema | Causa | Soluzione |
|---|---|---|
| Errore `EnforcementUsageCredits` («This environment is out of credits») | Agente con motore GitHub Copilot in un ambiente con 0 crediti Copilot (fatturazione a consumo attiva dal 1/9/2026 anche per ambienti Sviluppatore e di prova) | Creare un agente Standard; in alternativa chiedere all'IT di assegnare crediti all'ambiente o usare il pagamento a consumo con Azure (solo ambienti Produzione/Sandbox) |
| Agente con lingua principale inglese | La lingua si sceglie solo alla creazione | Ricreare l'agente impostando Italiano nelle impostazioni facoltative |
| Nome agente duplicato | Esisteva già un agente con lo stesso nome | Nome provvisorio con «2», poi rinomina dopo aver eliminato il vecchio agente |
| Escalation con messaggio generico | L'orchestratore sceglieva l'argomento di sistema «Esegui escalation» | Topic personalizzato con descrizione dettagliata dei temi riservati |
| Variabile non rinominabile («Argomento (0)», tipo unknown) | Topic non ancora salvato | Salvare il topic e aggiornare la pagina (F5), poi rinominare da {x} Variabili |
| Informazione presente nel PDF ma non trovata | Dato in una tabella: estratto non recuperato dalla ricerca SharePoint | Aggiungere frasi esplicite nel documento, sostituire il file e attendere la reindicizzazione (vedi il [caso del test 7](../tests/risultati-test.md#il-caso-del-test-7)) |
| Documento appena caricato non trovato | Indicizzazione SharePoint non ancora completata | Attendere da alcuni minuti ad alcune ore |
| Avviso «credenziali dell'autore» alla pubblicazione | Il flusso usa la connessione del creatore | Accettabile per la demo; in produzione account di servizio a permessi minimi |
| Benvenuto non visibile in Teams | Il benvenuto parte solo all'installazione | Rimuovere la cronologia della chat, disinstallare e reinstallare l'app |
| Messaggio di conferma con righe attaccate | Gli a capo singoli non vengono resi | Inserire una riga vuota tra le frasi del messaggio |

Le regole di licenza e di consumo dei crediti di Copilot Studio cambiano spesso: la situazione descritta è quella del tenant usato nel progetto (ottobre 2026).
