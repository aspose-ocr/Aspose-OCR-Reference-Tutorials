---
category: general
date: 2026-06-06
description: come eseguire OCR in Java – estrarre rapidamente il testo da un'immagine,
  convertire l'immagine in testo e leggere il testo da un jpg usando un semplice esempio
  di codice.
draft: false
keywords:
- how to perform OCR
- ocr in java
- extract text from image
- convert image to text
- read text from jpg
language: it
og_description: come eseguire OCR in Java – impara come estrarre testo da un'immagine,
  convertire l'immagine in testo e leggere il testo da un jpg con un esempio pronto
  all'uso.
og_title: Come eseguire l'OCR in Java – Guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  headline: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  type: TechArticle
- description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  name: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  steps:
  - name: What You’ll Learn
    text: '- Install an OCR library (yes, **ocr in java** is easier than you think).
      - Create and configure an OCR engine instance. - Load a JPG (or any image) and
      set the language. - Process the image and **extract text from image** files.
      - Print the recognized string to the console.'
  - name: Expected Output
    text: 'If `input.jpg` contains the Mongolian phrase “Сайн байна уу?” the console
      will show:'
  - name: 'Pro Tip: Batch Processing'
    text: 'If you need to **extract text from image** files in bulk, wrap the core
      logic in a loop:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Come eseguire OCR in Java – Guida completa per estrarre testo dalle immagini
url: /it/java/ocr-basics/how-to-perform-ocr-in-java-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR in Java – Guida completa per estrarre testo dalle immagini

Ti sei mai chiesto **come eseguire OCR** su una foto scattata con il tuo telefono? Non sei il solo. Che tu stia creando un'app per la scansione di ricevute o abbia semplicemente bisogno di estrarre testo da un PDF scansionato, **come eseguire OCR** in Java è una competenza che ripaga rapidamente. In questo tutorial percorreremo un esempio pratico che **estrae testo da file immagine**, **converte immagine in testo**, e mostra anche come **leggere testo da jpg** con poche righe di codice.

> *Suggerimento professionale:* Lo stesso approccio funziona per PNG, BMP o qualsiasi formato supportato dal motore OCR—basta cambiare il nome del file.

## Come eseguire OCR in Java – Panoramica

Il riconoscimento ottico dei caratteri (OCR) è la tecnologia che trasforma le immagini di lettere in testo reale e ricercabile. Nell'ecosistema Java esistono diverse librerie—Tesseract, Asprise e SDK commerciali—che espongono un flusso di lavoro simile: caricare un'immagine, indicare al motore la lingua prevista, eseguire il riconoscimento e ottenere il risultato. Di seguito useremo una classe generica `OcrEngine` per mantenere l'esempio chiaro, ma puoi sostituirla con qualsiasi implementazione concreta che segua lo stesso schema.

### Cosa imparerai

- Installa una libreria OCR (sì, **ocr in java** è più facile di quanto pensi).
- Crea e configura un'istanza del motore OCR.
- Carica un JPG (o qualsiasi immagine) e imposta la lingua.
- Elabora l'immagine e **estrarre testo da immagine**.
- Stampa la stringa riconosciuta sulla console.

Alla fine avrai un programma Java autonomo che potrai inserire in qualsiasi progetto e eseguire immediatamente.

![esempio di come eseguire OCR](ocr-example.png "illustrazione di come eseguire OCR in Java")

## Passo 1 – Installa e importa una libreria OCR (ocr in java)

Prima di scrivere una sola riga di Java, ti serve una libreria che faccia effettivamente il lavoro pesante. Se usi Maven, aggiungi una dipendenza come questa (sostituisci `com.example.ocr` con il vero group ID del SDK scelto):

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>1.4.2</version>
</dependency>
```

Se preferisci Gradle:

```gradle
implementation 'com.example:ocr-sdk:1.4.2'
```

Una volta che il JAR è nel tuo classpath, importa le classi di cui avrai bisogno:

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;
```

> **Perché è importante:** Importare le classi corrette evita errori “cannot find symbol” e rende felice il tuo IDE—nulla è più frustrante di un import mancante quando stai cercando di **convertire immagine in testo**.

## Passo 2 – Crea l'istanza del motore OCR (come eseguire OCR)

Ora che la libreria è pronta, avvia il motore. Considera il motore come il cervello che guarderà i pixel e indovinerà le lettere.

```java
// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

Creare il motore è solitamente poco costoso; la maggior parte degli SDK alloca buffer interni in modo pigro, così puoi riutilizzare in sicurezza la stessa istanza per molte immagini se stai elaborando un batch.

## Passo 3 – Carica l'immagine e imposta la lingua (estrarre testo da immagine)

Il passo successivo è fornire al motore qualcosa da leggere. Qui carichiamo un JPEG dal disco e indichiamo al motore OCR che il testo è in mongolo (codice ISO 639‑2 “mon”). Puoi modificare il percorso o il codice lingua per adattarlo al tuo caso d'uso.

```java
// Step 3: Load the image you want to recognize
ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/input.jpg"));

