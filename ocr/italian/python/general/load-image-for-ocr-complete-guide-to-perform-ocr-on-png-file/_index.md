---
category: general
date: 2026-06-25
description: Carica l'immagine per OCR ed esegui OCR su PNG con un tutorial Python
  passo‑passo usando aocr. Impara il debugging, il logging e le migliori pratiche.
draft: false
keywords:
- load image for OCR
- perform OCR on PNG
- aocr logging setup
- OCR debugging Python
- image preprocessing OCR
language: it
og_description: Carica l'immagine per OCR ed esegui OCR su PNG usando aocr. Questa
  guida ti accompagna nella registrazione, nel caricamento dell'immagine e nel riconoscimento
  con il codice completo.
og_title: Carica immagine per OCR – Tutorial Python passo passo
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Load image for OCR and perform OCR on PNG with a step‑by‑step Python
    tutorial using aocr. Learn debugging, logging, and best practices.
  headline: Load Image for OCR – Complete Guide to Perform OCR on PNG Files
  type: TechArticle
- questions:
  - answer: Usually not. `aocr` handles PNG natively, but if the image is huge (>10
      MP) you might want to downscale first to speed up processing.
    question: Do I need to convert the PNG to another format?
  - answer: Rotate the log after each run or limit the level to `INFO` once you’re
      confident the pipeline works.
    question: What if the logger file grows too large?
  - answer: Absolutely. Just call `ocr_png` for each file; the function creates a
      fresh logger each time, keeping logs isolated.
    question: Can I process multiple images in a loop?
  - answer: Yes – `engine.result` also contains `boxes` and `confidences`. Explore
      the `aocr` docs for `result.boxes` if you need layout information.
    question: Is there a way to get bounding boxes instead of plain text?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: Carica immagine per OCR – Guida completa per eseguire OCR su file PNG
url: /it/python/general/load-image-for-ocr-complete-guide-to-perform-ocr-on-png-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Carica Immagine per OCR – Guida Completa per Eseguire OCR su File PNG

Hai mai dovuto **caricare un'immagine per OCR** ma non sapevi come impostare un debugging adeguato? Non sei solo. In molti progetti il primo ostacolo è inserire quel PNG nel motore mantenendo la possibilità di vedere cosa succede sotto il cofano.  

In questo tutorial ti guideremo passo passo attraverso tutto ciò che serve per **eseguire OCR su file PNG** usando la libreria `aocr` – dalla configurazione di un logger per output dettagliati fino al riconoscimento effettivo del testo. Alla fine avrai uno script riutilizzabile da inserire in qualsiasi progetto Python, e comprenderai perché ogni componente è importante.

## Cosa Imparerai

- Come inizializzare il logger di `aocr` così da tracciare ogni passaggio.
- Il codice esatto per **caricare un'immagine per OCR** con `aocr.OcrEngine`.
- Come configurare il livello di logging per ottenere informazioni di debug granulari.
- Eseguire il motore per **eseguire OCR su PNG** e recuperare i risultati.
- Suggerimenti per gestire problemi comuni come file mancanti o formati non supportati.

Non è necessaria alcuna esperienza pregressa con `aocr`; basta avere Python 3 installato e un’immagine da leggere. Iniziamo.

![carica immagine per OCR esempio](assets/load-image-ocr.png "Illustrazione del caricamento di un'immagine per OCR in Python")

## Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------|
| Python 3.8+ | `aocr` mira a interpreti moderni e utilizza type hints. |
| Libreria `aocr` installata (`pip install aocr`) | Senza il pacchetto le classi che usiamo non esisteranno. |
| Un'immagine PNG da leggere | Il tutorial si concentra su **eseguire OCR su PNG**, quindi è essenziale un PNG. |
| Permessi di scrittura su una directory di log | Il logger deve creare `ocr_debug.log`. |

Se ti manca qualcuno di questi, installalo subito – ci vuole solo un minuto.

```bash
pip install aocr
```

## Passo 1: Carica Immagine per OCR – Inizializza il Logging

Prima di toccare l’immagine, configura un logger. Il debug di OCR può diventare un incubo se non sai cosa sta facendo il motore. La classe `aocr.Logging` scrive tutto su file, e impostando il livello a `DEBUG` vedrai ogni chiamata interna.

```python
import aocr

# Create a logger instance
ocr_logger = aocr.Logging()
# Choose where the log file will live – adjust the path to suit your project
ocr_logger.set_output_file("logs/ocr_debug.log")

# DEBUG gives you the most detail; you can switch to INFO for less noise
ocr_logger.set_level(aocr.LoggingLevel.DEBUG)
```

**Perché è importante:**  
Se il motore OCR non riesce a trovare il file o il formato dell’immagine non è supportato, il logger catturerà lo stack trace dell’eccezione. Questo ti salva da infinite ipotesi più tardi.

## Passo 2: Esegui OCR su PNG – Configura il Motore

Ora che il logger è pronto, collegalo al motore OCR. Questo passaggio lega i due in modo che ogni azione del motore venga registrata.

```python
# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
# Plug the logger into the engine
ocr_engine.logging = ocr_logger
```

**Consiglio professionale:**  
Puoi riutilizzare la stessa istanza `ocr_engine` per più immagini. Ricordati solo di cancellare lo stato precedente se elabori un batch.

## Passo 3: Carica Immagine per OCR – Fornisci il File PNG

