---
category: general
date: 2026-03-28
description: Preprocessa l'immagine per l'OCR e riconosci il testo dall'immagine con
  Aspose OCR. Scopri come estrarre il testo da una foto e migliorare l'accuratezza
  dell'OCR con la pre‑elaborazione passo dopo passo.
draft: false
keywords:
- preprocess image for OCR
- recognize text from image
- extract text from photo
- improve OCR accuracy preprocessing
- Aspose OCR Java
- image preprocessing pipeline
language: it
og_description: Preprocessa l'immagine per l'OCR ed estrai il testo dalla foto con
  Aspose OCR Java. Segui questo tutorial per migliorare la precisione dell'OCR con
  la preelaborazione in pochi semplici passaggi.
og_title: Preelaborazione dell'immagine per OCR – Guida completa Java
tags:
- OCR
- Java
- Image Processing
title: Preelaborare l'immagine per OCR – Incrementare la precisione dell'estrazione
  del testo in Java
url: /it/java/advanced-ocr-techniques/preprocess-image-for-ocr-boost-text-extraction-accuracy-in-j/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Preprocess Image for OCR – Guida Completa Java

Hai mai provato a **preprocess image for OCR** e hai comunque ottenuto un output incomprensibile? Non sei solo. In molti progetti reali, una scansione grezza o una foto scattata con lo smartphone contiene inclinazione, rumore o basso contrasto che confondono anche il motore di riconoscimento più avanzato. La buona notizia? Una breve pipeline di pre‑processing—de‑skew, denoise, binarize—può migliorare drasticamente **improve OCR accuracy preprocessing**.

In questo tutorial ti guideremo attraverso un esempio pratico che mostra esattamente come **recognize text from image** usando Aspose OCR per Java. Alla fine sarai in grado di **extract text from photo** file con molti meno errori, e comprenderai perché ogni passaggio di pre‑processing è importante.

> **Cosa otterrai**  
> * Un programma Java completamente eseguibile che carica una foto inclinata, applica tre filtri classici e stampa testo pulito.  
> * Approfondimento sul “perché” dietro de‑skew, denoise e binarize.  
> * Suggerimenti per gestire casi limite—file di grandi dimensioni, diversi formati immagine e ordine personalizzato dei filtri.

## Prerequisiti

- Java 8 o versioni successive installato (il codice si compila anche con JDK 11).  
- Maven o Gradle per scaricare la libreria Aspose OCR.  
- Un’immagine di esempio (ad es., `angled-photo.jpg`) leggermente ruotata e contenente qualche rumore visivo.  
- Familiarità di base con il metodo `main` di Java—non è necessaria un’esperienza approfondita in OCR.

Se ti manca qualcuno di questi, scarica l'ultima JDK da Oracle o OpenJDK e aggiungi la seguente dipendenza Maven al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check Maven Central for the newest version -->
</dependency>
```

## Passo 1 – Crea l'Istanza del Motore OCR

La prima cosa di cui hai bisogno è un oggetto `OcrEngine`. Pensalo come il cervello che in seguito leggerà l'immagine elaborata.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Perché è importante:** Il motore incapsula le impostazioni di riconoscimento, i pacchetti linguistici e—soprattutto per noi—le opzioni di preprocessing. Senza di esso, dovresti concatenare manualmente le librerie di elaborazione immagini, il che vanifica lo scopo di una pipeline pulita.

## Passo 2 – Costruisci una Pipeline di Pre‑processing (de‑skew → denoise → binarize)

Aspose OCR fornisce una classe integrata `PreprocessingOptions` che ti permette di impilare i filtri nell'ordine esatto di cui hai bisogno. Qui aggiungiamo tre filtri:

1. **DE_SKEW** – raddrizza il testo ruotato.  
2. **DENOISE** – leviga i pixel granulosi che potrebbero essere scambiati per caratteri.  
3. **BINARIZE** – converte l'immagine in puro bianco‑e‑nero, facilitando il lavoro del motore OCR.

```java
        // Step 2: Assemble the preprocessing pipeline
        PreprocessingOptions preprocessingOptions = new PreprocessingOptions();
        preprocessingOptions.addFilter(PreprocessFilter.DE_SKEW);   // correct rotation
        preprocessingOptions.addFilter(PreprocessFilter.DENOISE);  // remove grain
        preprocessingOptions.addFilter(PreprocessFilter.BINARIZE); // high‑contrast B&W

        // Attach the pipeline to the OCR engine
        ocrEngine.getRecognitionSettings().setPreprocessingOptions(preprocessingOptions);
```

> **Consiglio professionale:** L'ordine dei filtri è cruciale. Se binarizzi *prima* della denoising, il rumore può diventare macchie nere a bordi netti che confondono il riconoscitore. De‑skew prima garantisce che la linea di base del testo sia orizzontale, migliorando sia i risultati della denoise che della binarize.

## Passo 3 – Fornisci l'Immagine al Motore

Ora indirizziamo il motore verso il file che vogliamo leggere. Il percorso può essere assoluto o relativo alla radice del tuo progetto.

```java
        // Step 3: Run OCR on the target image
        String imagePath = "YOUR_DIRECTORY/angled-photo.jpg";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

