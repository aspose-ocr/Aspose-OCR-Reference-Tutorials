---
category: general
date: 2026-10-30
description: Scopri come migliorare l'OCR preelaborando le immagini in Java con Aspose
  OCR. Questa guida mostra come aumentare il contrasto dell'immagine, impostare il
  livello di contrasto e estrarre il testo in modo efficiente.
draft: false
keywords:
- how to improve OCR
- how to boost contrast
- preprocess image OCR
- extract text image Java
- recognize text image Java
lastmod: 2026-10-30
og_description: Scopri come migliorare l'OCR preelaborando le immagini in Java con
  Aspose OCR. La guida spiega come aumentare il contrasto, impostare il livello di
  contrasto e estrarre il testo rapidamente.
og_image_alt: Screenshot of a Java OCR preprocessing pipeline showing before‑and‑after
  contrast enhancement
og_title: Come migliorare l'OCR – Guida alla preelaborazione delle immagini in Java
schemas:
- author: Aspose
  dateModified: '2026-10-30'
  description: Learn how to improve OCR by preprocessing images in Java with Aspose
    OCR. This guide shows how to boost image contrast, set contrast level, and extract
    text efficiently.
  headline: How to improve OCR – preprocess image for OCR in Java with Aspose
  type: TechArticle
- description: Learn how to improve OCR by preprocessing images in Java with Aspose
    OCR. This guide shows how to boost image contrast, set contrast level, and extract
    text efficiently.
  name: How to improve OCR – preprocess image for OCR in Java with Aspose
  steps:
  - name: '**Deskew** – corrects slight rotations.'
    text: '**Deskew** – corrects slight rotations.'
  - name: '**Denoise** – removes speckles that confuse character segmentation.'
    text: '**Denoise** – removes speckles that confuse character segmentation.'
  - name: '**Contrast enhancement** – makes dark text stand out against the background.'
    text: '**Contrast enhancement** – makes dark text stand out against the background.'
  type: HowTo
- questions:
  - answer: Yes—load the appropriate language pack with `engine.setLanguage("fr")`
      or any supported ISO code to improve accuracy for non‑English text.
    question: Can I use this approach for languages other than English?
  - answer: It does not read PDF pages natively; you should extract images from the
      PDF first (e.g., with Aspose PDF) and then feed them to the OCR engine.
    question: Does Aspose OCR support PDF input directly?
  - answer: The library handles images up to 30 MP without needing to load the whole
      file into memory, thanks to its streaming architecture.
    question: How large an image can I process?
  - answer: Absolutely—iterate over the files, reuse the same `OcrEngine` instance,
      and add each file to `OcrInput`. This reduces per‑image overhead dramatically.
    question: Is there a way to batch‑process a folder of images?
  - answer: Try adjusting `setContrastLevel` in smaller increments, experiment with
      `setDenoiseMode`, or enable `setUseAdaptiveThreshold(true)` for difficult backgrounds.
    question: What if the OCR output still contains errors?
  type: FAQPage
tags:
- Java
- OCR
- Image Processing
title: Come migliorare l'OCR – preelaborare l'immagine per l'OCR in Java con Aspose
url: /it/java/advanced-ocr-techniques/preprocess-image-for-ocr-complete-java-guide-to-boost-contra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Preprocessare l'immagine per OCR – guida completa Java

Mai avuto bisogno di **preprocessare l'immagine per OCR** ma non eri sicuro quali impostazioni facciano davvero la differenza? Non sei solo. La maggior parte degli sviluppatori lancia un'immagine a un motore OCR sperando che la magia avvenga, per poi ottenere output incomprensibili. In questo tutorial percorreremo un esempio pratico, end‑to‑end, che **aumenta il contrasto dell'immagine**, regola il **livello di contrasto**, e infine **riconosce il testo dall'immagine** usando Aspose OCR per Java.

Al termine avrai uno snippet di codice riutilizzabile che **estrae testo usando OCR** in modo affidabile, anche su scansioni rumorose. Nessun trucco nascosto, solo passaggi chiari e la motivazione dietro ciascuno.

