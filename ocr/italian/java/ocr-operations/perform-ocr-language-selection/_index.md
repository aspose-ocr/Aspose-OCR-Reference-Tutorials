---
title: Esecuzione dell'OCR con selezione della lingua in Aspose.OCR
linktitle: Esecuzione dell'OCR con selezione della lingua in Aspose.OCR
second_title: API Java Aspose.OCR
description: Sblocca l'estrazione precisa del testo dalle immagini con Aspose.OCR per Java. Segui la nostra guida passo passo per un OCR accurato con la selezione della lingua.
weight: 11
url: /it/java/ocr-operations/perform-ocr-language-selection/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esecuzione dell'OCR con selezione della lingua in Aspose.OCR

## introduzione

Nel panorama in continua evoluzione della tecnologia, il riconoscimento ottico dei caratteri (OCR) svolge un ruolo fondamentale nell'estrazione di informazioni significative dalle immagini. Aspose.OCR per Java si distingue come un potente strumento che consente agli sviluppatori di integrare perfettamente le funzionalità OCR nelle loro applicazioni Java. In questa guida passo passo, esploreremo come eseguire l'OCR con la selezione della lingua utilizzando Aspose.OCR, sbloccando il potenziale per elaborare contenuti diversi con precisione.

## Prerequisiti

Prima di immergerti nel tutorial, assicurati di disporre dei seguenti prerequisiti:

- Ambiente di sviluppo Java: assicurati di avere Java installato sul tuo sistema e che il tuo ambiente di sviluppo sia configurato.

-  Libreria Aspose.OCR: scarica e installa la libreria Aspose.OCR per Java. È possibile trovare la libreria e la relativa documentazione[Qui](https://reference.aspose.com/ocr/java/).

- File immagine: prepara un file immagine contenente il testo che desideri estrarre. Ad esempio, utilizziamo un file denominato "p3.png".

## Importa pacchetti

Nel tuo progetto Java, importa i pacchetti necessari per sfruttare la funzionalità Aspose.OCR. Aggiungi le seguenti righe all'inizio del tuo file Java:

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

## Passaggio 1: configura la directory dei documenti

```java
// Il percorso della directory dei documenti.
String dataDir = "Your Document Directory";
```

Sostituisci "Directory dei documenti" con il percorso effettivo della directory in cui si trova il file immagine.

## Passaggio 2: definire il percorso dell'immagine

```java
// Il percorso dell'immagine
String file = dataDir + "p3.png";
```

Regola la variabile file in modo che punti al tuo file immagine specifico.

## Passaggio 3: creare un'istanza API Aspose.OCR

```java
// Crea un'istanza API
AsposeOCR api = new AsposeOCR();
```

Inizializza l'oggetto AsposeOCR per accedere alle sue funzionalità.

## Passaggio 4: imposta le opzioni di riconoscimento

```java
// Imposta le opzioni di riconoscimento
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Personalizza le impostazioni di riconoscimento in base alle tue esigenze. Regola parametri quali inclinazione, lingua e aree di riconoscimento.

## Passaggio 5: eseguire l'OCR e recuperare i risultati

```java
// Ottieni l'oggetto risultato
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Eseguire l'operazione OCR utilizzando il file immagine e le impostazioni specificati. Cattura il risultato nell'oggetto RecognitionResult.

## Passaggio 6: stampare e utilizzare i risultati

```java
// Stampa il risultato
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

Stampa il testo estratto, le aree di riconoscimento, la rappresentazione JSON, l'angolo di inclinazione ed eventuali avvisi. Utilizza i risultati secondo necessità nella tua applicazione.

## Conclusione

In questo tutorial, abbiamo approfondito la perfetta integrazione di Aspose.OCR per Java per eseguire l'OCR con la selezione della lingua. Questa potente libreria apre un mondo di possibilità per gli sviluppatori che desiderano estrarre il testo dalle immagini in modo accurato.

## Domande frequenti

### Q1: Posso utilizzare Aspose.OCR per più lingue in un unico processo di riconoscimento?

R1: Sì, è possibile impostare più lingue in RecognitionSettings per migliorare la precisione del riconoscimento per il contenuto multilingue.

### Q2: Come posso gestire diversi formati di immagine con Aspose.OCR?

R2: Aspose.OCR supporta vari formati di immagine, inclusi PNG, JPEG e TIFF. Fornisci semplicemente il percorso file corretto nella variabile del percorso immagine.

### Q3: Esiste un limite alla dimensione dell'immagine che Aspose.OCR può elaborare?

A3: Aspose.OCR può gestire immagini di varie dimensioni, ma immagini più grandi potrebbero richiedere più tempo e risorse di elaborazione.

### Q4: Posso ottimizzare le impostazioni di riconoscimento per aree specifiche all'interno di un'immagine?

A4: Assolutamente. Utilizza la funzione RecognitionAreas per definire rettangoli specifici all'interno dell'immagine per un riconoscimento mirato.

### Q5: Aspose.OCR è adatto sia a progetti personali che commerciali?

A5: Sì, Aspose.OCR offre opzioni di licenza flessibili, rendendolo adatto sia per uso personale che commerciale.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
