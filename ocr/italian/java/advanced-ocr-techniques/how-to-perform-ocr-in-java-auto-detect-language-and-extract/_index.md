---
category: general
date: 2026-04-26
description: Scopri come eseguire l'OCR e estrarre il testo da un'immagine usando
  Aspose OCR. Questa guida mostra come caricare l'immagine per l'OCR, abilitare il
  rilevamento automatico della lingua e l'OCR con rilevamento automatico della lingua.
draft: false
keywords:
- how to perform OCR
- extract text from image
- load image for OCR
- enable automatic language detection
- auto detect language OCR
language: it
og_description: Come eseguire l'OCR in Java con Aspose OCR. Impara a caricare l'immagine
  per l'OCR, abilitare il rilevamento automatico della lingua e estrarre il testo
  dall'immagine.
og_title: Come eseguire OCR in Java – Rilevamento automatico della lingua
tags:
- OCR
- Java
- Aspose
title: Come eseguire OCR in Java – Rilevamento automatico della lingua ed estrazione
  del testo
url: /it/java/advanced-ocr-techniques/how-to-perform-ocr-in-java-auto-detect-language-and-extract/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR in Java – Rilevamento automatico della lingua ed estrazione del testo

Ti è mai capitato di dover sapere **come eseguire OCR** su una foto che mescola inglese, spagnolo e forse alcuni caratteri giapponesi? Non sei solo: gli sviluppatori incontrano costantemente questo ostacolo quando le loro app devono leggere testo da documenti scansionati, ricevute o cartelli multilingue.  

La buona notizia? Con poche righe di Java e Aspose OCR puoi **caricare l'immagine per OCR**, attivare **l'abilitazione del rilevamento automatico della lingua**, e estrarre istantaneamente **testo dall'immagine** senza dover indovinare prima la lingua. In questo tutorial percorreremo l'esempio completo e eseguibile, spiegheremo perché ogni passaggio è importante e ti mostreremo come verificare il risultato dell'**OCR con rilevamento automatico della lingua**.

> **Cosa otterrai**  
> * Un programma Java funzionante che legge un PNG multilingua.  
> * Conoscenza delle impostazioni chiave OCR che rendono il rilevamento della lingua semplice.  
> * Suggerimenti per gestire file mancanti, lingue non supportate e ottimizzazioni delle prestazioni.

---

## Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------|
| Java 17 (or newer) | Aspose OCR è progettato per JVM moderne; le versioni più vecchie potrebbero non supportare le funzionalità dell'API. |
| Aspose OCR for Java library (latest version) | Fornisce `OcrEngine` e le capacità di rilevamento automatico della lingua. |
| An image file (`mixed_lang.png`) containing text in at least two languages | Dimostra la funzionalità di **OCR con rilevamento automatico della lingua**. |
| A Java IDE or simple command‑line setup | Per compilare ed eseguire il codice di esempio. |

Se non hai ancora scaricato il JAR di Aspose OCR, scaricalo dal repository Maven ufficiale:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- replace with the latest -->
</dependency>
```

---

## Passo 1: Creare l'istanza del motore OCR – Come eseguire OCR

La prima cosa da fare quando vuoi **eseguire OCR** è istanziare il motore. Pensa a `OcrEngine` come al cervello che analizzerà il bitmap e trasformerà i pixel in caratteri.

```java
// Step 1: Initialize the OCR engine
import com.aspose.ocr.*;

