---
category: general
date: 2026-06-16
description: Riconosci rapidamente le immagini di testo con Aspose OCR in Java. Scopri
  come impostare il dispositivo GPU, estrarre il testo da JPG e leggere l'immagine
  di testo utilizzando l'accelerazione GPU.
draft: false
keywords:
- recognize text image
- set gpu device
- extract text jpg
- how to recognize text
- read text picture
language: it
og_description: Riconosci il testo nelle immagini con Aspose OCR in Java. Questa guida
  mostra come impostare il dispositivo GPU, estrarre il testo da JPG e leggere l'immagine
  di testo in modo efficiente.
og_title: Riconoscere il testo in un'immagine in Java usando Aspose OCR + GPU
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text image quickly with Aspose OCR in Java. Learn how to
    set gpu device, extract text jpg, and read text picture using GPU acceleration.
  headline: recognize text image in Java using Aspose OCR + GPU
  type: TechArticle
tags:
- OCR
- Java
- Aspose
- GPU
title: Riconoscere il testo di un'immagine in Java usando Aspose OCR + GPU
url: /it/java/advanced-ocr-techniques/recognize-text-image-in-java-using-aspose-ocr-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere testo da immagine in Java con Aspose OCR + GPU

Ti sei mai chiesto come riconoscere il testo da un'immagine in un'applicazione Java senza bloccare la CPU? Non sei solo: gli sviluppatori cercano continuamente pipeline OCR più veloci e affidabili. In questo tutorial percorreremo una soluzione completa, accelerata dalla GPU, che ti permette di estrarre testo da una foto JPG in un lampo.

Inizieremo configurando Aspose OCR, poi abiliteremo l'accelerazione GPU e infine mostreremo come leggere i file immagine di testo, stampare i risultati e gestire gli eventuali intoppi. Alla fine saprai **come riconoscere il testo** su qualsiasi immagine, sia essa una fattura scannerizzata o uno screenshot casuale.

## Cosa ti serve

- **Java 17** (o qualsiasi JDK recente) – il codice funziona su tutti i runtime moderni.  
- **Aspose.OCR for Java** – disponibile su Maven Central.  
- Una **GPU** con supporto CUDA (opzionale ma altamente consigliata per le prestazioni).  
- Un'immagine JPEG di esempio (ad es. `sample.jpg`) che desideri elaborare.  

Nessun'altra libreria di terze parti è necessaria; tutto il resto è incluso in Aspose OCR.

## Passo 1: Aggiungi Aspose OCR al tuo progetto

Se usi Maven, inserisci la seguente dipendenza nel tuo `pom.xml`. Gli utenti Gradle possono copiare la riga `implementation` equivalente.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

> **Pro tip:** La versione di valutazione gratuita aggiunge una piccola filigrana. Per la produzione, procurati una licenza dal portale Aspose e chiama `License license = new License(); license.setLicense("Aspose.OCR.lic");` prima di qualsiasi operazione OCR.

## Passo 2: Carica l'immagine da elaborare

La prima cosa da fare quando vuoi **riconoscere testo da immagine** è fornire la foto al motore OCR. Aspose offre un pratico wrapper `ImageStream` che legge da un percorso file, da un `InputStream` o anche da un array di byte.

```java
import com.aspose.ocr.*;

public class GpuOcrExample {
    public static void main(String[] args) throws Exception {
        // Load the image – replace the path with your own picture
        OcrEngine engine = new OcrEngine();
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

Nota come manteniamo il codice minimale; la chiamata `setImage` accetta qualsiasi formato raster supportato da Aspose, inclusi JPEG, PNG e BMP.

## Passo 3: Abilita l'accelerazione GPU (set gpu device)

Ora arriva la parte che distingue questa guida: **set gpu device** per far girare il motore OCR sulla scheda grafica anziché sulla CPU. Questo può far risparmiare secondi sul tempo di elaborazione, soprattutto per immagini ad alta risoluzione.

```java
        // Enable GPU acceleration – this is where the magic happens
        engine.getRecognitionSettings().setUseGpu(true);

        // Optional: pick a specific GPU if you have more than one
        // engine.getRecognitionSettings().setGpuDeviceId(0);
