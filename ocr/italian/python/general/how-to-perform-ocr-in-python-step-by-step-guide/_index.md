---
category: general
date: 2026-08-15
description: Come eseguire OCR in Python rapidamente. Impara a estrarre testo da PNG,
  caricare l'immagine per OCR e migliorare l'accuratezza dell'OCR con il post‑processing
  AI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from PNG
- improve OCR accuracy
- load image for OCR
language: it
lastmod: 2026-08-15
og_description: Come eseguire l'OCR in Python è spiegato nella prima frase. Segui
  questo tutorial per estrarre testo da immagini PNG, caricare l'immagine per l'OCR
  e aumentare la precisione con il post‑processing AI.
og_image_alt: How to perform OCR example output displayed in a Python console
og_title: Come eseguire l'OCR in Python – guida completa per sviluppatori
schemas:
- author: Aspose
  dateModified: '2026-08-15'
  description: How to perform OCR in Python quickly. Learn to extract text from PNG,
    load image for OCR, and improve OCR accuracy with AI post‑processing.
  headline: How to perform OCR in Python – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Python
- AI post‑processing
title: Come eseguire l'OCR in Python – guida passo passo
url: /it/python/general/how-to-perform-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR in Python – guida passo‑passo

Eseguire OCR in Python è una necessità comune quando devi digitalizzare documenti o ricevute scannerizzate. In questo tutorial imparerai a estrarre testo da file PNG, caricare l’immagine per OCR e migliorare l’accuratezza OCR applicando un post‑processore guidato dall’AI.

Vedrai un esempio completo e eseguibile che inizia con il caricamento di un’immagine, esegue un motore OCR di base e termina con testo migliorato dall’AI. Non è necessaria alcuna documentazione esterna—basta seguire i passaggi, copiare il codice e farlo girare sulla tua macchina.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* Python 3.9 o versioni successive installato.
* Il pacchetto `ocr-engine` (un segnaposto per qualsiasi libreria OCR come Aspose.OCR, Tesseract‑wrapper, ecc.).
* Una libreria di supporto AI che fornisca il metodo `run_postprocessor` (ad esempio, un wrapper leggero per OpenAI).
* Un’immagine PNG di esempio (ad es., `sample_invoice.png`) posizionata in una directory nota.

Puoi installare i pacchetti richiesti con:

```bash
pip install ocr-engine ai-helper
```

> **Suggerimento professionale:** Se preferisci un motore OCR open‑source, sostituisci `ocr-engine` con `pytesseract` e adatta il codice di conseguenza. Il flusso complessivo rimane lo stesso.

## Passo 1: Creare un'istanza del motore OCR

Il primo compito è istanziare il motore OCR. Questo oggetto gestisce l’analisi a basso livello dell’immagine e il riconoscimento dei caratteri.

```python
from ocr_engine import OcrEngine   # Replace with your actual OCR library import

# Initialize the OCR engine
engine = OcrEngine()
```

Creare il motore una sola volta e riutilizzarlo su più immagini riduce il sovraccarico di inizializzazione e garantisce impostazioni coerenti.

## Passo 2: Caricare l'immagine da riconoscere

Caricare il formato di file corretto è essenziale. Qui dimostriamo il caricamento di un’immagine PNG, formato tipico per fatture e ricevute scannerizzate.

```python
import os

# Define the path to the PNG file you want to process
image_path = os.path.join("YOUR_DIRECTORY", "sample_invoice.png")

# Load the image into the OCR engine
engine.load_image(image_path)
```

Il metodo `load_image` legge il file in memoria e lo prepara per il riconoscimento. Se il file non viene trovato, il motore solleva un’eccezione informativa, così puoi gestire i file mancanti in modo elegante.

## Passo 3: Eseguire l'operazione OCR di base

Con l’immagine caricata, invoca il metodo `recognize` del motore OCR. Questo restituisce un oggetto risultato contenente il testo grezzo.

```python
# Run the OCR process
plain_result = engine.recognize()

# Display the raw OCR output
print("Raw OCR:", plain_result.text)
```

L’output tipicamente include interruzioni di riga e occasionali errori di riconoscimento, specialmente con scansioni a bassa risoluzione. A questo punto hai **estratto con successo testo da PNG** usando la pipeline OCR di base.

