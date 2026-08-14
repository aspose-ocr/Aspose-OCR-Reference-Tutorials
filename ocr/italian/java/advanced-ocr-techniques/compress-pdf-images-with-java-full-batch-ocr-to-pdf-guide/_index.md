---
category: general
date: 2026-07-05
description: Comprimi le immagini PDF durante la conversione da PNG a PDF usando Java.
  Impara la preelaborazione delle immagini per OCR, riconosci il testo da JPG e esegui
  OCR batch su PDF in un unico tutorial.
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: it
og_description: Comprimi le immagini PDF e converti PNG in PDF usando Java. Questa
  guida copre la pre‑elaborazione delle immagini per OCR, il riconoscimento del testo
  JPG e l'OCR batch in PDF.
og_title: Comprimi le immagini PDF con Java – Tutorial completo di OCR batch
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  headline: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  type: TechArticle
- description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  name: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints a line for each image, e.g.:'
  - name: What if my server has no GPU?
    text: Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains
      unchanged, and you still get multithreaded CPU processing.
  - name: My PDFs are still too large—can I lower the quality further?
    text: Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink
      size more aggressively but may blur fine glyphs. Test with a representative
      sample.
  - name: How do I handle other image formats (TIFF, BMP)?
    text: 'Add the extensions to the filter lambda:'
  - name: Can I keep the original color images instead of binarizing?
    text: Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder
      if you need color retention for downstream analysis.
  type: HowTo
tags:
- ocr
- java
- pdf
- image-processing
title: Comprimi le immagini PDF con Java – Guida completa all'OCR batch per PDF
url: /it/java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comprimi le immagini PDF con Java – Guida completa per OCR batch a PDF

Hai mai dovuto **comprimere le immagini PDF** trasformando una cartella di PNG in PDF ricercabili? Non sei l’unico. In molti flussi di automazione il punto dolente più grande è gestire contemporaneamente la qualità dell’immagine, l’accuratezza dell’OCR e la dimensione finale del PDF.  

In questo tutorial vedremo una soluzione pratica che **converte PNG in PDF**, applica **pre‑elaborazione delle immagini per OCR**, e infine **comprime le immagini PDF** così l’output rimane leggero. Alla fine saprai come **riconoscere testo JPG**, impostare un flusso di lavoro **batch OCR to PDF**, e mantenere i tuoi PDF ordinati.

## Cosa imparerai

- Configurare Aspose OCR per Java e applicare una licenza.  
- Configurare il motore per multithreading, accelerazione GPU e correzione ortografica.  
- Costruire una pipeline riutilizzabile di **pre‑elaborazione delle immagini per OCR** (denoise, contrasto, binarizzazione).  
- Usare **PdfSaveOptions** per **comprimere le immagini PDF** senza sacrificare la leggibilità.  
- Scorrere una directory per **convertire PNG in PDF** e **riconoscere testo JPG** in blocco.  
- Un programma Java completo, pronto‑da‑eseguire, da inserire in qualsiasi progetto.

> **Prerequisiti**: Java 8+, Maven o Gradle, una licenza Aspose OCR per Java, e una cartella di immagini PNG/JPG da elaborare.

---

## Passo 1: Applica la licenza Aspose OCR (Essenziale per la produzione)

Prima di poter chiamare le API OCR devi caricare una licenza valida; altrimenti sarai limitato alla versione di prova.

```java
import com.aspose.ocr.*;

public class LicenseSetup {
    public static void loadLicense() throws Exception {
        License license = new License();
        // Point to your license file – keep it out of source control!
        license.setLicense("Aspose.OCR.Java.lic");
    }
}
```

*Perché è importante*: Un motore con licenza sblocca il supporto GPU, una maggiore accuratezza e rimuove i watermark che altrimenti gonferebbero i tuoi file PDF.

---

## Passo 2: Configura il motore OCR – Thread, GPU e correzione ortografica

Un motore OCR veloce è la spina dorsale di qualsiasi lavoro **batch OCR to PDF**. Avvieremo tanti thread quanti ne può gestire la CPU host, abiliteremo l’accelerazione GPU (se hai una scheda compatibile) e stringeremo la correzione ortografica per pulire gli errori OCR.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.GPUSettings;
import com.aspose.ocr.spell.SpellCorrectionOptions;

