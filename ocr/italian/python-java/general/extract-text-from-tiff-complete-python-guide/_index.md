---
category: general
date: 2026-06-16
description: Estrai il testo da file TIFF usando OCR in Python. Impara come convertire
  i TIFF in testo passo dopo passo, gestendo documenti multipagina con facilità.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: it
og_description: Estrai il testo da file TIFF con OCR in Python. Segui questa guida
  per convertire i TIFF in testo, gestire scansioni multi‑pagina e ottenere risultati
  puliti.
og_title: Estrai testo da TIFF – Guida completa a Python
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: Estrai testo da TIFF – Guida completa a Python
url: /it/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai Testo da TIFF – Guida Completa Python

Hai mai avuto bisogno di **estrarre testo da TIFF** immagini ma non sapevi da dove cominciare? Non sei solo—molti sviluppatori incontrano questo ostacolo quando lavorano con archivi scansionati o documenti legacy. La buona notizia? Con poche righe di Python puoi **convertire TIFF in testo** in un attimo, anche quando il file contiene decine di pagine.

In questo tutorial percorreremo un esempio reale: caricare un TIFF multipagina, impostare la lingua OCR in francese e estrarre il testo riconosciuto da ogni pagina. Alla fine avrai uno script pronto all'uso, comprenderai perché ogni passaggio è importante e saprai come adattarlo ad altre lingue o formati immagine.

## Prerequisiti

- Python 3.8 o versioni successive installate.
- Il pacchetto `ocr` (o qualsiasi libreria OCR compatibile che offra una classe `OcrEngine`). Puoi installarlo con `pip install ocr-lib`—sostituisci con il nome reale del pacchetto che stai usando.
- Un file TIFF multipagina (ad es. `french-scans.tif`) che desideri elaborare.
- Familiarità di base con la scrittura di script Python.

Nessuna dipendenza pesante, nessun servizio esterno—solo puro Python e un motore OCR.

---

## Passo 1: Configura il Motore OCR per **Estrarre Testo da TIFF**

Prima di tutto—abbiamo bisogno di un'istanza del motore OCR e dobbiamo indicargli quale lingua usare. Nel nostro caso il materiale di origine è francese, quindi imposteremo la lingua di conseguenza.

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**Perché è importante:**  
L'impostazione della lingua migliora drasticamente l'accuratezza. Caratteri francesi come “é” o “ç” verrebbero interpretati erroneamente come simboli generici se il motore usa l'inglese di default. Selezionando esplicitamente il francese forniamo al motore la mappa dei caratteri corretta.

> **Suggerimento:** Se stai elaborando documenti in più lingue, puoi cambiare `engine.language` al volo prima di ogni chiamata a `recognize()`.

---

## Passo 2: Carica il TIFF Multipagina che Vuoi **Convertire da TIFF a Testo**

Un TIFF può contenere diversi frame—pensa a ogni frame come a una pagina separata. La libreria OCR astrae questo per noi, quindi basta indicare il file.

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**Avviso caso limite:**  
Se il percorso del file è errato o il TIFF è corrotto, il metodo `load_from_file` solleverà un'eccezione. Avvolgilo in un blocco `try/except` per il codice di produzione:

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## Passo 3: Esegui OCR sull'Intero Documento – Il Cuore di **Estrarre Testo da TIFF**

Ora lasciamo che il motore faccia la sua magia. La chiamata `recognize()` elabora tutte le pagine in un unico passaggio e restituisce un ricco oggetto risultato.

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**Cosa succede dietro le quinte?**  
Il motore itera su ogni frame, applica il pre‑processing (raddrizzamento, binarizzazione), esegue la rete neurale e aggrega l'output. Poiché abbiamo chiamato `recognize()` una sola volta, la libreria può condividere risorse tra le pagine, risultando più veloce rispetto a un ciclo manuale.

---

## Passo 4: Estrai il Testo Riconosciuto dal Risultato JSON – **Convertire TIFF in Testo** Pagina per Pagina

L'oggetto risultato può essere serializzato in JSON. All'interno di quel JSON troverai un array `pages`, ognuno contenente un campo `text`.

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

