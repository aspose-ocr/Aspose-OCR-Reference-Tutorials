---
date: 2026-05-24
description: Scopri come utilizzare OCR con Aspose.OCR per Java, estrarre testo dalle
  immagini, impostare i caratteri consentiti e applicare una licenza temporanea in
  pochi minuti.
keywords:
- how to use OCR
- extract text from images
- how to apply license
- how to set characters
linktitle: Specificare i caratteri consentiti in Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-05-24'
  description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  headline: How to Use OCR – Extract Text from Images with Aspose.OCR
  type: TechArticle
- description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  name: How to Use OCR – Extract Text from Images with Aspose.OCR
  steps:
  - name: Set Your Document Directory
    text: Choose a folder where OCR results and temporary files will be stored. This
      path is later used to locate the image you want to process.
  - name: Specify the Image Path
    text: Provide the full file system path or a class‑path resource location that
      points to the image you wish to analyse.
  - name: Create an Aspose.OCR Instance
    text: '`AsposeOCR` is the core engine that performs optical character recognition.
      Instantiate it with either a temporary or permanent license string.'
  - name: Perform OCR Recognition
    text: '`RecognizeLine` extracts a single line of text from the supplied image
      and returns it as a plain Java `String`. You can call this method repeatedly
      for multi‑line documents. > **Pro tip:** If you need to restrict the output
      to digits only (e.g., for invoice numbers), call `setAllowedCharacters("0123'
  type: HowTo
- questions:
  - answer: Visit the [temporary license page](https://purchase.aspose.com/temporary-license/)
      to request a trial key that removes evaluation watermarks.
    question: How can I obtain a temporary license for Aspose.OCR?
  - answer: Join the community at the [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16)
      for help and discussions.
    question: Where can I find support for Aspose.OCR?
  - answer: Yes, use the `setAllowedCharacters` API to define a custom whitelist of
      characters. This is ideal for numeric‑only fields.
    question: Can I specify allowed characters in Aspose.OCR?
  - answer: Absolutely—Aspose.OCR is regularly updated to stay compatible with the
      newest Java releases.
    question: Is Aspose.OCR compatible with the latest JDK versions?
  - answer: The library also supports block, paragraph, and full‑page recognition,
      language packs, and advanced image preprocessing.
    question: Are there additional OCR features beyond line recognition?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Come utilizzare OCR – Estrarre testo dalle immagini con Aspose.OCR
url: /it/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come utilizzare OCR – Estrarre testo dalle immagini con Aspose.OCR

## Risposte rapide
- **Cosa fa Aspose.OCR?** Estrae testo dalle immagini con alta precisione e consente di limitare i caratteri riconosciuti.  
- **È necessaria una licenza?** È richiesta una licenza temporanea o permanente per l'uso in produzione; la chiave temporanea rimuove le filigrane.  
- **Quale versione di JDK è supportata?** La libreria funziona con le ultime versioni di JDK (JDK 17, 19, 21).  
- **Posso limitare i caratteri riconosciuti?** Sì—usa il metodo `setAllowedCharacters` per restringere l'output.  
- **Quanto tempo richiede l'installazione?** Circa 10‑15 minuti per un'implementazione base end‑to‑end.

## Che cos'è “estrarre testo dalle immagini”?
Estrarre testo dalle immagini, noto anche come riconoscimento ottico dei caratteri (OCR), converte i caratteri visivi—stampati, scritti a mano o digitati—in stringhe leggibili dalla macchina. Questa trasformazione consente alle applicazioni di cercare, indicizzare, modificare e analizzare il contenuto in modo programmatico, supportando flussi di lavoro come l'elaborazione di fatture, l'archiviazione di documenti e l'automazione dell'inserimento dati.

## Perché usare Aspose.OCR per Java?
Aspose.OCR supporta **oltre 60 lingue**, può elaborare immagini fino a **10 MB** senza caricare l'intero file in memoria, e offre **>95 % di precisione** su scansioni pulite. La libreria è autonoma, non richiede motori OCR esterni, il che semplifica il deployment e riduce i costi di licenza.

## Prerequisiti

### Java Development Kit (JDK)

Assicurati di avere installato l'ultima versione del Java Development Kit. Puoi scaricarlo da [qui](https://www.oracle.com/java/technologies/javase-downloads.html).

### Libreria Aspose.OCR per Java

Scarica e installa la libreria Aspose.OCR per Java dal [link di download](https://releases.aspose.com/ocr/java/).

### Licenza Aspose.OCR

Per sbloccare tutte le funzionalità, ottieni una licenza. Puoi acquistarne una da [qui](https://purchase.aspose.com/buy) o richiedere una [licenza temporanea](https://purchase.aspose.com/temporary-license/) per scopi di prova.

## Come utilizzare OCR con Aspose.OCR per Java?

Carica la tua immagine, configura il motore OCR e chiama il metodo di riconoscimento—tutto in poche righe di codice. Questo paragrafo di risposta diretta ti indica esattamente cosa fare: crea un'istanza `AsposeOCR` con la tua stringa di licenza, imposta eventuali caratteri consentiti e invoca `RecognizeLine` sull'immagine target per ricevere il testo estratto. L'API gestisce internamente il pre‑processamento dell'immagine, così ottieni risultati puliti senza codice aggiuntivo.

### Importare i pacchetti

La classe `AsposeOCR` si trova nel pacchetto `com.aspose.ocr`. Importa le classi necessarie prima di iniziare a scrivere il codice.

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Guida passo‑passo

### Passo 1: Impostare la directory dei documenti

Scegli una cartella dove verranno archiviati i risultati OCR e i file temporanei. Questo percorso verrà poi usato per individuare l'immagine da elaborare.

```java
String dataDir = "Your Document Directory";
```

### Passo 2: Specificare il percorso dell'immagine

Fornisci il percorso completo nel file system o una risorsa nel class‑path che punti all'immagine che desideri analizzare.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### Passo 3: Creare un'istanza Aspose.OCR

`AsposeOCR` è il motore principale che esegue il riconoscimento ottico dei caratteri. Istanzialo con una stringa di licenza temporanea o permanente.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### Passo 4: Eseguire il riconoscimento OCR

`RecognizeLine` estrae una singola riga di testo dall'immagine fornita e la restituisce come una semplice `String` Java. Puoi chiamare questo metodo più volte per documenti multilinea.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Suggerimento:** Se devi limitare l'output solo a cifre (ad esempio per numeri di fattura), chiama `setAllowedCharacters("0123456789")` sull'istanza `AsposeOCR` prima di invocare `RecognizeLine`. Questo costringe il motore a ignorare qualsiasi simbolo non numerico.  
> `setAllowedCharacters` è un metodo di `AsposeOCR` che limita l'output OCR a una whitelist di caratteri specificata.

## Problemi comuni e soluzioni

| Problema | Motivo | Correzione |
|----------|--------|------------|
| **Nessun output o stringa vuota** | Percorso immagine errato o formato non supportato | Verifica `imagePath` e usa un formato supportato (JPEG, PNG, BMP) |
| **Errori di riconoscimento** | Immagine a bassa risoluzione o sfondo rumoroso | Pre‑elabora l'immagine (aumenta contrasto, binarizza) prima dell'OCR |
| **Licenza non applicata** | Chiave di licenza mancante o non valida | Assicurati che la stringa di licenza sia corretta e passata al costruttore `AsposeOCR` |

## Domande frequenti

**Q: Come posso ottenere una licenza temporanea per Aspose.OCR?**  
A: Visita la [pagina della licenza temporanea](https://purchase.aspose.com/temporary-license/) per richiedere una chiave di prova che rimuove le filigrane di valutazione.

**Q: Dove posso trovare supporto per Aspose.OCR?**  
A: Unisciti alla community sul [Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) per assistenza e discussioni.

**Q: Posso specificare i caratteri consentiti in Aspose.OCR?**  
A: Sì, usa l'API `setAllowedCharacters` per definire una whitelist personalizzata di caratteri. È ideale per campi solo numerici.

**Q: Aspose.OCR è compatibile con le ultime versioni di JDK?**  
A: Assolutamente—Aspose.OCR viene aggiornato regolarmente per rimanere compatibile con le ultime versioni di Java.

**Q: Ci sono funzionalità OCR aggiuntive oltre al riconoscimento di linee?**  
A: La libreria supporta anche il riconoscimento di blocchi, paragrafi e pagine intere, pacchetti linguistici e pre‑elaborazione avanzata delle immagini.

## Conclusione

Seguendo questo **tutorial Aspose OCR Java**, ora sai **come utilizzare OCR** per estrarre testo dalle immagini, limitare il set di caratteri e applicare una licenza temporanea per test rapidi. Approfondisci la [documentazione](https://reference.aspose.com/ocr/java/) completa per esplorare il supporto multilingua, l'elaborazione batch e le pipeline di pre‑elaborazione personalizzate.

---

**Ultimo aggiornamento:** 2026-05-24  
**Testato con:** Aspose.OCR for Java 24.11  
**Autore:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Tutorial correlati

- [Come impostare la licenza e verificare la licenza Aspose.OCR in Java](/ocr/java/ocr-basics/set-license/)
- [Convertire immagine in testo in Java usando Aspose.OCR BufferedImage](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Esempio Aspose OCR Java – Riconoscere linee nelle immagini](/ocr/java/advanced-ocr-techniques/recognize-lines/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}