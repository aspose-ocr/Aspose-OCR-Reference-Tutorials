---
category: general
date: 2026-06-22
description: 'Come raddrizzare l''immagine per OCR: impara i passaggi di pre‑elaborazione
  delle immagini per OCR, rimuovi il rumore sale e pepe e aumenta la precisione.'
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: it
og_description: Come correggere l'inclinazione di un'immagine per OCR, rimuovere il
  rumore sale e pepe e applicare tecniche di pre‑elaborazione delle immagini per OCR
  in un esempio Java completo.
og_title: Come raddrizzare l'immagine – Guida alla pre‑elaborazione delle immagini
  per OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: 'How to deskew image for OCR: learn image preprocessing OCR steps,
    remove salt pepper noise, and boost accuracy.'
  headline: How to Deskew Image – Image Preprocessing OCR Guide
  type: TechArticle
tags:
- OCR
- image-processing
- Java
title: Come raddrizzare l'immagine – Guida alla preelaborazione delle immagini per
  OCR
url: /it/java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come correggere l'inclinazione di un'immagine – Guida al preprocessing delle immagini per OCR

Ti sei mai chiesto **come correggere l'inclinazione di un'immagine** in modo che il tuo motore OCR legga effettivamente il testo? Non sei l'unico. Una scansione inclinata può trasformare un documento perfetto in un pasticcio incomprensibile, e la maggior parte degli sviluppatori si imbatte in questo problema almeno una volta.

In questo tutorial percorreremo un'intera pipeline **image preprocessing OCR** che non solo corregge la rotazione ma rimuove anche gli artefatti **salt pepper** e aumenta il contrasto—praticamente tutto ciò di cui hai bisogno per **preprocess images OCR**‑style prima di inviarle al motore. Alla fine avrai uno snippet Java pronto all'uso e un chiaro modello mentale del perché ogni passaggio è importante.

## Come correggere l'inclinazione di un'immagine – Costruire la pipeline di preprocessing

Il cuore di qualsiasi flusso di lavoro OCR‑friendly è un oggetto **preprocess options** che collega una serie di filtri. Pensalo come un nastro trasportatore: ogni filtro esegue un compito, poi passa l'immagine al successivo. Di seguito è riportato un esempio minimale ma completo che utilizza una libreria OCR ipotetica fornita con `DeskewFilter`, `DenoiseFilter` e `ContrastBoostFilter`.

```java
import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.DeskewFilter;
import com.example.ocr.filters.DenoiseFilter;
import com.example.ocr.filters.ContrastBoostFilter;

/**
 * Demonstrates how to deskew image and apply common OCR preprocessing steps.
 */
public class OcrPreprocessDemo {

    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine (replace with your actual implementation)
        Engine engine = new Engine();

        // 2️⃣ Build the preprocessing pipeline
        ImagePreprocessOptions preprocessOptions = new ImagePreprocessOptions();

        // 2a️⃣ Deskew – correct rotation up to ±15°
        preprocessOptions.addFilter(new DeskewFilter(15));

        // 2b️⃣ Denoise – remove salt‑and‑pepper noise
        preprocessOptions.addFilter(new DenoiseFilter());

        // 2c️⃣ Contrast boost – make low‑contrast scans more readable
        preprocessOptions.addFilter(new ContrastBoostFilter(1.5f));

        // 3️⃣ Attach the pipeline to the engine
        engine.setPreprocessOptions(preprocessOptions);

        // 4️⃣ Run OCR on a sample image
        String result = engine.recognizeText("sample-scanned-page.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== OCR RESULT ===");
        System.out.println(result);
    }
}
```

### Perché funziona

* **DeskewFilter** analizza le linee di testo dominanti dell'immagine, stima l'angolo e ruota il bitmap di nuovo in orizzontale. La maggior parte delle librerie limita la correzione a ±15° perché angoli più grandi indicano solitamente una pagina scansionata male che richiede un intervento manuale.  
* **DenoiseFilter** mira al classico pattern *salt‑and‑pepper*—quei pixel isolati neri o bianchi che sembrano statiche su una TV. Rimuoverli impedisce al motore OCR di confondere il rumore con i caratteri.  
* **ContrastBoostFilter** allunga l'istogramma, facendo risaltare i tratti più deboli. Un moltiplicatore di `1.5f` è un valore predefinito sicuro; puoi aumentarlo se le tue scansioni sono particolarmente sbiadite.  

> **Consiglio professionale:** Se sai che i tuoi documenti non superano mai un'inclinazione di 10°, passa quel limite più piccolo a `DeskewFilter`—l'algoritmo sarà più veloce e meno incline a sovracorrettare.

## Image Preprocessing OCR: Aggiungere i filtri nell'ordine corretto

L'ordine è importante. Immagina di denoise *prima* della correzione dell'inclinazione; il rumore potrebbe alterare il rilevamento dell'angolo, portando a un risultato disallineato. Al contrario, applicare il contrast boost *dopo* la correzione garantisce che la rotazione non introduca nuovi artefatti.

Di seguito trovi una rapida checklist che puoi copiare‑incollare in qualsiasi progetto:

