---
category: general
date: 2026-04-29
description: Impara a riconoscere il testo da un'immagine usando Aspose OCR in Java.
  Include i passaggi per estrarre il testo da un JPG, caricare l'immagine per l'OCR
  e impostare l'ID del dispositivo GPU.
draft: false
keywords:
- recognize text from image
- extract text from jpg
- how to extract text image
- load image for OCR
- set GPU device ID
language: it
og_description: Riconosci rapidamente il testo da un'immagine con Aspose OCR. Questa
  guida mostra come caricare un'immagine per l'OCR, estrarre il testo da un JPG e
  impostare l'ID del dispositivo GPU.
og_title: Riconosci il testo da un'immagine – OCR Java con accelerazione GPU
tags:
- Java
- OCR
- GPU
- Aspose
title: Riconoscere il testo da un'immagine – OCR Java con accelerazione GPU
url: /it/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere testo da immagine – Java OCR con accelerazione GPU

Hai mai provato a riconoscere il testo da un'immagine e ti sei ritrovato con un output incomprensibile? Non sei solo. In molti progetti—che tu stia digitalizzando ricevute, scansionando passaporti o estraendo dati dalle etichette dei prodotti—la qualità dell'OCR può fare la differenza per l'intera pipeline.  

La buona notizia? Con Aspose OCR puoi **recognize text from image** in pochi secondi, e se disponi di una GPU compatibile CUDA, puoi ridurre ulteriormente i tempi di elaborazione. In questo tutorial vedremo come caricare un'immagine per l'OCR, abilitare l'accelerazione GPU e infine estrarre il testo da un file JPG. Alla fine saprai esattamente come **extract text from jpg** files, come impostare l'ID del dispositivo GPU e perché ogni passaggio è importante.

## Cosa ti servirà

- **Java Development Kit (JDK) 11+** – il codice utilizza le funzionalità standard del linguaggio Java.  
- **Aspose OCR for Java** library (ultima versione al 2026). Puoi ottenerla da Maven Central o scaricare il JAR dal sito web di Aspose.  
- **GPU con supporto CUDA** con driver 11+ (opzionale ma altamente consigliato per la velocità).  
- Un'immagine di esempio, ad esempio `sample.jpg`, posizionata in una cartella a cui puoi fare riferimento dal tuo codice.  

Nessun servizio esterno, nessuna chiave cloud—solo un progetto Java locale e una macchina pronta per la GPU.

## Passo 1 – Carica l'immagine per l'OCR

Prima di poter riconoscere il testo, devi fornire al motore OCR qualcosa da leggere. È qui che entra in gioco il passaggio **load image for OCR**.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and load the image
        OcrEngine engine = new OcrEngine();

        // Load a JPG file – this is the “extract text from jpg” part
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

> **Why this matters:** Il metodo `ImageStream.fromFile` supporta molti formati (JPG, PNG, BMP). Usare un JPG mantiene le dimensioni del file ridotte, il che è particolarmente utile quando si elaborano centinaia di immagini su una GPU.

## Passo 2 – Abilita l'accelerazione GPU e imposta l'ID del dispositivo GPU

Se la tua macchina ha una GPU compatibile CUDA, puoi dire ad Aspose OCR di eseguire il lavoro pesante sulla scheda grafica. Questo è il passaggio **set GPU device ID**.

```java
        // Step 2: Enable GPU acceleration (requires CUDA 11+ and a compatible driver)
        engine.getProcessingSettings().setUseGpu(true);

        // Optional: Choose a specific GPU device (0 = first GPU)
        engine.getProcessingSettings().setGpuDeviceId(0);
```

> **Pro tip:** Se hai più GPU, puoi sperimentare con valori diversi di `gpuDeviceId` per vedere quale offre le migliori prestazioni. Il valore predefinito (`0`) di solito punta alla GPU primaria.

## Passo 3 – Esegui il processo OCR

Ora che l'immagine è caricata e il motore è pronto per il lavoro su GPU, è il momento di riconoscere effettivamente i caratteri.

```java
        // Step 3: Run the OCR process
        OcrResult result = engine.recognize();
```

> **What’s happening under the hood?** Il motore OCR suddivide l'immagine in linee di testo, esegue una rete neurale su ogni segmento e ricompone i risultati. Quando `setUseGpu(true)` è attivo, questa rete neurale gira sulla GPU invece che sulla CPU, riducendo drasticamente la latenza.

## Passo 4 – Estrai e visualizza il testo riconosciuto

