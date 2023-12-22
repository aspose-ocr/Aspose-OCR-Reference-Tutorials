---
title: Esecuzione dell'OCR sull'immagine dall'URL in Aspose.OCR per Java
linktitle: Esecuzione dell'OCR sull'immagine dall'URL in Aspose.OCR per Java
second_title: API Java Aspose.OCR
description: Sblocca l'estrazione perfetta del testo dell'immagine in Java con Aspose.OCR. OCR ad alta precisione con facile integrazione.
type: docs
weight: 11
url: /it/java/advanced-ocr-techniques/perform-ocr-image-from-url/
---
## introduzione

Benvenuti nella nostra guida passo passo sull'esecuzione del riconoscimento ottico dei caratteri (OCR) su un'immagine da un URL utilizzando Aspose.OCR per Java. Questo tutorial è progettato per aiutarti a integrare perfettamente Aspose.OCR nelle tue applicazioni Java, permettendoti di estrarre facilmente il testo dalle immagini. Aspose.OCR è una potente libreria OCR che supporta vari formati di immagine, rendendolo uno strumento prezioso per le applicazioni che richiedono l'estrazione di testo.

## Prerequisiti

Prima di immergerti nel tutorial, assicurati di possedere i seguenti prerequisiti:

1. Ambiente di sviluppo Java: assicurati di avere un ambiente di sviluppo Java funzionante configurato sul tuo computer.

2.  Libreria Aspose.OCR: scarica e installa la libreria Aspose.OCR per Java. Puoi trovare la libreria e la relativa documentazione su[Sito web Aspose.OCR](https://reference.aspose.com/ocr/java/).

## Importa pacchetti

Nel tuo progetto Java, importa i pacchetti necessari per Aspose.OCR:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Passaggio 1: crea un'istanza API

Inizializza un'istanza della classe AsposeOCR:

```java
AsposeOCR api = new AsposeOCR();
```

## Passaggio 2: definire l'URL dell'immagine

Specifica l'URL dell'immagine da cui desideri eseguire l'OCR:

```java
String uri = "https://www.example.com/tua-immagine.png";
```

## Passaggio 3: imposta le opzioni di riconoscimento

Configura le impostazioni di riconoscimento, come la disattivazione dell'inclinazione automatica e la definizione delle aree di riconoscimento:

```java
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);

// Definire le aree di riconoscimento utilizzando i rettangoli
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
```

## Passaggio 4: eseguire l'OCR

Richiamare il processo di riconoscimento OCR:

```java
RecognitionResult result = null;
try {
    result = api.RecognizePageFromUri(uri, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

## Passaggio 5: stampare i risultati

Visualizza i risultati del riconoscimento, incluso il testo estratto, il testo delle aree di riconoscimento, l'output JSON ed eventuali avvisi:

```java
System.out.println("Result: \n" + result.recognitionText + "\n\n");
System.out.println("RecognitionAreasText: \n");
for (String text : result.recognitionAreasText) {
    System.out.println(text);
}
System.out.println("JSON: \n" + result.GetJson());
System.out.println("Warnings: \n");
for (String warning : result.warnings) {
    System.out.println(warning);
}
```

Ripeti questi passaggi per integrare Aspose.OCR nella tua applicazione Java ed estrarre testo dalle immagini con precisione.

## Conclusione

In conclusione, sfruttare Aspose.OCR per Java fornisce una soluzione solida per le attività OCR, consentendo agli sviluppatori di estrarre senza problemi il testo dalle immagini. La guida passo passo garantisce un processo di integrazione fluido, rendendolo accessibile agli sviluppatori di tutti i livelli.

## Domande frequenti

### Q1: Quanto è accurato Aspose.OCR nel riconoscere il testo dalle immagini?

A1: Aspose.OCR offre un'elevata precisione nel riconoscimento del testo, soprattutto se configurato con aree di riconoscimento precise.

### Q2: Aspose.OCR può gestire più lingue durante il riconoscimento OCR?

A2: Sì, Aspose.OCR supporta il riconoscimento del testo in più lingue, offrendo versatilità per diverse applicazioni.

### Q3: Esistono considerazioni sulla licenza per l'utilizzo di Aspose.OCR in progetti commerciali?

A3: Sì, garantire la conformità ai termini di licenza Aspose.OCR per uso commerciale. Fare riferimento a[buy.aspose.com](https://purchase.aspose.com/buy) per i dettagli sulla licenza.

### Q4: Come posso ottenere supporto per i problemi relativi ad Aspose.OCR?

 A4: Visita il[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) per il supporto e le discussioni della comunità. Per il supporto premium, considera l'acquisto di una licenza temporanea da[Licenza temporanea](https://purchase.aspose.com/temporary-license/).

### Q5: È disponibile una prova gratuita per Aspose.OCR per Java?

 A5: Sì, esplora le funzionalità di Aspose.OCR con la prova gratuita disponibile su[releases.aspose.com](https://releases.aspose.com/).
