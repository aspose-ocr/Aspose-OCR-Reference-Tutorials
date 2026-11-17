---
category: general
date: 2026-11-17
description: Come abilitare la GPU in Java OCR per estrarre testo da un'immagine rapidamente.
  Scopri come configurare la GPU, estrarre testo e riconoscere testo Java con Aspose
  OCR.
draft: false
keywords:
- how to enable gpu
- high resolution ocr
- aspose ocr java
- extract text image java
- gpu acceleration ocr
lastmod: 2026-11-17
og_description: Come abilitare rapidamente la GPU per Java OCR. Questa guida mostra
  come configurare la GPU, estrarre testo da un'immagine e riconoscere testo Java
  usando Aspose OCR.
og_image_alt: 'Developer guide: Enable GPU for Java OCR using Aspose OCR library'
og_title: Come abilitare la GPU per Java OCR – guida passo‑passo
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: How to enable GPU in Java OCR to extract text from image fast. Learn
    how to configure GPU, extract text and recognize text java with Aspose OCR.
  headline: How to enable GPU for Java OCR – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: Yes, you can pass a PDF file directly to `setImage`; the library rasterizes
      each page before OCR.
    question: Does Aspose OCR support PDF input?
  - answer: Use `ocrEngine.getConfiguration().setCustomDictionary(List<String>)` to
      improve recognition of specialized vocabulary.
    question: How do I add custom dictionaries for domain‑specific terms?
  - answer: Currently only CUDA‑compatible NVIDIA GPUs on Windows and Linux are supported;
      macOS users fall back to CPU.
    question: Is GPU acceleration available on macOS?
  - answer: Absolutely—`OcrResult` includes a `getConfidence()` method for each `OcrWord`
      object.
    question: Can I retrieve the confidence score for each recognized word?
  - answer: A commercial Aspose OCR license is required for production deployments;
      a free evaluation license works for development and testing.
    question: What license is required for production use?
  type: FAQPage
tags:
- gpu ocr
- java ocr
- aspose ocr
- high resolution ocr
- java image processing
title: Come abilitare la GPU per Java OCR – guida passo‑passo
url: /it/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come abilitare la GPU per Java OCR – guida passo‑passo

Se stai cercando **come abilitare la GPU** durante l'estrazione di testo da immagini con Java, sei nel posto giusto. L'accelerazione GPU può ridurre il tempo di elaborazione OCR da diversi secondi a una frazione di secondo, soprattutto su scansioni ad alta risoluzione. In questa guida vedremo come installare Aspose OCR, configurare il dispositivo GPU e eseguire un programma completo di estrazione del testo che funziona in modo affidabile sia su macchine con GPU abilitata sia su macchine solo CPU.

## Risposte rapide
- **Qual è la versione minima di Java?** Java 17 o più recente.
- **Quale tipo di GPU è richiesto?** Qualsiasi GPU NVIDIA compatibile con CUDA (CUDA 11+).
- **È necessaria una licenza per eseguire il campione?** Una prova gratuita funziona per lo sviluppo; è necessaria una licenza commerciale per la produzione.
- **Quanto è più veloce l'OCR con GPU?** Fino a 5× più veloce su un'immagine da 4 MP rispetto alla CPU.
- **Posso tornare automaticamente alla CPU?** Sì—Aspose OCR ritorna alla CPU se non viene rilevata alcuna GPU.

## Cos'è l'accelerazione GPU per l'OCR?
L'accelerazione GPU per l'OCR significa eseguire i passaggi di inferenza della rete neurale su un processore grafico invece che sulla CPU, consentendo migliaia di operazioni in parallelo. Questo riduce drasticamente la latenza di inferenza, soprattutto per immagini ad alta risoluzione dove la CPU altrimenti diventerebbe un collo di bottiglia.

## Perché usare Aspose OCR per Java?
Aspose OCR supporta **oltre 50 formati di input** (inclusi PNG, JPEG, TIFF, PDF) e può elaborare documenti di centinaia di pagine senza caricare l'intero file in memoria. La sua API Java fornisce una singola classe `OcrEngine` che astrae le chiamate CUDA a basso livello, permettendoti di concentrarti sulla logica di business.

## Prerequisiti
- JDK Java 17+ installato.
- Maven 3.6+ o Gradle 7+ per la gestione delle dipendenze.
- Una GPU NVIDIA compatibile con CUDA con driver corrispondenti a CUDA 11.x o versioni successive.
- Accesso a Internet per scaricare la libreria Aspose OCR.

