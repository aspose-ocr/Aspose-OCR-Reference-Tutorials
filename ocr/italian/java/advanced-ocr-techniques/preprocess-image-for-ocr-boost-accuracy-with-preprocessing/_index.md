---
category: general
date: 2026-05-31
description: Preprocessa l'immagine per OCR per migliorare drasticamente l'accuratezza
  dell'OCR con la pre‑elaborazione usando Aspose OCR Java. Segui una guida completa
  passo‑passo.
draft: false
keywords:
- preprocess image for OCR
- improve OCR accuracy with preprocessing
language: it
og_description: Preprocessa l'immagine per l'OCR e scopri come migliorare l'accuratezza
  dell'OCR con la preelaborazione in Java usando Aspose OCR.
og_title: Preelabora l'immagine per OCR – Migliora l'accuratezza con la preelaborazione
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Preprocess image for OCR to dramatically improve OCR accuracy with
    preprocessing using Aspose OCR Java. Follow a complete step‑by‑step guide.
  headline: Preprocess Image for OCR – Boost Accuracy with Preprocessing
  type: TechArticle
- description: Preprocess image for OCR to dramatically improve OCR accuracy with
    preprocessing using Aspose OCR Java. Follow a complete step‑by‑step guide.
  name: Preprocess Image for OCR – Boost Accuracy with Preprocessing
  steps:
  - name: Loads the original PNG.
    text: Loads the original PNG.
  - name: Feeds it through `AutoDeskew`, `DenoiseMedian`, and `ContrastStretch`.
    text: Feeds it through `AutoDeskew`, `DenoiseMedian`, and `ContrastStretch`.
  - name: Runs the recognizer on the cleaned bitmap.
    text: Runs the recognizer on the cleaned bitmap.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Preprocessa l'immagine per OCR – Aumenta l'accuratezza con la preelaborazione
url: /it/java/advanced-ocr-techniques/preprocess-image-for-ocr-boost-accuracy-with-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Preprocessare l'Immagine per OCR – Incrementare la Precisione con il Preprocessamento

Ti sei mai chiesto perché i risultati OCR sembrano un pasticcio confuso anche se l'immagine di origine sembra a posto? Nella maggior parte dei casi il colpevole è nascosto nell'immagine—distorsione, rumore, basso contrasto—cose che ostacolano anche il riconoscitore più intelligente. **Preprocess image for OCR** e vedrai un salto drammatico nella qualità.  

In questo tutorial non solo ti mostreremo come preprocessare l'immagine per OCR, ma spiegheremo anche **come migliorare la precisione OCR con il preprocessamento** costruendo una piccola ma potente pipeline con Aspose OCR per Java. Alla fine avrai un programma pronto‑all'uso che trasforma un PNG rumoroso e inclinato in testo pulito e leggibile.

## Cosa Imparerai

- Perché il preprocessamento è importante per i motori OCR  
- Come configurare Aspose OCR in un progetto Java  
- Codice passo‑passo che **preprocesses image for OCR** usando filtri di deskew, denoise e contrasto  
- Suggerimenti per regolare la pipeline per **improve OCR accuracy with preprocessing** sui tuoi dataset  

Niente superfluo, solo un esempio completo e eseguibile e la logica dietro ogni riga.

## Prerequisiti

| Requisito | Motivo |
|-------------|--------|
| Java 8 o successivo | La libreria Aspose OCR Java richiede Java 8+ |
| Maven o Gradle (opzionale) | Semplifica l'aggiunta della dipendenza Aspose OCR |
| File di licenza Aspose OCR per Java (`Aspose.OCR.Java.lic`) | Necessario per sbloccare tutte le funzionalità |
| Un'immagine di esempio (es., `noisy_skewed.png`) | L'immagine su cui *preprocess image for OCR* |

Se qualcuno di questi manca, fermati ora e procurateli—provare a eseguire il codice senza licenza genererà semplicemente un'eccezione.

## Passo 1: Applica la tua licenza Aspose OCR

Prima di tutto. Il motore OCR non farà nulla di utile senza una licenza valida. Questo passo **preprocesses image for OCR** indirettamente sbloccando l'intero set di filtri immagine.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Apply your Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");
```

> **Consiglio professionale:** Mantieni il file di licenza fuori dal controllo di versione. Usa variabili d'ambiente o un vault sicuro in produzione.

## Passo 2: Inizializza il motore OCR e carica l'immagine sorgente

Ora creiamo il motore, indichiamo quale lingua ci aspettiamo e lo puntiamo al file che vogliamo *preprocess image for OCR*.

```java
        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Set the language – English works for most demos
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);

        // Load the source image (the one that needs preprocessing)
        ocrEngine.setImage(new OcrImage("YOUR_DIRECTORY/noisy_skewed.png"));
```

Perché impostare la lingua? Perché il motore può applicare euristiche specifiche per lingua, che già **improve OCR accuracy with preprocessing** prima ancora di toccare i filtri.

## Passo 3: Costruisci una Pipeline di Preprocessamento

Questo è il cuore del tutorial. Qui **preprocess image for OCR** concatenando tre filtri:

| Filtro | Cosa fa | Perché è importante per la precisione |
|--------|--------------|-----------------------------|
| `AutoDeskew` | Rileva e corregge la rotazione | Le linee di testo inclinate confondono la segmentazione dei caratteri |
| `DenoiseMedian(3)` | Riduzione del rumore con filtro mediano (kernel = 3) | Rimuove i puntini che sembrano caratteri erranti |
| `ContrastStretch` | Allunga l'istogramma per aumentare il contrasto | Gli sfondi scuri diventano leggibili, il testo chiaro risalta |

```java
        // Access the preprocessor
        OcrPreprocessor preprocessor = ocrEngine.getPreprocessor();

        // 1️⃣ Correct image skew
        preprocessor.addFilter(new AutoDeskew());

        // 2️⃣ Reduce noise with a median filter (kernel size = 3)
        preprocessor.addFilter(new DenoiseMedian(3));

        // 3️⃣ Enhance contrast for sharper edges
        preprocessor.addFilter(new ContrastStretch());
