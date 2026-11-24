---
category: general
date: 2026-09-10
description: Eseguire OCR su un'immagine usando Aspose OCR per Java. Impara a riconoscere
  il testo da JPEG, estrarre il testo dall'immagine e convertire l'immagine in testo
  in modo efficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- recognize text from JPEG
- extract text from image
- convert image to text
- load image for OCR
language: it
lastmod: 2026-09-10
og_description: Esegui OCR su un'immagine con Aspose OCR Java. Questo tutorial mostra
  come riconoscere il testo da un JPEG, estrarre il testo dall'immagine e convertire
  l'immagine in testo in poche righe di codice.
og_image_alt: Screenshot of Java code that performs OCR on an image using Aspose OCR
og_title: Esegui OCR su un'immagine con Aspose OCR – Guida Java
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  headline: How to perform OCR on image with Aspose OCR in Java
  type: TechArticle
- description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  name: How to perform OCR on image with Aspose OCR in Java
  steps:
  - name: Prerequisites
    text: '* Java Development Kit (JDK) 8 or later. * Maven or Gradle to manage dependencies
      (the example uses Maven). * A valid Aspose OCR for Java license (or a temporary
      evaluation key). * An image file named `sample.jpg` placed in a known directory.'
  - name: Load image for OCR
    text: '```java // Step 1: Load the image you want to process String imagePath
      = "YOUR_DIRECTORY/sample.jpg"; ImageStream imageStream = ImageStream.fromFile(imagePath);
      ```'
  - name: Create and configure the OCR engine
    text: '```java // Step 2: Create an OCR engine instance OcrEngine engine = new
      OcrEngine();'
  - name: Recognize text from JPEG
    text: '```java // Step 3: Attach the image to the engine engine.setImage(imageStream);'
  - name: Extract text from image and output
    text: '```java // Step 5: Output the recognized text System.out.println("=== Recognized
      Text ==="); System.out.println(result.getText()); ```'
  - name: Expected output
    text: 'Assuming `sample.jpg` contains the text “Hello World”, the console will
      display:'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: Come eseguire l'OCR su un'immagine con Aspose OCR in Java
url: /it/java/ocr-operations/how-to-perform-ocr-on-image-with-aspose-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR su immagine con Aspose OCR in Java

Se hai bisogno di **perform OCR on image** file in un'applicazione Java, questa guida fornisce una soluzione completa, pronta‑all'uso. Vedrai come **recognize text from JPEG** file, **extract text from image** dati e **convert image to text** usando l'API moderna di Aspose OCR.

Il tutorial guida attraverso ogni passaggio necessario—dall'importazione dell'immagine alla stampa del testo riconosciuto—così puoi integrare la funzionalità OCR senza cercare risorse aggiuntive. Non sono necessari strumenti esterni oltre alla libreria Aspose OCR per Java.

## Cosa otterrai

* **Load an image for OCR** direttamente dal file system.  
* Abilita il preprocessing di Aspose OCR (ad es., denoising) per migliorare l'accuratezza.  
* **Recognize text from JPEG** e altri formati raster.  
* **Extract text from image** e stampalo sulla console.  
* Comprendi come **convert image to text** in un esempio di codice pronto per la produzione.

### Prerequisiti

