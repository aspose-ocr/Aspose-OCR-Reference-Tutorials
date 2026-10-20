---
category: general
date: 2026-03-26
description: Impara come eseguire l'OCR in Python e riconoscere il testo da file immagine.
  Questa guida mostra come estrarre il testo da PNG e convertire rapidamente l'immagine
  in testo.
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: it
og_description: Come eseguire l'OCR in Python? Segui questa guida per riconoscere
  il testo da un'immagine, estrarre il testo da PNG e convertire l'immagine in testo
  con una licenza di prova.
og_title: Come eseguire OCR in Python – Tutorial completo
tags:
- OCR
- Python
- Image Processing
title: Come eseguire l'OCR in Python – Tutorial completo passo‑passo
url: /it/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR in Python – Tutorial completo passo‑passo  

Ti sei mai chiesto **come eseguire OCR** su una foto appena scattata con il tuo telefono? Non sei l'unico: gli sviluppatori di tutto il mondo hanno bisogno di un modo affidabile per riconoscere il testo da file immagine senza doversi confrontare con librerie native complesse.  

In questo tutorial percorreremo un esempio pratico che mostra **come eseguire OCR**, **riconoscere testo da immagine** e **estrarre testo da PNG** usando un wrapper Python leggero. Alla fine sarai in grado di **convertire immagine in testo** in poche righe di codice, e non dovrai preoccuparti di problemi di licenza perché utilizzeremo la modalità di prova integrata.

## Cosa imparerai  

* Come configurare una licenza di prova per il motore OCR (non è necessario specificare un percorso file).  
* La sequenza esatta di chiamate per **recognize text from image**.  
* Modi per **extract text from PNG** e gestire problemi comuni come font mancanti.  
* Consigli per scalare la soluzione quando si passa da una licenza di prova a una licenza di produzione.  

**Prerequisites** – è necessario Python 3.8+ e il pacchetto `ocr` (installabile tramite `pip install ocr`). Non sono richiesti altri strumenti esterni.

---  

![esempio di come eseguire OCR](https://example.com/ocr-demo.png "come eseguire OCR in Python – testo riconosciuto mostrato")  

*Testo alternativo dell'immagine: come eseguire OCR in Python – esempio di output*  

## Passo 1 – Attivare una licenza di prova (senza percorso file)  

Prima che il motore possa leggere qualsiasi cosa, ha bisogno di una licenza valida. La modalità di prova è perfetta per esperimenti e piccoli progetti.

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*Perché è importante:* L'oggetto licenza indica alla libreria OCR che stai operando in un sandbox. Se salti questo passaggio, il motore solleverà un `LicenseError` non appena chiami `recognize()`.

**Pro tip:** Quando passi a una licenza a pagamento, sostituisci le due righe sopra con `ocr.License("path/to/your/license.key").apply()`.

## Passo 2 – Creare l'istanza del motore OCR  

Ora che la prova è attiva, istanziamo il motore principale. Pensalo come il “cervello” che guarderà l'immagine e deciderà dove sono i caratteri.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*Perché è importante:* `OcrEngine` contiene configurazioni come i pacchetti lingua e le impostazioni DPI. Puoi modificarle in seguito, ma il valore predefinito funziona per la maggior parte dei PNG solo in inglese.

## Passo 3 – Caricare il PNG da elaborare  

Qui è dove **recognize text from image**. Il metodo `ocr.Imaging.Image.load()` supporta PNG, JPEG, BMP e alcuni altri formati.

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*Caso limite:* Se il tuo PNG utilizza una palette indicizzata (comune per gli screenshot), il loader lo convertirà automaticamente in un buffer RGB a 24 bit. Questa conversione può comportare un piccolo impatto sulle prestazioni, ma garantisce risultati OCR accurati.

## Passo 4 – Eseguire l'OCR e ottenere il testo  

Infine, chiediamo al motore di fare il suo lavoro e poi estraiamo il risultato in testo semplice.

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**Output previsto** (esempio per un'immagine semplice contenente “Hello World”):

```
Hello World
```

Se l'immagine contiene più righe, l'output manterrà i ritorni a capo, facilitando l'integrazione con processi successivi come parser CSV o pipeline NLP.

## Opzionale: Ottimizzazione per una maggiore precisione  

* **Language packs:** `ocr_engine.set_language("eng")` (predefinito) o `"fra"` per il francese.  
* **DPI scaling:** `ocr_engine.set_dpi(300)` può migliorare i risultati su scansioni a bassa risoluzione.  
* **Pre‑processing:** Applicare una soglia binaria (`ocr.Imaging.Image.threshold()`) prima di `set_image` spesso produce testo più pulito su sfondi rumorosi.  

Queste regolazioni sono utili quando si passa da una demo veloce a un **ocr tutorial python** di livello produzione che elabora centinaia di file al giorno.

## Script completo – Pronto da copiare e incollare  

Di seguito trovi lo script completo e eseguibile che combina tutti i passaggi sopra. Salvalo come `run_ocr.py` e sostituisci `YOUR_DIRECTORY/sample1.png` con il percorso del tuo PNG.

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

Eseguilo dalla riga di comando:

```bash
python run_ocr.py
```

Dovresti vedere il testo estratto stampato sulla console. Se ottieni una stringa vuota, verifica che l'immagine contenga effettivamente testo chiaro e ad alto contrasto e che la licenza di prova sia stata applicata senza errori.

## Domande frequenti e insidie  

* **“Funziona con JPEG?”** – Assolutamente. Il metodo `load()` rileva automaticamente il formato, così puoi sostituire PNG con JPEG senza modificare il codice.  
* **“E se l'immagine è ruotata?”** – Il motore può rilevare automaticamente l'orientamento, ma per risultati ottimali puoi pre‑ruotare con `input_image.rotate(90)` prima di `set_image`.  
* **“Posso elaborare più immagini in un ciclo?”** – Sì. Basta spostare le chiamate di caricamento e `recognize()` all'interno di un ciclo `for`; la stessa istanza `ocr_engine` può essere riutilizzata, risparmiando un piccolo overhead.  

## Prossimi passi – Da demo a produzione  

Ora che sai **come eseguire OCR**, considera questi argomenti di approfondimento:

* **Batch processing** – Combina questo script con `os.listdir()` per **extract text from PNG** in blocco.  
* **Integrate with PDF** – Usa `pdf2image` per convertire le pagine PDF in PNG, quindi inviarle nella stessa pipeline.  
* **Post‑processing** – Applica regex o fuzzy matching per pulire le comuni errate interpretazioni OCR (es., “0” vs “O”).  

Ognuno di questi si basa sull'idea centrale di **convert image to text** e amplia l'utilità del tuo flusso di lavoro OCR.

---  

### TL;DR  

Abbiamo coperto tutto ciò che devi sapere per **how to perform OCR** in Python: attivare una licenza di prova, creare un motore, caricare un PNG, eseguire il riconoscimento e stampare il risultato. Con poche righe di codice puoi **recognize text from image**, **extract text from PNG** e **convert image to text** per qualsiasi applicazione successiva.  

Provalo, regola le impostazioni DPI o lingua, e lascia che il motore faccia il lavoro pesante. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}