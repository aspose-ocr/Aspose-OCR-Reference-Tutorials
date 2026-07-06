---
category: general
date: 2026-02-22
description: Come utilizzare l'OCR in Java per estrarre testo da un'immagine, migliorare
  l'accuratezza dell'OCR e caricare l'immagine per l'OCR con esempi di codice pratici.
draft: false
keywords:
- how to use OCR
- extract text from image
- improve OCR accuracy
- load image for OCR
- OCR preprocessing
language: it
og_description: Come utilizzare l'OCR in Java per estrarre il testo da un'immagine
  e migliorare l'accuratezza dell'OCR. Segui questa guida per un esempio pronto all'uso.
og_title: Come usare OCR in Java – Guida completa passo‑a‑passo
tags:
- OCR
- Java
- Image Processing
title: Come usare l'OCR in Java – Guida completa passo‑a‑passo
url: /it/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/
---

to keep the English phrase inside bold, as it's a keyword. Probably keep as is.

Similarly other bold phrases: **load image for OCR**, **improve OCR accuracy**, **how to use OCR** etc. Keep them unchanged.

Thus translate surrounding text but keep bold phrases unchanged.

Proceed.

Will translate each section.

Make sure to keep code block placeholders as they are.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare OCR in Java – Guida completa passo‑passo

Ti è mai capitato di dover **how to use OCR** su uno screenshot inclinato e di chiederti perché l'output sembra un pasticcio? Non sei l'unico. In molte applicazioni reali—scansione di ricevute, digitalizzazione di moduli o estrazione di testo da meme—ottenere risultati affidabili dipende da alcune impostazioni semplici.

In questo tutorial vedremo **how to use OCR** per *estrarre testo da file immagine*, ti mostreremo come **improve OCR accuracy**, e dimostreremo il modo corretto di **load image for OCR** usando una popolare libreria OCR per Java. Alla fine avrai un programma autonomo da inserire in qualsiasi progetto.

## Cosa imparerai

- Il codice esatto di cui hai bisogno per **load image for OCR** (senza dipendenze nascoste).
- Quali flag di pre‑elaborazione migliorano **improve OCR accuracy** e perché sono importanti.
- Come leggere il risultato OCR e stamparlo sulla console.
- Gli errori più comuni—come dimenticare di impostare una regione di interesse o ignorare la riduzione del rumore—e come evitarli.

### Prerequisiti

- Java 17 o superiore (il codice si compila con qualsiasi JDK recente).
- Una libreria OCR che fornisca le classi `OcrEngine`, `ImagePreprocessingOptions`, `OcrInput` e `OcrResult` (ad esempio il pacchetto fittizio `com.example.ocr` usato nello snippet). Sostituiscilo con la libreria reale che stai utilizzando.
- Un’immagine di esempio (`skewed_noisy.png`) posizionata in una cartella a cui puoi fare riferimento.

> **Pro tip:** Se stai usando un SDK commerciale, assicurati che il file di licenza sia nel classpath; altrimenti il motore lancerà un errore di inizializzazione.

---

## Step 1: Crea un'istanza di OCR Engine – **how to use OCR** in modo efficace

La prima cosa di cui hai bisogno è un oggetto `OcrEngine`. Pensalo come il cervello che interpreterà i pixel.

```java
// Step 1: Initialize the OCR engine
import com.example.ocr.OcrEngine;

OcrEngine ocrEngine = new OcrEngine();
```

*Perché è importante:* Senza un motore non hai contesto per modelli linguistici, set di caratteri o euristiche di immagine. Istanziare il motore subito ti permette anche di collegare le opzioni di pre‑elaborazione in seguito.

---

## Step 2: Configura la Pre‑elaborazione dell'Immagine – **improve OCR accuracy**

La pre‑elaborazione è la salsa segreta che trasforma una scansione rumorosa in testo pulito e leggibile dalla macchina. Qui abilitiamo la correzione dell'inclinazione, la riduzione del rumore ad alto livello, l'auto‑contrasto e una regione di interesse (ROI) per concentrarci sulla parte rilevante dell’immagine.

```java
import com.example.ocr.ImagePreprocessingOptions;
import java.awt.Rectangle;

// Step 2: Set up preprocessing to improve OCR accuracy
ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
preprocessing.setDeskewEnabled(true); // Correct image rotation
preprocessing.setNoiseReductionLevel(
        ImagePreprocessingOptions.NoiseReduction.HIGH); // Reduce speckles
preprocessing.setAutoContrastEnabled(true); // Boost contrast
preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600)); // Process a sub‑region only

ocrEngine.setPreprocessingOptions(preprocessing);
```

*Perché è importante:*  
- **Deskew** allinea il testo ruotato, fondamentale quando si scansionano ricevute non perfettamente piatte.  
- **Noise reduction** elimina pixel sparsi che altrimenti verrebbero interpretati come caratteri.  
- **Auto‑contrast** espande la gamma tonale, facendo risaltare le lettere più deboli.  
- **ROI** indica al motore di ignorare i bordi irrilevanti, risparmiando tempo e memoria.

