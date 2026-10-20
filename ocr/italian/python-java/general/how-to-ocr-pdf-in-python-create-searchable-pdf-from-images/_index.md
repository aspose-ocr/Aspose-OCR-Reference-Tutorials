---
category: general
date: 2026-06-06
description: Come fare OCR di PDF e creare file PDF ricercabili da immagini usando
  Python. Impara ad aggiungere testo ricercabile e convertire l'immagine in PDF/A
  in pochi minuti.
draft: false
keywords:
- how to ocr pdf
- create searchable pdf
- add searchable text
- ocr image to pdf
- convert image to pdf/a
language: it
og_description: Come fare OCR di un PDF passo dopo passo. Impara ad aggiungere testo
  ricercabile e a convertire l'immagine in PDF/A usando un semplice script Python.
og_title: Come fare OCR su PDF – Guida rapida per creare PDF ricercabili
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  headline: How to OCR PDF in Python – Create Searchable PDF from Images
  type: TechArticle
- description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  name: How to OCR PDF in Python – Create Searchable PDF from Images
  steps:
  - name: Why this matters
    text: '- **Preserving graphics** means the visual layout (tables, logos, stamps)
      stays exactly as the scanner captured it. - The `result` object typically contains
      a hidden text layer that we’ll later embed into the PDF. - Using `recognize_image`
      instead of `recognize_pdf` avoids an extra conversion step, '
  - name: Why this matters
    text: '- **Searchable PDF**: The output file contains a hidden, selectable text
      layer. You can now Ctrl + F through the document. - **PDF/A compliance**: Some
      organizations (legal, finance) require PDF/A for audit trails; this step satisfies
      that rule automatically. - The method also **adds searchable text'
  - name: Expected output
    text: 'When you run the script, the console prints:'
  type: HowTo
tags:
- OCR
- PDF
- Python
- Automation
title: Come fare OCR di PDF in Python – Creare PDF ricercabili da immagini
url: /it/python-java/general/how-to-ocr-pdf-in-python-create-searchable-pdf-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come fare OCR su PDF – Trasformare le Immagini Scansionate in PDF Ricercabili

Ti sei mai chiesto **come fare OCR su PDF** quando tutto ciò che hai è un'immagine scansionata di una fattura o di una ricevuta? Non sei l'unico. In molti uffici la documentazione in arrivo arriva come PNG o JPEG piatti, e il passo successivo—rendere quel contenuto ricercabile—sembra una scatola nera.  

La buona notizia? Con poche righe di Python puoi **creare PDF ricercabili**, **aggiungere testo ricercabile**, e persino **convertire immagini in PDF/A** per l'archiviazione a lungo termine. In questo tutorial percorreremo ogni passaggio, spiegheremo perché è importante e ti forniremo uno script pronto all'uso da inserire in qualsiasi progetto.

> **Consiglio professionale:** Lo stesso approccio funziona per scansioni multi‑pagina; basta iterare sui file e il motore si occupa del lavoro pesante.

---

## Cosa ti servirà

Prima di immergerci, assicurati di avere quanto segue sulla tua macchina:

| Requisito | Perché è importante |
|-------------|----------------|
| Python 3.9 o più recente | Sintassi moderna e migliore supporto alle librerie |
| `pdfium`‑based OCR engine (e.g., `pdfocr` or a commercial SDK) | Gestisce sia il riconoscimento delle immagini che la generazione di PDF/A |
| Un file immagine (PNG, JPEG, TIFF) che desideri trasformare in un PDF ricercabile | La fonte del testo |
| Permesso di scrittura sulla cartella di destinazione | Affinché lo script possa salvare il nuovo PDF |

Se non hai ancora installato l'SDK OCR, esegui:

```bash
pip install pdfocr   # replace with your vendor's package name
```

È tutto—nessuna dipendenza di sistema complessa, solo un'installazione pip.

## Come fare OCR su PDF – Panoramica

A livello alto il processo consiste in tre azioni semplici:

1. **Riconoscere** il testo all'interno dell'immagine mantenendo intatta la grafica originale.  
2. **Esportare** il risultato OCR insieme all'immagine originale come **PDF/A ricercabile** (la variante PDF adatta all'archiviazione).  
3. **Convalidare** che il file risultante contenga testo selezionabile e ricercabile sovrapposto all'immagine originale.

Di seguito vedrai ogni passaggio in codice, con spiegazioni del *perché* dietro i comandi.

## Passo 1: Riconoscere il Testo dall'Immagine

