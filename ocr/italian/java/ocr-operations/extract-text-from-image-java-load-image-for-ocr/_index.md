---
category: general
date: 2026-04-29
description: estrarre testo da un'immagine in Java usando Aspose OCR – impara come
  caricare l'immagine per l'OCR e riconoscere il testo da una ricevuta in formato
  JSON.
draft: false
keywords:
- extract text from image java
- load image for OCR
- recognize text from receipt
- Aspose OCR Java
- JSON OCR result
language: it
og_description: estrarre testo da immagine java con Aspose OCR. Questo tutorial mostra
  come caricare un'immagine per OCR e riconoscere il testo da una ricevuta, restituendo
  JSON.
og_title: Estrai testo da immagine Java – Guida completa
tags:
- Java
- OCR
- Aspose
title: estrarre testo da immagine Java – caricare immagine per OCR
url: /it/java/ocr-operations/extract-text-from-image-java-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# estrarre testo da immagine java – Guida completa

Hai mai avuto bisogno di **estrarre testo da immagine java** ma non sapevi quale libreria scegliere? Non sei solo. Molti sviluppatori si trovano in difficoltà quando provano a caricare un'immagine per OCR e poi ricevono il testo grezzo in un formato difficile da gestire.  

In questo tutorial vedremo una soluzione pulita, end‑to‑end, che non solo **carica immagine per OCR** ma anche **riconosce testo da ricevuta** e restituisce una stringa JSON ordinata. Alla fine avrai una classe Java pronta all'uso che potrai inserire in qualsiasi progetto—senza ulteriori complicazioni.

## Cosa imparerai

- Come configurare Aspose OCR per Java (la libreria che rende il lavoro pesante indolore).  
- I passaggi esatti per **caricare immagine per OCR** dal disco.  
- Come configurare il motore per restituire i risultati in JSON, perfetto per l'elaborazione a valle.  
- Come **riconoscere testo da ricevuta** nelle immagini e verificare l'output.  

Non è necessaria alcuna esperienza pregressa con Aspose; basta un JDK funzionante e un IDE con cui ti trovi a tuo agio.

## Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------|
| **Java 17+** (or any recent JDK) | Aspose OCR fornisce binari compilati per runtime Java moderni. |
| **Maven or Gradle** (to pull the Aspose OCR dependency) | Rende la gestione delle dipendenze un gioco da ragazzi. |
| **A sample receipt image** (e.g., `receipt.png`) | Useremo questo file per dimostrare **riconoscere testo da ricevuta**. |
| **Internet connection** (once) | Necessaria per scaricare il JAR di Aspose la prima volta. |

Se li hai già, ottimo—tuffiamoci.

## Passo 1: Aggiungi Aspose OCR al tuo progetto

La prima cosa di cui hai bisogno è la libreria Aspose OCR. Se usi Maven, aggiungi il seguente snippet al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

Per Gradle, appare così:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Suggerimento:** Blocca il numero di versione. Aggiornare in seguito può introdurre sottili cambiamenti API che rompono il tuo codice.

Una volta risolta la dipendenza, sei pronto a scrivere codice Java che effettivamente **estrae testo da immagine java**.

## Passo 2: Carica l'immagine per OCR

Ora mostreremo la riga esatta che **carica immagine per OCR**. Aspose fornisce un comodo helper `ImageStream.fromFile`.

```java
// Step 2: Load the image you want to process
ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

Sostituisci `YOUR_DIRECTORY` con il percorso assoluto o relativo al tuo file di ricevuta. Se il percorso è errato, il motore lancerà una `FileNotFoundException`, quindi ricontrolla l'ortografia.

> **Perché è importante:** Caricare correttamente l'immagine è la base. Se l'immagine non viene letta, il motore OCR non ha nulla da riconoscere e otterrai un risultato JSON vuoto.

## Passo 3: Indica al motore di restituire JSON

Aspose OCR può emettere XML, testo semplice o JSON. Per le API moderne JSON è il più flessibile, quindi imposteremo il formato esplicitamente.

```java
ocrEngine.getResultSettings()
         .setResultFormat(OcrResultFormat.JSON); // XML is also available
```

Puoi passare a `OcrResultFormat.XML` con una sola modifica se il tuo sistema a valle preferisce XML. L'API è progettata per essere intercambiabile.

## Passo 4: Esegui il processo di riconoscimento

Con l'immagine caricata e il formato impostato, il passo successivo è effettivamente **riconoscere testo da ricevuta**. Qui avviene il lavoro pesante.

```java
// Step 4: Perform OCR
OcrResult ocrResult = ocrEngine.recognize();
```

La chiamata `recognize()` blocca fino a quando il motore termina l'analisi dell'immagine. Per immagini grandi potresti volerla eseguire in un thread in background, ma per una tipica ricevuta termina in una frazione di secondo.

## Passo 5: Recupera il risultato JSON

Infine, estraiamo la stringa JSON grezza e la stampiamo. Questa stringa contiene ogni pezzo di testo riconosciuto, il suo riquadro di delimitazione, i punteggi di confidenza e altro.

```java
// Step 5: Retrieve the JSON string
String jsonResult = ocrResult.getResultAsString();
System.out.println(jsonResult);
```

### Output previsto

Eseguendo il programma completo su una ricevuta chiara si ottiene qualcosa di simile:

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "rectangle": { "x": 12, "y": 15, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2026-04-28",
          "confidence": 0.95,
          "rectangle": { "x": 12, "y": 50, "width": 180, "height": 20 }
        },
        {
          "text": "Total $23.45",
          "confidence": 0.99,
          "rectangle": { "x": 12, "y": 120, "width": 150, "height": 25 }
        }
      ]
    }
  ]
}
```

