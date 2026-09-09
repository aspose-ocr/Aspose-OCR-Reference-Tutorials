---
category: general
date: 2026-01-02
description: Crea PDF ricercabile da un PDF di immagini scannerizzate usando Aspose
  OCR. Impara a impostare la lingua OCR, incorporare un PDF con livello di testo e
  applicare opzioni PDF ad alta compressione.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- high compression pdf
- embed text layer pdf
- set OCR language
language: it
og_description: Crea PDF ricercabili rapidamente. Questa guida mostra come convertire
  PDF di immagini scannerizzate, incorporare un livello di testo, impostare la lingua
  OCR e abilitare la compressione PDF ad alta efficienza.
og_title: Crea PDF ricercabile con Aspose OCR – Guida completa
tags:
- Aspose OCR
- Java PDF
- Document Automation
title: Crea PDF Ricercabile con Aspose OCR – Guida Passo‑Passo
url: /it/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea PDF Ricercabile – Tutorial di Programmazione Completo

Hai mai dovuto **creare PDF ricercabili** a partire da immagini scannerizzate ma non sapevi da dove cominciare? Non sei solo. In molti flussi di lavoro ricchi di documenti, un PDF costituito solo da immagini è un vicolo cieco per la ricerca e l'indicizzazione.  

La buona notizia è che con Aspose OCR puoi **convertire PDF di immagini scannerizzate** in un documento completamente ricercabile con poche righe di Java. Questo tutorial ti guida passo passo—dall’inizializzazione del motore OCR, alla configurazione delle impostazioni PDF ad alta compressione, all’inserimento di un livello di testo nascosto, fino alla scelta della lingua OCR corretta.

Alla fine di questa guida avrai un programma eseguibile che produce un PDF ricercabile, un file che potrai inserire in qualsiasi motore di ricerca o sistema di gestione documentale senza problemi.

---

## Crea PDF Ricercabile – Panoramica

Prima di immergerci nel codice, chiarifichiamo cosa significa realmente “creare PDF ricercabile”. Un PDF ricercabile contiene due livelli paralleli:

1. **Livello visivo** – l’immagine scannerizzata originale (o la pagina renderizzata).  
2. **Livello di testo** – caratteri invisibili ma leggibili dalla macchina, estratti tramite OCR.

Quando apri un PDF di questo tipo in Adobe Reader e selezioni del testo, interagisci in realtà con il livello di testo nascosto, non con l’immagine. Questo approccio a doppio livello è ciò che consente la funzionalità **embed text layer PDF**.

---

## Converti PDF di Immagine Scannerizzata con Aspose OCR

La prima cosa di cui hai bisogno è un’immagine scannerizzata (PNG, JPEG, TIFF) che vuoi trasformare in PDF. Aspose OCR può leggere quell’immagine, eseguire l’OCR e passare il risultato a un writer PDF.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Step 2: Configure PDF save options to embed a searchable text layer
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // enable searchable PDF
        pdfSaveOptions.setCompressionLevel(9);        // optional: high compression

        // Step 3: Perform OCR on the scanned image and save the result as a searchable PDF
        ocrEngine.recognizeImageAndSave(
                "YOUR_DIRECTORY/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,                // set OCR language
                "YOUR_DIRECTORY/output.pdf",                // output PDF file
                pdfSaveOptions);                            // options defined above

        // Step 4: Indicate that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

**Perché funziona:**  
- `setCreateSearchablePdf(true)` indica ad Aspose di generare il livello di testo nascosto, soddisfacendo il requisito **embed text layer pdf**.  
- `setCompressionLevel(9)` spinge il file nella fascia **high compression pdf**, riducendo le dimensioni finali senza compromettere la precisione dell’OCR.  
- L’argomento `RecognitionLanguage.ENGLISH` mostra come **set OCR language**; puoi sostituirlo con francese, tedesco, ecc., a seconda del materiale di partenza.

---

## Impostazioni PDF ad Alta Compressione

I PDF scannerizzati di grandi dimensioni possono rapidamente gonfiarsi fino a centinaia di megabyte. Aspose offre una semplice API di compressione che opera a livello PDF. Il metodo `setCompressionLevel` accetta valori da 0 (nessuna compressione) a 9 (compressione massima).  

```java
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.setCompressionLevel(9); // 9 = strongest compression
```

