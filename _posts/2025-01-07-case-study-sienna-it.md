---
layout: post
title: "Case Study: Sienna Fox — Costruire un Virtual Influencer da Zero"
date: 2025-01-07 10:00:00 +0100
categories: [case-study, risultati]
lang: it
description: "Uno sguardo dietro le quinte di Sienna Fox, la virtual influencer di riferimento costruita con Zirelia — dalla progettazione della persona ai primi post."
image: /assets/images/blog/data-export.png
---

## Chi è Sienna Fox?

Sienna Fox è una digital creator e lifestyle model di 23 anni con base a Los Angeles. Ama lo yoga mattutino, i caffè con latte d'avena, il biohacking e le sessioni di gaming a tarda notte.

Non esiste.

Sienna Fox è la virtual influencer di riferimento costruita e gestita dal progetto Zirelia — un test nel mondo reale delle capacità del motore, che gira 24/7 su un singolo server.

## Costruire la Persona

Il processo di design è iniziato non con la tecnologia, ma con il personaggio.

L'obiettivo era una persona che sembrasse **credibile e autentica** — abbastanza aspirazionale da attrarre follower, ma abbastanza accessibile da sembrare qualcuno che potresti davvero conoscere.

Decisioni chiave prese durante il design della persona:

- **Età 23**: Abbastanza giovane per essere autentica nello spazio lifestyle/wellness, abbastanza grande da avere opinioni ed esperienza
- **Location LA**: Massima rilevanza culturale per i social media anglofoni
- **Interessi misti**: Fitness + tech + dating = ampia varietà di contenuti senza sembrare dispersiva
- **Tono**: Giocoso ma non infantile, seducente ma non esplicito

La persona completa è stata definita in circa 200 righe di YAML prima che venisse scritto un singolo post.

## Costruire l'Identità Visiva

L'identità visiva è stata la parte più difficile.

**Step 1**: Generati 50 immagini seed con FLUX.1 usando descrittori dettagliati, con un prompt base fisso e angolazioni, luci e scene variate.

**Step 2**: Selezionate manualmente le migliori 30 immagini, scartando quelle con incoerenze del viso o artefatti.

**Step 3**: Addestrato un LoRA personalizzato su questo dataset in ~45 minuti su una GPU A100 di Replicate.

**Step 4**: Testato il LoRA su 20 prompt di scena diversi, verificando che il viso rimanesse coerente tra pose yoga, ambientazioni da caffè e look serali.

Costo totale: circa 8€ in compute Replicate.

## Il Primo Mese: Osservazioni Chiave

Dopo quattro settimane di operatività (warm-up manuale per le prime due settimane, poi automazione completa):

**Volume di contenuto**: 67 post generati e pubblicati, con una media di 2,4 al giorno e variazione naturale.

**Qualità dei contenuti**: Il cervello ha evitato con successo le ripetizioni in tutti i casi tranne 3 (che sono stati intercettati dal sistema di recupero della memoria e rigenerati).

**Qualità delle immagini**: Il 91% delle immagini ha superato il loop di controllo qualità al primo tentativo. Il restante 9% ha richiesto un solo tentativo aggiuntivo.

**Coerenza della voce**: La metrica più soggettiva — ma abbastanza coerente da far sì che i primi follower riconoscessero il suo tono nelle risposte.

## Cosa Abbiamo Imparato

**Il persona.yaml è tutto.** Le definizioni di personaggio vaghe producono contenuti vaghi. Più la persona è specifica e umana, più l'output è specifico e umano.

**La coerenza visiva richiede un LoRA.** I soli prompt testuali producono troppa variazione in decine di post. L'investimento nel LoRA (tempo + ~8€) si ripaga immediatamente.

**Il warm-up non è negoziabile.** Passare direttamente all'automazione su un account nuovo è il percorso più rapido verso la sospensione. Due settimane di attività manuale sono il minimo.

**La memoria conta più del previsto.** Senza la memoria ChromaDB, il cervello ripeteva argomenti nell'arco di una settimana. Con la memoria abilitata, la diversità dei contenuti è migliorata notevolmente.

## Il Motore Dietro l'Influencer

Sienna Fox gira su un singolo VPS con 4GB di RAM e 2 vCPU. Costo totale mensile dell'infrastruttura: circa 20€ (server) + costi API variabili in base al volume di pubblicazione.

Il motore Zirelia è ciò che rende possibile tutto questo a quel costo. L'intera pipeline — selezione argomento, generazione LLM, creazione immagine, schedulazione, pubblicazione — automatizzata e in esecuzione senza intervento umano.

Questa è la promessa di Zirelia: **definisci una persona, e il motore fa il resto.**
