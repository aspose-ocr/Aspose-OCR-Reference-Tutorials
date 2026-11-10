---
category: general
date: 2026-06-16
description: Impara come eseguire l'OCR su file immagine in Java. Questo tutorial
  copre il riconoscimento del testo da PNG, l'estrazione del testo dall'immagine,
  la conversione dell'immagine in testo e il caricamento dell'immagine per l'OCR.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: it
og_description: Esegui OCR su un'immagine usando Java. Questa guida mostra come riconoscere
  il testo da PNG, estrarre il testo dall'immagine e convertire l'immagine in testo
  con un esempio pronto all'uso.
og_title: Esegui OCR su un'immagine in Java – Tutorial completo di programmazione
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  headline: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  name: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'If `hello.png` contains the phrase “Hello, OCR world!”, the console will
      display something like:'
  - name: 5.1 Dealing with Low‑Resolution Images
    text: 'If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale
      the image before feeding it to the engine:'
  - name: 5.2 Multi‑Language Documents
    text: 'If you anticipate French or German text, simply add the language codes
      to `setLanguage`:'
  - name: 5.3 Skipping Empty Pages
    text: 'Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty
      image saves processing time:'
  type: HowTo
tags:
- Java
- OCR
- Image Processing
title: Esegui OCR su un'immagine in Java – Guida completa passo passo
url: /it/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine in Java – Guida Completa Passo‑per‑Passo

Ti è mai capitato di dover **eseguire OCR su immagine** ma non sapevi quale libreria Java scegliere? Non sei il solo. Che tu stia costruendo uno scanner per ricevute, un archivio di documenti, o semplicemente sia curioso di trasformare foto in testo ricercabile, imparare a **eseguire OCR su immagine** con Java è una competenza molto utile.

In questo tutorial vedremo tutto ciò che serve per **eseguire OCR su immagine**: caricare l’immagine, configurare il motore, riconoscere il testo e infine stampare il risultato. Alla fine sarai in grado di **riconoscere testo da PNG**, **estrarre testo da immagine** e **convertire immagine in testo** con poche righe di codice.

## Prerequisiti

- Java 17 o superiore (il codice si compila con qualsiasi JDK recente)
- Maven installato (o il tuo tool di build preferito)
- Familiarità di base con la sintassi Java
- Un file PNG da testare (lo chiameremo `hello.png`)

> **Consiglio:** Se non hai un PNG a disposizione, creane uno facendo uno screenshot di qualsiasi testo e salvandolo come `hello.png` in una cartella chiamata `resources`.

## Cosa Costruiremo

Una piccola applicazione console chiamata `OcrDemo` che:

1. **Carica immagine per OCR** – legge un PNG dal disco.
2. **Esegue OCR su immagine** – utilizza il motore Tesseract tramite Tess4J.
3. **Estrae testo da immagine** – restituisce una `String` con il contenuto riconosciuto.
4. Stampa il risultato sulla console.

Iniziamo.

## Passo 1: Configurare il Progetto e Aggiungere Tess4J

Per prima cosa, crea un nuovo progetto Maven (o Gradle, se preferisci). Aggiungi la dipendenza Tess4J, che avvolge il popolare motore OCR Tesseract.

```xml
<!-- pom.xml -->
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>ocr-demo</artifactId>
  <version>1.0.0</version>
  <properties>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
  </properties>

  <dependencies>
    <!-- Tess4J – Java wrapper for Tesseract OCR -->
    <dependency>
      <groupId>net.sourceforge.tess4j</groupId>
      <artifactId>tess4j</artifactId>
      <version>5.5.1</version>
    </dependency>
  </dependencies>
</project>
```

> **Perché Tess4J?** È attivamente mantenuto, funziona su più piattaforme e fornisce una pulita API Java per i compiti di **eseguire OCR su immagine**.

## Passo 2: Preparare la Logica di Caricamento Immagine

Ora scriveremo un metodo di supporto che **carica immagine per OCR**. Il metodo utilizza `ImageIO` di Java per leggere un PNG in un `BufferedImage`.

```java
package com.example.ocr;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Utility class responsible for loading images from the file system.
 */
public final class ImageLoader {

    private ImageLoader() { /* utility class */ }

    /**
     * Loads a PNG (or any supported format) from the given path.
     *
     * @param path absolute or relative path to the image file
     * @return BufferedImage instance ready for OCR processing
     * @throws IOException if the file cannot be read
     */
    public static BufferedImage load(String path) throws IOException {
        File imgFile = new File(path);
        if (!imgFile.exists()) {
            throw new IOException("Image file not found: " + path);
        }
        return ImageIO.read(imgFile);
    }
}
```

Nota come il nome del metodo rifletta chiaramente l’intento di **caricare immagine per OCR**, rendendo il codice auto‑documentante.

## Passo 3: Configurare il Motore OCR per **Eseguire OCR su Immagine**

Con l’immagine a disposizione, creiamo un’istanza `Tesseract`, abilitiamo il rilevamento automatico della lingua e chiamiamo `doOCR`. Questo è il cuore di come **eseguire OCR su immagine**.