Se salti uno di questi passaggi, è probabile che le prestazioni di **improve OCR accuracy** diminuiscano.

---

## Step 3: Carica l'Immagine per OCR – **load image for OCR** correttamente

Ora puntiamo effettivamente il motore al file che vogliamo leggere. La classe `OcrInput` può accettare più immagini, ma per questo esempio la manteniamo semplice.

```java
import com.example.ocr.OcrInput;

// Step 3: Load the image you want to extract text from
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png"); // replace with your real path
```

*Perché è importante:* Il percorso deve essere assoluto o relativo alla directory di lavoro; altrimenti il motore lancia una `FileNotFoundException`. Inoltre, il nome del metodo `add` suggerisce che puoi accodare diverse immagini—utile per l'elaborazione batch.

---

## Step 4: Esegui OCR e Stampa il Testo Riconosciuto – **how to use OCR** end‑to‑end

Infine, chiediamo al motore di riconoscere il testo e lo stampiamo. L'oggetto `OcrResult` contiene la stringa grezza, i punteggi di confidenza e i metadati riga per riga (se ti servono in seguito).

```java
import com.example.ocr.OcrResult;

// Step 4: Run OCR and print the extracted text
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Output previsto** (supponendo che l’immagine di esempio contenga “Hello, OCR World!”):

```
=== OCR Output ===
Hello, OCR World!
```

Se il risultato appare confuso, torna al Passo 2 e modifica le opzioni di pre‑elaborazione—magari riducendo il livello di riduzione del rumore o regolando il rettangolo ROI.

---

## Esempio Completo, Eseguibile

Di seguito trovi un programma Java completo che puoi copiare‑incollare in un file chiamato `OcrDemo.java`. Unisce tutti i passaggi discussi.

```java
// OcrDemo.java – A complete, runnable example showing how to use OCR in Java
import com.example.ocr.OcrEngine;
import com.example.ocr.ImagePreprocessingOptions;
import com.example.ocr.OcrInput;
import com.example.ocr.OcrResult;
import java.awt.Rectangle;

public class OcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing (this is the key to improve OCR accuracy)
        ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
        preprocessing.setDeskewEnabled(true);
        preprocessing.setNoiseReductionLevel(
                ImagePreprocessingOptions.NoiseReduction.HIGH);
        preprocessing.setAutoContrastEnabled(true);
        preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600));
        ocrEngine.setPreprocessingOptions(preprocessing);

        // 3️⃣ Load the image you want to extract text from
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace the path with your own image location
        ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run the OCR engine and print the result
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Salva il file, compila con `javac OcrDemo.java` e avvia con `java OcrDemo`. Se tutto è configurato correttamente vedrai il testo estratto stampato sulla console.

---

## Domande Frequenti & Casi Limite

| Domanda | Risposta |
|----------|----------|
| **E se la mia immagine è in formato JPEG?** | Il metodo `OcrInput.add()` accetta qualsiasi formato raster supportato—PNG, JPEG, BMP, TIFF. Basta cambiare l’estensione del file nel percorso. |
| **Posso elaborare più pagine contemporaneamente?** | Assolutamente. Chiama `ocrInput.add()` per ogni file, poi passa lo stesso `ocrInput` a `recognize()`. Il motore restituirà un `OcrResult` concatenato. |
| **E se il risultato OCR è vuoto?** | Verifica che la ROI contenga effettivamente del testo. Assicurati anche che `setDeskewEnabled(true)` sia attivo; una rotazione di 90° farà pensare al motore che l’immagine sia vuota. |
| **Come cambio il modello linguistico?** | La maggior parte delle librerie espone un metodo `setLanguage(String)` su `OcrEngine`. Chiamalo prima di `recognize()`, ad esempio `ocrEngine.setLanguage("eng")`. |
| **È possibile ottenere i punteggi di confidenza?** | Sì, `OcrResult` fornisce spesso `getConfidence()` per riga o per carattere. Usalo per filtrare i risultati a bassa confidenza. |

---

## Conclusione

Abbiamo coperto **how to use OCR** in Java dall’inizio alla fine: creazione del motore, configurazione della pre‑elaborazione per **improve OCR accuracy**, corretta **load image for OCR**, e infine stampa del testo estratto. Lo snippet di codice completo è pronto per l’esecuzione, e le spiegazioni forniscono il “perché” dietro ogni riga.

Pronto per il passo successivo? Prova a modificare il rettangolo ROI per focalizzarti su parti diverse dell’immagine, sperimenta con `NoiseReduction.MEDIUM`, o integra l’output in un PDF ricercabile. Puoi anche approfondire argomenti correlati come **extract text from image** usando servizi cloud, o elaborare in batch migliaia di file con una coda multithread.

Hai altre domande su OCR, pre‑elaborazione delle immagini o integrazione Java? Lascia un commento, e buona programmazione!

![Esempio di come usare OCR](/images/ocr-demo.png "how to use OCR – Java example showing preprocessing and result")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}