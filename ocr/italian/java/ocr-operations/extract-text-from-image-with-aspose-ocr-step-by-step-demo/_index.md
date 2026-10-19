---
category: general
date: 2026-02-14
description: Estrai il testo da un'immagine usando Aspose OCR. Scopri come caricare
  l'immagine per l'OCR, leggere il testo da un rettangolo e segui questo tutorial
  Aspose OCR in pochi minuti.
draft: false
keywords:
- extract text from image
- load image for ocr
- read text from rectangle
- aspose ocr tutorial
language: it
og_description: Estrai il testo dall'immagine istantaneamente. Questa guida mostra
  come caricare l'immagine per l'OCR, leggere il testo da un rettangolo e completare
  un tutorial su Aspose OCR.
og_title: Estrai il testo da un'immagine con Aspose OCR – Guida rapida
tags:
- Aspose
- OCR
- Java
title: Estrai il testo da un'immagine con Aspose OCR – Demo passo passo
url: /it/java/ocr-operations/extract-text-from-image-with-aspose-ocr-step-by-step-demo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai Testo da Immagine con Aspose OCR – Demo Passo‑per‑Passo

Hai mai avuto bisogno di **estrarre testo da un'immagine** ma non sapevi da dove cominciare? Non sei solo—molti sviluppatori incontrano questo ostacolo quando affrontano per la prima volta la scansione di ricevute o la verifica di documenti d'identità. La buona notizia? Con Aspose OCR puoi caricare un'immagine, definire l'esatta regione in cui si trova il testo e estrarre i caratteri in poche righe.

In questo **aspose ocr tutorial** ti guideremo passo passo su tutto ciò che ti serve: caricare l'immagine per l'OCR, impostare un rettangolo che indica al motore dove guardare e, infine, leggere il testo estratto. Alla fine avrai un programma Java eseguibile che stampa il testo ROI sulla console—senza misteri, solo una soluzione chiara e funzionante.

## Cosa Ti Serve

| Prerequisito | Perché è importante |
|--------------|----------------------|
| **Java JDK 8+** | Aspose OCR è distribuito come libreria Java; qualsiasi JDK moderno va bene. |
| **Aspose.OCR for Java** (download from the Aspose website or add via Maven) | Fornisce `OcrEngine`, `ImageStream` e le classi correlate. |
| **An image file** (e.g., `receipt.jpg`) that contains printable text | Indicheremo al motore un rettangolo all'interno di questo file. |
| **IDE or editor** (IntelliJ, Eclipse, VS Code…) | Ti aiuta a compilare ed eseguire rapidamente l'esempio. |

Se usi Maven, aggiungi questa dipendenza al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check Aspose for the latest version -->
</dependency>
```

> **Consiglio:** Il numero di versione sopra è corrente a partire da febbraio 2026. Aggiornare all'ultima release garantisce correzioni di bug e miglioramenti delle prestazioni.

## Passo 1 – Inizializzare il Motore OCR

Prima di tutto: ti serve un'istanza di `OcrEngine`. Pensala come il cervello che analizzerà i pixel.

```java
// Step 1: Create the OCR engine object
OcrEngine ocrEngine = new OcrEngine();
```

Perché crearla in questo modo? Aspose separa il motore (che contiene la configurazione) dai dati dell'immagine, offrendoti la flessibilità di riutilizzare lo stesso motore per più immagini, se lo desideri.

## Passo 2 – Caricare l'Immagine per l'OCR

Ora carichiamo effettivamente **l'immagine per l'OCR**. L'helper `ImageStream.fromFile` legge il file in uno stream che Aspose può interpretare.

```java
// Step 2: Load the target image (replace with your own path)
String imagePath = "YOUR_DIRECTORY/receipt.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

Se il file non viene trovato, il motore lancia un'eccezione, quindi potresti voler avvolgere questo codice in un blocco try‑catch in produzione. Per questa demo lasciamo che l'eccezione risalga—mantiene l'esempio pulito.

## Passo 3 – Definire il Rettangolo (Leggere Testo da Rettangolo)

Ecco dove brilla la parte **leggere testo da rettangolo**. Indichi al motore esattamente dove guardare, il che velocizza l'elaborazione e riduce i falsi positivi.

```java
// Step 3: Create a rectangle that covers the area with the receipt total
// Parameters: x, y, width, height (all in pixels)
Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);
```

> **Perché un rettangolo?**  
> La maggior parte dei documenti ha layout prevedibili—pensa a una ricevuta dove l'importo appare sempre vicino al fondo. Concentrandosi su quella sezione, il motore OCR ignora le grafiche irrilevanti e aumenta l'accuratezza.

