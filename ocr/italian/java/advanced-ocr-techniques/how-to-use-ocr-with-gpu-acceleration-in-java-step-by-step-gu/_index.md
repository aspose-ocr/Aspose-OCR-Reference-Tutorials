---
category: general
date: 2026-02-09
description: Come utilizzare rapidamente l'OCR con Aspose OCR, riconoscere il testo
  da un'immagine ed estrarre il testo da PNG impostando la modalità e il limite di
  memoria GPU.
draft: false
keywords:
- how to use ocr
- recognize text from image
- extract text from png
- how to set mode
- set gpu memory limit
language: it
og_description: Come utilizzare l'OCR in modo efficiente – impara a riconoscere il
  testo da un'immagine, estrarre il testo da PNG, impostare la modalità e controllare
  il limite di memoria GPU in Java.
og_title: Come utilizzare l'OCR con accelerazione GPU in Java
tags:
- OCR
- Java
- GPU
- Aspose
title: Come utilizzare l'OCR con accelerazione GPU in Java – Guida passo passo
url: /it/java/advanced-ocr-techniques/how-to-use-ocr-with-gpu-acceleration-in-java-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come utilizzare OCR con accelerazione GPU in Java – Tutorial di programmazione completo

Ti sei mai chiesto **how to use OCR** per estrarre testo da un'immagine senza scrivere un milione di righe di codice? Non sei solo. In molti progetti—scansione di fatture, elaborazione di ricevute o semplicemente digitalizzazione di documenti vecchi—gli sviluppatori hanno bisogno di un modo affidabile per **recognize text from image** file, soprattutto PNG che spesso contengono grafiche pulite e ad alta risoluzione.  

La buona notizia? Aspose OCR rende tutto questo un gioco da ragazzi e, con qualche piccola modifica alla configurazione, puoi persino delegare il lavoro pesante alla tua GPU. In questo tutorial percorreremo l’intero processo: dal caricamento di un PNG, alla **setting mode** per l’elaborazione GPU, al **setting GPU memory limit**, fino alla stampa del testo estratto. Alla fine avrai un programma Java eseguibile che fa esattamente quello di cui hai bisogno.

## What You’ll Learn

- Come installare e importare Aspose OCR per Java.
- Come **recognize text from image** file usando la libreria.
- Come **extract text from PNG** in modo efficiente.
- Come **set mode** su GPU e controllare l’utilizzo di memoria con **set GPU memory limit**.
- Problemi comuni e consigli per l’uso in scenari reali.

### Prerequisites

- Java 8 o superiore (il codice compila anche con JDK 11).
- Una GPU NVIDIA con driver compatibile CUDA se desideri l’accelerazione GPU.
- Aspose OCR per Java JAR (scaricabile dal sito Aspose o aggiunto via Maven/Gradle).
- Un’immagine PNG di esempio (ad es. `sample1.png`) posizionata in una cartella a cui puoi fare riferimento.

---

## How to Use OCR – Enable GPU Mode

La prima cosa da fare è dire ad Aspose OCR di eseguire il processo sulla GPU invece che sulla CPU. È qui che entra in gioco la keyword **how to set mode**.

```java
// Step 1: Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Step 2: Grab the configuration object
OcrEngineConfiguration config = ocrEngine.getConfiguration();

// Step 3: Switch processing mode to GPU
config.setProcessingMode(ProcessingMode.GPU);   // requires a CUDA‑compatible driver

// (Optional) Step 4: Limit GPU memory usage to 1024 MB
config.setGpuMemoryLimit(1024);                 // set gpu memory limit (MB)
```

**Perché è importante:**  
L’elaborazione su GPU può essere drasticamente più veloce per lotti grandi o immagini ad alta risoluzione, ma consuma anche memoria video. Chiamando `setGpuMemoryLimit`, eviti che la tua applicazione monopolizzi tutta la GPU, cosa cruciale quando lo stesso dispositivo esegue altri carichi di lavoro (ad es. un’interfaccia UI o un modello di machine‑learning).

---

## Recognize Text from Image Using Aspose OCR

Ora che il motore è configurato, dobbiamo indicargli il file da leggere. Questo è il cuore di **recognize text from image**.

```java
// Step 5: Define the image to be processed
ImageRecognitionResult imageInfo = new ImageRecognitionResult();
imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

// Step 6: Run the OCR operation
RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);
```

**Cosa succede dietro le quinte?**  
Aspose OCR carica il PNG, lo pre‑processa (binarizzazione, correzione di inclinazione, ecc.), quindi esegue la rete neurale OCR sulla GPU. L’oggetto risultato contiene il testo grezzo più i punteggi di confidenza per ogni riga.

