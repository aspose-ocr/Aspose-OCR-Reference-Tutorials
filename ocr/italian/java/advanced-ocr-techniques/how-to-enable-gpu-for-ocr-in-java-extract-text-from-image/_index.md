---
category: general
date: 2026-10-19
description: Scopri come abilitare la GPU nel codice Aspose OCR Java per estrarre
  testo da immagine. Converti foto in testo e riconosci il testo dalla foto in modo
  efficiente.
draft: false
keywords:
- how to enable gpu
- extract text from image
- convert photo to text
- how to extract text
- recognize text from photo
lastmod: 2026-10-19
og_description: Abilitare la GPU per l'OCR in Java ti consente di estrarre testo da
  immagine rapidamente, riducendo i tempi di elaborazione fino al 90% su GPU moderne.
  Scopri la configurazione step‑by‑step, i code snippets e i consigli di troubleshooting.
og_image_alt: Diagram illustrating how to enable GPU in Aspose OCR Java code – how
  to enable gpu
og_title: Come abilitare la GPU per l'OCR in Java – estrazione rapida del testo
schemas:
- author: Aspose
  dateModified: '2026-10-19'
  description: Learn how to enable GPU in Aspose OCR Java code to extract text from
    image. Convert photo to text and recognize text from photo efficiently.
  headline: How to Enable GPU for OCR in Java – Extract Text from Image
  type: TechArticle
- questions:
  - answer: Yes, as long as you have a Metal‑compatible GPU and the appropriate Aspose
      OCR binary for macOS. The same `setUseGpu(true)` call applies.
    question: Does this work on macOS?
  - answer: The Community Edition includes CPU‑only inference. To unlock GPU you need
      a licensed version (or a trial that includes GPU support).
    question: Can I use the free Community Edition?
  - answer: Call `ocrEngine.getConfig().setLanguage("spa")` for Spanish, `"fra"` for
      French, etc. Language packs are bundled with the library.
    question: What if I need to **recognize text from photo** in a language other
      than English?
  - answer: Yes—`ocrResult.getWords()` returns a collection where each `Word` object
      has a `getConfidence()` method.
    question: Is there a way to get confidence scores for each word?
  - answer: After creating the engine, invoke `ocrEngine.getConfig().setRequireGpu(true)`.
      The library will throw an exception if no compatible GPU is found, preventing
      silent CPU fallback.
    question: How can I enforce a strict GPU‑only mode?
  type: FAQPage
tags:
- OCR
- Java
- GPU
- Aspose
title: Come abilitare la GPU per l'OCR in Java – Estrarre testo da immagine
url: /it/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come abilitare la GPU per OCR in Java – estrarre testo da immagine

Ti sei mai chiesto **come abilitare la GPU** quando esegui OCR su una foto ad alta risoluzione? Non sei solo. Molti sviluppatori Java si trovano in difficoltà quando la loro pipeline OCR rallenta su un setup solo CPU, soprattutto quando le dimensioni dell'immagine superano qualche megapixel. La buona notizia? Abilitare l'accelerazione GPU con Aspose OCR è un gioco da ragazzi, e ti permette di **estrarre testo da immagine** in una frazione del tempo.

In questo tutorial percorreremo l'intero processo: dall'installazione della libreria Aspose OCR, all'attivazione del flag GPU, al caricamento di un'immagine grande, e infine **convertire foto in testo**. Alla fine saprai **come abilitare la GPU** in modo affidabile, e vedrai anche come **riconoscere testo da foto** su macchine con più GPU. Nessun riferimento esterno necessario—tutto ciò che ti serve è qui.

