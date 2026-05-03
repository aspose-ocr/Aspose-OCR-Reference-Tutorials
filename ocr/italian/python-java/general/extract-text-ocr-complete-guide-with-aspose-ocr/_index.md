---
category: general
date: 2026-05-03
description: Estrai rapidamente il testo OCR usando Aspose OCR. Scopri come migliorare
  l'accuratezza OCR, caricare l'immagine OCR, pre‑elaborare l'immagine OCR e eseguire
  la scansione OCR in Python.
draft: false
keywords:
- extract text ocr
- improve ocr accuracy
- load image ocr
- preprocess image ocr
- run OCR scan
language: it
og_description: Estrai rapidamente il testo OCR usando Aspose OCR. Impara come migliorare
  l'accuratezza OCR, caricare l'immagine OCR, pre‑elaborare l'immagine OCR e eseguire
  la scansione OCR in Python.
og_title: Estrai testo OCR – Guida completa con Aspose OCR
tags:
- OCR
- Python
- Aspose
title: Estrai testo OCR – Guida completa con Aspose OCR
url: /it/python-java/general/extract-text-ocr-complete-guide-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# estrarre testo OCR – Guida completa con Aspose OCR

Hai mai avuto bisogno di **estrarre testo OCR** da una scansione traballante ma non eri sicuro del perché i risultati sembrassero incomprensibili? Non sei solo—molti sviluppatori incontrano questo ostacolo quando l'immagine è inclinata, rumorosa o semplicemente a basso contrasto. La buona notizia è che qualche piccolo aggiustamento di configurazione può trasformare un'immagine confusa in testo pulito e ricercabile. In questo tutorial percorreremo un esempio completo, end‑to‑end, che ti mostra come **migliorare la precisione OCR**, **caricare immagine OCR**, **pre‑elaborare immagine OCR**, e infine **eseguire la scansione OCR** con Aspose OCR per Python.

Alla fine di questa guida avrai uno script eseguibile che legge un JPEG scansionato, lo pulisce automaticamente e stampa il testo estratto sulla console. Nessun misterioso link “vedi la documentazione”—tutto ciò di cui hai bisogno è qui.

## Di cosa avrai bisogno

