---
category: general
date: 2026-10-11
description: Scopri come eseguire l'OCR su un'immagine PNG in Java, estrarre il testo
  dall'immagine e convertire l'immagine in testo con un semplice esempio di OcrEngine.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: it
lastmod: 2026-10-11
og_description: Come eseguire l'OCR su un'immagine PNG in Java, estrarre il testo
  dall'immagine e convertire l'immagine in testo usando un esempio conciso e pronto
  all'uso.
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: Come eseguire l'OCR su un'immagine PNG in Java – guida completa
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  headline: How to perform OCR on a PNG image in Java
  type: TechArticle
- description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  name: How to perform OCR on a PNG image in Java
  steps:
  - name: 4.1 Handling low‑resolution PNGs
    text: 'Tesseract performs best on images with at least 300 DPI. If your source
      PNG is smaller, upscale it before OCR:'
  - name: 4.2 Extracting non‑English text
    text: 'To **extract text from image** that contains other languages, download
      the appropriate `.traineddata` files and set the language code:'
  - name: 4.3 Batch processing multiple PNGs
    text: 'If you need to **recognize text from PNG** files in a folder, iterate over
      the directory:'
  - name: 4.4 Dealing with OCR errors
    text: 'Typical OCR mistakes include misreading `0` (zero) as `O` or `1` as `l`.
      Post‑processing with regular expressions can clean the result:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Text Extraction
title: Come eseguire l'OCR su un'immagine PNG in Java
url: /it/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR su un'immagine PNG in Java

Se hai bisogno di **eseguire OCR** su un file immagine, imparare **come eseguire OCR** in Java è fondamentale per molte attività di automazione. Che tu stia digitalizzando ricevute, indicizzando documenti scansionati o creando un archivio fotografico ricercabile, la capacità di **estrarre testo da immagine** salva innumerevoli ore di lavoro manuale.

Questo tutorial ti mostra una soluzione completa e pronta all'uso che carica un PNG, esegue un motore OCR e **riconosce il testo da file PNG**. Vedrai anche come **convertire immagine in testo** e gestire problemi comuni come input a bassa risoluzione o caratteri non ASCII.

## Cosa otterrai

Al termine di questa guida sarai in grado di:

* **caricare immagine java** codice che legge un PNG dal disco,
* inizializzare un motore OCR leggero,
* **estrarre testo da immagine** e stampare il risultato sulla console,
* adattare la soluzione ad altri formati immagine o a elaborazioni batch.

Non sono richiesti servizi esterni—solo una singola libreria OCR open‑source (Tess4J) e il runtime Java SE.

---

## Prerequisiti

* Java 17 o superiore (il codice compila con JDK 17).
* Maven o Gradle per la gestione delle dipendenze.
* Familiarità di base con la riga di comando e l'IDE di tua scelta.
* La libreria `tess4j` (un wrapper Java per Tesseract). Aggiungi la seguente dipendenza Maven:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Se usi Gradle, l'equivalente è:

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

Hai inoltre bisogno dei file di dati di Tesseract (`.traineddata`). Scarica il pacchetto di dati inglese dal repository ufficiale e posizionalo in una cartella chiamata `tessdata` nella radice del progetto.

---

## Passo 1: Caricare l'immagine in Java

Caricare un PNG è semplice con la classe standard `ImageIO`. Il codice qui sotto dimostra **caricare immagine java** in modo sicuro e consapevole delle eccezioni:

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Reads a PNG file from the given path and returns a BufferedImage.
 *
 * @param path absolute or relative path to the PNG file
 * @return BufferedImage representation of the file
 * @throws Exception if the file cannot be read or is not a PNG
 */
private static BufferedImage loadPng(String path) throws Exception {
    File imgFile = new File(path);
    if (!imgFile.exists()) {
        throw new IllegalArgumentException("File not found: " + path);
    }
    BufferedImage img = ImageIO.read(imgFile);
    if (img == null) {
        throw new IllegalArgumentException("Unsupported image format or corrupt file: " + path);
    }
    return img;
}
```

**Perché è importante:** `ImageIO.read` rileva automaticamente il formato dell'immagine, ma controlliamo esplicitamente `null` per evitare fallimenti silenziosi quando il PNG è corrotto. Questo schema è una buona pratica quando **carichi immagine java** per OCR.

---

## Passo 2: Inizializzare il motore OCR

Tess4J avvolge il binario nativo di Tesseract, esponendo una semplice API Java. Il metodo seguente crea un'istanza `Tesseract`, la punta alla cartella `tessdata` e configura la lingua su English:

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;

/**
 * Configures and returns a ready‑to‑use Tesseract instance.
 *
 * @return configured ITesseract object
 */
private static ITesseract createOcrEngine() {
    ITesseract tesseract = new Tesseract();
    // Path to the folder that contains .traineddata files
    tesseract.setDatapath("tessdata");
    // Language code – "eng" for English; you can add more languages later
    tesseract.setLanguage("eng");
    // Optional: increase OCR accuracy for PNGs with low DPI
    tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
    return tesseract;
}
```

