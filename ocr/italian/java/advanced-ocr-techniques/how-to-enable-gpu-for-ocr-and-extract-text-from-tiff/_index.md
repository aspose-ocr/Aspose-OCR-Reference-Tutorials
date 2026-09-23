---
category: general
date: 2026-09-23
description: Impara come estrarre testo da file tiff rapidamente abilitando l'accelerazione
  GPU in Aspose OCR for Java. Guida passo‑passo che copre il caricamento del TIFF,
  l'impostazione dell'ID del dispositivo GPU e la lettura del testo.
draft: false
keywords:
- extract text from tiff file
- gpu acceleration java
- ocr tiff java
- aspose ocr gpu
lastmod: 2026-09-23
og_description: Impara come estrarre testo da file tiff rapidamente abilitando l'accelerazione
  GPU in Aspose OCR for Java. La guida mostra il caricamento del TIFF, la selezione
  di un dispositivo GPU e la lettura del testo estratto.
og_image_alt: 'Tutorial image: enabling GPU for OCR in Java'
og_title: Estrai testo da file tiff con accelerazione GPU in OCR Java
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to extract text from tiff file quickly by enabling GPU acceleration
    in Aspose OCR for Java. Step‑by‑step guide covers loading TIFF, setting GPU device
    ID, and reading text.
  headline: How to extract text from tiff file using GPU in OCR Java
  type: TechArticle
- questions:
  - answer: Absolutely—Aspose OCR runs on Windows, Linux, and macOS as long as the
      CUDA toolkit and drivers are installed.
    question: Does this work on Linux?
  - answer: Omit the `setUseGpu(true)` call or explicitly call `setUseGpu(false)`;
      the engine will run on CPU.
    question: What if I don’t have a GPU?
  - answer: Yes. `setImage` accepts JPEG, PNG, BMP, PDF, and more.
    question: Can I extract text from other formats?
  - answer: Accuracy drops sharply below 300 dpi. Pre‑process the image (binarization,
      deskew) for better results.
    question: How accurate is OCR on low‑resolution TIFFs?
  - answer: The library handles 30+ raster and document formats, including TIFF, JPEG,
      PNG, BMP, PDF, and GIF.
    question: How many formats does Aspose OCR support?
  type: FAQPage
tags:
- OCR
- Java
- GPU acceleration
title: Come estrarre testo da file tiff usando GPU in OCR Java
url: /it/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-and-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come estrarre testo da file tiff usando la GPU in OCR Java

Se hai bisogno di **estrarre testo da file tiff** rapidamente, attivare l'accelerazione GPU in Aspose OCR for Java è il modo più veloce. Nei primi 100 parole spiegheremo perché la GPU è importante, poi ti guideremo attraverso il caricamento di un TIFF, l'abilitazione della GPU, l'eventuale scelta di un dispositivo specifico, l'esecuzione dell'OCR e infine la lettura del testo estratto. Alla fine sarai in grado di convertire un TIFF in testo con poche righe di codice.

## Risposte rapide
- **Qual è il principale vantaggio dell'OCR con GPU?** Fino a 5× più veloce per l'elaborazione di grandi TIFF multi‑pagina.  
- **Quale versione di Java è richiesta?** Java 17 o successiva (Java 8+ funziona comunque).  
- **È necessaria una licenza speciale?** È richiesta una licenza valida di Aspose OCR for Java per l'uso in produzione.  
- **Posso eseguirlo su Linux?** Sì—Aspose OCR è cross‑platform; basta installare il toolkit CUDA.  
- **La GPU è opzionale?** Puoi tornare alla CPU chiamando `setUseGpu(false)`.

## Cos'è OcrEngine?
La classe `OcrEngine` è il componente centrale di Aspose OCR for Java. Incapsula tutte le funzionalità OCR, consentendoti di caricare immagini, configurare le opzioni di elaborazione come lingua e utilizzo della GPU, e recuperare il testo riconosciuto e i dati di confidenza in un oggetto comodo.

`OcrEngine` è la classe core di Aspose OCR che rappresenta il motore di elaborazione OCR e fornisce metodi per caricare immagini, configurare opzioni e recuperare i risultati.

## Come abilitare la GPU per OCR in Java?
Carica la tua immagine, attiva la GPU e chiama `recognize`—tutto quello che ti serve. Abilitare la GPU con `setUseGpu(true)` consente al motore di delegare il lavoro intensivo di pixel alla scheda grafica, riducendo drasticamente i tempi di elaborazione, specialmente per TIFF ad alta risoluzione o multi‑pagina.

## Di cosa avrai bisogno

