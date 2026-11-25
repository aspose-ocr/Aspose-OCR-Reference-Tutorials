---
category: general
date: 2026-08-18
description: Come abilitare la GPU per l'OCR in Java e riconoscere rapidamente il
  testo delle immagini, estrarre il testo da JPG, aggiungere filtri e impostare la
  lingua con Aspose.OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize image text
- extract text jpg
- how to add filter
- how to set language
language: it
lastmod: 2026-08-18
og_description: Come abilitare la GPU per l'OCR in Java e riconoscere istantaneamente
  il testo delle immagini, estrarre testo da JPG, aggiungere un filtro e impostare
  la lingua usando Aspose.OCR.
og_image_alt: Screenshot showing Java code that enables GPU for OCR with Aspose.OCR
og_title: Come abilitare la GPU per l'OCR in Java – guida completa di Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-08-18'
  description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  headline: How to enable GPU for OCR in Java using Aspose.OCR
  type: TechArticle
- description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  name: How to enable GPU for OCR in Java using Aspose.OCR
  steps:
  - name: 3.1 Set the OCR language
    text: '```java // Choose the language for recognition – this is the “how to set
      language” step engine.setLanguage(OcrLanguage.ENGLISH); ```'
  - name: 3.2 Add a preprocessing filter
    text: 'Noise, compression artifacts, or uneven lighting can hurt accuracy. Adding
      a denoise filter is the typical **how to add filter** approach:'
  - name: Expected output
    text: '``` Recognized text: The quick brown fox jumps over the lazy dog. ```'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: Come abilitare la GPU per l'OCR in Java usando Aspose.OCR
url: /it/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come abilitare la GPU per OCR in Java usando Aspose.OCR

Se hai bisogno di **come abilitare la GPU** per OCR in Java, questa guida ti accompagna passo passo. Abilitare l’accelerazione GPU ti consente di **riconoscere il testo nelle immagini** fino a diverse volte più velocemente, il che è fondamentale quando devi **estrarre testo JPG** in blocco. Tratteremo anche **come aggiungere un filtro**, **come impostare la lingua** e come recuperare il risultato finale.

Al termine di questo tutorial avrai un programma completo, eseguibile, che:

* Avvia il motore Aspose.OCR con supporto GPU.  
* Configura la lingua OCR (ad es. English).  
* Applica un filtro di denoising per migliorare la precisione.  
* Carica un’immagine JPEG, esegue il riconoscimento e stampa il testo estratto.

> **Prerequisito:** Java 17 o successiva, Maven e una licenza Aspose.OCR per Java (la versione di prova gratuita è sufficiente per la valutazione).

---

![Come abilitare GPU per OCR in Java](/images/ocr-gpu.png){alt="Come abilitare GPU per OCR in Java"}

## Cosa ti servirà

| Elemento | Motivo |
|------|--------|
| **Java Development Kit (JDK) 17+** | Necessario per compilare ed eseguire l’esempio. |
| **Maven** | Semplifica la gestione delle dipendenze per Aspose.OCR. |
| **Aspose.OCR per Java** | Fornisce la classe `OcrEngine` e il supporto GPU. |
| **Un’immagine JPEG di esempio** (`sample.jpg`) | Utilizzata per dimostrare **estrarre testo JPG**. |
| **Hardware compatibile con GPU** (opzionale ma consigliato) | Consente il boost di prestazioni che configureremo. |

---

## Passo 1: Configurare il progetto Maven

Crea un nuovo progetto Maven (o aggiungilo a uno esistente) e includi la dipendenza Aspose.OCR:

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-gpu-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Aspose.OCR for Java -->
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-ocr</artifactId>
            <version>23.12</version> <!-- Use the latest stable version -->
        </dependency>
    </dependencies>
</project>
```

> **Consiglio professionale:** Mantieni il numero di versione aggiornato; le versioni più recenti migliorano la gestione della GPU e aggiungono pacchetti lingua.

---

