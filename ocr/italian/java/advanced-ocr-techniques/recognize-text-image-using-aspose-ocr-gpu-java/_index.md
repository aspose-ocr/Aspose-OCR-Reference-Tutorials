---
category: general
date: 2026-02-17
description: Riconosci rapidamente il testo nelle immagini con il supporto GPU di
  Aspose OCR in Java. Scopri come estrarre il testo dall'immagine e impostare l'ID
  del dispositivo GPU per prestazioni ottimali.
draft: false
keywords:
- recognize text image
- extract text from image
- set gpu device id
- Aspose OCR Java
- GPU acceleration OCR
language: it
og_description: Riconosci rapidamente il testo nelle immagini con il supporto GPU
  di Aspose OCR in Java. Questa guida mostra come estrarre il testo dall'immagine
  e impostare l'ID del dispositivo GPU.
og_title: Riconoscere testo da immagine usando Aspose OCR GPU – Java
tags:
- Java
- OCR
- Aspose
- GPU
title: Riconoscere il testo da un'immagine usando Aspose OCR GPU – Java
url: /it/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Riconoscere immagini di testo usando Aspose OCR GPU – Java

Hai mai avuto bisogno di **recognize text image** in un'applicazione Java ma la CPU si soffocava con file di grandi dimensioni? Non sei l'unico—molti sviluppatori incontrano lo stesso ostacolo quando elaborano scansioni ad alta risoluzione. La buona notizia? Aspose OCR ti permette di **extract text from image** sulla GPU, riducendo drasticamente i tempi di elaborazione.  

In questo tutorial ti guideremo passo passo attraverso un esempio completo, pronto‑all'uso, che mostra esattamente come configurare la licenza, abilitare l'accelerazione GPU e **set gpu device id** quando hai più schede grafiche. Alla fine avrai un programma autonomo che stampa il testo riconosciuto sulla console—senza passaggi aggiuntivi.

## Cosa ti servirà

- **Java 17** o versioni più recenti (l'API è compatibile con Java 8+, ma l'ultima LTS offre migliori prestazioni).  
- Libreria **Aspose OCR for Java** (scarica il JAR dal sito web di Aspose).  
- Un valido **Aspose OCR license file** (`Aspose.OCR.lic`). La versione di prova gratuita funziona, ma le funzionalità GPU sono disponibili solo nella versione con licenza.  
- Un file immagine (`sample-image.png`) che contiene testo chiaro e leggibile da macchina.  
- Un ambiente abilitato alla GPU (una scheda compatibile NVIDIA CUDA funziona al meglio).  

Se qualcuno di questi ti è sconosciuto, non preoccuparti—ogni punto verrà spiegato man mano.

## Passo 1: Aggiungere Aspose OCR al tuo progetto

