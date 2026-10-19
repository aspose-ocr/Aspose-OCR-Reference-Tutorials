---
category: general
date: 2026-05-03
description: Crea un pool di thread fisso in Java per estrarre rapidamente il testo
  dalle immagini. Scopri come eseguire l'OCR, convertire l'immagine in testo e migliorare
  le prestazioni con l'elaborazione OCR parallela.
draft: false
keywords:
- create fixed thread pool
- extract text from images
- how to run OCR
- convert image to text
- parallel OCR processing
language: it
og_description: Crea un pool di thread fisso in Java per estrarre rapidamente il testo
  dalle immagini. Scopri come eseguire l'OCR, convertire l'immagine in testo e aumentare
  le prestazioni con l'elaborazione OCR parallela.
og_title: Crea un pool di thread fisso per OCR parallelo in Java
tags:
- Java
- OCR
- Multithreading
title: Crea un pool di thread fisso per OCR parallelo in Java
url: /it/java/advanced-ocr-techniques/create-fixed-thread-pool-for-parallel-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un Thread Pool Fisso per l'OCR Parallelo in Java

Ti è mai capitato di dover **creare un thread pool fisso** per velocizzare i lavori di OCR, ma non sapevi da dove cominciare? Non sei l'unico. In molti progetti con molte immagini, il collo di bottiglia è la chiamata OCR a thread singolo, e la soluzione è sorprendentemente semplice: avviare un pool di thread lavoratori e farli elaborare i file in parallelo.  

In questo tutorial imparerai a **estrarre testo dalle immagini** usando Aspose OCR, a **eseguire OCR** in modo efficiente e a **convertire immagine in testo** senza sovraccaricare la CPU. Alla fine avrai un programma Java pronto all'uso che dimostra **l'elaborazione OCR parallela** su una manciata di immagini di esempio.

## Cosa Costruirai

Metteremo insieme una piccola applicazione console che:

* Legge un elenco di percorsi di immagine (PNG, JPG, TIFF, BMP).
* **Crea un thread pool fisso** dimensionato al numero di core CPU.
* Invia un compito OCR per ogni immagine.
* Raccoglie il testo riconosciuto e lo stampa sulla console.
* Chiude l'esecutore in modo pulito.

Nessuno strumento di build esterno, nessun framework sofisticato—solo Java puro e la libreria Aspose OCR. Se hai Java 8+ e un IDE decente, sei pronto.

## Prerequisiti

* **Java Development Kit (JDK) 8 o superiore** – il codice usa le lambda, quindi le versioni più vecchie non compilerebbero.
* **Aspose OCR per Java** – scarica il JAR dal sito Aspose o includilo via Maven (`com.aspose:aspose-ocr`).
* Una cartella con alcune immagini di test (il codice punta a `YOUR_DIRECTORY`).  
* Familiarità di base con la concorrenza in Java (spiegheremo il resto).

> *Pro tip:* Se usi Maven, aggiungi la dipendenza al tuo `pom.xml` e lascia che l'IDE gestisca il classpath.  

---

## Passo 1: Aggiungi le Importazioni Necessarie

