---
category: general
date: 2026-03-18
description: Esegui OCR sull'immagine per estrarre rapidamente il testo dall'immagine.
  Scopri come caricare l'immagine per l'OCR, creare il motore OCR e migliorare la
  precisione dell'OCR con le opzioni linguistiche.
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: it
og_description: Esegui l'OCR su un'immagine con questa guida dettagliata. Impara a
  caricare l'immagine per l'OCR, creare il motore OCR e migliorare l'accuratezza dell'OCR
  per un'estrazione affidabile del testo.
og_title: Esegui OCR su Immagine – Tutorial Completo di Programmazione
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Esegui OCR su immagine – Guida passo‑passo
url: /it/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine – Tutorial Completo di Programmazione

Ti è mai capitato di **eseguire OCR su un'immagine** senza sapere quale libreria scegliere o come ottenere risultati affidabili? Non sei solo. In questa guida percorreremo tutto ciò che ti serve per **estrarre testo da un'immagine**, dal caricamento della foto alla regolazione delle opzioni linguistiche, così potrai **migliorare la precisione dell'OCR** ad ogni passo.

Copriamo come **caricare l'immagine per l'OCR**, come **creare il motore OCR**, e perché ogni impostazione è importante. Alla fine avrai uno script pronto all'uso che stampa il testo riconosciuto e comprenderai il “perché” dietro ogni riga—niente scorciatoie tipo “vedi la documentazione”. Immergiamoci.

## Cosa Ti Serve

- Python 3.8+ (il codice usa f‑strings e type hints)
- Il pacchetto ipotetico `ocr_lib` – installalo con `pip install ocr_lib`
- Un file immagine contenente testo stampato chiaro (ad es. `lab_report.png`)
- Un editor di testo o IDE di base (VS Code, PyCharm, quello che preferisci)

Se li hai già, ottimo—sei pronto. Altrimenti, scarica Python da python.org e esegui il comando pip; ci vuole solo un minuto.

![esempio di esecuzione OCR su immagine](/images/ocr-example.png)

*Testo alternativo: esecuzione OCR su immagine – output di esempio che mostra il testo estratto.*

## Passo 1: Crea il Motore OCR – Come **create OCR engine** in Python

Prima che possa avvenire qualsiasi riconoscimento, la libreria ha bisogno di un oggetto motore che contenga configurazione e stato di runtime. Pensa al motore come al cervello dell'operazione.

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**Perché è importante:** Istanziare il motore subito ti permette di aggiungere opzioni linguistiche in seguito e inoltre memorizza i modelli interni per chiamate successive più rapide.

## Passo 2: Carica l'Immagine per l'OCR – Il modo corretto di **load image for OCR**

Ora che abbiamo un motore, dobbiamo dargli qualcosa da leggere. Il metodo `setImageFromFile` accetta un percorso di file; il percorso può essere assoluto o relativo alla directory di lavoro dello script.

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**Consiglio professionale:** Usa un percorso assoluto o `os.path.join` per evitare sorprese del tipo “file non trovato” quando lo script viene eseguito da una cartella diversa.

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## Passo 3: Migliora la Precisione dell'OCR – Regolare le **language options** per **improve OCR accuracy**

L'OCR di base funziona, ma i vocabolari specifici di dominio (come il gergo di laboratorio) spesso lo ostacolano. Fornendo un dizionario personalizzato e una blacklist riduci i riconoscimenti errati, ad esempio confondere “0” con “O”.

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**Perché aiuta:** Il dizionario indica al modello OCR che “HPLC” è un token valido, impedendogli di spezzare la parola in nonsense. La blacklist dice al modello di trattare i simboli ambigui come rumore, migliorando direttamente **la precisione dell'OCR**.

## Passo 4: Esegui OCR su Immagine – La chiamata principale **perform OCR on image**

Con il motore pronto e l'immagine collegata, è il momento di riconoscere effettivamente il testo. Questo passo restituisce un oggetto `OcrResult` che puoi interrogare per testo grezzo, punteggi di confidenza o bounding box.

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

Se l'immagine è sfocata, vedrai numeri di confidenza più bassi nel risultato. È un segnale per pre‑processare l'immagine (ad es., aumentare il contrasto) prima di passarla al motore.

## Passo 5: Estrarre Testo da Immagine – Ottenere la stringa finale

Infine, chiediamo a `OcrResult` la sua rappresentazione testuale. Il metodo `getText()` restituisce una stringa plain‑text pronta per ulteriori elaborazioni (salvare su file, inserire in un database, ecc.).

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**Output previsto:** Supponendo che `lab_report.png` contenga una semplice tabella, potresti vedere qualcosa del tipo:

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

Questo è il passaggio **extract text from image** completato.

## Esempio Completo Funzionante – Metti Tutto Insieme

Di seguito trovi uno script unico che unisce i pezzi delle sezioni precedenti. Puoi copiarlo in `run_ocr.py` ed eseguire `python run_ocr.py`.

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### Checklist di verifica rapida

| ✅ | Elemento |
|---|------|
| ✔️ | Il motore è creato (`create OCR engine`) |
| ✔️ | L'immagine è caricata (`load image for OCR`) |
| ✔️ | Le opzioni linguistiche sono impostate (`improve OCR accuracy`) |
| ✔️ | L'OCR è eseguito (`perform OCR on image`) |
| ✔️ | Il testo è estratto (`extract text from image`) |

Esegui lo script e osserva la console. Se vedi il blocco “OCR Output” con il contenuto del tuo report, hai **eseguito OCR su immagine** con successo.

## Problemi comuni e come evitarli

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| **Input sfocato** | Il modello OCR non riesce a distinguere i caratteri | Pre‑processare con OpenCV: `cv2.GaussianBlur` o aumentare DPI |
| **Lingua errata** | La lingua predefinita potrebbe essere impostata su qualcosa di diverso dall'inglese | Chiamare `engine.setLanguage("eng")` prima di `recognize()` |
| **Termini del dizionario mancanti** | Le parole specifiche del dominio diventano illeggibili | Aggiungerle tramite `setDictionary` come mostrato al Passo 3 |
| **I caratteri nella blacklist causano** |  |  |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}