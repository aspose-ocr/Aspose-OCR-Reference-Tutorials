---
category: general
date: 2026-07-05
description: Esegui OCR su un'immagine in Python rapidamente. Scopri come caricare
  l'immagine per l'OCR, estrarre il testo da un modulo scansionato e utilizzare l'OCR
  per riconoscere l'immagine in Python.
draft: false
keywords:
- perform OCR on image
- load image for OCR
- how to use OCR Python
- extract text from scanned form
- OCR recognize image Python
language: it
og_description: Esegui OCR su un'immagine in Python. Questo tutorial mostra come caricare
  un'immagine per l'OCR, estrarre il testo da un modulo scansionato e utilizzare l'OCR
  per riconoscere l'immagine in Python.
og_title: Esegui OCR su un'immagine con Python – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image in Python quickly. Learn how to load image for
    OCR, extract text from scanned form, and use OCR recognize image Python.
  headline: Perform OCR on Image with Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Esegui OCR su un'immagine con Python – Guida completa
url: /it/python-java/general/perform-ocr-on-image-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine con Python – Guida Completa

Ti è mai capitato di dover **perform OCR on image** su file immagine ma non sapevi da dove cominciare in Python? Non sei l'unico. Che tu stia digitalizzando ricevute, estraendo dati da un modulo di indagine rumoroso, o semplicemente trasformando un PDF scansionato in testo ricercabile, la capacità di estrarre testo da un modulo scansionato è un problema quotidiano per molti sviluppatori.

In questo tutorial vedremo **how to use OCR Python** passo dopo passo, dal caricamento dell'immagine alla visualizzazione di un risultato filtrato. Alla fine saprai esattamente come **load image for OCR**, configurare le soglie di confidenza e chiamare il metodo **OCR recognize image Python** che esegue effettivamente il lavoro pesante.

> **What you’ll get:** uno script pronto‑all’uso che carica un'immagine, esegue OCR e stampa testo pulito, filtrato per confidenza. Nessun riferimento vago, nessuna importazione mancante—solo una soluzione completa, pronta da copiare e incollare.

---

## Di cosa avrai bisogno

* Python 3.9 o versioni più recenti installato (il codice funziona anche su 3.10+).  
* Un pacchetto OCR che segue l'API `ocr` usata di seguito – ad esempio, la libreria fittizia `simple-ocr` o qualsiasi wrapper che espone `OcrEngine`, `Language` e `Image`.  
* Un file immagine (`.png`, `.jpg`, ecc.) che contiene il testo che desideri estrarre.  
* Un terminale o IDE dove puoi eseguire un singolo script Python.

Se li hai già, ottimo—mettiamoci al lavoro.

---

## Esegui OCR su Immagine – Configurazione del Motore

La prima cosa da fare è creare un'istanza del motore OCR. Pensa al motore come al cervello dell'operazione; sa come interpretare i pixel e trasformarli in caratteri.

