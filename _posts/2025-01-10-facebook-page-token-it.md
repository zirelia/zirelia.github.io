---
layout: post
title: "Il Segreto dei Token Meta: Come evitare i blocchi API"
date: 2025-01-10 10:00:00 +0100
categories: [guida, configurazione]
lang: it
description: "La guida essenziale per ottenere il Permanent Page Access Token di Facebook. Risolviamo il mistero del bug 'User Token' e facciamo funzionare l'automazione 24/7."
image: /assets/images/blog/sienna-case-study.jpg
---

Abbiamo stabilito che Meta è la casa naturale per Zirelia. La barriera all'ingresso non sono gli algoritmi di shadowban, ma la navigazione dell'ostico **Meta Developer Portal**. Spesso gli account AI falliscono ancora prima di inviare la primissima richiesta API `v26.0` a causa dei Token svaniti nel nulla. 

Ecco come domare le API Graph e fare in modo che Zirelia pubblichi h24, senza continui refresh manuali.

## La Trappola della "Business Verification"
Appena crei la tua App nel portale Developer, potresti imbatterti in spaventosi banner rossi che richiedono documenti aziendali o partita IVA per la **Business Verification**. 

*Ignorali totalmente.* Non servono. 

Fin quando mantieni l'App in stato "Development" e concedi l'accesso solo ai TUOI account privati (il tuo Instagram associato e la tua Pagina Facebook), godrai degli stessi permessi illimitati senza dover verificare nessuna azienda.

## Perché il 'Page Dropdown' continua a resettarsi?

Il problema tecnico numero uno incontrato dalla community nel *Graph API Explorer* è non riuscire a generare un Token di Pagina; il menu a tendina ritorna perennemente su "User Token" o peggio, l'endpoint `me/accounts` restituisce un array vuoto `[]`.

Questo è un bug/misconfigurazione di permesso. La **Soluzione in 3 Step** definitiva:
1. Revoca l'accesso dell'App dalle "Integrazioni Business" sul tuo Profilo FB Personale.
2. Clicca di nuovo su "Generate Token" nel Graph Explorer e, *fondamentale*, nella finestra popup di autorizzazione Facebook clicca esplicitamente su "Modifica l'accesso precedente". Seleziona a mano la tua Nuova Pagina AI e il Profilo Instagram associato.
3. Seleziona tutti i permessi necessari: `instagram_basic`, `instagram_content_publish`, `pages_manage_posts`, ecc. 

## L'Access Token Permanente
Di default, i token utente decadono dopo 1 ora, e se estesi nel tool durano 60 giorni. Un'AI autonoma non può fermarsi ogni 60 giorni. Serve il **Permanent Page Access Token**: 

1. Prendi il Token da 60 giorni. 
2. Incollalo nel campo "Access Token" del Graph Explorer.
3. Esegui la query GET per l'endpoint `me/accounts`.
4. La stringa alfanumerica lunghissima che troverai affiancata al nome della tua Pagina Facebook nell'output JSON è il Santo Graal: è imperitura. 

Copia questa stringa. Sarà per sempre la variabile `META_ACCESS_TOKEN` nel file `.env` sul tuo Raspberry Pi. 

**Risultato finale:** Il tuo Cron/Celery è ora certificato a vita, a patto che tu non cambi forzatamente la password personale del tuo profilo Facebook. Zirelia può ora postare alle 4 del mattino, completamente slegata dalle tue direttive umane.
