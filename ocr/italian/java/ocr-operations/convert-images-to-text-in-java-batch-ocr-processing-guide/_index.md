---
category: general
date: 2026-01-02
description: Converti le immagini in testo con Java usando Aspose OCR. Padroneggia
  l'elaborazione OCR batch, leggi le immagini da una cartella e filtra i file per
  estensione.
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: it
og_description: Converti rapidamente le immagini in testo con Java. Questo tutorial
  copre l'elaborazione OCR batch, la lettura delle immagini da una cartella e il filtraggio
  dei file per estensione.
og_title: Converti le immagini in testo in Java – Guida completa all'OCR batch
tags:
- OCR
- Java
- Aspose
title: Converti le immagini in testo in Java – Guida al batch di elaborazione OCR
url: /it/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertire le immagini in testo in Java – Guida all'elaborazione OCR batch

Hai mai avuto bisogno di **convertire le immagini in testo** ma non sapevi come gestire decine di file contemporaneamente? Non sei solo—gli sviluppatori lottano costantemente per estrarre dati da PNG, JPG e altre scansioni. La buona notizia? Con Aspose OCR puoi creare in pochi minuti una pipeline di elaborazione OCR batch, leggere le immagini da strutture di cartelle e persino filtrare i file per estensione così lavori solo su ciò che importa.

In questo tutorial costruiremo un programma Java autonomo che attraversa una directory, seleziona ogni `.png` o `.jpg`, invia ogni immagine ad Aspose OCR in modo asincrono e stampa il testo estratto nell'ordine originale. Alla fine avrai uno snippet riutilizzabile da inserire in qualsiasi progetto che necessita di **convertire le immagini in testo** su larga scala.

---

![Convert images to text example](https://example.com/convert-images-to-text.png "Screenshot of Java console output showing converted text from PNG files")

## Cosa costruirai

- Un singolo motore `AsposeOCR` condiviso tra i thread (efficiente e thread‑safe).  
- Un `ParallelRecognizer` che esegue i job OCR in parallelo, perfetto per **l'elaborazione OCR batch**.  
- Logica che **legge le immagini dalla cartella** usando `java.nio.file.Files`.  
- Filtri semplici per **estrarre il testo da file PNG** mantenendo la gestione dei JPG.  
- Spegnimento pulito del pool di thread interno per evitare perdite di risorse.

### Prerequisiti

- Java 17 (o qualsiasi versione LTS recente).  
- Maven o Gradle per scaricare la libreria Aspose OCR.  
- Una cartella piena di immagini PNG/JPG che desideri elaborare.  
- Familiarità di base con gli stream Java—nulla di complicato richiesto.

> **Consiglio professionale:** Se non hai ancora una licenza, Aspose offre una chiave temporanea gratuita che puoi usare per i test.

---

## Passo 1 – Configura il progetto e aggiungi Aspose OCR

Per prima cosa, crea un nuovo progetto Maven (o Gradle, a tua scelta). Aggiungi la dipendenza Aspose OCR al file `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Perché è importante:** Dichiarare la dipendenza in anticipo garantisce che il compilatore possa vedere `AsposeOCR`, `ParallelRecognizer` e le classi correlate. Assicura inoltre che la stessa versione venga usata su tutte le macchine, il che è cruciale per un **elaborazione OCR batch** riproducibile.

Una volta completata la build, aggiorna il tuo IDE e dovresti vedere i pacchetti Aspose sotto `External Libraries`.

---

## Passo 2 – Convertire le immagini in testo – Inizializzare il motore OCR

Abbiamo bisogno di **una** sola istanza del motore OCR per l'intera esecuzione. Condividerla tra i thread risparmia memoria e velocizza le operazioni perché il motore carica i pacchetti linguistici una sola volta.

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

> **Spiegazione:** `ParallelRecognizer` avvolge il motore in un thread‑pool. Quando invii molti file, ciascuno ottiene il proprio thread di lavoro, abilitando un vero parallelismo su CPU multi‑core.

---

## Passo 3 – Leggere le immagini dalla cartella – Percorrere l'albero delle directory

Ora dobbiamo **leggere le immagini dalla cartella** e raccogliere ogni PNG o JPG. L'API `Files.walk` lo rende una singola riga, ma aggiungeremo un filtro per **estrarre il testo da PNG** solo quando necessario.

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

> **Perché filtriamo qui:** Usare `filter` ci permette di **filtrare i file per estensione** subito, riducendo I/O non necessario in seguito. Mantiene anche il codice leggibile—nessuna necessità di regex complesse.

---

## Passo 4 – Elaborazione OCR batch – Inviare i job in modo asincrono

Con l'elenco dei file pronto, inviamo ogni percorso al `ParallelRecognizer`. Il metodo `recognizeAsync` restituisce un `Future<OcrResult>` che memorizziamo per un successivo recupero.

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

> **Cosa succede dietro le quinte?** Ogni chiamata accoda un task al servizio executor interno del recognizer. I task vengono eseguiti in parallelo, così una cartella con 100 immagini può essere elaborata in una frazione del tempo che richiederebbe un ciclo a thread singolo.

---

## Passo 5 – Recuperare i risultati nell'ordine originale – Conservare la sequenza dei file

Poiché abbiamo memorizzato i future nello stesso ordine di `imagePaths`, possiamo semplicemente iterare sulla lista e chiamare `get()`. La chiamata blocca solo fino al completamento di quell'immagine specifica, preservando l'ordine senza ulteriori gestioni.

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

**Esempio di output della console** (troncato per brevità):

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

> **Gestione dei casi limite:** Se una particolare immagine genera un'eccezione (file corrotto, formato non supportato), la catturiamo e continuiamo a elaborare le altre—un'abitudine essenziale per pipeline di **elaborazione OCR batch** affidabili.

---

## Passo 6 – Pulizia – Chiudere il Recognizer

Non dimenticare mai di chiudere il pool di thread interno; altrimenti la tua JVM potrebbe rimanere in attesa all'uscita.

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

Ecco fatto! Il programma ora percorrerà qualsiasi directory, filtrerà i file PNG/JPG, eseguirà l'OCR in parallelo e stamperà i risultati.

---

## Esempio completo funzionante

Di seguito trovi la classe Java completa, pronta per il copia‑incolla. Sostituisci `"YOUR_DIRECTORY"` con il percorso della tua cartella di immagini ed eseguila dal tuo IDE o dalla riga di comando.

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

Esegui la classe, osserva la console riempirsi di stringhe estratte e celebra il fatto di aver appena **convertito le immagini in testo** senza scrivere alcun ciclo che blocca l'I/O.

---

## Domande frequenti (FAQ)

**Q: Posso elaborare anche PDF o TIFF?**  
A: Assolutamente. Aspose OCR supporta molti formati—basta aggiungere le estensioni di file appropriate al filtro nel Passo 2.

**Q: E se ho bisogno di una lingua diversa, come lo spagnolo?**  
A: Cambia `RecognitionLanguage.ENGLISH` in `RecognitionLanguage.SPANISH`. Assicurati che il pacchetto linguistico sia installato (Aspose include la maggior parte delle lingue principali di default).

**Q: La mia cartella contiene sottocartelle—verranno scansionate?**  
A: Sì. `Files.walk` attraversa l'intero albero in modo ricorsivo, quindi ogni PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}