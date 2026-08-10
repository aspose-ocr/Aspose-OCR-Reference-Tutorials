---
category: general
date: 2026-03-18
description: Esegui OCR sull'immagine ed estrai il testo scritto a mano da una foto.
  Scopri come convertire un'immagine scritta a mano, estrarre il testo da un JPG e
  riconoscere il testo da una foto.
draft: false
keywords:
- perform OCR on image
- convert handwritten image
- extract text from jpg
- extract handwritten text
- recognize text from photo
language: it
og_description: Esegui OCR sull'immagine per estrarre il testo scritto a mano da una
  foto. Questo tutorial mostra come convertire l'immagine scritta a mano e riconoscere
  il testo da file JPG.
og_title: Esegui OCR su immagine – Guida completa al testo scritto a mano
tags:
- OCR
- Python
- Handwriting Recognition
title: Esegui OCR sull'immagine – Converti l'immagine scritta a mano in testo
url: /it/python/general/perform-ocr-on-image-convert-handwritten-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine – Estrazione di Testo a Mano Full‑Stack

Ti è mai capitato di dover **perform OCR on image** file ma non eri sicuro che il motore potesse leggere una scrittura a mano disordinata? Non sei il solo. In molte applicazioni reali — pensa a scanner di ricevute di spese o a utility per prendere appunti — ti imbatterai in foto di scarabocchi che devono essere trasformati in testo semplice.  

In questa guida ti mostreremo come **convert handwritten image** file, **extract text from jpg**, e persino **recognize text from photo** flussi usando una piccola libreria in stile Python chiamata `ocr`. Alla fine avrai uno script pronto all'uso che estrae ogni parola da un appunto scritto a mano, indipendentemente da quanto fosse traballante la penna.

## Di cosa avrai bisogno

- Python 3.8+ (il codice funziona su qualsiasi interprete recente)
- Il pacchetto ipotetico `ocr` – installalo con `pip install ocr-lib` (sostituisci con il nome reale del pacchetto che usi)
- Una fotografia chiara di un appunto scritto a mano salvata come `note.jpg` (o qualsiasi altro formato immagine)
- Una modesta dose di curiosità — non è necessario un background avanzato di ML

È tutto. Nessun servizio esterno, nessuna chiave API, solo un motore locale che può **perform OCR on image** dati.

![perform OCR on image screenshot](example.png)

*Testo alternativo: perform OCR on image screenshot che mostra l'editor di codice con lo script OCR.*

## Implementazione passo‑passo

Di seguito suddividiamo il processo in piccoli pezzi. Ogni intestazione include una parola chiave così puoi scorrere rapidamente, e ogni blocco spiega **perché** facciamo quello che facciamo — non solo **cosa**.

### Passo 1: Installa e verifica la libreria OCR

Prima di poter **perform OCR on image** file, la libreria deve essere presente nel tuo ambiente. Apri un terminale ed esegui:

```bash
pip install ocr-lib
```

**Suggerimento:** se lavori in un ambiente virtuale (altamente consigliato), attivalo prima. Questo mantiene le dipendenze ordinate ed evita conflitti di versione.

Dopo l'installazione, assicuriamoci che Python possa importare il pacchetto:

```python
try:
    import ocr
    print("OCR library loaded successfully.")
except ImportError as e:
    raise SystemExit("Failed to import ocr library. Did you run pip install?") from e
```

Se vedi il messaggio di successo, sei pronto a **convert handwritten image** dati.

### Passo 2: Crea un'istanza del motore e scegli la modalità Handwritten