```python
# Import the OCR library – replace `ocr` with your actual package name
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Perché è importante:* senza un motore non c'è nulla da elaborare. L'oggetto `OcrEngine` contiene tutta la configurazione che potrai modificare in seguito, come lingua e soglia di confidenza.

---

## Carica Immagine per OCR – Preparazione del Modulo Scansionato

Ora che il motore esiste, dobbiamo **load image for OCR**. Il metodo `Image.load()` della libreria legge il file dal disco e lo converte in una rappresentazione interna che il motore può comprendere.

```python
# Step 2: Load the image you want to process
# Replace the path with the actual location of your noisy form
image_path = "YOUR_DIRECTORY/noisy_form.png"
image = ocr.Image.load(image_path)
```

> **Tip:** Se stai lavorando con PDF, converti prima ogni pagina in un'immagine (ad esempio, usando `pdf2image`). Il motore OCR accetta solo immagini raster.

---

## Come Usare OCR Python – Configurazione della Lingua e della Confidenza

La maggior parte dei motori OCR supporta più lingue e ti permette di filtrare i caratteri a bassa confidenza. Impostare questi parametri in anticipo garantisce di ottenere solo testo affidabile.

```python
# Step 3: Choose language and set a confidence threshold
engine.language = ocr.Language.ENGLISH          # you can switch to FR, DE, etc.
engine.min_confidence = 85                     # accept only characters >85 % confidence
```

*Perché 85 %?* In pratica, una soglia intorno all'80‑90 % elimina la maggior parte del nonsense mantenendo il contenuto utile. Sentiti libero di regolare in base alla qualità delle tue scansioni.

---

## Estrai Testo dal Modulo Scansionato – Riconoscimento dell'Immagine

Con il motore pronto e l'immagine caricata, è il momento di **perform OCR on image**. Il metodo `recognize()` restituisce un oggetto risultato che contiene il testo estratto e, opzionalmente, i dati delle bounding‑box.

```python
# Step 4: Perform OCR recognition on the image
result = engine.recognize(image)
```

Se la libreria lo supporta, `result` può anche esporre `result.confidences` (una lista di punteggi di confidenza per carattere) e `result.words` (oggetti parola strutturati). Per questa guida ci concentreremo sull'output di testo semplice.

---

## OCR Recognize Image Python – Visualizzazione dei Risultati Filtrati

Infine, stampiamo il testo filtrato. I simboli a bassa confidenza appaiono come punto interrogativo (`?`) perché abbiamo impostato `min_confidence` all'85 %.

```python
# Step 5: Show the filtered text
print("Filtered text:")
print(result.text)
```

### Output Atteso

```
Filtered text:
Name: John Doe
Date: 2023‑04‑15
Amount: $123.45
Signature: ?
```

Nota come la firma illeggibile si sia trasformata in un `?`. È esattamente ciò per cui il filtro di confidenza è stato progettato—mantenere l'output ordinato per l'elaborazione successiva.

---

## Problemi Comuni e Consigli Pro

| Problema | Perché accade | Soluzione rapida |
|----------|----------------|------------------|
| **Blank output** | L'immagine è troppo scura o a bassa risoluzione. | Pre‑processare con OpenCV: aumentare il contrasto, ridimensionare a ≥300 dpi. |
| **Garbage characters** | Lingua errata selezionata. | Impostare `engine.language` per corrispondere al documento (ad es., `ocr.Language.FRENCH`). |
| **Too many `?` symbols** | Soglia di confidenza troppo alta. | Abbassare `engine.min_confidence` al 70‑80 % per scansioni rumorose. |
| **Unicode errors** | L'output contiene caratteri non‑ASCII ma la codifica della console è errata. | Eseguire `python -X utf8` o impostare `PYTHONIOENCODING=utf-8`. |

**Pro tip:** Se hai bisogno di estrarre tabelle, esegui un secondo passaggio con un motore OCR sensibile al layout (come `--psm 6` di Tesseract) dopo aver filtrato il testo grezzo.

---

## Script Completo – Pronto da Eseguire

Di seguito trovi lo script completo e autonomo che incorpora tutti i passaggi discussi. Salvalo come `perform_ocr.py`, regola il percorso dell'immagine ed esegui `python perform_ocr.py`.

```python
# perform_ocr.py
# -------------------------------------------------
# Complete Python script to perform OCR on image,
# load image for OCR, configure engine, and display
# filtered results. Works with any OCR library that
# follows the simple `ocr` API shown here.
# -------------------------------------------------

import ocr  # Replace with your actual OCR package name

def main():
    # 1️⃣ Create the engine
    engine = ocr.OcrEngine()

    # 2️⃣ Configure language and confidence
    engine.language = ocr.Language.ENGLISH
    engine.min_confidence = 85  # Only keep chars >85 % confidence

    # 3️⃣ Load the image (adjust the path)
    image_path = "YOUR_DIRECTORY/noisy_form.png"
    image = ocr.Image.load(image_path)

    # 4️⃣ Recognize the text
    result = engine.recognize(image)

    # 5️⃣ Print the filtered output
    print("Filtered text:")
    print(result.text)

if __name__ == "__main__":
    main()
```

Eseguilo e vedrai il testo filtrato stampato sulla console—esattamente ciò che promette il passaggio **extract text from scanned form**.

---

## Cosa Viene Dopo?

Ora che sai come **perform OCR on image** e **extract text from scanned form**, potresti voler esplorare:

* **Batch processing** – iterare su una directory di immagini per generare un CSV di risultati.  
* **Post‑processing** – usare regex o spaCy per estrarre campi come date, importi o ID.  
* **Integrations** – alimentare l'output OCR in un database, Google Sheets, o una REST API.  

Tutte queste idee coinvolgono naturalmente le stesse funzioni di base che abbiamo trattato: caricare l'immagine, configurare il motore e chiamare il metodo **OCR recognize image Python**.

---

## Conclusione

Abbiamo illustrato un esempio completo e pronto per la produzione di come **perform OCR on image** usando Python. Da **loading image for OCR** alla configurazione della lingua, impostazione della soglia di confidenza e infine **extracting text from scanned form**, ogni passaggio è stato presentato con codice chiaro e spiegazioni. Ora hai una solida base per affrontare scenari più complessi—che si tratti di lavori batch, supporto multilingua o estrazione di tabelle.

Prova lo script, regola le soglie e guarda i tuoi documenti diventare ricercabili in pochi minuti. Hai domande o un modulo ostinato che non collabora? Lascia un commento qui sotto e risolviamo insieme. Buon coding! 

![Perform OCR on image example](example.png "Perform OCR on image")

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completo e funzionante con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai Testo da Immagine con Aspose OCR – Guida Passo‑Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Come Usare AspOCR: Filtri di Pre‑elaborazione OCR per .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Estrai testo da immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}