## Risposte rapide
- **Qual è il primo passo per migliorare l'OCR?** Carica la tua licenza Aspose OCR prima di creare il motore.  
- **Quali tre opzioni di preprocessing sono le più importanti?** Deskew, denoise e miglioramento del contrasto.  
- **Quale livello di contrasto funziona per la maggior parte dei documenti stampati?** Intorno a 1.3 f offre un buon equilibrio.  
- **Posso vedere l'immagine elaborata?** Sì—esporta il bitmap intermedio in PNG.  
- **È necessaria una licenza per la produzione?** Assolutamente; una versione di prova funziona in modalità limitata e aggiunge filigrane.

## Come migliorare l'OCR preelaborando le immagini in Java?

Carica l'immagine, applica deskew, denoise e regola il contrasto, quindi esegui il riconoscitore. La pipeline di Aspose OCR elabora l'immagine in quell'ordine esatto, garantendo che ogni trasformazione operi sui dati più puliti possibile prima che il riconoscitore basato su rete neurale li veda. Questo approccio a due fasi—pre‑processare poi riconoscere—offre fino al 30 % di precisione dei caratteri più alta su documenti scansionati tipici.

## Cos'è Aspose OCR per Java?

Aspose OCR per Java è una libreria che supporta **oltre 30 formati di immagine** (inclusi JPEG, PNG, TIFF, BMP) e può elaborare un batch multi‑immagine di 200 pagine in meno di 2 secondi su un server standard a 8 core. Fornisce filtri integrati di deskew, denoise e miglioramento del contrasto che puoi configurare programmaticamente.

## Di cosa avrai bisogno

- Java 17 o versioni successive (qualsiasi JDK recente funziona)
- Libreria Aspose OCR per Java (scarica dal sito ufficiale di Aspose)
- Un file di licenza Aspose OCR valido (`Aspose.OCR.lic`)
- Un'immagine di input (`input.jpg`) che desideri leggere
- Il tuo IDE preferito o una semplice configurazione da riga di comando

Se li hai già, ottimo—tuffiamoci subito.

## Qual è il primo passo: caricare la licenza Aspose OCR?

Carica la licenza prima di creare qualsiasi oggetto OCR in modo che il motore funzioni in modalità completa anziché in modalità di prova. Questo previene le filigrane, sblocca tutte le opzioni di preprocessing e garantisce che il motore OCR possa accedere ai pacchetti linguistici con licenza e alle ottimizzazioni di prestazioni necessarie per un'estrazione accurata del testo.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {

        // Load the Aspose OCR license – this disables the evaluation limits
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Perché è importante:** Senza una licenza adeguata, il motore funziona in modalità valutazione, il che può troncare i risultati o aggiungere filigrane. Impostare la licenza in anticipo garantisce anche che le successive opzioni di preprocessing vengano applicate in modalità completa.

## Come si inizializza il motore OCR?

La classe `OcrEngine` è il componente centrale che esegue l'OCR e fornisce i controlli di preprocessing. Crea una singola istanza di `OcrEngine` e riutilizzala per ogni immagine per evitare il caricamento ripetuto del modello. Riutilizzare il motore memorizza nella cache i modelli di rete neurale interni, riducendo la latenza per immagine fino al 40 % e abbassando il consumo di memoria, rendendo l'elaborazione batch più efficiente.

```java
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Consiglio professionale:** Mantieni il motore come singleton se prevedi di elaborare molte immagini in batch; memorizza nella cache le risorse interne e velocizza le chiamate successive.

## Come configurare il preprocessing – deskew, denoise e miglioramento del contrasto

Ecco dove **preprocessiamo l'immagine per OCR**. Le tre impostazioni che modificheremo sono:

1. **Deskew** – corregge leggere rotazioni.
2. **Denoise** – rimuove i granelli che confondono la segmentazione dei caratteri.
3. **Miglioramento del contrasto** – fa risaltare il testo scuro rispetto allo sfondo.

```java
        // Access preprocessing settings
        PreprocessingSettings preprocessing = ocrEngine.getPreprocessing();

        // Enable automatic deskew (helps with scanned pages that are a few degrees off)
        preprocessing.setDeskew(true);
        preprocessing.setDeskewAngleTolerance(0.1); // tolerance in degrees

        // Turn on denoising – median works well for salt‑and‑pepper noise
        preprocessing.setDenoise(true);
        preprocessing.setDenoiseMode(DenoiseMode.MEDIAN); // alternatives: GAUSSIAN

        // Boost contrast – this is the “boost image contrast” step
        preprocessing.setContrastEnhance(true);
        preprocessing.setContrastLevel(1.3f); // 1.0 = no change, >1.0 = stronger contrast
