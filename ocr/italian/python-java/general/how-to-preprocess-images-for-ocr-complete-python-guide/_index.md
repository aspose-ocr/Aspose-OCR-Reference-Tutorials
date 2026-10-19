---
category: general
date: 2026-06-06
description: Come pre‑processare le immagini per OCR usando Python. Impara a binarizzare
  l'immagine con Otsu, a raddrizzare i documenti scansionati e a migliorare l'accuratezza
  OCR per il testo tedesco.
draft: false
keywords:
- how to preprocess images for OCR
- binarize image using otsu
- how to deskew scanned documents
- how to improve OCR accuracy
- extract text from german image
language: it
og_description: Come pre-elaborare le immagini per l'OCR in Python. Questo tutorial
  mostra come binarizzare l'immagine usando Otsu, come raddrizzare i documenti scannerizzati
  e come migliorare l'accuratezza dell'OCR per immagini tedesche.
og_title: Come preelaborare le immagini per OCR – Guida completa Python
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  headline: How to Preprocess Images for OCR – Complete Python Guide
  type: TechArticle
- description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  name: How to Preprocess Images for OCR – Complete Python Guide
  steps:
  - name: How to Deskew Scanned Documents
    text: The `deskew` call above is the concrete answer to **how to deskew scanned
      documents**. Internally it estimates the dominant text line angle via Hough
      transform and rotates the image back. If your documents are rotated more than
      5°, bump `max_angle` up, but beware of over‑rotation artifacts.
  - name: Binarize Image Using Otsu
    text: The `binarize(method="otsu")` line directly answers the query **binarize
      image using otsu**. Otsu’s algorithm computes a threshold that minimizes intra‑class
      variance, which is perfect for documents with bimodal histograms (dark text
      vs. light background).
  - name: Expected Output
    text: 'Assuming the sample scan contains the sentence “Die schnelle braune Füchsin
      springt über den faulen Hund.” you should see something like:'
  type: HowTo
tags:
- OCR
- image preprocessing
- Python
- German language
title: Come preelaborare le immagini per OCR – Guida completa in Python
url: /it/python-java/general/how-to-preprocess-images-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come Preprocessare le Immagini per OCR – Guida Completa in Python

Ti sei mai chiesto **come preprocessare le immagini per OCR** in modo che il testo risulti cristallino? Non sei l’unico. I documenti scansionati—soprattutto le pagine tedesche rumorose—possono essere un incubo per qualsiasi motore OCR. La buona notizia? Alcuni passaggi intelligenti di preprocessing possono trasformare una scansione sfocata e macchiata in un’immagine pulita e leggibile dalla macchina.

In questo tutorial percorreremo un esempio pratico che mostra **come preprocessare le immagini per OCR** usando Python. Imparerai a **binarizzare l’immagine usando Otsu**, **come correggere l’inclinazione dei documenti scansionati**, e in generale **come migliorare la precisione OCR** quando devi **estrarre testo da file immagine in tedesco**. Niente fronzoli, solo uno script funzionante che puoi copiare‑incollare oggi.

## Cosa Ti Serve

- **Python 3.9+** (qualsiasi versione recente va bene)
- Una libreria OCR che espone una classe `OcrEngine` – per la demo assumiamo un pacchetto generico `ocr`. Installala con `pip install ocr-lib`.
- Una scansione tedesca rumorosa (`noisy_german_scan.tif`) su cui vuoi testare.
- Una conoscenza di base delle funzioni Python (se hai già scritto un `def`, sei a posto).

> **Consiglio professionale:** Se usi un SDK OCR diverso (ad esempio Tesseract tramite `pytesseract`), i concetti rimangono gli stessi—basta adattare i nomi dei metodi.

## Panoramica della Soluzione

1. **Creare un’istanza del motore OCR.**  
2. **Impostare la lingua di riconoscimento su tedesco.**  
3. **Costruire una pipeline di preprocessing personalizzata** che includa correzione dell’inclinazione, denoising, binarizzazione (Otsu) e stretching del contrasto.  
4. **Collegare la pipeline al motore** così ogni immagine la attraversa automaticamente.  
5. **Eseguire l’OCR** su una scansione tedesca rumorosa.  
6. **Stampare il testo estratto** per verificare il risultato.

