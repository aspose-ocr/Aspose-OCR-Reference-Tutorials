---
category: general
date: 2026-10-19
description: Come estrarre testo da un'immagine rapidamente con l'accelerazione GPU
  usando Aspose OCR in Java. Scopri come abilitare la GPU, riconoscere il testo da
  PNG, leggere il testo da una foto e convertire l'immagine in testo.
draft: false
keywords:
- extract text from image
- recognize text from png
- read text from photo
- convert image to text
lastmod: 2026-10-19
og_description: Scopri come estrarre testo da un'immagine con Aspose OCR accelerato
  da GPU in Java. Abilita la GPU, riconosci il testo da PNG, leggi il testo da una
  foto e converti l'immagine in testo in modo efficiente.
og_image_alt: Diagram showing GPU‑accelerated OCR flow from image loading to text
  extraction
og_title: Estrai testo da un'immagine con Aspose OCR accelerato da GPU (Java)
schemas:
- author: Aspose
  dateModified: '2026-10-19'
  description: How to extract text from image quickly with GPU acceleration using
    Aspose OCR in Java. Learn to enable GPU, recognize text from PNG, read text from
    photo, and convert image to text.
  headline: How to extract text from image with GPU‑accelerated Aspose OCR
  type: TechArticle
- description: How to extract text from image quickly with GPU acceleration using
    Aspose OCR in Java. Learn to enable GPU, recognize text from PNG, read text from
    photo, and convert image to text.
  name: How to extract text from image with GPU‑accelerated Aspose OCR
  steps:
  - name: initialize the OCR engine – **how to enable GPU**
    text: '`OcrEngine` is the central class that holds all OCR settings, including
      the GPU flag. > **Why this matters:** Without an `OcrEngine` you have no context
      for the image or the hardware options. Instantiating it early also allows you
      to tweak options before loading the file.'
  - name: load the image you want to process – **extract text from image**
    text: '`ImageStream.fromFile` reads any supported format; PNG is preferred because
      it retains lossless detail. > **Edge case:** If your image lives in a different
      folder, adjust the path accordingly. For large batches, loop over a directory
      and call `setImage` for each file.'
  - name: turn on GPU acceleration – **how to enable GPU**
    text: Calling `setUseGpu(true)` instructs the native library to off‑load the heavy
      lifting to the graphics card. If no compatible GPU is found, Aspose silently
      falls back to CPU, so your application never crashes. > **What if I don’t have
      a GPU?** The call is ignored and OCR runs on the CPU. You can verif
  - name: perform the OCR – **recognize text from PNG**
    text: Invoke `recognize()` to start the analysis. The method returns an `OcrResult`
      object containing raw text, confidence scores, and optional bounding‑box data.
      > **Why wait until now?** The OCR process is computationally intensive; doing
      it after all settings are applied ensures maximum efficiency, esp
  - name: output the detected string – **read text from photo**
    text: 'Print the result to the console. In production you might store it in a
      database or send it over a network, but `System.out.println` keeps the example
      minimal. > **Expected output:** If `sample-photo.png` contains the words “Hello
      World”, the console will display: That’s the whole program—no external'
  type: HowTo
- questions:
  - answer: Yes, Aspose OCR will automatically fall back to CPU if no CUDA‑compatible
      GPU is detected.
    question: Can I use GPU acceleration on any machine?
  - answer: Java 17 or newer is recommended for best performance and long‑term support.
    question: What Java version is required?
  - answer: A free trial works for evaluation; a commercial license is required for
      production use.
    question: Do I need a license for development?
  - answer: Tests show up to 5× speed‑up on an NVIDIA RTX 3080 versus CPU‑only processing.
    question: How much faster is GPU OCR?
  - answer: The Java API runs on Windows, Linux, and macOS; GPU acceleration works
      on any system with an NVIDIA CUDA driver.
    question: Is the code cross‑platform?
  type: FAQPage
tags:
- OCR
- Java
- GPU-Acceleration
title: Come estrarre testo da un'immagine con Aspose OCR accelerato da GPU
url: /it/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-fast-extraction-of-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come estrarre testo con OCR Aspose accelerato da GPU

Ti sei mai chiesto **how to enable GPU** per l'OCR e ottenere risultati istantanei da una foto? Non sei solo. In molti progetti di computer‑vision il collo di bottiglia è il passaggio OCR, soprattutto quando si lavora con file PNG ad alta risoluzione. La buona notizia è che Aspose OCR ti consente di attivare l'accelerazione GPU con una singola riga di codice, riducendo drasticamente i tempi di elaborazione. In questa guida imparerai a **extract text from image** file, **recognize text from PNG** asset, **read text from photo** input e, infine, **convert image to text** usando la libreria Aspose OCR.

