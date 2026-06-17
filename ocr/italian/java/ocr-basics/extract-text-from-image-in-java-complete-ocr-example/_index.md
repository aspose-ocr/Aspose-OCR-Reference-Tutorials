---
category: general
date: 2026-02-19
description: Estrai il testo da un'immagine usando Java OCR. Scopri un esempio di
  OCR in Java che carica un'immagine per l'OCR ed estrae il testo da file di fatture
  in pochi passaggi.
draft: false
keywords:
- extract text from image
- java ocr example
- load image for ocr
- extract text from invoice
language: it
og_description: Estrai il testo da un'immagine usando Java OCR. Questa guida mostra
  come caricare l'immagine per l'OCR ed estrarre il testo dalle fatture con un semplice
  esempio di OCR in Java.
og_title: Estrai testo da un'immagine in Java – Esempio completo di OCR
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Estrai testo da immagine in Java – Esempio completo di OCR
url: /it/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da immagine in Java – Esempio OCR completo

Hai mai avuto bisogno di **estrarre testo da un'immagine** ma non eri sicuro quale libreria scegliere? Non sei solo—molti sviluppatori si trovano di fronte a questo ostacolo quando automatizzano l'elaborazione delle fatture o creano archivi ricercabili. La buona notizia? Con poche righe di Java puoi caricare un'immagine per l'OCR, definire una regione di interesse e ottenere il testo esatto di cui hai bisogno.  

In questo tutorial percorreremo un **java ocr example** che mostra esattamente come **load image for OCR**, impostare una ROI e **extract text from invoice** file usando Aspose.OCR. Alla fine avrai un programma eseguibile da inserire in qualsiasi progetto Java.

## Cosa imparerai

- Come creare un'istanza di `OcrEngine` e perché è importante.
- Il modo corretto per **load image for OCR** con `ImageStream` di Aspose.
- Impostare una **region of interest (ROI)** così elabori solo la parte dell'immagine che contiene l'importo della fattura.
- Estrarre il testo riconosciuto e stamparlo sulla console.
- Problemi comuni (ad esempio coordinate del rettangolo errate) e soluzioni rapide.

**Prerequisiti**

- Java 8 o versioni successive installate.
- Maven o Gradle per scaricare la libreria Aspose.OCR (`com.aspose:aspose-ocr`).
- Un'immagine di fattura di esempio (`invoice.png`) posizionata in una directory nota.

Hai tutto questo? Ottimo—tuffiamoci.

![Estrai testo da immagine usando Java OCR](/images/extract-text-from-image-java.png "estrai testo da immagine esempio")

## Estrai testo da immagine – Esempio OCR Java passo‑per‑passo

Di seguito trovi il codice sorgente completo. Sentiti libero di copiarlo e incollarlo in `RoiOcrExample.java` ed eseguirlo direttamente.

```java
import com.aspose.ocr.*;

public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance.
        // The engine holds all configuration and performs the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image.
        // You can point to any PNG, JPG, or TIFF file. Here we use a sample invoice.
        String imagePath = "YOUR_DIRECTORY/invoice.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Define the region of interest (ROI) you want to recognize.
        // x = 120, y = 340, width = 500, height = 120 – tweak these values for your own layout.
        Rectangle regionOfInterest = new Rectangle(120, 340, 500, 120);
        ocrEngine.setRegionOfInterest(regionOfInterest);

        // Step 4: Perform OCR on the specified ROI and retrieve the text.
        // recognize() returns an OcrResult object; getText() extracts the plain string.
        String extractedText = ocrEngine.recognize().getText();

        // Step 5: Output the recognized text.
        System.out.println("ROI text: " + extractedText);
    }
}
```

### Perché ogni passaggio è importante

