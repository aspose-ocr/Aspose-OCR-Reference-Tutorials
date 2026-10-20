---
category: general
date: 2026-03-28
description: Esegui OCR su un'immagine in Java usando Aspose OCR per convertire l'immagine
  in testo, estrai il testo tailandese da PNG in modo rapido e affidabile.
draft: false
keywords:
- run OCR on image
- convert image to text
- extract text from PNG
- extract Thai text
- recognize Thai text
language: it
og_description: Esegui OCR su un'immagine usando Java e Aspose OCR. Scopri come convertire
  l'immagine in testo, estrarre testo tailandese da PNG e gestire le insidie comuni.
og_title: Esegui OCR su un'immagine con Java – Estrai rapidamente il testo tailandese
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Esegui OCR su immagine con Java – Estrai testo tailandese da PNG
url: /it/java/ocr-operations/run-ocr-on-image-with-java-extract-thai-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine con Java – Tutorial Completo

Ti sei mai chiesto come **eseguire OCR su immagine** direttamente dal codice Java? Forse hai una collezione di ricevute tailandesi, documenti scannerizzati o screenshot e ti serve il testo senza doverlo digitare manualmente. È un problema comune, soprattutto quando la sorgente è un PNG e la lingua non è latina.  

In questa guida ti mostreremo esattamente come **eseguire OCR su immagine** usando la libreria Aspose OCR, convertire l'immagine in testo semplice e estrarre i caratteri tailandesi in modo affidabile. Alla fine sarai in grado di **convertire immagine in testo**, **estrarre testo da PNG** e persino **riconoscere testo tailandese** con poche righe di codice.

## Cosa Copre Questo Tutorial

* Impostare la dipendenza Aspose OCR in un progetto Maven/Gradle.  
* Inizializzare il `OcrEngine` e configurarlo per la lingua tailandese.  
* Eseguire OCR su un file PNG e gestire eventuali errori.  
* Stampare il risultato sulla console e verificare l'output.  

Non è necessaria alcuna esperienza pregressa con Aspose—basta un IDE Java di base e un file immagine che desideri elaborare.

## Prerequisiti

* Java 8 o versioni successive installate (la libreria funziona anche con Java 11+).  
* Uno strumento di build – Maven o Gradle (mostreremo lo snippet Maven).  
* Una licenza Aspose OCR (la versione di prova gratuita è valida per i test, ma una licenza rimuove i limiti di valutazione).  
* Un PNG che contiene testo tailandese, ad esempio `input.png` posizionato nella cartella resources del tuo progetto.

---

## Passo 1: Aggiungi Aspose OCR al Tuo Progetto

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version -->
</dependency>
```

### Gradle (Kotlin DSL)

```kotlin
implementation("com.aspose:aspose-ocr:23.9")
```

> **Consiglio:** Mantieni la versione della libreria sincronizzata con le note di rilascio ufficiali di Aspose; le versioni più recenti aggiungono pacchetti linguistici e ottimizzazioni delle prestazioni.

Una volta risolta la dipendenza, il tuo IDE dovrebbe importare automaticamente le classi necessarie.

## Passo 2: Inizializza il Motore OCR

Il motore è il cuore del processo – pensalo come il “cervello” che analizza i pattern dei pixel. Indicheremo inoltre che ci interessano solo i caratteri tailandesi.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Tell the engine to look for Thai language patterns
        ocrEngine.getRecognitionSettings().setLanguage("th");
```

Perché impostare esplicitamente la lingua? Perché specificare `"th"` restringe il set di caratteri, velocizzando il riconoscimento e riducendo gli errori di lettura di glifi simili.

## Passo 3: Esegui OCR sul File PNG

Ora forniamo al motore l'immagine che vogliamo decodificare. Il metodo `recognizeImage` restituisce un oggetto `OcrResult` che contiene la stringa estratta e i punteggi di confidenza.