## Come abilitare la GPU per Java OCR?
Carica la libreria Aspose OCR, crea un `OcrEngine` e attiva il supporto GPU in poche righe di codice. Il motore rileva automaticamente i dispositivi disponibili; è anche possibile specificare un ID dispositivo per puntare a una GPU specifica in ambienti multi‑GPU.

## Come funziona OcrEngine?
`OcrEngine` è la classe centrale che orchestra la pre‑elaborazione delle immagini, l'inferenza della rete neurale e l'aggregazione dei risultati. Accetta immagini come percorsi di file, oggetti `java.io.File` o istanze `java.awt.image.BufferedImage`, offrendoti flessibilità su come fornire i dati al pipeline.

## Come configurare l'accelerazione GPU (come configurare GPU)
Qui è dove indichi ad Aspose OCR di usare la GPU e quale dispositivo scegliere.

Per abilitare l'accelerazione GPU crei un'istanza `GpuConfiguration`, imposti `setEnable(true)`, opzionalmente scegli un dispositivo con `setDeviceId(int)` e lo associ a `OcrEngine` tramite `setGpuConfiguration`. La configurazione ti consente anche di definire una strategia di fallback, ad esempio tornare alla CPU quando il dispositivo richiesto non è disponibile, garantendo la stabilità dell'applicazione.  
```java
        // Step 3: Enable GPU acceleration (optional: select a specific device)
        GpuConfiguration gpuConfig = new GpuConfiguration();
        gpuConfig.setEnabled(true);          // turn on GPU support
        gpuConfig.setDeviceId(0);            // choose GPU 0 (default first device)

        // Attach the GPU config to the OCR engine
        ocrEngine.setGpuConfiguration(gpuConfig);
```

Perché abilitare la GPU? Il pipeline OCR esegue diverse reti neurali convoluzionali. Eseguire queste reti su una GPU sfrutta migliaia di core in parallelo, riducendo il tempo di inferenza da 3–5 secondi sulla CPU a meno di 1 secondo su una moderna RTX 3080 per un'immagine da 4 MP. Se il dispositivo specificato non è presente, Aspose ritorna silenziosamente alla CPU, evitando crash.

### Gestione dei casi limite

Le applicazioni robuste devono verificare che un driver CUDA sia installato prima di tentare operazioni GPU.

```java
        // Verify that a GPU was actually engaged
        if (!gpuConfig.isEnabled() || !gpuConfig.isDeviceAvailable()) {
            System.out.println("GPU not detected – falling back to CPU. " +
                               "Performance will be slower.");
        }
```

## Passo 1 – Installa Aspose OCR e prepara la tua immagine (come abilitare GPU)

Prima, aggiungi la dipendenza Aspose OCR al tuo progetto. Se usi Maven, aggiungi:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- latest as of Jan 2026 -->
</dependency>
```

Gli utenti Gradle possono aggiungere:

```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

Posiziona un file ad alta risoluzione (ad es., `sample-highres.png`) in una cartella a cui puoi fare riferimento dal codice. L'immagine dovrebbe essere almeno a 300 dpi per la massima precisione OCR.

> **Suggerimento:** Se stai testando su un laptop senza GPU discreta, puoi comunque eseguire il codice; il motore tornerà automaticamente alla CPU.

![illustrazione di come abilitare la GPU](placeholder.png "Diagramma che mostra il pipeline OCR Java con accelerazione GPU – come abilitare la GPU")
[illustrazione di come abilitare la GPU](placeholder.png "Diagramma che mostra il pipeline OCR Java con accelerazione GPU – come abilitare la GPU")

## Passo 2 – Crea il motore OCR e carica l'immagine (estrarre testo dall'immagine)

La classe `OcrEngine` è l'oggetto di livello superiore che rappresenta una singola sessione OCR.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.*;

public class GpuOcrTutorial {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to process
        // Replace with the absolute or relative path to your PNG/JPEG/TIFF
        ocrEngine.setImage("YOUR_DIRECTORY/sample-highres.png");
```

Il metodo `setImage` accetta un percorso di file, un `java.io.File` o un `java.awt.image.BufferedImage`. Fornire una sorgente ad alta risoluzione garantisce che la GPU abbia abbastanza pixel per tenere tutti i suoi core occupati, il che si traduce in notevoli guadagni di velocità.

## Passo 3 – Configura l'accelerazione GPU (come configurare GPU)

L'oggetto `GpuConfiguration` ti consente di abilitare l'uso della GPU, selezionare un dispositivo e definire il comportamento di fallback per il motore OCR.

```java
        // Step 3: Enable GPU acceleration (optional: select a specific device)
        GpuConfiguration gpuConfig = new GpuConfiguration();
        gpuConfig.setEnabled(true);          // turn on GPU support
        gpuConfig.setDeviceId(0);            // choose GPU 0 (default first device)

