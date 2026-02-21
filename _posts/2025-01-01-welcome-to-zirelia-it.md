---
layout: post
title: "Benvenuti in Zirelia — Il Motore Autonomo per Virtual Influencer AI"
date: 2025-01-01 10:00:00 +0100
categories: [annuncio, visione]
lang: it
description: "E se il tuo profilo social si gestisse da solo — generando contenuti, creando immagini e pubblicando 24/7 — mentre dormi? Questo è Zirelia."
image: /assets/images/blog/welcome.png
---

## Il Paradosso dell'Influencer

Costruire una presenza sui social media è un lavoro a tempo pieno. Creare contenuti ogni giorno, mantenere un'identità visiva coerente, pubblicare al momento giusto, interagire con i follower — non si ferma mai.

Ma cosa succede se l'"influencer" non ha bisogno di dormire, mangiare o prendersi un giorno libero?

È questa l'idea alla base di **Zirelia**: un motore AI completamente autonomo che crea e gestisce una persona virtuale da zero a fine, senza intervento manuale.

## Cosa Fa Zirelia

Zirelia è costruito attorno a tre capacità fondamentali:

**Il Cervello** — Alimentato da GPT-4 e LangChain, Zirelia genera pensieri autentici, opinioni e idee di contenuto basate su una persona configurabile. Conosce il background della persona, i suoi interessi, il tono di voce e la routine quotidiana. Ha persino memoria — usando ChromaDB per ricordare i post passati ed evitare le ripetizioni.

**L'Immaginazione** — Ogni post può includere un'immagine generata dall'AI, creata da FLUX.1 tramite l'API di Replicate. Le immagini vengono generate per corrispondere all'identità visiva della persona, con un loop di controllo qualità che riprova se l'output non soddisfa lo standard.

**Le Mani** — Zirelia pubblica automaticamente su Twitter/X tramite l'API ufficiale. Carica media, scrive didascalie e programma i post in base a finestre temporali ottimali — senza bisogno di intervento umano.

## L'Architettura

Il sistema è completamente self-hosted e si avvia tramite Docker Compose:

```
docker compose up -d
```

Questo avvia cinque servizi: il server REST FastAPI, la coda task Celery, Redis, PostgreSQL per la cronologia dei post e il demone SmartScheduler che gira 24/7.

## Definisci una Persona, Ottieni un Influencer

Tutto inizia con un file YAML. Ecco un esempio minimale:

```yaml
name: "Sienna Fox"
age: 23
occupation: "Digital Creator & Lifestyle Model"
voice:
  tone: "Giocosa, sicura, autentica"
  style: "Frasi brevi, emoji, conversazionale"
interests:
  - "Fitness & benessere"
  - "Tech & AI"
  - "Viaggi"
```

Da questa definizione, Zirelia costruisce una persona completa — e inizia a generare contenuti che suonano genuinamente umani.

## Open Source, Self-Hosted

Zirelia è **open source** sotto la licenza Elastic License 2.0. Porti le tue chiavi API (OpenAI, Replicate, Twitter/X), il tuo server e la tua definizione di persona. L'Autore non ha accesso ai tuoi dati o ai contenuti generati.

Questa è la prima release. La roadmap include supporto Instagram, sintesi vocale e una dashboard di controllo visuale.

**Metti una stella al progetto su GitHub e unisciti all'esperimento.**