Ecco il cuore del tutorial: effettivamente **caricare un'immagine per OCR**. Il metodo `load_image` accetta un percorso file; internamente decodifica il PNG in una bitmap comprensibile al motore.

```python
# Path to the PNG you want to read
image_path = "samples/invoice.png"

# Load the image – this is where we “load image for OCR”
ocr_engine.load_image(image_path)
```

### Casi Limite da Tenere d'Occhio

1. **File Non Trovato** – Se il percorso è errato, `aocr` solleva un `FileNotFoundError`. Il logger lo segnalerà, ma puoi anche gestirlo:

   ```python
   try:
       ocr_engine.load_image(image_path)
   except FileNotFoundError as e:
       print(f"❌ Could not locate {image_path}: {e}")
       raise
   ```

2. **Formato Non Supportato** – Sebbene PNG sia ampiamente supportato, un file corrotto può generare `UnsupportedFormatError`. In tal caso, considera di convertire l’immagine in un PNG pulito con Pillow prima del caricamento.

## Passo 4: Esegui OCR su PNG – Avvia il Riconoscimento

Ora che l’immagine è in memoria, puoi finalmente **eseguire OCR su PNG**. Il metodo `recognize` avvia le pipeline del motore (pre‑processing, segmentazione, classificazione) e popola l’oggetto risultato.

```python
# Execute the OCR process
ocr_engine.recognize()
```

Dopo questa chiamata, il motore contiene il testo riconosciuto. Puoi accedervi tramite l’attributo `result`:

```python
# Retrieve the plain text output
recognized_text = ocr_engine.result.text
print("📝 OCR Result:")
print(recognized_text)
```

**Perché controllare il risultato:**  
Alcuni motori OCR restituiscono stringhe vuote per immagini a basso contrasto. Vedere subito il risultato ti permette di decidere se è necessario pre‑processare (ad esempio aumentare il contrasto) prima di rieseguire.

## Passo 5: Raccogli Tutto – Una Funzione Riutilizzabile

Unire i pezzi in un’unica funzione rende semplice chiamarla da altri script o da un servizio web. Questo dimostra anche come **caricare un'immagine per OCR** e **eseguire OCR su PNG** in un unico pacchetto ordinato.

```python
def ocr_png(image_path: str, log_dir: str = "logs") -> str:
    """
    Load a PNG image, run aocr OCR, and return the extracted text.
    
    Parameters
    ----------
    image_path : str
        Full path to the PNG file.
    log_dir : str, optional
        Directory where the debug log will be written.
    
    Returns
    -------
    str
        The plain‑text OCR result.
    """
    import os
    import aocr

    # Ensure the log directory exists
    os.makedirs(log_dir, exist_ok=True)

    # ---------- Logging ----------
    logger = aocr.Logging()
    logger.set_output_file(os.path.join(log_dir, "ocr_debug.log"))
    logger.set_level(aocr.LoggingLevel.DEBUG)

    # ---------- Engine ----------
    engine = aocr.OcrEngine()
    engine.logging = logger

    # ---------- Load Image ----------
    try:
        engine.load_image(image_path)
    except Exception as exc:
        logger.error(f"Failed to load image {image_path}: {exc}")
        raise

    # ---------- Recognize ----------
    engine.recognize()
    return engine.result.text

# Example usage
if __name__ == "__main__":
    txt = ocr_png("samples/invoice.png")
    print("\n--- Extracted Text ---\n")
    print(txt)
```

Eseguendo lo script otterrai un dettagliato `ocr_debug.log` nella cartella `logs`, poi stamperà il testo riconosciuto sulla console. Hai ora un’utilità **eseguire OCR su PNG** che puoi importare altrove.

## Domande Frequenti & Trappole

- **Devo convertire il PNG in un altro formato?**  
  Di solito no. `aocr` gestisce PNG nativamente, ma se l’immagine è molto grande (>10 MP) potresti ridimensionarla prima per velocizzare l’elaborazione.

- **E se il file di log diventa troppo grande?**  
  Ruota il log dopo ogni esecuzione o limita il livello a `INFO` una volta che la pipeline funziona correttamente.

- **Posso elaborare più immagini in un ciclo?**  
  Assolutamente. Basta chiamare `ocr_png` per ogni file; la funzione crea un nuovo logger ogni volta, mantenendo i log isolati.

- **C’è un modo per ottenere le bounding box invece del solo testo?**  
  Sì – `engine.result` contiene anche `boxes` e `confidences`. Consulta la documentazione di `aocr` per `result.boxes` se ti servono informazioni di layout.

## Conclusione

Ora sai come **caricare un'immagine per OCR** e **eseguire OCR su PNG** usando la libreria `aocr`, con una configurazione di logging robusta che rende il debug indolore. La funzione di esempio incapsula l’intero workflow, così puoi inserirla in qualsiasi progetto e cominciare subito a estrarre testo.

Prossimi passi? Prova a fornire al motore diversi tipi di immagine (JPEG, TIFF) per vedere come varia l’accuratezza, oppure sperimenta tecniche di pre‑processing come la sogliatura per migliorare i risultati su scansioni rumorose. E se sei curioso di estrarre dati strutturati (tabelle, moduli), dai un’occhiata alle sezioni `aocr` sull’analisi del layout – si integrano perfettamente con quanto hai appena costruito.

Buon coding, e che le tue pipeline OCR siano sempre prive di errori!


## Cosa Dovresti Imparare Dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}