public class AutoDetectDemo {
    public static void main(String[] args) throws Exception {

        // Create a fresh OcrEngine object – this is where the magic starts
        OcrEngine ocrEngine = new OcrEngine();
```

> **Consiglio:** Riutilizzare lo stesso `OcrEngine` per molte immagini può migliorare le prestazioni perché il motore memorizza internamente i modelli linguistici nella cache.

---

## Passo 2: Abilitare il rilevamento automatico della lingua – Abilitare il rilevamento automatico della lingua

Per impostazione predefinita Aspose OCR assume l'inglese. Per immagini multilingue devi indicargli di “indovinare” la lingua per blocco di testo. È ciò che fa il flag **enable automatic language detection**.

```java
        // Step 2: Turn on auto‑language detection for each region
        ocrEngine.getRecognitionSettings()
                 .setLanguage(OcrLanguage.AUTO_DETECT);
```

Perché è importante: il motore ora ispeziona ogni segmento dell'immagine, sceglie la lingua più probabile e applica il set di caratteri corretto. Senza questo, otterresti un output illeggibile per le sezioni non‑inglesi.

---

## Passo 3: Caricare l'immagine per OCR – Caricare l'immagine per OCR

Ora carichiamo effettivamente **l'immagine per OCR**. Il percorso può essere assoluto o relativo; assicurati solo che il file esista, altrimenti otterrai una `FileNotFoundException`.

```java
        // Step 3: Point the engine at the image that contains mixed‑language text
        ocrEngine.setImage("YOUR_DIRECTORY/mixed_lang.png");
```

> **Caso limite:** Se la tua immagine si trova nella cartella resources di un progetto Maven, usa `getClass().getResource("/mixed_lang.png")` per evitare percorsi codificati.

---

## Passo 4: Eseguire il riconoscimento ed estrarre testo dall'immagine – Estrarre testo dall'immagine

Con il motore configurato e l'immagine caricata, è il momento di **eseguire OCR**. La chiamata `recognize()` fa il lavoro pesante, mentre `getText()` restituisce una semplice `String`.

```java
        // Step 4: Execute OCR and fetch the recognized text
        String recognizedText = ocrEngine.recognize().getText();
```

A questo punto la libreria ha già effettuato **OCR con rilevamento automatico della lingua** per ogni blocco, quindi la variabile `recognizedText` contiene una trascrizione pulita e consapevole della lingua.

---

## Passo 5: Visualizzare il risultato – Verificare l'output dell'OCR con rilevamento automatico della lingua

Infine, stampiamo il risultato sulla console. In un'app reale potresti scriverlo su un file, in un database o inviarlo a un servizio di traduzione.

```java
        // Step 5: Show the output – you’ll see language tags if you enable them
        System.out.println("Auto‑detected language output:\n" + recognizedText);
    }
}
```

### Output previsto

Supponendo che `mixed_lang.png` contenga “Hello” (inglese) e “¡Hola!” (spagnolo), vedrai qualcosa di simile:

```
Auto‑detected language output:
Hello
¡Hola!
```

Se abiliti `setShowLanguage(true)` nelle impostazioni, il motore antepone a ogni riga un codice lingua, ad esempio `[en] Hello` e `[es] ¡Hola!`.

---

## Domande comuni e insidie

### Cosa succede se il percorso dell'immagine è errato?

Il motore lancia una `FileNotFoundException`. Avvolgi la chiamata in un blocco try‑catch e fornisci all'utente un messaggio amichevole:

```java
try {
    ocrEngine.setImage("path/to/image.png");
} catch (FileNotFoundException e) {
    System.err.println("Image not found – check the file path!");
    return;
}
```

### Posso limitare le lingue per velocizzare il rilevamento?

Sì. Invece di `AUTO_DETECT`, puoi fornire un elenco:

```java
ocrEngine.getRecognitionSettings()
         .setLanguage(new OcrLanguage[]{OcrLanguage.ENGLISH, OcrLanguage.SPANISH});
```

Ciò riduce lo spazio di ricerca e può migliorare le prestazioni su grandi lotti.

### Come gestisce **OCR con rilevamento automatico della lingua** il testo scritto a mano?

Aspose OCR si concentra sul testo stampato. Gli script scritti a mano solitamente richiedono un motore diverso (ad esempio, Aspose OCR for Handwriting). Tentare di forzare il rilevamento produrrà risultati scadenti.

---

## Esempio completo funzionante (pronto per copia‑incolla)

Di seguito trovi l'intero programma, pronto per essere compilato ed eseguito. Sostituisci `YOUR_DIRECTORY` con la cartella reale che contiene `mixed_lang.png`.

```java
import com.aspose.ocr.*;

public class AutoDetectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine – this is where the magic starts
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection for each text block
        ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.AUTO_DETECT);

        // Step 3: Load the image that contains mixed‑language text
        // Make sure the file exists; otherwise an exception is thrown
        ocrEngine.setImage("YOUR_DIRECTORY/mixed_lang.png");

        // Step 4: Run the recognition process and obtain the extracted text
        String recognizedText = ocrEngine.recognize().getText();

        // Step 5: Display the auto‑detected language output
        System.out.println("Auto‑detected language output:\n" + recognizedText);
    }
}
```

Eseguilo con:

```bash
javac -cp "aspose-ocr-23.10.jar" AutoDetectDemo.java
java -cp ".:aspose-ocr-23.10.jar" AutoDetectDemo
```

Dovresti vedere l'output della console descritto in precedenza.

---

## Estendere la soluzione

Ora che sai **come eseguire OCR**, considera i seguenti passi successivi:

* **Elaborazione batch** – Scorri una cartella di immagini, riutilizzando la stessa istanza di `OcrEngine` per velocità.
* **Salvataggio dei risultati** – Scrivi il testo estratto in file `.txt` o salvalo in un database.
* **Post‑elaborazione** – Usa espressioni regolari per pulire le interruzioni di riga o rimuovere caratteri indesiderati.
* **Integrazione** – Invia l'output a un'API di traduzione (Google Translate, Azure Translator) per applicazioni multilingue.

Ciascuna di queste estensioni continua a basarsi sui concetti fondamentali trattati: caricare l'immagine, abilitare il rilevamento della lingua e estrarre il testo.

---

## Conclusione

Abbiamo percorso un esempio completo, end‑to‑end, che mostra **come eseguire OCR** in Java rilevando automaticamente le lingue. Seguendo i cinque passaggi—creare il motore, abilitare il rilevamento automatico della lingua, caricare l'immagine, eseguire il riconoscimento e visualizzare i risultati—puoi estrarre in modo affidabile **testo da immagini** che contengono più script.  

Ricorda, la chiave per un **OCR con rilevamento automatico della lingua** fluido è lasciare che il motore decida per blocco; forzare una singola lingua spesso porta a output illeggibili. Sperimenta con diverse qualità d'immagine, elenchi di lingue e ottimizzazioni delle prestazioni per perfezionare l'esperienza per il tuo caso d'uso specifico.

Hai uno scenario non coperto qui? Lascia un commento e risolviamo insieme. Buona programmazione!  

![esempio di come eseguire OCR](/images/ocr-demo.png "Screenshot che mostra come eseguire OCR con Aspose OCR in Java")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}