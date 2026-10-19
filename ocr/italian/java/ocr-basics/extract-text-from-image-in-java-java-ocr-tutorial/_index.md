---
category: general
date: 2026-03-07
description: Estrai testo da un'immagine con Java OCR. Scopri come caricare l'immagine
  per l'OCR, configurare la lingua e eseguire un tutorial completo di Java OCR in
  pochi minuti.
draft: false
keywords:
- extract text from image
- load image for ocr
- use OCR in java
- java ocr tutorial
language: it
og_description: Estrai il testo da un'immagine usando Java OCR. Questo tutorial mostra
  come caricare un'immagine per l'OCR, configurare la lingua e eseguire un tutorial
  Java OCR passo passo.
og_title: Estrai il testo da un'immagine in Java – Guida completa all'OCR
tags:
- OCR
- Java
- Image Processing
title: Estrai testo da un'immagine in Java – Tutorial OCR Java
url: /it/java/ocr-basics/extract-text-from-image-in-java-java-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da immagine in Java – Guida completa OCR

Ti è mai capitato di dover **estrarre testo da immagine** ma non sapevi da dove cominciare in Java? Non sei l'unico—gli sviluppatori si scontrano spesso con questo ostacolo quando trasformano cartelli scansionati, ricevute o appunti scritti a mano in stringhe ricercabili.  

La buona notizia? In pochi minuti puoi avere una pipeline OCR funzionante che legge Kannada, Inglese o qualsiasi lingua supportata. In questo tutorial **caricheremo l'immagine per OCR**, configureremo il motore e percorreremo un **tutorial OCR Java** che puoi copiare‑incollare ed eseguire subito.

## Cosa copre questa guida

Inizieremo elencando gli strumenti necessari, poi passeremo direttamente a un'implementazione **passo‑passo**. Alla fine sarai in grado di:

* Caricare un file immagine in un `ImageInputStream` Java.
* Configurare un motore OCR per riconoscere una lingua specifica (Kannada nel nostro esempio).
* Eseguire il processo di riconoscimento e stampare il testo estratto.
* Regolare le impostazioni per una migliore precisione e gestire le problematiche comuni.

Nessuna documentazione esterna necessaria—tutto ciò che ti serve è qui.  

