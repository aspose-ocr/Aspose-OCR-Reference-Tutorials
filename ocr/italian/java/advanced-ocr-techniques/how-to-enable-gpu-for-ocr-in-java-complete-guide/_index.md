---
category: general
date: 2026-10-08
description: Come abilitare la GPU per una rapida elaborazione OCR. Impara a caricare
  immagini ad alta risoluzione, riconoscere il testo nell'immagine e estrarre il testo
  usando Aspose OCR.
draft: false
keywords:
- how to enable gpu
- load high resolution image
- recognize text image
- extract text OCR
- GPU accelerated OCR
lastmod: 2026-10-08
og_description: Come abilitare la GPU per una rapida elaborazione OCR. Questa guida
  mostra come caricare immagini ad alta risoluzione, riconoscere il testo nell'immagine
  e estrarre il testo con Aspose OCR.
og_image_alt: Diagram showing GPU-accelerated OCR workflow in Java
og_title: Come abilitare la GPU per l'OCR in Java – guida completa
schemas:
- author: Aspose
  dateModified: '2026-10-08'
  description: How to enable GPU for fast OCR processing. Learn to load high resolution
    image, recognize text image, and extract text using Aspose OCR.
  headline: How to enable GPU for OCR in Java – complete guide
  type: TechArticle
- questions:
  - answer: Java 17 or newer (older JDKs work with minor tweaks).
    question: What is the minimum Java version?
  - answer: Any NVIDIA GPU that supports CUDA 12+ will work.
    question: Do I need a specific GPU?
  - answer: Aspose OCR for Java 23.10 or later.
    question: Which Aspose version is required?
  - answer: Yes, the GPU driver works without a display.
    question: Can I run this on a headless server?
  - answer: Yes, a valid Aspose OCR license is required for non‑trial use.
    question: Is a license mandatory for production?
  type: FAQPage
tags:
- OCR
- Java
- GPU
- Aspose
title: Come abilitare la GPU per l'OCR in Java – guida completa
url: /it/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come abilitare la GPU per OCR in Java – guida completa

Se stai cercando di **come abilitare la GPU** per il tuo flusso di lavoro OCR e ridurre drasticamente i tempi di elaborazione, sei nel posto giusto. L'accelerazione GPU sposta il lavoro pesante di estrazione del testo dalla CPU alla scheda grafica, il che è particolarmente utile quando lavori con scansioni ad alta risoluzione o elabori in batch migliaia di pagine.

In questo tutorial vedremo come caricare un **immagine ad alta risoluzione**, configurare Aspose OCR per l'esecuzione sulla GPU e infine **riconoscere l'immagine di testo** e **estrarre il testo** con poche righe di Java. Alla fine avrai un programma pronto all'uso che dimostra **l'abilitazione dell'elaborazione GPU** end‑to‑end.

## Risposte rapide
- **Qual è la versione minima di Java?** Java 17 o successiva (JDK più vecchi funzionano con piccole modifiche).  
- **È necessaria una GPU specifica?** Qualsiasi GPU NVIDIA che supporta CUDA 12+ funzionerà.  
- **Quale versione di Aspose è richiesta?** Aspose OCR per Java 23.10 o successiva.  
- **Posso eseguirlo su un server headless?** Sì, il driver GPU funziona senza display.  
- **È obbligatoria una licenza per la produzione?** Sì, è necessaria una licenza valida di Aspose OCR per l'uso non‑trial.

## Cosa ti servirà

Avrai bisogno dei seguenti elementi prima di iniziare:

