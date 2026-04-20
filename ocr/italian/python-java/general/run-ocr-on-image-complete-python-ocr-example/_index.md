---
category: general
date: 2026-03-18
description: Esegui OCR su un'immagine rapidamente con Python. Scopri come riconoscere
  il testo da PNG, caricare l'immagine per l'OCR e estrarre le parole dall'immagine
  in una guida passo‑passo.
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: it
og_description: Esegui OCR su un'immagine usando Python. Questo tutorial mostra come
  riconoscere il testo da un PNG, caricare l'immagine per l'OCR e estrarre le parole
  dall'immagine con un esempio di codice completo.
og_title: Esegui OCR su immagine – Guida Python
tags:
- OCR
- Python
- Image Processing
title: Esegui OCR su immagine – Esempio completo di OCR in Python
url: /it/python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine – Esempio Completo di OCR in Python

Ti è mai capitato di **eseguire OCR su file immagine** ma non sapevi da dove cominciare? Non sei l'unico; molti sviluppatori si trovano di fronte a questo ostacolo quando affrontano per la prima volta l'estrazione di testo da documenti scansionati. In questo tutorial percorreremo un **esempio di OCR in Python** che ti permette di **riconoscere testo da PNG**, **caricare immagine per OCR**, e **estrarre parole dall'immagine** con punteggi di confidenza—tutto in poche righe di codice.

Copriamo tutto ciò di cui hai bisogno: la libreria richiesta, come configurare il motore, perché ogni passaggio è importante e come appare l'output. Alla fine potrai inserire questo snippet nel tuo progetto e iniziare a estrarre testo da qualsiasi immagine all'istante. Niente fronzoli, solo una soluzione pratica e funzionante.

## Cosa ti servirà

Prima di immergerci, assicurati di avere:

- Python 3.8 o versioni successive installate  
- Il pacchetto `ocrengine` (o qualsiasi libreria che fornisca una classe `OcrEngine`). Puoi installarlo con `pip install ocrengine` – adatta il nome se usi una libreria OCR diversa come `pytesseract`.  
- Un file immagine (PNG, JPG, ecc.) che desideri elaborare – per questa guida useremo `invoice.png`.  

È tutto. Nessuna dipendenza pesante, nessun servizio esterno, solo puro Python.

![run OCR on image example showing a scanned invoice](/images/run-ocr-on-image.png)

*Testo alternativo: esempio di esecuzione OCR su immagine – fattura scansionata in fase di elaborazione*

## Passo 1 – Installa e Importa la Libreria OCR

Prima di tutto, portiamo il motore OCR nel nostro ambiente e lo importiamo. Se usi il pacchetto ipotetico `ocrengine`, l'importazione è così:

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**Perché è importante:** Importare la classe corretta ti dà accesso ai metodi che chiameremo più tardi, come `setImageFromFile` e `recognize`. Se salti questo passaggio, Python solleverà un `ModuleNotFoundError` e rimarrai bloccato prima ancora di caricare un'immagine.

## Passo 2 – Crea un'Istanza del Motore OCR

Ora che la libreria è pronta, ci serve un oggetto motore che contenga la configurazione e lo stato del processo di riconoscimento.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*Consiglio professionale:* Alcuni motori OCR ti permettono di regolare i modelli linguistici o le impostazioni DPI in questo punto. Per un **esempio di OCR python** di base, le impostazioni predefinite vanno bene, ma se lavori con scansioni a bassa risoluzione, considera di modificarle qui.

## Passo 3 – Carica l'Immagine da Elaborare

Il passo logico successivo è **caricare immagine per OCR**. Indichi al motore il percorso del file PNG (o di qualsiasi formato supportato) che desideri analizzare.

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**Cosa succede dietro le quinte?** Il motore legge i dati dei pixel, li converte in un formato comprensibile dall'algoritmo di riconoscimento e li memorizza internamente. Se il percorso è errato, otterrai un `FileNotFoundError`, quindi verifica che l'immagine esista.

## Passo 4 – Esegui l'Algoritmo di Riconoscimento

