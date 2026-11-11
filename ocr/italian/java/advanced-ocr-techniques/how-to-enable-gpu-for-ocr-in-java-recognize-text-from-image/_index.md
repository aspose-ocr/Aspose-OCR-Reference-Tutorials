---
category: general
date: 2026-08-22
description: Come abilitare la GPU nell'OCR Java per riconoscere rapidamente il testo
  da un'immagine. Impara a estrarre il testo da PNG, impostare le opzioni dell'immagine
  e riconoscere il testo in modo efficiente usando Aspose OCR.
draft: false
keywords:
- how to enable gpu
- recognize text image java
- aspose ocr java tutorial
- extract text from png
- set image options
lastmod: 2026-08-22
og_description: Come abilitare la GPU nell'OCR Java per riconoscere rapidamente il
  testo da un'immagine. Questa guida mostra come estrarre il testo da PNG, impostare
  le opzioni dell'immagine e riconoscere il testo in modo efficiente usando Aspose
  OCR.
og_image_alt: Java OCR GPU example code snippet showing Aspose OCR usage
og_title: Come abilitare la GPU per l'OCR in Java – estrazione rapida del testo
schemas:
- author: Aspose
  dateModified: '2026-08-22'
  description: How to enable GPU in Java OCR to recognize text from image quickly.
    Learn to extract text from PNG, set image options, and recognize text efficiently
    using Aspose OCR.
  headline: How to Enable GPU for OCR in Java – Recognize Text from Image Fast
  type: TechArticle
- description: How to enable GPU in Java OCR to recognize text from image quickly.
    Learn to extract text from PNG, set image options, and recognize text efficiently
    using Aspose OCR.
  name: How to Enable GPU for OCR in Java – Recognize Text from Image Fast
  steps:
  - name: '**Low‑resolution scans (< 150 dpi).** Upscale first or ask the user for
      a higher‑resolution scan.'
    text: '**Low‑resolution scans (< 150 dpi).** Upscale first or ask the user for
      a higher‑resolution scan.'
  - name: '**Handwritten notes.** The default model focuses on printed text; you’d
      need a custom trained model for cursive.'
    text: '**Handwritten notes.** The default model focuses on printed text; you’d
      need a custom trained model for cursive.'
  - name: '**Multiple languages.** Pass a comma‑separated list to `RecognitionLanguage`,
      e.g., `RecognitionLanguage.ENGLISH_FRENCH`.'
    text: '**Multiple languages.** Pass a comma‑separated list to `RecognitionLanguage`,
      e.g., `RecognitionLanguage.ENGLISH_FRENCH`.'
  type: HowTo
- questions:
  - answer: Yes, the Aspose OCR trial includes full GPU support; you just need to
      enable it in code.
    question: Does the free trial support GPU acceleration?
  - answer: Aspose OCR can rasterize PDF pages internally, but for best performance
      convert to high‑resolution PNG first.
    question: Can I process PDFs directly without converting to images?
  - answer: CUDA 11.2 or newer is recommended; older versions may work but are not
      officially tested.
    question: What CUDA version is required?
  - answer: Validate file size and type before processing, and run the OCR in a sandboxed
      thread to mitigate risks.
    question: Is it safe to run OCR on untrusted user uploads?
  - answer: Set `ocrEngine.setDebugMode(true)`; the console will list the selected
      GPU device and memory statistics.
    question: How do I enable logging to verify GPU usage?
  type: FAQPage
tags:
- OCR
- Java
- GPU
title: Come abilitare la GPU per l'OCR in Java – Riconoscere rapidamente il testo
  da un'immagine
url: /it/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come abilitare la GPU per OCR in Java – Riconoscere il testo da immagine rapidamente

Abilitare l'accelerazione GPU in un'applicazione OCR Java può ridurre drasticamente i tempi di elaborazione, soprattutto quando è necessario estrarre testo da immagini di grandi dimensioni o da lotti ad alto volume. In questo tutorial imparerai **come abilitare la GPU**, come **riconoscere il testo da immagine** e i passaggi esatti per **estrarre testo da PNG** usando la libreria Aspose OCR. Esamineremo anche le opzioni di pre‑elaborazione delle immagini che migliorano l'accuratezza e risponderemo alle domande comuni su “come riconoscere il testo” lungo il percorso.

