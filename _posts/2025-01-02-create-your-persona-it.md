---
layout: post
title: "Costruire la Tua Persona AI: Il File YAML Che Dà Vita a un Personaggio"
date: 2025-01-02 10:00:00 +0100
categories: [guida, persona]
lang: it
description: "Il persona.yaml è il cuore di Zirelia. Ecco come progettare un personaggio che sembri reale, pubblichi in modo autentico e rimanga coerente 24/7."
image: /assets/images/blog/create-persona.png
---

## Perché il Design della Persona è Importante

Un'AI che pubblica contenuti casuali è solo rumore. Ciò che separa un virtual influencer di successo da un account spam è la **coerenza** — una voce riconoscibile, un'estetica coerente, una personalità credibile.

In Zirelia, tutto questo vive in un singolo file: `config/persona.yaml`.

## L'Anatomia di una Persona

Una persona ben progettata ha cinque livelli:

### 1. Identità

I fatti base che ancorano tutto il resto:

```yaml
name: "Sienna Fox"
age: 23
nationality: "Americana (Los Angeles, CA)"
occupation: "Digital Creator & Lifestyle Model"
```

Non sono solo metadati — il LLM li usa per inquadrare ogni contenuto. Una creator di 23 anni da LA pubblica in modo molto diverso da un dirigente londinese di 45 anni.

### 2. Tratti Fisici

Usati dalla pipeline di generazione immagini per mantenere la coerenza visiva:

```yaml
physical_traits:
  hair: "Castano chiaro / Biondo scuro (Ondulato)"
  eyes: "Nocciola / Marrone caldo"
  style: "Casual-chic, athleisure, stile spiaggia"
  vibe: "Naturale, abbronzata, accessibile"
```

Questi descrittori vengono iniettati in ogni prompt di FLUX.1, garantendo che le immagini generate sembrino la stessa persona in centinaia di post.

### 3. Voce e Tono

È qui che il personaggio prende davvero vita:

```yaml
voice:
  tone: "Seducente ma amichevole, come una migliore amica figa di cui sei innamorato"
  style: "Breve, incisivo, usa gli emoji in modo naturale"
  catchphrases:
    - "Solo per te... 😉"
    - "Ti sei già innamorato?"
    - "Vibes check ✨"
  avoid:
    - "Linguaggio formale"
    - "Tono corporate"
    - "Negatività"
```

Il LLM usa questo come guida di stile per ogni didascalia, risposta e pensiero che genera.

### 4. Routine Quotidiana

Lo SmartScheduler di Zirelia usa la routine della persona per scegliere argomenti contestualmente appropriati:

```yaml
routine:
  morning: ["Stretching/Yoga mattutino", "Caffè in felpa oversize", "Journaling"]
  afternoon: ["Lavoro dal caffè", "Allenamento in palestra", "Commissioni"]
  evening: ["Tramonto in spiaggia", "Preparativi per la cena"]
  night: ["Pensieri notturni", "Gaming", "Skincare routine"]
```

Un post generato alle 7 del mattino menzionerà il caffè del mattino, non un locale notturno.

### 5. Interessi

Il motore di contenuto sceglie argomenti da questa lista, mescolando interessi principali (70%) con varietà casuale (30%):

```yaml
interests:
  - "Bio-hacking & Salute"
  - "Relazioni & Dating moderno"
  - "Tech & AI"
  - "Viaggi di lusso"
  - "Psicologia & Mindset"
  - "Moda & Style"
```

## Il Risultato

Con un persona.yaml ben costruito, Zirelia genera contenuti che suonano come una persona reale — perché l'AI ha un vero personaggio da cui attingere.

Il cervello non si limita a riempire template. Ragiona su cosa direbbe questa persona specifica, a quest'ora del giorno, dati i suoi interessi e la sua storia.

Questa è la differenza tra automazione e autenticità.