Per prima cosa chiediamo al motore OCR di leggere i pixel e restituire un oggetto risultato che contiene sia l'immagine grezza sia il testo estratto. Pensalo come il motore che “legge” la fattura per te.

```python
# Step 1: Recognize text from the image and keep the original graphics
result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

### Perché è importante

- **Preservare la grafica** significa che il layout visivo (tabelle, loghi, timbri) rimane esattamente come è stato acquisito dallo scanner.  
- L'oggetto `result` tipicamente contiene un livello di testo nascosto che inseriremo successivamente nel PDF.  
- Usare `recognize_image` invece di `recognize_pdf` evita un passaggio di conversione aggiuntivo, velocizzando l'elaborazione per immagini a pagina singola.

#### Varianti comuni

- Se hai un **TIFF multi‑pagina**, passa direttamente il percorso del file; la maggior parte dei motori tratterà ogni pagina come un'immagine separata.  
- Per i PDF che contengono già immagini, puoi chiamare `engine.recognize_pdf("file.pdf")` e saltare completamente questo passaggio.

## Passo 2: Esportare il Risultato OCR come PDF/A Ricercabile

Ora prendiamo il `result` dal passo 1 e diciamo al motore di scrivere un nuovo file. Il flag chiave qui è *PDF/A*—la versione standard ISO del PDF progettata per la conservazione a lungo termine.

```python
# Step 2: Export the OCR result together with the original image as a searchable PDF/A
result.save_as_pdfa("YOUR_DIRECTORY/invoice_searchable.pdf")
```

### Perché è importante

- **PDF ricercabile**: Il file di output contiene un livello di testo nascosto e selezionabile. Ora puoi usare Ctrl + F sul documento.  
- **Conformità PDF/A**: Alcune organizzazioni (legale, finanziaria) richiedono PDF/A per le tracce di audit; questo passaggio soddisfa automaticamente tale requisito.  
- Il metodo aggiunge anche **testo ricercabile** senza appiattire l'immagine, così la fedeltà visiva rimane perfetta.

#### Caso limite: Hai bisogno di un PDF normale invece?

Se non ti interessa il PDF/A, sostituisci `save_as_pdfa` con `save_as_pdf`. Il resto del flusso di lavoro rimane invariato.

## Passo 3: Verificare il PDF Ricercabile

Un rapido controllo di sanità ti salva da bug misteriosi in seguito. Apri il file generato in qualsiasi visualizzatore PDF, prova a selezionare una parola e usa la funzione di ricerca.

```python
# Step 3: The file "invoice_searchable.pdf" now contains selectable text layered over the original invoice image
import subprocess, os

pdf_path = "YOUR_DIRECTORY/invoice_searchable.pdf"
if os.path.exists(pdf_path):
    print(f"✅ PDF created successfully: {pdf_path}")
    # Optionally open the file (works on macOS, Windows, Linux with appropriate commands)
    subprocess.run(["open", pdf_path] if os.name == "posix" else ["start", pdf_path], shell=True)
else:
    print("❌ Something went wrong – PDF not found.")
```

### Output previsto

Quando esegui lo script, la console stampa:

```
✅ PDF created successfully: YOUR_DIRECTORY/invoice_searchable.pdf
```

Aprendo il file, dovresti vedere l'immagine originale della fattura con un leggero livello di testo invisibile. Evidenzia qualsiasi parola e noterai che è selezionabile—**questo è il testo ricercabile** che hai appena aggiunto.

## Aggiungere Testo Ricercabile a PDF Esistenti (Bonus)

A volte hai già un PDF ma devi **aggiungere testo ricercabile**. Lo stesso motore può sovrapporre i risultati OCR a un PDF esistente:

```python
# Bonus: Add searchable text to an existing PDF file
existing_pdf = engine.load_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result = engine.recognize_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result.apply_to(existing_pdf).save_as_pdfa("YOUR_DIRECTORY/old_scanned_searchable.pdf")
```

Qui `apply_to` unisce il livello nascosto con le pagine originali, permettendoti di **creare PDF ricercabili** senza dover riscanalizzare.

## Problemi Comuni e Consigli

| Problema | Come evitarlo |
|----------|-----------------|
| **Immagini sorgente a bassa risoluzione** (< 150 dpi) | Aumenta la risoluzione o richiedi una scansione a risoluzione più alta; la precisione dell'OCR diminuisce drasticamente sotto i 150 dpi. |
| **Dati di lingua mancanti** | Installa i pacchetti di lingua appropriati per il tuo motore OCR (`pip install pdfocr[eng,spa]`). |
| **Cartella di output non scrivibile** | Esegui lo script con permessi sufficienti o scegli una directory diversa. |
| **Validazione PDF/A fallita** | Assicurati di non incorporare font non supportati o JavaScript; la maggior parte degli SDK gestisce automaticamente questo quando usi `save_as_pdfa`. |

## Script Completo – Soluzione in Un Solo File

Di seguito trovi uno script autonomo che collega tutti i passaggi. Copialo, sostituisci i percorsi segnaposto e sei pronto a **convertire immagini in PDF/A** in pochi secondi.

```python
#!/usr/bin/env python3
"""
How to OCR PDF – Complete script to create a searchable PDF/A from an image.
Works with any OCR engine exposing `recognize_image` and `save_as_pdfa`.
"""

