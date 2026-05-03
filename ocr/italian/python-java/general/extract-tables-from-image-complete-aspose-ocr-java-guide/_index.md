---
category: general
date: 2026-05-03
description: Estrai tabelle da un'immagine usando Aspose OCR Java. Impara a caricare
  l'immagine per l'OCR, estrarre la tabella da un PNG, convertire il testo della tabella
  dell'immagine e riconoscere rapidamente l'immagine di una ricevuta.
draft: false
keywords:
- extract tables from image
- extract table from png
- load image for ocr
- convert image table text
- recognize receipt image
language: it
og_description: Estrai tabelle da un'immagine con Aspose OCR Java. Questa guida mostra
  come caricare l'immagine per l'OCR, estrarre la tabella da un PNG, convertire il
  testo della tabella dell'immagine e riconoscere l'immagine della ricevuta.
og_title: Estrai tabelle dall'immagine – Tutorial Java OCR di Aspose
tags:
- Aspose OCR
- Java
- Image Processing
title: Estrai tabelle dall'immagine – Guida completa Aspose OCR Java
url: /it/python-java/general/extract-tables-from-image-complete-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai tabelle da immagine – Guida completa Aspose OCR Java

Ti è mai capitato di dover **estrarre tabelle da immagine** ma di scontrarti con un ostacolo? Forse hai una ricevuta scansionata o una fattura fotografata e i dati tabulari sono sepolti in un PNG. In questo tutorial vedrai esattamente come *caricare immagine per OCR*, trasformare quell’immagine in righe strutturate e **convertire il testo della tabella dell'immagine** in qualcosa con cui puoi lavorare in Java.  

Passeremo in rassegna ogni passaggio, dalla licenza del motore Aspose OCR alla stampa di ogni cella delle tabelle rilevate. Alla fine sarai in grado di **riconoscere immagini di ricevute** e estrarre le loro tabelle senza alcuno sforzo.

## Cosa imparerai

- Come inizializzare il motore Aspose OCR e applicare la tua licenza.
- Perché abilitare il rilevamento delle tabelle è la chiave per **estrarre tabelle da immagine**.
- Il codice esatto necessario per **caricare immagine per OCR** ed eseguire il riconoscimento su un PNG.
- Modi per gestire tabelle multiple, scansioni a bassa risoluzione e problemi comuni.
- Come **convertire il testo della tabella dell’immagine** in un formato stampabile (o pronto per il database).

Nessuna documentazione esterna necessaria—tutto ciò che ti serve è qui.

## Prerequisiti

- Java 17 o superiore (il codice utilizza il moderno sistema di moduli).
- Un file di licenza Aspose OCR per Java (`Aspose.OCR.Java.lic`). Se stai solo sperimentando, anche una chiave di valutazione temporanea funziona.
- Un’immagine PNG che contiene una tabella chiara (ad es., `receipt_with_table.png`).  
- Maven o Gradle per scaricare la dipendenza Aspose OCR:

```xml
<!-- Maven snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

> **Consiglio professionale:** Mantieni il file di licenza accanto alla cartella `src/main/resources` in modo che il percorso rimanga stabile tra gli ambienti.

---

## Passo 1 – Inizializza il motore OCR per **estrarre tabelle da immagine**

Prima che il motore possa fare qualcosa, deve sapere che sei un utente legittimo.

```java
import com.aspose.ocr.*;

public class TableExtractor {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Apply your Aspose OCR license – this removes evaluation watermarks
        License license = new License();
        license.setLicense("Aspose.OCR.Java.lic");
        ocrEngine.setLicense(license);
```

*Perché è importante:* Senza una licenza valida il motore OCR funziona in modalità di prova, il che può troncare i risultati o aggiungere filigrane indesiderate—rendendo l'estrazione delle tabelle inaffidabile.

---

## Passo 2 – Abilita il rilevamento delle tabelle (**estrarre tabella da png**)

Il rilevamento delle tabelle non è attivo per impostazione predefinita; devi attivarlo.

```java
        // Step 2: Turn on table detection so the engine looks for tabular structures
        ocrEngine.getConfig().setEnableTableDetection(true);
```

Abilitare questo flag indica ad Aspose OCR di trattare gruppi di testo allineato come righe e colonne, che è esattamente ciò di cui hai bisogno quando vuoi **estrarre tabelle da immagine** in file PNG.

---

## Passo 3 – **Caricare immagine per OCR** e **riconoscere immagine di ricevuta**

Ora carichiamo effettivamente l’immagine nel motore.

```java
        // Step 3: Load the PNG that contains the table
        // You can also use Image.fromStream(...) for in‑memory data
        Image inputImage = Image.fromFile("YOUR_DIRECTORY/receipt_with_table.png");

        // Run the recognition process – this returns an OcrResult object
        OcrResult ocrResult = ocrEngine.recognize(inputImage);
```

Se ti trovi in uno scenario di **riconoscere immagine di ricevuta**, potresti voler pre‑processare l’immagine (raddrizzare, aumentare il contrasto). Questo è al di fuori dello scopo di questa breve guida, ma vale la pena esplorarlo per scansioni rumorose.

---

## Passo 4 – Elabora il risultato OCR e **converti il testo della tabella dell’immagine**

L'oggetto `OcrResult` può contenere una o più tabelle. Iteriamo su di esse e stampiamo ogni cella.

```java
        // Step 4: Iterate over every detected table
        if (ocrResult.getTables().isEmpty()) {
            System.out.println("No tables were detected. Try improving image quality.");
            return;
        }

