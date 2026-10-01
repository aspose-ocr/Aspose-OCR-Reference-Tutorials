---
category: general
date: 2026-01-12
description: come impostare la lingua in Aspose OCR Python ed estrarre testo da un'immagine
  usando un dizionario personalizzato. Tutorial passo‑passo per sviluppatori.
draft: false
keywords:
- how to set language
- extract text from image
- how to extract text
- how to add dictionary
- how to process image
language: it
og_description: come impostare la lingua in Aspose OCR Python ed estrarre il testo
  da un'immagine con un dizionario personalizzato. Scopri l'intero flusso di lavoro
  in pochi minuti.
og_title: Come impostare la lingua in Aspose OCR Python – Guida completa
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Come impostare la lingua in Aspose OCR Python – Guida completa
url: /it/python-java/general/how-to-set-language-in-aspose-ocr-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# come impostare la lingua in Aspose OCR Python – Guida completa

Ti sei mai chiesto **come impostare la lingua** quando usi Aspose OCR in Python? Non sei solo—molti sviluppatori incontrano questo problema quando il modello predefinito in inglese non riconosce codici prodotto, numeri di serie o testo multilingue. La buona notizia è che la soluzione è sia semplice che potente. In questo tutorial vedremo come configurare la lingua, aggiungere un dizionario personalizzato, estrarre testo da un'immagine e, infine, elaborare l'immagine per ottenere i migliori risultati OCR.

Copriamo tutto ciò che devi sapere: dall'installazione della libreria all'esecuzione di un esempio completo che stampa il testo estratto. Alla fine sarai in grado di **estrarre testo da immagine** con fiducia, anche quando il contenuto include codici insoliti o lingue miste.

## Prerequisiti

* Python 3.8+ installato (il codice utilizza f‑strings, quindi le versioni precedenti non funzioneranno).
* Una licenza attiva di Aspose OCR per Python o una chiave di prova gratuita.
* Il pacchetto `asposeocr` installato tramite `pip install asposeocr`.
* Un'immagine di esempio (`product_label.png`) che contiene il testo che desideri leggere.

Se hai già questi elementi, ottimo—passiamo oltre. Altrimenti, scarica la prova gratuita dal sito di Aspose e esegui il comando di installazione; ci vuole solo un minuto.

## Passo 1: Importare il modulo Aspose OCR

La prima cosa da fare è importare le classi OCR nel tuo script. Questa è la base per **come impostare la lingua** in seguito.

```python
# Step 1: Import the Aspose OCR module
import asposeocr as ocr
```

> **Consiglio:** Mantieni le importazioni in cima al file. Rende lo script più facile da leggere, soprattutto quando torni su di esso in seguito.

## Passo 2: Come impostare la lingua

Per impostazione predefinita, Aspose OCR assume l'inglese. Se la tua immagine contiene francese, tedesco o qualsiasi altra lingua, dovrai indicare al motore quale lingua utilizzare. È qui che la parola chiave principale brilla.

```python
# Step 2: Create an OCR engine and set the recognition language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # change to ocr.Language.FRENCH, etc.
```

Perché è importante? I motori OCR si basano su modelli di caratteri specifici per lingua. Fornire la lingua corretta migliora notevolmente l'accuratezza—soprattutto per i caratteri accentati o le legature specifiche della lingua.

> **Nota:** Se devi supportare più lingue contemporaneamente, puoi passare una lista come `ocr.Language.ENGLISH | ocr.Language.SPANISH`.

## Passo 3: Come aggiungere un dizionario (parole definite dall'utente)

A volte il motore OCR interpreta erroneamente codici prodotto come “AB‑1234”. Puoi aumentare la confidenza fornendo un dizionario personalizzato. Questo risponde direttamente a **come aggiungere un dizionario** in Aspose OCR.

```python
# Step 3: Supply product codes that must be recognized with higher confidence
ocr_engine.set_user_defined_words(["AB-1234", "ZX-9876", "SKU-001"])
```

Il motore tratta queste parole come “note” e le privilegerà rispetto a caratteri simili. È particolarmente utile per numeri SKU, codici seriali o nomi di marca che non fanno parte di una lingua naturale.

