---
category: general
date: 2026-05-03
description: Estrai il testo dall'immagine istantaneamente usando Aspose OCR. Impara
  a definire la regione di interesse, caricare l'immagine per l'OCR e estrarre il
  testo dalla fattura in pochi minuti.
draft: false
keywords:
- extract text from image
- define region of interest
- load image for ocr
- extract text from invoice
- process image with ocr
language: it
og_description: Estrai il testo da un'immagine usando Aspose OCR. Questa guida mostra
  come definire la regione di interesse, caricare l'immagine per l'OCR ed estrarre
  il testo dalla fattura in modo efficiente.
og_title: Estrai il testo da un'immagine con Aspose OCR – Tutorial completo
tags:
- ocr
- python
- image-processing
title: Estrai il testo da un'immagine con Aspose OCR – Guida passo passo
url: /it/python-java/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da immagine con Aspose OCR – Guida passo‑passo

Hai bisogno di **estrarre testo da immagine** rapidamente? Non sei solo—gli sviluppatori lottano costantemente con scansioni rumorose, ricevute e fatture. In questo tutorial percorreremo una soluzione completa che non solo mostra come *estrarre testo da immagine* ma dimostra anche come **definire la regione di interesse**, **caricare immagine per OCR**, e recuperare la riga esatta di cui hai bisogno da una fattura.  

Copriamo tutto, dall'installazione della libreria Aspose OCR alla gestione di casi particolari come pagine ruotate. Alla fine avrai uno script eseguibile che estrae il testo desiderato con una singola chiamata—senza necessità di ritagli manuali.  

## Cosa imparerai

- Come **caricare immagine per OCR** usando l'API Python di Aspose.  
- Il modo migliore per **definire la regione di interesse** (ROI) così elabori solo la parte dell'immagine che importa.  
- Come **estrarre testo da fattura** senza includere l'intera pagina.  
- Suggerimenti per **processare immagine con OCR** in modo efficiente ed evitare gli errori più comuni.  

**Prerequisiti** – un ambiente Python 3.9+ recente, un file di licenza Aspose OCR valido e un'immagine (ad es., un PNG di fattura). Non sono richiesti altri strumenti esterni.

---

## Passo 1 – Inizializza il motore OCR (Configurazione primaria)

Prima di poter **processare immagine con OCR**, ti serve un'istanza del motore che contenga la tua licenza. Questo passaggio è cruciale perché un motore non licenziato restituisce solo un set di risultati limitato.

```python
import aspose.ocr as ocr  # Make sure you installed aspose-ocr via pip

# Create the OCR engine
ocr_engine = ocr.OcrEngine()

# Apply your license – replace the path with your actual .lic file location
ocr_engine.license = ocr.License().set_license("Aspose.OCR.Java.lic")
```

*Perché è importante*: l'oggetto `OcrEngine` è il cuore della libreria; gestisce i modelli linguistici, il pre‑processing dell'immagine e la licenza. Impostare la licenza fin da subito garantisce la massima precisione e nessun watermark.

---

## Passo 2 – Caricare immagine per OCR

Ora che il motore è pronto, dobbiamo **caricare immagine per OCR**. Aspose supporta molti formati (PNG, JPEG, TIFF), ma usare `Image.from_file` garantisce che l'immagine venga decodificata correttamente.

```python
# Load the target image – change the path to point at your invoice file
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.from_file(image_path)
```

> **Pro tip**: mantieni i file immagine sotto i 5 MB per la massima velocità di elaborazione. File più grandi possono essere ridimensionati con `image.resize(width, height)` prima dell'OCR.

---

## Passo 3 – Definire la regione di interesse (ROI)

La maggior parte delle fatture contiene molto testo irrilevante—blocchi di indirizzo, piè di pagina, ecc. Con **definire la regione di interesse** indichiamo al motore di guardare solo dove si trovano l'importo o la data, migliorando velocità e precisione.

```python
# Define ROI: (x, y, width, height) in pixels
# Adjust these numbers based on the layout of your specific invoice
roi = ocr.Rectangle(150, 300, 400, 120)
```

*Come funziona*: la classe `Rectangle` ritaglia l'immagine virtualmente; il motore OCR non vede pixel al di fuori del rettangolo, quindi il rumore fuori dalla ROI viene ignorato.

---

## Passo 4 – Riconoscere testo all'interno della ROI

Con motore, immagine e ROI pronti, finalmente **estraiamo testo da immagine**. Il metodo `recognize` restituisce un oggetto `OcrResult` contenente la stringa rilevata e i punteggi di confidenza.