```

Se hai più GPU, decommenta la riga `setGpuDeviceId` e sostituisci `0` con l'indice del dispositivo che preferisci. Aspose tornerà automaticamente alla CPU se non trova una GPU compatibile, così non dovrai preoccuparti di crash.

## Passo 4: Esegui OCR – come riconoscere testo

Con l'immagine caricata e la GPU attivata, possiamo finalmente **come riconoscere testo** sull'immagine. Il metodo `recognize()` esegue l'intera pipeline—pre‑elaborazione, segmentazione, classificazione dei caratteri e post‑elaborazione.

```java
        // Execute the OCR process
        OcrResult result = engine.recognize();
```

L'oggetto `OcrResult` restituito contiene la stringa grezza, i punteggi di confidenza e persino le bounding box se ti servono informazioni di layout in seguito.

## Passo 5: Output del testo riconosciuto – estrarre testo jpg / leggere immagine di testo

Facciamo **estrarre testo jpg** e **leggere immagine di testo** stampando semplicemente il risultato sulla console. In un'applicazione reale probabilmente scriveresti questo risultato in un database o in un file.

```java
        // Show the recognized text in the console
        System.out.println("Recognized text:");
        System.out.println(result.getText());
    }
}
```

Quando esegui il programma, dovresti vedere qualcosa di simile:

```
Recognized text:
Invoice #12345
Date: 2026-06-15
Total: $1,250.00
```

Se l'immagine contiene rumore, puoi regolare le impostazioni di pre‑elaborazione di Aspose (contrasto, binarizzazione, ecc.)—ma le impostazioni predefinite funzionano per la maggior parte dei file JPG puliti.

## Esempio completo funzionante

Mettendo tutto insieme, ecco la classe completa, pronta per l'esecuzione:

```java
import com.aspose.ocr.*;

public class GpuOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the image to be processed
        OcrEngine engine = new OcrEngine();
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Step 2: Enable GPU acceleration for faster recognition
        engine.getRecognitionSettings().setUseGpu(true);
        // Optional: specify a GPU device index if multiple GPUs are present
        // engine.getRecognitionSettings().setGpuDeviceId(0);

        // Step 3: Perform OCR on the loaded image
        OcrResult result = engine.recognize();

        // Step 4: Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(result.getText());
    }
}
```

> **Output previsto:** La console stampa esattamente il testo presente in `sample.jpg`. Se la foto è una fotografia di una ricevuta, vedrai ogni riga come una stringa separata, mantenendo le interruzioni di riga.

## Casi limite e problemi comuni

| Situazione | Cosa controllare | Correzione suggerita |
|------------|------------------|----------------------|
| **GPU multiple** | La GPU predefinita potrebbe non essere la più potente. | Usa `setGpuDeviceId` per puntare alla scheda ad alte prestazioni. |
| **Out‑of‑memory su immagini grandi** | JPG ad altissima risoluzione possono esaurire la memoria della GPU. | Ridimensiona prima l'immagine (`engine.getPreprocessingSettings().setResizeFactor(0.5)`). |
| **Bassa confidenza** | Alcuni caratteri possono essere letti in modo errato se la foto è sfocata. | Abilita `engine.getRecognitionSettings().setUseLanguageModel(true)` per correzioni contestuali. |
| **Formato immagine non supportato** | Aspose OCR supporta molti formati, ma non i dati RAW del sensore. | Converti il file in JPEG o PNG prima di passarlo al motore. |

Affrontare questi scenari garantisce che il tuo flusso di lavoro **riconoscere testo da immagine** rimanga robusto in diversi ambienti.

## Pro tip per un OCR più veloce e pulito

- **Elaborazione batch:** Riutilizza una singola istanza di `OcrEngine` per molte immagini; il contesto GPU rimane attivo, risparmiando il sovraccarico di inizializzazione.  
- **Sicurezza dei thread:** Ogni thread dovrebbe avere il proprio oggetto `OcrEngine`; la classe non è thread‑safe.  
- **Licenza precoce:** Carica la licenza Aspose all’avvio dell’applicazione per evitare la filigrana di valutazione.  
- **Logging:** Abilita `engine.getLogSettings().setEnableLogging(true)` se devi capire perché una determinata immagine fallisce.

## Conclusione

Abbiamo appena mostrato come **riconoscere testo da immagine** in Java usando Aspose OCR con accelerazione GPU. Seguendo i passaggi—aggiungere la libreria, caricare un JPEG, **set gpu device**, eseguire il motore OCR e infine **estrarre testo jpg** o **leggere immagine di testo**—puoi trasformare

## Cosa dovresti imparare dopo?


I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}