// Step 3b: Specify the language (e.g., English = "eng", Mongolian = "mon")
ocrEngine.getSettings().setLanguage("mon");
```

> **Nota a margine:** Se non imposti una lingua, il motore usa per default l'inglese, il che può ridurre drasticamente l'accuratezza quando il testo è in realtà cirillico o in un altro script. Specifica sempre la lingua corretta quando puoi.

## Passo 4 – Elabora l'immagine e ottieni il risultato (convertire immagine in testo)

Con l'immagine e la lingua impostate, chiedi al motore di fare la sua magia. La chiamata `process()` esegue l'algoritmo OCR e restituisce un oggetto `OcrResult` contenente la stringa riconosciuta e i punteggi di confidenza.

```java
// Step 4: Process the image and obtain the recognition result
OcrResult ocrResult = ocrEngine.process();
```

Dietro le quinte, il motore può eseguire pre‑elaborazione—raddrizzamento, binarizzazione, riduzione del rumore—così non devi scrivere questi passaggi tu stesso. Ecco perché la maggior parte delle librerie OCR moderne è un piacere da usare per attività di **convertire immagine in testo**.

## Passo 5 – Output del testo estratto (leggere testo da jpg)

Infine, estrai il testo semplice dal risultato e fai qualcosa di utile con esso. Per questa demo lo stampiamo semplicemente sulla console, ma potresti scriverlo su un file, inviarlo a un indice di ricerca o passarne a un altro servizio.

```java
// Step 5: Output the extracted text
System.out.println(ocrResult.getText());
```

Quella riga dimostra da sola che hai **letto testo da jpg** (o qualsiasi formato supportato) con successo. Se l'output appare confuso, ricontrolla il codice lingua e la qualità dell'immagine.

## Esempio completo funzionante (tutti i passi combinati)

Di seguito trovi una classe Java completa, pronta per l'esecuzione, che collega tutti i componenti. Copiala in un file chiamato `OcrDemo.java`, regola il percorso dell'immagine e la lingua, quindi esegui `javac OcrDemo.java && java OcrDemo`.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to perform OCR in Java using a generic OCR SDK.
 * This example loads a JPG, sets the language to Mongolian, and prints
 * the recognized text to the console.
 *
 * Replace the import package with the actual library you are using.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Validate command‑line arguments
        if (args.length < 2) {
            System.err.println("Usage: java OcrDemo <image-path> <language-code>");
            System.exit(1);
        }

        String imagePath = args[0];   // e.g., "input.jpg"
        String language = args[1];    // e.g., "mon" for Mongolian

        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image
        ocrEngine.setImage(new OcrInputImage(imagePath));

        // Step 3: Set the language (ISO‑639‑2)
        ocrEngine.getSettings().setLanguage(language);

        // Step 4: Run the recognition
        OcrResult result = ocrEngine.process();

        // Step 5: Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### Output previsto

Se `input.jpg` contiene la frase mongola “Сайн байна уу?” la console mostrerà:

```
=== Recognized Text ===
Сайн байна уу?
```

Se l'immagine è sfocata o il codice lingua è errato, vedrai caratteri confusi o una stringa vuota—problemi comuni che discuteremo subito dopo.

## Problemi comuni e come risolverli

| Sintomo | Causa probabile | Risoluzione |
|---------|-----------------|-------------|
| Caratteri cirillici confusi | Codice lingua errato (default a inglese) | Imposta `ocrEngine.getSettings().setLanguage("mon")` o il codice appropriato. |
| Nessun output | Percorso immagine errato o file illeggibile | Verifica il percorso, assicurati che il file esista e che il processo abbia i permessi di lettura. |
| Bassa accuratezza (<70 %) | L'immagine ha basso contrasto o è ruotata | Pre‑elabora l'immagine: aumenta il contrasto, raddrizza o converti in scala di grigi prima di passarla al motore. |
| `OutOfMemoryError` su PDF grandi | Caricamento di molte pagine ad alta risoluzione contemporaneamente | Elabora le pagine una alla volta, o ridimensiona le immagini prima dell'OCR. |

### Suggerimento professionale: Elaborazione batch

Se hai bisogno di **estrarre testo da immagine** file in blocco, avvolgi la logica principale in un ciclo:

```java
for (File img : new File("batchFolder").listFiles()) {
    ocrEngine.setImage(new OcrInputImage(img.getAbsolutePath()));
    OcrResult r = ocrEngine.process();
    System.out.println(r.getText());
}
```

## Approfondimenti – Cosa esplorare dopo?

- **Language Packs:** La maggior parte degli SDK OCR ti permette di scaricare file di dati lingua aggiuntivi. Aggiungere un nuovo pacchetto ti consente di **convertire immagine in testo** per lingue oltre l'inglese e il mongolo.
- **PDF OCR:** Combina questo codice con Apache PDFBox per

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrarre testo da immagini – Nozioni di base OCR con Aspose.OCR per Java](/ocr/english/java/ocr-basics/)
- [Convertire immagine in testo in Java usando Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Come fare OCR su testo immagine con lingua usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}