### Output grezzo previsto (esempio)

```
Raw OCR: Invoice #12345
Date: 2023/07/15
Total: $1,234.56
```

## Passo 4: Migliorare il testo OCR usando un post‑processore AI

L’OCR di base può incontrare difficoltà con sfondi rumorosi, caratteri insoliti o note scritte a mano. Un post‑processore AI può pulire la stringa grezza, correggere l’ortografia e persino riformattare i dati.

```python
from ai_helper import AIHelper   # Replace with your actual AI helper import

# Initialize the AI helper (assumes you have set up API keys elsewhere)
ai = AIHelper()

# Run the AI‑based post‑processor on the raw OCR text
enhanced_text = ai.run_postprocessor(plain_result.text)

# Show the AI‑enhanced result
print("AI‑enhanced OCR:", enhanced_text)
```

Il modello AI analizza la stringa grezza, corregge errori comuni di OCR (ad es., “1,234.56” → “1,234.56”) e può anche inferire campi mancanti.

### Output migliorato previsto (esempio)

```
AI‑enhanced OCR: Invoice #12345
Date: 2023‑07‑15
Total: $1,234.56
```

Applicando questo passaggio **migliori l'accuratezza OCR** senza modificare i parametri a basso livello del motore.

## Script completo eseguibile

Unendo tutti i pezzi ottieni uno script unico che puoi eseguire direttamente:

```python
import os
from ocr_engine import OcrEngine          # OCR library
from ai_helper import AIHelper             # AI post‑processing library

def main():
    # 1️⃣ Create OCR engine
    engine = OcrEngine()

    # 2️⃣ Load PNG image
    image_path = os.path.join("YOUR_DIRECTORY", "sample_invoice.png")
    engine.load_image(image_path)

    # 3️⃣ Basic OCR
    plain_result = engine.recognize()
    print("Raw OCR:", plain_result.text)

    # 4️⃣ AI post‑processing
    ai = AIHelper()
    enhanced_text = ai.run_postprocessor(plain_result.text)
    print("AI‑enhanced OCR:", enhanced_text)

if __name__ == "__main__":
    main()
```

Salva il file come `ocr_demo.py` e esegui:

```bash
python ocr_demo.py
```

Dovresti vedere sia i risultati OCR grezzi sia quelli migliorati dall’AI stampati sulla console.

## Domande comuni e casi limite

| Domanda | Risposta |
|----------|--------|
| **E se l'immagine non è una PNG?** | La maggior parte delle librerie OCR accetta JPEG, BMP o TIFF. Cambia l’estensione del file in `image_path` e verifica che il motore supporti il formato. |
| **Come gestire PDF multi‑pagina?** | Converti prima ogni pagina in PNG (o un altro formato raster), poi itera sulle pagine e applica lo stesso script. |
| **Posso elaborare in batch molte immagini?** | Sì—avvolgi la logica in un ciclo `for` che itera su una cartella di file PNG. Riutilizzare la stessa istanza `engine` migliora le prestazioni. |
| **E se il helper AI genera un errore?** | Cattura le eccezioni intorno a `run_postprocessor` e ricorri al testo OCR grezzo, registrando il fallimento per una revisione successiva. |

## Conclusione

In questa guida hai imparato **come eseguire OCR in Python**, dal caricamento di un’immagine PNG all’estrazione del testo e infine **migliorare l'accuratezza OCR** con un post‑processore AI. Lo script completo dimostra il flusso end‑to‑end, così da poterlo integrare subito in pipeline di automazione più ampie.

Successivamente, considera di approfondire:

* **estrarre testo da PNG** in modalità batch per grandi archivi di documenti.
* Tecniche avanzate di **caricamento immagine per OCR** come pre‑elaborazione dell’immagine (raddrizzamento, riduzione del rumore) per aumentare l'accuratezza di base.
* Modelli AI personalizzati adattati a layout di documenti specifici, che possono ulteriormente **migliorare l'accuratezza OCR** oltre il post‑processing generico.

Buona programmazione e goditi la potenza di un OCR affidabile combinato con l'AI!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Converti immagine in testo: estrai testo da immagine usando Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Estrai testo da immagine con Aspose OCR – Guida passo‑passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Estrai testo da immagine – Ottimizzazione OCR con Aspose.OCR per .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}