---
category: general
date: 2026-02-17
description: Impara a utilizzare un pool di thread fisso in Java per estrarre testo
  da immagini PNG con elaborazione OCR parallela e chiudere correttamente il servizio
  Executor.
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: it
og_description: Scopri come un pool di thread fisso in Java può estrarre testo da
  immagini PNG in parallelo, convertire il testo delle pagine scansionate e chiudere
  in modo sicuro il servizio executor.
og_title: Pool di thread fisso Java – OCR parallelo per PNG
tags:
- java
- ocr
- multithreading
- aspose
title: Pool di thread fisso Java – OCR parallelo per PNG
url: /it/java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# fixed thread pool java – OCR parallelo per PNG

Ti sei mai chiesto come velocizzare l'OCR su un sacco di file PNG usando un **fixed thread pool java**? In questo tutorial vedremo come **estrarre testo da PNG** in parallelo, **convertire il testo delle pagine scansionate** in stringhe modificabili, e chiudere in modo sicuro **shut down executor service** una volta completato il lavoro.

Se ti sei mai trovato a fissare un ciclo monothread che si trascina per minuti, conosci la frustrazione di dover attendere che ogni pagina finisca prima che la successiva inizi. La buona notizia? Con poche righe di Java e Aspose OCR puoi sfruttare tutta la potenza dei tuoi core CPU, trasformare quelle pagine scansionate in testo ricercabile e mantenere la tua applicazione reattiva.  

Di seguito trovi un esempio completo, pronto‑da‑eseguire, più spiegazioni sul perché ogni pezzo è importante, le insidie più comuni e consigli applicabili a qualsiasi libreria OCR.

---

## Cosa ti servirà

- **Java 17** (o qualsiasi JDK recente) – il codice utilizza la sintassi moderna `var` con parsimonia, ma funziona anche su versioni più vecchie.  
- **Aspose.OCR for Java** library – puoi scaricarla da Maven Central o ottenere una versione di prova da Aspose.  
- Un insieme di file **PNG** che desideri elaborare – pensa a ricevute scansionate, pagine di libri o screenshot.  
- Familiarità di base con la concorrenza in Java – non obbligatoria, ma utile.

Questo è tutto. Nessun servizio esterno, nessun Docker, solo Java puro e un po' di magia multithreading.

---

## Passo 1: Aggiungi la dipendenza Aspose OCR e la licenza (Opzionale)

Per prima cosa, assicurati che il JAR di Aspose OCR sia nel tuo classpath. Se usi Maven, aggiungi:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Se non hai una licenza, la libreria funzionerà in modalità valutazione; il codice si comporta allo stesso modo. Per caricare una licenza (raccomandato per la produzione), posiziona `Aspose.OCR.lic` nella cartella delle risorse e usa:

```java
// Load the Aspose OCR license (optional)
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

> **Consiglio professionale:** Mantieni il file di licenza fuori dal controllo di versione per evitare esposizioni accidentali.

---

## Passo 2: Crea un'istanza `OcrEngine` thread‑safe

L'`OcrEngine` di Aspose OCR è thread‑safe finché riutilizzi la stessa istanza tra i task. Crearla una sola volta salva memoria ed evita l'overhead di reinizializzare il motore per ogni immagine.

```java
// One shared OcrEngine for all threads
OcrEngine ocrEngine = new OcrEngine();
```

Perché riutilizzarla? Pensa al motore come a un lavoratore pesante che carica i modelli linguistici in memoria. Creare un nuovo motore per immagine sarebbe come assumere un nuovo specialista per ogni piccolo lavoro – costoso e inutile.

---

## Passo 3: Configura un Fixed Thread Pool Java

Ora arriva la star dello spettacolo: un **fixed thread pool java**. Lo dimensioneremo in base al numero di processori logici così ogni core riceve lavoro senza sovraccaricare.

```java
// Determine available processors and create a fixed pool
int threadCount = Runtime.getRuntime().availableProcessors();
ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);
```

Usare un pool *fixed* (invece di uno cached) ti garantisce un utilizzo prevedibile delle risorse e previene i temuti picchi di “out‑of‑memory” quando centinaia di immagini arrivano contemporaneamente.

---

## Passo 4: Elenca i file PNG da elaborare (Estrai testo da PNG)

Raccogli i percorsi delle immagini che vuoi sottoporre a OCR. In un progetto reale potresti scansionare una directory o leggere da un database; qui inseriremo manualmente qualche esempio.

```java
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png"
);
```

> **Nota:** L'estensione del file **png** è importante perché Aspose OCR rileva automaticamente il formato, ma potresti fornire anche JPEG o TIFF.

---

## Passo 5: Invia i task OCR – Elaborazione OCR parallela

Ogni immagine diventa un callable che restituisce il testo riconosciuto. Poiché l'`OcrEngine` è condiviso, dobbiamo solo passare il percorso del file al task.

```java
List<Future<String>> ocrFutures = new ArrayList<>();

