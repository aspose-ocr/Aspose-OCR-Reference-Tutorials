---
date: 2026-02-09
description: Scopri come convertire un'immagine in testo ed estrarre i rettangoli
  delle aree di testo usando la libreria Aspose OCR per Java. Guida passo‑passo con
  esempi di codice.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: Converti immagine in testo – Riconosci il testo dall'immagine e recupera i
  rettangoli delle aree di testo
url: /it/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converti Immagine in Testo – Riconosci Testo da Immagine e Recupera i Rettangoli delle Aree di Testo

## Introduzione

Se devi **convertire immagine in testo** e **riconoscere testo da file immagine** in un'applicazione Java, Aspose.OCR per Java offre un modo rapido e preciso per farlo. In questo tutorial percorreremo passo passo le operazioni necessarie per estrarre i paragrafi da un'immagine, ottenere i rettangoli di delimitazione per ogni area di testo e stampare tali coordinate sulla console. Alla fine comprenderai perché questo approccio funziona, come integrare la libreria e dove potrai estenderla per i tuoi casi d'uso.

## Risposte Rapide
- **Cosa significa “riconoscere testo da immagine”?** Significa convertire i caratteri visivi presenti in un'immagine in dati stringa modificabili.  
- **Quale libreria gestisce questo in Java?** Aspose.OCR per Java.  
- **È necessaria una licenza per lo sviluppo?** È disponibile una licenza temporanea per i test; per la produzione è richiesta una licenza completa.  
- **Posso estrarre paragrafi invece di singole parole?** Sì – usa `AreasType.PARAGRAPHS` per ottenere i rettangoli a livello di paragrafo.  
- **Il codice è compatibile con Java 11+?** Assolutamente sì, l'API funziona con Java 11 e versioni successive.

## Cos’è “convertire immagine in testo” in Aspose.OCR?
Il metodo `RecognizePage` di Aspose.OCR analizza il bitmap, applica gli algoritmi OCR e restituisce la stringa riconosciuta. Quando richiedi le aree di testo, la libreria calcola anche le coordinate esatte del `Rectangle` per ogni blocco di testo, facilitando l'evidenziazione o l'elaborazione di sezioni specifiche in seguito.

## Perché usare questa **java ocr library**?
- **Alta precisione** – supporta più lingue e font complessi.  
- **Integrazione semplice** – un unico JAR aggiunge tutte le funzionalità OCR.  
- **Output flessibile** – puoi recuperare testo grezzo, HTML formattato o i rettangoli precisi delle aree di testo.  
- **Thread‑safe** – adatta a ambienti server ad alto throughput.

## Prerequisiti

- **Java Development Kit** (JDK 11 o versioni successive) installato sulla tua macchina.  
- Libreria **Aspose.OCR per Java** – scaricala dal sito ufficiale [qui](https://releases.aspose.com/ocr/java/).  
- Un IDE o uno strumento di build (Maven/Gradle) per gestire la dipendenza JAR.

## Importa i Pacchetti

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

## Guida Passo‑Passo

### Passo 1: Configura il Progetto
Crea un nuovo progetto Java (o aggiungilo a uno esistente) e posiziona il JAR di Aspose.OCR nel classpath. Se usi Maven, aggiungi la dipendenza come indicato nel pacchetto scaricato.

### Passo 2: Definisci la Directory del Documento e il Percorso dell'Immagine
Specifica dove si trova l'immagine di esempio:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Passo 3: Crea l'Istanza Aspose.OCR
Istanzia il motore OCR:

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### Passo 4: Riconosci il Testo nell'Immagine
Chiama `RecognizePage` per convertire l'immagine in testo semplice. Questo passaggio dimostra la funzionalità principale **recognize text image java**:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Passo 5: Ottieni i Rettangoli con le Aree di Testo
Ora recupera i rettangoli di delimitazione per ogni paragrafo (o altro tipo di area). Qui **estrai paragrafi da immagine** e ottieni le loro coordinate:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Problemi Comuni & Risoluzione

| Sintomo | Causa Probabile | Soluzione |
|---------|-----------------|-----------|
| `IOException` su `RecognizePage` | Percorso file errato o permessi di lettura mancanti | Verifica che `imagePath` punti a un PNG/JPG esistente e che l'app abbia accesso al file system. |
| Stringa di risultato vuota | Immagine di bassa qualità o lingua non supportata | Pre‑elabora l'immagine (aumenta contrasto, binarizza) o specifica la lingua corretta con `api.setLanguage("eng")`. |
| Nessun rettangolo restituito | Uso di `AreasType` errato (es. `WORDS` quando ti aspetti paragrafi) | Passa a `AreasType.PARAGRAPHS` o `AreasType.LINES` secondo necessità. |

## Domande Frequenti

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

In questo **aspose ocr java tutorial** hai imparato come **convertire immagine in testo** usando Aspose.OCR per Java, estrarre i paragrafi e recuperare i rettangoli esatti che circondano ogni blocco di testo. Queste funzionalità ti consentono di creare PDF ricercabili, evidenziare testo in overlay UI o alimentare dati strutturati a processi a valle. Esplora ulteriormente l'API per personalizzare le impostazioni della lingua, gestire diversi formati di immagine o integrarla con lo storage cloud.

---

**Ultimo aggiornamento:** 2026-02-09  
**Testato con:** Aspose.OCR 23.10 per Java  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}