---
category: general
date: 2026-06-06
description: Come eseguire l'OCR di un PDF con Python, estrarre testo da PDF, convertire
  il testo di PDF scansionati e cambiare la lingua dell'OCR in poche righe di codice.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert scanned pdf text
- perform ocr on pdf
- change ocr language
language: it
og_description: 'Come fare OCR di PDF con Python: una guida pratica che ti mostra
  come estrarre testo da PDF, convertire il testo di PDF scansionati e cambiare la
  lingua dell''OCR senza sforzo.'
og_title: Come fare OCR di PDF in Python – Tutorial completo di programmazione
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Python, extract text from PDF, convert scanned
    PDF text, and change OCR language in just a few lines of code.
  headline: How to OCR PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Come fare OCR di PDF in Python – Guida completa passo passo
url: /it/python-java/general/how-to-ocr-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come fare OCR su PDF in Python – Guida completa passo‑passo

Ti sei mai chiesto **come fare OCR su PDF** senza pagare costosi strumenti SaaS? Non sei l'unico. Che tu stia digitalizzando vecchi libri, estraendo dati da fatture, o semplicemente abbia bisogno di testo ricercabile da un report scansionato, padroneggiare l'OCR di PDF in Python può farti risparmiare ore di copia manuale.

In questo tutorial percorreremo un esempio conciso e funzionante che **estrae testo da PDF**, ti mostrerà come **convertire il testo di PDF scansionati** in stringhe modificabili, e dimostrerà anche come **cambiare la lingua dell'OCR** se il tuo documento non è in inglese. Alla fine avrai uno snippet riutilizzabile da inserire in qualsiasi progetto.

## Prerequisiti & Configurazione

Prima di immergerci, assicurati di avere:

- Python 3.8+ installato (il codice funziona su 3.9, 3.10 e versioni successive)
- Il pacchetto `ocr` che fornisce la classe `OcrEngine` (puoi installarlo via `pip install ocr-lib` – sostituisci con il nome reale del pacchetto che usi)
- Un file PDF da elaborare; per la demo useremo `high_res_book.pdf` collocato in una cartella chiamata `YOUR_DIRECTORY`

Se utilizzi un ambiente virtuale (altamente consigliato), attivalo prima:

```bash
python -m venv .venv
source .venv/bin/activate   # on Windows: .venv\Scripts\activate
pip install ocr-lib
```

> **Consiglio professionale:** Tieni i tuoi file PDF in una directory dedicata `data/` per evitare problemi legati ai percorsi in seguito.

## Passo 1: Creare un'Istanza del Motore OCR (Come fare OCR su PDF – Inizializzazione)

La prima cosa da fare quando vuoi **eseguire OCR su PDF** è istanziare il motore. Pensa al motore come al cervello che leggerà ogni pagina, interpreterà i glifi e ti restituirà testo semplice.

```python
# Step 1: Create an OCR engine instance
engine = OcrEngine()
```

Perché è importante: senza un motore non hai contesto per le impostazioni della lingua, le opzioni di rendering o la gestione del PDF. L'oggetto `OcrEngine` contiene tutti questi valori predefiniti e ti permette di modificarli in seguito.

## Passo 2: Impostare la Lingua di Riconoscimento (Cambia Lingua OCR)

La maggior parte delle librerie OCR usa l'inglese come predefinito, ma cosa succede se il tuo documento è in francese, tedesco o addirittura giapponese? Cambiare lingua è semplice come chiamare `set_recognition_language`. Questo soddisfa il requisito **cambia lingua OCR** e garantisce una maggiore accuratezza.

```python
# Step 2: Set the recognition language to English (or any supported language)
engine.set_recognition_language(ocr.Language.ENGLISH)   # swap ENGLISH for FRANCAIS, etc.
```

> **Perché potresti averne bisogno:** Un archivio multilingue contiene spesso pagine con lingue miste. Cambiare lingua al volo evita il riconoscimento errato di caratteri come “ß” o “ñ”.

## Passo 3: Configurare le Opzioni di Rendering del PDF (Convertire Efficacemente il Testo di PDF Scansionati)

Quando si lavora con PDF scansionati, la risoluzione e la modalità colore influenzano drasticamente la qualità dell'OCR. Renderizzare a 300 DPI in scala di grigi è un buon compromesso per la maggior parte dei documenti—abbastanza alto da catturare i dettagli, ma sufficientemente basso da mantenere ragionevole l'uso della memoria.

```python
# Step 3: Configure PDF rendering options (300 DPI, grayscale)
engine.pdf_render_options() \
      .set_dpi(300) \
      .set_color_mode("grayscale")
```

Le chiamate concatenate possono sembrare eleganti, ma sono semplicemente un'API fluida che restituisce lo stesso oggetto opzioni ogni volta. Se ti serve il colore (ad esempio per diagrammi a colori), sostituisci `"grayscale"` con `"color"`.

## Passo 4: Riconoscere il PDF e Ottenere il Testo della Prima Pagina (Estrarre Testo da PDF)

Ora arriva il cuore di **come fare OCR su PDF**: fornire al motore il percorso del file e prelevare il testo riconosciuto. Il metodo restituisce una lista di risultati per pagina; ogni risultato contiene un attributo `text`.

