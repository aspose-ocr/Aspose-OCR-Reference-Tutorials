---
category: general
date: 2026-06-16
description: Definisci la regione di interesse nell'OCR per estrarre il testo spagnolo
  dalle carte d'identità. Impara come caricare l'immagine per l'OCR e specificare
  la ROI in modo efficiente.
draft: false
keywords:
- define region of interest
- load image for ocr
- how to specify roi
- extract id card text
- extract spanish text image
language: it
og_description: Definisci l'area di interesse nell'OCR per estrarre il testo spagnolo
  dalle carte d'identità. Guida passo passo su come caricare le immagini e specificare
  l'ROI.
og_title: Definisci la regione di interesse nell'OCR – Tutorial completo di Python
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Define region of interest in OCR to extract Spanish text from ID cards.
    Learn how to load image for OCR and specify ROI efficiently.
  headline: Define region of interest in OCR – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Definisci la regione di interesse nell'OCR – Tutorial completo di Python
url: /it/python-java/general/define-region-of-interest-in-ocr-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definisci la regione di interesse in OCR – Tutorial Python Completo

Ti sei mai chiesto come **definire la regione di interesse in OCR** in modo da leggere solo la parte di un’immagine di cui hai realmente bisogno? In questo tutorial ti guideremo passo passo, mostrandoti anche come **caricare l’immagine per OCR** ed estrarre testo in spagnolo da una carta d’identità con poche righe di Python.  

Se ti sei mai trovato davanti a una scansione rumorosa e hai pensato “Deve esserci un modo più pulito per catturare il campo nome”, sei nel posto giusto. Alla fine sarai in grado di estrarre il testo della carta d’identità che ti interessa senza incappare nel caos di sfondo.

## Cosa Imparerai

- Perché dovresti **definire la regione di interesse** prima di eseguire l’OCR.  
- I passaggi esatti per **caricare l’immagine per OCR** usando un popolare wrapper Python per OCR.  
- Come **specificare la ROI** con coordinate pixel.  
- Modi per **estrarre il testo della carta d’identità** in modo affidabile, anche quando la lingua di origine è lo spagnolo.  
- Suggerimenti per gestire casi particolari come carte ruotate o scansioni a basso contrasto.  

Non è necessario avere una padronanza pregressa dell’OCR—basta un ambiente Python 3 funzionante e un file JPEG di una carta d’identità da testare.

---

![Define region of interest illustration](placeholder.png){alt="Esempio di definizione della regione di interesse che mostra un rettangolo evidenziato su un’immagine di carta d’identità"}

## Passo 1: Installa e Importa la Libreria OCR

Prima di tutto, ti serve una libreria che esponga una classe `OcrEngine` simile allo snippet che hai visto. Per questa guida useremo il pacchetto fittizio `ocr`, ma gli stessi concetti valgono per `pytesseract`, `easyocr` o qualsiasi wrapper che ti permetta di impostare una lingua e una ROI.

```bash
pip install ocr   # Replace with the actual package name you use
```

```python
# Import the library and any helper classes
import ocr
from ocr import Rectangle, Image
```

*Pro tip:* Se usi `pytesseract`, la classe `Rectangle` diventa una semplice tupla `(left, top, width, height)`. Il resto del flusso rimane identico.

## Passo 2: Carica l’Immagine per OCR

Ora **carichiamo l’immagine per OCR**. Il motore si aspetta un oggetto `ocr.Image`, quindi gli forniamo il file che contiene la carta d’identità. Assicurati che il percorso sia assoluto o relativo alla directory di lavoro del tuo script.

```python
# Create the OCR engine instance
engine = ocr.OcrEngine()

# Tell the engine which language we’re interested in – Spanish in this case
engine.language = ocr.Language.SPANISH

# Load the source image that contains the text to be recognized
engine.image = Image.load_from_file("YOUR_DIRECTORY/id-card.jpg")
```

Se l’immagine è molto grande, considera di ridimensionarla prima; i motori OCR lavorano più velocemente su immagini con larghezza inferiore a 1500 px.

## Passo 3: Come Specificare la ROI (Definire la Regione di Interesse)

Ecco il cuore del tutorial: **come specificare la ROI**. Una regione di interesse è semplicemente un rettangolo che dice al motore OCR: “Guarda solo dentro questi limiti pixel”. Pensala come un riquadro intorno al campo nome su una carta d’identità.

```python
# Define the region of interest – left, top, width, height (all in pixels)
engine.region_of_interest = Rectangle(
    left=120,   # X‑coordinate of the left edge
    top=80,     # Y‑coordinate of the top edge
    width=340,  # Width of the box
    height=200  # Height of the box
)
```

Perché questi numeri? Nella nostra immagine di esempio il nome si trova circa a 120 px dal bordo sinistro e a 80 px dal bordo superiore. Regolali per adattarli al layout delle carte che stai elaborando.  

*Caso limite:* Se la carta è ruotata di 90°, scambia `width` e `height` e aggiusta `left`/`top` di conseguenza, oppure pre‑ruota l’immagine con Pillow prima di passarla al motore.

