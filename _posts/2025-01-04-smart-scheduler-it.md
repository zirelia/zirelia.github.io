---
layout: post
title: "Lo SmartScheduler: Come Zirelia Pubblica Come un Umano, Non Come un Bot"
date: 2025-01-04 10:00:00 +0100
categories: [architettura, automazione]
lang: it
description: "Pubblicare a intervalli fissi è il modo più rapido per essere flaggati. Ecco come lo SmartScheduler di Zirelia imita il comportamento umano per restare sotto il radar."
image: /assets/images/blog/smart-scheduler.png
---

## Il Problema del Rilevamento Bot

Le piattaforme social stanno diventando sempre più brave a rilevare gli account automatizzati. Uno dei segnali più chiari: la **regolarità meccanica**.

Una persona reale non pubblica esattamente alle 09:00, 13:00 e 18:00 ogni singolo giorno. Pubblica quando ne ha voglia, salta un giorno quando è occupata, pubblica due volte in una domenica pigra e resta silenziosa durante le festività.

Uno script di automazione ingenuo con un cron fisso non assomiglia per nulla a questo — e le piattaforme se ne accorgono.

Lo **SmartScheduler** di Zirelia è progettato per risolvere esattamente questo problema.

## Come Funziona lo SmartScheduler

### Finestre Temporali, Non Orari Fissi

Invece di pubblicare a orari esatti, lo scheduler definisce *finestre* di pubblicazione basate sulla routine quotidiana della persona:

```python
TIME_WINDOWS = {
    "morning":   (8, 10),   # 8:00–10:00
    "afternoon": (12, 15),  # 12:00–15:00
    "evening":   (17, 20),  # 17:00–20:00
    "night":     (21, 23),  # 21:00–23:00
}
```

All'interno di ogni finestra, l'orario effettivo del post è **randomizzato** con una distribuzione gaussiana attorno al punto medio. Il risultato sembra umano perché lo è statisticamente.

### Variazione del Volume Giornaliero

Lo scheduler non pubblica lo stesso numero di volte ogni giorno. Estrae da un range configurabile:

```env
MAX_DAILY_POSTS=3
MIN_DAILY_POSTS=1
```

Alcuni giorni pubblica una volta. Alcuni giorni tre volte. Occasionalmente salta un giorno del tutto — come un creator reale che "si è disconnesso".

### Consapevolezza di Festività ed Eventi

Lo SmartScheduler conosce le festività (configurabili per locale) e riduce la frequenza di pubblicazione durante queste. Può anche essere configurato per pubblicare di *più* durante eventi di tendenza.

```python
HOLIDAYS = ["2025-12-25", "2025-01-01", "2025-04-25"]
```

Durante le festività, lo scheduler riduce i post a 0–1 e adatta gli argomenti dei contenuti all'occasione.

### Supporto Fuso Orario

Tutto gira nel fuso orario locale della persona (default: `America/Los_Angeles`), così i post appaiono a orari locali naturali:

```env
TIMEZONE=America/Los_Angeles
```

## Rate Limiting di Sicurezza

Oltre alla randomizzazione della schedulazione, il `SafetyManager` impone limiti rigidi per prevenire abusi accidentali dell'API:

- Massimo N post per finestra di 24 ore continuative
- Intervallo minimo tra post consecutivi (configurabile)
- Pausa automatica se Twitter/X restituisce errori di rate limit

## Avviare lo Scheduler

```bash
# Tramite Docker (consigliato)
docker compose up scheduler -d

# Oppure direttamente
python run_scheduler.py
```

Lo scheduler gira come demone persistente, svegliandosi periodicamente per verificare se è ora di generare e pubblicare. Registra ogni decisione — orario del post, selezione dell'argomento, risultato della pubblicazione — in un file di log locale.

Il risultato: un feed che sembra organico, cresce in modo costante e non attiva gli algoritmi di rilevamento delle piattaforme.
