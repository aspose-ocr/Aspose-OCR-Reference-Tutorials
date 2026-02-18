---
category: general
date: 2026-02-17
description: Scopri come utilizzare l'OCR in Java per riconoscere il testo da file
  immagine, estrarre il testo da ricevute PNG e convertire la ricevuta in JSON con
  Aspose OCR.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from png
- convert receipt to json
language: it
og_description: Guida passo passo su come utilizzare l'OCR in Java per riconoscere
  il testo da un'immagine, estrarre il testo dalle ricevute PNG e convertire la ricevuta
  in JSON.
og_title: Come usare OCR in Java – Riconoscere il testo da un'immagine
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Come usare l'OCR in Java – Riconosci rapidamente il testo da un'immagine
url: /it/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/
---

translations and placeholders unchanged.

Let's construct final.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare OCR in Java – Riconoscere rapidamente il testo da un'immagine

Ti sei mai chiesto **come usare OCR** per estrarre il testo da una foto di una ricevuta? Forse hai provato alcuni strumenti online, solo per finire con caratteri incomprensibili o un formato che non riesci a analizzare. La buona notizia è che con poche righe di codice Java puoi **recognize text from image** files, **extract text from PNG** receipts, e persino **convert receipt to JSON** per l'elaborazione successiva.  

In questo tutorial ti guideremo attraverso l'intero flusso di lavoro—dalla licenza della libreria Aspose OCR fino all'ottenimento di un payload JSON pulito che puoi inserire in un database o in un modello di machine‑learning. Nessuna teoria superflua, solo un esempio pratico e eseguibile che puoi copiare‑incollare nel tuo IDE. Alla fine avrai un programma autonomo che prende `receipt.png` e restituisce una stringa JSON pronta all'uso.

## Cosa ti servirà

