---
category: general
date: 2026-11-17
description: Scopri come eseguire l'OCR su un'immagine in Java ed estrarre il testo
  dalle foto usando un semplice esempio di codice. Include consigli su come leggere
  le immagini in Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: it
lastmod: 2026-11-17
og_description: Come eseguire l'OCR su un'immagine in Java e estrarre il testo rapidamente.
  Segui questa guida per leggere un'immagine in Java e convertire l'immagine in testo
  con un esempio pronto all'uso.
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: Come eseguire l'OCR su un'immagine in Java – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: Come eseguire l'OCR su un'immagine in Java – guida passo passo
url: /it/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR su un'immagine in Java – guida passo‑passo

Se hai bisogno di **how to perform OCR** su un'immagine, questo tutorial ti mostra una soluzione completa e eseguibile in Java. Vedrai come leggere un file immagine, configurare un motore OCR e estrarre il testo riconosciuto dal motore.

Lavorare con documenti scansionati, ricevute o screenshot richiede spesso la conversione del contenuto visivo in testo ricercabile. Questa guida ti accompagna passo dopo passo, dal caricamento dell'immagine alla stampa del testo estratto, e copre anche le difficoltà comuni come formati di file non supportati e risultati nulli.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* Java Development Kit (JDK) 8 o versioni successive installato.
* Uno strumento di build (Maven o Gradle) per scaricare la libreria OCR.
* Un file immagine (JPEG, PNG, BMP) che desideri elaborare.

Il codice utilizza la **OCR library from the `com.asprise.ocr` package** perché richiede un solo JAR e funziona su tutte le principali piattaforme. Sostituiscila con un altro provider (Tesseract, Google Vision, ecc.) scambiando le istruzioni di importazione e il codice di inizializzazione del motore.

## Passo 1: Aggiungi la dipendenza OCR

Se usi Maven, aggiungi la seguente dipendenza al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

Per Gradle, inserisci questa riga in `build.gradle`:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

Queste righe garantiscono che il codice **read image Java** possa compilare e che il motore OCR sia disponibile a runtime.

## Passo 2: Leggi l'immagine con Java

Leggere un file immagine è il primo passo concreto in qualsiasi workflow **extract text image**. La classe integrata di Java `ImageIO` gestisce la maggior parte dei formati comuni.

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**Perché è importante:** `ImageIO.read` restituisce `null` per formati non supportati o file corrotti. Il metodo sopra registra il problema e restituisce `null` così il passo successivo può reagire in modo appropriato.

## Passo 3: Crea e configura il motore OCR

Il motore OCR deve sapere quale lingua riconoscere. Impostare la lingua migliora notevolmente la precisione, soprattutto per documenti non‑inglesi.

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**Perché è importante:** Avviare il motore è un'operazione relativamente pesante, quindi dovresti crearlo una sola volta e riutilizzarlo per più immagini se la tua applicazione elabora batch.

## Passo 4: Esegui OCR e converti l'immagine in testo

Ora che l'immagine è caricata e il motore è pronto, puoi avviare il passaggio di riconoscimento. Questo è il cuore di **how to perform OCR**.

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**Gestione dei casi limite:** Se l'immagine è `null`, il metodo restituisce una stringa vuota invece di lanciare una `NullPointerException`. Questo rende il codice circostante più robusto quando si gestiscono file forniti dagli utenti.

## Passo 5: Visualizza il testo estratto

Infine, stampa il risultato sulla console o inoltralo a un altro componente (ad es., un database o un widget UI).

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

Quando esegui il programma con `java OcrDemo sample.jpg`, la console mostra i caratteri riconosciuti. Questo completa il ciclo **convert image to text**.

### Output previsto

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

Se l'immagine non contiene caratteri leggibili, il programma stampa `(no text detected)`.

## Variazioni comuni e come adattarle

| Variazione | Cosa cambia | Quando usarla |
|------------|-------------|---------------|
| **Different language** | Sostituisci `"eng"` con `"spa"` per lo spagnolo, `"fra"` per il francese, ecc. | Documenti scritti in una lingua diversa dall'inglese |
| **Batch processing** | Cicla su un elenco di percorsi file, riutilizza la stessa istanza `Ocr`. | Grandi insiemi di pagine scansionate |
| **Higher accuracy** | Usa `Ocr.SPEED_SLOW` o abilita `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")` per scansioni solo numeriche. | Quando la qualità OCR è critica (ad es., numeri di fattura) |
| **Tesseract alternative** | Scambia l'import con `net.sourceforge.tess4j.Tesseract` e adatta il codice di inizializzazione. | Progetti che dipendono già da Tesseract |

## Pro tips

* **Ridimensiona le immagini grandi** prima di passarle al motore; la velocità dell'OCR scala con il numero di pixel.
* **Pre‑processa** l'immagine (scala di grigi, aumento del contrasto) usando librerie come OpenCV se la sorgente è rumorosa.
* **Metti in cache il motore OCR** se lo chiami molte volte in breve tempo—avviare e fermare il motore comporta un overhead.
* **Convalida il risultato** con espressioni regolari quando ti aspetti un formato specifico (ad esempio date, numeri di telefono).

## Conclusione

Ora sai **how to perform OCR** su un'immagine in Java, dalla lettura del file alla visualizzazione del testo estratto. Il tutorial ha coperto le tecniche **read image Java**, **extract text image**, **convert image to text** e **image to text java**, fornendo consigli pratici per scenari reali.  

Da qui puoi:

* Integrare il passo OCR in un servizio web che riceve upload.
* Combinare l'output con un indice di ricerca per la ricerca full‑text su documenti scansionati.
* Esplorare opzioni OCR avanzate come il supporto multilingua o set di caratteri personalizzati.

Buon coding e divertiti a trasformare le immagini in testo ricercabile!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come utilizzare OCR in Java – Estrarre testo da immagine con correzione ortografica](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [Converti immagine in testo in Java usando Aspose OCR – Guida completa](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [Come abilitare GPU per OCR in Java – Estrarre testo da immagine](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}