## Risposte rapide
- **Can I use GPU acceleration on any machine?** Sì, Aspose OCR tornerà automaticamente alla CPU se non viene rilevata una GPU compatibile CUDA.  
- **What Java version is required?** Java 17 o versioni successive sono consigliate per le migliori prestazioni e il supporto a lungo termine.  
- **Do I need a license for development?** Una prova gratuita è sufficiente per la valutazione; è necessaria una licenza commerciale per l'uso in produzione.  
- **How much faster is GPU OCR?** I test mostrano un'accelerazione fino a 5× su una NVIDIA RTX 3080 rispetto all'elaborazione solo CPU.  
- **Is the code cross‑platform?** L'API Java funziona su Windows, Linux e macOS; l'accelerazione GPU funziona su qualsiasi sistema con driver NVIDIA CUDA.

## Cos'è extract text from image?
L'estrazione di testo da un'immagine si riferisce al processo di conversione dei caratteri visivi presenti in una bitmap — come PNG, JPEG o TIFF — in stringhe ricercabili e modificabili usando la tecnologia di riconoscimento ottico dei caratteri (OCR). Il motore OCR analizza i pattern dei pixel, identifica lettere e numeri e restituisce testo semplice che può essere indicizzato o modificato.

## Perché usare OCR accelerato da GPU?
Aspose OCR supporta **50+ formati di input e output** e può elaborare documenti di centinaia di pagine senza caricare l'intero file in memoria. Quando l'accelerazione GPU è abilitata, lo stesso carico di lavoro OCR che richiede ~2 secondi sulla CPU può terminare in meno di 0,4 secondi su una moderna RTX 3080, offrendo un notevole aumento di produttività per le pipeline di elaborazione batch.

## Prerequisiti

| Requisito | Perché è importante |
|-----------|----------------------|
| Java 17 o versioni successive | Fornisce supporto a lungo termine e miglioramenti di prestazioni rispetto ai runtime più vecchi. |
| Strumento di build Maven o Gradle | Scarica automaticamente la dipendenza `aspose-ocr` e la mantiene aggiornata. |
| Una GPU compatibile CUDA (opzionale) | Abilita la chiamata `setUseGpu(true)` per delegare l'analisi pesante delle immagini alla scheda grafica. |
| Un file immagine (`sample-photo.png`) in una cartella nota | Funge da sorgente per il motore OCR da leggere e convertire. |

Se qualcuna di queste è mancante, puoi comunque eseguire l'esempio; la libreria tornerà semplicemente all'elaborazione CPU.

## Configurazione del progetto

### 1️⃣ aggiungi Aspose OCR al tuo build

Per Maven, aggiungi questo snippet al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest stable version -->
</dependency>
```

Per Gradle, inserisci quanto segue in `build.gradle`:

```gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Pro tip:** Tieni d'occhio il repository Maven di Aspose; rilasciano regolarmente patch di performance.

### 2️⃣ struttura delle directory

Crea una cartella chiamata `resources` nella radice del tuo progetto e inserisci `sample-photo.png` lì. Il codice la referenzierà con un percorso relativo, così non dovrai codificare percorsi assoluti.

## Come abilitare GPU per OCR?

Carica il motore OCR, attiva la GPU e avvia il riconoscimento in tre passaggi concisi. Questa risposta diretta ti indica esattamente cosa fare: istanziare `OcrEngine`, abilitare la GPU con `setUseGpu(true)`, quindi chiamare `recognize()` sull'immagine caricata. L'intera operazione si completa in una singola catena di metodi, offrendoti la massima velocità con un codice minimo.

### Passo 1: inizializza il motore OCR – **how to enable GPU**

`OcrEngine` è la classe centrale che contiene tutte le impostazioni OCR, incluso il flag GPU.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Why this matters:** Senza un `OcrEngine` non hai contesto per l'immagine o le opzioni hardware. Istanziare subito permette anche di modificare le opzioni prima di caricare il file.

### Passo 2: carica l'immagine da elaborare – **extract text from image**

`ImageStream.fromFile` legge qualsiasi formato supportato; PNG è preferito perché conserva i dettagli senza perdita.

```java
        // Step 2: Load the image to be recognized
        ocrEngine.setImage(ImageStream.fromFile("resources/sample-photo.png"));
```

> **Edge case:** Se la tua immagine si trova in una cartella diversa, regola il percorso di conseguenza. Per grandi batch, itera su una directory e chiama `setImage` per ogni file.

### Passo 3: attiva l'accelerazione GPU – **how to enable GPU**

Chiamare `setUseGpu(true)` istruisce la libreria nativa a delegare il lavoro pesante alla scheda grafica. Se non viene trovata una GPU compatibile, Aspose torna silenziosamente alla CPU, così la tua applicazione non si blocca mai.

```java
        // Step 3: Enable GPU acceleration (optional – ignored if no GPU is available)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **Cosa succede se non ho una GPU?** La chiamata viene ignorata e l'OCR viene eseguito sulla CPU. Puoi verificare la modalità in seguito con `ocrEngine.getEngineOptions().isUseGpu()`.

### Passo 4: esegui l'OCR – **recognize text from PNG**

Invoca `recognize()` per avviare l'analisi. Il metodo restituisce un oggetto `OcrResult` contenente testo grezzo, punteggi di confidenza e dati opzionali di bounding‑box.

```java
        // Step 4: Perform the OCR recognition
        OcrResult ocrResult = ocrEngine.recognize();
