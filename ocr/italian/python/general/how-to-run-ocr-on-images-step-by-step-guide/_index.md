---
category: general
date: 2026-01-02
description: Come eseguire OCR ed estrarre rapidamente il testo da un'immagine. Scopri
  come caricare l'immagine per l'OCR, migliorare l'accuratezza dell'OCR e ottenere
  risultati affidabili.
draft: false
keywords:
- how to run OCR
- extract text from image
- how to load image
- improve OCR accuracy
- load image for OCR
language: it
og_description: Come eseguire l'OCR su qualsiasi immagine. Questa guida ti mostra
  come caricare l'immagine per l'OCR, estrarre il testo dall'immagine e migliorare
  l'accuratezza dell'OCR con il post‑processing AI.
og_title: Come eseguire l'OCR – Tutorial completo per l'estrazione accurata del testo
tags:
- OCR
- Python
- image processing
title: Come eseguire OCR su immagini – Guida passo passo
url: /it/python/general/how-to-run-ocr-on-images-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR – Tutorial completo per un'estrazione di testo accurata

Ti sei mai chiesto **come eseguire OCR** su uno screenshot pieno di errori di battitura? Non sei solo. In molti progetti, gli sviluppatori devono estrarre testo pulito e ricercabile da documenti scansionati, ricevute o persino meme, e il risultato grezzo può essere caotico. La buona notizia? Con poche righe di Python puoi caricare un'immagine, eseguire il motore OCR e poi migliorare i risultati con un post‑processore potenziato dall'IA.  

In questo tutorial vedremo tutto quello che devi sapere: da **come caricare l'immagine** nel motore, all'estrazione del testo dall'immagine, fino al miglioramento della precisione OCR usando un post‑processore intelligente. Nessun servizio esterno, solo un esempio autonomo che puoi eseguire subito.

---

## Cosa ti servirà

- **Python 3.9+** (qualsiasi versione recente va bene)
- Un'istanza del motore OCR (per la demo assumiamo un oggetto generico `engine` che segue il tipico schema `load_image → recognize → run_postprocessor`)
- Un'immagine di esempio, ad es. `sample_with_typos.png`, collocata in una cartella a cui puoi fare riferimento
- Facoltativo: un ambiente virtuale per tenere ordinate le dipendenze

> **Consiglio professionale:** Se usi Tesseract, installalo tramite il gestore di pacchetti del tuo OS e poi avvolgilo con un wrapper Python come `pytesseract`. Il codice qui sotto astrae il motore, così puoi scambiare le implementazioni senza modificare la logica circostante.

---

## Passo 1 – Come caricare l'immagine per OCR

La prima cosa da fare è puntare il motore OCR al file che vuoi leggere. È qui che la frase **come caricare l'immagine** diventa letterale: fornisci al motore un percorso e lui prepara il bitmap per il riconoscimento.

```python
# Step 1: Load the image into the OCR engine
ocr_engine = engine               # assume the OCR engine instance is already created
ocr_engine.load_image("YOUR_DIRECTORY/sample_with_typos.png")
```

**Perché è importante:**  
Caricare correttamente l'immagine garantisce che il motore veda esattamente i dati pixel che intendi elaborare. Saltare la pre‑elaborazione (come il ridimensionamento o la conversione in scala di grigi) può far interpretare male i caratteri al motore, soprattutto in scansioni a basso contrasto.

---

## Passo 2 – Eseguire OCR per estrarre testo dall'immagine

Ora che l'immagine è pronta, invochiamo la routine OCR principale. Il metodo restituisce un oggetto il cui attributo `.text` contiene la stringa grezza.

```python
# Step 2: Run the basic OCR to obtain the raw text output
raw_result = ocr_engine.recognize()   # returns an object with a .text attribute
```

**Cosa ottieni:**  
`raw_result.text` conterrà ogni parola che il motore è riuscito a rilevare, inclusi errori di ortografia o artefatti causati dal rumore. Pensalo come la **estrazione grezza** — la base per qualsiasi ulteriore raffinamento.

---

## Passo 3 – Migliorare la precisione OCR con post‑processing potenziato dall'IA

La maggior parte delle pipeline OCR moderne espone un hook per il post‑processing. Nel nostro esempio, `run_postprocessor` applica un modello IA leggero che corregge errori comuni, normalizza la punteggiatura e persino riordina le parole quando il layout è confuso.

```python
# Step 3: Apply the AI‑enhanced post‑processor to improve accuracy
enhanced_result = ocr_engine.run_postprocessor(raw_result)
```

**Perché usare un post‑processore?**  
Anche i migliori motori OCR inciampano su caratteri distorti o sfondi rumorosi. Uno strato guidato dall'IA può apprendere da un corpus di testi corretti, migliorando drasticamente **la precisione OCR** senza intervento manuale.

---

## Passo 4 – Stampare sia i risultati grezzi che quelli migliorati dall'IA

