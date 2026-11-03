---
category: general
date: 2026-01-12
description: Scopri come riconoscere il testo dalle immagini ed estrarre il testo
  dai file PNG utilizzando Aspose OCR in Java. L'elaborazione parallela lo rende veloce.
draft: false
keywords:
- recognize text from images
- extract text from png
language: it
og_description: Scopri il modo più semplice per riconoscere il testo dalle immagini
  in Java ed estrarre il testo dai file PNG usando Aspose OCR con elaborazione parallela.
og_title: Riconoscere il testo dalle immagini con Java – Guida OCR parallela
tags:
- OCR
- Java
- Aspose
title: Riconoscere il testo dalle immagini con Java – Tutorial OCR parallelo
url: /it/java/advanced-ocr-techniques/recognize-text-from-images-with-java-parallel-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere testo da immagini con Java – Tutorial OCR Parallelo

Hai mai dovuto **riconoscere testo da immagini** ma ti sei bloccato al “come‑faccio?”? Non sei l’unico. Che tu stia digitalizzando fatture, estraendo dati da screenshot o creando un archivio ricercabile, la capacità di *riconoscere testo da immagini* è un vero punto di svolta.  

In questa guida percorreremo un esempio Java completo, pronto all’esecuzione, che non solo **riconosce testo da immagini** ma mostra anche come **estrarre testo da png** usando il motore parallelo integrato di Aspose OCR. Nessuno script esterno, nessun pezzo mancante—solo codice chiaro e spiegazioni semplici.

## Cosa Imparerai

- Configurare Aspose OCR in un progetto Java  
- Abilitare l’elaborazione parallela per velocizzare i lavori batch  
- Caricare una collezione di file PNG e **estrarre testo da png** in modo efficiente  
- Gestire le difficoltà più comuni (file grandi, risultati vuoti, limiti di thread)  
- Visualizzare il codice sorgente completo, eseguibile, alla fine dell’articolo  

Al termine avrai una soluzione copy‑paste che potrai adattare a qualsiasi flusso di lavoro di estrazione di testo basato su immagini.

## Prerequisiti

Prima di iniziare, assicurati di avere:

| Requisito | Perché è importante |
|-----------|----------------------|
| Java 8 o superiore | L’API Java di Aspose OCR richiede Java 8+ |
| Maven o Gradle (per la gestione delle dipendenze) | Semplifica l’aggiunta della libreria Aspose OCR |
| Alcune immagini PNG da elaborare | Il tutorial usa `doc1.png`‑`doc4.png` come esempi |
| Conoscenze di base della sintassi Java | Il codice è lineare, ma dovrai compilarlo ed eseguirlo |

Se ti manca qualcosa, scarica l’ultima JDK da Oracle o AdoptOpenJDK e crea un semplice progetto Maven—nulla di complicato.

![recognize text from images diagram](image.png){alt="diagramma del riconoscimento del testo da immagini"}

## Passo 1 – Aggiungere Aspose OCR al Progetto