- **Java Development Kit (JDK) 8+** – qualsiasi versione recente funziona.  
- **Aspose OCR for Java** library (l'artifact Maven è `com.aspose:aspose-ocr`).  
- Un **valid Aspose OCR license file** (`Aspose.OCR.lic`). La versione di prova gratuita funziona per i test, ma una licenza corretta rimuove i limiti di valutazione.  
- Un file immagine (PNG, JPEG, ecc.) che contiene il testo che vuoi leggere—chiamiamolo `receipt.png` e posizionalo in una cartella nota.  
- Il tuo IDE preferito (IntelliJ IDEA, Eclipse, VS Code…) – sei libero di scegliere.

> **Consiglio professionale:** Tieni il file di licenza al di fuori della cartella sorgente e fai riferimento ad esso tramite un percorso assoluto o relativo per evitare di commetterlo al controllo versione.

Ora che i prerequisiti sono chiari, immergiamoci nel codice reale.

## Come usare OCR – Passaggi fondamentali

Di seguito trovi una panoramica ad alto livello delle azioni che eseguiremo:

1. **Load the Aspose OCR library** and apply your license.  
2. **Create an `OcrEngine` instance** – this is the engine that does the heavy lifting.  
3. **Prepare an `OcrInput` object** pointing at the image you want to process.  
4. **Call `recognize` with `ResultFormat.JSON`** to get a JSON representation of the extracted text.  
5. **Handle the JSON output** – print it, write it to a file, or parse it further.

Ogni passaggio è spiegato in dettaglio nelle sezioni successive.

## Passo 1 – Installa Aspose OCR e applica la tua licenza

Per prima cosa, aggiungi la dipendenza Aspose OCR al tuo `pom.xml` se usi Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Ora, nel tuo codice Java, carica la licenza. Questo passaggio è fondamentale; senza di esso la libreria funziona in modalità di valutazione e può inserire filigrane nell'output.

```java
import com.aspose.ocr.*;

public class OcrSetup {
    public static void applyLicense() throws Exception {
        // Replace the path with the actual location of your Aspose.OCR.lic file
        License ocrLicense = new License();
        ocrLicense.setLicense("C:/licenses/Aspose.OCR.lic");
    }
}
```

> **Why this matters:** L'oggetto `License` informa il motore OCR che sei autorizzato a utilizzare l'intero set di funzionalità, che include il riconoscimento ad alta precisione e l'esportazione JSON. Saltare questo passaggio ti permetterà comunque di **recognize text from image**, ma i risultati potrebbero essere limitati.

## Passo 2 – Crea l'istanza del motore OCR

La classe `OcrEngine` è il punto di ingresso per tutte le operazioni OCR. Pensala come il “cervello” che legge i pixel e decide quali caratteri rappresentano.

```java
import com.aspose.ocr.*;

public class OcrEngineFactory {
    public static OcrEngine createEngine() {
        // No special configuration needed for basic usage
        return new OcrEngine();
    }
}
```

Puoi personalizzare il motore (ad esempio impostare la lingua, abilitare il deskew) in seguito se le tue ricevute contengono script non latini o sono scansionate con un angolo. Per la maggior parte delle ricevute statunitensi, le impostazioni predefinite funzionano perfettamente.

## Passo 3 – Carica l'immagine da elaborare

Ora indicheremo al motore OCR il file che contiene la ricevuta. La classe `OcrInput` può accettare più immagini, ma per questo tutorial la manterremo semplice con un unico PNG.

```java
import com.aspose.ocr.*;

public class ImageLoader {
    public static OcrInput loadImage(String imagePath) {
        OcrInput input = new OcrInput();
        // Add the PNG receipt – this is where we **extract text from PNG**
        input.add(imagePath);
        return input;
    }
}
```

Se mai dovessi **extract text from PNG** in blocco, chiama semplicemente `input.add()` più volte o passa un elenco di percorsi file.

## Passo 4 – Riconosci il testo e converti la ricevuta in JSON

Ecco il cuore del tutorial. Chiediamo al motore di riconoscere il testo e di restituire il risultato in formato JSON. Il flag `ResultFormat.JSON` fa tutto il lavoro pesante per noi.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonRecognizer {
    public static String recognizeToJson(OcrEngine engine, OcrInput input) throws Exception {
        // Perform OCR and request JSON output
        OcrResult result = engine.recognize(input, ResultFormat.JSON);
        // Retrieve the JSON string
        return result.getJson();
    }
}
```

Il payload JSON include ogni linea riconosciuta, il suo riquadro di delimitazione, il punteggio di confidenza e il testo grezzo. Questa struttura rende banale **convert receipt to JSON** e poi inviarlo a qualsiasi API downstream.

## Passo 5 – Metti tutto insieme ed esegui il programma

Di seguito trovi la classe Java completa, pronta per l'esecuzione, che unisce tutti i passaggi. Salvala come `JsonExportDemo.java` (o con un nome a tua scelta) ed eseguila dal tuo IDE o da riga di comando.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonExportDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license (replace with your actual license file)
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.lic"); // <-- adjust path if needed

        // 2️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Prepare the input image that contains the text to be recognized
        OcrInput ocrInput = new OcrInput();
        // Replace with the absolute or relative path to your receipt PNG
        ocrInput.add("YOUR_DIRECTORY/receipt.png"); // <-- **extract text from PNG** here

        // 4️⃣ Perform recognition and request the result in JSON format
        OcrResult ocrResult = ocrEngine.recognize(ocrInput, ResultFormat.JSON);

        // 5️⃣ Retrieve the JSON string from the result
        String jsonResult = ocrResult.getJson();

        // 6️⃣ Output the JSON (or save it to a file for further processing)
        System.out.println(jsonResult);
    }
}
```

### Output previsto

L'esecuzione del programma stampa una stringa JSON simile a quella seguente (il contenuto esatto dipende dalla tua ricevuta):

```json
{
  "pages": [
    {
      "lines": [
        {
          "text": "Store Name",
          "confidence": 0.99,
          "boundingBox": [12, 34, 200, 45]
        },
        {
          "text": "Date: 2024-02-15",
          "confidence": 0.98,
          "boundingBox": [12, 60, 180, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.97,
          "boundingBox": [12, 120, 150, 45]
        }
      ]
    }
  ]
}
```

Ora puoi inviare questo JSON a un database, a un endpoint REST o a una pipeline di analisi dati. Il passaggio **convert receipt to JSON** è già stato eseguito per te.

## Domande comuni e casi particolari

### E se l'immagine è ruotata?

Aspose OCR rileva e corregge automaticamente rotazioni lievi. Per immagini fortemente inclinate, chiama `engine.getImagePreprocessingOptions().setDeskew(true)` prima del riconoscimento.

### Come gestire più lingue?

Usa `engine.getLanguage()` per impostare la lingua desiderata, ad esempio `engine.setLanguage(Language.FRENCH)`. Questo è utile quando devi **recognize text from image** che contiene ricevute multilingue.

### Posso ottenere testo semplice invece di JSON?

Assolutamente. Sostituisci `ResultFormat.JSON` con `ResultFormat.TEXT` e chiama `result.getText()`.

### È possibile limitare l'OCR a una regione specifica?

Sì—usa `ocrInput.add(imagePath, new Rectangle(x, y, width, height))` per focalizzarti sull'area della ricevuta, il che può migliorare velocità e precisione.

## Consigli professionali per OCR pronto alla produzione

- **Cache della licenza** se stai elaborando molti file in un ciclo; crearla ripetutamente aggiunge overhead.  
- **Elaborazione batch**: carica tutti i percorsi delle ricevute in un unico `OcrInput` e chiama `recognize` una sola volta. Il JSON conterrà un array di pagine, ciascuna con le proprie linee.  
- **Convalida JSON**: dopo aver ottenuto la stringa, analizzala con una libreria come Jackson per assicurarti che sia ben formata prima di archiviarla.  
- **Monitora la confidenza**: il JSON include un campo `confidence` per ogni linea. Filtra le linee al di sotto di una soglia (es. 0.85) per evitare dati spazzatura.  
- **Proteggi la tua licenza**: conserva `Aspose.OCR.lic` in un vault sicuro o in una variabile d'ambiente, specialmente nelle distribuzioni cloud.

## Conclusione

Abbiamo coperto **how to use OCR** in Java per **recognize text from image**, **extract text from PNG** receipts e **convert receipt to JSON**—tutto con un esempio conciso, end‑to‑end. I passaggi sono semplici, il codice è completamente eseguibile e l'output JSON ti fornisce una rappresentazione strutturata pronta per qualsiasi sistema downstream.

Successivamente potresti esplorare scenari più avanzati: inviare il JSON ad Apache Kafka per l'elaborazione in tempo reale, applicare pattern regex per estrarre i totali delle voci, o integrare un servizio OCR cloud per scalabilità. Qualunque sia la tua scelta, i fondamenti appena appresi rimarranno gli stessi.

Hai domande o hai incontrato un problema provando questo esempio? Lascia un commento qui sotto e risolviamo insieme. Buon coding e divertiti a trasformare quelle immagini di ricevute disordinate in dati puliti e ricercabili!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}