public class EngineConfig {
    public static OcrEngine createEngine() {
        OcrEngine ocrEngine = new OcrEngine();

        // Use all available logical processors
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Enable GPU – huge speedup for large batches
        GPUSettings gpu = new GPUSettings();
        gpu.setEnabled(true);
        ocrEngine.setGpuSettings(gpu);

        // Light spell correction: fix common typos without over‑correcting
        SpellCorrectionOptions spellOpts = new SpellCorrectionOptions();
        spellOpts.setMaxEditDistance(1);
        ocrEngine.getSpellCorrection().setOptions(spellOpts);

        return ocrEngine;
    }
}
```

*Suggerimento professionale*: Se stai eseguendo su un server headless senza GPU, imposta semplicemente `gpu.setEnabled(false)` – il codice funzionerà comunque, solo un po’ più lentamente.

---

## Passo 3: Costruisci una pipeline di pre‑elaborazione delle immagini

Le scansioni grezze spesso soffrono di rumore, basso contrasto o illuminazione non uniforme. **La pre‑elaborazione delle immagini per OCR** migliora drasticamente i tassi di riconoscimento, specialmente negli scenari **riconoscere testo JPG**.

```java
import com.aspose.ocr.*;

public class PreprocessorSetup {
    public static ImagePreprocessor createPreprocessor() {
        return new ImagePreprocessor.Builder()
                .addDenoise(0.7)      // Reduce grain while preserving edges
                .addContrast(1.15)    // Boost contrast for clearer glyphs
                .addBinarize()        // Convert to black‑and‑white for OCR
                .build();
    }
}
```

*Perché concatenamo questi*: La denoising prima impedisce al binarizzatore di amplificare i granelli; il contrasto poi assicura che i caratteri risaltino; infine, la binarizzazione fornisce al motore OCR un’immagine binaria pulita con cui lavorare.

---

## Passo 4: Prepara le opzioni di salvataggio PDF – **Comprimere le immagini PDF** in modo efficiente

Aspose ti permette di affinare l’output PDF. Attiveremo la compressione delle immagini e imposteremo un livello di qualità che bilancia dimensione e leggibilità.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOptions {
    public static PdfSaveOptions createOptions() {
        PdfSaveOptions options = new PdfSaveOptions();
        options.setCompressImages(true);   // This is the key to compress PDF images
        options.setImageQuality(90);       // 90% retains sharp text while shrinking file size
        return options;
    }
}
```

*Risultato*: Ogni PDF ricercabile sarà notevolmente più piccolo—ideale per l’archiviazione o l’invio via email.

---

## Passo 5: Elabora la cartella – **Converti PNG in PDF** e **riconosci testo JPG** in un unico ciclo