## Risposte rapide
- **Cosa fa “abilitare la GPU”?** Sposta l'inferenza della rete neurale OCR sulla scheda grafica, riducendo il tempo di elaborazione fino al 90 % su hardware moderno.  
- **Ho bisogno di una licenza speciale?** Sì, il supporto GPU è disponibile solo nell'edizione licenziata di Aspose OCR per Java (o in una versione di prova che includa i kernel GPU).  
- **Quali GPU sono supportate?** GPU NVIDIA con CUDA 12.x (capacità di calcolo 3.5+) e GPU AMD con ROCm 5.x (capacità di calcolo 6.0+).  
- **Posso tornare automaticamente alla CPU?** La libreria rileva GPU mancanti o incompatibili e passa trasparentemente alla CPU, ma è possibile imporre una modalità solo GPU.  
- **Il codice è compatibile con Java 17?** Assolutamente—Aspose OCR 23.x è destinato a Java 11+ e funziona perfettamente con Java 17.

## Cos'è l'accelerazione GPU per OCR?

L'accelerazione GPU per OCR è il processo di utilizzo di un processore grafico per eseguire i modelli di deep‑learning che riconoscono i caratteri, invece della CPU. Questo velocizza notevolmente l'estrazione del testo, soprattutto per immagini grandi o elaborate in batch. Spostando i pesanti strati convoluzionali sulla GPU, la latenza diminuisce e il throughput aumenta, rendendo possibile l'elaborazione in tempo reale per foto ad alta risoluzione.

## Perché usare la modalità GPU di Aspose OCR?

Aspose OCR supporta **oltre 50 formati di input** (JPEG, PNG, BMP, TIFF, PDF, ecc.) e può elaborare un'immagine da 20 MP in meno di un secondo su una RTX 3080, rispetto a 8 secondi su una CPU di fascia alta. La libreria fornisce anche fallback integrato, pacchetti linguistici per più di 30 lingue e una semplice API Java che richiede solo un singolo flag per abilitare la GPU.

## Prerequisiti

- Java 17 o versioni successive installate.  
- Una GPU NVIDIA o AMD supportata con driver aggiornati (CUDA 12.x per NVIDIA, ROCm 5.x per AMD).  
- JAR di Aspose OCR per Java – scarica l'ultima versione 23.x dal sito Aspose.  
- Maven o Gradle per gestire le dipendenze (mostreremo uno snippet Maven).  
- Un'immagine ad alta risoluzione (ad es., `high-res-photo.jpg`) che desideri elaborare.

Se qualcuno di questi manca, il codice compilerà comunque, ma il flag GPU sarà ignorato e si tornerà all'elaborazione CPU.

## Come abilitare la GPU per OCR in Java?

Carica il motore OCR, chiama `setUseGpu(true)` ed esegui l'immagine tramite il metodo `recognize`. Quella singola riga attiva i kernel GPU che alimentano la rete neurale convoluzionale. **`setUseGpu(true)` abilita l'elaborazione GPU per il motore OCR.** Il motore OCR è un'istanza di `com.aspose.ocr.OcrEngine` che esegue il riconoscimento del testo.

## Passo 1 – aggiungere Aspose OCR al tuo build (come abilitare la GPU)

Prima di tutto: indica al tuo progetto dove trovare la libreria OCR. In Maven, aggiungi la seguente dipendenza al tuo `pom.xml`:

```xml
<!-- Step 1: Include Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

> **Suggerimento:** Se usi Gradle, l'equivalente è `implementation 'com.aspose:aspose-ocr:23.10'`. Mantenere la libreria aggiornata garantisce di ottenere i kernel GPU più recenti e le correzioni di bug.

Ora che la libreria è nel classpath, possiamo effettivamente **abilitare la GPU** nel motore OCR.

## Passo 2 – creare il motore OCR e attivare la GPU (come abilitare la GPU)

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Instantiate the OCR engine – this is the core object.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Enable GPU acceleration.
        // This is the line that answers the question "how to enable gpu".
        ocrEngine.getConfig().setUseGpu(true);

        // Optional: If your system has more than one GPU, pick the one you want.
        // The device ID is zero‑based, so 0 refers to the first GPU.
        // ocrEngine.getConfig().setGpuDeviceId(0);

        // Step 2.3: Process the image and get the result.
        OcrResult ocrResult = ocrEngine.processImage("YOUR_DIRECTORY/high-res-photo.jpg");

        // Step 2.4: Print the recognized text – now you have converted photo to text.
        System.out.println(ocrResult.getText());
    }
}
```

