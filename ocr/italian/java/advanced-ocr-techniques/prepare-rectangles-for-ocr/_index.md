---
date: 2026-02-20
description: Scopri come riconoscere i rettangoli di pagina con Aspose.OCR per Java,
  estrarre progetti Java di immagini di testo e segui questo tutorial Aspose OCR per
  Java per un OCR preciso.
linktitle: How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR
second_title: Aspose.OCR Java API
title: Come riconoscere i rettangoli di pagina per il riconoscimento del testo OCR
  in Aspose.OCR
url: /it/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
weight: 13
---

.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come riconoscere i rettangoli di pagina per il riconoscimento del testo OCR in Aspose.OCR

Nelle moderne pipeline di automazione dei documenti, **recognize page rectangles** è la tecnica chiave che consente di indicare al motore OCR esattamente dove guardare. Limitando Aspose.OCR alle aree che contengono effettivamente testo, aumenti la velocità, riduci il rumore e ottieni risultati più puliti. In questo tutorial percorreremo ogni passaggio—configurazione della libreria, licenza, definizione dei rettangoli e chiamata finale all'API OCR—così potrai estrarre testo da qualsiasi immagine con sicurezza.

## Risposte rapide
- **Quale libreria gestisce il riconoscimento del testo OCR in Java?** Aspose.OCR per Java.  
- **È necessaria una licenza per l'uso in produzione?** Sì – una licenza valida di Aspose.OCR sblocca tutte le funzionalità.  
- **Posso limitare l'OCR a parti specifiche di un'immagine?** Assolutamente; definisci i rettangoli che delimitano le zone di interesse.  
- **Quali sono i prerequisiti principali?** JDK 17+, Aspose.OCR per Java e un IDE Java.  
- **Questo approccio è adatto per estrarre testo da immagini?** Sì, è un modo efficiente per **extract text image java** projects.

## Che cosa significa “recognize page rectangles”?
L'espressione si riferisce alla pratica di fornire un elenco di oggetti `java.awt.Rectangle` al motore OCR affinché elabori solo quelle specifiche regioni di una pagina. Questo approccio mirato riduce i tempi di elaborazione e migliora l'accuratezza, soprattutto su documenti complessi come fatture o moduli.

## Perché preparare i rettangoli per il riconoscimento del testo OCR?
Definire i rettangoli concentra il motore sulle regioni che contengono effettivamente testo, il che:
* Riduce i tempi di elaborazione.  
* Migliora l'accuratezza ignorando sfondi rumorosi.  
* Consente di estrarre solo i dati necessari—perfetto per moduli, fatture e ricevute.  

## Prerequisiti

Prima di iniziare, assicurati di avere:

- **Java Development Kit (JDK)** – Aspose.OCR per Java funziona con JDK 17 o versioni successive. Scaricalo dal sito Oracle.  
- **Libreria Aspose.OCR per Java** – Ottieni l'ultimo JAR dalla pagina di download ufficiale [qui](https://releases.aspose.com/ocr/java/). Segui la guida all'installazione [qui](https://reference.aspose.com/ocr/java/).  
- **Ambiente di sviluppo** – Qualsiasi IDE Java (IntelliJ IDEA, Eclipse, VS Code, ecc.) va bene.

## Importare i pacchetti

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

## Passo 1: Configurare la licenza

```java
SetLicense.main(null);
```

Chiamare `SetLicense` attiva la licenza di Aspose.OCR, rimuovendo i limiti di valutazione e abilitando il riconoscimento del testo OCR a piena funzionalità.

## Passo 2: Definire la directory del documento e il percorso dell'immagine

```java
String dataDir = "Your Document Directory";
String imagePath = dataDir + "p.png";
```

Sostituisci `"Your Document Directory"` con il percorso assoluto dove si trova la tua immagine (`p.png`). Questa è l'immagine che verrà elaborata.

## Passo 3: Creare un'istanza di Aspose.OCR

```java
AsposeOCR api = new AsposeOCR();
```

Instanziare `AsposeOCR` ti dà accesso al metodo `RecognizePage`, che esegue l'effettivo OCR.

## Passo 4: Preparare i rettangoli con i testi

```java
ArrayList<Rectangle> rectArray = new ArrayList<Rectangle>();
rectArray.add(new Rectangle(138, 352, 2033, 537));
rectArray.add(new Rectangle(147, 890, 2033, 1157));
rectArray.add(new Rectangle(923, 2045, 465, 102));
rectArray.add(new Rectangle(104, 2147, 2076, 819));
```

Ogni `Rectangle(x, y, width, height)` indica ad Aspose.OCR esattamente dove cercare il testo. Regola le coordinate per farle corrispondere al layout della tua immagine di origine.

## Passo 5: Eseguire il riconoscimento OCR

```java
try {
    String result = api.RecognizePage(imagePath, rectArray);
    System.out.println("Result with rect: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

La chiamata a `RecognizePage` elabora solo i rettangoli definiti e restituisce la stringa estratta. L'output sulla console ti permette di verificare immediatamente il risultato del **ocr text recognition**.

## Problemi comuni e suggerimenti

| Problema | Causa | Soluzione |
|----------|-------|-----------|
| **Nessun output** | Coordinate dei rettangoli o percorso dell'immagine errati | Verifica il valore di `dataDir` e assicurati che i rettangoli coprano effettivamente le regioni di testo. |
| **Caratteri spazzatura** | Immagine a bassa risoluzione o font non supportato | Usa una sorgente a risoluzione più alta o applica pre‑elaborazione dell'immagine (es. binarizzazione). |
| **Licenza non applicata** | `SetLicense` non chiamato prima dell'OCR | Assicurati che `SetLicense.main(null);` venga eseguito prima di qualsiasi chiamata API. |
| **Ritardo di prestazioni** | Troppi rettangoli grandi | Limita il numero di rettangoli e tienili il più aderenti possibile al testo. |

## Domande frequenti

**D:** *Aspose.OCR è compatibile con altri linguaggi di programmazione?*  
**R:** Sì, Aspose.OCR supporta anche .NET, C++ e Python. Consulta la documentazione ufficiale per esempi specifici per linguaggio.

**D:** *Posso usare Aspose.OCR in un progetto commerciale?*  
**R:** Assolutamente. Acquista una licenza commerciale tramite l'[Aspose store](https://purchase.aspose.com/buy).

**D:** *È disponibile una versione di prova gratuita?*  
**R:** Sì, puoi scaricare una versione di prova [qui](https://releases.aspose.com/).

**D:** *Come ottengo una licenza temporanea per la valutazione?*  
**R:** Le licenze temporanee sono fornite tramite il [portale licenze temporanee di Aspose](https://purchase.aspose.com/temporary-license/).

**D:** *Dove posso trovare supporto dalla community?*  
**R:** Visita il forum Aspose.OCR [qui](https://forum.aspose.com/c/ocr/16) per domande, suggerimenti e esempi di codice.

## Conclusione

Ora sai come **recognize page rectangles** con Aspose.OCR per Java, impostare una licenza, definire i percorsi delle immagini e—soprattutto—preparare rettangoli precisi per concentrare l'OCR sulle parti esatte dell'immagine di cui hai bisogno. Questa tecnica è ideale per qualsiasi **aspose ocr java tutorial** che richieda un'estrazione di testo precisa e ad alte prestazioni.

---

**Ultimo aggiornamento:** 2026-02-20  
**Testato con:** Aspose.OCR per Java 24.12  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}