## Passo 2: Inizializzare il motore OCR e **come abilitare la GPU**

Il cuore della soluzione è `OcrEngine`. Istanziarlo è semplice, ma devi attivare esplicitamente l’accelerazione GPU:

```java
import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2.2: Enable GPU acceleration (this is the “how to enable GPU” part)
        engine.setUseGpu(true); // <-- GPU is now active

        // Step 2.3: Configure language and preprocessing filter (covered later)
```

**Perché abilitare la GPU?**  
Quando viene chiamato `setUseGpu(true)`, Aspose.OCR delega i kernel di elaborazione immagine pesanti alla scheda grafica. Su una GPU NVIDIA/AMD moderna la velocità di riconoscimento può passare da ~200 ms per pagina a < 80 ms, riducendo drasticamente il tempo totale di elaborazione per grandi lotti.

---

## Passo 3: **Come impostare la lingua** e **come aggiungere un filtro**

### 3.1 Impostare la lingua OCR

```java
        // Choose the language for recognition – this is the “how to set language” step
        engine.setLanguage(OcrLanguage.ENGLISH);
```

Aspose.OCR include pacchetti lingua per oltre 100 lingue. Sostituisci `ENGLISH` con `FRENCH`, `CHINESE_SIMPLIFIED`, ecc., per adattarlo al tuo materiale sorgente.

### 3.2 Aggiungere un filtro di pre‑elaborazione

Rumore, artefatti di compressione o illuminazione non uniforme possono penalizzare la precisione. Aggiungere un filtro di denoise è l’approccio tipico **come aggiungere un filtro**:

```java
        // Add a denoising filter to improve OCR quality – “how to add filter”
        engine.addPreprocessFilter(FilterType.DENOISE);
```

Altri filtri utili includono `FilterType.CONTRAST`, `FilterType.BRIGHTNESS` e `FilterType.BINARIZE`. Puoi concatenare più filtri chiamando più volte `addPreprocessFilter`.

---

## Passo 4: Caricare l’immagine – **estrarre testo JPG**

Ora puntiamo il motore al file JPEG da elaborare:

```java
        // Load the JPEG image – this demonstrates “extract text JPG”
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

Sostituisci `YOUR_DIRECTORY` con il percorso reale dove risiede `sample.jpg`. Aspose.OCR supporta anche PNG, BMP, TIFF e PDF; la stessa chiamata funziona per questi formati.

---

## Passo 5: Eseguire OCR e **riconoscere il testo nell’immagine**

Con il motore configurato, invoca la routine di riconoscimento:

```java
        // Run the OCR operation – “recognize image text”
        engine.recognize();

        // Retrieve the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);
    }
}
```

Il metodo `recognize()` elabora l’immagine sulla GPU (se abilitata) e riempie il buffer interno di testo. `getText()` restituisce una `String` in plain‑text, che puoi scrivere su file, su un database o passare a pipeline NLP successive.

### Output previsto

```
Recognized text: The quick brown fox jumps over the lazy dog.
```

Se l’immagine contiene più righe, la stringa restituita include caratteri di nuova linea (`\n`) preservando il layout originale.

---

## Passo 6: Verificare l’uso della GPU (opzionale)

Per confermare che la GPU sia effettivamente utilizzata, abilita il logging di Aspose:

```java
        // Enable diagnostic logging (optional)
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
```

Ispeziona `ocr-debug.log` dopo un’esecuzione; dovresti vedere voci come `GPU device: NVIDIA GeForce RTX 3080` e `Processing time (GPU): 78 ms`. Se il log menziona **CPU**, ricontrolla l’installazione del driver e che la chiamata `setUseGpu(true)` sia presente.

---

## Problemi comuni e come evitarli

| Sintomo | Probabile causa | Soluzione |
|---------|----------------|-----------|
| **`java.lang.UnsatisfiedLinkError: no aspose_ocr_native`** | Mancano le librerie native GPU | Installa l’ultimo driver GPU e assicurati che i binari native `aspose-ocr` siano nel `java.library.path`. |
| **Scarsa accuratezza su immagini scure** | Nessun filtro di pre‑elaborazione | Aggiungi `engine.addPreprocessFilter(FilterType.BRIGHTNESS)` o aumenta `FilterType.CONTRAST`. |
| **`OutOfMemoryError` su grandi lotti** | Esaurimento della memoria GPU | Elabora le immagini in batch più piccoli o disabilita la GPU (`engine.setUseGpu(false)`) per risoluzioni molto elevate. |
| **Output in lingua errata** | Lingua impostata in modo sbagliato | Verifica che `engine.setLanguage(OcrLanguage.YOUR_LANGUAGE)` corrisponda al testo sorgente. |

---

## Esempio completo, eseguibile

Di seguito trovi la classe Java completa da copiare‑incollare in `src/main/java/com/example/HelloWorldOcr.java`. Include tutti i passaggi, la gestione degli errori e il logging opzionale.

```java
package com.example;

