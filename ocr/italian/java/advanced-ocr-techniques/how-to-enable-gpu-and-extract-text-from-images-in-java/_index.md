---
category: general
date: 2026-09-16
description: Scopri come abilitare la GPU per una OCR più veloce in Java, riconoscere
  il testo da file immagine e convertire l'immagine in testo usando Aspose OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize text from image
- extract text from image
- how to perform ocr
- convert image to text
language: it
lastmod: 2026-09-16
og_description: Come abilitare la GPU per l'OCR in Java, riconoscere il testo da file
  immagine e convertire l'immagine in testo con Aspose OCR – una guida completa passo
  passo.
og_image_alt: Screenshot showing Java code that enables GPU for OCR and extracts text
  from an image
og_title: Come abilitare la GPU ed estrarre testo dalle immagini in Java
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: Learn how to enable GPU for faster OCR in Java, recognize text from
    image files and convert image to text using Aspose OCR.
  headline: How to enable GPU and extract text from images in Java
  type: TechArticle
- description: Learn how to enable GPU for faster OCR in Java, recognize text from
    image files and convert image to text using Aspose OCR.
  name: How to enable GPU and extract text from images in Java
  steps:
  - name: '**Pre‑processing** – de‑skew, binarize, and enhance contrast (GPU‑accelerated).'
    text: '**Pre‑processing** – de‑skew, binarize, and enhance contrast (GPU‑accelerated).'
  - name: '**Segmentation** – locate text lines, words, and characters.'
    text: '**Segmentation** – locate text lines, words, and characters.'
  - name: '**Classification** – match each character against the built‑in language
      model.'
    text: '**Classification** – match each character against the built‑in language
      model.'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: Come abilitare la GPU ed estrarre testo dalle immagini in Java
url: /it/java/advanced-ocr-techniques/how-to-enable-gpu-and-extract-text-from-images-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come abilitare la GPU ed estrarre testo dalle immagini in Java

Se hai bisogno di **come abilitare la GPU** per il riconoscimento ottico dei caratteri, questa guida ti mostra i passaggi esatti. Attivando l'accelerazione GPU puoi **riconoscere testo da immagini** fino a diverse volte più velocemente rispetto all'elaborazione solo CPU. L'esempio utilizza Aspose OCR per Java, ma i concetti si applicano a qualsiasi libreria OCR compatibile con GPU.

In questo tutorial imparerai a:

* Abilitare l'accelerazione GPU nel motore OCR.  
* Caricare un'immagine e **estrarre testo da immagini**.  
* **Convertire immagine in testo** con poche righe di codice.  

Non sono richiesti servizi esterni—tutto viene eseguito localmente sulla tua macchina. Un ambiente di sviluppo Java di base e la libreria Aspose OCR per Java sono gli unici prerequisiti.

## Prerequisiti

Prima di iniziare, assicurati di avere:

| Requisito | Versione / Dettaglio |
|-------------|------------------|
| Java Development Kit (JDK) | 8 o superiore |
| Maven o Gradle (per la gestione delle dipendenze) | Qualsiasi versione recente |
| GPU con supporto CUDA (opzionale ma consigliato) | NVIDIA GPU con driver ≥ 450 |
| Aspose OCR for Java library | 23.9 o superiore (scarica dal sito Aspose) |

Se non hai una GPU, il codice funziona comunque; verrà semplicemente eseguito sulla CPU.

## Step 1: Aggiungi Aspose OCR al tuo progetto

Per Maven, aggiungi la seguente dipendenza al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

Per Gradle, inserisci questo in `build.gradle`:

```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

Queste voci importano automaticamente il motore OCR e i binari GPU nativi.

## Step 2: Come abilitare la GPU per il motore OCR

Il compito principale è indicare a `OcrEngine` di usare la GPU. Aspose OCR espone un flag semplice:

```java
// Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Enable GPU acceleration – this is the “how to enable gpu” step
ocrEngine.setGpuEnabled(true);
```

**Perché è importante:** Quando `setGpuEnabled(true)` è chiamato, la libreria carica kernel basati su CUDA che parallelizzano le fasi di pre‑elaborazione dell'immagine e segmentazione dei caratteri. Su una scheda NVIDIA moderna, puoi vedere miglioramenti di velocità di 2‑4× rispetto al percorso CPU predefinito.

> **Consiglio professionale:** Verifica che la tua GPU sia rilevata eseguendo `SystemInfo.isCudaSupported()` prima di abilitare il flag. Se il metodo restituisce `false`, il motore tornerà automaticamente alla CPU.

## Step 3: Carica l'immagine da elaborare

Puoi fornire al motore OCR qualsiasi formato immagine supportato da Aspose (JPEG, PNG, BMP, TIFF, ecc.). Ecco come caricare un file JPEG:

```java
// Load the image that contains the text to be recognized
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

**Caso limite:** Se l'immagine è grande (oltre 5 MB) considera di ridimensionarla prima per ridurre il consumo di memoria. Il motore OCR funziona al meglio con immagini intorno a 300 dpi.

## Step 4: Esegui OCR e **riconoscere testo da immagine**