La maggior parte dei motori OCR riconosce per impostazione predefinita il testo stampato. Poiché vogliamo **extract handwritten text**, dobbiamo cambiare esplicitamente la modalità. Questo passo è cruciale perché la scrittura a mano spesso richiede pre‑elaborazioni diverse (come l'ammorbidimento dei tratti).

```python
# Step 2: Initialize the OCR engine
engine = ocr.OcrEngine()

# Tell the engine we’re dealing with handwriting
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

print("Engine configured for handwritten recognition.")
```

*Perché è importante:* i caratteri scritti a mano possono variare enormemente in dimensione e inclinazione. Impostando `RecognitionMode.HANDWRITTEN`, il motore applica un modello addestrato su campioni corsivi, aumentando drasticamente l'accuratezza.

### Passo 3: Carica la foto da analizzare

Ora eseguiamo effettivamente **perform OCR on image** sul contenuto. Il metodo `load_image` accetta un percorso o un oggetto simile a un file. Per dimostrazione, caricheremo un JPEG, ma la stessa chiamata funziona per PNG, BMP o anche pagine PDF.

```python
# Step 3: Load the image file (replace the path with yours)
image_path = "YOUR_DIRECTORY/note.jpg"
engine.load_image(image_path)

print(f"Image '{image_path}' loaded into the OCR engine.")
```

Se la tua immagine si trova in un bucket cloud, scaricala prima o passa un flusso `BytesIO` — `ocr` è sufficientemente flessibile da gestire entrambi.

### Passo 4: Esegui il processo di riconoscimento

Con il motore pronto e l'immagine in memoria, finalmente **perform OCR on image** e recuperiamo il testo grezzo.

```python
# Step 4: Execute recognition
extracted_text = engine.recognize()

print("=== Extracted Text ===")
print(extracted_text)
```

La chiamata `recognize()` restituisce una semplice stringa Unicode. Per la maggior parte dei casi d'uso puoi scriverla direttamente in un file `.txt`, passarla a una pipeline di linguaggio naturale o visualizzarla in una GUI.

### Passo 5: Opzionale – Pulisci o post‑processa l'output

L'OCR su scrittura a mano non è perfetto; spesso vedrai interruzioni di riga indesiderate o caratteri riconosciuti erroneamente. Un rapido passo di pulizia può migliorare i risultati successivi.

```python
# Step 5: Simple post‑processing (optional)
def tidy(text):
    # Collapse multiple spaces, strip leading/trailing whitespace
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(extracted_text)

print("\n=== Cleaned Text ===")
print(clean_text)
```

Sentiti libero di collegare correttori ortografici, modelli linguistici o regex personalizzate a seconda del tuo dominio.

### Script completo – Pronto da copiare e incollare

Mettendo tutto insieme, ecco il programma completo e eseguibile che **extracts handwritten text** da un JPEG e stampa un risultato ordinato.

```python
# -*- coding: utf-8 -*-
"""
Complete example: Perform OCR on image to extract handwritten text.
"""

# -------------------------------------------------
# Step 1: Import the OCR library and create an engine
# -------------------------------------------------
import ocr

engine = ocr.OcrEngine()

# -------------------------------------------------
# Step 2: Set the engine to recognize handwritten text
# -------------------------------------------------
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

# -------------------------------------------------
# Step 3: Load the image you want to analyze
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/note.jpg"   # <-- change this to your file
engine.load_image(image_path)

# -------------------------------------------------
# Step 4: Perform recognition and output the extracted text
# -------------------------------------------------
raw_text = engine.recognize()
print("=== Raw OCR Output ===")
print(raw_text)

# -------------------------------------------------
# Step 5: Optional cleanup for nicer display
# -------------------------------------------------
def tidy(text):
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(raw_text)
print("\n=== Cleaned OCR Output ===")
print(clean_text)
```

**Output previsto** (il tuo testo reale sarà diverso, ovviamente):

```
=== Raw OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3

=== Cleaned OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3
```

Se vedi spazzatura, ricontrolla la qualità dell'immagine (buona illuminazione, minimo sfocamento) e assicurati di essere in modalità `HANDWRITTEN`. Questi due fattori spiegano la maggior parte degli errori di riconoscimento.

## Domande frequenti (FAQ)

| Domanda | Risposta |
|----------|--------|
| **Posso usarlo per estrarre testo da un PNG?** | Assolutamente. `engine.load_image("scan.png")` funziona allo stesso modo. |
| **E se la mia immagine è una pagina PDF?** | Converti prima la pagina in un'immagine (ad esempio, con `pdf2image`) poi passala al motore. |
| **La libreria è thread‑safe?** | Sì, puoi istanziare oggetti `OcrEngine` separati per thread. |
| **In che modo questo differisce da `pytesseract`?** | `ocr` astrae il binario Tesseract e include un modello per la scrittura a mano integrato, così non è necessario installare eseguibili esterni. |
| **E se devo **extract text from JPG** file in massa?** | Avvolgi lo script in un ciclo, o usa `engine.load_image` su ogni file e raccogli i risultati in una lista o CSV. |

## Casi limite e migliori pratiche

1. **Foto a basso contrasto** – Aumenta il contrasto programmaticamente prima del caricamento, o usa `engine.apply_preprocessing('contrast', level=2)`.
2. **Misto stampato e scritto a mano** – Esegui due passaggi: prima con `HANDWRITTEN`, poi con `PRINTED`, e unisci gli output.
3. **Immagini grandi** – Ridimensiona a circa 1500 px di larghezza; i motori OCR di solito funzionano più velocemente con buffer più piccoli senza perdere precisione.
4. **Caratteri Unicode** – La libreria restituisce stringhe UTF‑8, così puoi gestire emoji, lettere accentate o simboli matematici subito.

## Conclusione

Abbiamo appena attraversato un esempio concreto di come **perform OCR on image** file, mirati specificamente a note scritte a mano. Installando il pacchetto `ocr`, configurando il motore in modalità `HANDWRITTEN`, caricando una foto e chiamando `recognize()`, puoi **convert handwritten image** dati in testo pulito e ricercabile.  

Da qui potresti **extract text from jpg** file in massa, inviare l'output a un'app per prendere appunti, o combinarlo con sintesi vocale per l'accessibilità. Il cielo è il limite, e il codice sopra ti fornisce una solida base per sperimentare.  

Hai un trucco da condividere — forse un formato di file diverso o un'astuta tecnica di pre‑elaborazione? Lascia un commento e continuiamo la conversazione. Buon coding e divertiti a trasformare quei scarabocchi in oro digitale!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}