```

### Perché regolare il livello di contrasto?

Aumentare il livello di contrasto allunga l'istogramma dell'immagine, rendendo i pixel scuri più scuri e quelli luminosi più luminosi. In pratica, un **livello di contrasto** di `1.3f` spesso offre il miglior equilibrio per i documenti stampati, mentre un valore superiore a `1.5f` può sovra‑esporre i tratti sottili. Sentiti libero di sperimentare; l'impostazione è poco costosa da modificare e può migliorare drasticamente il tasso di successo del **riconoscimento del testo dall'immagine**.

## Come preparare l'immagine di input?

La classe `OcrInput` rappresenta una collezione di immagini che il motore OCR elaborerà. La classe `OcrInput` astrae la gestione dei file, consentendoti di aggiungere una o più immagini per l'elaborazione batch. Puoi specificare percorsi di file individuali, stream o array di byte, e il motore tratterà ogni voce come una pagina separata, gestendo automaticamente il rilevamento del formato e la conversione secondo necessità.

```java
        // Prepare the image for OCR – you can add more files to the same OcrInput
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.jpg");
```

**Caso limite:** Se la tua immagine è in un formato non standard (ad esempio TIFF con più pagine), puoi caricare ogni pagina separatamente o convertirla prima in PNG/JPEG.

## Come funziona la fase di riconoscimento?

Quando invochi il metodo `recognize`, il motore applica prima la pipeline di preprocessing configurata—deskew, denoise e miglioramento del contrasto—in quell'ordine esatto. Dopo che l'immagine è stata pulita, viene passata al riconoscitore basato su rete neurale, che analizza le forme dei caratteri e restituisce il testo estratto come stringa.

```java
        // Run OCR – this returns a result object containing the extracted text
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Cosa succede dietro le quinte?** Aspose OCR applica prima la trasformazione deskew, poi esegue il filtro denoise e infine regola il contrasto prima di fornire l'immagine al suo riconoscitore basato su rete neurale. L'ordine è intenzionale; modificarlo potrebbe portare a risultati sub‑ottimali.

## Come ottenere il testo riconosciuto?

Dopo il completamento del riconoscimento, puoi recuperare il risultato tramite `getText` o `getTextLines`. In questo esempio stampiamo semplicemente la stringa estratta sulla console, ma in produzione potresti scriverla su un file, archiviarla in un database o inviarla tramite rete a servizi downstream.

```java
        // Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

### Output previsto

Se `input.jpg` contiene la frase “Hello World!”, la console dovrebbe mostrare:

```
Hello World!
```

Se l'output appare confuso, ricontrolla i valori di preprocessing—soprattutto il **livello di contrasto** e la **modalità denoise**—e prova un formato immagine diverso.

## Come visualizzare l'immagine pre‑elaborata (opzionale)?

Se hai bisogno di ispezionare ciò che il motore OCR vede dopo il preprocessing, puoi esportare il bitmap intermedio in un file PNG usando il metodo `saveProcessedImage`. Questo controllo visivo ti aiuta a verificare che le regolazioni di deskew, denoise e contrasto siano state applicate correttamente prima del riconoscimento.

```java
        // Export the pre‑processed image for debugging
        BufferedImage processed = preprocessing.getProcessedImage();
        ImageIO.write(processed, "png", new File("processed.png"));
