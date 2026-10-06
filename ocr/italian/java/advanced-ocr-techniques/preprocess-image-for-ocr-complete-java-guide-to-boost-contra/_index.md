---
category: general
date: 2026-02-17
description: Preprocessa l'immagine per OCR con Aspose OCR in Java. Impara a aumentare
  il contrasto dell'immagine, impostare il livello di contrasto e riconoscere il testo
  dall'immagine in pochi minuti.
draft: false
keywords:
- preprocess image for ocr
- boost image contrast
- recognize text from image
- extract text using OCR
- set contrast level
language: it
og_description: Preprocessa l'immagine per OCR usando Aspose OCR Java. Questa guida
  mostra come aumentare il contrasto dell'immagine, impostare il livello di contrasto
  e riconoscere rapidamente il testo dall'immagine.
og_title: Preelaborazione dell'immagine per OCR – Tutorial Java per aumentare il contrasto
  ed estrarre il testo
tags:
- Java
- OCR
- Image Processing
title: Preprocessare l'immagine per OCR – Guida completa Java per aumentare il contrasto
  ed estrarre il testo
url: /it/java/advanced-ocr-techniques/preprocess-image-for-ocr-complete-java-guide-to-boost-contra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Preprocess Image for OCR – Guida Completa Java

Ti è mai capitato di dover **preprocessare un'immagine per OCR** senza sapere quali impostazioni fanno davvero la differenza? Non sei solo. La maggior parte degli sviluppatori lancia un'immagine a un motore OCR sperando che la magia accada, per poi ottenere un output incomprensibile. In questo tutorial percorreremo un esempio pratico, end‑to‑end, che **aumenta il contrasto dell'immagine**, regola il **livello di contrasto**, e infine **riconosce il testo dall'immagine** usando Aspose OCR per Java.

Al termine avrai uno snippet di codice riutilizzabile che **estrae testo usando OCR** in modo affidabile, anche su scansioni rumorose. Nessun trucco nascosto, solo passaggi chiari e la logica dietro ciascuno.

## Cosa Ti Serve

- Java 17 o versioni successive (il codice compila con qualsiasi JDK recente)
- Libreria Aspose OCR per Java (scaricabile dal sito ufficiale Aspose)
- Un file di licenza Aspose OCR valido (`Aspose.OCR.lic`)
- Un'immagine di input (`input.jpg`) che desideri leggere
- Un IDE preferito o una semplice configurazione da riga di comando

Se hai già tutto, ottimo—tuffiamoci subito.

## Passo 1: Carica la Licenza Aspose OCR (Configurazione Principale)