Ora abbiamo una lista Python pulita dove ogni elemento corrisponde all'output OCR di una pagina.

---

## Passo 5: Stampa o Salva il Testo per Ogni Pagina – L'Ultimo Pezzo di **Estrarre Testo da TIFF**

Facciamo un ciclo sulle pagine e mostriamo il testo estratto. Puoi anche scrivere ogni pagina in un file `.txt` separato se preferisci.

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### Output Atteso (esempio)

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

Se l'OCR ha avuto successo, vedrai un blocco pulito di frasi francesi per ogni pagina. Se noti caratteri confusi, ricontrolla l'impostazione della lingua o considera di aumentare la risoluzione dell'immagine prima dell'OCR.

---

## Gestire le Problematiche Comuni Quando **Converti TIFF in Testo**

| Problema | Perché accade | Soluzione rapida |
|----------|----------------|-------------------|
| **Array `pages` vuoto** | Il TIFF non è stato caricato correttamente o ha zero frame. | Verifica il percorso del file e assicurati che il TIFF non sia un PNG a pagina singola mascherato da TIFF. |
| **Caratteri spazzatura** | Mancata corrispondenza della lingua o bassa qualità dell'immagine. | Imposta la corretta `engine.language` e pre‑processa l'immagine (ad es. aumenta DPI). |
| **Esaurimento memoria su TIFF enormi** | Caricare tutte le pagine contemporaneamente consuma RAM. | Elabora a blocchi: carica un singolo frame, riconosci, poi scarta prima di passare al successivo. |
| **Errori Unicode durante la stampa** | La codifica della console non supporta i caratteri accentati. | Usa `print(page["text"].encode('utf-8').decode('utf-8'))` o configura il tuo terminale per UTF‑8. |

---

## Estendere lo Script: Da **Estrarre Testo da TIFF** a Elaborazione Batch

Ora che hai una solida base, considera i prossimi passi:

1. **Conversione batch** – Avvolgi l'intero flusso in una funzione `def ocr_tiff(path):` e itera su una directory di file TIFF.  
2. **Output su file** – Invece di stampare, scrivi il testo di ogni pagina in `page_{i}.txt` o concatena tutto in un unico documento.  
3. **Motori OCR alternativi** – Se ti serve maggiore accuratezza, sostituisci `ocr.OcrEngine()` con Tesseract (`pytesseract`) o Azure Cognitive Services—mantieni la stessa logica di “estrarre testo da TIFF”.  
4. **Post‑processing** – Esegui il controllo ortografico, il rilevamento della lingua o la pulizia con regex per sistemare l'output OCR grezzo.  

---

## Script Completo, Pronto all'Esecuzione

Di seguito il codice completo, pronto per il copia‑incolla. Include una gestione di base degli errori e il salvataggio opzionale del testo di ogni pagina in file separati.

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

Esegui questo script, punta `tiff_file` al tuo documento e osserva la console riempirsi di frasi francesi pulite. Se hai fornito `out_folder`, troverai anche una serie di file `page_#.txt` pronti per l'elaborazione successiva.

---

## Conclusione

Abbiamo appena **estratto testo da file TIFF** usando un flusso di lavoro OCR Python semplice, e ora sai come **convertire TIFF in testo** in modo affidabile. Dall'inizializzare il motore con la lingua corretta al ciclo su ogni risultato JSON della pagina, ogni passaggio è stato spiegato con il “perché” dietro di esso, così puoi adattare il modello ad altre lingue, formati immagine o lavori batch più grandi.

Cosa fare dopo? Prova a sostituire il backend OCR con Tesseract, sperimenta diversi pacchetti linguistici, o integra l'output in un database ricercabile. Il cielo è il limite quando puoi trasformare in modo affidabile le immagini scansionate in testo ricercabile.

Sentiti libero di lasciare un commento se incontri problemi o hai idee per ulteriori miglioramenti. Buon coding!

## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completo e funzionante con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai Testo da Immagine con Aspose OCR – Guida Passo‑Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Estrai Testo da Immagini Usando Operazione OCR su Cartelle](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Converti Immagine in Testo – Esegui OCR su Immagine da URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}