        for (Table table : ocrResult.getTables()) {
            System.out.println("Table detected:");
            for (TableRow row : table.getRows()) {
                // Join each cell's text with a tab for easy copy‑paste
                String line = row.getCells()
                                 .stream()
                                 .map(Cell::getText)
                                 .reduce((a, b) -> a + "\t" + b)
                                 .orElse("");
                System.out.println(line);
            }
            System.out.println(); // Blank line between tables
        }
    }
}
```

**Cosa fa:**  

- Verifica se sono state trovate tabelle; in caso contrario, suggerisce una regolazione della qualità.  
- Per ogni tabella, stampa le righe con celle separate da tabulazioni, un formato comodo per le importazioni CSV.  
- La chiamata `Cell::getText` è il cuore di **convertire il testo della tabella dell’immagine** – estrae la stringa OCR grezza da ogni cella.

### Output previsto

Assumendo che `receipt_with_table.png` contenga una semplice tabella 3 × 2, vedrai qualcosa del genere:

```
Table detected:
Item	Quantity
Apple	2
Banana	5
```

Se l’immagine contiene più tabelle, ciascuna sarà separata da una riga vuota.

---

## Passo 5 – Verifica le tabelle estratte e gestisci i casi limite

### Problemi comuni

| Problema | Perché succede | Soluzione rapida |
|----------|----------------|------------------|
| **Nessuna tabella rilevata** | Immagine troppo sfocata o a basso contrasto | Applicare la binarizzazione (`ImageProcessing.applyThreshold`) prima di OCR |
| **Celle unite** | Le linee della tabella sono deboli, OCR le tratta come un unico blocco | Aumentare `TableDetectionSensitivity` in `ocrEngine.getConfig()` |
| **Ordine colonne errato** | Immagine inclinata che causa disallineamento | Usare `ImageProcessing.deskew` o ruotare l’immagine di 90° |

### Cosa fare dopo

- **Esporta in CSV** – sostituisci `System.out.println(line);` con un `FileWriter` per salvare i dati.  
- **Inserisci in un database** – mappa ogni riga a un POJO e usa JPA per la persistenza.  
- **Combina con altre API** – per l’elaborazione delle ricevute potresti anche estrarre i totali usando espressioni regolari sul testo OCR.

---

## Esempio completo funzionante (pronto per copia‑incolla)

```java
import com.aspose.ocr.*;

public class TableExtractor {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine and apply license
        OcrEngine ocrEngine = new OcrEngine();
        License license = new License();
        license.setLicense("Aspose.OCR.Java.lic");
        ocrEngine.setLicense(license);

        // Enable table detection – crucial for extracting tables from image
        ocrEngine.getConfig().setEnableTableDetection(true);

        // Load the PNG image (replace with your actual path)
        Image inputImage = Image.fromFile("YOUR_DIRECTORY/receipt_with_table.png");

        // Recognize the image – this step performs OCR on the whole picture
        OcrResult ocrResult = ocrEngine.recognize(inputImage);

        // Verify we have tables; otherwise suggest a quality fix
        if (ocrResult.getTables().isEmpty()) {
            System.out.println("No tables were detected. Try improving image quality.");
            return;
        }

        // Print each table row by row, converting image table text into tab‑separated values
        for (Table table : ocrResult.getTables()) {
            System.out.println("Table detected:");
            for (TableRow row : table.getRows()) {
                String line = row.getCells()
                                 .stream()
                                 .map(Cell::getText)
                                 .reduce((a, b) -> a + "\t" + b)
                                 .orElse("");
                System.out.println(line);
            }
            System.out.println(); // Blank line between tables
        }
    }
}
```

Esegui questo programma, puntalo a un PNG che contiene una tabella chiara, e osserva la console riempirsi di righe formattate ordinatamente.

---

## Conclusione

Ora disponi di una soluzione solida, end‑to‑end, per **estrarre tabelle da immagine** usando Aspose OCR per Java. Dalla licenza a **caricare immagine per OCR**, abilitando **estrarre tabella da png**, e infine **convertire il testo della tabella dell’immagine**, ogni passaggio è coperto da spiegazioni e consigli pratici.  

Successivamente, prova a concatenare l’output in un file CSV, inserire le righe in un database relazionale, o combinare il passaggio OCR con una routine di estrazione del totale della ricevuta. Lo stesso schema funziona per fatture, listini prezzi e qualsiasi documento scansionato che nasconde dati dietro una griglia.

Hai domande su come gestire ricevute a bassa risoluzione o scalare questo a elaborazioni batch? Lascia un commento qui sotto, e buona programmazione!  

![Esempio di estrazione tabelle da immagine](https://example.com/assets/extract-tables-from-image.png "Estrai tabelle da immagine – output di esempio")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}