> **E se l'immagine è enorme?** Aspose OCR ridimensiona automaticamente le immagini più grandi di 2000 px sul lato più lungo, ma puoi sovrascrivere questo valore tramite `ocrEngine.getRecognitionSettings().setMaxImageDimension(1500)` se la memoria è un problema.

## Passo 4 – Output del Testo Riconosciuto

Infine, stampiamo la stringa estratta sulla console. In un'applicazione reale potresti scriverla in un database, in un file o inviarla a una pipeline NLP a valle.

```java
        // Step 4: Print the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Output Atteso

Se `angled-photo.jpg` contiene la frase *“The quick brown fox jumps over the lazy dog.”* dovresti vedere qualcosa di simile:

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

Nota come l'output è pulito—nessun simbolo estraneo, nessuna riga interrotta. Questa è la potenza di **preprocess image for OCR**.

## Passo 5 – Verifica e Regola (Opzionale)

Anche con una pipeline solida, potresti incontrare casi limite:

| Situazione | Suggerimento consigliato |
|------------|--------------------------|
| **Contrasto molto basso** (es., documenti scansionati sbiaditi) | Inserisci un filtro extra `ContrastAdjustment` prima della binarizzazione. |
| **Sfondo colorato** (es., ricevute con timbri colorati) | Aggiungi il filtro `BackgroundRemoval` o converti manualmente in scala di grigi prima. |
| **PDF multi‑pagina** | Itera su ogni immagine di pagina e riutilizza lo stesso `preprocessingOptions`. |

Puoi sperimentare chiamando `preprocessingOptions.addFilter(PreprocessFilter.CONTRAST)` o qualsiasi altro filtro elencato nella documentazione API di Aspose OCR.

## Esempio Completo, Eseguibile

Di seguito trovi il programma completo, pronto per essere copiato‑incollato in un file chiamato `PreprocessExample.java`. Assicurati che la dipendenza Maven sia risolta prima di compilare.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing: de‑skew → denoise → binarize
        PreprocessingOptions preprocessingOptions = new PreprocessingOptions();
        preprocessingOptions.addFilter(PreprocessFilter.DE_SKEW);
        preprocessingOptions.addFilter(PreprocessFilter.DENOISE);
        preprocessingOptions.addFilter(PreprocessFilter.BINARIZE);
        ocrEngine.getRecognitionSettings().setPreprocessingOptions(preprocessingOptions);

        // 3️⃣ Perform OCR on the chosen image
        String imagePath = "YOUR_DIRECTORY/angled-photo.jpg";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // 4️⃣ Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Compila ed esegui:

```bash
mvn compile exec:java -Dexec.mainClass=PreprocessExample
```

Dovresti vedere il testo pulito stampato sulla console, confermando che hai eseguito correttamente **preprocess image for OCR** e **recognize text from image**.

## Domande Frequenti & Risposte

**Q1: Funziona con file PNG o TIFF?**  
Sì—Aspose OCR supporta JPEG, PNG, BMP, TIFF e diversi altri formati. La stessa pipeline di preprocessing si applica; la libreria rileva automaticamente il formato.

**Q2: E se devo estrarre testo da una foto scattata con il telefono?**  
Le foto dei telefoni spesso hanno illuminazione non uniforme. Aggiungere un filtro `LIGHTING_CORRECTION` prima della binarizzazione può aiutare. La modifica al codice è una singola riga:

```java
preprocessingOptions.addFilter(PreprocessFilter.LIGHTING_CORRECTION);
```

**Q3: Posso cambiare la lingua dell'OCR?**  
Assolutamente. Dopo aver creato il motore, imposta la lingua:

```java
ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.SPANISH);
```

**Q4: Come migliora questo la precisione dell'OCR preprocessing?**  
Ogni filtro riduce un tipo specifico di rumore visivo. De‑skew allinea le linee di testo, denoise rimuove le macchie casuali e binarize crea un'immagine ad alto contrasto. Insieme forniscono all'algoritmo di riconoscimento un segnale più pulito, il che si traduce in una maggiore accuratezza a livello di carattere—spesso un aumento del 15‑30 % su input rumorosi.

## Prossimi Passi & Argomenti Correlati

- **Batch processing:** Avvolgi la logica principale in un ciclo per gestire intere cartelle di foto.  
- **Custom filter order:** Sperimenta con `BINARIZE` prima di `DENOISE` per documenti già ad alto contrasto.  
- **Performance tuning:** Usa `ocrEngine.getRecognitionSettings().setThreadCount(4)` per parallelizzare su macchine multi‑core.  
- **Alternative libraries:** Confronta Aspose OCR con Tesseract‑Java per scenari open‑source.  
- **Post‑processing:** Applica il controllo ortografico o la pulizia con regex all'output grezzo per risultati ancora più puliti.

Padroneggiando il flusso di lavoro **preprocess image for OCR**, scoprirai che estrarre testo da fonti fotografiche diventa un compito prevedibile e ripetibile, anziché un esperimento incerto.

---

*Pronto a potenziare la tua pipeline OCR? Prendi il codice, modifica i filtri e guarda la precisione aumentare. Se incontri un problema, lascia un commento qui sotto—buona programmazione!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}