Prima che il motore OCR faccia qualsiasi cosa, deve sapere che sei in possesso di una licenza. Altrimenti otterrai una filigrana di prova.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {

        // Load the Aspose OCR license – this disables the evaluation limits
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Perché è importante:** Senza una licenza corretta, il motore gira in modalità valutazione, il che può troncare i risultati o aggiungere filigrane. Impostare la licenza subito garantisce che tutte le opzioni di pre‑elaborazione successive vengano applicate in modalità completa.

## Passo 2: Inizializza il Motore OCR

Creare un'istanza di `OcrEngine` ti dà accesso sia al riconoscimento sia alle pipeline di pre‑elaborazione.

```java
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Consiglio professionale:** Mantieni il motore come singleton se prevedi di elaborare molte immagini in batch; così cache le risorse interne e velocizza le chiamate successive.

## Passo 3: Configura la Pre‑elaborazione – Deskew, Denoise e Potenziamento del Contrasto

Qui è dove **preprocessiamo l'immagine per OCR**. I tre parametri che regoleremo sono:

1. **Deskew** – corregge rotazioni leggere.
2. **Denoise** – rimuove i granelli che confondono la segmentazione dei caratteri.
3. **Potenzia il contrasto** – rende il testo scuro più evidente rispetto allo sfondo.

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

### Perché Regolare il Livello di Contrasto?

Aumentare il livello di contrasto allunga l'istogramma dell'immagine, rendendo i pixel scuri più scuri e quelli chiari più luminosi. In pratica, un **livello di contrasto** di `1.3f` spesso offre il miglior equilibrio per documenti stampati, mentre un valore superiore a `1.5f` può sovra‑esporre tratti sottili. Sentiti libero di sperimentare; la modifica è poco costosa e può migliorare drasticamente il tasso di successo del **recognize text from image**.

## Passo 4: Prepara l'Immagine di Input

La classe `OcrInput` astrae la gestione dei file. Puoi aggiungere più immagini se ti serve un'elaborazione batch.

```java
        // Prepare the image for OCR – you can add more files to the same OcrInput
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.jpg");
```

**Caso limite:** Se la tua immagine è in un formato non standard (ad es., TIFF con più pagine), puoi caricare ogni pagina separatamente o convertirla prima in PNG/JPEG.

## Passo 5: Esegui il Riconoscimento

Ora il motore esegue la pipeline di pre‑elaborazione che abbiamo configurato, poi passa l'immagine pulita all'algoritmo OCR core.

```java
        // Run OCR – this returns a result object containing the extracted text
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Cosa succede dietro le quinte?** Aspose OCR applica prima la trasformazione deskew, poi il filtro denoise, e infine regola il contrasto prima di inviare l'immagine al suo riconoscitore basato su rete neurale. L'ordine è intenzionale; cambiarlo potrebbe portare a risultati sub‑ottimali.

## Passo 6: Output del Testo Riconosciuto

Infine, stampiamo la stringa estratta sulla console. In un'applicazione reale potresti scriverla su un file o inviarla su rete.

```java
        // Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

### Output Atteso

Se `input.jpg` contiene la frase “Hello World!”, la console dovrebbe mostrare:

```
Hello World!
```

Se l'output appare confuso, ricontrolla i valori di pre‑elaborazione—soprattutto il **livello di contrasto** e la **modalità denoise**—e prova un formato immagine diverso.

## Bonus: Visualizzare l'Immagine Pre‑elaborata (Opzionale)

A volte vuoi vedere cosa vede il motore dopo deskew, denoise e potenziamento del contrasto. Aspose OCR ti permette di esportare il bitmap intermedio:

```java
        // Export the pre‑processed image for debugging
        BufferedImage processed = preprocessing.getProcessedImage();
        ImageIO.write(processed, "png", new File("processed.png"));
```

Apri `processed.png` fianco a fianco con l'originale; noterai un orizzonte più dritto e testo più nitido. Questo passaggio è utile quando devi capire perché una scansione specifica fallisce.

![esempio di pre‑elaborazione immagine per OCR](/images/ocr-preprocess-example.png "pre‑elaborazione immagine per OCR – prima e dopo il potenziamento del contrasto")

*L'immagine sopra illustra come aumentare il contrasto e rimuovere il rumore trasformi una scansione sfocata in una foto pulita, pronta per l'OCR.*

## Problemi Comuni & Come Evitarli

| Problema | Perché Accade | Soluzione |
|----------|----------------|-----------|
| **Contrasto eccessivo** (`setContrastLevel` troppo alto) | Lo sfondo chiaro diventa bianco, cancellando i caratteri deboli | Mantieni il livello tra 1.1 e 1.4 per la maggior parte dei testi stampati |
| **Tolleranza deskew troppo bassa** | Piccole rotazioni rimangono non corrette | Aumenta `setDeskewAngleTolerance` a 0.2 o 0.3 per libri scansionati |
| **Uso di denoise GAUSSIAN su immagini binarie** | Sfuma i bordi, unendo i caratteri | Usa `DenoiseMode.MEDIAN` per scansioni in bianco‑e‑nero |
| **Licenza mancante** | Il motore ricade in modalità trial, troncando l'output | Verifica il percorso verso `Aspose.OCR.lic` e che il file sia leggibile |

## Prossimi Passi: Oltre la Pre‑elaborazione Base

Ora che sai **preprocessare un'immagine per OCR** e **estrarre testo usando OCR**, considera queste estensioni:

- **Language packs** – carica dizionari specifici per lingua per migliorare l'accuratezza su testi non inglesi.
- **Region‑of‑interest (ROI) cropping** – concentra l'elaborazione su una sotto‑sezione dell'immagine se ti serve solo una parte della pagina.
- **Elaborazione batch** – itera su una cartella di immagini, riutilizzando la stessa istanza di `OcrEngine` per velocizzare.
- **Integrazione con PDF** – combina Aspose OCR con Aspose PDF per convertire PDF scansionati in PDF ricercabili in un'unica pipeline.

Ognuno di questi argomenti incorpora naturalmente le nostre parole chiave secondarie: continuerai a **boost image contrast**, **set contrast level**, e a **recognize text from image** in molti scenari.

## Conclusione

Abbiamo coperto tutto ciò che serve per **preprocessare un'immagine per OCR** usando Aspose OCR per Java: caricamento della licenza, configurazione di deskew, denoise e potenziamento del contrasto, caricamento dell'immagine e infine **riconoscimento del testo dall'immagine**. Con l'esempio completo e funzionante sopra, ora puoi **estrarre testo usando OCR** su qualsiasi immagine adeguatamente preparata.

Prova il codice, modifica il **livello di contrasto**, e osserva l'aumento di precisione. Quando sei pronto, esplora modelli specifici per lingua o pipeline batch per trasformare questa demo a immagine singola in una soluzione di livello produzione.

*Buon coding, e che le tue scansioni siano sempre nitide!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}