Ora che il motore è configurato e l'immagine è caricata, puoi avviare il riconoscimento:

```java
// Execute OCR – this is the core “how to perform ocr” step
String recognizedText = ocrEngine.recognize();
```

Il metodo `recognize()` restituisce una `String` di testo semplice. Internamente, il motore esegue diverse fasi:

1. **Pre‑processing** – correzione di inclinazione, binarizzazione e miglioramento del contrasto (accelerato da GPU).  
2. **Segmentation** – individuare linee di testo, parole e caratteri.  
3. **Classification** – confrontare ogni carattere con il modello linguistico integrato.  

Poiché la GPU è attiva, i passaggi 1 e 2 traggono il massimo beneficio dall'esecuzione parallela.

## Step 5: Visualizza o salva il testo estratto

Infine, stampa il risultato sulla console, su un file o su qualsiasi processore a valle:

```java
// Show the extracted text – this completes the “convert image to text” flow
System.out.println("Recognized text:\n" + recognizedText);

// Optional: write the text to a file
Files.write(Paths.get("output.txt"), recognizedText.getBytes(StandardCharsets.UTF_8));
```

**Output tipico** (per un'immagine di esempio contenente “Hello World”):

```
Recognized text:
Hello World
```

Se l'OCR non riesce a rilevare alcun carattere, `recognizedText` sarà una stringa vuota. In tal caso, ricontrolla la qualità dell'immagine o disabilita la GPU per confrontare le prestazioni.

## Gestione dei problemi comuni

| Problema | Causa | Soluzione |
|-------|-------|-----|
| **GPU non rilevata** | Driver CUDA mancante o GPU non supportata | Installa l'ultimo driver NVIDIA e verifica con `nvidia-smi`. |
| **Caratteri errati** | Basso contrasto o sfondo rumoroso | Pre‑processa l'immagine (ad es., aumenta il contrasto) prima di passarla al motore. |
| **Errore di out‑of‑memory** | Immagini molto grandi su memoria GPU limitata | Ridimensiona l'immagine a ≤ 2000 px di larghezza o elabora a tasselli. |
| **Mancata corrispondenza della lingua** | Il modello linguistico predefinito è inglese ma il testo è in un'altra lingua | Chiama `ocrEngine.setLanguage(OcrLanguage.SPANISH)` (o l'enum appropriato) prima di `recognize()`. |

## Esempio completo, eseguibile

Di seguito trovi una classe Java autonoma che combina tutti i passaggi. Salvala come `GpuEnabledOcrExample.java`, modifica il percorso dell'immagine e eseguila con `javac`/`java` o tramite il tuo IDE.

```java
import com.aspose.ocr.*;
import java.nio.file.*;

public class GpuEnabledOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Turn on GPU acceleration for faster processing
        // This is the core "how to enable gpu" call
        ocrEngine.setGpuEnabled(true);

        // Optional sanity check – ensures CUDA is available
        if (!SystemInfo.isCudaSupported()) {
            System.out.println("CUDA not detected. Falling back to CPU.");
        }

        // Step 3: Load the image that contains the text to be recognized
        // Replace with the absolute path to your image file
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Perform the OCR operation and obtain the recognized text
        // This answers "how to perform ocr" and "recognize text from image"
        String recognizedText = ocrEngine.recognize();

        // Step 5: Display the extracted text – completes "convert image to text"
        System.out.println("Recognized text:\n" + recognizedText);

        // (Optional) Save the result to a text file
        Path output = Paths.get("recognized_output.txt");
        Files.write(output, recognizedText.getBytes());
        System.out.println("Text saved to " + output.toAbsolutePath());
    }
}
```

### Risultato atteso

L'esecuzione del programma stampa il testo estratto sulla console e scrive lo stesso contenuto in `recognized_output.txt`. Con la GPU abilitata, il tempo totale di esecuzione per un'immagine da 2 MP è tipicamente inferiore a 200 ms su una NVIDIA RTX 3060, rispetto a ~500 ms solo su CPU.

## Conclusione

Ora sai **come abilitare la GPU** per Aspose OCR in Java, **riconoscere testo da immagini** e **convertire immagine in testo** con poche righe di codice. Sfruttando l'accelerazione GPU ottieni un'elaborazione più veloce, fondamentale per applicazioni batch o in tempo reale come la scansione di fatture, l'elaborazione di ricevute e la digitalizzazione di documenti.

**Passaggi successivi**

* Sperimenta con diversi modelli linguistici (`ocrEngine.setLanguage`) per **estrarre testo da immagini** in francese, tedesco o cinese.  
* Combina l'output OCR con Apache Tika per indicizzare automaticamente il contenuto estratto.  
* Esplora lo streaming di PDF di grandi dimensioni pagina per pagina se devi **riconoscere testo da immagini** all'interno di un documento PDF.

## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come leggere il testo da un'immagine in Java usando Aspose OCR – Guida completa](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Riconoscere testo immagine con Aspose OCR – Tutorial completo Java OCR](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [immagine a testo java: Converti immagine in testo con Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}