Per prima cosa, includi il JAR di Aspose OCR nel tuo classpath. Se usi Maven, aggiungi la seguente dipendenza a `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Per Gradle, è:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Se preferisci il metodo manuale, copia il JAR nella cartella `libs/` e aggiungilo al percorso dei moduli dell'IDE.

> **Pro tip:** Mantieni il numero di versione sincronizzato con le note di rilascio della libreria; le versioni più recenti spesso introducono ottimizzazioni delle prestazioni per l'elaborazione GPU.

## Passo 2: Caricare la licenza Aspose OCR (necessario per l'uso della GPU)

Senza licenza la chiamata `setEnableGpu(true)` tornerà silenziosamente alla modalità CPU. Carica la licenza subito all'inizio di `main`:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

Sostituisci `YOUR_DIRECTORY` con il percorso assoluto o relativo dove hai salvato il file `.lic`. Se il percorso è errato, Aspose genererà una `FileNotFoundException`, quindi verifica attentamente l'ortografia.

## Passo 3: Creare il motore OCR e abilitare l'accelerazione GPU

Ora istanziamo `OcrEngine` e gli diciamo di usare la GPU. Il metodo `setGpuDeviceId` ti consente di scegliere una scheda specifica quando ne è presente più di una.

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

Perché preoccuparsi dell'ID del dispositivo? In un server con più GPU potresti riservare una scheda per il pre‑processing delle immagini e un'altra per l'OCR. Impostare l'ID garantisce che l'hardware corretto esegua il lavoro pesante.

## Passo 4: Preparare l'immagine di input

Aspose OCR funziona con diversi formati (PNG, JPG, BMP, TIFF). Avvolgi il tuo file in un oggetto `OcrInput`:

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

Se devi elaborare uno stream (ad esempio, un file caricato), usa `ocrInput.add(InputStream)` al suo posto.

## Passo 5: Eseguire il processo di riconoscimento e recuperare il risultato

Il metodo `recognize` restituisce un `OcrResult` che contiene il testo semplice, i punteggi di confidenza e persino le informazioni di layout se ti servono.

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

La console mostrerà qualcosa del genere:

```
Recognized text:
Hello, world!
This is a sample image.
```

Se l'immagine è sfocata o la lingua non è supportata, il risultato potrebbe essere vuoto. In tal caso, controlla il valore `ocrResult.getConfidence()` (0‑100) per decidere se riprovare con un pre‑processing.

## Esempio completo, eseguibile

Unendo tutti i pezzi ottieni una singola classe Java che puoi copiare‑incollare nel tuo IDE:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license – required for GPU usage
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // 2️⃣ Create OCR engine and turn on GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getDevice().setEnableGpu(true);      // enable GPU acceleration
        ocrEngine.getDevice().setGpuDeviceId(0);       // optional: select GPU index

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/sample-image.png");

        // 4️⃣ Perform recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + ocrResult.getText());
    }
}
```

> **Expected output:** La console stampa il testo esatto che appare in `sample-image.png`. Se la GPU è attiva, noterai che il tempo di elaborazione scende da diversi secondi (CPU) a meno di un secondo per scansioni tipiche a 300 dpi.

## Domande frequenti e casi particolari

### Funziona su un server headless?

Sì. Il driver GPU deve essere installato, ma non è necessario alcun display. Basta assicurarsi che il toolkit `CUDA` (o l'equivalente per la tua GPU) sia nel `PATH` di sistema.

### E se ho più di una GPU e voglio usare GPU 1?

Change the device ID:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

### Come estrarre testo da immagine in una lingua diversa?

Set the language before calling `recognize`:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose supporta oltre 30 lingue; consulta la documentazione API per l'elenco completo.

### E se l'immagine contiene più pagine (ad esempio, un PDF convertito in immagini)?

Create a separate `OcrInput` entry for each page, or loop over the files:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

Il motore concatenarà i risultati in ordine.

### Come gestire risultati a bassa confidenza?

Check the confidence score:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

I tipici passaggi di pre‑processing includono binarizzazione, riduzione del rumore o ridimensionamento a 300 dpi.

## Suggerimenti per le prestazioni

- **Batch processing:** Aggiungere molte immagini a un unico `OcrInput` riduce l'overhead di inizializzare ripetutamente il contesto GPU.  
- **Warm‑up:** Esegui un riconoscimento fittizio una volta dopo l'avvio della JVM; la prima chiamata comporta latenza di inizializzazione del driver.  
- **Memory management:** Rilascia gli oggetti `OcrInput` di grandi dimensioni (`ocrInput.clear()`) dopo aver terminato per liberare memoria GPU.  

## Conclusione

Ora sai come **recognize text image** in modo efficiente con il motore GPU di Aspose OCR in Java, come **extract text from image** in qualsiasi lingua supportata, e come **set gpu device id** quando lavori con più schede grafiche. Il codice completo e eseguibile sopra dovrebbe funzionare subito—basta sostituire i percorsi della licenza e dell'immagine.

Pronto per il passo successivo? Prova a elaborare una cartella di PDF scansionati, sperimenta con diverse opzioni `setLanguage`, o combina l'OCR con un modello di machine‑learning per il post‑processing. Le possibilità sono infinite, e i guadagni di prestazioni grazie all'accelerazione GPU rendono fattibili anche progetti su larga scala.

Buon coding, e sentiti libero di lasciare un commento se incontri qualche problema!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}