> **Perché è importante:** Impostare `setUseGpu(true)` indica alla libreria nativa sottostante di spostare il lavoro pesante della rete neurale convoluzionale sulla GPU. Su una moderna RTX 3080, la stessa immagine che richiede 8 secondi sulla CPU può essere elaborata in meno di 1 secondo. Se salti questo passo, **riconoscerai comunque il testo da foto**, ma non otterrai i miglioramenti di prestazioni.

## Passo 3 – verificare che la GPU sia effettivamente in uso

Potresti chiederti, “La GPU sta davvero facendo il lavoro?” Il modo più semplice per verificarlo è osservare l'output della console della libreria Aspose OCR quando abiliti il logging di debug:

```java
// Enable verbose logging – helpful for confirming GPU usage.
ocrEngine.getConfig().setLogLevel(com.aspose.ocr.Config.LogLevel.DEBUG);
```

Quando esegui il programma, vedrai righe come:

```
[DEBUG] Using GPU device 0 (NVIDIA GeForce RTX 3080) for OCR processing.
```

Se non vedi quel messaggio, ricontrolla l'installazione dei driver e assicurati che la GPU soddisfi la capacità di calcolo minima (3.5 per NVIDIA, 6.0 per AMD).

## Passo 4 – gestire più GPU e casi limite

### Selezionare una GPU diversa

Se la tua workstation ha più di una GPU (ad esempio, una GPU integrata Intel e una scheda NVIDIA dedicata), puoi puntare a quella più veloce:

```java
ocrEngine.getConfig().setGpuDeviceId(1); // 1 = second GPU in the system
```

### Cosa succede se non viene rilevata alcuna GPU?

Aspose OCR ricade elegantemente sulla CPU quando non riesce a trovare una GPU adatta. Per evitare il fallback silenzioso, puoi aggiungere una protezione. **`setRequireGpu(true)` forza la libreria a usare una GPU e lancia un'eccezione se non ne trova alcuna.** Questo ti assicura di essere consapevole quando la GPU non è disponibile.

```java
if (!ocrEngine.getConfig().isGpuAvailable()) {
    throw new IllegalStateException("No compatible GPU found – cannot enable GPU acceleration.");
}
```

### Immagini grandi e limiti di memoria

Elaborare un'immagine da 100 MP può comunque esaurire la memoria GPU. Un trucco pratico è ridimensionare l'immagine **giusto il necessario** per rimanere entro i limiti di memoria mantenendo la chiarezza del testo:

```java
ocrEngine.getConfig().setMaxImageDimension(4096); // caps width/height to 4096px
```

### Formati immagine supportati

Aspose OCR riconosce JPEG, PNG, BMP, TIFF e anche PDF. Se devi **estrarre testo da immagine** da file memorizzati in un formato diverso, convertili prima usando una libreria come ImageIO.

## Passo 5 – output previsto e verifica

Quando il programma termina, la console stamperà il testo OCR grezzo. Per una tipica foto di ricevuta, potresti vedere:

```
Store: Coffee Corner
Date: 2026-02-25
Items:
  - Latte $4.50
  - Croissant $2.75
Total: $7.25
```

Se l'output appare confuso, considera:

* Assicurarsi che l'immagine sia ben illuminata e non eccessivamente compressa.  
* Regolare l'opzione `setLanguage` se il testo non è in inglese.  
* Verificare che la versione del kernel GPU corrisponda al driver (versioni non corrispondenti possono causare artefatti sottili).

**`ocrResult.getWords()` restituisce una collezione di oggetti `Word`, ognuno dei quali fornisce un punteggio di confidenza tramite `getConfidence()`.** Questo ti permette di filtrare i risultati a bassa confidenza.

## Passo 6 – andare oltre: elaborazione batch e chiamate asincrone