L'ultimo pezzo del puzzle è **extract text from jpg** e mostrarlo all'utente. L'oggetto `OcrResult` contiene il testo semplice, i punteggi di confidenza e persino le bounding box se ti servono in seguito.

```java
        // Step 4: Display the recognized text
        System.out.println("Recognized text:");
        System.out.println(result.getText());

        // Optional: Print confidence (helps with quality checks)
        System.out.println("Overall confidence: " + result.getConfidence());
    }
}
```

### Output previsto

Se `sample.jpg` contiene la frase “Hello World”, la console dovrebbe stampare:

```
Recognized text:
Hello World
Overall confidence: 0.98
```

Il valore di confidenza varia da 0 a 1; valori superiori a 0,8 sono generalmente affidabili per scansioni pulite.

## Passo 5 – Varianti comuni e casi limite

### Lavorare con file PNG o BMP

Se la tua immagine di origine non è un JPG, cambia semplicemente l'estensione del file:

```java
engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.png"));
```

Il resto del flusso di lavoro rimane identico—**how to extract text image** non dipende dal formato del file finché Aspose lo supporta.

### Gestire immagini a bassa risoluzione

Le immagini a bassa risoluzione spesso producono punteggi di confidenza più bassi. Puoi migliorare i risultati:

1. Upscaling the image with a library like OpenCV before feeding it to Aspose.  
2. Adjusting `engine.getProcessingSettings().setResolution(300);` per forzare un DPI più alto durante l'elaborazione interna.

### Eseguire solo su CPU

Se non disponi di una GPU compatibile CUDA, basta saltare le righe relative alla GPU:

```java
engine.getProcessingSettings().setUseGpu(false);
```

L'OCR tornerà a utilizzare la CPU, che è più lenta ma comunque perfettamente funzionale.

## Suggerimenti pratici per la produzione

- **Batch Processing:** Avvolgi la logica OCR in un ciclo e riutilizza la stessa istanza `OcrEngine`. Questo riduce l'overhead di caricamento ripetuto delle librerie native.  
- **Error Handling:** Cattura sempre `IOException` e `OcrException` per gestire in modo elegante file corrotti.  
- **Memory Management:** Dopo l'elaborazione, chiama `engine.dispose();` per liberare la memoria GPU nativa, soprattutto quando si elaborano migliaia di immagini.  

```java
        // Clean up resources
        engine.dispose();
```

- **Logging:** Memorizza `result.getConfidence()` insieme al testo estratto. Le voci con bassa confidenza possono essere inviate a una coda di revisione manuale.

## Esempio completo funzionante

Di seguito trovi il programma completo e autonomo che puoi copiare‑incollare nel tuo IDE. Sostituisci semplicemente `YOUR_DIRECTORY` con il percorso della tua cartella immagini.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // Load a JPG image – this is how you extract text from jpg
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Enable GPU acceleration (requires CUDA 11+ and a compatible driver)
        engine.getProcessingSettings().setUseGpu(true);

        // Optional: Select a specific GPU device (0 = first GPU)
        engine.getProcessingSettings().setGpuDeviceId(0);

        // Run the OCR process
        OcrResult result = engine.recognize();

        // Show the recognized text
        System.out.println("Recognized text:");
        System.out.println(result.getText());

        // Show confidence for quality checks
        System.out.println("Overall confidence: " + result.getConfidence());

        // Release native resources
        engine.dispose();
    }
}
```

> **Result verification:** Confronta il testo stampato con l'immagine originale. Se la confidenza è bassa, considera i suggerimenti nella sezione “Varianti comuni e casi limite”.

## Conclusione

Abbiamo appena coperto tutto ciò che ti serve per **recognize text from image** usando Aspose OCR in Java, dal caricamento del file all'abilitazione dell'accelerazione GPU e infine all'estrazione del testo. Seguendo questi passaggi puoi affidabilmente **extract text from jpg** files, controllare quale GPU esegue il carico di lavoro con **set GPU device ID**, e persino adattare il flusso ad altri formati di immagine.

Pronto per la prossima sfida? Prova a concatenare questa pipeline OCR con un inserimento in database, o a fornire i risultati a un modello di elaborazione del linguaggio naturale per la categorizzazione automatica. Le possibilità sono infinite, e il modello di base—**load image for OCR → enable GPU → recognize → extract**—rimane lo stesso.

Se incontri difficoltà, ricontrolla la versione del driver CUDA, assicurati che il JAR di Aspose OCR corrisponda al tuo JDK, e ricorda di liberare il motore dopo ogni batch. Buon coding, e che il tuo OCR sia sempre preciso!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}