```java
        // Step 3: Perform OCR on the target image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

Se il file non viene trovato, Aspose genera una `FileNotFoundException`. È consigliabile avvolgere la chiamata in un blocco `try‑catch` per il codice di produzione, ma per questo tutorial lo manterremo semplice.

## Passo 4: Output del Testo Riconosciuto

Infine, stampiamo il risultato. Il metodo `getText()` restituisce una semplice `String` Java che puoi memorizzare, inviare su una rete o scrivere su un file.

```java
        // Step 4: Display the extracted Thai text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Quando esegui il programma, dovresti vedere qualcosa di simile:

```
=== Recognized Thai Text ===
สวัสดีครับ นี่คือข้อความจากรูปภาพ
```

Se l'output appare confuso, verifica che il PNG di origine sia ad alta risoluzione (almeno 300 dpi) e che il codice lingua `"th"` corrisponda alla lingua di destinazione.

### Listing Completo

Di seguito trovi il file Java completo, pronto per l'esecuzione. Copialo e incollalo nel tuo IDE, sostituisci il percorso dell'immagine se necessario e premi **Run**.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Select Thai language for recognition
        ocrEngine.getRecognitionSettings().setLanguage("th");

        // Run OCR on the PNG image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // Output the recognized text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

![esempio di esecuzione OCR su immagine](image.png "esempio di esecuzione OCR su immagine – codice Java che estrae testo tailandese da PNG")

## Passo 5: Variazioni Comuni & Casi Limite

### Convertire Immagine in Testo in Altri Formati

Se hai bisogno di **convertire immagine in testo** per un JPEG o BMP, basta cambiare l'estensione del file in `imagePath`. Aspose OCR supporta PNG, JPEG, BMP, TIFF e persino pagine PDF.

### Estrarre Testo da PNG con più Lingue

Puoi chiedere al motore di rilevare più lingue contemporaneamente:

```java
ocrEngine.getRecognitionSettings().setLanguage("th,en");
```

Il risultato conterrà un mix di caratteri tailandesi e inglesi, utile per ricevute bilingue.

### Gestire Immagini a Bassa Qualità

Per scansioni sfocate, considera l'abilitazione del preprocessing:

```java
ocrEngine.getRecognitionSettings().setPreprocessMode(PreprocessMode.Auto);
```

Questo attiva gli algoritmi integrati di riduzione del rumore e miglioramento del contrasto, migliorando il passo di **estrarre testo da PNG**.

### Attivazione Licenza

Senza licenza, Aspose inserisce una linea di filigrana nell'output dopo 100 pagine. Attiva la tua licenza subito:

```java
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

Posiziona il file `.lic` accanto al tuo JAR o riferiscilo tramite un percorso assoluto.

## Domande Frequenti

**Q: Funziona su Linux?**  
A: Assolutamente. Aspose OCR è puro Java, quindi qualsiasi OS compatibile con JVM va bene.

**Q: E se il PNG contiene Thai scritto a mano?**  
A: Il riconoscimento della scrittura a mano è limitato; potresti aver bisogno di un modello di rete neurale dedicato. Aspose OCR eccelle con testo stampato.

**Q: Posso elaborare in batch una cartella di immagini?**  
A: Avvolgi la chiamata `recognizeImage` in un ciclo su `Files.list(Paths.get("folder"))`. Ricorda di riutilizzare la stessa istanza di `OcrEngine` per le prestazioni.

## Conclusione

Abbiamo illustrato un esempio completo, end‑to‑end, di come **eseguire OCR su immagine** in Java, specificamente per **estrarre testo tailandese** da un PNG. Inizializzando il `OcrEngine`, impostando la lingua, invocando `recognizeImage` e stampando il risultato, ora disponi di un metodo affidabile per **convertire immagine in testo** senza servizi di terze parti.

Da qui potresti:

* **estrarre testo da PNG** file in massa per progetti di data‑mining.  
* Combinare l'output OCR con un'API di traduzione per ottenere equivalenti in inglese.  
* Esplorare altre lingue supportate da Aspose, come Cinese o Arabo, cambiando il codice lingua.

Provalo con le tue immagini—regola le impostazioni di preprocessing, sperimenta con diversi formati di file e osserva quanto la soluzione sia robusta nel tuo flusso di lavoro reale.

Buon coding, e che le tue pipeline OCR siano sempre accurate!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}