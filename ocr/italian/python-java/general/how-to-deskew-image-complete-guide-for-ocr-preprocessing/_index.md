---
category: general
date: 2026-07-05
description: Come correggere rapidamente l'inclinazione di un'immagine. Impara a pre‑processare
  l'immagine per OCR, correggere la rotazione dell'immagine e convertire la scansione
  in testo con Python.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- convert scan to text
- correct image rotation
language: it
og_description: Come correggere l'inclinazione di un'immagine e preelaborare l'immagine
  per OCR. Questa guida mostra come correggere la rotazione dell'immagine ed estrarre
  il testo dall'immagine usando Python.
og_title: Come raddrizzare l'immagine – Pre‑elaborazione OCR passo passo
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to deskew image quickly. Learn to preprocess image for OCR, correct
    image rotation, and convert scan to text with Python.
  headline: How to Deskew Image – Complete Guide for OCR Preprocessing
  type: TechArticle
tags:
- OCR
- image-processing
- Python
title: Come raddrizzare l'immagine – Guida completa alla pre‑elaborazione OCR
url: /it/python-java/general/how-to-deskew-image-complete-guide-for-ocr-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come Correggere l'Inclinazione di un'Immagine – Guida Completa per la Pre‑elaborazione OCR

Ti sei mai chiesto **come correggere l'inclinazione di un'immagine** che sembra essere stata scansionata con uno scanner storto? Non sei l'unico. In molti progetti reali la prima cosa da fare prima di **estrarre testo da un'immagine** è raddrizzare quel disallineamento.  

In questo tutorial percorreremo un esempio pratico, end‑to‑end, che **preelabora l'immagine per OCR**, corregge la rotazione e infine **converte la scansione in testo** usando una libreria OCR per Python. Nessun riferimento vago, solo uno script funzionante da copiare‑incollare, più consigli sui problemi più comuni.  

## Cosa Riuscirai a Ottenere

* Caricare qualsiasi JPEG o PNG scansionato leggermente inclinato.  
* Applicare un filtro di correzione dell'inclinazione e un passaggio di binarizzazione per migliorare l'accuratezza OCR.  
* Eseguire il motore OCR e **estrarre testo da un'immagine** in modo affidabile.  
* Comprendere perché **la rotazione corretta dell'immagine** è importante per l'estrazione del testo successiva.  

### Prerequisiti

* Python 3.9+ installato sulla tua macchina.  
* Un pacchetto OCR installabile via pip che imiti lo spazio dei nomi `ocr` usato nell'esempio (ad esempio, un leggero wrapper attorno a Tesseract).  
* Familiarità di base con le funzioni Python e i concetti di elaborazione delle immagini.  

Se li hai, tuffiamoci.

![how to deskew image example](deskew_before_after.png){alt="come correggere l'inclinazione dell'immagine – prima e dopo la correzione"}

## Passo 1: Configurare il Motore OCR – Come Correggere l'Inclinazione dell'Immagine con Python

Prima di tutto: ti serve un motore OCR che possa comprendere la lingua del tuo documento. Il frammento qui sotto mostra il boilerplate minimo per creare il motore e indicargli che stai lavorando con testo in inglese.

```python
import ocr  # Assume this is a wrapper around your OCR backend

# Create an OCR engine instance and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH
```

*Perché è importante:*  L'impostazione della lingua del motore influenza il set di caratteri e il dizionario utilizzati. Saltare questo passaggio può far sì che l'OCR interpreti erroneamente parole comuni, soprattutto dopo aver **corretto la rotazione dell'immagine**.

## Passo 2: Caricare l'Immagine Scansionata da Raddrizzare

Ora carichiamo il file in memoria. Sostituisci `"YOUR_DIRECTORY/skewed_scan.jpg"` con il percorso della tua immagine.

```python
# Load the raw scanned image
raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")
```

Se l'immagine è già in un array NumPy o in un `Mat` di OpenCV, puoi adattare il caricatore di conseguenza – la chiave è che l'oggetto deve esporre il metodo `apply_filter` usato in seguito.

## Passo 3: Preelaborare l'Immagine per OCR – Correggere l'Inclinazione e Binarizzare

Ecco dove avviene la magia. Concatenamo due filtri:

1. **Deskew** – rileva automaticamente la linea di base del testo dominante e ruota l'immagine nuovamente in orizzontale.  
2. **Binarize (Otsu)** – converte l'immagine in puro bianco‑e‑nero, migliorando drasticamente i tassi di riconoscimento.

```python
# Preprocess: deskew then binarize
preprocessed_image = (
    raw_image
    .apply_filter(ocr.Filter.deskew())          # <-- how to deskew image
    .apply_filter(ocr.Filter.binarize_otsu())  # improves OCR reliability
)
```

*Consiglio professionale:*  Se noti che il testo appare ancora sfocato dopo la binarizzazione, prova a regolare il contrasto o a usare un metodo di sogliatura diverso. Il modulo `ocr.Filter` include spesso `adaptive_threshold()` per i casi più difficili.

## Passo 4: Eseguire l'OCR – Estrarre Testo da un'Immagine