## Passo 4: Esegui l’OCR All’interno della ROI

Con la ROI definita, il motore ignorerà tutto ciò che sta fuori dal rettangolo. Questo non solo velocizza l’elaborazione, ma riduce anche i falsi positivi causati da grafiche di sfondo.

```python
# Run OCR only inside the defined ROI
roi_result = engine.recognize()
```

La chiamata `recognize()` restituisce un oggetto che contiene il testo riconosciuto, i punteggi di confidenza e i riquadri di delimitazione per ogni parola.

## Passo 5: Estrai il Testo della Carta d’Identità (e Verifica l’Uscita in Spagnolo)

Infine, **estraiamo il testo della carta d’identità** dal risultato della ROI e lo stampiamo. Poiché abbiamo impostato la lingua su spagnolo in precedenza, il motore OCR utilizzerà dizionari specifici per la lingua, migliorando l’accuratezza per caratteri accentati come “ñ” o “á”.

```python
# Output the recognized text from the ROI
print("ROI text:", roi_result.text)
```

### Output Atteso

```
ROI text: JUAN PÉREZ GARCÍA
```

Se vedi caratteri incomprensibili, ricontrolla che l’immagine sia effettivamente in spagnolo e che i file di dati della lingua siano installati nella libreria OCR.

## Problemi Comuni & Come Evitarli

| Sintomo | Probabile Causa | Soluzione |
|---------|-----------------|-----------|
| Stringa vuota restituita | La ROI non interseca alcun testo | Verifica le coordinate con un visualizzatore di immagini; usa `engine.debug_draw_roi()` se disponibile. |
| Molti caratteri spazzatura | Pacchetto lingua errato | Re‑installa i dati della lingua spagnola o passa a `ocr.Language.AUTO`. |
| Punteggi di confidenza bassi | Immagine sfocata o a basso contrasto | Pre‑elabora con OpenCV – applica `cv2.GaussianBlur` e `cv2.threshold`. |
| OCR eseguito sull’intera immagine nonostante la ROI | Uso di una versione della libreria più vecchia | Aggiorna all’ultima versione del pacchetto `ocr`; le versioni precedenti ignoravano la ROI. |

## Estendere l’Esempio: ROI Multiple

A volte è necessario estrarre più di un campo (ad es., nome e numero di ID). Il modello rimane lo stesso: cambia `engine.region_of_interest` e chiama nuovamente `recognize()`.

```python
# ROI for the ID number (different coordinates)
engine.region_of_interest = Rectangle(120, 300, 340, 80)
id_result = engine.recognize()
print("ID Number:", id_result.text)
```

Puoi anche elaborare in batch un elenco di rettangoli se la libreria lo supporta, risparmiando un round‑trip al motore OCR.

## Script Completo Funzionante

Mettendo tutto insieme, ecco uno script pronto all’uso che **definisce la regione di interesse**, **carica l’immagine per OCR** e **estrae testo in spagnolo** da una carta d’identità.

```python
import ocr
from ocr import Rectangle, Image

def extract_name_from_id(image_path):
    """
    Loads an image, defines a ROI around the name field,
    runs OCR in Spanish, and returns the recognized text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.SPANISH
    engine.image = Image.load_from_file(image_path)

    # Adjust these numbers to match your card layout
    engine.region_of_interest = Rectangle(left=120, top=80, width=340, height=200)

    result = engine.recognize()
    return result.text.strip()

if __name__ == "__main__":
    name = extract_name_from_id("YOUR_DIRECTORY/id-card.jpg")
    print("Extracted Name:", name)
```

Esegui lo script e dovresti vedere il nome stampato sulla console. Modifica i valori del rettangolo per puntare ad altri campi, e avrai un’utilità riutilizzabile per qualsiasi documento tipo carta d’identità.

## Prossimi Passi

- **Elaborazione batch:** Scorri una cartella di carte d’identità e salva ogni nome estratto in un file CSV.  
- **Rilevamento lingua:** Consenti all’utente di scegliere la lingua dinamicamente; `ocr.Language.AUTO` può essere utile.  
- **Post‑elaborazione:** Applica pattern regex per pulire gli errori comuni dell’OCR (ad es., sostituire “0” con “O” quando appare nei nomi).  

Padroneggiando come **definire la regione di interesse** hai sbloccato un modo potente per **estrarre il testo della carta d’identità** in modo rapido e preciso, soprattutto quando lavori con documenti in lingua spagnola.

---

### TL;DR

Ti abbiamo mostrato come **definire la regione di interesse in OCR**, **caricare l’immagine per OCR** e **specificare la ROI** per **estrarre testo spagnolo da un’immagine** di una carta d’identità. L’esempio completo gira in meno di un minuto e può essere adattato a qualsiasi layout con pochi aggiustamenti di coordinate. Provalo, modifica il rettangolo e guarda l’OCR focalizzarsi come un laser.

Happy coding!

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come Estrarre Testo da Immagine Preparando Rettangoli in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Estrarre Testo da Immagine C# con Selezione della Lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Estrarre Testo da Immagine – Ottimizzazione OCR con Aspose.OCR per .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}