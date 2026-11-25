---
category: general
date: 2026-07-21
description: Estrai il testo da un'immagine usando Java OCR. Scopri come convertire
  PNG in testo, leggere il testo da PNG, caricare l'immagine per l'OCR ed eseguire
  l'OCR sull'immagine in pochi passaggi.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: it
lastmod: 2026-07-21
og_description: Estrai testo da un'immagine con Java. Questa guida ti mostra come
  convertire PNG in testo, leggere il testo da PNG, caricare l'immagine per OCR e
  eseguire OCR sull'immagine in modo efficiente.
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: Estrai il testo da un'immagine in Java – Tutorial OCR passo passo
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  headline: Extract Text from Image in Java – Complete OCR Guide
  type: TechArticle
- description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  name: Extract Text from Image in Java – Complete OCR Guide
  steps:
  - name: Low‑Quality Images
    text: 'If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix
      is to pre‑process the image:'
  - name: Multi‑Language Support
    text: Tess4J can handle many languages. Just download the appropriate `.traineddata`
      file and point `tesseract.setLanguage("spa")` for Spanish, for example.
  - name: Large PDFs or Multi‑Page Images
    text: If you need to **extract text from image** files inside a PDF, split each
      page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Estrai il testo da un'immagine in Java – Guida completa all'OCR
url: /it/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrarre testo da immagine in Java – Guida completa OCR

Hai mai avuto bisogno di **estrarre testo da immagine** ma non eri sicuro quale libreria Java scegliere? Non sei solo. Che tu stia digitalizzando ricevute, scansionando PDF o creando un archivio ricercabile, estrarre testo da un PNG è un problema quotidiano per molti sviluppatori.

In questo tutorial percorreremo una soluzione pratica che ti permette di **convertire PNG in testo**, **leggere testo da PNG**, **caricare immagine per OCR** e **eseguire OCR su immagine** — il tutto con poche righe di codice Java pulito. Alla fine avrai un programma eseguibile da inserire in qualsiasi progetto.

## Cosa costruirai

Creeremo una piccola applicazione console Java che:

1. Carica un file PNG dal disco.  
2. Invia l'immagine a un motore OCR (Tess4J, un wrapper Java per Tesseract).  
3. Stampa il testo riconosciuto sulla console.

Nessun servizio esterno, nessuna magia — solo puro Java e un motore OCR open‑source.

## Prerequisiti

- **Java 17** o successiva (il codice compila anche con versioni precedenti, ma Java 17 ti offre le ultime novità del linguaggio).  
- **Maven** o **Gradle** per la gestione delle dipendenze.  
- Un PNG di esempio chiamato `sample.png` posizionato in una cartella a cui puoi fare riferimento (ad esempio `src/main/resources`).  
- Familiarità di base con il metodo `main` di Java e la gestione delle eccezioni.

Se qualcuno di questi ti è sconosciuto, non preoccuparti — ogni passaggio include un breve riepilogo.

## Passo 1: Configura il progetto e aggiungi la libreria OCR

Per prima cosa, crea un nuovo progetto Maven (o Gradle se preferisci). Aggiungi la dipendenza Tess4J, che include i binari di Tesseract per te.

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
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

> **Suggerimento:** Se stai usando Gradle, la riga equivalente è `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'`.

Aggiungendo questa libreria ottieni la classe `Tesseract`, che gestisce il lavoro pesante di **eseguire OCR su dati immagine**.

## Passo 2: Caricare immagine per OCR

Ora dobbiamo **caricare immagine per OCR**. Tess4J funziona con `java.awt.image.BufferedImage`, quindi leggeremo il PNG usando `ImageIO`.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class OcrDemo {

    /**
     * Loads a PNG file from the given path and returns a BufferedImage.
     *
     * @param path absolute or relative path to the PNG file
     * @return BufferedImage containing the image data
     * @throws IOException if the file cannot be read
     */
    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image to be recognized
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }
```

Il metodo sopra isola in modo pulito la logica di **caricare immagine per OCR**, rendendo il resto del codice più facile da testare. Nota il commento — rispecchia lo snippet originale ampliandolo per chiarezza.

## Passo 3: Eseguire OCR su immagine

Con l'immagine in memoria, ora possiamo **eseguire OCR su immagine**. L'istanza `Tesseract` è il nostro motore; la configureremo per usare i dati di lingua inglese predefiniti forniti con Tess4J.

```java
    /**
     * Runs OCR on the supplied BufferedImage and returns the extracted text.
     *
     * @param image the image to analyze
     * @return plain text recognized from the image
     * @throws TesseractException if the OCR process fails
     */
    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();

        // Optional: set the datapath if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");

        // Step 4: Run OCR and capture the recognized text
        return tesseract.doOCR(image);
    }
