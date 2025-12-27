---
category: general
date: 2025-12-27
description: Estrai il testo da un'immagine usando Aspose OCR e correggi gli errori
  di OCR. Scopri come caricare l'immagine per l'OCR e correggere rapidamente gli errori.
draft: false
keywords:
- extract text from image
- load image for ocr
- how to correct ocr errors
- Aspose OCR Python
- OCR post‑processing
language: it
og_description: Estrai il testo dall'immagine con Aspose OCR e correggi istantaneamente
  gli errori di OCR. Segui questo tutorial per caricare l'immagine per l'OCR e pulire
  i risultati.
og_title: Estrai testo da immagine con Aspose OCR – Guida completa
tags:
- OCR
- Python
- Aspose
- Text Extraction
title: Estrai testo da immagine con Aspose OCR – Guida passo‑passo
url: /it/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da immagine con Aspose OCR – Guida passo‑passo

Hai mai avuto bisogno di **estrarre testo da un'immagine** ma ti sei impantanato in output OCR disordinati? Non sei il solo. In molti progetti di automazione—pensa al processamento di fatture, alla scansione di ricevute o alla digitalizzazione di vecchi documenti—il primo ostacolo è ottenere testo pulito e ricercabile da un'immagine.  

In questo tutorial ti guideremo attraverso un esempio completo e eseguibile che mostra come **caricare l'immagine per OCR**, eseguire il riconoscimento e poi **correggere gli errori OCR** usando il correttore ortografico basato su AI di Aspose. Alla fine avrai uno script unico che trasforma un PNG di una fattura in testo pulito e ricercabile, pronto per qualsiasi flusso di lavoro successivo tu abbia in mente.

## Cosa imparerai

- Come installare e importare le librerie Aspose OCR e AI in Python.  
- Il codice esatto necessario per **caricare l'immagine per OCR** (senza congetture).  
- Come eseguire il motore OCR e catturare la stringa grezza.  
- Perché l'OCR produce spesso errori di battitura e come il correttore ortografico integrato può **correggere gli errori OCR** automaticamente.  
- Suggerimenti per gestire casi particolari come PDF multi‑pagina o scansioni a bassa risoluzione.

> **Prerequisiti:** Python 3.8+, una licenza valida di Aspose OCR (o una prova gratuita) e un file immagine (ad es., `invoice.png`) che desideri elaborare.

---

## Estrai testo da immagine – Configurare Aspose OCR

Prima di poter fare qualsiasi cosa, abbiamo bisogno dei pacchetti giusti. Aspose distribuisce il suo motore OCR come modulo installabile con pip.

```bash
pip install aspose-ocr
```

Se desideri anche il post‑processore AI, installa il pacchetto complementare:

```bash
pip install aspose-ocr-ai
```

> **Consiglio professionale:** Mantieni i pacchetti aggiornati. Alla data di stesura le versioni più recenti sono `aspose-ocr 23.12` e `aspose-ocr-ai 23.12`.

Una volta che le librerie sono sul tuo sistema, importa le classi che utilizzerai:

```python
# Step 1: Import the OCR and AI classes
from aspose.ocr import OcrEngine, AsposeAI
```

> **Perché è importante:** L'importazione delle classi specifiche mantiene pulito lo spazio dei nomi e rende evidente quali componenti sono responsabili del riconoscimento rispetto al post‑processing.

---

## Carica immagine per OCR – Preparare il PNG della tua fattura

Il passo logico successivo è puntare il motore al file che vuoi leggere. È qui che la parola chiave **caricare immagine per OCR** brilla.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 3: Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Spiegazione:** `OcrEngine()` crea un nuovo motore con impostazioni predefinite (lingua inglese, autorotazione, ecc.). Il metodo `load_image()` accetta un percorso file, uno stream o anche un array di byte—così puoi fornire immagini da disco, dal web o da un buffer in memoria.

### Problemi comuni durante il caricamento delle immagini

| Problema | Sintomo | Soluzione |
|----------|----------|-----------|
| Bassa DPI (<300) | Caratteri confusi, numeri mancanti | Ricampiona l'immagine a 300 dpi o superiore prima del caricamento |
| Modalità colore errata (CMYK) | Forme dei caratteri errate | Converti in RGB usando Pillow (`Image.convert("RGB")`) |
| PDF multi‑pagina | Viene elaborata solo la prima pagina | Converti ogni pagina in immagine e itera su di esse |

---

## Esegui OCR e ottieni il testo grezzo

Ora che il motore sa dove si trova l’immagine, possiamo effettivamente leggerla.

```python
# Step 4: Perform OCR to extract raw text
raw_text = ocr_engine.recognize()
print("Raw OCR output:")
print(raw_text)
```

La chiamata `recognize()` restituisce una semplice stringa Python. In molti scenari reali l'output conterrà spazi superflui, caratteri letti erroneamente o interruzioni di riga spezzate—specialmente con ricevute che usano font condensati.

> **Perché catturiamo prima raw_text:** Ti fornisce una base di riferimento per confrontarla con la versione pulita in seguito, utile per il debug o per l’audit.

---

## Come correggere gli errori OCR – Usare Aspose AI Spell‑Check