for (String imagePath : imageFiles) {
    ocrFutures.add(threadPool.submit(() -> {
        // Prepare input for this image
        OcrInput input = new OcrInput();
        input.add(imagePath);

        // Perform OCR using the shared engine
        OcrResult result = ocrEngine.recognize(input);

        // Return the plain text
        return result.getText();
    }));
}
```

Perché avvolgerlo in un `Future`? Ci permette di lanciare tutti i job subito, per poi raccogliere i risultati nell'ordine in cui sono stati inviati – perfetto per preservare l'ordine delle pagine quando **convertire il testo delle pagine scansionate** in un documento.

---

## Passo 6: Recupera i risultati e visualizzali (Converti testo delle pagine scansionate)

Ora attendiamo che ogni `Future` termini e stampiamo l'output. La chiamata `get()` blocca solo fino al completamento del task specifico, non dell'intero pool.

```java
for (Future<String> future : ocrFutures) {
    System.out.println("----");
    System.out.println(future.get()); // prints OCR result for one PNG
}
```

Un tipico output della console appare così:

```
----
The quick brown fox jumps over the lazy dog.
----
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----
Page 3 content goes here…
```

Se preferisci scrivere i risultati su file, sostituisci `System.out.println` con una chiamata a `Files.writeString`.

---

## Passo 7: Chiudi correttamente il servizio Executor

Quando tutti i task sono terminati, è fondamentale **shut down executor service**; altrimenti la JVM potrebbe mantenere thread non‑daemon attivi, impedendo una chiusura pulita.

```java
threadPool.shutdown();               // No new tasks accepted
if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
    threadPool.shutdownNow();        // Force shutdown after timeout
}
```

Il pattern `awaitTermination` dà al pool la possibilità di completare il lavoro in corso prima di forzare la chiusura. Ignorare questo passaggio è una causa comune di perdite di memoria in applicazioni a lungo termine.

---

## Esempio completo funzionante

Mettendo tutto insieme, ecco il programma completo che puoi copiare‑incollare in `ParallelBatchDemo.java` e eseguire:

```java
import com.aspose.ocr.*;

import java.util.*;
import java.util.concurrent.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license (optional)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // 2️⃣ Shared, thread‑safe OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Fixed thread pool java – one thread per core
        int threadCount = Runtime.getRuntime().availableProcessors();
        ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);

        // 4️⃣ Files to process – extract text from png
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png"
        );

        // 5️⃣ Submit tasks – parallel OCR processing
        List<Future<String>> ocrFutures = new ArrayList<>();
        for (String imagePath : imageFiles) {
            ocrFutures.add(threadPool.submit(() -> {
                OcrInput input = new OcrInput();
                input.add(imagePath);
                OcrResult result = ocrEngine.recognize(input);
                return result.getText();
            }));
        }

        // 6️⃣ Retrieve and print – convert scanned pages text
        for (Future<String> future : ocrFutures) {
            System.out.println("----");
            System.out.println(future.get());
        }

        // 7️⃣ Shut down executor service cleanly
        threadPool.shutdown();
        if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
            threadPool.shutdownNow();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}