I progetti reali spesso hanno bisogno di **estrarre testo da immagine** da collezioni. Puoi avvolgere la logica sopra in un ciclo o usare `CompletableFuture` di Java per eseguire più job OCR in parallelo, ciascuno su un flusso GPU separato (se l'hardware lo supporta). Ecco uno schizzo veloce:

```java
import java.util.concurrent.*;
import java.nio.file.*;

public class BatchGpuOcr {
    public static void main(String[] args) throws Exception {
        ExecutorService pool = Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors());

        Files.list(Paths.get("photos/"))
             .filter(p -> p.toString().endsWith(".jpg"))
             .forEach(path -> pool.submit(() -> {
                 OcrEngine engine = new OcrEngine();
                 engine.getConfig().setUseGpu(true);
                 OcrResult result = engine.processImage(path.toString());
                 System.out.println("Result for " + path.getFileName() + ":\n" + result.getText());
             }));

        pool.shutdown();
        pool.awaitTermination(1, TimeUnit.HOURS);
    }
}
```

Questo approccio ti consente di **convertire foto in testo** su larga scala mantenendo i vantaggi dell'accelerazione GPU.

## Domande frequenti (FAQ)

**D: Funziona su macOS?**  
R: Sì, purché tu abbia una GPU compatibile con Metal e il binario Aspose OCR appropriato per macOS. Vale la stessa chiamata `setUseGpu(true)`.

**D: Posso usare la Community Edition gratuita?**  
R: La Community Edition include solo inferenza CPU. Per sbloccare la GPU è necessaria una versione licenziata (o una versione di prova che includa il supporto GPU).

**D: Cosa succede se devo **riconoscere testo da foto** in una lingua diversa dall'inglese?**  
R: Chiama `ocrEngine.getConfig().setLanguage("spa")` per lo spagnolo, `"fra"` per il francese, ecc. I pacchetti linguistici sono inclusi nella libreria.

**D: È possibile ottenere i punteggi di confidenza per ogni parola?**  
R: Sì—`ocrResult.getWords()` restituisce una collezione dove ogni oggetto `Word` ha un metodo `getConfidence()`.

**D: Come posso imporre una modalità solo GPU?**  
R: Dopo aver creato il motore, invoca `ocrEngine.getConfig().setRequireGpu(true)`. La libreria lancerà un'eccezione se non trova una GPU compatibile, evitando il fallback silenzioso alla CPU.

## Conclusione

Abbiamo coperto **come abilitare la GPU** per Aspose OCR in Java, illustrato un esempio completo e eseguibile, ed esplorato le difficoltà comuni quando vuoi **estrarre testo da immagine**, **convertire foto in testo**, o **riconoscere testo da foto**. Attivando un singolo flag e assicurandoti che i driver siano aggiornati, puoi risparmiare secondi su ogni chiamata OCR e scalare a enormi batch di immagini senza sforzo.

Pronto per il passo successivo? Prova a inviare l'output OCR in una pipeline di elaborazione del linguaggio naturale, o sperimenta diversi filtri di pre‑elaborazione delle immagini per aumentare la precisione. Il cielo è il limite quando combini OCR potenziato da GPU con gli strumenti Java moderni.

---

![Diagramma che mostra come abilitare la GPU nel codice Aspose OCR Java – come abilitare gpu](gpu-ocr-diagram.png)

[Diagramma che mostra come abilitare la GPU nel codice Aspose OCR Java – come abilitare gpu](gpu-ocr-diagram.png)

*Testo alternativo dell'immagine:* "Diagramma che illustra come abilitare la GPU nel codice Aspose OCR Java – come abilitare gpu"

---

**Ultimo aggiornamento:** 2026-10-19  
**Testato con:** Aspose OCR per Java 23.10  
**Autore:** Aspose  

```xml
<!-- Step 1: Include Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

## Tutorial correlati

- [Come configurare GPU per OCR Riconoscere testo da immagine](/ocr/java/advanced-ocr-techniques/how-to-configure-gpu-for-ocr-recognize-text-from-image/)
- [Riconoscere testo immagine usando Aspose OCR GPU Java](/ocr/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/)
- [Estrarre testo da immagine con guida Aspose OCR Java](/ocr/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}