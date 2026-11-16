---
category: general
date: 2026-02-27
description: Scopri come utilizzare l'OCR in Java per estrarre il testo dalle immagini
  di file TIFF e PDF usando l'elaborazione parallela di Aspose OCR. Guida rapida e
  semplice.
draft: false
keywords:
- how to use ocr
- perform ocr on pdf
- extract text from tiff
- extract image text java
language: it
og_description: Scopri come utilizzare l'OCR in Java per estrarre il testo dalle immagini
  di file TIFF e PDF con l'elaborazione parallela di Aspose OCR.
og_title: Come usare OCR in Java – Elaborazione parallela con Aspose
tags:
- OCR
- Java
- Aspose
title: Come utilizzare l'OCR in Java – Elaborazione parallela con Aspose
url: /it/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare OCR in Java – Elaborazione parallela con Aspose

Ti sei mai chiesto **come usare OCR** per estrarre il testo da un documento scansionato senza sforzo? Non sei l'unico. Gli sviluppatori si scontrano continuamente con un ostacolo quando devono leggere il testo dalle immagini—soprattutto TIFF e PDF—mantenendo sotto controllo le prestazioni.  

In questo tutorial ti mostreremo una soluzione completa, pronta‑da‑eseguire, che **estrae il testo dalle immagini in Java** usando Aspose OCR, attiva l’elaborazione parallela e ti permette persino di limitare il numero di thread. Alla fine avrai una singola classe che può **eseguire OCR su PDF** e **estrarre testo da TIFF** in una frazione del tempo richiesto da un approccio monothread.

> **Cosa otterrai**  
> * Una chiara spiegazione del perché l'OCR parallelo è importante.  
> * Un programma Java completo (senza import mancanti).  
> * Suggerimenti per regolare l'uso dei thread e gestire le insidie più comuni.  

## Prerequisiti

- Java 8 o superiore (il codice compila anche con JDK 11).  
- Libreria Aspose.OCR per Java – puoi scaricare l'ultimo JAR da Maven Central (`com.aspose:aspose-ocr`).  
- Un file immagine (`.tif`, `.tiff`) o un PDF da elaborare.  
- Una quantità moderata di RAM—l'elaborazione parallela avvierà alcuni thread, ma Aspose è efficiente in termini di memoria.

Se hai tutto questo, immergiamoci.

![Diagramma che mostra il flusso OCR – come usare OCR in Java con elaborazione parallela](how-to-use-ocr-pipeline.png)

*Testo alternativo immagine: diagramma di esempio su come usare OCR*  

---

## Step 1: Configura il tuo progetto e aggiungi Aspose OCR

### Perché è importante

Prima di poter **eseguire OCR su PDF** o su qualsiasi immagine, la libreria deve trovarsi nel classpath. Senza di essa il compilatore lancerà `ClassNotFoundException` e rimarrai bloccato al passo due.

### Come fare

Se usi Maven, aggiungi la dipendenza:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the newest version -->
</dependency>
```

Per Gradle:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Consiglio professionale:** Mantieni il numero di versione in linea con le note di rilascio di Aspose; le versioni più recenti includono spesso miglioramenti di prestazioni per l'elaborazione parallela.

---

## Step 2: Crea il motore OCR e abilita l'elaborazione parallela

### Perché è importante

Per impostazione predefinita Aspose OCR funziona su un singolo thread. Quando gli fornisci un PDF multipagina o un batch di TIFF, il motore elabora ogni pagina una dopo l'altra—lento e inefficiente. Abilitare l'elaborazione parallela consente alla CPU di elaborare più pagine contemporaneamente, riducendo drasticamente i tempi di esecuzione.

### Codice

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Path to the input file (TIFF or PDF)
        String inputPath = "YOUR_DIRECTORY/input.tif";

        // 2️⃣ Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Turn on parallel processing – this is the core of how to use OCR efficiently
        ocrEngine.getConfig().setUseParallelProcessing(true);

        // 4️⃣ (Optional) Limit threads – you can cap it to the number of cores you have
        // ocrEngine.getConfig().setMaxThreads(Runtime.getRuntime().availableProcessors());

        // 5️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.processImage(inputPath);

        // 6️⃣ Output the recognised text
        System.out.println(ocrResult.getText());
    }
}
```

**Spiegazione delle righe chiave**

- `setUseParallelProcessing(true)`: indica ad Aspose di suddividere il carico di lavoro tra i core CPU disponibili.  
- `setMaxThreads(...)`: puoi limitare il pool di thread se sei su un server condiviso o vuoi lasciare margine per altri servizi.  
- `processImage(inputPath)`: funziona sia per file immagine sia per documenti PDF, così la stessa chiamata **esegue OCR su PDF** e su TIFF allo stesso modo.

---

## Step 3: Gestire tipi di input diversi – PDF vs. TIFF

### Perché è importante

Anche se `processImage` accetta una stringa di percorso, il trattamento interno differisce. I PDF contengono spesso più pagine, ognuna delle quali diventa un lavoro OCR separato. I TIFF possono essere a pagina singola o multipagina; Aspose tratta ogni frame come una pagina.

### Cosa tenere d'occhio

| Input | Problema tipico | Correzione consigliata |
|------|----------------|------------------------|
| PDF | I PDF di grandi dimensioni possono esaurire la memoria se tutte le pagine vengono caricate simultaneamente. | Usa `ocrEngine.getConfig().setMemoryOptimization(true);` (disponibile nelle versioni più recenti). |
| TIFF multipagina | Alcuni TIFF più vecchi usano compressioni non supportate. | Converti in un formato supportato prima, oppure usa l’aiutante `TiffImage` di Aspose. |