**Perché lo facciamo:** Inizializzare il motore una sola volta e riutilizzarlo per più immagini riduce il sovraccarico di avvio. La chiamata `setOcrEngineMode` seleziona la modalità predefinita, che funziona bene per la maggior parte dei PNG. Se incontri scansioni rumorose, puoi sperimentare altre modalità (ad es., `OEM_LSTM_ONLY`).

---

## Passo 3: Eseguire OCR e **riconoscere testo da PNG**

Ora combiniamo il caricatore di immagini e il motore OCR. Il metodo qui sotto esegue OCR su un `BufferedImage` e restituisce la stringa estratta:

```java
/**
 * Runs OCR on the supplied image and returns the recognized text.
 *
 * @param image BufferedImage containing the PNG to process
 * @param tesseract configured OCR engine
 * @return plain‑text result of OCR
 * @throws Exception if OCR fails
 */
private static String extractText(BufferedImage image, ITesseract tesseract) throws Exception {
    // Tess4J can directly accept a BufferedImage
    return tesseract.doOCR(image);
}
```

**Esempio completo eseguibile**

```java
import java.awt.image.BufferedImage;
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.TesseractException;

public class OcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the PNG file
            BufferedImage image = loadPng("sample.png");

            // 2️⃣ Create and configure the OCR engine
            ITesseract ocrEngine = createOcrEngine();

            // 3️⃣ Recognize text from PNG
            String recognizedText = extractText(image, ocrEngine);

            // 4️⃣ Display the result – this is the **convert image to text** step
            System.out.println("=== OCR RESULT ===");
            System.out.println(recognizedText);
        } catch (Exception e) {
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps -----
    // loadPng, createOcrEngine, extractText (copy-pasted here for completeness)
    // ... (methods omitted for brevity; see the sections above) ...
}
```

**Output previsto**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

La console mostrerà i caratteri esatti che il motore ha estratto da `sample.png`. Se il PNG contiene una sola parola, l'output sarà quella parola seguita da un newline.

---

## Passo 4: Varianti comuni e casi limite

### 4.1 Gestione di PNG a bassa risoluzione

Tesseract funziona al meglio su immagini con almeno 300 DPI. Se il tuo PNG di origine è più piccolo, ingrandiscilo prima dell'OCR:

```java
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.RenderingHints;

private static BufferedImage upscale(BufferedImage src, int scaleFactor) {
    int width = src.getWidth() * scaleFactor;
    int height = src.getHeight() * scaleFactor;
    Image tmp = src.getScaledInstance(width, height, Image.SCALE_SMOOTH);
    BufferedImage resized = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
    Graphics2D g2d = resized.createGraphics();
    g2d.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                         RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g2d.drawImage(tmp, 0, 0, null);
    g2d.dispose();
    return resized;
}
```

Applica `upscale(image, 2)` prima di chiamare `extractText` per migliorare l'accuratezza.

### 4.2 Estrarre testo non inglese

Per **estrarre testo da immagine** che contiene altre lingue, scarica i file `.traineddata` appropriati e imposta il codice lingua:

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 Elaborazione batch di più PNG

Se devi **riconoscere testo da PNG** in una cartella, itera sulla directory:

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 Gestire errori di OCR

Gli errori tipici di OCR includono la lettura errata di `0` (zero) come `O` o di `1` come `l`. Un post‑processing con espressioni regolari può pulire il risultato:

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

---

## Suggerimenti professionali per un OCR affidabile in Java

| Suggerimento | Motivo |
|--------------|--------|
| **Usa un PNG lossless** | Gli artefatti di compressione nei JPEG possono confondere il motore. |
| **Rimuovi i bordi bianchi** | Spazi bianchi superflui aumentano il tempo di elaborazione e possono generare falsi positivi. |
| **Imposta `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`** solo quando il layout è sconosciuto; altrimenti scegli una modalità specifica (es., `PSM_SINGLE_BLOCK`). |
| **Cache l'istanza `ITesseract`** |  |

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come leggere il testo da un'immagine in Java usando Aspose OCR – Guida completa](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Come usare OCR in Java – Riconoscere rapidamente il testo da un'immagine](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [OCR di immagini batch in Java – Estrarre rapidamente il testo da file PNG](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}