## Risposte rapide
- **Qual è il maggior guadagno di velocità?** Fino a 5× più veloce su una RTX 2060 di fascia media rispetto a OCR solo CPU.  
- **Ho bisogno di una licenza speciale?** Una licenza standard Aspose OCR funziona per la GPU; basta abilitare il flag GPU.  
- **Quale versione di Java è richiesta?** Java 17 o superiore è consigliata per prestazioni ottimali.  
- **Posso eseguirlo dentro Docker?** Sì – basta aggiungere il flag `--gpus all` e installare i driver NVIDIA nel container.  
- **Il codice è compatibile con altri formati immagine?** La stessa API funziona per JPEG, TIFF, BMP e PNG senza modifiche.

## Di cosa avrai bisogno

Hai bisogno di una macchina con GPU abilitata, della libreria Aspose OCR per Java e di un ambiente di sviluppo Java 17 (o superiore). Una configurazione tipica include una NVIDIA RTX 3060 o qualsiasi scheda compatibile CUDA, l'ultimo JAR Aspose OCR da Maven Central e una fattura PNG di esempio per il benchmark.

**Risposta diretta (40‑70 parole):** Per iniziare devi installare Java 17, aggiungere la dipendenza Aspose OCR al tuo progetto, verificare che la JVM rilevi almeno un dispositivo CUDA e avere un'immagine di test pronta. Una volta soddisfatti questi prerequisiti, puoi abilitare la GPU nel motore OCR e iniziare a elaborare le immagini alla velocità della GPU.

- **Java 17** (o superiore) – il codice compila con versioni precedenti ma 17 offre il miglior supporto API.  
- **Aspose OCR per Java** – ottieni l'ultimo JAR dal sito Aspose o da Maven Central.  
- **Una GPU compatibile CUDA** – ad es. NVIDIA RTX 3060, RTX 2070 o qualsiasi scheda moderna con driver appropriati.  
- **Immagine di test** – una fattura PNG di grande formato funziona bene per misurare le prestazioni.

> **Consiglio professionale:** sui laptop con grafica integrata e discreta, forza la JVM a usare la GPU discreta tramite il pannello di controllo del driver; altrimenti la libreria torna silenziosamente alla CPU.

![how to enable gpu example](image.png "how to enable gpu example")
[how to enable gpu example](image.png "how to enable gpu example")

*Testo alternativo: esempio di come abilitare la gpu che mostra uno snippet di codice Java.*

## Passo 1 – Installa Aspose OCR e verifica la disponibilità della GPU

GpuSettings è una classe che controlla l'uso della GPU per il motore Aspose OCR.

Aggiungi la dipendenza Maven (o copia il JAR in `libs/`):

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Check for the latest version -->
</dependency>
```

Esegui lo snippet di verifica per elencare i dispositivi disponibili:

```java
import com.aspose.ocr.GpuSettings;

public class GpuCheck {
    public static void main(String[] args) {
        GpuSettings settings = new GpuSettings();
        System.out.println("GPU enabled? " + settings.getEnable());
        System.out.println("Detected GPU count: " + settings.getDeviceCount());
    }
}
```

Se l'output mostra un conteggio di dispositivi diverso da zero, la tua JVM vede la GPU. Se riporta zero, ricontrolla l'installazione dei driver e che la variabile d'ambiente `CUDA_PATH` sia impostata.

## Passo 2 – Come abilitare la GPU in Aspose OCR

**Risposta diretta (40‑70 parole):** Abilita la GPU creando un oggetto `GpuSettings`, impostando `setEnable(true)`, opzionalmente specificando l'ID del dispositivo, e passando questo oggetto di impostazioni al costruttore `AsposeOCR`. Dopo di ciò, tutte le successive chiamate OCR verranno eseguite sulla GPU selezionata, fornendo i miglioramenti di velocità descritti nella sezione delle prestazioni.

La classe `GpuSettings` consente di attivare/disattivare l'uso della GPU e di selezionare un dispositivo specifico quando sono presenti più GPU.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.GpuSettings;
import com.aspose.ocr.ImageProcessingOptions;
import com.aspose.ocr.RecognitionLanguage;
import com.aspose.ocr.OcrResult;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // 2️⃣ Enable GPU processing (auto‑detects available device)
        GpuSettings gpuSettings = new GpuSettings();
        gpuSettings.setEnable(true);          // turn GPU on
        gpuSettings.setDeviceId(0);           // first GPU (change if you have multiple)
        ocrEngine.setGpuSettings(gpuSettings);

        // 3️⃣ Optimize image preprocessing for GPU performance
        ImageProcessingOptions imgOpts = new ImageProcessingOptions();
        imgOpts.setAutoDeskew(true);
        imgOpts.setBinarization(true);
        ocrEngine.setImageProcessingOptions(imgOpts);

        // 4️⃣ Recognize text from an image file (PNG in this case)
        OcrResult result = ocrEngine.recognizeImage(
                "YOUR_DIRECTORY/large_invoice.png",
                RecognitionLanguage.ENGLISH);

        // 5️⃣ Output the detected text
        System.out.println("Detected text:\n" + result.getText());
    }
}
```

