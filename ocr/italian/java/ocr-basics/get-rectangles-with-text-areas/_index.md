---
date: 2025-12-10
description: Impara a riconoscere il testo da un'immagine ed estrarre i paragrafi
  dall'immagine usando Aspose.OCR per Java. Guida passo‑passo con esempi di codice.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: Riconosci il testo da un'immagine e recupera i rettangoli delle aree di testo
url: /it/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Riconoscere il testo da immagine e recuperare i rettangoli delle aree di testo

## Introduzione

Se hai bisogno di **recognize text from image** in un'applicazione Java, Aspose.OCR per Java offre un modo rapido e preciso per farlo. In questo tutorial percorreremo passo passo le operazioni necessarie per estrarre i paragrafi da un'immagine, ottenere i rettangoli di delimitazione per ogni area di testo e stampare quelle coordinate sulla console. Alla fine comprenderai perché questo approccio funziona, come integrare la libreria e dove potrai estenderla per i tuoi casi d'uso.

## Risposte rapide
- **What does “recognize text from image” mean?** Cosa significa “recognize text from image”? Significa convertire i caratteri visivi presenti in un'immagine in dati stringa modificabili.  
- **Which library handles this in Java?** Quale libreria gestisce questo in Java? Aspose.OCR per Java.  
- **Do I need a license for development?** È necessaria una licenza per lo sviluppo? È disponibile una licenza temporanea per i test; una licenza completa è richiesta per la produzione.  
- **Can I extract paragraphs instead of single words?** Posso estrarre paragrafi invece di singole parole? Sì – usa `AreasType.PARAGRAPHS` per ottenere i rettangoli a livello di paragrafo.  
- **Is the code compatible with Java 11+?** Il codice è compatibile con Java 11+? Assolutamente, l'API funziona con Java 11 e versioni successive.

## Cos'è “recognize text from image” in Aspose.OCR?
Il metodo `RecognizePage` di Aspose.OCR analizza il bitmap, applica gli algoritmi OCR e restituisce la stringa riconosciuta. Quando richiedi le aree di testo, la libreria calcola anche le coordinate esatte del `Rectangle` per ogni blocco di testo, facilitando l'evidenziazione o l'elaborazione di sezioni specifiche in seguito.

## Perché usare Aspose.OCR per Java?
- **High accuracy** – supporta più lingue e font complessi.  
- **Easy integration** – un unico JAR aggiunge tutte le funzionalità OCR.  
- **Flexible output** – puoi recuperare testo grezzo, HTML formattato o rettangoli precisi delle aree di testo.  
- **Thread‑safe** – adatto a ambienti server ad alto throughput.

## Prerequisiti

- **Java Development Kit** (JDK 11 o successivo) installato sulla tua macchina.  
- **Aspose.OCR per Java** – scaricalo dal sito ufficiale [qui](https://releases.aspose.com/ocr/java/).  
- Un IDE o uno strumento di build (Maven/Gradle) per gestire la dipendenza JAR.

## Importare i pacchetti

Nel tuo progetto Java, importa le classi necessarie:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Guida passo‑passo

### Passo 1: Configura il tuo progetto
Crea un nuovo progetto Java (o aggiungilo a uno esistente) e posiziona il JAR di Aspose.OCR nel classpath. Se usi Maven, aggiungi la dipendenza come descritto nel pacchetto scaricato.

### Passo 2: Definisci la directory del documento e il percorso dell'immagine
Specifica dove si trova l'immagine di esempio:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Passo 3: Crea l'istanza Aspose.OCR
Istanzia il motore OCR:

```java
// Create Aspose.OCR instance
AsposeOCR api = new AsposeOCR();
```

### Passo 4: Riconosci il testo nell'immagine
Chiama `RecognizePage` per convertire l'immagine in testo semplice. Questo passaggio dimostra la capacità principale di **recognize text from image**:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Passo 5: Ottieni i rettangoli con le aree di testo
Ora recupera i rettangoli di delimitazione per ogni paragrafo (o altri tipi di area). È qui che **extract paragraphs from image** e ottieni le loro coordinate:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Problemi comuni e risoluzione

| Sintomo | Probabile causa | Risoluzione |
|---------|-----------------|-------------|
| `IOException` on `RecognizePage` | Percorso file errato o permessi di lettura mancanti | Verifica che `imagePath` punti a un PNG/JPG esistente e che l'app abbia accesso al file system. |
| Empty result string | Immagine di bassa qualità o lingua non supportata | Pre‑elabora l'immagine (aumenta contrasto, binarizza) o specifica la lingua corretta usando `api.setLanguage("eng")`. |
| No rectangles returned | Uso di `AreasType` errato (es. `WORDS` quando ti aspetti paragrafi) | Passa a `AreasType.PARAGRAPHS` o `AreasType.LINES` secondo necessità. |

## Domande frequenti

**D: Aspose.OCR è compatibile con Java 11?**  
R: Sì, Aspose.OCR funziona con Java 11 e versioni successive.

**D: Posso usare Aspose.OCR sia per progetti personali che commerciali?**  
R: Sì, è utilizzabile in qualsiasi tipo di progetto. Per i dettagli sulla licenza, visita [qui](https://purchase.aspose.com/buy).

**D: Come ottengo una licenza temporanea per la valutazione?**  
R: Puoi ottenere una licenza temporanea [qui](https://purchase.aspose.com/temporary-license/).

**D: Dove posso trovare supporto della community o assistenza ufficiale?**  
R: Per supporto e discussioni, visita il [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16).

**D: Aspose.OCR supporta il multithreading?**  
R: Sì, la libreria è thread‑safe e può essere usata in ambienti concorrenti per migliori prestazioni.

## Conclusione

In questo tutorial hai imparato come **recognize text from image** usando Aspose.OCR per Java, estrarre paragrafi e recuperare i rettangoli esatti che circondano ogni blocco di testo. Queste funzionalità ti consentono di creare PDF ricercabili, evidenziare testo in overlay UI o alimentare dati strutturati in processi successivi. Esplora ulteriormente l'API per personalizzare le impostazioni della lingua, gestire formati immagine diversi o integrare con storage cloud.

---

**Ultimo aggiornamento:** 2025-12-10  
**Testato con:** Aspose.OCR 23.10 per Java  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}