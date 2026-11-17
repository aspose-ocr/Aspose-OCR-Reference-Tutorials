---
category: general
date: 2026-04-26
description: Come utilizzare i thread per caricare immagini per OCR in Python. Impara
  l'elaborazione OCR asincrona con callback, thread in background e caricamento delle
  immagini in pochi semplici passaggi.
draft: false
keywords:
- how to use threading
- load image for OCR
- python threading OCR
- async OCR callback
- background thread image processing
language: it
og_description: Come utilizzare i thread per caricare un'immagine per l'OCR in Python.
  Questa guida mostra un esempio completo e eseguibile con callback e esecuzione in
  background.
og_title: Come usare il threading per caricare l'immagine per OCR
tags:
- Python
- Threading
- OCR
- Image Processing
title: Come utilizzare il threading per caricare l'immagine per OCR
url: /it/python-java/general/how-to-use-threading-to-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare il threading per caricare un'immagine per OCR

Ti sei mai chiesto **come usare il threading** per caricare un'immagine per OCR senza bloccare la tua app? È uno scenario che si presenta sia che tu stia costruendo uno scanner desktop, un servizio web, o uno script semplice che elabora immagini massive. La buona notizia? Poche righe di Python e il giusto pattern di threading manterranno la tua UI reattiva mentre il motore OCR fa la sua magia.

In questo tutorial percorreremo un esempio completo, end‑to‑end: caricare un PNG di grandi dimensioni, avviare l'OCR su un thread in background e gestire il risultato con un callback. Alla fine non solo saprai **come usare il threading**, ma anche come **caricare un'immagine per OCR** in modo pulito e riutilizzabile.

## Cosa ti servirà