**Prerequisiti**: Java 17 o superiore, uno strumento di build come Maven o Gradle, e una libreria OCR che fornisce una classe `OcrEngine` (ad esempio, l'ipotetico SDK *SimpleOCR*). Se usi Maven, aggiungi la dipendenza mostrata più avanti.

---

## Passo 1 – Configura il tuo progetto e aggiungi la libreria OCR

Prima di scrivere codice, assicurati che il tuo progetto possa vedere le classi OCR. Con Maven, inserisci questo snippet nel tuo `pom.xml`:

```xml
<!-- Maven dependency for SimpleOCR (replace with your actual OCR SDK) -->
<dependency>
    <groupId>com.example</groupId>
    <artifactId>simple-ocr</artifactId>
    <version>1.4.2</version>
</dependency>
```

Se preferisci Gradle, l'equivalente è:

```gradle
implementation 'com.example:simple-ocr:1.4.2'
```

> **Consiglio:** Mantieni la versione della libreria aggiornata; le versioni più recenti spesso includono miglioramenti ai modelli linguistici che aumentano la precisione.

Una volta risolta la dipendenza, aggiorna il tuo IDE e sei pronto per scrivere codice.

## Passo 2 – Importa le classi necessarie

Di seguito trovi l'elenco completo degli import necessari per l'esempio. Sono deliberatamente ridotti al minimo così puoi vedere esattamente cosa fa ogni classe.

```java
import com.example.ocr.OcrEngine;      // Main OCR engine
import com.example.ocr.OcrResult;      // Holds recognition result
import com.example.io.ImageInputStream; // Wrapper for image files
import java.nio.file.Paths;             // Convenient path handling
import java.io.IOException;             // For proper exception handling
```

> **Perché questi import?** `OcrEngine` e `OcrResult` sono il cuore del processo OCR, mentre `ImageInputStream` astrae il boilerplate di lettura dei file. L'uso di `java.nio.file.Paths` rende il codice indipendente dal sistema operativo.

## Passo 3 – Carica l'immagine per OCR

Ora arriva la parte che spesso blocca le persone: fornire al motore il formato immagine corretto. L'SDK OCR si aspetta un `ImageInputStream`, che puoi ottenere da qualsiasi file su disco.

```java
// Step 3: Load the image that contains the text you want to extract
String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));
```

> **Caso limite:** Se l'immagine è corrotta o in un formato non supportato (ad esempio, GIF), il costruttore lancerà un `IOException`. Avvolgi la chiamata in un blocco try‑catch o valida il file in anticipo.

## Passo 4 – Configura il motore per riconoscere una lingua specifica

La maggior parte dei motori OCR offre supporto multilingue. Per migliorare la precisione dovresti indicare al motore esattamente quale lingua cercare. Nel nostro caso usiamo il codice lingua `"kn"` per il Kannada.

```java
// Step 4: Create and configure the OCR engine for Kannada
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getConfig().setLanguage("kn"); // 'kn' = Kannada
```

> **Perché impostare la lingua?** Limitare il set di caratteri riduce i falsi positivi, specialmente quando si trattano script con molti glifi simili.

Se mai dovessi cambiare lingua, basta modificare la stringa del codice—non sono necessarie altre modifiche.

## Passo 5 – Esegui il processo OCR ed estrai il testo

Con l'immagine caricata e il motore configurato, il riconoscimento effettivo è una singola chiamata di metodo. L'oggetto risultato ti fornisce il testo semplice e, opzionalmente, i punteggi di confidenza.

```java
// Step 5: Run OCR and retrieve the recognized text
OcrResult ocrResult = ocrEngine.recognize(imageStream);
String extractedText = ocrResult.getText();
```

> **Domanda comune:** *E se l'OCR restituisce una stringa vuota?*  
> Tipicamente significa che la qualità dell'immagine è troppo bassa (sfocatura, basso contrasto) o che la lingua non è stata impostata correttamente. Prova a pre‑processare l'immagine (aumenta il contrasto, binarizza) o ricontrolla il codice lingua.

## Passo 6 – Visualizza il risultato

Infine, stampa l'output sulla console. In un'applicazione reale potresti salvarlo in un database o inserirlo in un indice di ricerca.

```java
// Step 6: Output the recognized Kannada text
System.out.println("Extracted text:");
System.out.println(extractedText);
```

### Output previsto

Se l'immagine di origine contiene la frase Kannada “ಕರ್ನಾಟಕ” (Karnataka), la console dovrebbe mostrare:

```
Extracted text:
ಕರ್ನಾಟಕ
```

Ecco fatto—un flusso di lavoro completo **uso OCR in Java** che puoi adattare a qualsiasi lingua o sorgente immagine.

---

## Esempio completo funzionante

Di seguito trovi l'intero programma, pronto per la compilazione. Sostituisci `YOUR_DIRECTORY` con il percorso reale del tuo file immagine.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrResult;
import com.example.io.ImageInputStream;
import java.nio.file.Paths;
import java.io.IOException;

public class KannadaOcrExample {
    public static void main(String[] args) {
        try {
            // Create OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Configure for Kannada (language code "kn")
            ocrEngine.getConfig().setLanguage("kn");

            // Load the image you want to extract text from
            String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
            ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));

            // Run the OCR process
            OcrResult ocrResult = ocrEngine.recognize(imageStream);

            // Print the extracted text
            System.out.println("Extracted text:");
            System.out.println(ocrResult.getText());
        } catch (IOException e) {
            System.err.println("Failed to load image or run OCR: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Unexpected error during OCR: " + e.getMessage());
        }
    }
}
```

> **Suggerimento:** Per il codice di produzione, considera di riutilizzare una singola istanza di `OcrEngine` per più immagini; crearla ripetutamente può essere costoso.

---

## Domande frequenti & casi limite

### Come migliorare la precisione su foto rumorose?

- **Pre‑processa** l'immagine: convertila in scala di grigi, applica un filtro mediano o aumenta il contrasto.
- **Ridimensiona** l'immagine a almeno 300 DPI; la maggior parte dei motori OCR si aspetta quella risoluzione.
- **Imposta una whitelist** di caratteri se conosci l'output previsto (ad esempio, solo cifre).

### Posso usare questo approccio per PDF?

Sì. Estrai ogni pagina come immagine (usando PDFBox o iText), poi passa quelle immagini nella stessa pipeline. Il codice rimane identico; solo la sorgente dell'immagine cambia.

### Cosa fare se devo riconoscere più lingue in una singola immagine?

La maggior parte degli SDK consente di passare una lista separata da virgole, come `"en,kn"`. Il motore cercherà di corrispondere a uno qualsiasi degli script forniti.

### È possibile ottenere i punteggi di confidenza?

`OcrResult` spesso include un metodo `getConfidence()` che restituisce un float tra 0 e 1 per ogni riga. Usalo per filtrare i risultati a bassa confidenza.

---

## Prossimi passi

Ora che puoi **estrarre testo da immagine** usando Java, potresti esplorare:

* **Elaborazione batch** – iterare su una cartella di immagini e scrivere i risultati in CSV.
* **Integrazione con Apache Tika** – combinare OCR con l'analisi dei documenti per un indice di ricerca unificato.
* **API lato server** – esporre la logica OCR tramite un endpoint REST (Spring Boot lo rende triviale).
* **Librerie alternative** – provare Tesseract via `tess4j` se ti serve una soluzione open‑source.

Ognuno di questi argomenti si basa sui concetti fondamentali trattati in questo **java ocr tutorial**, quindi sentiti libero di sperimentare ed estendere il codice.

---

## Conclusione

Abbiamo percorso un esempio Java completo che **estrae testo da immagine**, mostrando esattamente come **caricare l'immagine per OCR**, configurare le impostazioni della lingua e **usare OCR in Java** per recuperare stringhe leggibili. Lo snippet è autonomo, gestisce gli errori in modo elegante e può essere inserito in qualsiasi progetto Java con il minimo sforzo.  

Provalo, modifica il codice della lingua, e presto trasformerai documenti scansionati in dati ricercabili senza alcuno sforzo. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}