Con una tela pulita e raddrizzata, passiamo l'immagine al motore. L'oggetto risultato contiene la stringa riconosciuta, i punteggi di confidenza e persino le bounding box se ti servono in seguito.

```python
# Perform recognition on the preprocessed image
recognition_result = engine.recognize(preprocessed_image)

# Print the raw text output
print(recognition_result.text)
```

Un output tipico appare così:

```
Invoice #12345
Date: 2026-07-01
Total: $1,250.00
Thank you for your business!
```

Nota come le interruzioni di riga siano perfettamente allineate? Questo è il vantaggio di una **rotazione corretta dell'immagine** – l'OCR non deve più indovinare l'orientamento delle linee.

## Passo 5: Mettere Tutto Insieme – Uno Script Monofile per Convertire la Scansione in Testo

Di seguito trovi lo script completo, eseguibile, che combina tutti i componenti discussi. Salvalo come `deskew_ocr.py` ed esegui `python deskew_ocr.py`.

```python
#!/usr/bin/env python3
"""
Complete example: how to deskew image, preprocess it for OCR,
and extract text from a scanned document.
"""

import ocr  # Replace with your actual OCR library import

def main():
    # 1️⃣ Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Load the image (change path as needed)
    raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")

    # 3️⃣ Preprocess – deskew then binarize
    preprocessed = (
        raw_image
        .apply_filter(ocr.Filter.deskew())          # how to deskew image
        .apply_filter(ocr.Filter.binarize_otsu())  # preprocess image for OCR
    )

    # 4️⃣ Recognize text
    result = engine.recognize(preprocessed)

    # 5️⃣ Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

### Perché Questo Funziona

* **Deskew prima** – ruotare l'immagine prima della binarizzazione garantisce che l'algoritmo di sogliatura lavori su un orizzonte livellato.  
* **Binarizzare dopo il deskew** – il metodo di Otsu assume un istogramma bimodale; una pagina inclinata rovinerebbe tale assunzione.  
* **Modello di lingua inglese** – indica all'OCR quali caratteri aspettarsi, riducendo i falsi positivi.  

Se devi gestire altre lingue, basta sostituire `ocr.Language.ENGLISH` con l'enumerazione appropriata.

## Domande Frequenti & Casi Limite

| Domanda | Risposta |
|----------|--------|
| *E se la scansione è capovolta?* | Il filtro `deskew()` di solito rileva anche una rotazione di 180°. Se fallisce, chiama `apply_filter(ocr.Filter.rotate(180))` prima del deskew. |
| *Il mio documento contiene grafiche a colori – la binarizzazione le eliminerà?* | Sì. Per contenuti misti, considera di usare solo `ocr.Filter.deskew()`, poi esegui l'OCR sull'immagine a colori. Puoi comunque estrarre il testo preservando le grafiche. |
| *Posso elaborare un batch di file?* | Racchiudi la logica in un ciclo, leggi ogni percorso file da una lista e salva ogni `result.text` in un file `.txt` separato. |
| *Come migliorare l'accuratezza su scansioni a bassa risoluzione?* | Ingrandisci l'immagine con un filtro bicubico **prima** del deskew, poi applica un filtro di nitidezza. Più pixel forniscono al motore OCR indizi migliori. |

## Bonus: Verifica Visiva del Deskew

Se vuoi vedere il prima e dopo affiancati, aggiungi un rapido snippet Matplotlib:

```python
import matplotlib.pyplot as plt

def show_comparison(original, processed):
    fig, axs = plt.subplots(1, 2, figsize=(10, 4))
    axs[0].imshow(original.to_numpy(), cmap='gray')
    axs[0].set_title('Original')
    axs[0].axis('off')

    axs[1].imshow(processed.to_numpy(), cmap='gray')
    axs[1].set_title('Deskewed & Binarized')
    axs[1].axis('off')
    plt.show()

show_comparison(raw_image, preprocessed)
```

## Conclusione

Abbiamo coperto **come correggere l'inclinazione di un'immagine**, perché **preelaborare l'immagine per OCR** è essenziale, e come **estrarre testo da un'immagine** per infine **convertire la scansione in testo**. Il flusso di lavoro—carica → deskew → binarizza → riconosci—assicura che l'OCR veda una pagina pulita e dritta, il che si traduce in maggiore accuratezza e meno correzioni manuali.

Qual è il prossimo passo nel tuo percorso OCR? Prova a sperimentare con:

* Pacchetti linguistici diversi (`ocr.Language.FRENCH`, ecc.).  
* Aggiungere un passo di analisi del layout per rilevare colonne o tabelle.  
* Esportare i risultati OCR in PDF ricercabili usando una libreria PDF.

Sentiti libero di lasciare un commento se incontri un problema, o condividi le tue modifiche per gestire scansioni particolarmente ostinate. Buona programmazione, e che le tue immagini rimangano sempre perfettamente livellate!

## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come Usare AspOCR: Filtri OCR di Pre‑elaborazione Immagine per .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Estrai testo da immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Come Eseguire OCR su Immagine – Esegui OCR su Immagine nel Riconoscimento Immagini OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}