**Caso limite:** Se il rettangolo supera i limiti dell'immagine, Aspose lo limita silenziosamente, ma perderai dati. Un rapido controllo di coerenza può prevenirlo:

```java
if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
    regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
    throw new IllegalArgumentException("ROI exceeds image dimensions.");
}
```

## Passo 4 – Elaborare l'Immagine

Con tutto impostato, chiediamo al motore di fare la sua magia.

```java
// Step 4: Run OCR on the defined ROI
OcrResult ocrResult = ocrEngine.process();
```

La chiamata `process()` restituisce un oggetto `OcrResult` che contiene il testo estratto, i punteggi di confidenza e persino le bounding box per ogni parola, se ti servono in seguito.

## Passo 5 – Stampare il Testo Estratto

Infine, stampa il risultato. In un'app reale potresti salvarlo in un database o inviarlo a un altro servizio, ma per questo tutorial basta un output sulla console.

```java
// Step 5: Display the recognized text
System.out.println("ROI text:");
System.out.println(ocrResult.getText());
```

**Output atteso** (supponendo che il rettangolo abbia catturato l'importo totale su una ricevuta):

```
ROI text:
$12.34
```

Se il ROI è vuoto o l'immagine è sfocata, vedrai una stringa vuota o caratteri illeggibili. Regola il rettangolo, migliora la qualità dell'immagine o abilita le opzioni di pre‑elaborazione di Aspose (ad esempio, `setAutoSkewCorrection(true)`).

## Esempio Completo Funzionante

Di seguito trovi il programma completo, pronto per l'esecuzione. Copialo in un file chiamato `RoiDemo.java`, regola il percorso dell'immagine e esegui `javac RoiDemo.java && java RoiDemo`.

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

/**
 * Demo: Extract text from a specific rectangle (ROI) in an image using Aspose OCR.
 * Adjust the rectangle coordinates to match the area you want to read.
 */
public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        // Replace YOUR_DIRECTORY with the actual folder containing receipt.jpg
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.jpg"));

        // Step 3: Define the region of interest where text is expected
        // (x, y, width, height) in pixels
        Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
        ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);

        // Optional sanity check – ensures ROI fits inside the image
        if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
            regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
            throw new IllegalArgumentException("ROI exceeds image dimensions.");
        }

        // Step 4: Perform OCR on the defined ROI
        OcrResult ocrResult = ocrEngine.process();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

> **Verifica del risultato:** Dopo l'esecuzione, confronta l'output della console con il testo reale all'interno del rettangolo. Se corrispondono, hai estratto con successo **testo da immagine** usando Aspose OCR.

## Domande Frequenti & Suggerimenti

### E se devo elaborare più ROI nella stessa immagine?
Crea un nuovo `Rectangle` per ogni area, chiama nuovamente `setRegionOfInterest` e riesegui `process()`. Il motore riutilizza gli stessi dati dell'immagine, quindi le prestazioni rimangono rapide.

### Come gestisce Aspose lingue o font diversi?
Puoi cambiare il modello linguistico tramite `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.English)`. Per script non latini, carica il pacchetto linguistico appropriato (disponibile nella pagina di download di Aspose).

### La libreria supporta input PDF?
Sì—Aspose OCR può accettare stream PDF direttamente. Basta sostituire `ImageStream.fromFile` con `ImageStream.fromPdfFile("doc.pdf")` e, opzionalmente, specificare il numero di pagina.

### Posso migliorare l'accuratezza su scansioni di bassa qualità?
Abilita la pre‑elaborazione:

```java
ocrEngine.getEngineOptions().setAutoSkewCorrection(true);
ocrEngine.getEngineOptions().setBinarizationMethod(BinarizationMethod.Otsu);
```

## Conclusione

Abbiamo appena percorso un **aspose ocr tutorial** completo che mostra come **estrarre testo da un'immagine**, **caricare l'immagine per l'OCR** e **leggere testo da rettangolo** usando Java. I passaggi chiave sono: inizializzare il motore, fornirgli un'immagine, definire una regione di interesse, elaborare e infine stampare il risultato.

Da qui potresti esplorare:

* **Elaborazione batch** – iterare su una cartella di ricevute e memorizzare ogni totale in un database.  
* **Rilevamento dinamico di ROI** – utilizzare librerie di elaborazione immagini (OpenCV) per individuare automaticamente i blocchi di testo.  
* **Post‑elaborazione** – applicare regex o fuzzy matching per pulire le stranezze dell'OCR.

Prova queste idee, regola il rettangolo per adattarlo ai tuoi documenti e avrai una solida pipeline di estrazione del testo in pochissimo tempo. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}