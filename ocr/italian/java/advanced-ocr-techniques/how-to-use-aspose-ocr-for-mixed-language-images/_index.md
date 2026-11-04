---
category: general
date: 2026-05-06
description: Come utilizzare Aspose OCR per riconoscere il testo da un'immagine, abilitare
  il rilevamento automatico della lingua e migliorare la velocità OCR in Java.
draft: false
keywords:
- how to use aspose
- recognize text from image
- improve ocr speed
- load image for ocr
- enable automatic language detection
language: it
og_description: Come utilizzare Aspose OCR per riconoscere rapidamente il testo da
  un'immagine, abilitare il rilevamento automatico della lingua e migliorare la velocità
  OCR in Java.
og_title: Come utilizzare Aspose OCR per immagini multilingue
tags:
- Aspose
- OCR
- Java
- Image Processing
title: Come utilizzare Aspose OCR per immagini multilingue
url: /it/java/advanced-ocr-techniques/how-to-use-aspose-ocr-for-mixed-language-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come utilizzare Aspose OCR per immagini multilingue

Ti sei mai chiesto **come usare Aspose** per estrarre testo da un'immagine che contiene più lingue contemporaneamente? Non sei solo—gli sviluppatori spesso si trovano di fronte a un ostacolo quando un'immagine mescola inglese, russo, hindi o qualsiasi altro script. La buona notizia è che Aspose OCR gestisce tutto ciò in modo fluido, e puoi persino **riconoscere testo da immagine** più velocemente restringendo il set di lingue.

In questo tutorial percorreremo un esempio Java completo, pronto per l'esecuzione, che **carica immagine per OCR**, attiva il **rilevamento automatico della lingua** e mostra un trucco semplice per **migliorare la velocità OCR**. Alla fine avrai un programma autonomo che stampa il testo estratto sulla console e comprenderai perché ogni impostazione è importante.

> **Prerequisiti** – Java 17+ installato, Maven o Gradle per la gestione delle dipendenze e una licenza Aspose OCR (la versione di prova gratuita è sufficiente per la valutazione). Non sono richieste altre librerie.

---

## Passo 1 – Aggiungi Aspose OCR al tuo progetto

Prima di poter **usare Aspose**, è necessario avere la libreria nel classpath. Con Maven appare così:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

Se preferisci Gradle:

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** Rimani sulla versione stabile più recente; le versioni più nuove includono spesso miglioramenti delle prestazioni che influenzano direttamente **migliorare la velocità OCR**.

---

## Passo 2 – Crea l'istanza del motore OCR  

Il cuore di ogni flusso di lavoro Aspose OCR è il `OcrEngine`. Istanziare il motore è semplice, ma vale la pena notare che esso mantiene cache interne. Riutilizzare una singola istanza per molte immagini può effettivamente **migliorare la velocità OCR** perché la libreria evita ripetute inizializzazioni native.

```java
import com.aspose.ocr.*;

public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialise the OCR engine – one instance per application is ideal
        OcrEngine ocrEngine = new OcrEngine();
```

---

## Passo 3 – **Carica immagine per OCR**  

Aspose accetta molti formati immagine (PNG, JPEG, TIFF, BMP). Qui dimostriamo il caricamento di un PNG che contiene testo in inglese, russo e hindi. L'helper `ImageStream.fromFile` astrae i dettagli di I/O dei file e garantisce che l'immagine venga correttamente trasmessa al motore.

```java
        // Step 3: Load the picture that holds mixed languages
        // Replace the path with the actual location of your image file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));
```

> **E se l'immagine è in memoria?** Usa `ImageStream.fromByteArray(byte[])` invece—perfetto per i servizi web che ricevono immagini come flussi di byte.

---

## Passo 4 – Abilita il rilevamento automatico della lingua  

Per impostazione predefinita Aspose OCR assume una sola lingua, il che può portare a output illeggibile su immagini multilingue. Attivare il rilevamento automatico indica al motore di individuare lo script di ogni blocco di testo prima del riconoscimento.