Ora mettiamo tutto insieme. Il ciclo scorre una directory di input, esegue l’OCR su ogni PNG o JPG, e scrive un PDF ricercabile in una cartella di output. Il nome del PDF rispecchia il nome dell’immagine sorgente.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.PdfSaveOptions;
import java.io.File;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license
        LicenseSetup.loadLicense();

        // 2️⃣ Engine & preprocessing
        OcrEngine ocrEngine = EngineConfig.createEngine();
        ocrEngine.setPreprocessor(PreprocessorSetup.createPreprocessor());

        // 3️⃣ PDF options (compress PDF images)
        PdfSaveOptions pdfOptions = PdfOptions.createOptions();

        // 4️⃣ Define input / output folders
        File inputFolder = new File("YOUR_DIRECTORY/input");
        File outputFolder = new File("YOUR_DIRECTORY/output");
        if (!outputFolder.exists()) outputFolder.mkdirs();

        // 5️⃣ Filter PNG & JPG files
        File[] imageFiles = inputFolder.listFiles((dir, name) ->
                name.toLowerCase().endsWith(".png") || name.toLowerCase().endsWith(".jpg"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG or JPG files found in the input folder.");
            return;
        }

        // 6️⃣ Process each file
        for (File image : imageFiles) {
            // Recognize text – works for both PNG and JPG
            ocrEngine.recognizeImage(image.getAbsolutePath());

            // Build output PDF path (same base name)
            String pdfPath = outputFolder.getAbsolutePath() + File.separator +
                    image.getName().replaceAll("\\.(png|jpg)$", ".pdf");

            // Save as searchable PDF – this step also compresses images
            ocrEngine.saveAsSearchablePdf(pdfPath, pdfOptions);

            System.out.println("✅ Processed: " + image.getName() + " → " + pdfPath);
        }

        System.out.println("🎉 All files have been converted and compressed!");
    }
}
```

### Output previsto

L’esecuzione del programma stampa una riga per ogni immagine, ad esempio:

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

Apri qualsiasi PDF risultante in un visualizzatore e vedrai testo selezionabile e ricercabile, mentre la dimensione del file è tipicamente **30‑50 % più piccola** rispetto a una controparte non compressa.

---

## Domande comuni e casi limite

### E se il mio server non ha GPU?
Imposta semplicemente `gpuSettings.setEnabled(false)`. Il resto della pipeline rimane invariato e ottieni comunque l’elaborazione multithreaded su CPU.

### I miei PDF sono ancora troppo grandi—posso abbassare ulteriormente la qualità?
Sì. Regola `options.setImageQuality(70)` o anche `50`. Valori più bassi riducono la dimensione in modo più aggressivo ma possono sfocare i glifi più fini. Prova con un campione rappresentativo.

### Come gestisco altri formati immagine (TIFF, BMP)?
Aggiungi le estensioni al filtro lambda:

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

La stessa pipeline di pre‑elaborazione funziona per la maggior parte dei formati raster.

### Posso mantenere le immagini a colori originali invece di binarizzarle?
Sostituisci `.addBinarize()` con `.addGrayscale()` nel builder del preprocessore se hai bisogno di conservare il colore per analisi successive.

---

## Suggerimenti professionali per un OCR batch pronto per la produzione

- **Gestione della memoria**: Riutilizza una singola istanza `OcrEngine` (come mostrato) per evitare l’overhead di creare/distruggere oggetti per ogni immagine.  
- **Gestione degli errori**: Avvolgi il blocco per file in un `try/catch` per registrare i fallimenti senza interrompere l’intero batch.  
- **Logging**: Usa un framework di logging adeguato (SLF4J, Log4j) invece di `System.out.println` per soluzioni scalabili.  
- **Parallelismo**: Per cartelle molto grandi, considera di elaborare le sotto‑directory con stream paralleli, ma tieni d’occhio la contesa della GPU.  
- **Sicurezza**: Conserva il file di licenza fuori dal repository e proteggilo con permessi di file system.

---

## Conclusione

Abbiamo appena dimostrato come **comprimere le immagini PDF** mentre eseguiamo una conversione **batch OCR to PDF** che **converte PNG in PDF**, **riconosce testo JPG**, e applica una robusta pipeline **di pre‑elaborazione delle immagini per OCR**. Il programma Java completo è autonomo, gira su qualsiasi JDK moderno, e produce PDF ricercabili e leggeri pronti per l’archiviazione o l’analisi successiva.

Prossimi passi? Sperimenta con diversi parametri di pre‑elaborazione, prova lingue OCR diverse dall’inglese, o integra il flusso in un microservizio Spring Boot che osserva una directory e processa i file al volo. I concetti fondamentali—caricamento licenza, configurazione motore, pre‑elaborazione e compressione PDF—rimangono gli stessi, fornendoti una solida base per qualsiasi progetto basato su OCR.

Hai domande o vuoi condividere le tue modifiche? Lascia un commento qui sotto, e buona programmazione!

![Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output](alt="Diagramma del flusso OCR batch che mostra immagini di input, pre‑elaborazione, motore OCR e output PDF compresso")


## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Riconosci testo PDF – Operazioni OCR con Aspose.OCR per Java](/ocr/english/java/ocr-operations/)
- [Riconosci testo da immagine con Aspose OCR – Tutorial OCR Java completo](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Converti immagine in testo in Java usando Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}