- Java 17 o successiva (il codice utilizza il sistema di moduli ma funziona su JDK più vecchi con piccole modifiche)  
- Aspose OCR per Java 23.10 (o l'ultima versione) – puoi prendere le coordinate Maven dal sito Aspose  
- Una GPU NVIDIA con driver CUDA 12+ installati (altrimenti la libreria rifiuterà di avviarsi)  
- Un'immagine di esempio ad alta risoluzione (PNG o JPEG) da cui desideri leggere il testo  

È tutto. Nessun servizio esterno, nessun credito cloud, solo la tua macchina e lo stack di driver corretto.

![Flusso di lavoro OCR GPU – come abilitare l'elaborazione GPU](gpu-ocr-workflow.png)

[Flusso di lavoro OCR GPU – come abilitare l'elaborazione GPU](gpu-ocr-workflow.png)

*Testo alternativo dell'immagine: diagramma che illustra come abilitare la GPU per l'elaborazione OCR in Java.*

## Cos'è l'OCR accelerato da GPU?

L'OCR accelerato da GPU sposta l'inferenza della rete neurale dalla CPU alla scheda grafica, offrendo fino a 10× più velocità di elaborazione per immagini superiori a 2 MP. Aspose OCR sfrutta kernel CUDA pre‑compilati per Windows, Linux e macOS, consentendoti di mantenere la stessa API Java ottenendo al contempo il boost di velocità.

## Perché utilizzare l'accelerazione GPU per l'OCR?

Aspose OCR supporta **oltre 50 formati di input e output** e può elaborare documenti di centinaia di pagine senza caricare l'intero file in memoria. Quando la GPU è abilitata, una scansione di 3000 × 2000 pixel che richiede 4 secondi sulla CPU scende a meno di 0,5 secondi, riducendo il tempo totale del batch di oltre l'80 %.

## Implementazione passo‑passo

Di seguito suddividiamo la soluzione in blocchi logici. Ogni sezione contiene uno snippet di codice conciso, una spiegazione del **perché** il passaggio è importante e alcuni consigli pratici che probabilmente apprezzerai in seguito.

### Come abilitare la GPU per OCR – passo 1: installare le dipendenze e verificare CUDA

Per il passo 1, devi confermare che le librerie runtime di CUDA siano visibili al sistema operativo e che il driver GPU sia correttamente installato. Verifica l'installazione eseguendo il comando di versione per il compilatore o l'Interfaccia di Gestione del Sistema NVIDIA, che dovrebbe mostrare i dettagli del driver e della GPU.

On Windows you can verify with:

```bat
nvcc --version
```

On Linux:

```bash
nvidia-smi
```

**Suggerimento:** Mantieni il driver GPU aggiornato ma evita le versioni “latest‑beta”; a volte rompono la compatibilità binaria con le librerie native di Aspose.

### Come abilitare la GPU per OCR – passo 2: aggiungere la dipendenza Maven di Aspose OCR

Nel passo 2 aggiungi Aspose OCR al tuo sistema di build affinché il compilatore Java possa trovare il motore OCR e i binari GPU nativi. Includere le coordinate Maven garantisce che sia la libreria core sia i file nativi specifici per la piattaforma vengano scaricati automaticamente durante l'aggiornamento del progetto.

Aggiungi quanto segue al tuo `pom.xml`. Questo include il motore OCR core e i binari GPU nativi per Windows, Linux e macOS.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

If you prefer Gradle, the equivalent is:

```gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

Dopo aver aggiornato il progetto, le classi `OcrEngine`, `OcrDeviceType` e `ImageStream` diventano disponibili.

### Come abilitare la GPU per OCR – passo 3: creare il motore OCR e abilitare la GPU

La classe `OcrEngine` è l'oggetto centrale di Aspose OCR che gestisce il caricamento delle immagini, il preprocessing e l'inferenza. `OcrDeviceType` è un'enumerazione che indica al motore se eseguire su CPU o GPU. `ImageStream` rappresenta i dati dell'immagine in memoria che il motore consuma. Questa configurazione consente al motore di delegare l'inferenza della rete neurale alla GPU, riducendo drasticamente la latenza.

Ora diciamo effettivamente ad Aspose di eseguire sulla GPU. `OcrEngine` espone un oggetto `Device` dove possiamo cambiare il tipo di dispositivo di elaborazione.

```java
import com.aspose.ocr.*;

public class GpuOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 3.1: Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3.2: Enable GPU processing (requires a CUDA‑enabled driver & runtime)
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Optional: limit the number of GPU streams for better resource control
        ocrEngine.getDevice().setStreamCount(2);

        // Step 3.3: Load the high‑resolution image to be recognized
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample-highres.png"));

        // Step 3.4: Perform OCR and retrieve the recognized text
        String recognizedText = ocrEngine.recognize().getText();

        // Step 3.5: Display the extracted text
        System.out.println("=== OCR RESULT ===");
        System.out.println(recognizedText);
    }
}
```

**Perché è importante:** Impostare `OcrDeviceType.GPU` sostituisce il motore di inferenza sottostante da un'implementazione solo CPU a una accelerata da CUDA. La chiamata opzionale `setStreamCount` ti permette di controllare il parallelismo; due stream sono un valore predefinito sicuro sulla maggior parte delle schede consumer.

### Come abilitare la GPU per OCR – passo 4: caricare un'immagine ad alta risoluzione

`ImageStream` è un wrapper leggero che legge i file immagine in un buffer di byte compatibile con il motore OCR. Caricare una sorgente ad alta risoluzione fornisce al modello più dettagli visivi, il che si traduce in una maggiore precisione per caratteri piccoli o script complessi. Il wrapper normalizza anche il formato dei dati dell'immagine richiesto dallo strato nativo, garantendo un'elaborazione fluida.

Se hai bisogno di **caricare un'immagine ad alta risoluzione** da un URL o da un array di byte in memoria, puoi usare:

```java
byte[] imageBytes = java.nio.file.Files.readAllBytes(Paths.get("remote-image.png"));
ocrEngine.setImage(ImageStream.fromBytes(imageBytes));
```

**Caso limite:** Alcune GPU hanno una dimensione massima della texture (spesso 16384 × 16384). Se la tua immagine supera tale limite, considera di ridimensionare a una dimensione che mantenga comunque la leggibilità (ad es., 3000 × 2000). Il motore OCR ridimensionerà automaticamente se chiami `ocrEngine.setResizeFactor(0.5)` prima del caricamento.

### Come abilitare la GPU per OCR – passo 5: riconoscere l'immagine di testo ed estrarre il testo

`OcrResult` è il contenitore restituito da `ocrEngine.recognize()`. Contiene il testo semplice, i punteggi di confidenza, le bounding box e un payload JSON opzionale. Dopo il riconoscimento puoi chiamare `getText()` per recuperare la stringa estratta, o ispezionare le informazioni di layout dettagliate per ulteriori elaborazioni come la validazione o il post‑processing.

```java
OcrResult result = ocrEngine.recognize();
String plainText = result.getText();
System.out.println("Detected text length: " + plainText.length());

// Optional: iterate over each line with its confidence
result.getPages().forEach(page -> {
    page.getLines().forEach(line -> {
        System.out.printf("Line: \"%s\" (Confidence: %.2f%%)%n",
                line.getText(), line.getConfidence() * 100);
    });
});
```

**Perché potresti volere questo:** Il passaggio `recognize text image` è dove la GPU brilla—grandi immagini che richiederebbero secondi sulla CPU vengono elaborate in una frazione di tempo. I punteggi di confidenza ti permettono di filtrare i risultati di bassa qualità, un trucco utile quando in seguito **come estrarre il testo** per analisi a valle.

### Consigli professionali e problemi comuni

| Situazione | Cosa fare |
|-----------|------------|
| **Errori Out‑of‑memory** sulla GPU | Riduci `setStreamCount` a 1, oppure ridimensiona l'immagine prima di passarla al motore. |
| **Caratteri non riconosciuti** nonostante l'alta risoluzione | Assicurati che il modello linguistico (`ocrEngine.setLanguage(OcrLanguage.ENGLISH)`) corrisponda alla lingua del testo. |
| **Mancata corrispondenza della versione CUDA** | Allinea la versione del toolkit CUDA a quella fornita con Aspose OCR (controlla le note di rilascio). |
| **GPU multiple** | Usa `ocrEngine.getDevice().setDeviceId(1)` per selezionare la seconda GPU se la prima è occupata. |
| **Esecuzione su server headless** | Nessun passaggio aggiuntivo necessario; il driver GPU funziona senza display. |

## Come estrarre il testo – verificare l'output

Quando esegui la classe sopra, dovresti vedere qualcosa del genere:

```
=== OCR RESULT ===
Welcome to the Aspose OCR demo!
Your GPU is now accelerating text extraction.
```

Se l'output appare confuso, ricontrolla che l'immagine sia davvero ad alta risoluzione e che il driver GPU sia correttamente installato. Puoi anche abilitare il logging dettagliato:

```java
ocrEngine.setLogLevel(OcrLogLevel.DEBUG);
```

I log mostreranno se i kernel CUDA nativi sono stati caricati correttamente.

## Prossimi passi e argomenti correlati

- **Elaborazione batch:** Avvolgi il `OcrEngine` in un ciclo e fornisci un elenco di percorsi immagine. Ricorda di riutilizzare la stessa istanza del motore per evitare il sovraccarico di inizializzazione GPU ripetuta.  
- **Rilevamento della lingua:** Aspose OCR supporta oltre 30 lingue. Cambia con `ocrEngine.setLanguage(OcrLanguage.FRENCH)`.  
- **Post‑processing:** Usa espressioni regolari per pulire la stringa estratta, o inviala a una pipeline NLP a valle.  
- **Dispositivi alternativi:** Se non disponi di una GPU compatibile con CUDA, puoi tornare a `OcrDeviceType.CPU`. Lo stesso codice funziona; basta cambiare il tipo di dispositivo.  
- **Benchmark delle prestazioni:** Misura la differenza di tempo con `System.nanoTime()` prima e dopo `recognize()` per quantificare il guadagno da **abilitare l'elaborazione GPU**.

---

**Last updated:** 2026-10-08  
**Tested with:** Aspose OCR for Java 23.10  
**Author:** Aspose

## Tutorial correlati

- [Riconoscere l'immagine di testo usando Aspose Ocr GPU Java](/ocr/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/)
- [Estrarre testo da immagine con Aspose Ocr Java Guida rapida](/ocr/java/ocr-basics/extract-text-from-image-with-aspose-ocr-java-quick-guide/)
- [OCR di immagini batch in Java: estrarre testo da file PNG velocemente](/ocr/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}