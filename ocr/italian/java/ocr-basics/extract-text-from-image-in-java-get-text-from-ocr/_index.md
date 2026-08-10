---
category: general
date: 2026-05-25
description: Estrai il testo da un'immagine in Java usando l'OCR. Scopri come caricare
  l'immagine per l'OCR, riconoscere il testo dalla foto e ottenere il testo dall'OCR
  con un semplice esempio di codice.
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: it
og_description: Estrai il testo da un'immagine in Java con una guida passo‑passo.
  Impara a caricare l'immagine per l'OCR, riconoscere il testo dalla foto e ottenere
  il testo dall'OCR in modo efficiente.
og_title: Estrai testo da immagine in Java – Ottieni testo da OCR
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  headline: Extract Text from Image in Java – Get Text from OCR
  type: TechArticle
- description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  name: Extract Text from Image in Java – Get Text from OCR
  steps:
  - name: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
    text: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
  - name: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
    text: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
  - name: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
    text: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
  - name: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
    text: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
  - name: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
    text: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Estrai il testo dall’immagine in Java – Ottieni il testo dall’OCR
url: /it/java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da immagine in Java – Ottieni testo da OCR

Hai mai avuto bisogno di **estrarre testo da immagine** ma non eri sicuro quale libreria Java scegliere? Non sei solo. Che tu stia digitalizzando ricevute, estraendo numeri di serie da foto di prodotti, o semplicemente giocando con un progetto secondario divertente, trasformare un'immagine in testo modificabile è un ostacolo comune.

In questo tutorial ti guideremo attraverso un esempio completo, pronto‑da‑eseguire, che ti mostra come **caricare immagine per OCR**, configurare il motore e infine **riconoscere testo da foto** così potrai **ottenere testo da OCR** con poche righe di codice. Nessun riferimento vago—tutto ciò di cui hai bisogno è qui.

## Cosa imparerai

* Come configurare un motore OCR leggero in Java.  
* I passaggi esatti per **caricare immagine per OCR** e gestire percorsi di file diversi.  
* Perché la configurazione della lingua è importante quando vuoi **estrarre testo da immagine** che non è in inglese.  
* Come stampare in modo sicuro il risultato e cosa fare quando il motore non restituisce nulla.  
* Una serie di consigli professionali per evitare gli errori più comuni.

Alla fine di questa guida avrai un programma autonomo che legge un JPEG (o PNG) contenente caratteri ucraini e stampa la stringa riconosciuta sulla console. Sentiti libero di cambiare lingua o immagine—tutto è modulare.

---

![Diagramma che mostra il flusso di estrazione del testo da immagine usando il motore OCR Java](/images/extract-text-from-image-java.png)

*Testo alternativo: Diagramma di flusso del processo di estrazione del testo da immagine in Java.*

## Prerequisiti

* **Java Development Kit (JDK) 11+** – il codice utilizza il moderno sistema di moduli, ma versioni precedenti funzionano con piccole modifiche.  
* **Maven o Gradle** – per scaricare la libreria OCR (useremo **Asprise OCR** come opzione leggera e gratuita per lo sviluppo).  
* Un file immagine di esempio (ad es. `ukrainian_sign.jpg`) posizionato in un luogo accessibile dal programma.  
* Familiarità di base con il metodo `main` di Java e la gestione delle eccezioni.

Se li hai, sei pronto per partire. Altrimenti, scarica il JDK da Oracle o AdoptOpenJDK e configura un semplice progetto Maven—niente di troppo complicato.

---

## Passo 1: Aggiungi la dipendenza OCR

Per prima cosa, indica al tuo strumento di build di scaricare il motore OCR. Per Maven, inserisci questo in `pom.xml`:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

Se preferisci Gradle, l'equivalente è:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

Queste coordinate scaricano un JAR compatto che include `OcrEngine`, `OcrLanguage` e le classi di supporto che utilizzeremo. Non sono richiesti binari nativi aggiuntivi per gli script latini e cirillici di base.

## Passo 2: Crea una classe Java per **estrarre testo da immagine**

Ora scriveremo il programma vero e proprio. Salva quanto segue come `ExtractTextDemo.java` all'interno di `src/main/java/com/example/ocr/`.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;

/**
 * Demonstrates how to extract text from image using Asprise OCR.
 * The example loads a JPEG, sets the language to Ukrainian,
 * runs recognition, and prints the result.
 */
public class ExtractTextDemo {

    public static void main(String[] args) {
        // ---- 1️⃣  Initialize the OCR engine ---------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---- 2️⃣  Configure the engine to recognize Ukrainian text -----------
        // This is crucial if your image contains non‑Latin characters.
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.UKRAINIAN);

        // ---- 3️⃣  Load the image that contains Ukrainian characters ----------
        // Replace the path with the location of your own picture.
        String imagePath = "YOUR_DIRECTORY/ukrainian_sign.jpg";
        try {
            ocrEngine.getImage().loadFromFile(imagePath);
        } catch (Exception e) {
            System.err.println("Failed to load image: " + e.getMessage());
            return;
        }

        // ---- 4️⃣  Perform OCR recognition and obtain the extracted text -------
        String recognizedText;
        try {
            recognizedText = ocrEngine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Recognition error: " + e.getMessage());
            return;
        }