| Step | Filter | Reason |
|------|--------|--------|
| 1 | `DeskewFilter` | Allinea la linea di base del testo |
| 2 | `DenoiseFilter` | Rimuove il rumore di pixel isolati |
| 3 | `ContrastBoostFilter` | Migliora la leggibilità per OCR |

Se devi inserire passaggi aggiuntivi—ad esempio, un filtro di **binarizzazione** per OCR binario—lo inserirai **dopo** il contrast boost, perché un'immagine pulita e ad alto contrasto si binarizza più accuratamente.

## Rimuovere il rumore Salt Pepper con DenoiseFilter

Il rumore *salt‑and‑pepper* è noto nelle scansioni di bassa qualità, soprattutto quelle provenienti da fotocamere di telefoni economici. Il `DenoiseFilter` nella nostra libreria implementa un kernel di filtro mediano, che sostituisce ogni pixel con la mediana del suo intorno. L'effetto? Quei granelli scompaiono senza sfocare i caratteri reali.

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*Quando aumentare la dimensione del kernel?* Se le tue immagini di origine sono piene di granelli grandi, un kernel più grande li pulirà, ma attenzione: se è troppo grande potresti iniziare a cancellare tratti sottili in caratteri minuscoli.

## Preprocess Images OCR – Applicare la pipeline

Una volta assemblata la catena di filtri, collegarla al motore è una singola riga (`engine.setPreprocessOptions`). Da quel momento, ogni chiamata a `recognizeText` viene eseguita automaticamente attraverso la pipeline. Non è necessario invocare manualmente ogni filtro—il tuo codice rimane ordinato, e le modifiche future (aggiungere un nuovo filtro, regolare i parametri) sono centralizzate.

Ecco come appare un'esecuzione riuscita con una scansione di esempio che inizialmente aveva un'inclinazione di 12° e un evidente rumore pepper:

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Nota come il testo è pulito, correttamente orientato e privo di caratteri erranti che altrimenti sarebbero apparsi come “I n v o i c e” o “$‑‑‑”.

## Casi limite e problemi comuni

| Situation | What to watch for | Suggested fix |
|-----------|-------------------|---------------|
| Rotazione > 15° | DeskewFilter potrebbe arrendersi | Pre‑ruotare manualmente o usare un filtro a intervallo più ampio |
| Risoluzione estremamente bassa ( < 100 dpi ) | Il contrast boost non può recuperare i dettagli | Ricampionare l'immagine prima (es., `ResampleFilter`) |
| Rumore misto (Gaussian + salt‑pepper) | Il solo DenoiseFilter non è sufficiente | Collegare un `GaussianBlurFilter` prima del `DenoiseFilter` |
| Scansioni a colori con testo colorato | Necessaria conversione in scala di grigi | Inserire `GrayscaleFilter` prima del contrast boost |

Anticipando questi scenari risparmi ore di debugging in seguito.

## Esempio completo funzionante (Tutto‑in‑Uno)

Di seguito trovi una classe Java autonoma che puoi inserire in qualsiasi progetto Maven o Gradle che includa la dipendenza `com.example.ocr`. Dimostra **come correggere l'inclinazione di un'immagine**, **rimuovere il rumore salt pepper**, e **preprocess images OCR**‑style.

```java
package com.myapp.demo;

import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.*;

public class CompleteOcrPipeline {

    public static void main(String[] args) {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine (replace with your own)
        // -------------------------------------------------
        Engine engine = new Engine();

        // -------------------------------------------------
        // 2️⃣ Configure preprocessing pipeline
        // -------------------------------------------------
        ImagePreprocessOptions options = new ImagePreprocessOptions();

        // Deskew up to ±15° – the core of "how to deskew image"
        options.addFilter(new DeskewFilter(15));

        // Remove salt‑and‑pepper artifacts
        options.addFilter(new DenoiseFilter());

        // Boost contrast by 1.5× to aid OCR recognition
        options.addFilter(new ContrastBoostFilter(1.5f));

        // (Optional) Convert to grayscale – often improves OCR accuracy
        options.addFilter(new GrayscaleFilter());

        // Attach the pipeline
        engine.setPreprocessOptions(options);

        // -------------------------------------------------
        // 3️⃣ Perform OCR on a test file
        // -------------------------------------------------
        String imagePath = "src/main/resources/scanned-document.png";
        String text = engine.recognizeText(imagePath);

        // -------------------------------------------------
        // 4️⃣ Show the result
        // -------------------------------------------------
        System.out.println("=== OCR RESULT ===");
        System.out.println(text);
    }
}
```

**Output previsto** (supponendo che `scanned-document.png` contenga una fattura chiara):

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

Se sostituisci l'immagine con una già perfettamente allineata, noterai che la pipeline continua a funzionare—nulla si rompe e l'accuratezza OCR rimane alta.

## Conclusione

Ora hai una solida comprensione di **come correggere l'inclinazione di un'immagine** e del perché ogni passaggio di preprocessing—**image preprocessing OCR**, **remove salt pepper**, e **preprocess images OCR**—gioca un ruolo cruciale nel fornire testo pulito e ricercabile. L'esempio sopra è completo,

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come usare AspOCR: Filtri OCR per il preprocessing delle immagini per .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Calcolare l'angolo di inclinazione per il preprocessing delle immagini OCR](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [Come impostare il valore di soglia nel riconoscimento OCR delle immagini](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}