Vedere la differenza fianco a fianco ti aiuta a valutare l'efficacia del post‑processore e a decidere se sono necessari ulteriori aggiustamenti.

```python
# Step 4: Print the raw and AI‑enhanced OCR results
print("Raw OCR:      ", raw_result.text)
print("AI‑enhanced:  ", enhanced_result.text)
```

### Output previsto

```
Raw OCR:       Th1s 1s 4  s@mple w1th typ0s.
AI‑enhanced:   This is a sample with typos.
```

Nell'output grezzo puoi individuare errori evidenti (`Th1s` → `This`, `4` → `a`, `s@mple` → `sample`). La versione migliorata dall'IA pulisce questi errori, fornendo una frase leggibile dall'uomo.

---

## Esempio completo funzionante (tutti i passaggi combinati)

Di seguito trovi lo script completo da copiare‑incollare in un file chiamato `ocr_demo.py`. Assicurati di sostituire `"YOUR_DIRECTORY"` con il percorso reale della tua immagine.

```python
# ocr_demo.py
# Complete, runnable example that shows how to run OCR,
# extract text from image, and improve OCR accuracy.

# -------------------------------------------------
# 1️⃣ Import the OCR engine (replace with your actual import)
# -------------------------------------------------
# Example placeholder:
# from my_ocr_lib import OCRengine
# engine = OCRengine()

# For this tutorial we assume `engine` is already instantiated.
# -------------------------------------------------

# -------------------------------------------------
# 2️⃣ Load the image
# -------------------------------------------------
ocr_engine = engine                     # existing OCR engine instance
ocr_engine.load_image("YOUR_DIRECTORY/sample_with_typos.png")

# -------------------------------------------------
# 3️⃣ Recognize raw text
# -------------------------------------------------
raw_result = ocr_engine.recognize()    # returns an object with .text

# -------------------------------------------------
# 4️⃣ Post‑process to improve accuracy
# -------------------------------------------------
enhanced_result = ocr_engine.run_postprocessor(raw_result)

# -------------------------------------------------
# 5️⃣ Display both results
# -------------------------------------------------
print("Raw OCR:      ", raw_result.text)
print("AI‑enhanced:  ", enhanced_result.text)
```

Eseguilo con:

```bash
python ocr_demo.py
```

Dovresti vedere le stringhe grezze e pulite stampate sulla console, proprio come nella sezione “Output previsto” sopra.

---

## Domande frequenti e casi particolari

### E se la mia immagine è in un formato diverso (ad es. PDF o TIFF)?

La maggior parte dei motori OCR accetta un percorso file, ma potrebbe richiedere un passaggio di conversione per PDF multi‑pagina. Puoi usare `pdf2image` per trasformare ogni pagina in PNG prima di passarla al motore.

### Come gestisco lingue diverse dall'inglese?

Passa il codice lingua al motore durante l'inizializzazione, ad es. `engine = OCRengine(lang='fra')`. Anche il post‑processore potrebbe necessitare di un modello specifico per la lingua per correggere correttamente le diacritiche.

### Il mio output OCR contiene ancora caratteri strani — e ora?

Considera di pre‑elaborare l'immagine:  
- **Ridimensiona** a una DPI più alta (300 dpi è una buona base).  
- **Converti in scala di grigi** per ridurre il rumore cromatico.  
- **Applica sogliatura** (`cv2.threshold`) per aumentare il contrasto.

Questi passaggi spesso **migliorano la precisione OCR** prima che il post‑processore IA venga eseguito.

---

## Consigli per sfruttare al meglio il tuo flusso di lavoro OCR

- **Elaborazione batch:** cicla su una cartella di immagini e salva ogni risultato in un CSV per analisi successive.  
- **Caching:** se esegui più volte la stessa immagine, memorizza il risultato grezzo per evitare calcoli ridondanti.  
- **Aggiornamenti modello:** riaddestra periodicamente o aggiorna il post‑processore IA con nuovi esempi corretti; il modello migliora col tempo.  
- **Log degli errori:** cattura le eccezioni da `recognize()` e `run_postprocessor()` così da identificare i file problematici in seguito.

---

## Conclusione

Ora sai **come eseguire OCR** su qualsiasi immagine, dal caricamento all'estrazione del testo fino alla rifinitura con un post‑processore potenziato dall'IA. Seguendo i passaggi sopra otterrai costantemente stringhe più pulite e affidabili — che tu stia costruendo uno scanner di ricevute, un archivio di documenti o un semplice progetto hobby.

Pronto per la prossima sfida? Prova a integrare **estrazione di testo da immagine** in un database ricercabile, o sperimenta regole di post‑processing personalizzate per il tuo dominio. Il cielo è il limite, e con la pipeline giusta difficilmente un errore di battitura ti sfuggirà.

Buon coding! 🚀

![esempio di come eseguire OCR](https://example.com/ocr-demo.png "esempio di come eseguire OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}