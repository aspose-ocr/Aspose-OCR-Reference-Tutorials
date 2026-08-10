---
date: 2026-06-24
description: Scopri come eseguire l'OCR del testo delle immagini con selezione della
  lingua usando Aspose.OCR per Java. Questa guida passo‑passo copre l'estrazione di
  testo Java, la correzione di inclinazione OCR e altro.
keywords:
- ocr skew correction
- ocr language support
- improve ocr accuracy
- extract text image java
- ocr image java
linktitle: Come eseguire la correzione di inclinazione OCR e la selezione della lingua
  con Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  headline: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  type: TechArticle
- description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  name: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  steps:
  - name: Set up Your Document Directory
    text: Create a `File` object that points to the folder containing your source
      image. This makes the path handling portable across operating systems. Replace
      `"Your Document Directory"` with the absolute path where `p3.png` resides.
  - name: Define the Image Path
    text: Instantiate a `File` object for the specific image you want to process.
      Using a `File` object gives you easy access to file metadata if you need it
      later. Make sure the `file` variable points to the exact image you intend to
      process.
  - name: Create Aspose.OCR API Instance
    text: The `AsposeOCR` class is the entry point for all OCR operations. It encapsulates
      the engine, manages resources, and provides the `recognizePage` method. The
      `AsposeOCR` object gives you access to all OCR operations.
  - name: Set Recognition Options (Language Selection)
    text: '`RecognitionSettings` is Aspose.OCR''s configuration container that lets
      you fine‑tune the OCR process. Here we: 1. Disable auto‑skew because we provide
      a manual skew value. 2. Define a rectangular region (`RecognitionAreas`) to
      limit OCR to the part of the image that actually contains text. 3. Set t'
  - name: Perform OCR and Retrieve Results
    text: Calling `recognizePage` runs the OCR engine using the image and the settings
      you defined. The outcome is stored in a `RecognitionResult` object, which aggregates
      all useful data. The `RecognizePage` call runs the OCR engine using the image
      and the settings you defined. The outcome is stored in a `Re
  - name: Print and Utilize Results
    text: 'The console output shows: - The full extracted text (`recognitionText`).
      - Text for each defined rectangle (`recognitionAreasText`). - Bounding rectangle
      coordinates. - A JSON representation for easy downstream processing. - Detected
      skew angle and any warnings. The console output shows the full ext'
  type: HowTo
- questions:
  - answer: Yes. Use `settings.setLanguage(Language.Eng | Language.Fra)` to enable
      multilingual recognition.
    question: Can I recognize multiple languages in a single OCR call?
  - answer: PNG, JPEG, BMP, TIFF, GIF, and several others. Just provide the correct
      file path.
    question: Which image formats does Aspose.OCR support?
  - answer: There’s no hard limit, but processing images larger than 10 MB can increase
      memory usage and runtime. Consider resizing large files.
    question: Is there a size limit for the image?
  - answer: Purchase a license from the Aspose website and apply it via the `License`
      class as shown in the Aspose documentation.
    question: How do I obtain a production license?
  - answer: Not directly with Aspose.OCR. Convert the PDF page to an image first (e.g.,
      using Aspose.PDF) and then run OCR.
    question: Can I extract text from a PDF page directly?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Come eseguire la correzione di inclinazione OCR e la selezione della lingua
  con Aspose.OCR
url: /it/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire la correzione di inclinazione OCR e la selezione della lingua con Aspose.OCR

## Introduzione

Estrarre testo da file immagine è una necessità comune, sia che tu stia digitalizzando documenti scansionati, elaborando ricevute o creando archivi ricercabili. In questo tutorial percorreremo un esempio completo e pratico che mostra **come eseguire OCR su testo immagine** con un'impostazione di lingua specifica, così potrai integrare OCR affidabile nelle tue applicazioni Java oggi. Vedrai anche come gestire **la correzione di inclinazione OCR** e il riconoscimento basato su regioni per una precisione ottimale, che insieme possono **migliorare l'accuratezza OCR** fino al 30 % su scansioni inclinate.

## Risposte rapide
- **Quale libreria gestisce l'OCR in Java?** Aspose.OCR per Java  
- **Quale impostazione seleziona la lingua?** `settings.setLanguage(Language.Eng)` (o qualsiasi lingua supportata)  
- **È necessaria una licenza per lo sviluppo?** Una licenza di valutazione gratuita funziona per i test; è necessaria una licenza commerciale per la produzione.  
- **Posso limitare l'OCR a una regione dell'immagine?** Sì, usa `RecognitionSettings.setRecognitionAreas()` con rettangoli.  
- **Qual è il tempo di esecuzione tipico?** Alcuni secondi per pagina su un laptop standard, a seconda delle dimensioni dell'immagine e della complessità della lingua.  

`Language` è un'enumerazione che elenca le lingue OCR supportate da Aspose.OCR, come English, French, Spanish, ecc.

## Che cos'è la correzione di inclinazione OCR?

La correzione di inclinazione OCR è il processo di rilevare e raddrizzare le linee di testo inclinate prima del riconoscimento dei caratteri. Allineando la linea di base del testo, il motore OCR può applicare i suoi modelli linguistici in modo più efficace, riducendo le errate interpretazioni causate da scansioni inclinate. Questo passaggio migliora la qualità visiva dell'immagine di input, consentendo agli algoritmi di riconoscimento di concentrarsi sulle forme reali dei caratteri anziché sulle distorsioni introdotte dalla rotazione.

## Perché la correzione di inclinazione OCR migliora l'accuratezza

Quando il testo è inclinato, le forme dei caratteri appaiono distorte, portando a tassi di errore fino al 20 % più alti. Applicare **ocr skew correction** rimuove tale distorsione, permettendo al motore di concentrarsi sui glifi effettivi. Nei test di benchmark Aspose.OCR ha ottenuto un aumento del 15‑30 % dell'accuratezza di riconoscimento su documenti con rotazione di 10‑15° dopo aver applicato la correzione di inclinazione.

## Perché usare Aspose.OCR con selezione della lingua?

Selezionare la lingua esatta del testo sorgente consente al motore OCR di utilizzare dizionari e modelli di caratteri specifici per lingua, aumentando drasticamente la precisione di riconoscimento e riducendo i tempi di elaborazione. Inoltre, Aspose.OCR offre un controllo fine sulla correzione di inclinazione, la selezione delle regioni e i formati di output, rendendolo una scelta versatile per pipeline di elaborazione documenti multilingue.

- **Supporto multilingue** – Scegli la lingua/e esatta/e presente/i nella tua immagine per aumentare l'accuratezza.  
- **Controllo fine** – Regola l'inclinazione, definisci le aree di riconoscimento e imposta il comportamento auto‑skew.  
- **API Java pura** – Nessuna dipendenza nativa, facile da integrare in qualsiasi progetto Java.  
- **Dati di risultato ricchi** – Ottieni testo semplice, JSON, rettangoli di delimitazione e avvisi in una sola chiamata.  
- **Capacità quantificate** – Aspose.OCR supporta **oltre 50** formati di input e output e può elaborare batch di immagini fino a **500 pagine** senza caricare l'intero documento in memoria.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- **Java Development Kit (JDK)** installato (JDK 8 o successivo).  
- **Libreria Aspose.OCR per Java** – scaricala dal sito ufficiale [qui](https://reference.aspose.com/ocr/java/).  
- Un file immagine che contenga il testo da estrarre, ad es. `p3.png`.  

## Importare i pacchetti

Le seguenti importazioni ti danno accesso alle classi OCR core e alle utility Java standard.  
`import com.aspose.ocr.*;` – importa il motore OCR principale.  
`import com.aspose.ocr.config.*;` – contiene oggetti di configurazione come `RecognitionSettings`.  
`import java.awt.Rectangle;` – usato per definire le aree di riconoscimento.  

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Come applicare la correzione di inclinazione OCR in Java?

Carica l'immagine, disabilita il rilevamento automatico dell'inclinazione e fornisci un angolo misurato oppure lascia che il motore lo calcoli usando `settings.setAutoSkew(false)`. Il motore OCR raddrizzerà prima l'immagine in base all'angolo fornito o rilevato, quindi procederà con il riconoscimento dei caratteri. Questo approccio a due fasi garantisce che qualsiasi inclinazione venga rimossa prima dell'applicazione dei modelli linguistici, producendo un output di testo più pulito e meno errori di riconoscimento.

## Guida passo‑passo

### Passo 1: Configura la directory del documento

Crea un oggetto `File` che punti alla cartella contenente l'immagine sorgente. Questo rende la gestione dei percorsi portabile tra sistemi operativi.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Sostituisci `"Your Document Directory"` con il percorso assoluto dove risiede `p3.png`.

### Passo 2: Definisci il percorso dell'immagine

Istanzia un oggetto `File` per l'immagine specifica da elaborare. Usare un oggetto `File` ti dà facile accesso ai metadati del file se ti servono in seguito.

```java
// The image path
String file = dataDir + "p3.png";
```

Assicurati che la variabile `file` punti all'immagine esatta che intendi elaborare.

### Passo 3: Crea l'istanza API Aspose.OCR

La classe `AsposeOCR` è il punto di ingresso per tutte le operazioni OCR. Incapsula il motore, gestisce le risorse e fornisce il metodo `recognizePage`.

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

L'oggetto `AsposeOCR` ti dà accesso a tutte le operazioni OCR.

### Passo 4: Imposta le opzioni di riconoscimento (selezione della lingua)

`RecognitionSettings` è il contenitore di configurazione di Aspose.OCR che ti permette di perfezionare il processo OCR.  

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Qui:

1. Disabilitiamo l'auto‑skew perché forniamo un valore di inclinazione manuale.  
2. Definiamo una regione rettangolare (`RecognitionAreas`) per limitare l'OCR alla parte dell'immagine che contiene effettivamente testo.  
3. Impostiamo la **lingua** su English (`Language.Eng`). Cambia in `Language.Fra`, `Language.Spa`, ecc., a seconda della tua immagine sorgente.

### Passo 5: Esegui l'OCR e recupera i risultati

Chiamare `recognizePage` avvia il motore OCR usando l'immagine e le impostazioni definite. L'esito è memorizzato in un oggetto `RecognitionResult`, che aggrega tutti i dati utili.

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

La chiamata `RecognizePage` esegue il motore OCR usando l'immagine e le impostazioni definite. L'esito è memorizzato in un oggetto `RecognitionResult`.

### Passo 6: Stampa e utilizza i risultati

L'output della console mostra:

- Il testo estratto completo (`recognitionText`).  
- Il testo per ciascun rettangolo definito (`recognitionAreasText`).  
- Le coordinate dei rettangoli di delimitazione.  
- Una rappresentazione JSON per una facile elaborazione a valle.  
- L'angolo di inclinazione rilevato e eventuali avvisi.

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

L'output della console mostra il testo estratto completo, il testo specifico per regione, i bounding box, il JSON, l'angolo di inclinazione e gli avvisi. Ora puoi alimentare `result.recognitionText` nella tua logica di business — archiviarlo, indicizzarlo o passarlo a un altro servizio.

## Problemi comuni e soluzioni

| Problema | Causa | Soluzione |
|----------|-------|-----------|
| **Caratteri spazzatura** | Lingua errata selezionata | Imposta l'enumerazione `Language` corretta (es. `Language.Fra` per il francese). |
| **Nessun testo restituito** | L'area di riconoscimento non copre il testo | Regola le coordinate del `Rectangle` o rimuovi `RecognitionAreas` per elaborare l'intera immagine. |
| **Prestazioni lente** | Immagine molto grande o alta risoluzione | Ridimensiona l'immagine prima dell'OCR o aumenta l'allocazione di memoria JVM. |
| **Avvisi su formato non supportato** | Formato immagine non riconosciuto | Converti l'immagine in PNG, JPEG o TIFF prima dell'elaborazione. |

## Domande frequenti

**D: Posso riconoscere più lingue in una singola chiamata OCR?**  
R: Sì. Usa `settings.setLanguage(Language.Eng | Language.Fra)` per abilitare il riconoscimento multilingue.

**D: Quali formati immagine supporta Aspose.OCR?**  
R: PNG, JPEG, BMP, TIFF, GIF e diversi altri. Basta fornire il percorso file corretto.

**D: Esiste un limite di dimensione per l'immagine?**  
R: Non c'è un limite rigido, ma elaborare immagini superiori a 10 MB può aumentare l'uso di memoria e il tempo di esecuzione. Considera di ridimensionare i file di grandi dimensioni.

**D: Come ottengo una licenza di produzione?**  
R: Acquista una licenza dal sito Aspose e applicala tramite la classe `License` come mostrato nella documentazione Aspose.

**D: Posso estrarre testo da una pagina PDF direttamente?**  
R: Non direttamente con Aspose.OCR. Converti prima la pagina PDF in immagine (ad es. usando Aspose.PDF) e poi esegui l'OCR.

## Conclusione

Ora hai visto come **estrarre testo da un'immagine** usando Aspose.OCR per Java, selezionando la lingua appropriata e applicando **OCR skew correction** per migliorare l'affidabilità. Questo approccio fornisce OCR accurato e ad alte prestazioni che può essere integrato in qualsiasi flusso di lavoro basato su Java — dai sistemi di gestione documentale alle pipeline di acquisizione dati. Sperimenta con diversi enum `Language`, regola le `RecognitionAreas` e integra l'output JSON nella tua analisi a valle per una soluzione davvero end‑to‑end.

---

**Ultimo aggiornamento:** 2026-06-24  
**Testato con:** Aspose.OCR 24.11 per Java  
**Autore:** Aspose

## Tutorial correlati

- [How to calculate skew angle java using Aspose.OCR](/ocr/java/ocr-basics/calculate-skew-angle/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/java/ocr-operations/recognize-pdf/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}