Aspose fornisce un wrapper AI leggero che può eseguire un correttore ortografico sul risultato grezzo. Questo risponde direttamente alla domanda **come correggere gli errori OCR**.

```python
# Step 5: Initialise the AI post‑processor and choose a spell‑check processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("spell_check")
```

Puoi sostituire `"spell_check"` con altri processori come `"grammar_check"` o `"named_entity_recognition"` se il tuo caso d'uso lo richiede.

```python
# Step 6: Clean the OCR output using the selected post‑processor
clean_text = ai_processor.run_postprocessor(raw_text)

# Step 7: Output the corrected text
print("\nCorrected OCR output:")
print(clean_text)
```

### Cosa fa il correttore ortografico dietro le quinte

1. **Tokenizzazione** – Divide la stringa grezza in parole e punteggiatura.  
2. **Ricerca nel dizionario** – Confronta ogni token con un dizionario inglese (o uno personalizzato che puoi fornire).  
3. **Punteggio contestuale** – Usa un piccolo modello linguistico per decidere se una correzione si adatta alle parole circostanti.  
4. **Sostituzione** – Restituisce una nuova stringa con le correzioni più probabili applicate.

> **Caso limite:** Se la lingua di origine non è l'inglese, passa il codice lingua appropriato quando crei `AsposeAI()` (ad es., `AsposeAI(language="fr")`).

---

## Verifica e utilizza il testo pulito

A questo punto hai due variabili: `raw_text` (l'output OCR diretto) e `clean_text` (la versione corretta). Quale conservare dipende dalle esigenze successive.

```python
# Example: Save the cleaned text to a .txt file for later indexing
with open("invoice_extracted.txt", "w", encoding="utf-8") as f:
    f.write(clean_text)

print("\n✅ Cleaned text saved to invoice_extracted.txt")
```

Se stai alimentando il risultato in un motore di ricerca, un database o un modello di machine‑learning, preferisci sempre la versione **pulita**—altrimenti propagherai rumore OCR lungo l’intera pipeline.

---

## Esempio completo funzionante

Di seguito trovi lo script completo che puoi copiare‑incollare in un file chiamato `extract_invoice.py`. Si assume che tu abbia già installato i due pacchetti Aspose e che l’immagine si trovi in `YOUR_DIRECTORY/invoice.png`.

```python
# extract_invoice.py
# -------------------------------------------------------------
# Complete example: extract text from image and correct OCR errors
# -------------------------------------------------------------

# 1️⃣ Import required classes
from aspose.ocr import OcrEngine, AsposeAI

# 2️⃣ Create OCR engine and load the target image
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

# 3️⃣ Run OCR – get raw text
raw_text = ocr_engine.recognize()
print("Raw OCR output:")
print(raw_text)

# 4️⃣ Initialise AI spell‑check post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("spell_check")

# 5️⃣ Clean the OCR output
clean_text = ai_processor.run_postprocessor(raw_text)

# 6️⃣ Show the corrected result
print("\nCorrected OCR output:")
print(clean_text)

# 7️⃣ Persist the cleaned text for later use
with open("invoice_extracted.txt", "w", encoding="utf-8") as out_file:
    out_file.write(clean_text)

print("\n✅ Cleaned text saved to invoice_extracted.txt")
```

Eseguilo con:

```bash
python extract_invoice.py
```

Dovresti vedere il dump grezzo seguito da una versione più ordinata, e un file chiamato `invoice_extracted.txt` apparirà nella stessa cartella.

---

## Domande frequenti (FAQ)

**D: Questo funziona con i PDF?**  
R: Non direttamente. Converti ogni pagina PDF in un’immagine (ad es., usando `pdf2image`) e fai girare lo script sui PNG risultanti.

**D: La mia lingua non è l'inglese—posso comunque usare il correttore ortografico?**  
R: Sì. Passa il codice lingua desiderato a `AsposeAI(language="de")` per il tedesco, `"es"` per lo spagnolo, ecc.

**D: E se il motore OCR rileva male la disposizione di una tabella?**  
R: Aspose OCR offre il flag `set_layout_analysis(True)`. Attivarlo migliora il riconoscimento delle tabelle ma può aumentare i tempi di elaborazione.

**D: Come gestire batch estremamente grandi?**  
R: Avvolgi la logica principale in una funzione e usa un pool di thread o async IO per parallelizzare su più core o macchine.

---

## Conclusione

Abbiamo mostrato come **estrarre testo da immagine** usando Aspose OCR, come **caricare l'immagine per OCR**, e il modo più semplice per **correggere gli errori OCR** con il correttore ortografico AI integrato. Lo script completo e eseguibile dimostra il flusso end‑to‑end—from loading the invoice PNG to saving a clean, searchable `.txt` file.

Sentiti libero di sperimentare: sostituisci il correttore ortografico con la correzione grammaticale, alimenta l'output in un classificatore NLP, o integra il processo in un più ampio sistema di gestione documentale. Il cielo è il limite una volta che disponi di testo affidabile e corretto.

Hai altre domande su OCR, Aspose o automazione Python? Lascia un commento qui sotto, e buona programmazione! 

---

![Esempio di estrazione testo da immagine](extract_text_image.png "Estrai testo da immagine con Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}