Nota come ogni riga della ricevuta sia un blocco separato con un punteggio di confidenza. Ora puoi inviare questo JSON a qualsiasi sistema a valle—memorizzarlo in un database, inviarlo via HTTP o alimentarlo a un modello di machine‑learning.

## Esempio completo funzionante

Di seguito trovi la classe Java completa e autonoma che mette tutto insieme. Copiala, regola il percorso dell'immagine e esegui `mvn compile exec:java` (o il comando equivalente di Gradle).

```java
import com.aspose.ocr.*;

public class JsonExportExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Make sure the path points to a real receipt image on your machine
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Configure the engine to return results in JSON format
        ocrEngine.getResultSettings()
                 .setResultFormat(OcrResultFormat.JSON); // XML is also available

        // Step 4: Run the OCR recognition process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Retrieve the raw JSON string and output it
        String jsonResult = ocrResult.getResultAsString();
        System.out.println(jsonResult);
    }
}
```

> **Attenzione a:**  
> • **Errori di percorso file** – ricontrolla le barre su Windows vs. macOS/Linux.  
> • **Out‑of‑memory** – immagini grandi potrebbero richiedere `ocrEngine.setMemoryOptimization(true)`.  
> • **Impostazioni della lingua** – se la tua ricevuta contiene caratteri non latini, chiama `ocrEngine.setLanguage(OcrLanguage.SPANISH)` (o qualsiasi lingua supportata) prima di `recognize()`.

## Testare la soluzione

1. **Esegui il programma** – dovresti vedere un blob JSON stampato sulla console.  
2. **Valida il JSON** – copia l'output su <https://jsonlint.com/> per assicurarti che sia ben formato.  
3. **Analizzalo** – in un progetto reale useresti una libreria come Jackson o Gson per mappare il JSON a POJO per una gestione più semplice.

Se incontri un array `pages` vuoto, i colpevoli più comuni sono: il file immagine non è stato trovato, o l'immagine è troppo sfocata per le impostazioni predefinite del motore. In quest'ultimo caso, prova ad aumentare i DPI o applicare un passo di pre‑elaborazione (es., binarizzazione) prima di passarla ad Aspose.

## Varianti e casi limite

| Scenario | Cosa modificare |
|----------|----------------|
| **Multiple pages** (e.g., multi‑page PDF converted to images) | Itera su ogni immagine, chiama `ocrEngine.setImage(...)` all'interno del ciclo e aggrega i risultati JSON. |
| **Different output format** | Sostituisci `OcrResultFormat.JSON` con `OcrResultFormat.XML` o `OcrResultFormat.PLAIN_TEXT`. |
| **Performance tuning** | Usa `ocrEngine.setRecognitionMode(OcrRecognitionMode.FAST)` per velocità, o `OcrRecognitionMode.ACCURATE` per qualità. |
| **Non‑receipt documents** | Regola `ocrEngine.getPageSegmentationSettings().setDetectTables(true)` se hai bisogno di estrarre tabelle. |

Queste modifiche ti permettono di adattare il flusso principale di **estrarre testo da immagine java** a una vasta gamma di problemi reali.

## Conclusione

Abbiamo appena coperto un metodo conciso, pronto per la produzione, per **estrarre testo da immagine java** usando Aspose OCR. Seguendo i cinque passaggi—creare il motore, **caricare immagine per OCR**, impostare l'output JSON, **riconoscere testo da ricevuta**, e infine leggere il JSON—puoi integrare l'OCR in qualsiasi backend Java con poco sforzo.  

Da qui potresti voler:

- Memorizzare il JSON in un database NoSQL per analisi future.  
- Inoltrare il risultato a un chatbot che risponde a domande sulle ricevute.  
- Combinarlo con Apache Tika per gestire PDF, DOCX e altri formati.

Provalo, modifica le impostazioni per adattarle ai tuoi documenti specifici, e lascia che la macchina faccia il lavoro pesante mentre tu ti concentri a creare valore.

---

![estrarre testo da immagine java](placeholder-image.png "estrarre testo da immagine java")

*Figura: Rappresentazione visiva della pipeline OCR – dal file immagine all'output JSON.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}