```

![esempio di preprocessamento immagine per OCR](/images/ocr-preprocess-example.png "preprocessamento immagine per OCR – prima e dopo il potenziamento del contrasto")
[esempio di preprocessamento immagine per OCR](/images/ocr-preprocess-example.png "preprocessamento immagine per OCR – prima e dopo il potenziamento del contrasto")

*L'immagine sopra illustra come aumentare il contrasto e denoise trasformi una scansione sfocata in un'immagine pulita, pronta per l'OCR.*

## Problemi comuni e come evitarli

| Problema | Perché succede | Soluzione |
|----------|----------------|-----------|
| **Sovra‑contrasto** (`setContrastLevel` troppo alto) | Lo sfondo chiaro diventa bianco, cancellando i caratteri deboli | Mantieni il livello tra 1.1 e 1.4 per la maggior parte del testo stampato |
| **Tolleranza deskew troppo bassa** | Le piccole rotazioni rimangono non corrette | Aumenta `setDeskewAngleTolerance` a 0.2 o 0.3 per libri scansionati |
| **Usare denoise GAUSSIAN su immagini binarie** | Sfuma i bordi, unendo i caratteri | Usa `DenoiseMode.MEDIAN` per scansioni in bianco e nero |
| **Licenza mancante** | Il motore torna in modalità di prova, troncando l'output | Verifica il percorso di `Aspose.OCR.lic` e che il file sia leggibile |

## Domande frequenti

**D: Posso usare questo approccio per lingue diverse dall'inglese?**  
R: Sì—carica il pacchetto linguistico appropriato con `engine.setLanguage("fr")` o qualsiasi codice ISO supportato per migliorare la precisione per testi non‑inglesi.

**D: Aspose OCR supporta l'input PDF direttamente?**  
R: Non legge le pagine PDF nativamente; dovresti prima estrarre le immagini dal PDF (ad esempio con Aspose PDF) e poi passarle al motore OCR.

**D: Quanto grande può essere un'immagine che posso elaborare?**  
R: La libreria gestisce immagini fino a 30 MP senza dover caricare l'intero file in memoria, grazie alla sua architettura di streaming.

**D: Esiste un modo per elaborare in batch una cartella di immagini?**  
R: Assolutamente—itera sui file, riutilizza la stessa istanza di `OcrEngine` e aggiungi ogni file a `OcrInput`. Questo riduce drasticamente l'overhead per immagine.

**D: Cosa fare se l'output OCR contiene ancora errori?**  
R: Prova a regolare `setContrastLevel` a incrementi più piccoli, sperimenta con `setDenoiseMode`, o abilita `setUseAdaptiveThreshold(true)` per sfondi difficili.

## Prossimi passi: andare oltre il preprocessing di base

Ora che puoi **preprocessare l'immagine per OCR** e **estrarre testo usando OCR**, considera queste estensioni:

- **Pacchetti linguistici** – carica dizionari linguistici specifici per migliorare la precisione per testi non‑inglesi.  
- **Ritaglio di regione di interesse (ROI)** – concentrati su una sottosezione dell'immagine se ti serve solo una parte della pagina.  
- **Elaborazione batch** – itera su una directory di immagini, riutilizzando la stessa istanza di `OcrEngine` per velocità.  
- **Integrazione con PDF** – combina Aspose OCR con Aspose PDF per convertire PDF scansionati in PDF ricercabili in un'unica pipeline.

Ognuno di questi argomenti incorpora naturalmente le nostre parole chiave secondarie: continuerai a **aumentare il contrasto dell'immagine**, **impostare il livello di contrasto**, e a **riconoscere il testo dall'immagine** in molti scenari.

## Conclusione

Abbiamo coperto tutto ciò di cui hai bisogno per **preprocessare l'immagine per OCR** usando Aspose OCR per Java: caricare la licenza, configurare deskew, denoise e miglioramento del contrasto, fornire l'immagine e infine **riconoscere il testo dall'immagine**. Con l'esempio completo e eseguibile sopra, ora puoi **estrarre testo usando OCR** su qualsiasi immagine adeguatamente preparata.

Esegui il codice, regola il **livello di contrasto**, e osserva l'aumento della precisione. Quando sei pronto, esplora modelli specifici per lingua o pipeline batch per trasformare questa demo a immagine singola in una soluzione di livello produzione.

*Buona programmazione, e che le tue scansioni siano sempre nitide!*

---

**Ultimo aggiornamento:** 2026-10-30  
**Testato con:** Aspose OCR per Java 24.11  
**Autore:** Aspose

## Tutorial correlati

- [Estrarre testo da immagine con guida Aspose OCR Java](/ocr/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/)
- [Riconoscere testo immagine usando Aspose OCR GPU Java](/ocr/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/)
- [Creare motore OCR Java per riconoscere testo da immagini grandi](/ocr/java/advanced-ocr-techniques/create-ocr-engine-java-recognize-text-from-large-images/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}