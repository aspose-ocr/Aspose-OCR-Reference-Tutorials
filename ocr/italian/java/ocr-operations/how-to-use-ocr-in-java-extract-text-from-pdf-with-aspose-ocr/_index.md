---
category: general
date: 2026-02-17
description: Come utilizzare l'OCR in Java per estrarre testo da PDF, convertire PDF
  in immagini ed eseguire l'OCR su file PDF scansionati utilizzando Aspose.OCR.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- convert pdf to images
- perform OCR on pdf
- recognize scanned pdf
language: it
og_description: Come utilizzare l'OCR in Java per estrarre testo da file PDF. Impara
  a convertire i PDF in immagini e a riconoscere i PDF scansionati con Aspose.OCR.
og_title: Come utilizzare OCR in Java – Guida completa
tags:
- OCR
- Java
- Aspose
title: Come utilizzare l'OCR in Java – Estrarre testo da PDF con Aspose.OCR
url: /it/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare OCR in Java – Estrarre testo da PDF con Aspose.OCR

Ti sei mai chiesto **come usare OCR** per trasformare un PDF scansionato in testo ricercabile? Non sei l'unico. La maggior parte degli sviluppatori si imbatte in un ostacolo quando un PDF arriva come una serie di immagini, e i tradizionali estrattori di testo non restituiscono nulla. La buona notizia? Con poche righe di Java e Aspose.OCR puoi **estrarre testo da PDF**, **convertire PDF in immagini** e **riconoscere PDF scansionati** in un unico flusso di lavoro senza problemi.

In questo tutorial percorreremo tutto ciò che devi sapere—dalla licenza della libreria alla stampa del risultato finale. Alla fine avrai un programma pronto all'uso che estrae testo semplice da qualsiasi rapporto, fattura o ebook scansionato. Nessun servizio esterno, nessuna magia—solo puro codice Java sotto il tuo controllo.

## Cosa ti serve

- **Java Development Kit (JDK) 8+** – qualsiasi versione recente funziona.  
- **Aspose.OCR for Java** JAR (scaricalo dal sito Aspose).  
- Un **file di licenza Aspose.OCR valido** (`Aspose.OCR.lic`). La versione di prova gratuita funziona, ma una licenza sblocca la massima precisione.  
- Un **PDF scansionato di esempio** (ad es., `scanned-report.pdf`).  
- Un IDE o un semplice editor di testo più un terminale.

È tutto. Nessun Maven, nessun Gradle, nessuna dipendenza extra—solo il JAR di Aspose.OCR nel tuo classpath.

![esempio di utilizzo OCR](image-placeholder.png "esempio di utilizzo OCR")

## Passo 1 – Carica la tua licenza Aspose.OCR (Perché è importante)

Prima che il motore possa funzionare a piena velocità devi indicargli dove si trova la tua licenza. Saltare questo passo forza la libreria in modalità di valutazione, che aggiunge filigrane all'output e può limitare la precisione.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – required for unrestricted OCR
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**Perché funziona:** La classe `License` legge il file `.lic` e lo registra a livello globale. Una volta impostata, ogni `OcrEngine` che crei utilizzerà automaticamente le funzionalità con licenza.

## Passo 2 – Crea il motore OCR (Il motore dietro la magia)

Un'istanza di `OcrEngine` è il cavallo di lavoro che analizza le immagini e restituisce testo. Pensala come il cervello che interpreta i pattern di pixel.

```java
        // Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Consiglio professionale:** Puoi modificare lingua, soglie di confidenza, o persino abilitare l'accelerazione GPU tramite le proprietà del motore. Per la maggior parte dei PDF in inglese le impostazioni predefinite vanno bene.

## Passo 3 – Prepara l'input: aggiungi il tuo PDF (Converti PDF in immagini in background)

Aspose.OCR tratta ogni pagina di un PDF come un'immagine. Quando chiami `addPdf`, la libreria rasterizza silenziosamente ogni pagina, che è esattamente ciò di cui hai bisogno per **convertire PDF in immagini** prima del riconoscimento.

```java
        // Prepare OCR input – each PDF page becomes an image internally
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");
```

**What’s happening:**  
- Il PDF viene aperto.  
- Ogni pagina viene renderizzata a 300 dpi (predefinito) per preservare i dettagli dei caratteri.  
- Gli oggetti bitmap renderizzati vengono memorizzati nella collezione `OcrInput`.

Se hai mai bisogno delle immagini grezze (per il debug o per pre‑elaborazioni personalizzate), chiama `ocrInput.getPages()` dopo questo passo.

## Passo 4 – Esegui il processo OCR (Esegui OCR su PDF)

Ora inizia il lavoro pesante. Il metodo `recognize` itera su ogni immagine, esegue l'algoritmo di riconoscimento e aggrega i risultati in un `OcrResult`.

```java
        // Run OCR on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Perché è importante:** `OcrResult` contiene non solo il testo semplice ma anche i punteggi di confidenza, le bounding box e il riferimento all'immagine originale. Per la maggior parte dei casi d'uso ti basterà `getText()`.