```python
# Perform OCR only within the defined ROI
ocr_result = ocr_engine.recognize(image, roi=roi)

# Print the raw extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

**Output previsto** (esempio per una tipica riga di totale fattura):

```
Text inside ROI:
Total Amount: $1,245.67
```

Se la ROI è posizionata correttamente, vedrai solo la riga di cui hai bisogno—nulla più.

---

## Passo 5 – Esempio completo funzionante (pronto per copia‑incolla)

Di seguito lo script completo che collega tutti i passaggi precedenti. Salvalo come `extract_invoice_roi.py` ed esegui `python extract_invoice_roi.py`.

```python
# extract_invoice_roi.py
import aspose.ocr as ocr

def main():
    # 1️⃣ Initialize OCR engine and apply license
    ocr_engine = ocr.OcrEngine()
    ocr_engine.license = ocr.License().set_license("Aspose.OCR.Java.lic")

    # 2️⃣ Load the image you want to process
    image = ocr.Image.from_file("YOUR_DIRECTORY/invoice.png")

    # 3️⃣ Define the region of interest (ROI) – rectangle where the text lives
    roi = ocr.Rectangle(150, 300, 400, 120)   # (x, y, width, height)

    # 4️⃣ Recognize text only inside the ROI
    ocr_result = ocr_engine.recognize(image, roi=roi)

    # 5️⃣ Display the extracted text
    print("Text inside ROI:")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

Esegui lo script e dovresti vedere la riga mirata stampata sulla console. Se ottieni una stringa vuota, ricontrolla le coordinate della ROI—anche qualche pixel di scostamento può escludere completamente il testo.

---

## Passo 6 – Varianti comuni e casi particolari

### a) Layout di fattura diversi  
Le fatture di fornitori differenti spesso spostano il riquadro dell'importo totale. Per **processare immagine con OCR** su più layout, considera:

- **Multiple ROI**: esegui il motore sequenzialmente con diversi rettangoli e scegli il risultato con la più alta confidenza.  
- **Rilevamento ROI dinamico**: usa una libreria leggera di elaborazione immagini (ad es., OpenCV) per individuare prima l'etichetta “Total”, poi calcola la ROI relativa ad essa.

### b) Immagini ruotate o inclinate  
Se la scansione è inclinata, chiama `image.rotate(angle)` prima del riconoscimento:

```python
image = image.rotate(2.5)  # Rotate 2.5 degrees clockwise
```

Aspose OCR offre anche l'auto‑deskew, ma la rotazione manuale ti dà un controllo più preciso.

### c) Caratteri non latini  
Il modello linguistico predefinito è l'inglese. Per **estrarre testo da fattura** scritta in un'altra lingua, imposta la lingua prima del riconoscimento:

```python
ocr_engine.language = ocr.Language.French  # Example for French invoices
```

### d) PDF di grandi dimensioni  
Quando lavori con PDF multi‑pagina, estrai prima ogni pagina come immagine (Aspose PDF → Image) e poi applica la stessa logica ROI per pagina.

---

## Passo 7 – Consigli sulle prestazioni e pro‑tips

- **Cache del motore**: creare `OcrEngine` ripetutamente in un ciclo rallenta. Istanzialo una sola volta e riutilizzalo.  
- **Elaborazione batch**: se hai dozzine di fatture, avvolgi la chiamata OCR in un `ThreadPoolExecutor` per parallelizzare il lavoro I/O‑bound.  
- **Controllo di confidenza**: `ocr_result.confidence` restituisce un float tra 0 e 1. Scarta i risultati sotto 0,85 e ricorri a una ROI più ampia o a una revisione manuale.  

> **Attenzione**: impostare una ROI troppo piccola può tagliare i caratteri, generando output illeggibile. Testa sempre con qualche fattura di esempio prima di scalare.

---

## Conclusione

Ora disponi di un metodo solido, pronto per la produzione, per **estrarre testo da immagine** usando Aspose OCR, completo di una modalità per **definire la regione di interesse**, **caricare immagine per OCR** e **estrarre testo da fattura** in modo affidabile. Limitando l'OCR a una ROI ristretta aumenti sia la velocità sia la precisione—perfetto per l'elaborazione batch di migliaia di ricevute.  

Pronto per il passo successivo? Prova a integrare questo script in un'API Flask così la tua web app può caricare una fattura e restituire immediatamente l'importo totale. Oppure sperimenta con ROI multiple per estrarre data, numero fattura e nome del fornitore in un unico passaggio. Le possibilità sono infinite, e con le basi illustrate qui sei pronto ad affrontare qualsiasi sfida OCR.

Buon coding, e che il tuo testo estratto sia sempre pulito!  

![Workflow diagram showing how to extract text from image using Aspose OCR](workflow.png){: .center-image alt="Workflow to extract text from image using Aspose OCR"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}