- Java 17 o successiva (il codice funziona anche su Java 8+).  
- Aspose OCR for Java 23.10 (o l'ultima versione).  
- Una GPU compatibile con CUDA con l'ultimo driver installato.  
- Un file TIFF multi‑pagina di esempio (ad es., `sample_large.tif`).  

Nessun Maven? Basta inserire il JAR nel tuo classpath.

![How to enable GPU tutorial](gpu-ocr.png)

[How to enable GPU tutorial](gpu-ocr.png)

*Testo alternativo immagine: Come abilitare la GPU per OCR in Java*

## Passo 1: caricare un'immagine TIFF per OCR

Il metodo `setImage` avvolge il file in un `ImageStream`, consentendo al motore di gestire TIFF multi‑pagina senza divisione manuale. Se il file non viene trovato, viene lanciata una chiara `FileNotFoundException`.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the TIFF file – this is where we "read text from TIFF"
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample_large.tif"));
```

> **Perché è importante:** La chiamata `setImage` astrae la gestione delle pagine, così puoi elaborare un intero documento con una singola istanza del motore.

## Passo 2: abilitare l'accelerazione GPU

Attivare la GPU è un singolo flag booleano. Nella maggior parte dei sistemi la GPU predefinita è il dispositivo 0, ma puoi lasciare che Aspose selezioni automaticamente il dispositivo ottimale.

```java
        // Enable GPU acceleration (requires a supported driver)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **Consiglio professionale:** Su workstation con più GPU, specificare l'ID del dispositivo evita il passaggio inaspettato a una GPU integrata più lenta.

## Passo 3: impostare l'ID della GPU (opzionale)

Se sai quale GPU dovrebbe gestire l'OCR—ad esempio una scheda AI dedicata—puoi impostarla esplicitamente con `setGpuDeviceId`.  

```java
        // Optional: select the GPU device (0 = first device, 1 = second, etc.)
        ocrEngine.getEngineOptions().setGpuDeviceId(0);
```

> **Caso limite:** Passare un ID non valido genera `IllegalArgumentException`. Usa `ocrEngine.getEngineOptions().getAvailableGpuDevices()` per elencare gli ID validi.

## Passo 4: elaborare l'immagine ed estrarre il testo dall'immagine

Eseguire l'OCR restituisce un `OcrResult` che contiene la stringa semplice e, facoltativamente, i punteggi di confidenza.  

```java
        // Perform OCR – this is where we "convert TIFF to text"
        OcrResult ocrResult = ocrEngine.process();

        // Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Output previsto

Se il TIFF contiene “Hello, World!” il risultato sarà simile a:

```
Recognized text:
Hello, World!
```

Il motore gestisce automaticamente interruzioni di riga, punteggiatura e rilevamento di layout di base. Per l'estrazione per pagina, esplora `ocrResult.getPages()`.

## Passo 5: verificare l'output e gestire i problemi comuni

La GPU può essere bypassata per diversi motivi. Se la versione del driver installato è più vecchia del minimo richiesto, la libreria non può inizializzare CUDA. Memoria video insufficiente può far ricadere il motore sulla CPU, e alcune grafiche integrate non hanno la capacità di calcolo necessaria per l'accelerazione OCR.

### Perché la GPU potrebbe non essere utilizzata?

- **Incompatibilità driver:** Il driver GPU deve soddisfare la versione minima elencata nelle note di rilascio di Aspose.  
- **Memoria insufficiente:** Immagini molto grandi possono superare la VRAM; il motore ricade allora sulla CPU e registra un avviso.  
- **Hardware non supportato:** Le grafiche integrate spesso non hanno la capacità di calcolo richiesta.

### Come ricadere sulla CPU programmaticamente

Se devi garantire l'elaborazione su CPU, chiama il setter delle opzioni del motore con un flag false. Questo disabilita qualsiasi tentativo di usare la GPU e forza la pipeline OCR a funzionare interamente sul processore host, utile su macchine senza schede grafiche compatibili.

```java
if (!ocrEngine.getEngineOptions().isGpuAvailable()) {
    System.out.println("GPU not available – switching to CPU.");
    ocrEngine.getEngineOptions().setUseGpu(false);
}
```

### Leggere testo da TIFF in un ciclo

Durante l'elaborazione di molti file, itera su una directory mantenendo l'accelerazione GPU attiva.

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".tif"))) {
    ocrEngine.setImage(ImageStream.fromFile(file.getAbsolutePath()));
    OcrResult result = ocrEngine.process();
    System.out.println("File: " + file.getName());
    System.out.println(result.getText());
}
```

Questa porzione di codice mostra come **leggere testo da file TIFF** in blocco senza perdere il vantaggio di prestazioni.

## Domande frequenti (FAQ)

**D: Questo funziona su Linux?**  
R: Assolutamente—Aspose OCR funziona su Windows, Linux e macOS purché il toolkit CUDA e i driver siano installati.

**D: E se non ho una GPU?**  
R: Ometti la chiamata `setUseGpu(true)` o chiama esplicitamente `setUseGpu(false)`; il motore verrà eseguito sulla CPU.

**D: Posso estrarre testo da altri formati?**  
R: Sì. `setImage` accetta JPEG, PNG, BMP, PDF e altri.

**D: Quanto è accurato l'OCR su TIFF a bassa risoluzione?**  
R: L'accuratezza diminuisce drasticamente sotto i 300 dpi. Pre‑elabora l'immagine (binarizzazione, correzione inclinazione) per risultati migliori.

**D: Quanti formati supporta Aspose OCR?**  
R: La libreria gestisce più di 30 formati raster e documenti, inclusi TIFF, JPEG, PNG, BMP, PDF e GIF.

## Conclusione

Ora sai **come estrarre testo da file tiff** usando l'accelerazione GPU in Aspose OCR for Java, come impostare un ID di dispositivo GPU specifico e come elaborare TIFF singoli o multipli in modo efficiente. Attivando un singolo flag ottieni miglioramenti di velocità enormi senza modificare alcuna logica OCR.

Passi successivi che potresti provare:

- Elaborazione batch di centinaia di TIFF in thread paralleli.  
- Caricamento di pacchetti linguistici personalizzati per migliorare il riconoscimento di vocabolari specializzati.  
- Post‑elaborazione del testo estratto con regex per pulire la formattazione.

Se incontri problemi, lascia un commento qui sotto. Buona programmazione!

---

**Ultimo aggiornamento:** 2026-09-23  
**Testato con:** Aspose OCR for Java 23.10  
**Autore:** Aspose

## Tutorial correlati

- [Come abilitare GPU per OCR Java Guida passo passo](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-step-by-step-guide/)
- [Riconoscere testo da immagine con Aspose OCR Guida completa Java](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/)
- [Preprocessare immagine OCR in Java per aumentare precisione estrazione testo](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}