Alcuni consigli:

- **Usa formati immagine lossless** (PNG) per scansioni ricche di testo; JPEG è migliore per le foto.  
- **Abilita il subset dei font** se incorpori font personalizzati—Aspose lo fa automaticamente quando crei un PDF ricercabile.  
- **Verifica la dimensione dell’output** dopo ogni modifica; a volte una compressione di livello 8 ti offre una riduzione del 10 % della dimensione con una perdita di qualità trascurabile rispetto al livello 9.

---

## Inserisci Livello di Testo PDF per la Ricercabilità

Se ometti la chiamata `setCreateSearchablePdf(true)`, il file risultante avrà un aspetto corretto ma non potrai cercarne il contenuto. Il livello di testo nascosto viene creato mappando ogni carattere riconosciuto alla sua posizione sulla pagina.  

```java
pdfSaveOptions.setCreateSearchablePdf(true);
```

**Cosa tenere d’occhio:**  

- **Documenti multilingue** – potresti dover eseguire l’OCR due volte, una per lingua, e poi unire i livelli di testo.  
- **Layout complessi** (tabelle, colonne multiple) – Aspose fa un buon lavoro, ma controlla l’output con un visualizzatore PDF che mostri il testo nascosto (ad esempio la modalità “Edit PDF” di Adobe Acrobat).

---

## Imposta la Lingua OCR per un Riconoscimento Accurato

L’accuratezza del motore OCR dipende dalla lingua che gli indichi di aspettarsi. Aspose fornisce un set di lingue integrate, e puoi anche aggiungere pacchetti linguistici personalizzati.

```java
ocrEngine.recognizeImageAndSave(
        "input.png",
        RecognitionLanguage.ENGLISH, // change to RecognitionLanguage.FRENCH, etc.
        "output.pdf",
        pdfSaveOptions);
```

**Quando cambiare lingua:**  

- I documenti contengono **script non latini** (Cirillico, Arabo) – passa alla `RecognitionLanguage` appropriata.  
- Pagine con lingue miste – puoi chiamare `recognizeImageAndSave` due volte, ciascuna volta con una lingua diversa, e poi unire i PDF.

---

## Esecuzione dell’Esempio Completo

Di seguito trovi il programma completo, pronto per l’esecuzione. Sostituisci i percorsi segnaposto con i percorsi reali dei file, assicurati che il JAR di Aspose OCR sia nel classpath, ed esegui.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Configure PDF save options
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // embed text layer PDF
        pdfSaveOptions.setCompressionLevel(9);        // high compression PDF

        // Perform OCR and save searchable PDF
        ocrEngine.recognizeImageAndSave(
                "C:/scans/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,          // set OCR language
                "C:/output/searchable.pdf",           // output PDF
                pdfSaveOptions);                      // options defined above

        System.out.println("Searchable PDF created.");
    }
}
```

**Output previsto:** Quando esegui il programma, la console stampa:

```
Searchable PDF created.
```

Apri `searchable.pdf` in qualsiasi visualizzatore PDF, prova a selezionare del testo e vedrai il livello invisibile in azione. Hai creato con successo **create searchable pdf** da un’immagine scannerizzata.

---

![create searchable pdf example](image-placeholder.png "create searchable pdf example")

*Lo screenshot sopra (segnaposto) mostrerebbe tipicamente il visualizzatore PDF con testo selezionabile sopra una pagina scannerizzata.*

---

## Conclusione

Abbiamo coperto tutto ciò che ti serve per **create searchable PDF** usando Aspose OCR:

- Inizializzare il motore OCR.  
- **Convertire PDF di immagine scannerizzata** passando un PNG/JPEG a `recognizeImageAndSave`.  
- Usare `setCreateSearchablePdf(true)` per **embed text layer PDF**.  
- Applicare `setCompressionLevel(9)` per un **high compression PDF** leggero.  
- Scegliere la `RecognitionLanguage` corretta per **set OCR language** e massimizzare l’accuratezza.

Da qui puoi sperimentare con l’elaborazione batch, lingue diverse, o persino combinare più pagine scannerizzate in un unico PDF ricercabile. Lo stesso schema funziona per altre lingue come lo spagnolo o il giapponese—basta sostituire l’enum `RecognitionLanguage`.

Sentiti libero di lasciare un commento se incontri difficoltà, e buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}