import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // -------------------------------------------------
        // 1️⃣ Enable GPU acceleration – how to enable GPU
        // -------------------------------------------------
        engine.setUseGpu(true);

        // -------------------------------------------------
        // 2️⃣ Set language – how to set language
        // -------------------------------------------------
        engine.setLanguage(OcrLanguage.ENGLISH); // Change if needed

        // -------------------------------------------------
        // 3️⃣ Add preprocessing filter – how to add filter
        // -------------------------------------------------
        engine.addPreprocessFilter(FilterType.DENOISE);
        // Optional: engine.addPreprocessFilter(FilterType.CONTRAST);

        // -------------------------------------------------
        // 4️⃣ Load the JPEG image – extract text JPG
        // -------------------------------------------------
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        engine.setImage(ImageStream.fromFile(imagePath));

        // -------------------------------------------------
        // 5️⃣ Perform OCR – recognize image text
        // -------------------------------------------------
        engine.recognize();

        // Retrieve and display the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);

        // -------------------------------------------------
        // 6️⃣ Optional: write output to a file
        // -------------------------------------------------
        java.nio.file.Files.writeString(
                java.nio.file.Paths.get("output.txt"),
                text,
                java.nio.charset.StandardCharsets.UTF_8
        );

        // -------------------------------------------------
        // 7️⃣ Optional: enable debug logging to verify GPU usage
        // -------------------------------------------------
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
    }
}
```

**Eseguire il programma**

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HelloWorldOcr
```

Dovresti vedere il testo riconosciuto stampato sulla console e salvato in `output.txt`. Il file `ocr-debug.log` confermerà l’utilizzo della GPU.

---

## Conclusione

In questo tutorial abbiamo mostrato **come abilitare la GPU** per Aspose.OCR in Java, come **riconoscere il testo nell’immagine**, **estrarre testo JPG**, **come aggiungere un filtro** e **come impostare la lingua**—tutto all’interno di un unico programma autonomo. Abilitando la GPU ottieni un notevole incremento di velocità, mentre filtri e impostazioni linguistiche garantiscono alta accuratezza su fonti immagine diverse.

**Passi successivi**

* Sperimenta filtri aggiuntivi come `FilterType.BINARIZE` per documenti scansionati.  
* Passa a altre lingue (`OcrLanguage.SPANISH`, `OcrLanguage.CHINESE_SIMPLIFIED`) per ampliare il supporto multilingue.  
* Combina questa pipeline OCR con Apache PDFBox per estrarre testo direttamente da pagine PDF.  

Sentiti libero di adattare il codice per l’elaborazione batch, integrarlo in un servizio Spring Boot o collegarlo a una coda di messaggi per carichi OCR in tempo reale. Buona programmazione!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Read Text from an Image in Java Using Aspose OCR – Complete Guide](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Preprocess Image OCR in Java with Aspose OCR – Boost Accuracy & Extract Text](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}