## Passo 5 – Recupera e visualizza il testo estratto

Infine, estrai la stringa di testo semplice dal risultato e stampala. Puoi anche scriverla su un file, inviarla a un indice di ricerca o introdurla in una pipeline NLP a valle.

```java
        // Output the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

### Output previsto

Se `scanned-report.pdf` contiene un semplice paragrafo, vedrai qualcosa del genere:

```
Extracted text:
Quarterly Sales Report
Region: North America
Total Revenue: $4,527,000
...
```

La formattazione esatta rispecchia il layout originale, preservando le interruzioni di riga dove possibile.

## Gestione dei casi limite comuni

### 1. PDF multilingua

Se il tuo documento contiene testo in francese o spagnolo, imposta la lingua prima di chiamare `recognize`:

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);
```

Puoi fornire un array di lingue per consentire al motore di rilevarle automaticamente.

### 2. Scansioni a bassa risoluzione

Quando lavori con scansioni a 150 dpi, aumenta il DPI di rendering interno:

```java
ocrInput.addPdf("low-res.pdf", 600); // render at 600 dpi for better accuracy
```

Un DPI più alto migliora la chiarezza dei caratteri ma consuma più memoria.

### 3. PDF di grandi dimensioni (Gestione della memoria)

Per PDF con decine di pagine, elabora in batch:

```java
int batchSize = 10;
for (int i = 0; i < ocrInput.getPages().size(); i += batchSize) {
    List<OcrPage> batch = ocrInput.getPages().subList(i, Math.min(i + batchSize, ocrInput.getPages().size()));
    OcrInput batchInput = new OcrInput();
    batchInput.getPages().addAll(batch);
    OcrResult batchResult = ocrEngine.recognize(batchInput);
    // Append batchResult.getText() to your final output
}
```

Questo approccio impedisce al heap della JVM di gonfiarsi.

## Esempio completo, pronto all'uso

Di seguito il programma completo—incluse importazioni e gestione della licenza—così puoi copiare‑incollare ed eseguire immediatamente.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (required for full functionality)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Step 2: Create an OCR engine instance that will perform the recognition
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Prepare the OCR input by adding the PDF file.
        // Each page of the PDF is internally converted to an image.
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");

        // Step 4: Run the OCR process on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

Eseguilo con:

```bash
javac -cp "path/to/aspose-ocr.jar" PdfOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" PdfOcrDemo
```

Dovresti vedere il testo estratto stampato sulla console.

## Riepilogo – Cosa abbiamo coperto

- **Come usare OCR** in Java con Aspose.OCR.  
- Il flusso di lavoro per **estrarre testo da PDF**.  
- Internamente, la libreria **converte PDF in immagini** prima di riconoscere i caratteri.  
- Suggerimenti per **eseguire OCR su PDF** con più lingue, scansioni a bassa risoluzione e documenti di grandi dimensioni.  
- Un esempio di codice completo e eseguibile che puoi inserire in qualsiasi progetto Java.

## Prossimi passi e argomenti correlati

Ora che puoi **riconoscere PDF scansionati**, considera queste idee successive:

- **Generazione di PDF ricercabili** – sovrapponi il testo OCR al PDF originale per creare un documento ricercabile.  
- **Servizio di elaborazione batch** – incapsula il codice in un microservizio Spring Boot che accetta PDF via REST.  
- **Integrazione con Elasticsearch** – indicizza il testo estratto per una ricerca full‑text veloce nel tuo repository di documenti.  
- **Pre‑elaborazione delle immagini** – usa OpenCV per correggere l'inclinazione o ridurre il rumore delle pagine prima dell'OCR per una precisione ancora maggiore.

Ognuno di questi argomenti si basa sui concetti fondamentali che abbiamo esplorato, quindi sentiti libero di sperimentare e lasciare che il motore OCR faccia il lavoro pesante.

---

*Buon coding! Se hai incontrato problemi—come errori di licenza o risultati null inaspettati—lascia un commento qui sotto. Sono sempre disponibile per una sessione di debug.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}