Con l'immagine caricata, finalmente **esegui OCR su immagine** per estrarre il contenuto testuale.

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

A questo punto il motore scandisce il bitmap, applica il pattern matching e restituisce un oggetto che contiene ogni parola, riga e metrica di confidenza rilevate.

## Passo 5 – Itera sulle Parole Riconosciute e Mostra la Confidenza

La parte più utile di qualsiasi flusso OCR è vedere **la confidenza** per ogni token estratto. Ti indica quanto il motore è sicuro di ciascuna parola, permettendoti di filtrare i risultati a bassa confidenza se necessario.

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**Output atteso** (esempio):

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

Ora puoi vedere esattamente **quali parole sono state estratte dall'immagine** e quanto è affidabile ogni rilevamento. Questo è il cuore di qualsiasi pipeline **estrarre parole da immagine**.

## Gestione dei Casi Limite più Comuni

### E se l'Immagine è in Scala di Grigi?

Alcuni motori OCR funzionano meglio con immagini a colori. Se noti una bassa confidenza generale, prova a convertire il PNG in una versione bianco‑nero ad alto contrasto prima di passarla al motore. Pillow può aiutare:

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### Gestione di Più Lingue

Se il tuo documento contiene sia inglese che spagnolo, dovrai **riconoscere testo da PNG** usando un modello multilingue. La maggior parte dei motori ti consente di impostare l'elenco delle lingue durante l'inizializzazione:

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### Filtrare le Parole a Bassa Confidenza

A volte ti servono solo le parole con confidenza superiore, ad esempio, al 90 %. Un filtro rapido è così:

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## Script Completo, Pronto all'Esecuzione

Riunendo tutto, ecco uno script unico che puoi copiare‑incollare e far girare subito (sostituisci solo il percorso del tuo PNG).

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

Eseguilo con:

```bash
python run_ocr_on_image.py
```

Dovresti vedere l'elenco di parole e le percentuali di confidenza stampate sulla console, esattamente come mostrato in precedenza.

## Domande Frequenti

**Funziona con file JPG o TIFF?**  
Assolutamente. Il metodo `setImageFromFile` accetta qualsiasi formato che la libreria sottostante può decodificare, quindi puoi **eseguire OCR su file immagine** di tipo JPG, TIFF, BMP, ecc.

**Posso elaborare più immagini in un ciclo?**  
Certo. Avvolgi i passaggi di caricamento e riconoscimento all'interno di un `for` loop su una lista di percorsi file. Ricorda solo di reinizializzare il motore se la libreria richiede una nuova istanza per immagine.

**E se ho bisogno del testo in una singola stringa invece che parola per parola?**  
La maggior parte degli oggetti risultato OCR espone un metodo `getText()` che restituisce l'intero documento. Esempio:

```python
full_text = ocr_result.getText()
print(full_text)
```

## Prossimi Passi e Argomenti Correlati

Ora che sai **come eseguire OCR su immagine**, considera di approfondire:

- **Post‑processing**: Usa espressioni regolari per pulire date, importi o ID estratti dalle fatture.  
- **Elaborazione batch**: Combina lo script con `os.listdir()` per gestire intere cartelle di documenti scansionati.  
- **Librerie alternative**: `pytesseract` è un'opzione open‑source popolare; il flusso di lavoro è simile—basta sostituire le chiamate al motore.  
- **Esportazione dei risultati**: Scrivi le parole estratte e le relative confidenze in CSV per analisi successive.

Ognuna di queste estensioni si basa direttamente sulla base che abbiamo costruito qui, permettendoti di trasformare i dati OCR grezzi in informazioni utili.

---

### TL;DR

Abbiamo mostrato un **esempio di OCR python** conciso che dimostra come **caricare immagine per OCR**, **eseguire OCR su immagine** e **estrarre parole da immagine** riportando la confidenza. Lo script completo è pronto all'uso e ora possiedi le conoscenze per adattarlo a qualsiasi progetto che necessiti di **riconoscere testo da PNG** (o altri formati). Provalo, regola le soglie di confidenza e guarda le tue applicazioni diventare consapevoli del testo in pochi minuti. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}