Di seguito scomponiamo ogni passaggio, spieghiamo **perché** è importante e mostriamo il codice esatto di cui hai bisogno.

![come preprocessare le immagini per OCR esempio](image.png "come preprocessare le immagini per OCR esempio")

## Step 1: Creare un’Istanza del Motore OCR

Prima di tutto—senza un motore, non succede nulla. L’oggetto `OcrEngine` è il punto di ingresso che coordina tutti i successivi processi.

```python
# Step 1: Initialize the OCR engine
from ocr import OcrEngine, Language

ocr_engine = OcrEngine()
```

*Perché è importante:* Inizializzare il motore configura le risorse interne (come i modelli linguistici) e ti fornisce una base pulita a cui collegare una pipeline personalizzata in seguito.

## Step 2: Impostare la Lingua di Riconoscimento su Tedesco

La precisione OCR dipende molto dalla lingua. Indicando al motore di aspettarsi il tedesco, attivi il set di caratteri corretto e il modello linguistico appropriato.

```python
# Step 2: Tell the engine we’re working with German text
ocr_engine.set_recognition_language(Language.GERMAN)
```

Se salti questo passaggio, il motore potrebbe usare l’inglese di default, riconoscendo male le umlaut (ä, ö, ü) e il carattere ß—trappole comuni quando si lavora con scansioni tedesche.

## Step 3: Costruire una Pipeline di Preprocessing Personalizzata

Questo è il cuore di **come preprocessare le immagini per OCR**. Concatenamo quattro trasformazioni:

| Trasformazione | Cosa fa | Perché è utile |
|----------------|---------|----------------|
| **Deskew** | Ruota l’immagine nuovamente in orizzontale (max 5°) | Le scansioni raramente sono perfettamente allineate; la correzione dell’inclinazione elimina la slant che confonde la segmentazione dei caratteri. |
| **Denoise** | Riduce i punti casuali (intensità 0.7) | Il rumore crea bordi falsi che il motore OCR può interpretare come caratteri. |
| **Binarize (Otsu)** | Converte in bianco‑nero usando il metodo di Otsu | Un’immagine binaria pulita fornisce al motore un contrasto netto tra primo piano (testo) e sfondo. |
| **Contrast Stretch** | Espande la gamma dinamica | Migliora la leggibilità di tratti deboli, specialmente su documenti vecchi. |

```python
# Step 3: Assemble the preprocessing pipeline
preprocessing_pipeline = (
    ocr_engine.preprocessing()
               .deskew(max_angle=5)          # auto‑deskew up to 5°
               .denoise(strength=0.7)       # medium denoise
               .binarize(method="otsu")      # **binarize image using Otsu**
               .contrast(stretch=True)      # auto contrast stretch
)

# Explanation:
# - `deskew` corrects rotation; 5° is a safe ceiling for most scans.
# - `denoise` with 0.7 balances smoothing without erasing thin characters.
# - `binarize` with method "otsu" automatically selects the optimal threshold.
# - `contrast` stretch brightens faint ink while keeping dark ink dark.
```

### Come Correggere l’Inclinazione dei Documenti Scansionati

La chiamata `deskew` sopra è la risposta concreta a **come correggere l’inclinazione dei documenti scansionati**. Internamente stima l’angolo dominante delle linee di testo tramite trasformata di Hough e ruota l’immagine indietro. Se i tuoi documenti sono ruotati più di 5°, aumenta `max_angle`, ma fai attenzione agli artefatti di sovra‑rotazione.

### Binarizzare l’Immagine Usando Otsu

La riga `binarize(method="otsu")` risponde direttamente alla query **binarizzare immagine usando otsu**. L’algoritmo di Otsu calcola una soglia che minimizza la varianza intra‑classe, perfetta per documenti con istogrammi bimodali (testo scuro vs. sfondo chiaro).

## Step 4: Collegare la Pipeline al Motore

Ora diciamo al motore OCR di eseguire ogni immagine in ingresso attraverso la pipeline appena creata.