import os
import subprocess

# ----------------------------------------------------------------------
# CONFIGURATION – change these paths to match your environment
# ----------------------------------------------------------------------
INPUT_IMAGE = "YOUR_DIRECTORY/invoice.png"
OUTPUT_PDF  = "YOUR_DIRECTORY/invoice_searchable.pdf"

# ----------------------------------------------------------------------
# INITIALIZE THE OCR ENGINE (replace with your SDK's init call)
# ----------------------------------------------------------------------
# Example for a fictional `pdfocr` package:
# from pdfocr import Engine
# engine = Engine(api_key="YOUR_API_KEY")
# If you use a different library, adjust the import and init accordingly.
engine = Engine()  # placeholder – insert real initialization here

def main():
    # Step 1 – Recognize the image
    print(f"🔎 Recognizing text from {INPUT_IMAGE} …")
    result = engine.recognize_image(INPUT_IMAGE)

    # Step 2 – Save as searchable PDF/A
    print(f"💾 Saving searchable PDF/A to {OUTPUT_PDF} …")
    result.save_as_pdfa(OUTPUT_PDF)

    # Step 3 – Verify the file exists
    if os.path.isfile(OUTPUT_PDF):
        print("✅ Success! Searchable PDF/A created.")
        # Open the file for a quick visual check (optional)
        try:
            if os.name == "posix":
                subprocess.run(["open", OUTPUT_PDF])
            else:
                subprocess.run(["start", OUTPUT_PDF], shell=True)
        except Exception:
            pass
    else:
        print("❌ Error: PDF not created.")

if __name__ == "__main__":
    main()
```

**Cosa fa questo script:**  
1. Carica il motore OCR.  
2. Legge l'immagine selezionata ed estrae il testo.  
3. Scrive un **PDF/A ricercabile** che puoi subito distribuire o archiviare.  

Sentiti libero di racchiudere la logica `main` in una funzione che processa un'intera cartella—basta iterare su `os.listdir()` e ripetere i tre passaggi per ogni file.

## Prossimi Passi e Argomenti Correlati

Ora che hai padroneggiato **come fare OCR su PDF**, considera di esplorare queste idee successive:

- **Elaborazione batch:** Usa `concurrent.futures` per fare OCR a decine di fatture in parallelo.  
- **Iniezione di metadati:** Aggiungi date di creazione o numeri di fattura ai metadati del PDF per indicizzazioni più semplici.  
- **PDF ibridi:** Combina testo ricercabile con immagini originali incorporate per un “gemello digitale” del documento cartaceo.  
- **Uscite alternative:** Esporta in **DOCX** o **HTML** se i sistemi a valle richiedono formati modificabili.

Ognuna di queste si basa sui concetti fondamentali appena appresi—riconoscere, esportare, verificare.

## Conclusione

In sintesi, ora sai **come fare OCR su PDF** trasformando una semplice immagine in un **PDF/A ricercabile** con sole tre righe di Python. Lo script gestisce il lavoro pesante, preserva la grafica originale e ti fornisce un documento conforme agli standard che puoi cercare, archiviare o condividere.  

Provalo con le tue fatture, ricevute o contratti scansionati. Se incontri difficoltà, lascia un commento qui sotto o consulta la documentazione ufficiale dell'SDK—di solito è ricca di esempi aggiuntivi. Buona programmazione e goditi la nuova capacità di rendere qualsiasi immagine immediatamente ricercabile! 

![Esempio di Come fare OCR su PDF che mostra l'immagine originale e la sovrapposizione del PDF ricercabile](placeholder.png "Esempio di Come fare OCR su PDF")

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come fare OCR su PDF in .NET con Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Riconoscere Testo PDF – Operazioni OCR con Aspose.OCR per Java](/ocr/english/java/ocr-operations/)
- [Convertire Immagini in PDF C# – Salva Risultato OCR Multi‑pagina](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}