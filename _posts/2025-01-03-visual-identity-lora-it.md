---
layout: post
title: "Coerenza Visiva su Scala: Addestrare un LoRA per il Tuo AI Influencer"
date: 2025-01-03 10:00:00 +0100
categories: [guida, generazione-immagini]
lang: it
description: "Come addestrare un modello LoRA personalizzato affinché ogni immagine generata da Zirelia sembri la stessa persona — stessa faccia, stesso stile, stesso brand."
image: /assets/images/blog/visual-identity-lora.png
---

## Il Problema dell'Identità Visiva

Il testo è facile da mantenere coerente. Definisci una voce e il LLM la segue. Ma le immagini sono più difficili.

Out-of-the-box, FLUX.1 genererà ogni volta un viso diverso, anche con gli stessi descrittori. "Capelli castano chiaro ondulati, occhi nocciola, pelle abbronzata" produrrà decine di variazioni — nessuna delle quali è riconoscibilmente la stessa persona.

Perché un virtual influencer sembri reale, **ogni immagine deve sembrare la stessa persona**.

La soluzione: un modello **LoRA** (Low-Rank Adaptation) personalizzato, addestrato su un dataset sintetico della tua persona.

## Cos'è un LoRA?

Un LoRA è una tecnica di fine-tuning leggera per i modelli di diffusione. Invece di riaddestrare l'intero modello (che costerebbe migliaia di euro), si addestra un piccolo layer adattatore che orienta il modello verso il tuo personaggio specifico.

Il risultato: un modello che genera il viso della tua persona in modo coerente, indipendentemente dalla scena, dall'illuminazione o dall'outfit.

## Step 1: Costruire un Dataset Sintetico

Non hai bisogno di foto reali. Genera un dataset di 30–50 immagini usando FLUX.1 con descrittori dettagliati, coprendo:

- Luci diverse (ora d'oro, studio, luce naturale)
- Espressioni diverse (sorridente, seria, che ride, di profilo)
- Ambientazioni diverse (caffè, palestra, spiaggia, casa)
- Stili di abbigliamento diversi

Consiglio sulla coerenza: usa un seed fisso per il primo batch, poi varia angolazioni e contesti.

## Step 2: Didascaliare il Dataset

Ogni immagine ha bisogno di una didascalia testuale che descriva la scena. Esempio:

```
a photo of [trigger_word], a 23-year-old woman with light brown wavy hair
and hazel eyes, wearing workout clothes, in a modern gym, natural lighting,
photorealistic, 4k
```

Sostituisci `[trigger_word]` con un identificatore univoco (es. `siennafox23`) che attiverà la tua persona durante l'inferenza.

## Step 3: Addestrare il LoRA

Usa la pipeline di training hosted di **Replicate** o esegui localmente con `kohya_ss`:

```bash
python train_network.py \
  --pretrained_model_name_or_path="black-forest-labs/FLUX.1-dev" \
  --train_data_dir="./dataset_sienna" \
  --output_dir="./lora_sienna" \
  --network_dim=32 \
  --max_train_epochs=20
```

Il training richiede ~30 minuti su una GPU A100 tramite Replicate.

## Step 4: Configurare Zirelia per Usare il Tuo LoRA

Nel file `.env`:

```env
REPLICATE_MODEL_VERSION=il-tuo-username/sienna-fox-lora:latest
LORA_TRIGGER_WORD=siennafox23
```

Da questo momento, ogni immagine che Zirelia genera includerà automaticamente la trigger word nel prompt, producendo un viso coerente in tutti i post.

## Il Loop di Controllo Qualità

Zirelia include un critico integrato che valuta le immagini generate prima di pubblicarle. Se l'immagine non supera i controlli di qualità (viso sbagliato, artefatti, distorsioni delle mani), la pipeline riprova fino a 3 volte con prompt aggiustati.

Il risultato è un feed in cui ogni immagine sembra scattata dallo stesso fotografo, della stessa persona — automaticamente, su scala.