        // Attach the GPU config to the OCR engine
        ocrEngine.setGpuConfiguration(gpuConfig);
```

## Passo 4 – Esegui il riconoscimento del testo (riconoscere testo java)

Con il motore e la GPU pronti, puoi finalmente estrarre i caratteri.

Il metodo `recognize()` esegue il pipeline OCR e restituisce un `OcrResult` contenente il testo semplice, i punteggi di confidenza e, facoltativamente, i dati delle bounding‑box.  
```java
        // Step 4: Perform the recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Output previsto** (troncato per brevità):

```
Recognized text:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

Se la tua immagine contiene più lingue, puoi aggiungere i pacchetti lingua prima di chiamare `recognize()`:

```java
ocrEngine.getLanguage().add(OcrLanguage.FRENCH);
ocrEngine.getLanguage().add(OcrLanguage.SPANISH);
```

## Passo 5 – Revisiona l'output e i prossimi passi

Esegui il programma con:

```bash
mvn compile exec:java -Dexec.mainClass=GpuOcrTutorial
```

Su una macchina con una GPU decente, l'OCR termina in **meno di un secondo per un'immagine da 4 MP**, rispetto a 3–5 secondi solo con la CPU. Questo incremento di velocità è particolarmente utile in scenari di elaborazione batch o in pipeline di ingestione documenti in tempo reale.

### Domande comuni

* **Cosa succede se ricevo l'errore “CUDA driver version is insufficient”?**  
  Aggiorna il driver NVIDIA all'ultima versione che corrisponde al toolkit CUDA fornito con Aspose (tipicamente CUDA 11.x nel 2026).

* **Posso elaborare un batch di immagini?**  
  Sì. Riutilizza una singola istanza `OcrEngine` all'interno di un ciclo per evitare la creazione ripetuta di contesti GPU, il che migliora il throughput.

* **Esiste un limite di memoria?**  
  L'uso della memoria GPU scala con le dimensioni dell'immagine; per TIFF molto grandi, suddividi l'immagine in tasselli prima di passarla al motore per rimanere entro i tipici limiti di 8 GB di memoria GPU.

### Suggerimenti professionali

* **Fissa la GPU** – su server multi‑GPU, imposta `gpuConfig.setDeviceId(1)` per riservare la seconda GPU per l'OCR mentre la prima gestisce altri carichi di lavoro.  
* **Riscaldamento** – chiama `ocrEngine.recognize()` su una piccola immagine fittizia una volta all'avvio; questo carica le reti neurali sulla GPU, eliminando la latenza della prima chiamata.  
* **Sicurezza dei thread** – ogni thread dovrebbe possedere la propria istanza `OcrEngine`; la classe non è thread‑safe, quindi la condivisione tra thread può causare condizioni di race.

## Domande frequenti

**D: Aspose OCR supporta l'input PDF?**  
R: Sì, puoi passare un file PDF direttamente a `setImage`; la libreria rasterizza ogni pagina prima dell'OCR.

**D: Come aggiungere dizionari personalizzati per termini specifici di dominio?**  
R: Usa `ocrEngine.getConfiguration().setCustomDictionary(List<String>)` per migliorare il riconoscimento del vocabolario specializzato.

**D: L'accelerazione GPU è disponibile su macOS?**  
R: Attualmente sono supportate solo GPU NVIDIA compatibili con CUDA su Windows e Linux; gli utenti macOS ricorrono alla CPU.

**D: Posso recuperare il punteggio di confidenza per ogni parola riconosciuta?**  
R: Assolutamente—`OcrResult` include un metodo `getConfidence()` per ogni oggetto `OcrWord`.

**D: Quale licenza è necessaria per l'uso in produzione?**  
R: È necessaria una licenza commerciale Aspose OCR per le distribuzioni in produzione; una licenza di valutazione gratuita è valida per sviluppo e test.

---

**Ultimo aggiornamento:** 2026-11-17  
**Testato con:** Aspose OCR 24.11 per Java  
**Autore:** Aspose  






```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- latest as of Jan 2026 -->
</dependency>
```

```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

## Tutorial correlati

- [Esempio Aspose Ocr Java Estrai Testo Da Immagine Con GPU](/ocr/java/advanced-ocr-techniques/aspose-ocr-java-example-extract-text-from-image-with-gpu/)
- [Riconosci Testo Da Immagine Java Ocr Con Accelerazione GPU](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/)
- [Tutorial OCR Accelerato GPU Java Guida Per Immagine Rapida In Testo](/ocr/java/advanced-ocr-techniques/gpu-accelerated-ocr-tutorial-java-guide-to-fast-image-to-tex/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}