```python
# Step 4: Register the custom pipeline
ocr_engine.set_preprocessing(preprocessing_pipeline)
```

*Perché è importante:* Senza la registrazione, il motore elaborerebbe la scansione grezza, ignorando tutta la pulizia che abbiamo configurato. Questo passaggio garantisce **come migliorare la precisione OCR** applicando lo stesso preprocessing in modo coerente.

## Step 5: Riconoscere il Testo da una Scansione Tedesca Rumorosa

È il momento di mettere tutto insieme. Forniamo al motore un’immagine tedesca rumorosa e lasciamo che faccia il lavoro pesante.

```python
# Step 5: Run OCR on the target file
image_path = "YOUR_DIRECTORY/noisy_german_scan.tif"
recognition_result = ocr_engine.recognize_image(image_path)
```

Se sei curioso delle prestazioni, puoi cronometrarne la chiamata:

```python
import time
start = time.time()
result = ocr_engine.recognize_image(image_path)
print(f"OCR took {time.time() - start:.2f}s")
```

## Step 6: Stampare il Testo Riconosciuto

Infine, stampiamo la stringa estratta. Questa è la risposta diretta a **estrarre testo da immagine tedesca**.

```python
# Step 6: Display the OCR output
print("=== Recognized German Text ===")
print(recognition_result.text)
```

### Output Atteso

Supponendo che la scansione di esempio contenga la frase “Die schnelle braune Füchsin springt über den faulen Hund.” dovresti vedere qualcosa di simile:

```
=== Recognized German Text ===
Die schnelle braune Füchsin springt über den faulen Hund.
```

Se l’output contiene ancora caratteri illeggibili, considera di regolare la forza del `denoise` o aumentare `max_angle` per la correzione dell’inclinazione.

## Problemi Comuni & Come Affrontarli

- **Modello linguistico mancante:** Dimenticare `set_recognition_language(Language.GERMAN)` porta spesso a perdere le umlaut. Controlla la chiamata.
- **Over‑denoising:** Una forza superiore a 0.9 può cancellare tratti sottili, specialmente in font più vecchi. Mantieni 0.5‑0.7 nella maggior parte dei casi.
- **Formato file errato:** Alcuni motori OCR non gestiscono TIFF multi‑pagina. Se hai un documento multi‑pagina, dividilo in file singoli prima.
- **Ordine della pipeline:** L’ordine mostrato (deskew → denoise → binarize → contrast) è intenzionale. Binarizzare prima del denoising può fissare il rumore; denoise sempre per primo.

## Estendere la Pipeline (Cosa Viene Dopo?)

Ora che hai una solida base, potresti voler:

- **Aggiungere un’apertura morfologica** per pulire piccoli blob (`.morph_open(kernel=3)`).
- **Integrare un modello linguistico** per la correzione post‑processo (`ocr_engine.apply_spellcheck()`).
- **Parallelizzare l’elaborazione batch** per grandi dataset usando `concurrent.futures`.

Tutte queste sono estensioni naturali che mantengono intatta l’idea di **come preprocessare le immagini per OCR** mentre potenziano **come migliorare la precisione OCR** ancora di più.

## Conclusione

Abbiamo appena coperto **come preprocessare le immagini per OCR** dall’inizio alla fine: creare un motore, impostare la lingua tedesca, costruire una pipeline che **binarizza l’immagine usando Otsu**, **come correggere l’inclinazione dei documenti scansionati**, e infine **estrarre testo da immagine tedesca** con maggiore fiducia. Seguendo i sei passaggi sopra vedrai un salto notevole nella qualità del riconoscimento—niente più correzioni manuali infinite.

Prova lo script con le tue scansioni, sperimenta i parametri e lascia che i risultati parlino da soli. Hai domande su un particolare aggiustamento di preprocessing? Lascia un commento e approfondiremo insieme.

Buona programmazione, e che il tuo OCR sia sempre preciso!

## Cosa Dovresti Imparare Dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrarre testo da immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Come Impostare il Valore di Soglia nel Riconoscimento Immagine OCR](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Come Eseguire OCR su Immagine – Eseguire OCR su Immagine nel Riconoscimento Immagine OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}