---
category: general
date: 2026-03-18
description: Come correggere rapidamente l'inclinazione di un'immagine usando Aspose
  OCR Java. Impara a preelaborare l'immagine per l'OCR, pulire l'immagine scansionata
  e migliorare la precisione dell'OCR in pochi semplici passaggi.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- clean scanned image
- improve ocr accuracy
language: it
og_description: Come correggere l'inclinazione di un'immagine con Aspose OCR Java,
  preelaborare l'immagine per l'OCR, pulire l'immagine scansionata e migliorare l'accuratezza
  dell'OCR.
og_title: Come raddrizzare l'immagine per OCR – Guida Java
tags:
- OCR
- Java
- Image Processing
title: Come raddrizzare l'immagine per OCR – Guida di pre‑elaborazione Java
url: /it/java/advanced-ocr-techniques/how-to-deskew-image-for-ocr-java-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come correggere l'inclinazione di un'immagine per OCR – Guida di pre‑processing Java

Ti sei mai chiesto **come correggere l'inclinazione di un'immagine** che esce dallo scanner con un angolo strano? Non sei l'unico—molti sviluppatori incontrano questo problema quando cercano di estrarre testo da documenti ricchi di immagini. La buona notizia? Con poche righe di Java e Aspose OCR puoi raddrizzare, ridurre il rumore e ottenere testo pulito senza sforzo.

In questo tutorial percorreremo l'intero flusso di lavoro: caricamento di una scansione rumorosa e ruotata, applicazione di un filtro di correzione dell'inclinazione, rimozione del disturbo visivo e, infine, **estrazione del testo dall'immagine**. Alla fine saprai **preprocessare l'immagine per OCR**, **pulire le immagini scansionate** e **migliorare l'accuratezza OCR** per qualsiasi progetto che richieda un'estrazione affidabile del testo.

## Cosa ti servirà

- Java 17 (o qualsiasi JDK recente) – il codice utilizza le funzionalità standard del linguaggio.  
- Libreria Aspose OCR per Java (la versione di prova gratuita è sufficiente per sperimentare).  
- Un'immagine di esempio che sia sia rumorosa sia ruotata (ad es., `noisy-rotated.png`).  
- Il tuo IDE preferito (IntelliJ IDEA, Eclipse, VS Code…) – qualsiasi cosa possa compilare Java.  

Nessun framework aggiuntivo, nessuna magia Maven/Gradle; le sole istruzioni `import` sono quelle mostrate di seguito.

---

## Come correggere l'inclinazione dell'immagine con Aspose OCR