- Python 3.9+ (la sintassi che usiamo funziona su qualsiasi versione recente)
- `pillow` per la gestione delle immagini (`pip install pillow`)
- `pytesseract` come un leggero wrapper attorno a Tesseract OCR (`pip install pytesseract`)
- Motore Tesseract OCR installato sulla tua macchina (scarica da [tesseract‑ocr.org](https://github.com/tesseract-ocr/tesseract))
- Un file immagine di grandi dimensioni che vuoi processare (`large_image.png` in questa guida)

Nessun framework extra, nessun async/await—solo il classico `threading` e un callback.

## Passo 1: Importare il modulo threading (necessario per l'esecuzione in background)

La prima cosa che facciamo è importare il modulo `threading`. Esso fornisce la classe `Thread`, che ci permette di eseguire qualsiasi funzione in un thread OS separato.

```python
import threading
```

*Perché è importante*: Se esegui l'OCR sul thread principale, il tuo programma (soprattutto una GUI) si bloccherà finché l'OCR non termina. Delegando il lavoro a un thread in background, il thread principale rimane libero di aggiornare l'interfaccia, gestire l'input dell'utente o avviare altre attività.

## Passo 2: Definire un callback che verrà invocato al termine dell'OCR

Un callback è semplicemente una funzione che un altro pezzo di codice chiama quando ha terminato. Qui stamperemo il testo riconosciuto, ma potresti salvarlo, inviarlo sulla rete o aggiornare un widget UI.

```python
def ocr_done(result_text: str) -> None:
    """Called when the OCR thread finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)   # Display the recognized text
```

*Consiglio professionale*: Mantieni il callback leggero. Un'elaborazione pesante all'interno del callback vanifica lo scopo del threading perché bloccherà comunque il thread che lo ha chiamato (spesso il thread principale).

## Passo 3: Caricare l'immagine da processare

Caricare l'immagine è una preoccupazione separata dall'OCR, ma è comunque parte del flusso di lavoro complessivo. Usare Pillow rende questo banale.

```python
from PIL import Image

def load_image(path: str) -> Image.Image:
    """Loads an image from disk and returns a Pillow Image object."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img
    except Exception as exc:
        raise RuntimeError(f"Failed to load image: {exc}") from exc
```

*Perché lo facciamo qui*: Se l'immagine è enorme, caricarla sul thread principale potrebbe già causare un intoppo. In molte app reali potresti anche delegare il caricamento a un thread, ma per chiarezza lo manteniamo sincrono.

## Passo 4: Creare un piccolo wrapper per il motore OCR

Il frammento originale usava `engine.process_async`. Lo imiteremo con una piccola classe che avvia internamente un thread e chiama il callback fornito al termine.

```python
import pytesseract

class SimpleOcrEngine:
    """A minimal OCR engine that runs pytesseract in a background thread."""

    def __init__(self, image: Image.Image):
        self.image = image

    def _run_ocr(self, callback):
        """Internal method executed in the worker thread."""
        try:
            # pytesseract returns the recognized text as a plain string
            text = pytesseract.image_to_string(self.image)
            callback(text)
        except Exception as exc:
            callback(f"OCR failed: {exc}")

    def process_async(self, callback):
        """Public method to start OCR on a new thread."""
        worker = threading.Thread(target=self._run_ocr, args=(callback,))
        worker.daemon = True          # Daemon so it won’t block program exit
        worker.start()
        print("OCR thread started…")
```

*Spiegazione*:  
- `_run_ocr` esegue il lavoro pesante.  
- `process_async` crea un oggetto `Thread`, lo segna come daemon (così l'interprete può terminare anche se il thread è ancora in esecuzione), e lo avvia.  
- Il callback riceve o il testo OCR o un messaggio di errore.

## Passo 5: Mettere tutto insieme e fare altro lavoro mentre l'OCR è in esecuzione

Ora orchestriamo l'intero flusso: carichiamo l'immagine, istanziamo il motore, avviamo l'OCR asincrono e manteniamo il thread principale occupato con qualcos'altro (qui stampiamo semplicemente un messaggio).

```python
if __name__ == "__main__":
    # 1️⃣ Load the image you want to OCR
    img_path = "YOUR_DIRECTORY/large_image.png"
    image = load_image(img_path)

    # 2️⃣ Create the OCR engine instance
    engine = SimpleOcrEngine(image)

    # 3️⃣ Start OCR on a background thread, passing our callback
    engine.process_async(callback=ocr_done)

    # 4️⃣ Do other work while OCR runs (simulated with a loop)
    for i in range(5):
        print(f"Main thread doing other work… ({i+1}/5)")
        # In a real app you might update a progress bar, handle UI events, etc.
        threading.Event().wait(0.5)  # Sleep 0.5 s without blocking the OS thread

    # Give the OCR thread a moment to finish before the script exits
    threading.Event().wait(2)
    print("Script finished.")
```

**Output previsto (troncato per brevità):**

```
Image 'YOUR_DIRECTORY/large_image.png' loaded – size: (3840, 2160)
OCR thread started…
Main thread doing other work… (1/5)
Main thread doing other work… (2/5)
...
--- Async OCR finished ---
The quick brown fox jumps over the lazy dog.
Script finished.
```

Se l'OCR fallisce, il callback stamperà un messaggio di errore invece del testo.

---

## Perché questo approccio funziona meglio di un semplice ciclo

- **Reattività**: Il thread principale non si blocca mai sulla chiamata OCR, che può richiedere secondi per immagini grandi.
- **Scalabilità**: Puoi avviare più istanze di `SimpleOcrEngine`, ognuna sul proprio thread, per processare un batch di immagini in parallelo.
- **Separazione delle preoccupazioni**: Il caricamento, l'elaborazione e la gestione del risultato sono separati in modo pulito, rendendo il codice più facile da testare e mantenere.

## Errori comuni e come evitarli

| Problema | Cosa succede | Soluzione |
|----------|--------------|-----------|
| Dimenticare di impostare il thread come *daemon* | Lo script resta in attesa dopo che il lavoro principale è terminato perché il thread OCR è ancora attivo. | Imposta `worker.daemon = True` **o** `join()` il thread prima di uscire. |
| Usare una variabile globale per il risultato senza lock | Le condizioni di gara possono corrompere i dati quando più thread scrivono simultaneamente. | Passa il risultato tramite un callback (come facciamo noi) o usa contenitori thread‑safe come `queue.Queue`. |
| Caricare un'immagine enorme sul thread principale | L'interfaccia si blocca prima che l'OCR in background inizi. | Delega anche il caricamento dell'immagine a un thread, o usa tecniche di caricamento lazy. |
| Non gestire le eccezioni all'interno del thread di lavoro | Le eccezioni non catturate uccidono silenziosamente il thread, lasciandoti senza risultato. | Avvolgi la logica OCR in `try/except` e inoltra l'errore al callback. |

## Estendere questo pattern

- **Segnalazione di avanzamento**: Usa una `queue.Queue` condivisa per inviare percentuali di avanzamento intermedie dal thread OCR al thread principale.
- **Pool di thread**: Per l'elaborazione batch, sostituisci gli oggetti `Thread` individuali con un `concurrent.futures.ThreadPoolExecutor`.
- **Integrazione GUI**: In un'app Tkinter o PyQt, programma il callback con `after()` (Tkinter) o `QTimer.singleShot` (Qt) per garantire che gli aggiornamenti UI avvengano sul thread principale.

## Esempio completo funzionante (pronto per copia‑incolla)

```python
import threading
from PIL import Image
import pytesseract

def ocr_done(result_text: str) -> None:
    """Callback invoked when OCR finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)

def load_image(path: str) -> Image.Image:
    """Load an image and report its size."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}