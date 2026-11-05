---
category: general
date: 2026-08-28
description: Scopri come estrarre testo da immagini png in Java usando Aspose OCR.
  Questo tutorial copre l'elaborazione batch OCR, la lettura delle immagini da una
  cartella e il filtraggio dei file per estensione.
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: Scopri come estrarre testo da immagini png in Java usando Aspose OCR.
  Questo tutorial copre l'elaborazione batch OCR, la lettura delle immagini da una
  cartella e il filtraggio dei file per estensione.
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: Come estrarre testo da png in Java – guida batch OCR
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Come estrarre testo da png in Java – guida batch OCR
url: /it/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come estrarre testo da png in Java – guida batch OCR

Se hai mai dovuto **estrarre testo da png** file ma non sapevi come scalare l'operazione oltre una manciata di immagini, sei nel posto giusto. Molti sviluppatori iniziano con una singola chiamata OCR per immagine e si imbattono rapidamente in limiti di prestazioni quando la cartella cresce a decine o centinaia di file. Con Aspose OCR per Java puoi creare una solida pipeline OCR batch che attraversa una directory, filtra solo i tipi di immagine di tuo interesse, esegue il riconoscimento in parallelo e restituisce i risultati nello stesso ordine dei file di origine. Alla fine di questa guida avrai uno snippet Java pronto da usare che gestisce **batch OCR processing** in modo affidabile ed efficiente.