* Java Development Kit (JDK) 8 o successivo.  
* Maven o Gradle per gestire le dipendenze (l'esempio utilizza Maven).  
* Una licenza valida di Aspose OCR per Java (o una chiave di valutazione temporanea).  
* Un file immagine chiamato `sample.jpg` collocato in una directory nota.

> **Pro tip:** Usa JPEG ad alta risoluzione (300 dpi o superiore) per i migliori tassi di riconoscimento.  

## Passo 1: Aggiungi Aspose OCR al tuo progetto

Se gestisci le dipendenze con Maven, inserisci il seguente snippet nel tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version>
</dependency>
```

Per Gradle, aggiungi:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Queste coordinate scaricano l'ultima versione stabile della libreria Aspose OCR, che include le funzionalità di preprocessing utilizzate più avanti.

## Esegui OCR su immagine – passo‑per‑passo

Le sezioni seguenti scompongono il programma completo. Ogni blocco è un pezzo autonomo che puoi copiare, incollare ed eseguire.

### Carica immagine per OCR

```java
// Step 1: Load the image you want to process
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ImageStream imageStream = ImageStream.fromFile(imagePath);
```

*Perché è importante:*  
`ImageStream.fromFile` legge i byte grezzi del JPEG e li prepara per il motore OCR. Il metodo funziona con qualsiasi formato raster supportato da Aspose OCR, quindi puoi sostituire il JPEG con PNG o BMP senza modificare il codice.

### Crea e configura il motore OCR

```java
// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();

// Enable preprocessing to improve accuracy (e.g., denoising)
engine.getPreprocessing().setDenoise(true);
```

*Perché è importante:*  
L'istanziazione di `OcrEngine` alloca il motore di riconoscimento principale. Abilitare il flag **denoise** rimuove il rumore visivo che spesso interferisce con il rilevamento dei caratteri, specialmente nei JPEG scansionati.

### Riconosci testo da JPEG

```java
// Step 3: Attach the image to the engine
engine.setImage(imageStream);

// Step 4: Perform OCR recognition
OcrResult result = engine.recognize();
```

*Perché è importante:*  
`engine.setImage` collega i dati dell'immagine al flusso OCR. `engine.recognize()` esegue l'intero processo di riconoscimento, restituendo un `OcrResult` che contiene il testo estratto e le metriche di confidenza.

### Estrai testo dall'immagine e stampa

```java
// Step 5: Output the recognized text
System.out.println("=== Recognized Text ===");
System.out.println(result.getText());
```

*Perché è importante:*  
`result.getText()` fornisce la rappresentazione in testo semplice del contenuto dell'immagine. Stampandolo sulla console dimostra che **convert image to text** è riuscito, e puoi reindirizzare questa stringa a file, database o servizi a valle.

## Esempio completo, eseguibile

Di seguito la classe Java completa che incorpora tutti i passaggi. Sostituisci `YOUR_DIRECTORY` con il percorso assoluto del tuo file JPEG.

```java
import com.aspose.ocr.*;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the image for OCR
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ImageStream imageStream = ImageStream.fromFile(imagePath);

        // Create and configure the OCR engine
        OcrEngine engine = new OcrEngine();
        engine.getPreprocessing().setDenoise(true); // improve accuracy

        // Attach the image and run recognition
        engine.setImage(imageStream);
        OcrResult result = engine.recognize();

        // Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### Output previsto

Assumendo che `sample.jpg` contenga il testo “Hello World”, la console mostrerà:

```
=== Recognized Text ===
Hello World
```

Se l'immagine contiene più righe, ciascuna riga apparirà su una propria linea nell'output.

## Variazioni comuni e casi limite

| Situazione                                 | Modifica consigliata |
|-------------------------------------------|-------------------|
| **Low‑resolution JPEG** (≤150 dpi)        | Aumenta `engine.getPreprocessing().setUpsample(true);` per consentire ad Aspose di ingrandire prima del riconoscimento. |
| **Colored background** (e.g., scanned forms) | Abilita `engine.getPreprocessing().setBinarize(true);` per convertire l'immagine in bianco‑e‑nero. |
| **Non‑Latin script** (e.g., Cyrillic)    | Imposta la lingua: `engine.getLanguage().setLanguage(OcrLanguage.RUSSIAN);`. |
| **Large batch processing**                | Riutilizza una singola istanza di `OcrEngine` su più immagini per ridurre l'overhead di avvio. |
| **Need confidence scores**                | Accedi a `result.getConfidence()` per i valori di confidenza per carattere. |

Queste regolazioni illustrano come puoi **load image for OCR** in diverse condizioni mantenendo comunque **perform OCR on image** in modo affidabile.

## Considerazioni sulle prestazioni

* **Memory usage:** Ogni `ImageStream` mantiene l'intera immagine in memoria. Per file molto grandi (ad es., >10 MB), considera lo streaming dell'immagine a blocchi usando `ImageStream.fromByteArray`.  
* **Thread safety:** `OcrEngine` non è *thread‑safe*. Crea un'istanza separata per thread se prevedi di parallelizzare le attività OCR.  
* **License mode:** La modalità di valutazione limita il numero di pagine elaborate per sessione. Distribuisci una versione con licenza per carichi di lavoro di produzione.

## Conclusione

Ora sai come **perform OCR on image** file in Java usando Aspose OCR. Il tutorial ha coperto il caricamento di un'immagine, l'abilitazione del preprocessing, il riconoscimento del testo da JPEG, l'estrazione del testo e la conversione dell'immagine in testo—tutto in un unico programma conciso.  

Da qui puoi esplorare argomenti correlati come **recognize text from JPEG** in massa, integrare l'output con un indice di ricerca, o combinare OCR con l'elaborazione del linguaggio naturale per pipeline di documenti più intelligenti. Sperimenta le opzioni di preprocessing per ottenere la massima accuratezza per le tue specifiche fonti di immagini.

--- 

*Immagine che illustra l'output del codice*  
![eseguire OCR su immagine usando Aspose OCR Java](image-placeholder.png){alt="eseguire OCR su immagine usando Aspose OCR Java"}

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [riconoscere testo immagine con Aspose OCR – Tutorial OCR Java completo](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Come fare OCR del testo immagine con lingua usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Preprocessare OCR immagine in Java con Aspose OCR – Aumentare precisione ed estrarre testo](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}