- **Python 3.8+** (l'ultima versione stabile funziona meglio)
- **Aspose.OCR for Python via .NET** – installa con `pip install aspose-ocr`
- Un **file di licenza** (`Aspose.OCR.Java.lic`) se ne hai acquistato uno (la versione di prova gratuita funziona per i test)
- Un'immagine che desideri elaborare (ad es. `skewed_scanned_doc.jpg`)

È tutto. Se hai questi elementi, possiamo passare direttamente al codice.

## Passo 1: Estrarre testo OCR con il motore OCR di Aspose

La prima cosa da fare è avviare il motore OCR e applicare la tua licenza. Pensa al motore come al cervello che leggerà l'immagine; senza licenza rifiuterà di funzionare oltre un piccolo limite demo.

```python
# Step 1: Create an OCR engine instance and apply your license
import aspose.ocr as ocr

ocr_engine = ocr.OcrEngine()
ocr_engine.license = ocr.License().set_license("Aspose.OCR.Java.lic")
```

> **Perché è importante:** Applicare la licenza in anticipo evita un fallimento silenzioso in seguito. Se salti questo passo, il motore tornerà a una modalità limitata e otterrai solo una manciata di caratteri—definitivamente non quello che ti aspetti quando provi a **estrarre testo OCR**.

## Passo 2: Migliorare la precisione OCR con la pre‑elaborazione

Le scansioni storte o granulose sono la rovina di qualsiasi progetto OCR. Aspose ti permette di attivare una serie di impostazioni utili che ruotano, rimuovono il rumore e aumentano il contrasto automaticamente. Questo è il cuore di **migliorare la precisione OCR**.

```python
# Step 2: Enable preprocessing to improve accuracy on skewed or noisy scans
ocr_engine.config.auto_deskew = True          # automatically corrects rotation
ocr_engine.config.remove_noise = True         # reduces speckles
ocr_engine.config.enhance_contrast = True     # boosts text visibility
ocr_engine.config.binarization = "Otsu"       # choose a robust binarization method
```

- **auto_deskew** – ruota l'immagine nuovamente in orizzontale, fondamentale quando il documento originale non era perfettamente piatto.
- **remove_noise** – elimina le macchie casuali che spesso appaiono nei JPEG a bassa risoluzione.
- **enhance_contrast** – rende il testo scuro più scuro e lo sfondo chiaro più chiaro, aiutando il motore a distinguere i caratteri.
- **binarization = "Otsu"** – un algoritmo classico che decide la soglia migliore per la conversione in bianco‑nero.

> **Consiglio professionale:** Se sai che le tue immagini di origine sono già pulite, puoi disattivare queste opzioni per velocizzare l'elaborazione. Ma per la maggior parte delle scansioni reali, lasciarle attive è la scelta più sicura.

## Passo 3: Caricare immagine OCR per la scansione

Ora che il motore è pronto, dobbiamo **caricare immagine OCR**. Il metodo `Image.from_file` di Aspose supporta JPEG, PNG, TIFF e alcuni altri formati.

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Image.from_file("YOUR_DIRECTORY/skewed_scanned_doc.jpg")
```

Sostituisci `YOUR_DIRECTORY` con il percorso reale sul tuo computer. Se stai lavorando con uno stream di byte in memoria (ad es. da un upload web), puoi anche usare `ocr.Image.from_bytes(byte_data)`—lo stesso motore lo gestirà.

> **Caso limite:** I file TIFF di grandi dimensioni possono consumare molta memoria. Se incontri un `MemoryError`, considera di ridurre la risoluzione dell'immagine prima o di usare `ocr_engine.config.max_image_size` per limitare le dimensioni.

## Passo 4: Eseguire la scansione OCR e ottenere i risultati

Con l'immagine caricata e la pre‑elaborazione attiva, l'ultimo passo è **eseguire la scansione OCR**. Questa chiamata gestisce tutto il lavoro pesante dietro le quinte.

```python
# Step 4: Run the OCR process on the prepared image
ocr_result = ocr_engine.recognize(input_image)
```

L'oggetto `ocr_result` contiene diverse proprietà utili:

- `ocr_result.text` – la stringa semplice di cui hai bisogno.
- `ocr_result.confidence` – un punteggio numerico (0‑100) che indica l'affidabilità complessiva.
- `ocr_result.words` – una lista di oggetti parola con coordinate del riquadro di delimitazione, utile per evidenziare.

## Passo 5: Stampare il testo estratto

Infine, restituiamo il risultato. In un'applicazione reale potresti scrivere il testo su un file, un database o inviarlo a un indice di ricerca. Per questo tutorial, un semplice `print` è sufficiente.

```python
# Step 5: Print the extracted text
print("=== Extracted Text ===")
print(ocr_result.text)
print("\nConfidence:", ocr_result.confidence)
```

**Output previsto** (esempio per una fattura semplice):

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑04‑30
Total: $1,250.00

Confidence: 96.2
```

Se la confidenza è bassa (< 80), potresti voler rivedere le opzioni di pre‑elaborazione o provare un metodo di binarizzazione diverso come `"Sauvola"`.

## Bonus: Visualizzare la pipeline di pre‑elaborazione (Opzionale)

A volte è utile vedere cosa ha fatto il motore all'immagine. Aspose ti permette di esportare il bitmap elaborato:

```python
# Save the pre‑processed image for debugging
processed_image = ocr_engine.config.get_processed_image()
processed_image.save("processed_debug.png")
```

Potresti quindi inserire l'immagine nella documentazione:

<img src="ocr_workflow.png" alt="diagramma del flusso di estrarre testo OCR che mostra i passaggi di pre‑elaborazione">

> **Perché potresti farlo:** Quando il risultato OCR sembra sbagliato, uno sguardo veloce a `processed_debug.png` spesso rivela se l'immagine era ancora troppo scura, ancora inclinata, o aveva rumore residuo.

## Domande frequenti e problemi comuni

- **E se il mio documento è multi‑pagina?**  
  Aspose OCR funziona pagina per pagina. Cicla su ogni immagine di pagina e concatena `ocr_result.text`.

- **Posso riconoscere lingue diverse dall'inglese?**  
  Sì—imposta `ocr_engine.config.language = "fra"` (o qualsiasi codice ISO‑639‑2) prima di chiamare `recognize`.

- **C'è un limite alle dimensioni dell'immagine?**  
  Il motore limita a 10 MP per impostazione predefinita. Aumenta `ocr_engine.config.max_image_size` se ti servono scansioni più grandi, ma controlla l'uso della memoria.

- **Ho bisogno di un motore OCR separato per i PDF?**  
  Per i PDF puoi prima estrarre ogni pagina come immagine (usando Aspose.PDF) o utilizzare la funzione OCR PDF integrata. I passaggi mostrati qui rimangono gli stessi dopo aver ottenuto un'immagine.

## Riepilogo

Abbiamo coperto come **estrarre testo OCR** usando Aspose OCR per Python, dalla licenza del motore alla regolazione delle impostazioni che **migliorano la precisione OCR**, al caricamento del file sorgente, e infine **eseguire la scansione OCR** per ottenere testo pulito. Lo script completo è pronto per il copia‑incolla, e ora comprendi perché ogni flag di configurazione è importante.

## Cosa fare dopo?

- **Sperimenta con diversi metodi di binarizzazione** (`"Sauvola"`, `"Bradley"`). Alcuni caratteri rispondono meglio a soglie adattive.
- **Integra con un motore di ricerca** (ad es. Elasticsearch) usando il punteggio di confidenza per ordinare i risultati.
- **Combina con librerie di post‑elaborazione OCR** come `pyspellchecker` per pulire le comuni errate riconoscimenti.
- **Esplora l'elaborazione batch** per centinaia di scansioni—incapsula i passaggi in una funzione e fornisci una cartella di immagini.

Sentiti libero di modificare il codice, aggiungere i tuoi log, o integrarlo in una pipeline di gestione documenti più ampia. Se incontri problemi, lascia un commento qui sotto—buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}