![Esempio di conversione di immagini in testo](https://example.com/convert-images-to-text.png "Screenshot dell'output della console Java che mostra il testo convertito da file PNG")

## Risposte rapide
- **Quale libreria gestisce l'OCR?** Aspose OCR for Java.
- **Posso elaborare PNG e JPG insieme?** Sì – il campione filtra entrambe le estensioni.
- **Il motore OCR è thread‑safe?** Una singola istanza condivisa di `AsposeOCR` è sicura per l'uso concorrente.
- **Ho bisogno di una licenza per i test?** Una chiave temporanea gratuita è disponibile da Aspose.
- **Le sottocartelle verranno scansionate automaticamente?** `Files.walk` attraversa l'intero albero ricorsivamente.

## Che cos'è estrarre testo da png?
`extract text from png` si riferisce al processo di applicare il riconoscimento ottico dei caratteri (OCR) ai file Portable Network Graphics in modo che i caratteri visibili diventino stringhe ricercabili e modificabili. Il motore di Aspose OCR legge i dati dei pixel, identifica le forme dei glifi e restituisce testo Unicode in una singola chiamata di metodo.

## Perché usare Aspose OCR per Java?
Aspose OCR supporta **30+ lingue**, elabora fino a **500 immagini al minuto** su un server standard a 8‑core e può gestire file fino a **200 MB** senza caricare l'intera immagine in memoria. Queste capacità quantificate significano che puoi eseguire in modo affidabile lavori batch su larga scala su hardware di consumo senza superare i limiti di memoria.

## Prerequisiti
- Java 17 (o qualsiasi versione LTS recente).
- Maven o Gradle per la gestione delle dipendenze.
- Una directory contenente immagini PNG/JPG che desideri elaborare.
- Familiarità di base con gli stream Java e il pacchetto `java.nio.file`.
- (Opzionale) Una chiave di licenza temporanea Aspose OCR per la valutazione.

> **Consiglio:** La chiave temporanea gratuita scade dopo 30 giorni, ma ti offre pieno accesso API per i test.

## Come mantiene l'ordine la pipeline OCR batch?
`Future<OcrResult>` rappresenta un risultato OCR pendente che può essere recuperato una volta terminata l'elaborazione. La pipeline preserva l'ordine originale dei file memorizzando gli oggetti `Future<OcrResult>` in una lista che rispecchia l'ordine della collezione di input `Path`. Quando in seguito iteri sui futures e chiami `get()`, ogni chiamata blocca solo per la sua immagine corrispondente, così la sequenza di output corrisponde a quella di input senza logica di ordinamento aggiuntiva.

## Che cos'è Aspose OCR per Java?
`AsposeOCR` è la classe principale della libreria Aspose OCR che incapsula tutti i pacchetti linguistici, le impostazioni di riconoscimento e le risorse native interne. È progettata per essere istanziata una sola volta per l'intera durata dell'applicazione e condivisa in modo sicuro tra più thread. Poiché carica i dati linguistici una sola volta, riutilizzare la stessa istanza riduce l'overhead di inizializzazione e migliora il throughput per le operazioni batch.

## Come configurare il progetto e aggiungere Aspose OCR
Per prima cosa, crea un progetto Maven (o Gradle) e aggiungi la dipendenza Aspose OCR al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **Perché è importante:** Dichiarare la dipendenza in anticipo garantisce che il compilatore possa vedere `AsposeOCR`, `ParallelRecognizer` e le classi correlate. Garantisce inoltre che la stessa versione venga utilizzata su tutte le macchine, il che è cruciale per un **batch OCR processing** riproducibile.

Aggiorna il tuo IDE dopo il completamento della build; ora dovresti vedere i pacchetti Aspose sotto **External Libraries**.

## Come inizializzare il motore OCR – condividere una singola istanza
`AsposeOCR` è la classe principale del motore OCR fornita dalla libreria Aspose OCR. Abbiamo bisogno di **una** sola istanza del motore OCR per l'intera esecuzione. Condividerla tra i thread fa risparmiare memoria e velocizza le cose perché il motore carica i pacchetti linguistici una sola volta.

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

`AsposeOCR` è thread‑safe, quindi puoi passarla in modo sicuro a un `ParallelRecognizer` che gestirà un pool di thread di lavoro.

> **Spiegazione:** `ParallelRecognizer` avvolge il motore in un thread‑pool. Quando invii molti file, ognuno ottiene il proprio thread di lavoro, abilitando il vero parallelismo su CPU multi‑core.

## Come leggere le immagini dalla cartella – attraversare l'albero delle directory
`Files.walk` è un metodo Java NIO che attraversa ricorsivamente un albero di file e restituisce uno stream di oggetti `Path`. Ora dobbiamo **leggere le immagini dalla cartella** e raccogliere ogni PNG o JPG. L'API `Files.walk` lo rende un'unica riga, ma aggiungeremo un filtro per **estrarre testo da png** solo quando necessario.

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **Perché filtriamo qui:** Usare `filter` ci permette di **filtrare i file per estensione** subito, riducendo I/O non necessario più avanti. Mantiene anche il codice leggibile—non servono regex complessi.

## Come inviare i job OCR in modo asincrono
`recognizeAsync` invia un'immagine al motore OCR per l'elaborazione asincrona e restituisce un `Future<OcrResult>` che rappresenta il risultato pendente. Con l'elenco dei file pronto, spingiamo ogni percorso al `ParallelRecognizer`. Il metodo `recognizeAsync` restituisce un `Future<OcrResult>` che memorizziamo per il recupero successivo.

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **Cosa succede dietro le quinte?** Ogni chiamata accoda un task nel servizio executor interno del riconoscitore. I task vengono eseguiti in parallelo, così una cartella con 100 immagini può essere processata in una frazione del tempo di un ciclo monothread.

## Come recuperare i risultati mantenendo la sequenza dei file
`Future<OcrResult>` contiene il risultato di un task OCR asincrono e fornisce un metodo `get()` per ottenere il testo riconosciuto. Poiché abbiamo memorizzato i futures nello stesso ordine di `imagePaths`, possiamo semplicemente iterare sulla lista e chiamare `get()`. La chiamata blocca solo fino al completamento di quell'immagine specifica, preservando l'ordine senza ulteriori registrazioni.

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**Esempio di output della console** (troncato per brevità):

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **Gestione dei casi limite:** Se una particolare immagine genera un'eccezione (file corrotto, formato non supportato), la catturiamo e continuiamo a elaborare il resto—un'abitudine essenziale per pipeline **batch OCR processing** affidabili.

## Come pulire le risorse – chiudere il riconoscitore
`ParallelRecognizer.shutdown()` interrompe il pool di thread interno, assicurando che tutti i task OCR siano completati prima che l'applicazione termini. Non dimenticare mai di chiudere il pool interno; altrimenti la tua JVM potrebbe bloccarsi all'uscita.

```java
recognizer.shutdown();
```

È tutto! Il programma ora attraversa qualsiasi directory, filtra i file PNG/JPG, esegue l'OCR in parallelo e stampa i risultati nell'ordine originale.

---

## Esempio completo funzionante (copia‑incolla)

Di seguito trovi la classe Java completa e pronta all'esecuzione. Sostituisci `"YOUR_DIRECTORY"` con il percorso della tua cartella di immagini ed eseguila dal tuo IDE o dalla riga di comando.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

Esegui la classe, osserva la console riempirsi di stringhe estratte e celebra il fatto che hai appena **convertito immagini in testo** senza scrivere alcun ciclo che blocca I/O.

---

## Domande frequenti (FAQ)

**Q: Posso elaborare PDF o TIFF anche?**  
A: Assolutamente. Aspose OCR supporta oltre 30 formati—including PDF, TIFF, BMP e GIF—basta aggiungere le estensioni desiderate al filtro nel passaggio di attraversamento della directory.

**Q: E se avessi bisogno di una lingua diversa dall'inglese, come lo spagnolo?**  
A: Cambia `RecognitionLanguage.ENGLISH` in `RecognitionLanguage.SPANISH` (o qualsiasi lingua supportata). I pacchetti linguistici sono inclusi nella libreria, quindi non è necessario alcun download aggiuntivo.

**Q: La mia cartella contiene sottocartelle—verranno scansionate?**  
A: Sì. `Files.walk` attraversa l'intero albero ricorsivamente, quindi ogni PNG/J

**Q: Come gestire immagini estremamente grandi che superano i 200 MB?**  
A: Abilita la modalità streaming chiamando `ocrEngine.setUseStreaming(true)`. Questo indica al motore di leggere l'immagine a blocchi, riducendo drasticamente l'uso di memoria di picco.

**Q: Esiste un modo per limitare il numero di thread OCR concorrenti?**  
A: Sì. Quando costruisci `ParallelRecognizer`, passa il numero massimo di thread desiderato come secondo argomento (ad es., `new ParallelRecognizer(ocrEngine, 4)`).

---

## Ultimo aggiornamento: 2026-08-28  
**Testato con:** Aspose OCR for Java 24.10  
**Autore:** Aspose  

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

## Tutorial correlati

- [Converti immagini in testo in Java Guida elaborazione OCR batch](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [Leggi testo da immagine in Java Guida completa Aspose OCR](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Estrai testo da immagini usando Aspose.OCR – Caratteri consentiti](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}