## Passo 4: Come elaborare l'immagine

Ora che il motore è configurato, devi caricare l'immagine che vuoi analizzare. Questo affronta **come elaborare l'immagine** in modo pulito e ripetibile.

```python
# Step 4: Load the image containing the product label
image = ocr.Image.load("YOUR_DIRECTORY/product_label.png")
```

Se lavori con PDF, puoi prima convertire ogni pagina in un'immagine—Aspose OCR lo supporta nativamente.

## Passo 5: Come estrarre testo da immagine

Con tutto impostato, l'ultimo passo è eseguire l'OCR e recuperare il testo. Questo è il fulcro di **come estrarre testo** da un'immagine.

```python
# Step 5: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)

# Step 6: Print the extracted text
print(ocr_result.text)
```

Quando esegui lo script, dovresti vedere qualcosa del genere:

```
Product: AB-1234
Batch: ZX-9876
SKU: SKU-001
```

Se l'output appare confuso, ricontrolla di aver impostato la lingua corretta e che il tuo dizionario personalizzato contenga le stringhe esatte che ti aspetti.

## Esempio completo funzionante

Mettendo tutto insieme, ecco lo script completo che puoi copiare‑incollare in un file chiamato `extract_label.py`. Assicurati di sostituire `YOUR_DIRECTORY` con il percorso reale della tua immagine.

```python
import asposeocr as ocr

# Create OCR engine and set language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # Change if needed

# Add custom dictionary entries
ocr_engine.set_user_defined_words(["AB-1234", "ZX-9876", "SKU-001"])

# Load the target image
image = ocr.Image.load("YOUR_DIRECTORY/product_label.png")

# Perform OCR
ocr_result = ocr_engine.process(image)

# Output the result
print("=== OCR Extraction Result ===")
print(ocr_result.text)
```

### Output previsto

```
=== OCR Extraction Result ===
Product: AB-1234
Batch: ZX-9876
SKU: SKU-001
```

Se vedi i codici esatti che hai aggiunto al dizionario, hai padroneggiato con successo **come impostare la lingua**, **come aggiungere un dizionario** e **come estrarre testo da immagine** usando Aspose OCR.

## Gestione dei casi limite comuni

| Situazione | Cosa fare |
|------------|-----------|
| **L'immagine è sfocata** | Pre‑processa con `ocr.Image.apply_filter()` per nitidezza prima di chiamare `process()`. |
| **Più lingue in una singola immagine** | Imposta `ocr_engine.language = ocr.Language.ENGLISH | ocr.Language.SPANISH`. |
| **PDF di grandi dimensioni** | Itera su ogni pagina, convertila in `ocr.Image` e chiama `process()` per pagina. |
| **Caratteri inaspettati** | Aggiungili alla lista di parole definite dall'utente; Aspose OCR li tratta come token ad alta confidenza. |

## Riferimento visivo

![come impostare la lingua in Aspose OCR esempio](image.png "Screenshot che mostra come impostare la lingua in Aspose OCR Python")

*Testo alternativo:* **come impostare la lingua** screenshot che illustra l'assegnazione della proprietà language in un IDE Python.

## Conclusione

Ora sai **come impostare la lingua** in Aspose OCR Python, come **aggiungere voci al dizionario**, e i passaggi esatti per **estrarre testo da immagine** e **elaborare immagini** per risultati ottimali. L'esempio completo sopra può essere inserito in qualsiasi progetto, modificato per lingue diverse e ampliato per gestire l'elaborazione batch o input PDF.

Pronto per la prossima sfida? Prova a sostituire `ocr.Language.ENGLISH` con `ocr.Language.FRENCH` e osserva il miglioramento di accuratezza sulle etichette in lingua francese. Oppure sperimenta con il metodo `set_user_defined_words` per includere un intero catalogo di prodotti—il tuo motore OCR tratterà ogni voce come una corrispondenza ad alta confidenza.

Buona programmazione, e che i risultati OCR siano sempre cristallini!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}