Di seguito un breve snippet che mostra come rilevare il tipo di file e registrare un messaggio amichevole:

```java
import java.nio.file.*;

String ext = Files.probeContentType(Paths.get(inputPath)).toLowerCase();
if (ext.contains("pdf")) {
    System.out.println("Processing a PDF – expect multiple pages.");
} else if (ext.contains("tiff") || ext.contains("tif")) {
    System.out.println("Processing a TIFF image.");
} else {
    System.out.println("Unsupported file type. This demo works with PDF and TIFF.");
}
```

---

## Step 4: Verificare l'output – Cosa dovresti vedere?

Quando il programma termina, vedrai il testo grezzo estratto stampato sulla console. Per una semplice fattura scansionata, l'output potrebbe apparire così:

```
Invoice #12345
Date: 02/15/2026
Total Amount: $1,250.00
Thank you for your business!
```

Se l'OCR ha difficoltà con una pagina specifica, Aspose inserisce una riga segnaposto come `[Unrecognizable]`. Potrai filtrare queste righe in seguito se ti servono dati puliti.

**Controllo rapido di sanità**

```java
if (ocrResult.getText().trim().isEmpty()) {
    System.err.println("No text detected – verify the image quality or try a different language.");
}
```

---

## Step 5: Ottimizzare le prestazioni – Quando regolare il conteggio dei thread

### Perché è importante

Più thread non significano sempre risultati più rapidi. Su un laptop a 4 core, lanciare 8 thread può generare overhead di cambio di contesto. Al contrario, su un server a 32 core potresti voler sfruttare tutta la potenza disponibile.

### Come trovare il punto ottimale

```java
int cores = Runtime.getRuntime().availableProcessors();
System.out.println("Available processors: " + cores);

// Experiment: set max threads to half the cores first
ocrEngine.getConfig().setMaxThreads(Math.max(1, cores / 2));
```

Esegui il programma con impostazioni diverse e cronometra:

```java
long start = System.nanoTime();
ocrEngine.processImage(inputPath);
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed time (ms): " + elapsed / 1_000_000);
```

Registra i tempi, scegli la configurazione che offre il miglior throughput e fissala per la produzione.

---

## Step 6: Estendere la demo – Elaborazione batch di più file

Se devi **estrarre testo da immagini in Java** da un’intera cartella, avvolgi la logica principale in un ciclo:

```java
Path folder = Paths.get("YOUR_DIRECTORY");
try (DirectoryStream<Path> stream = Files.newDirectoryStream(folder, "*.{tif,tiff,pdf}")) {
    for (Path file : stream) {
        System.out.println("\n--- Processing: " + file.getFileName() + " ---");
        OcrResult result = ocrEngine.processImage(file.toString());
        // Save or further process result.getText()
    }
}
```

Questo schema scala bene perché il motore esegue già in parallelo le pagine di ciascun file. Il ciclo esterno è sequenziale, ma potresti anche inviare ogni file a un `ExecutorService` se devi saturare un’enorme fattoria di CPU.

---

## Problemi comuni e come evitarli

| Sintomo | Causa probabile | Soluzione |
|---------|----------------|-----------|
| `OutOfMemoryError` | Troppi pagine caricate contemporaneamente (specialmente con PDF enormi). | Abilita l'ottimizzazione della memoria (`setMemoryOptimization(true)`) o elabora i PDF pagina‑per‑pagina usando `processPage`. |
| Caratteri distorti | Configurazione errata di lingua/charset. | Chiama `ocrEngine.getConfig().setLanguage(OcrLanguage.English);` o l’enum lingua appropriato. |
| Prestazioni lente nonostante il flag parallelo | Il sistema operativo limita la creazione di thread o la JVM è avviata con un heap ridotto. | Aumenta il flag heap `-Xmx`, e verifica i limiti di thread dell'OS (`ulimit -u`). |
| Output vuoto | Risoluzione dell'immagine di input < 300 dpi. | Ingrandisci l'immagine prima dell'OCR o usa uno scanner che produca una risoluzione più alta. |

---

## Riepilogo – Cosa abbiamo coperto

- **Come usare OCR** in Java con `OcrEngine` di Aspose.  
- Abilitare **l'elaborazione parallela** per velocizzare **l'esecuzione di OCR su PDF** e **l'estrazione di testo da TIFF**.  
- Regolare il conteggio dei thread per ottenere prestazioni ottimali.  
- Gestire casi particolari come PDF di grandi dimensioni, TIFF multipagina e impostazioni linguistiche.  
- Estendere la demo a un elaboratore batch per carichi di lavoro reali.

---

## Prossimi passi

Ora che hai padroneggiato le basi, considera di approfondire questi argomenti correlati:

- **Estrarre testo da immagini in Java** da appunti scritti a mano (abilita `setHandwritingRecognition(true)`).  
- Integrare l'output OCR con Apache Tika per l'estrazione dei metadati.  
- Salvare i risultati in Elasticsearch per archivi documentali ricercabili.  
- Usare l'OCR di Aspose con altri linguaggi come Python o .NET—i principi rimangono gli stessi.

Sentiti libero di sperimentare con limiti di thread diversi, formati immagine e pacchetti lingua. Più giochi, più comprenderai i compromessi tra velocità e precisione.

---

### Buon coding!

Se incontri difficoltà o hai idee per ulteriori ottimizzazioni, lascia un commento qui sotto. Sono sempre disponibile per una discussione su trucchi OCR—senza sforzo, solo codice.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}