Per prima cosa, indica a Maven (o Gradle) di scaricare la libreria Aspose OCR. In un file `pom.xml`, aggiungi:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Se preferisci Gradle, l’equivalente è:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Suggerimento:** Controlla il [repository Maven di Aspose OCR](https://repo.aspose.com/repo) per la versione più recente. Tenere la libreria aggiornata garantisce di avere gli ultimi miglioramenti OCR e le correzioni di bug.

## Passo 2 – Abilitare l’Elaborazione Parallela (il segreto)

Aspose OCR può distribuire il carico di lavoro su più core CPU. È così che manteniamo l’operazione **riconoscere testo da immagini** veloce, anche con decine di file PNG.

```java
// Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Configure parallel options – up to 4 cores in this demo
ParallelOptions parallelOptions = new ParallelOptions();
parallelOptions.setMaxDegreeOfParallelism(4); // Adjust based on your machine
ocrEngine.setParallelOptions(parallelOptions);
```

Perché impostare un limite? Sovraccaricare i thread può privare di risorse altri processi, soprattutto su server condivisi. Quattro core sono un valore di sicurezza per la maggior parte dei desktop; aumentalo se sai che l’hardware può gestirne di più.

## Passo 3 – Preparare l’Elenco dei File PNG

Il tutorial si concentra su **estrarre testo da png**, ma lo stesso codice funziona per JPEG, BMP, ecc. Metti le tue immagini in una cartella e riferiscile così:

```java
String[] imageFiles = {
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
};
```

> **Nota:** Sostituisci `YOUR_DIRECTORY` con il percorso assoluto o relativo dove risiedono i file PNG. Se devi elaborare una cartella dinamica, puoi usare `Files.list(Paths.get("YOUR_DIRECTORY"))` per costruire l’array automaticamente.

## Passo 4 – Eseguire OCR su Ogni Immagine (il motore fa il lavoro pesante)

Anche se abbiamo abilitato il parallelismo, continuiamo a iterare sull’array di file. Aspose OCR distribuisce internamente il lavoro di riconoscimento sui thread configurati.

```java
for (String imagePath : imageFiles) {
    // Load the image into the engine
    ocrEngine.setImage(imagePath);
    
    // Perform recognition
    OcrResult result = ocrEngine.recognize();
    
    // Guard against empty results
    String text = result.getText();
    if (text == null || text.isEmpty()) {
        System.out.println("[" + imagePath + "] => No text found.");
        continue;
    }
    
    // Print a short preview (first 50 characters)
    System.out.println("[" + imagePath + "] => " +
        text.substring(0, Math.min(50, text.length())) + "...");
}
```

### Perché un ciclo e non uno stream parallelo?

Aspose OCR già suddivide l’elaborazione delle immagini internamente in base a `ParallelOptions`. Avvolgere la chiamata in uno stream parallelo esterno raddoppierebbe il lavoro e potrebbe addirittura ridurre le prestazioni. Fidati della libreria per gestire i thread.

## Passo 5 – Casi Limite & Consigli Pratici

| Situazione | Cosa fare |
|------------|-----------|
| **PNG enorme ( > 10 MB )** | Aumenta l’heap JVM (`-Xmx2g`) o ridimensiona l’immagine prima di passarla al motore. |
| **Formati di immagine misti** | Usa `ocrEngine.setImage(new File(imagePath))` – il motore rileva automaticamente il formato. |
| **Serve il testo completo, non solo un’anteprima** | Salva `result.getText()` in un `StringBuilder` o scrivilo su file per analisi successive. |
| **Esecuzione su server CI senza GUI** | Nessun passaggio extra—Aspose OCR è completamente headless. |
| **Scadenza della licenza** | Registra una licenza temporanea con `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` per evitare filigrane di valutazione. |

## Esempio Completo Funzionante

Di seguito la classe Java completa che puoi copiare, incollare ed eseguire. Include tutti gli elementi discussi, più qualche commento per chiarezza.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.parallel.*;

public class ParallelOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create and initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing (up to 4 CPU cores)
        ParallelOptions parallelOptions = new ParallelOptions();
        parallelOptions.setMaxDegreeOfParallelism(4); // Adjust as needed
        ocrEngine.setParallelOptions(parallelOptions);

        // Step 3: Define the PNG files to be processed
        String[] imageFiles = {
            "YOUR_DIRECTORY/doc1.png",
            "YOUR_DIRECTORY/doc2.png",
            "YOUR_DIRECTORY/doc3.png",
            "YOUR_DIRECTORY/doc4.png"
        };

        // Step 4: Recognize text from each image (engine handles parallelism internally)
        for (String imagePath : imageFiles) {
            // Load the image
            ocrEngine.setImage(imagePath);

            // Perform OCR
            OcrResult result = ocrEngine.recognize();

            // Extract the recognized text
            String text = result.getText();

            // Guard against empty results
            if (text == null || text.isEmpty()) {
                System.out.println("[" + imagePath + "] => No text found.");
                continue;
            }

            // Step 5: Output a short preview (first 50 characters)
            System.out.println("[" + imagePath + "] => " +
                text.substring(0, Math.min(50, text.length())) + "...");
        }
    }
}
```

### Output Atteso

Se `doc1.png` contiene la frase “Invoice #12345 – Total $250.00”, vedrai qualcosa di simile:

```
[YOUR_DIRECTORY/doc1.png] => Invoice #12345 – Total $250.00...
[YOUR_DIRECTORY/doc2.png] => No text found.
[YOUR_DIRECTORY/doc3.png] => Customer Name: John Doe...
[YOUR_DIRECTORY/doc4.png] => ...
```

L’anteprima è troncata a 50 caratteri, ma la stringa completa è disponibile in `result.getText()` per qualsiasi elaborazione successiva.

## Conclusione

Ora disponi di un modello solido, pronto per la produzione, per **riconoscere testo da immagini** usando Aspose OCR in Java, e hai visto esattamente come **estrarre testo da png** con accelerazioni parallele. I passaggi principali—configurazione del motore, impostazione del parallelismo, preparazione dell’elenco immagini e gestione dei risultati—sono tutti coperti, insieme a una serie di consigli pratici per evitare problemi comuni.

Qual è il prossimo passo? Prova a sostituire l’elenco PNG con una scansione dinamica della directory, indirizza l’output OCR verso un indice di ricerca come Elasticsearch, o sperimenta le impostazioni OCR specifiche per lingua (`ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH)`). Il cielo è il limite una volta padroneggiato il flusso di lavoro di base.

Se hai incontrato difficoltà o hai idee per ampliare questo tutorial, lascia un commento qui sotto. Buon coding e buona trasformazione di quelle immagini ostinate in testo ricercabile!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}