---
category: general
date: 2026-06-25
description: Come usare l'OCR in Python – impara a caricare l'immagine per l'OCR,
  riconoscere il testo in una regione e estrarre rapidamente il testo della regione.
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: it
og_description: Come utilizzare l'OCR in Python – guida passo passo per caricare un'immagine,
  riconoscere il testo in una regione specifica ed estrarre il numero della fattura.
og_title: 'Come utilizzare OCR in Python: caricare l''immagine ed estrarre il testo
  della regione'
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 'Come usare OCR in Python: caricare l''immagine ed estrarre il testo della
  regione'
url: /it/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare OCR in Python: Caricare l'immagine ed estrarre il testo della regione

**Come usare OCR in Python** è più semplice di quanto pensi. Hai mai fissato una fattura scansionata e ti sei chiesto come estrarre solo il numero della fattura senza analizzare l'intera pagina? Non sei solo—molti sviluppatori incontrano questo ostacolo quando si avvicinano per la prima volta al riconoscimento ottico dei caratteri. In questa guida vedremo come caricare un'immagine per OCR, definire un rettangolo, riconoscere il testo in quella regione e infine estrarre il testo della regione. Alla fine avrai uno script pronto all'uso che isola qualsiasi pezzo di testo di cui hai bisogno.

> *Consiglio professionale:* Se lavori con PDF, converti prima ogni pagina in un'immagine—la maggior parte delle librerie OCR gestisce al meglio PNG/JPEG.

## Di cosa avrai bisogno

- Python 3.8+ (si consiglia l'ultima versione stabile)  
- Una libreria OCR che espone una classe `OcrEngine` (ad es., **ocr** da `pip install ocr-lib`)  
- Un'immagine di esempio—qui useremo `invoice.png` posizionata in una cartella a tua scelta  
- Familiarità di base con i rettangoli (x, y, width, height)  

Nessuna dipendenza pesante, nessuna GPU richiesta—solo lavoro su CPU, il che rende tutto portabile.

---

## Come usare OCR: Inizializzare il motore (Passo 1)

Prima che possa essere letto qualsiasi testo, è necessaria un'istanza del motore OCR. Pensala come il cervello che analizzerà i pattern dei pixel.

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Perché è importante:* Inizializzare il motore carica i modelli linguistici e imposta le configurazioni predefinite. Saltare questo passo genererebbe un'eccezione nel momento in cui chiami `recognize_region`.

## Caricare l'immagine per OCR (Passo 2)

Ora che il motore è pronto, gli forniamo un'immagine. Il metodo `Image.load` della libreria gestisce i formati più comuni e normalizza il bitmap.

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

Se il file non viene trovato, Python solleverà un `FileNotFoundError`. Assicurati che il percorso sia assoluto o relativo alla directory di lavoro del tuo script.  

*Caso limite:* Alcuni motori OCR si aspettano un'immagine in scala di grigi. Se noti scarsa accuratezza, converti prima l'immagine:

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## Riconoscere il testo nella regione (Passo 3)

Definire la regione è il punto in cui indichi al motore *dove* guardare. Il `Rectangle` accetta valori in virgola mobile per una precisione sub‑pixel, utile quando si lavora con scansioni ad alta risoluzione.

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – angolo superiore sinistro del rettangolo (in pixel)  
- **width, height** – dimensioni del riquadro  

Potresti chiederti come trovare questi numeri. Un modo rapido è aprire l'immagine in qualsiasi editor (ad es., GIMP o Paint.NET) e usare lo strumento di selezione per leggere le coordinate.  

*Perché non fare OCR sull'intera pagina?* Limitare l'area riduce il rumore, velocizza l'elaborazione e migliora notevolmente l'accuratezza per campi piccoli come i numeri di fattura.

---

## Come estrarre il testo della regione (Passo 4)

Con la regione impostata, chiedi al motore di riconoscere solo quella porzione. L'oggetto risultato contiene il testo grezzo e i punteggi di confidenza.

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

Se il motore OCR supporta più lingue, puoi passare un codice lingua opzionale:

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*Errore comune:* Alcuni motori restituiscono una lista di parole invece di una singola stringa. In questi casi, concatenale:

```python
text = " ".join(region_result.words)
```

---

## Stampare il numero di fattura estratto (Passo 5)

Infine, stampa—o salva—il testo estratto. Puoi anche post‑processare la stringa per rimuovere spazi bianchi superflui o caratteri non numerici.

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

Eseguendo lo script con un rettangolo correttamente allineato dovrebbe restituire qualcosa del genere:

```
Invoice number: 20231578
```

Se ottieni caratteri spazzatura, ricontrolla le coordinate del rettangolo o considera di aumentare la risoluzione dell'immagine.

---

## Esempio completo funzionante

Mettendo tutto insieme, ecco uno script autonomo che puoi copiare‑incollare ed eseguire:

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

Salva il file come `extract_invoice.py`, sostituisci `YOUR_DIRECTORY` con la cartella reale, ed esegui:

```bash
python extract_invoice.py
```

Dovresti vedere il numero di fattura stampato sulla console.

---

## Domande frequenti

**Q: E se il numero di fattura è stampato con un font elegante?**  
A: La maggior parte dei moderni motori OCR gestisce un'ampia gamma di font, ma puoi aumentare l'accuratezza addestrando un modello linguistico personalizzato o pre‑processando l'immagine (ad es., applicando un filtro di soglia).

**Q: Posso estrarre più campi contemporaneamente?**  
A: Assolutamente. Definisci una lista di oggetti `Rectangle`—uno per campo—e itera su di essi, memorizzando ogni risultato in un dizionario.

**Q: Funziona su PDF multi‑pagina?**  
A: Converti prima ogni pagina in un'immagine (usando `pdf2image` o simili), poi applica la stessa estrazione basata sulla regione per ogni pagina.

---

## Conclusioni

In questo tutorial abbiamo coperto **come usare OCR** in Python per caricare un'immagine, riconoscere il testo in una regione specifica ed estrarre il testo di quella regione—perfetto per estrarre numeri di fattura, ID ordine o qualsiasi piccolo frammento di dati da documenti scansionati. Isolando l'area di interesse ottieni velocità, accuratezza e meno problemi di post‑processing.

Pronto per il passo successivo? Prova a estendere lo script per gestire **load image for OCR** da una cartella di fatture batch, o sperimenta con **recognize text in region** per campi diversi come date e totali. Lo stesso schema si applica—basta cambiare le coordinate del rettangolo.

Se hai incontrato problemi o hai idee per miglioramenti, lascia un commento qui sotto. Buon coding, e che le tue pipeline OCR siano sempre accurate!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrarre testo da immagine con Aspose OCR – Guida passo‑passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Come estrarre testo da immagine preparando rettangoli in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Come usare AspOCR: filtri di pre‑processing per OCR su immagine in .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}