```

> **Perché aspettare fino a ora?** Il processo OCR è computazionalmente intensivo; eseguirlo dopo aver applicato tutte le impostazioni garantisce la massima efficienza, soprattutto quando la GPU è attiva.

### Passo 5: output della stringa rilevata – **read text from photo**

Stampa il risultato sulla console. In produzione potresti memorizzarlo in un database o inviarlo su una rete, ma `System.out.println` mantiene l'esempio minimale.

```java
        // Step 5: Output the recognized text
        System.out.println("Detected text:");
        System.out.println(ocrResult.getText());

        // Optional: Verify GPU usage
        System.out.println("GPU used: " + ocrEngine.getEngineOptions().isUseGpu());
    }
}
```

> **Expected output:** Se `sample-photo.png` contiene le parole “Hello World”, la console mostrerà:

```
Detected text:
Hello World
GPU used: true
```

Questo è l'intero programma—nessun servizio esterno, nessun file di configurazione nascosto.

## Panoramica visiva

![come abilitare gpu per OCR](gpu-ocr-diagram.png "Diagramma che mostra il flusso dal caricamento dell'immagine all'OCR accelerato da GPU")

[come abilitare gpu per OCR](gpu-ocr-diagram.png "Diagramma che mostra il flusso dal caricamento dell'immagine all'OCR accelerato da GPU")

*Il diagramma illustra ogni passaggio della pipeline, enfatizzando dove si trova il flag **how to enable GPU**.*

## Domande comuni & edge case

| Domanda | Risposta |
|----------|----------|
| **Can I process multiple images in one run?** | Sì. Avvolgi i passaggi 2‑5 in un ciclo `for (File img : folder.listFiles())` e chiama `ocrEngine.setImage` per ogni file. |
| **What image formats are supported?** | JPEG, PNG, BMP, TIFF e GIF sono tutti supportati nativamente da Aspose OCR. |
| **How do I handle low‑quality scans?** | Imposta `ocrEngine.getEngineOptions().setPreprocessMode(PreprocessMode.Auto)` prima del riconoscimento per far sì che il motore pulisca automaticamente il rumore. |
| **Is there a way to get confidence scores?** | `ocrResult.getMeanConfidence()` restituisce una confidenza media (0‑100). La confidenza per singolo carattere è disponibile tramite `ocrResult.getTextLines()`. |
| **Will this work on macOS with Metal GPU?** | Aspose OCR attualmente utilizza CUDA solo su GPU NVIDIA. Su macOS tornerai alla CPU a meno che non usi un eGPU NVIDIA. |

## Suggerimenti sulle prestazioni

1. **Batch processing:** Carica tutte le immagini in memoria prima, abilita la GPU una sola volta, poi esegui il ciclo. Questo riduce l'overhead del driver.  
2. **Image resizing:** Ridimensiona i PNG molto grandi a un massimo di 2000 px sul lato più lungo; l'accuratezza OCR rimane alta mentre l'uso della memoria GPU diminuisce.  
3. **Warm‑up call:** Esegui un `recognize()` fittizio su un'immagine piccola prima del carico di lavoro reale per consentire al driver GPU di inizializzarsi—questo può ridurre di qualche millisecondo la prima immagine reale.

## Riepilogo & prossimi passi

Abbiamo coperto **how to enable GPU** per Aspose OCR, mostrato come **extract text from image** file, dimostrato **recognize text from PNG**, e guidato attraverso i flussi di lavoro **read text from photo** e **convert image to text**. Lo snippet Java completo sopra è pronto per il copy‑paste, e le note sulle prestazioni dovrebbero aiutarti a spremere ogni millisecondo dal tuo hardware.

Cosa segue? Considera di estendere la soluzione a:

* **Export OCR results to JSON** per analisi successive.  
* **Integrate with a Spring Boot REST endpoint** così altri servizi possono inviare foto e ricevere risposte in testo semplice.  
* **Apply language‑specific dictionaries** tramite `ocrEngine.getEngineOptions().setLanguage(Language.English)` per migliorare l'accuratezza su documenti multilingue.

Sentiti libero di sperimentare—sostituisci il PNG con un PDF scansionato, abilita `setPreserveFormatting(true)`, o concatenare più passaggi OCR per immagini rumorose. Il cielo è il limite una volta che hai padroneggiato **how to enable GPU** per OCR.

---

**Ultimo aggiornamento:** 2026-10-19  
**Testato con:** Aspose OCR 24.11 for Java  
**Autore:** Aspose

## Tutorial correlati

- [Come abilitare GPU per OCR in Java - Estrarre testo da immagine](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)
- [Riconoscere testo immagine usando Aspose OCR GPU Java](/ocr/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/)
- [OCR batch di immagini in Java - Estrarre testo da file PNG velocemente](/ocr/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}