1. **Creare il motore OCR** – senza un motore non c'è contesto per l'elaborazione delle immagini. L'oggetto ti permette anche di regolare i language pack in seguito se hai bisogno di supporto multilingua.  
2. **Caricare l'immagine** – `ImageStream.fromFile` astrae il formato del file, garantendo che il motore legga i byte correttamente. Se lo salti, otterrai un `NullPointerException`.  
3. **Impostare la ROI** – elaborare l'intera pagina può essere inefficiente. Restringendo il rettangolo all'area del totale della fattura, acceleri il riconoscimento e riduci il rumore.  
4. **Chiamare `recognize()`** – qui avviene la magia. Il metodo esegue l'algoritmo OCR sulla ROI e produce un oggetto risultato.  
5. **Stampare l'output** – nei progetti reali probabilmente memorizzeresti il testo in un database, ma `System.out.println` è perfetto per una demo rapida.

## Carica immagine per OCR

Se ti chiedi se il percorso debba essere assoluto o relativo, la risposta è che entrambi funzionano—basta assicurarsi che il processo Java possa leggere il file. Su Windows, le barre rovesciate devono essere escape (`C:\\images\\invoice.png`) oppure puoi usare le barre normali (`C:/images/invoice.png`).  

**Suggerimento professionale:** Se elabori molte fatture in un ciclo, riutilizza la stessa istanza di `OcrEngine`; essa memorizza nella cache le risorse interne e migliora il throughput.

## Definisci la Region of Interest (ROI)

Scegliere il rettangolo giusto può richiedere qualche tentativo. Un modo pratico per trovare le coordinate è aprire l'immagine in un editor grafico (come GIMP o Paint.NET) e posizionare il cursore sull'area—vedrai i valori X/Y nella barra di stato.  

Caso limite: alcune fatture hanno layout variabili. In tal caso potresti eseguire una rapida pre‑scansione sull'intera immagine, individuare parole chiave come “Total:” con una regex, quindi regolare dinamicamente la ROI.

## Esegui OCR e ottieni il testo

La chiamata `recognize()` è sincrona—il tuo thread resta bloccato finché il motore non termina. Per grandi lotti potresti voler avviare un pool di thread e processare le immagini in parallelo. Ricorda solo che ogni thread ha bisogno della propria istanza di `OcrEngine`; non sono thread‑safe.

## Esegui e verifica l'output

Compila ed esegui:

```bash
javac -cp "path/to/aspose-ocr.jar" RoiOcrExample.java
java -cp ".:path/to/aspose-ocr.jar" RoiOcrExample
```

Dovresti vedere qualcosa di simile:

```
ROI text: $1,254.00
```

Se l'output appare illeggibile, ricontrolla le coordinate della ROI e assicurati che la qualità dell'immagine sia alta (300 dpi o più è l'ideale).  

### Problemi comuni e come risolverli

| Sintomo | Probabile causa | Risoluzione |
|---------|----------------|-------------|
| Stringa vuota | ROI fuori dai limiti dell'immagine | Verifica i valori del rettangolo rispetto alle dimensioni dell'immagine |
| Parole errate | Bassa risoluzione | Usa una sorgente a più alta risoluzione o applica pre‑elaborazione dell'immagine (ad es., binarizzazione) |
| `java.lang.NoClassDefFoundError` | JAR Aspose mancante nel classpath | Aggiungi `aspose-ocr.jar` a `-cp` o usa la gestione delle dipendenze di Maven/Gradle |

## Conclusione

Ora sai come **extract text from image** in Java usando un conciso **java ocr example**. Caricando correttamente l'immagine, definendo una ROI mirata e chiamando `recognize()`, puoi affidabilmente **extract text from invoice** file e alimentare quei dati nei sistemi a valle.

Cosa fare dopo? Prova a sostituire la ROI per campi diversi (data, nome del fornitore), sperimenta con i language pack per fatture multilingua, o integra il passaggio OCR in un microservizio Spring Boot. Lo stesso schema funziona per ricevute, passaporti o qualsiasi documento in cui è necessaria un'estrazione precisa del testo.

Se hai domande su come scalare questa soluzione o gestire scansioni rumorose, lascia un commento qui sotto—buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}