### Perché abilitare la GPU?

L'accelerazione GPU scarica il lavoro pesante di moltiplicazione di matrici che i modelli OCR eseguono su migliaia di core paralleli. In pratica vedrai **accelerazioni da 2‑5×** su una RTX 2060 modesta, e ancora di più su schede più recenti. Il compromesso è un consumo di memoria leggermente più alto, ma di solito non è un problema per PNG di dimensioni tipiche di fatture.

## Passo 3 – Riconoscere il testo da immagine Java – migliori pratiche

Il metodo `recognizeImage` elabora il file immagine fornito e restituisce il testo estratto.

**Risposta diretta (40‑70 parole):** Chiama `ocrEngine.recognizeImage(filePath)` dopo aver abilitato la GPU; il metodo rileva automaticamente il formato del file, esegue il modello OCR sulla GPU e restituisce il testo estratto. Per la massima accuratezza, assicurati che l'immagine sia binarizzata e deskewed prima della chiamata.

Il codice sopra lo fa già, ma ecco una versione semplificata che isola la chiamata OCR:

```java
// Assuming ocrEngine is already configured with GPU
String imagePath = "sample.png";
OcrResult ocrResult = ocrEngine.recognizeImage(imagePath, RecognitionLanguage.ENGLISH);
String extractedText = ocrResult.getText();

System.out.println("Extracted text from PNG:");
System.out.println(extractedText);
```

**Cosa noterai:** Il metodo `recognizeImage` rileva automaticamente il tipo di file, quindi puoi fornire JPEG, TIFF o PNG senza flag aggiuntivi. Ecco perché **estrarre testo da PNG** funziona subito.

### Gestione di file di grandi dimensioni

Se il tuo PNG è più grande di 5 MB, considera di ridimensionarlo prima dell'OCR:

```java
imgOpts.setResizeFactor(0.5); // shrink to 50 % of original dimensions
ocrEngine.setImageProcessingOptions(imgOpts);
```

Il down‑sampling riduce l'uso di memoria GPU e spesso migliora l'accuratezza perché il modello vede bordi più puliti.

## Passo 4 – Come impostare le opzioni immagine per una migliore accuratezza

ImageOptions è un oggetto di configurazione che consente di regolare i passaggi di pre‑elaborazione come deskewing e binarizzazione prima dell'OCR.

**Risposta diretta (40‑70 parole):** Usa l'oggetto `ImageOptions` per abilitare auto‑deskew, binarizzazione e ridimensionamento opzionale prima di passare l'immagine al motore OCR. I valori tipici sono `setAutoDeskew(true)`, `setBinarization(true)` e un fattore di ridimensionamento tra 0.5 e 0.8 per scansioni grandi. Queste impostazioni migliorano contrasto e allineamento, aiutando la rete neurale a riconoscere i caratteri più accuratamente, soprattutto su documenti rumorosi o inclinati.

La frase **come impostare immagine** appare naturalmente quando parliamo di pre‑elaborazione. Aspose OCR offre una serie di impostazioni:

| Opzione                     | Cosa fa                                   | Valore tipico |
|----------------------------|-------------------------------------------|---------------|
| `setAutoDeskew(true)`      | Raddrizza le linee di testo inclinate    | true          |
| `setBinarization(true)`    | Converte in bianco‑nero per migliorare il contrasto | true          |
| `setResizeFactor(x)`       | Ridimensiona l'immagine (0 < x ≤ 1)       | 0.5‑0.8       |
| `setContrastAdjustment(y)` | Aumenta il contrasto (0‑100)              | 30            |

Puoi combinarle in qualsiasi ordine; la libreria le applica sequenzialmente prima di inviare l'immagine alla rete neurale. La sperimentazione è fondamentale—diverse fatture possono richiedere soglie diverse.

## Passo 5 – Come riconoscere il testo in casi limite

La classe `GpuExample` dimostra un flusso OCR end‑to‑end completo usando Aspose OCR con accelerazione GPU.

