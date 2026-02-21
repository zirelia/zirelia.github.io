---
layout: post
title: "Il Cervello: Dentro il Motore di Contenuto LLM di Zirelia"
date: 2025-01-05 10:00:00 +0100
categories: [architettura, ai]
lang: it
description: "Come Zirelia usa LangGraph, GPT-4 e la memoria ChromaDB per generare contenuti che suonano genuinamente umani — non come un template compilato."
image: /assets/images/blog/support-triage.png
---

## Il Problema con l'Automazione Basata su Template

La maggior parte degli strumenti di automazione social funziona con template:

> "Buongiorno! Oggi mi sento [AGGETTIVO]. Guarda il mio ultimo [TIPO_CONTENUTO]! #hashtag"

Il risultato è prevedibile, ripetitivo e immediatamente riconoscibile come automatizzato. I follower si disimpegnano. Le piattaforme lo flaggano.

Zirelia adotta un approccio completamente diverso: invece di riempire template, **ragiona** a partire dal carattere della persona.

## L'Architettura: Workflow LangGraph

La generazione di contenuti in Zirelia è un workflow multi-step orchestrato da **LangGraph**:

```
[Selezione Argomento] → [Generazione Pensiero] → [Scrittura Didascalia] → [Prompt Visivo] → [Controllo Qualità]
```

Ogni step è una chiamata LLM con un prompt specifico e ricco di contesto. I passaggi trasmettono dati in avanti, costruendo un post completo a partire da un'idea iniziale.

### Step 1: Selezione Autonoma dell'Argomento

Il cervello non aspetta istruzioni su cosa pubblicare. Seleziona argomenti autonomamente in base a:

- **Ora del giorno** → mattina = caffè/benessere; notte = introspezione/gaming
- **Interessi della persona** → selezione casuale ponderata dalla config YAML
- **Contesto memoria** → cosa è stato pubblicato recentemente (per evitare ripetizioni)

```python
def get_autonomous_topic(self, time_of_day: str) -> str:
    routine_topics = self.persona.routine.get(time_of_day, [])
    interest_topics = self.persona.interests
    # 70% routine, 30% interessi
    pool = routine_topics * 7 + interest_topics * 3
    return random.choice(pool)
```

### Step 2: Generazione del Pensiero

L'argomento selezionato viene passato al `PersonaBrain`, che genera un "pensiero" grezzo — un monologo interno dal punto di vista della persona:

```
System: Sei Sienna Fox, una creator di LA di 23 anni. Sei giocosa, sicura e autentica...
Human: A cosa stai pensando adesso? Argomento: sessione di yoga mattutina.
```

Il LLM risponde in personaggio, producendo qualcosa di autentico invece che generico.

### Step 3: Scrittura della Didascalia

Il pensiero grezzo viene raffinato in una didascalia social media rifinita, formattata per la piattaforma target (limiti di caratteri Twitter/X, stile hashtag, densità emoji).

### Step 4: Generazione del Prompt Visivo

Il cervello espande l'argomento in un prompt dettagliato per la generazione di immagini, incorporando:
- I descrittori fisici della persona
- La trigger word del LoRA
- Il contesto della scena (ora del giorno, location)
- Modificatori di qualità (fotorealistico, 4k, luce golden hour)

## Memoria: Vector Store ChromaDB

Il componente più importante per l'autenticità a lungo termine è la **memoria**.

Ogni post pubblicato viene embedato e archiviato in ChromaDB. Prima di generare nuovo contenuto, il cervello recupera i post passati semanticamente simili:

```python
similar_posts = memory.search(topic, n_results=5)
# Iniettato nel prompt: "Hai già pubblicato su X. Evita di ripeterti."
```

Questo impedisce all'AI di pubblicare ripetutamente gli stessi contenuti — una chiara spia dell'automazione.

Nel tempo, la persona sviluppa una storia di contenuti coerente, come se avesse un vero passato.

## Il Risultato

Un motore di contenuto che non si limita a riempire spazi vuoti — pensa, ricorda e crea.

La differenza è percepibile da qualsiasi lettore che interagisce con il feed abbastanza a lungo da notarla: i post sembrano provenire da un personaggio coerente ed in evoluzione, non da una macchina che gira con il pilota automatico.