```

Qui abbiamo unito i passaggi originali “Step 1” e “Step 4” in un unico metodo, perché l'oggetto `Tesseract` è poco costoso da creare e vogliamo che il codice rimanga compatto. Il commento fa ancora riferimento ai passaggi originali per tracciabilità.

## Passo 4: Metti tutto insieme – Metodo main

Infine, uniamo tutto in `main`. Qui **leggerai testo da PNG** e vedrai il risultato stampato sulla console.

```java
    public static void main(String[] args) {
        // Adjust the path to point at your PNG file
        String imagePath = "src/main/resources/sample.png";

        try {
            // Load the PNG image
            BufferedImage image = loadImage(imagePath);

            // Extract text from the image
            String recognizedText = extractText(image);

            // Step 5: Display the extracted text
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR error: " + e.getMessage());
        }
    }
}
```

Quando esegui `mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"` (o l'equivalente Gradle), dovresti vedere qualcosa del genere:

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

Quell'output dimostra che hai estratto con successo **testo da immagine**, **convertito PNG in testo** e **letto testo da PNG** in un unico programma ordinato.

## Gestire casi limite comuni

### Immagini a bassa qualità

Se il PNG è sfocato o ha basso contrasto, l'accuratezza dell'OCR diminuisce. Una rapida soluzione è pre‑processare l'immagine:

```java
// Example: Convert to grayscale and apply a binary threshold
BufferedImage gray = new BufferedImage(
        image.getWidth(), image.getHeight(),
        BufferedImage.TYPE_BYTE_GRAY);
Graphics2D g = gray.createGraphics();
g.drawImage(image, 0, 0, null);
g.dispose();

// Simple binary threshold
for (int y = 0; y < gray.getHeight(); y++) {
    for (int x = 0; x < gray.getWidth(); x++) {
        int rgb = gray.getRGB(x, y) & 0xFF;
        int binary = rgb < 128 ? 0x000000 : 0xFFFFFF;
        gray.setRGB(x, y, binary);
    }
}
String text = extractText(gray);
```

### Supporto multilingua

Tess4J può gestire molte lingue. Basta scaricare il file `.traineddata` appropriato e impostare `tesseract.setLanguage("spa")` per lo spagnolo, ad esempio.

### PDF grandi o immagini multipagina

Se devi **estrarre testo da immagine** contenuti in un PDF, dividi prima ogni pagina in PNG (usando PDFBox) e poi passa ogni PNG alla stessa routine OCR.

## Esempio completo funzionante (tutto il codice in un unico posto)

Di seguito trovi la classe Java completa, pronta per l'esecuzione. Copiala e incollala in `src/main/java/com/example/ocrdemo/OcrDemo.java` e sei pronto a partire.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Demonstrates how to extract text from image (PNG) using Java and Tess4J.
 */
public class OcrDemo {

    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image for OCR
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }

    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();
        // Uncomment and set if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");
        // Step 4: Perform OCR on image
        return tesseract.doOCR(image);
    }

    public static void main(String[] args) {
        // Path to the PNG you want to convert to text
        String imagePath = "src/main/resources/sample.png";

        try {
            BufferedImage image = loadImage(imagePath);
            String recognizedText = extractText(image);
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("Error during OCR: " + e.getMessage());
        }
    }
}
```

Eseguendo la classe stampa il risultato OCR, confermando che hai eseguito con successo **OCR su immagine** e trasformato il tuo PNG in testo modificabile.

## Riepilogo e prossimi passi

Abbiamo iniziato **estrarre testo da immagine** usando una configurazione Java leggera. Ora sai come **caricare immagine per OCR**, **eseguire OCR su immagine** e **leggere testo da PNG** — blocchi fondamentali per qualsiasi pipeline di digitalizzazione dei documenti.

Vuoi andare oltre? Prova queste idee:

- **Elaborazione batch:** Scorri una directory di PNG e scrivi ogni risultato in un file `.txt`.  
- **Integrare con un database:** Memorizza le stringhe estratte insieme ai metadati per archivi ricercabili.  
- **Combinare con NLP:** Invia l'output OCR a un modello di analisi del sentiment per rapidi insight.  

Ognuna di queste estensioni si basa sugli stessi concetti fondamentali trattati, quindi sei pronto a sperimentare.

---

*Happy coding! If you hit any snags

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completo e funzionante con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrarre testo da immagine Java con Aspose.OCR modalità rilevamento aree](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [immagine a testo java: Converti immagine in testo con Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Come fare OCR del testo immagine con lingua usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}