**Risposta diretta (40‑70 parole):** Per scansioni a bassa risoluzione, prima ingrandisci l'immagine o richiedi una sorgente a più alta risoluzione; per note scritte a mano, passa a un modello personalizzato; e per documenti multilingue, passa una lista separata da virgole a `RecognitionLanguage`. Queste regolazioni garantiscono che il motore accelerato dalla GPU fornisca risultati affidabili.

Anche con la potenza della GPU, alcuni scenari ostacolano l'OCR:

1. **Scansioni a bassa risoluzione (< 150 dpi).** Ingrandisci prima o chiedi all'utente una scansione a risoluzione più alta.  
2. **Note scritte a mano.** Il modello predefinito si concentra su testo stampato; è necessario un modello personalizzato per la scrittura corsiva.  
3. **Molteplici lingue.** Passa una lista separata da virgole a `RecognitionLanguage`, ad esempio `RecognitionLanguage.ENGLISH_FRENCH`.

```java
ocrEngine.recognizeImage("multilang.png",
        RecognitionLanguage.ENGLISH_FRENCH);
```

## Output previsto

Eseguendo la classe completa `GpuExample` su `large_invoice.png` dovrebbe stampare qualcosa del genere:

```
Detected text:
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
...
```

Se vedi caratteri incomprensibili, ricontrolla che `gpuSettings.setEnable(true)` abbia effettivamente avuto effetto (la console elencherà il dispositivo GPU se abiliti il logging di debug).

## Problemi comuni & consigli professionali

- **Dimenticato di impostare l'ID del dispositivo GPU.** Su sistemi con più GPU, potrebbe essere necessario `setDeviceId(1)`.  
- **Esecuzione dentro Docker senza runtime NVIDIA.** Aggiungi `--gpus all` al comando `docker run`.  
- **Mescolare percorsi di codice solo CPU e abilitati GPU.** Mantieni una singola istanza `AsposeOCR` per thread per evitare conflitti di stato.  
- **Perdite di memoria.** Chiama `ocrEngine.dispose()` quando hai finito, specialmente in servizi a lunga esecuzione.

## Domande frequenti

**D: La versione di prova gratuita supporta l'accelerazione GPU?**  
R: Sì, la versione di prova Aspose OCR include il supporto completo alla GPU; devi solo abilitarla nel codice.

**D: Posso elaborare PDF direttamente senza convertirli in immagini?**  
R: Aspose OCR può rasterizzare le pagine PDF internamente, ma per le migliori prestazioni convertili prima in PNG ad alta risoluzione.

**D: Quale versione di CUDA è richiesta?**  
R: Si consiglia CUDA 11.2 o superiore; versioni più vecchie possono funzionare ma non sono testate ufficialmente.

**D: È sicuro eseguire OCR su upload di utenti non attendibili?**  
R: Convalida dimensione e tipo del file prima dell'elaborazione e esegui l'OCR in un thread sandbox per mitigare i rischi.

**D: Come abilito il logging per verificare l'uso della GPU?**  
R: Imposta `ocrEngine.setDebugMode(true)`; la console elencherà il dispositivo GPU selezionato e le statistiche di memoria.

## Conclusione

Abbiamo illustrato **come abilitare la GPU** per Aspose OCR in Java, mostrato come **riconoscere il testo da immagine**, dimostrato il modo più semplice per **estrarre testo da PNG**, spiegato **come impostare le opzioni immagine**, e trattato le sfumature di **come riconoscere il testo** in file reali. Con la GPU attivata, il tuo pipeline OCR dovrebbe essere notevolmente più veloce, rendendola adatta a scenari ad alto volume come l'elaborazione batch di fatture o la scansione di documenti in tempo reale.

Pronto per il passo successivo? Prova a sostituire il modello inglese predefinito con uno multilingue, o sperimenta pipeline di pre‑elaborazione personalizzate per ricevute rumorose. Il cielo è il limite—soprattutto quando hai una GPU che fa il lavoro pesante.

**Ultimo aggiornamento:** 2026-08-22  
**Testato con:** Aspose OCR for Java 24.10  
**Autore:** Aspose

## Tutorial correlati

- [Riconoscere testo da immagine con Aspose OCR tutorial completo Java OCR](/ocr/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Come impostare la licenza Aspose OCR e verificarla in Java](/ocr/java/ocr-basics/set-license/)
- [Estrarre testo da immagine Java con Aspose.OCR modalità rileva aree](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}