```java
        // Step 4: Turn on auto‑detect – this is the key to handling mixed‑language images
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

---

## Passo 5 – **Migliora la velocità OCR** limitando il pool di lingue  

Il rilevamento automatico completo analizza tutte le lingue supportate da Aspose (oltre 70). Se conosci in anticipo le possibili lingue, puoi fornire al motore un suggerimento. Fornire un array più piccolo riduce lo spazio di ricerca e quindi **migliora la velocità OCR**.

```java
        // Step 5 (optional but recommended): Limit detection to known languages
        // "en" = English, "ru" = Russian, "hi" = Hindi
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });
```

> **Perché questo aiuta?** Il motore salta i modelli linguistici non necessari, risparmiando cicli CPU e memoria. Se in seguito aggiungi altre lingue, basta aggiornare l'array—non è necessario riscrivere il codice.

---

## Passo 6 – Esegui il riconoscimento e **Riconosci testo da immagine**

Ora avviene il lavoro pesante. `recognize()` restituisce un oggetto `OcrResult` che contiene il testo semplice, i punteggi di confidenza e persino le informazioni di layout se ti servono in seguito.

```java
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 7: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Output previsto sulla console

```
=== Extracted Text ===
Hello world!
Привет мир!
नमस्ते दुनिया!
```

Se l'immagine contiene rumore aggiuntivo o testo inclinato, potresti vedere una confidenza più bassa per quelle righe. In tal caso, considera il pre‑processing dell'immagine (deskew, binarizzazione) prima di passarla ad Aspose.

---

## Domande comuni e casi limite

### E se l'immagine è enorme (ad es., >10 MP)?

Le immagini di grandi dimensioni consumano più memoria e possono rallentare l'elaborazione. Un modo rapido per **migliorare la velocità OCR** è ridimensionare l'immagine mantenendo la leggibilità:

```java
// Example using java.awt for simple resizing (optional)
BufferedImage original = ImageIO.read(new File("large.png"));
int targetWidth = 2000; // adjust based on your needs
BufferedImage resized = new BufferedImage(targetWidth,
        (original.getHeight() * targetWidth) / original.getWidth(),
        BufferedImage.TYPE_INT_RGB);
Graphics2D g = resized.createGraphics();
g.drawImage(original, 0, 0, targetWidth, resized.getHeight(), null);
g.dispose();
ocrEngine.setImage(ImageStream.fromImage(resized));
```

### Come gestire script da destra a sinistra come l'arabo?

Aspose OCR rispetta automaticamente la direzione dello script, ma potresti voler impostare il flag `RightToLeft` per il post‑processing:

```java
ocrEngine.getSettings().setRightToLeft(true);
```

### Posso estrarre testo da PDF invece che da immagini?

Sì—converti ogni pagina PDF in un'immagine (usando Aspose PDF o qualsiasi rasterizzatore) e passa il risultato allo stesso pipeline OCR. Si applica la stessa logica di **riconoscere testo da immagine**.

---

## Esempio completo funzionante (pronto per copia‑incolla)

```java
import com.aspose.ocr.*;
import java.io.File;

/**
 * Demonstrates how to use Aspose OCR to recognize text from an image
 * that contains multiple languages, with automatic language detection
 * and a speed‑optimising language whitelist.
 */
public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine – reuse this instance for many images
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that holds mixed languages (replace with your path)
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));

        // Enable automatic detection of language per text block
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // OPTIONAL: Restrict detection to English, Russian, and Hindi to boost speed
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });

        // Run OCR and capture the result
        OcrResult ocrResult = ocrEngine.recognize();

        // Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Salva il file come `MixedLanguageDemo.java`, compila con `javac` e avvia con `java MixedLanguageDemo`. Se tutto è configurato correttamente, vedrai il testo multilingue stampato sulla console.

---

## Conclusione

Ora sai **come usare Aspose** per **riconoscere testo da immagine** contenenti diverse lingue, come **abilitare il rilevamento automatico della lingua** e un suggerimento pratico per **migliorare la velocità OCR** limitando il pool di lingue. Il codice completo sopra è pronto per copia‑incolla, e le spiegazioni dovrebbero darti la fiducia necessaria per adattare la soluzione—sia che tu debba **caricare immagine per OCR** da uno stream, da un array di byte o anche da uno snapshot di webcam.

Prossimi passi? Prova a sperimentare con:

* Aggiungere pre‑processing dell'immagine (denoise, binarize) per scansioni di bassa qualità.  
* Esportare `OcrResult` come JSON per servizi downstream.  
* Integrare il motore in un endpoint REST Spring Boot così i client possono caricare immagini e ricevere il testo estratto istantaneamente.

Buona programmazione, e che i tuoi pipeline OCR siano veloci, accurate e multilingue!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}