```

Nota che non dobbiamo scrivere alcun codice di elaborazione immagine da zero—Aspose fornisce filtri pronti all'uso. Questo migliora drasticamente **improve OCR accuracy with preprocessing** mantenendo l'implementazione concisa.

## Passo 4: Esegui l'OCR sull'Immagine Pre‑processata

Con la pipeline in atto, il motore applica automaticamente i filtri prima del riconoscimento. Tutto quello che serve è una singola chiamata:

```java
        // Perform OCR on the pre‑processed image
        String extractedText = ocrEngine.recognize();
```

Dietro le quinte il motore:

1. Carica il PNG originale.  
2. Lo passa attraverso `AutoDeskew`, `DenoiseMedian` e `ContrastStretch`.  
3. Esegue il riconoscitore sul bitmap pulito.  

Questa è la magia di **preprocess image for OCR**—il lavoro pesante è astratto.

## Passo 5: Output del Testo Riconosciuto

Infine, stampa il risultato sulla console o scrivilo su un file. Per scopi dimostrativi, un semplice `System.out.println` fa il lavoro.

```java
        // Show the extracted text
        System.out.println(extractedText);
    }
}
```

Se tutto è andato bene, dovresti vedere frasi pulite e leggibili invece di un pasticcio confuso. L'output esatto dipende dall'immagine sorgente, ma noterai un chiaro miglioramento rispetto all'esecuzione dell'OCR sul file grezzo.

### Output Atteso (esempio)

```
The quick brown fox jumps over the lazy dog.
This is a sample text line for OCR testing.
```

Se continui a ottenere caratteri strani, ricontrolla l'ordine dei filtri—a volte applicare `ContrastStretch` *prima* di `DenoiseMedian` produce risultati migliori su scansioni molto degradate.

## Visualizzare la Pipeline (Opzionale)

Di seguito è uno schema di come l'immagine fluisce attraverso ogni filtro. Può aiutarti a spiegare il processo ai colleghi o a includerlo nella documentazione.

![diagramma della pipeline preprocess image for OCR](pipeline.png "Diagramma che mostra le fasi AutoDeskew → DenoiseMedian → ContrastStretch per preprocess image for OCR")

*Testo alternativo:* *diagramma preprocess image for OCR che illustra i tre filtri applicati prima del riconoscimento.*

## Problemi Comuni & Come Risolverli

| Sintomo | Causa Probabile | Risoluzione |
|---------|-----------------|-------------|
| Il testo è ancora sfocato dopo il preprocessamento | Il filtro di contrasto non è sufficientemente forte | Aumenta il fattore di stretch o prova `HistogramEqualization` |
| OCR genera `NullPointerException` | Il percorso del file di licenza è errato | Verifica il percorso e assicurati che il file sia leggibile |
| La distorsione persiste | Rotazione dell'immagine > 15° (limite AutoDeskew) | Pre‑ruota manualmente usando `AffineTransform` prima della pipeline |
| Troppi falsi positivi | Livello di rumore alto, dimensione del kernel troppo piccola | Aumenta il kernel mediano (es., `new DenoiseMedian(5)`) |

Anticipando questi problemi, **improve OCR accuracy with preprocessing** anche sulle scansioni più difficili.

## Estendere la Pipeline

Vuoi più controllo? Aspose OCR ti permette di aggiungere filtri personalizzati o riordinare quelli esistenti. Ecco alcune idee:

- **Binarization**: `preprocessor.addFilter(new BinarizeOtsu());` – forza bianco‑e‑nero puro, utile per documenti stampati.  
- **Resize**: `preprocessor.addFilter(new Scale(2.0));` – ingrandisce le immagini a bassa risoluzione, spesso migliorando la precisione.  
- **Sharpen**: `preprocessor.addFilter(new Sharpen());` – accentua i bordi per caratteri molto piccoli.  

Ricorda, ogni filtro aggiuntivo aumenta il tempo di elaborazione, quindi esegui benchmark sull'hardware di destinazione.

## Codice Sorgente Completo (Pronto per Copia‑Incolla)

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply your Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create the OCR engine and configure language & source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);
        ocrEngine.setImage(new OcrImage("YOUR_DIRECTORY/noisy_skewed.png"));

        // Step 3: Build a preprocessing pipeline to improve OCR accuracy with preprocessing
        OcrPreprocessor preprocessor = ocrEngine.getPreprocessor();
        preprocessor.addFilter(new AutoDeskew());               // Correct image skew
        preprocessor.addFilter(new DenoiseMedian(3));           // Reduce noise (kernel size = 3)
        preprocessor.addFilter(new ContrastStretch());         // Enhance contrast

        // Step 4: Perform OCR on the pre‑processed image
        String extractedText = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println(extractedText);
    }
}
```

Salva questo come `PreprocessDemo.java`, aggiungi il JAR Aspose OCR al tuo classpath (o dichiaralo in Maven), e esegui:



## Cosa Dovresti Imparare Dopo?

- [Come eseguire OCR su testo immagine con lingua usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Estrarre testo da immagine Java con Aspose.OCR modalità Rileva Aree](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Come calcolare l'angolo di inclinazione in Java usando Aspose.OCR](/ocr/english/java/ocr-basics/calculate-skew-angle/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}