```java
package com.example.ocr;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

/**
 * Wrapper around Tess4J that abstracts the OCR workflow.
 */
public final class OcrEngine {

    private final ITesseract tesseract;

    public OcrEngine() {
        tesseract = new Tesseract();

        // Use the bundled tessdata folder (you can also point to a custom one)
        tesseract.setDatapath("tessdata");

        // Enable automatic language detection – improves accuracy across multilingual images
        tesseract.setLanguage("eng"); // fallback language
        tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
        tesseract.setPageSegMode(ITesseract.PSM_AUTO);
    }

    /**
     * Performs OCR on the supplied BufferedImage and returns the recognized text.
     *
     * @param image image to be processed
     * @return the text extracted from the image
     * @throws TesseractException if OCR fails
     */
    public String recognize(BufferedImage image) throws TesseractException {
        return tesseract.doOCR(image);
    }
}
```

> **Perché abilitare l’auto‑rilevamento?** Permette al motore di scegliere il modello linguistico migliore per l’immagine, utile soprattutto quando **converti immagine in testo** da fonti che mescolano inglese e altri alfabeti.

## Passo 4: Mettere Tutto Insieme – L’Applicazione Principale

Ecco il punto di ingresso che **riconosce testo da PNG**, **estrae testo da immagine** e infine stampa il risultato. Questo è l’esempio completo e eseguibile.

```java
package com.example.ocr;

import net.sourceforge.tess4j.TesseractException;
import java.awt.image.BufferedImage;
import java.io.IOException;

/**
 * Demo application that shows how to perform OCR on image files.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Path to the PNG you want to process
        String imagePath = "resources/hello.png";

        try {
            // Step 1: Load image for OCR
            BufferedImage image = ImageLoader.load(imagePath);

            // Step 2: Create OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Step 3: Perform OCR on image and retrieve the text
            String recognizedText = engine.recognize(image);

            // Step 4: Output the recognized text to the console
            System.out.println("=== Recognized Text ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

### Output Atteso

Se `hello.png` contiene la frase “Hello, OCR world!”, la console mostrerà qualcosa di simile:

```
=== Recognized Text ===
Hello, OCR world!
```

L’output esatto può variare leggermente a seconda della qualità dell’immagine, ma dovresti vedere il testo inserito nel PNG.

## Passo 5: Gestire i Casi Edge più Comuni

### 5.1 Gestire Immagini a Bassa Risoluzione

Se il PNG di origine è sfocato, la precisione dell’OCR diminuisce. Una soluzione rapida è ingrandire l’immagine prima di passarla al motore:

```java
import java.awt.Graphics2D;
import java.awt.RenderingHints;

public static BufferedImage upscale(BufferedImage original, int factor) {
    int width = original.getWidth() * factor;
    int height = original.getHeight() * factor;
    BufferedImage scaled = new BufferedImage(width, height, original.getType());
    Graphics2D g = scaled.createGraphics();
    g.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                       RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g.drawImage(original, 0, 0, width, height, null);
    g.dispose();
    return scaled;
}
```

Chiama `upscale(image, 2)` prima di `engine.recognize(image)` per migliorare i risultati.

### 5.2 Documenti Multilingue

Se prevedi testo in francese o tedesco, aggiungi semplicemente i codici lingua a `setLanguage`:

```java
tesseract.setLanguage("eng+fra+deu");
```

Il motore proverà così a **estrarre testo da immagine** usando i modelli linguistici combinati.

### 5.3 Saltare Pagine Vuote

A volte una pagina PDF scansionata si traduce in un PNG vuoto. Rilevare un’immagine vuota salva tempo di elaborazione:

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## Passo 6: Impacchettare ed Eseguire l’Applicazione

1. **Compila:** `mvn clean compile`
2. **Esegui:** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

Assicurati che la cartella `tessdata` (contenente i file di lingua) sia accanto al JAR compilato o specifica il suo percorso assoluto in `OcrEngine`.

## Conclusione

Ora disponi di un modello solido, pronto per la produzione, per **eseguire OCR su immagine** con Java. Dalla **caricamento immagine per OCR** al **riconoscere testo da PNG**, abbiamo coperto come **estrarre testo da immagine**, **convertire immagine in testo** e gestire scenari difficili come scansioni a bassa risoluzione o contenuti multilingue.

Prossimamente potresti esplorare:

- **Elaborazione batch** – iterare su una directory di PNG e scrivere ogni risultato in un file `.txt`.
- **Generazione PDF** – incorporare il testo estratto in PDF ricercabili.
- **Servizi OCR cloud** – confrontare le prestazioni locali di Tesseract con API come Google Vision o Azure Cognitive Services.

Sentiti libero di sperimentare, modificare i parametri e condividere i tuoi risultati. Buona programmazione, e che le tue immagini si trasformino sempre in testo pulito e ricercabile!

![Diagramma che mostra il flusso di lavoro OCR per eseguire OCR su immagine](https://example.com/ocr-workflow.png "esempio di eseguire OCR su immagine")


## Cosa Dovresti Imparare Dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑per‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}