```python
# Step 4: Recognize the PDF and print the text of the first page
results = engine.recognize_pdf("YOUR_DIRECTORY/high_res_book.pdf")
print(results[0].text)   # Text from the first page
```

Se ti serve l'intero documento, itera su `results`:

```python
for i, page in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(page.text)
```

### E se il PDF è Criptato?

Alcuni PDF sono protetti da password. In tal caso puoi passare la password a `recognize_pdf`:

```python
results = engine.recognize_pdf(
    "YOUR_DIRECTORY/secure_doc.pdf",
    password="mySecret123"
)
```

Il motore decritterà al volo prima di eseguire l'OCR—nessun passaggio aggiuntivo necessario.

## Passo 5: Post‑Processing del Testo Estratto (Rifinire l'Estrazione del Testo da PDF)

L'output grezzo dell'OCR contiene spesso interruzioni di riga, spazi extra o occasionali caratteri riconosciuti in modo errato. Una rapida routine di pulizia rende la stringa estratta pronta per l'elaborazione successiva (indicizzazione, archiviazione in database, ecc.).

```python
import re

def clean_ocr_text(raw: str) -> str:
    # Remove multiple spaces and line breaks
    text = re.sub(r'\s+', ' ', raw)
    # Strip leading/trailing whitespace
    return text.strip()

clean_text = clean_ocr_text(results[0].text)
print(clean_text)
```

Ora puoi **estrarre testo da PDF** e inviarlo a qualsiasi pipeline NLP, motore di ricerca o semplice operazione `open(...).write()`.

## Bonus: Elaborazione Batch di Più PDF (Scalare l'Esecuzione OCR su PDF)

Se hai una cartella piena di PDF scansionati, avvolgi la logica in un ciclo:

```python
import pathlib

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    print(f"Processing {pdf_path.name} …")
    pages = engine.recognize_pdf(str(pdf_path))
    full_text = "\n".join(page.text for page in pages)
    cleaned = clean_ocr_text(full_text)

    # Save the extracted text alongside the PDF
    txt_path = pdf_path.with_suffix(".txt")
    txt_path.write_text(cleaned, encoding="utf-8")
    print(f"Saved extracted text to {txt_path.name}")
```

Questo snippet mostra come **eseguire OCR su PDF** in blocco, una necessità comune nei progetti di digitalizzazione.

## Output Atteso

Eseguire l'esempio a pagina singola (Passo 4) dovrebbe stampare qualcosa del genere:

```
In the beginning God created the heavens and the earth. Now the earth was formless …
```

Se hai elaborato un libro a più pagine, la console mostrerà il testo pulito di ogni pagina, e lo script batch lascerà un file `.txt` accanto a ciascun PDF.

## Problemi Comuni & Come Evitarli

| Problema | Sintomi | Soluzione |
|----------|----------|-----------|
| PDF sorgente a bassa risoluzione | Caratteri illeggibili, parole mancanti | Aumenta DPI (`set_dpi(400)` o superiore) |
| Lingua impostata errata | Molti simboli sconosciuti, specialmente caratteri accentati | Usa `engine.set_recognition_language(ocr.Language.FRENCH)` o l'enumerazione appropriata |
| PDF grande che causa errore di memoria | `MemoryError` o crash dopo alcune pagine | Processa le pagine a blocchi (`engine.recognize_pdf(..., max_pages=10)`) |
| Font mancanti nel PDF | Output vuoto per alcune pagine | Assicurati che il PDF contenga effettivamente immagini raster; alcuni PDF sono solo vettoriali e richiedono una gestione diversa |

## Illustrazione

Di seguito una rapida visuale del flusso di lavoro. Il testo alternativo è deliberatamente SEO‑friendly.

![diagramma del flusso di lavoro per OCR di PDF che mostra l'inizializzazione del motore, impostazione della lingua, opzioni di rendering, riconoscimento e estrazione del testo](/images/ocr-workflow.png)

*Il diagramma non è necessario per l'esecuzione del codice, ma aiuta gli apprendisti visivi a vedere dove si inserisce ogni passo.*

## Conclusione

Abbiamo coperto **come fare OCR su PDF** in Python dall'inizio alla fine: creazione di un motore OCR, **cambio della lingua OCR**, configurazione del rendering per **convertire il testo di PDF scansionati**, e infine **estrazione del testo da PDF** per usi successivi. L'esempio completo, eseguibile, è pronto per essere inserito in qualsiasi progetto, e lo script batch opzionale mostra come scalare la soluzione.

Prossimamente potresti voler esplorare:

- Aggiungere **esecuzione OCR su PDF** per archivi multilingue iterando su una lista di lingue.
- Integrare il testo estratto con Elasticsearch per la ricerca full‑text.
- Usare l'OCR per creare PDF ricercabili incorporando il livello di testo nel file originale (molte librerie espongono un metodo `save_as_searchable_pdf`).

Sentiti libero di sperimentare, modificare le impostazioni DPI, o passare a un backend OCR diverso. I fondamenti rimangono gli stessi, e ora hai una solida base su cui costruire.

Buon coding, e che i tuoi documenti scansionati diventino finalmente ricercabili!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}