La prima cosa da affrontare è l'inclinazione dell'immagine. Se le linee di testo non sono orizzontali, il motore OCR interpreterà erroneamente i caratteri. Il `DeskewFilter` fa il lavoro pesante.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;
import com.aspose.ocr.preprocess.DeskewFilter;
import com.aspose.ocr.preprocess.DenoiseFilter;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the raw scanned image
        Image scannedImage = Image.load("YOUR_DIRECTORY/noisy-rotated.png");

        // Step 3: Correct the image orientation (deskew)
        DeskewFilter deskewFilter = new DeskewFilter();
        scannedImage = deskewFilter.apply(scannedImage);

        // Step 4: Reduce visual noise (denoise)
        DenoiseFilter denoiseFilter = new DenoiseFilter();
        scannedImage = denoiseFilter.apply(scannedImage);

        // Step 5: Perform OCR on the cleaned image
        String recognizedText = ocrEngine.recognize(scannedImage);

        // Step 6: Output the extracted text
        System.out.println(recognizedText);
    }
}
```

> **Perché è importante:** Il `DeskewFilter` analizza la geometria dell'immagine, stima l'angolo di rotazione e ruota il bitmap fino a riportarlo su un orizzonte livellato. Senza questo passaggio la maggior parte dei motori OCR tratta le lettere inclinate come glifi completamente diversi, ostacolando i tuoi sforzi di **migliorare l'accuratezza OCR**.  
> 
> **Consiglio esperto:** Se devi gestire documenti che potrebbero essere capovolti, abilita il flag `setAutoRotate` sul `DeskewFilter` (disponibile nelle versioni più recenti di Aspose). Ruota automaticamente di 180° quando necessario.

![Diagramma che mostra prima e dopo la rotazione – come correggere l'inclinazione dell'immagine](https://example.com/deskew-diagram.png "esempio di come correggere l'inclinazione dell'immagine")

*Testo alternativo dell'immagine: esempio di come correggere l'inclinazione dell'immagine*

---

## Preprocessare l'immagine per OCR – Riduzione del rumore e pulizia

Una volta che l'immagine è dritta, il prossimo ostacolo è il rumore visivo—quei puntini, artefatti di compressione o pattern di sfondo tenue che confondono il motore OCR. Il `DenoiseFilter` applica un algoritmo di levigatura sottile che preserva i bordi (le lettere) mentre elimina la granulosità.

```java
// Step 4 (continued): Reduce visual noise (denoise)
DenoiseFilter denoiseFilter = new DenoiseFilter();
scannedImage = denoiseFilter.apply(scannedImage);
```

### Quando regolare le impostazioni di riduzione del rumore

- **Scansioni molto scure:** aumenta la potenza del filtro (`denoiseFilter.setStrength(2)`) per eliminare le ombre di sfondo.  
- **Font a stampa fine:** diminuisci la potenza per evitare di sfocare i piccoli serif.  
- **Documenti a colori:** converti prima in scala di grigi (`scannedImage = scannedImage.toGrayscale();`)—il motore OCR funziona al meglio su immagini a canale singolo.  

Queste regolazioni fanno parte delle migliori pratiche per **pulire le immagini scansionate**; un bitmap più pulito si traduce direttamente in punteggi di fiducia più alti dal motore OCR.

---

## Estrarre testo dall'immagine – Eseguire il motore OCR

Ora che la foto è dritta e priva di rumore, è il momento di **estrarre testo dall'immagine**. La classe `OcrEngine` gestisce tutto dietro le quinte: segmentazione, classificazione dei caratteri e modellazione linguistica.

```java
// Step 5: Perform OCR on the cleaned image
String recognizedText = ocrEngine.recognize(scannedImage);
System.out.println(recognizedText);
```

#### Output previsto

Se il tuo file di origine contiene la riga “**Invoice # 12345**”, la console dovrebbe stampare qualcosa di simile:

```
Invoice # 12345
Date: 2026-03-18
Total: $1,250.00
```

Se l'output appare confuso, ricontrolla i passaggi precedenti—soprattutto la correzione dell'inclinazione. Anche una rotazione di 1° può corrompere numeri e simboli.

---

## Problemi comuni e consigli per **migliorare l'accuratezza OCR**

| Problema | Perché influisce sull'accuratezza | Correzione rapida |
|----------|-----------------------------------|-------------------|
| **Rotazione residua** | OCR si aspetta linee di base orizzontali. | Verifica con `deskewFilter.getAngle()` e registra il valore. |
| **Eccessiva riduzione del rumore** | Sfuma tratti sottili, trasformando “i” in “l”. | Usa `setStrength(0.5)` per font delicati. |
| **Formato immagine errato** | La compressione JPEG aggiunge artefatti. | Preferisci PNG o TIFF per archiviazione senza perdita. |
| **Lingua errata** | Il motore predefinisce l'inglese; altri alfabeti richiedono impostazione esplicita. | `ocrEngine.setLanguage(OcrEngine.Language.Spanish);` |
| **Bassa risoluzione (≤150 DPI)** | Non ci sono abbastanza pixel per una segmentazione affidabile. | Ricampiona a 300 DPI prima della lavorazione (`scannedImage = scannedImage.resample(300);`). |

### Bonus: Elaborazione batch

Se hai una cartella di scansioni, avvolgi il demo in un ciclo:

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.endsWith(".png"))) {
    Image img = Image.load(file.getAbsolutePath());
    img = new DeskewFilter().apply(img);
    img = new DenoiseFilter().apply(img);
    String text = ocrEngine.recognize(img);
    System.out.println("=== " + file.getName() + " ===");
    System.out.println(text);
}
```

Questo modello ti consente di **preprocessare l'immagine per OCR** su larga scala, mantenendo il codice ordinato e le prestazioni prevedibili.

---

## Riepilogo e prossimi passi

Abbiamo coperto **come correggere l'inclinazione di un'immagine**, **preprocessare l'immagine per OCR** e infine **estrarre testo dall'immagine** usando Aspose OCR Java. Raddrizzando la scansione, pulendo il rumore e fornendo un bitmap impeccabile al motore, noterai un evidente **miglioramento dell'accuratezza OCR** in tutti i casi.

Cosa fare dopo? Considera queste estensioni:

- **Rilevamento della lingua** – cambia `ocrEngine.setLanguage` in base allo script rilevato.  
- **Output PDF** – inserisci il testo riconosciuto in un generatore PDF per documenti ricercabili.  
- **Post‑processing con machine‑learning** – esegui il controllo ortografico o dizionari personalizzati sul risultato OCR.  

Prova queste idee, sperimenta con diverse intensità dei filtri e avrai presto una pipeline solida per qualsiasi progetto di digitalizzazione documentale.

*Buon coding! Se incontri un problema, lascia un commento qui sotto—ti aiuterò a perfezionare i parametri di correzione dell'inclinazione e di riduzione del rumore.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}