        // ---- 5️⃣  Output the recognized text to the console -------------------
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### Perché questa struttura funziona

* **Blocchi numerati separati** rendono il flusso facile da seguire, specialmente quando cerchi dove **caricare immagine per OCR** o **riconoscere testo da foto**.  
* Il `try/catch` attorno al caricamento dell'immagine e al riconoscimento garantisce che il programma fallisca in modo elegante—utile quando il percorso del file è errato o il motore OCR non trova i dati della lingua.  
* Impostare la lingua all'inizio (passo 2) migliora notevolmente l'accuratezza per script non‑inglesi. Se in seguito ti serve **java image to text** per altre lingue, basta sostituire `OcrLanguage.UKRAINIAN` con `OcrLanguage.ENGLISH`, `FRENCH`, ecc.

---

## Passo 3: Compila ed esegui il programma

Dalla radice del progetto, esegui:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

Oppure, se usi Gradle:

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

Assumendo che `ukrainian_sign.jpg` contenga il testo *«Ласкаво просимо»* (ucraino per “Benvenuto”), dovresti vedere qualcosa del genere:

```
=== OCR Result ===
Ласкаво просимо
```

Quell'output conferma che hai estratto con successo **testo da immagine** e **ottenuto testo da OCR** in un'unica esecuzione.

---

## Passo 4: Modifica il flusso di lavoro – Da **Java Image to Text** in progetti reali

Sebbene la demo sia minimale, le applicazioni reali spesso richiedono un po' di più:

| Scenario | Cosa modificare | Motivo |
|----------|----------------|--------|
| **Elaborazione batch** | Itera su una `List<Path>` e salva ogni risultato in un database. | Riduce il lavoro manuale quando hai centinaia di foto. |
| **Formati immagine diversi** | Usa `ImageIO.read(new File(path))` per pre‑processare, poi passa il `BufferedImage` a `ocrEngine.getImage().loadFromBufferedImage(bufImg)`. | Gestisce PNG, BMP o anche PDF dopo la conversione. |
| **Ottimizzazione delle prestazioni** | Chiama `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)` se accetti una precisione leggermente inferiore. | Accelera il riconoscimento su hardware a bassa potenza. |
| **Post‑elaborazione** | Rimuovi spazi bianchi, sostituisci errori comuni OCR (`0` → `O`, `1` → `I`). | Migliora la qualità dei dati a valle. |

Queste variazioni mantengono intatta l'idea di base—**riconoscere testo da foto**—offrendoti flessibilità per carichi di lavoro di produzione.

---

## Problemi comuni e consigli professionali

1. **Impostazione della lingua errata** – Se dimentichi il passo 2, il motore usa l'inglese di default, trasformando i caratteri cirillici in spazzatura. Controlla sempre il codice della lingua.  
2. **La qualità dell'immagine è importante** – Foto a bassa risoluzione o sfocate riducono l'accuratezza. Pre‑processa con miglioramento del contrasto o binarizzazione se necessario.  
3. **Particolarità del percorso file** – Su Windows, i backslash devono essere escapati (`C:\\images\\file.jpg`). Usare `Path.of(...)` da `java.nio.file` evita questo problema.  
4. **Perdite di memoria** – `OcrEngine` mantiene risorse native. Chiama `ocrEngine.dispose()` quando hai finito, specialmente in servizi a lunga esecuzione.  
5. **Sicurezza dei thread** – Il motore non è thread‑safe di default. Crea un'istanza separata per thread o sincronizza l'accesso.

---

## Esempio completo funzionante (Tutto‑in‑uno)

Di seguito trovi un unico file che puoi copiare‑incollare in qualsiasi IDE. Include la chiamata `dispose()` e un piccolo metodo di supporto per rendere il codice un po' più pulito.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;
import java.nio.file.Path;

/**
 * Complete, runnable demo that extracts text from an image using Java OCR.
 */
public class FullDemo {

    public static void main(String[] args) {
        // Path to the image – change this to your own file.
        Path imgPath = Path.of("YOUR_DIRECTORY/ukrainian_sign.jpg");

        // Run the OCR workflow and capture the output.
        String result = extractTextFromImage(imgPath, OcrLanguage.UKRAINIAN);
        if (result != null) {
            System.out.println("=== OCR Result ===");
            System.out.println(result);
        }
    }

    /**
     * Core method that encapsulates the 5‑step OCR process.
     *
     * @param imagePath Path to the image file.
     * @param language  Desired OCR language.
     * @return Recognized text, or {@code null} if something went wrong.
     */
    private static String extractTextFromImage(Path imagePath, OcrLanguage language) {
        OcrEngine engine = new OcrEngine();
        try {
            // 1️⃣ Set language
            engine.getEngineOptions().setLanguage(language);

            // 2️⃣ Load image
            engine.getImage().loadFromFile(imagePath.toString());

            // 3️⃣ Recognize and return text
            return engine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Error during OCR: " + e.getMessage());
            return null;
        } finally {
            // 4️⃣ Release native resources
            engine.dispose();
        }
    }
}
```

Eseguendo questo programma otterrai lo stesso output della console mostrato in precedenza. Sentiti libero di sostituire `OcrLanguage.UKRAINIAN` con `OcrLanguage.ENGLISH` o qualsiasi altra lingua supportata per vedere come il motore si adatta.

---

## Conclusione

Abbiamo percorso tutto ciò di cui hai bisogno per **estrarre testo da immagine** usando Java: dall'aggiungere la dipendenza OCR, a **caricare immagine per OCR**, 

## Tutorial correlati

- [riconoscere immagine di testo con Aspose OCR – Tutorial completo OCR Java](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Come fare OCR del testo di un'immagine con lingua usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Convertire immagine in testo in Java usando Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}