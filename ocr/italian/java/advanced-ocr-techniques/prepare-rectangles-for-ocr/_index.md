---
date: 2025-12-06
description: Scopri come utilizzare Aspose.OCR per Java per eseguire il riconoscimento
  OCR del testo, estrarre il testo dalle immagini e preparare rettangoli per il riconoscimento
  mirato.
language: it
linktitle: Preparing Rectangles for OCR Text Recognition in Aspose.OCR
second_title: Aspose.OCR Java API
title: Preparazione dei rettangoli per il riconoscimento del testo OCR in Aspose.OCR
url: /java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Preparare i Rettangoli per il Riconoscimento del Testo OCR in Aspose.OCR

## Introduction

Nel mondo odierno guidato dai dati, il **ocr text recognition** è una pietra angolare per trasformare documenti scansionati, screenshot e foto in contenuti ricercabili e modificabili. Aspose.OCR per Java rende questo processo veloce e affidabile, soprattutto quando è necessario concentrarsi su aree specifiche di un'immagine. In questo tutorial percorreremo tutti i passaggi necessari per preparare rettangoli che limitano l'OCR alle regioni di interesse, offrendoti un controllo preciso e migliori prestazioni.

## Quick Answers
- **Quale libreria gestisce il riconoscimento del testo OCR in Java?** Aspose.OCR for Java.  
- **Ho bisogno di una licenza per l'uso in produzione?** Sì – una licenza valida di Aspose.OCR sblocca tutte le funzionalità.  
- **Posso limitare l'OCR a determinate parti di un'immagine?** Assolutamente; definisci rettangoli che delimitano le zone di interesse.  
- **Quali sono i prerequisiti principali?** JDK 17+, Aspose.OCR for Java e un IDE Java.  
- **Questo approccio è adatto per estrarre testo dalle immagini?** Sì, è un modo efficiente per **extract text image java** progetti.

## What is OCR Text Recognition?
Il riconoscimento del testo OCR (Optical Character Recognition) converte immagini basate su pixel in caratteri leggibili da macchine. Consente di cercare, modificare e analizzare contenuti che originariamente esistevano solo come immagini.

## Why Prepare Rectangles for OCR Text Recognition?
Definire rettangoli concentra il motore sulle regioni che contengono effettivamente testo, il che:
* Riduce il tempo di elaborazione.
* Migliora l'accuratezza ignorando sfondi rumorosi.
* Consente di estrarre solo i dati necessari—perfetto per moduli, fatture e ricevute.

## Prerequisites

Prima di iniziare, assicurati di avere:

- **Java Development Kit (JDK)** – Aspose.OCR per Java funziona con JDK 17 o versioni successive. Scaricalo dal sito Oracle.
- **Aspose.OCR per Java library** – Ottieni l'ultimo JAR dalla pagina di download ufficiale [qui](https://releases.aspose.com/ocr/java/). Segui la guida di installazione [qui](https://reference.aspose.com/ocr/java/).
- **Ambiente di sviluppo** – Qualsiasi IDE Java (IntelliJ IDEA, Eclipse, VS Code, ecc.) va bene.

## Import Packages

Nel tuo file sorgente Java, importa le classi Aspose.OCR necessarie e le utility standard di Java:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

> *Importiamo `java.awt.Rectangle` perché l'API OCR si aspetta rettangoli che definiscono le regioni da analizzare.*

## Step 1: Set Up License

```java
SetLicense.main(null);
```

Chiamare `SetLicense` attiva la tua licenza Aspose.OCR, rimuovendo i limiti di valutazione e abilitando il riconoscimento del testo OCR con tutte le funzionalità.

## Step 2: Define Document Directory and Image Path

```java
String dataDir = "Your Document Directory";
String imagePath = dataDir + "p.png";
```

Sostituisci `"Your Document Directory"` con il percorso assoluto dove si trova la tua immagine (`p.png`). Questa è l'immagine che verrà elaborata.

## Step 3: Create Aspose.OCR Instance

```java
AsposeOCR api = new AsposeOCR();
```

Istanziare `AsposeOCR` ti dà accesso al metodo `RecognizePage`, che esegue l'OCR vero e proprio.

## Step 4: Prepare Rectangles with Texts

```java
ArrayList<Rectangle> rectArray = new ArrayList<Rectangle>();
rectArray.add(new Rectangle(138, 352, 2033, 537));
rectArray.add(new Rectangle(147, 890, 2033, 1157));
rectArray.add(new Rectangle(923, 2045, 465, 102));
rectArray.add(new Rectangle(104, 2147, 2076, 819));
```

Ogni `Rectangle(x, y, width, height)` indica ad AsposeOCR esattamente dove cercare il testo. Regola le coordinate per corrispondere al layout della tua immagine di origine.

## Step 5: Perform OCR Recognition

```java
try {
    String result = api.RecognizePage(imagePath, rectArray);
    System.out.println("Result with rect: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

La chiamata `RecognizePage` elabora solo i rettangoli definiti e restituisce la stringa estratta. L'output della console ti consente di verificare immediatamente il risultato del **ocr text recognition**.

## Common Issues and Tips

| Problema | Causa | Soluzione |
|----------|-------|-----------|
| **Nessun output** | Coordinate dei rettangoli o percorso dell'immagine errati | Verifica il valore di `dataDir` e assicurati che i rettangoli coprano effettivamente le regioni di testo. |
| **Caratteri spazzatura** | Immagine a bassa risoluzione o font non supportato | Usa una sorgente a risoluzione più alta o applica pre‑elaborazione dell'immagine (es. binarizzazione). |
| **Licenza non applicata** | `SetLicense` non chiamato prima dell'OCR | Assicurati che `SetLicense.main(null);` venga eseguito prima di qualsiasi chiamata API. |
| **Ritardo delle prestazioni** | Troppi rettangoli grandi | Limita il numero di rettangoli e tienili il più aderenti possibile al testo. |

## Conclusion

Ora hai imparato come integrare Aspose.OCR per Java, configurare una licenza, definire i percorsi delle immagini e—soprattutto—preparare rettangoli per concentrare il **ocr text recognition** su parti specifiche di un'immagine. Questa tecnica è ideale per qualsiasi **java ocr tutorial** che richieda un'estrazione di testo precisa e ad alte prestazioni.

## Frequently Asked Questions

**D: Aspose.OCR è compatibile con altri linguaggi di programmazione?**  
R: Sì, Aspose.OCR supporta anche .NET, C++ e Python. Consulta la documentazione ufficiale per esempi specifici per linguaggio.

**D: Posso usare Aspose.OCR in un progetto commerciale?**  
R: Assolutamente. Acquista una licenza commerciale tramite l'[Aspose store](https://purchase.aspose.com/buy).

**D: È disponibile una versione di prova gratuita?**  
R: Sì, puoi scaricare una versione di prova [qui](https://releases.aspose.com/).

**D: Come posso ottenere una licenza temporanea per la valutazione?**  
R: Le licenze temporanee sono fornite tramite il [portale di licenza temporanea Aspose](https://purchase.aspose.com/temporary-license/).

**D: Dove posso trovare supporto dalla community?**  
R: Visita il [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) per domande, suggerimenti e esempi di codice.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-06  
**Tested With:** Aspose.OCR for Java 24.12  
**Author:** Aspose  

---