---

## Extract Text from PNG with GPU Memory Limit

Dopo il riconoscimento, estrarre la stringa semplice è banale, ma molti sviluppatori dimenticano di verificare l’output. Ecco come puoi **extract text from PNG** in modo sicuro e visualizzarlo.

```java
// Step 7: Output the recognized text
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Output previsto (esempio):**

```
Recognized text:
Invoice #12345
Date: 2026-02-09
Total: $1,250.00
Thank you for your business!
```

Se l’immagine contiene rumore o caratteri insoliti, potresti vedere caratteri illeggibili. In tal caso, considera di regolare le opzioni di pre‑processing (ad es. `config.setLanguage(Language.ENGLISH)` o `config.setAutoSkewCorrection(true)`).

---

## Full, Runnable Example

Di seguito il programma Java completo che mette insieme tutti i passaggi. Copialo in un file chiamato `GpuExample.java`, modifica il percorso dell’immagine e eseguilo con `javac`/`java` o dal tuo IDE.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.configuration.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Specify the image to be processed
        ImageRecognitionResult imageInfo = new ImageRecognitionResult();
        imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

        // Step 2: Create the OCR engine and enable GPU processing
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration config = ocrEngine.getConfiguration();

        // Step 3: Set processing mode to GPU (requires CUDA driver)
        config.setProcessingMode(ProcessingMode.GPU);

        // Step 4 (optional): Limit GPU memory usage to 1024 MB
        config.setGpuMemoryLimit(1024);

        // Step 5: Perform recognition
        RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);

        // Step 6: Print the extracted text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Esecuzione del programma**

```bash
javac -cp "path/to/aspose-ocr.jar" GpuExample.java
java -cp ".:path/to/aspose-ocr.jar" GpuExample
```

Assicurati che il JAR sia nel classpath; altrimenti otterrai `ClassNotFoundException`.

---

## Pro Tips & Common Pitfalls

- **Versione del driver GPU:** Il flag `ProcessingMode.GPU` genererà un’eccezione se il driver CUDA è mancante o incompatibile. Verifica con `nvidia-smi`.
- **Gestione della memoria:** Se elabori molte immagini contemporaneamente, aumenta il valore di `setGpuMemoryLimit` o esegui i job in sequenza per evitare errori di out‑of‑memory.
- **Formato immagine:** Sebbene PNG funzioni benissimo, i JPEG ad alta compressione possono causare errori di riconoscimento. Considera di convertire in PNG lossless prima dell’OCR.
- **Supporto linguistico:** Per impostazione predefinita Aspose OCR assume l’inglese. Per altre lingue, chiama `config.setLanguage(Language.SPANISH)` (o l’enum appropriato) prima di `recognize`.
- **Test delle prestazioni:** Esegui un benchmark rapido (`System.nanoTime()`) con e senza GPU per verificare che il guadagno di velocità giustifichi la complessità aggiuntiva.

---

## Frequently Asked Questions

**Funziona su macOS o Linux?**  
Sì—Aspose OCR è cross‑platform. Basta assicurarsi di avere una GPU compatibile CUDA e il driver corretto installato per il proprio OS.

**E se non ho una GPU?**  
Puoi semplicemente omettere la riga `setProcessingMode(ProcessingMode.GPU)`; il motore tornerà automaticamente alla modalità CPU.

**Posso elaborare PDF direttamente?**  
Aspose OCR è focalizzato su immagini raster. Per i PDF, estrai prima ogni pagina come immagine (ad es. usando Aspose PDF) e poi passa i PNG al flusso OCR.

---

## Conclusion

In sintesi, **how to use OCR** con Aspose in Java si riduce a tre passaggi chiari: configurare il motore (inclusi **how to set mode** e **set GPU memory limit**), puntarlo al tuo PNG e leggere la stringa risultante. Lo snippet sopra è una soluzione completamente funzionante, end‑to‑end, che puoi inserire in qualsiasi progetto Java.

Ora che hai padroneggiato **recognize text from image** e **extract text from PNG**, puoi ampliare il flusso di lavoro: elaborare in batch cartelle, salvare i risultati in un database o persino alimentare pipeline NLP successive. Il cielo è il limite—basta tenere d’occhio la memoria GPU e la compatibilità dei driver.

Hai altre domande su OCR, accelerazione GPU o le funzionalità di Aspose? Sentiti libero di lasciare un commento o di esplorare la documentazione ufficiale di Aspose OCR per opzioni di personalizzazione più approfondite. Buona programmazione! 🚀

![how to use ocr diagram](https://example.com/images/ocr-gpu-diagram.png "diagramma di come utilizzare ocr")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}