Per prima cosa, porta le classi di cui abbiamo bisogno nello scope. Non è solo boilerplate; ogni importazione indica alla JVM dove trovare il motore OCR, le utility per la gestione delle immagini e gli strumenti di concorrenza che ci permettono di **creare un thread pool fisso**.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;
```

* `com.aspose.ocr.*` – l'API OCR di base.  
* `java.util.*` – collezioni per memorizzare i percorsi delle immagini e i risultati.  
* `java.util.concurrent.*` – il pacchetto di concorrenza che contiene `ExecutorService` e `Future`.

---

## Passo 2: Definisci le Immagini da Elaborare

Successivamente, elenchiamo i file da cui vogliamo **estrarre testo dalle immagini**. Usare `Arrays.asList` mantiene il codice conciso e ci permette di sostituire la tua directory senza toccare il resto della logica.

```java
List<String> imagePaths = Arrays.asList(
        "YOUR_DIRECTORY/image1.png",
        "YOUR_DIRECTORY/image2.jpg",
        "YOUR_DIRECTORY/image3.tif",
        "YOUR_DIRECTORY/image4.bmp"
);
```

Sentiti libero di aggiungere altre voci; il thread pool si adatterà automaticamente in base al numero di core CPU disponibili.

---

## Passo 3: **Crea un Thread Pool Fisso** in Base ai Core CPU

Ecco il cuore del tutorial. Chiediamo al runtime quanti core sono disponibili e chiediamo alla factory `Executors` di darci un pool di esattamente quella dimensione. Perché fisso? Perché un numero prevedibile di thread evita la temuta “esplosione di thread” che può affamare le risorse del sistema operativo.

```java
int coreCount = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(coreCount);
```

* `availableProcessors()` restituisce il conteggio dei core logici (inclusi gli hyper‑thread).  
* `newFixedThreadPool(coreCount)` garantisce che non superiamo mai la capacità della CPU, il modo più sicuro per **eseguire OCR** in parallelo.

---

## Passo 4: Invia un Compito OCR per Ogni Immagine

Ora trasformiamo ogni percorso di file in un `Callable` che **esegue OCR**, riconosce il testo e restituisce il risultato. Nota che istanziamo un nuovo `OcrEngine` all'interno della lambda—questo evita la condivisione non thread‑safe dello stato del motore.

```java
List<Future<String>> ocrResults = new ArrayList<>();
for (String path : imagePaths) {
    ocrResults.add(executor.submit(() -> {
        OcrEngine engine = new OcrEngine();          // fresh engine per task
        engine.setImage(ImageStream.fromFile(path));
        engine.getLanguage().setEnglish(true);
        return engine.recognize() ? engine.getText()
                                   : "Failed: " + path;
    }));
}
```

* Ogni chiamata a `submit` passa la lambda al pool, che la programma su un thread inattivo.  
* Gli oggetti `Future<String>` ci permettono di recuperare il testo riconosciuto in seguito, preservando l'ordine se necessario.

---

## Passo 5: Recupera e Visualizza il Testo Riconosciuto

Una volta che tutti i compiti sono in coda, iteriamo semplicemente sulla lista di `Future`, chiamando `get()` per bloccarci finché ogni lavoro OCR non termina. Qui è dove il passo **convertire immagine in testo** diventa visibile: la chiamata `engine.getText()` restituisce la stringa grezza.

```java
for (Future<String> result : ocrResults) {
    System.out.println("OCR result:\n" + result.get());
}
```

Un tipico output sulla console appare così:

```
OCR result:
Hello world!
OCR result:
Invoice #12345
Date: 2026‑04‑30
...
```

Se un file fallisce (ad esempio perché è corrotto), vedrai una riga che inizia con `Failed:` seguita dal percorso—utile per un rapido debug.

---

## Passo 6: Pulisci il Servizio Executor

Non dimenticare mai di chiudere il pool; altrimenti la JVM potrebbe rimanere in esecuzione, pensando che ci siano ancora lavori da fare. Una chiusura graduale permette ai task in corso di terminare prima che il processo esca.

```java
executor.shutdown();
```

Puoi anche chiamare `awaitTermination` se devi imporre un timeout, ma per la maggior parte delle utility da riga di comando un semplice `shutdown()` è sufficiente.

---

## Esempio Completo Funzionante

Di seguito trovi il programma completo, pronto per essere eseguito. Copialo‑incollalo in un file chiamato `ParallelOcrTutorial.java`, aggiusta i percorsi delle immagini e compila/esegui con `javac` + `java` come faresti normalmente.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Define the images to be processed
        List<String> imagePaths = Arrays.asList(
                "YOUR_DIRECTORY/image1.png",
                "YOUR_DIRECTORY/image2.jpg",
                "YOUR_DIRECTORY/image3.tif",
                "YOUR_DIRECTORY/image4.bmp"
        );

        // Step 3: Create a fixed‑size thread pool matching the CPU cores
        int coreCount = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(coreCount);

        // Step 4: Submit an OCR task for each image
        List<Future<String>> ocrResults = new ArrayList<>();
        for (String path : imagePaths) {
            ocrResults.add(executor.submit(() -> {
                OcrEngine engine = new OcrEngine();          // fresh engine per task
                engine.setImage(ImageStream.fromFile(path));
                engine.getLanguage().setEnglish(true);
                return engine.recognize() ? engine.getText()
                                           : "Failed: " + path;
            }));
        }

        // Step 5: Retrieve and display the recognized text
        for (Future<String> result : ocrResults) {
            System.out.println("OCR result:\n" + result.get());
        }

        // Step 6: Clean up the executor service
        executor.shutdown();
    }
}
```

**Risultato atteso:** il contenuto testuale di ogni immagine stampato sulla console, nello stesso ordine della lista `imagePaths`. Se qualche immagine non può essere elaborata, vedrai un avviso di errore al posto di una riga vuota.

---

## Domande Frequenti & Casi Limite

### E se ho più immagini dei thread?

Il thread pool fisso accoderà automaticamente i task in eccesso. Non appena un thread termina il suo lavoro OCR corrente, ne prende in carico un altro. Questo comportamento di accodamento è l’essenza dell'**elaborazione OCR parallela**—ottieni il massimo throughput senza sovraccaricare la CPU.

### Posso cambiare la lingua?

Assolutamente. Sostituisci `engine.getLanguage().setEnglish(true);` con il flag della lingua desiderata, ad esempio `setFrench(true)` o abilita più lingue chiamando diversi setter prima di `recognize()`.

### Come gestisco immagini molto grandi?

File di grandi dimensioni possono consumare molta memoria per thread. Se noti `OutOfMemoryError`, considera di ridimensionare l'immagine prima di passarla al motore, oppure aumenta la dimensione dell'heap con `-Xmx`. Un altro approccio è usare un **cached thread pool** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}