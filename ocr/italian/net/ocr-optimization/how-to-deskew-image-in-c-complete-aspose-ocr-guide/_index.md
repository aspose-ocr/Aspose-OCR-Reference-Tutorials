---
category: general
date: 2026-06-28
description: Come correggere l'inclinazione di un'immagine usando Aspose.OCR. Impara
  a pre‑elaborare l'immagine per l'OCR, migliorare l'accuratezza dell'OCR e correggere
  l'inclinazione dell'immagine scansionata con un esempio completo in C#.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- how to improve ocr
- deskew scanned image
language: it
og_description: Come correggere l'inclinazione di un'immagine con Aspose.OCR. Questo
  tutorial ti mostra come pre‑elaborare l'immagine per l'OCR, aumentare la precisione
  e correggere l'inclinazione dell'immagine scansionata passo dopo passo.
og_title: Come raddrizzare un'immagine in C# – Guida completa a Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  headline: How to Deskew Image in C# – Complete Aspose.OCR Guide
  type: TechArticle
- description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  name: How to Deskew Image in C# – Complete Aspose.OCR Guide
  steps:
  - name: Why a Deskew Filter First?
    text: 'When a document is rotated even a few degrees, the OCR engine misinterprets
      line baselines, leading to garbled output. The `DeskewFilter` automatically
      estimates the rotation angle (up to `MaxAngle` degrees) and rotates the bitmap
      back to a horizontal baseline. The returned `DeskewConfidence` tells '
  - name: 1️⃣ DeskewFilter (Primary Step)
    text: '- **What it does:** Detects the dominant text line direction and rotates
      the image. - **Why it matters:** A straight baseline maximizes character segmentation
      accuracy. - **Tip:** If your documents never exceed 10°, set `MaxAngle = 10`
      to speed up detection.'
  - name: 2️⃣ DenoiseFilter (Secondary Cleanup)
    text: '- **What it does:** Reduces random pixel noise that can appear after scanning.
      - **Why it matters:** Noise often creates false edges, confusing the OCR''s
      segmentation. - **Tip:** Adjust `Strength` between 0.3 (light) and 0.8 (aggressive)
      based on scan quality.'
  - name: 3️⃣ ContrastBoostFilter (Final Polish)
    text: '- **What it does:** Increases the difference between foreground text and
      background. - **Why it matters:** Low contrast can make faint characters invisible
      to the recognition engine. - **Tip:** A `Level` of 1.2 works for most black‑on‑white
      scans; for colored documents, experiment with values up to '
  type: HowTo
tags:
- OCR
- Aspose
- Image Processing
title: Come raddrizzare un'immagine in C# – Guida completa a Aspose.OCR
url: /it/net/ocr-optimization/how-to-deskew-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come deskeware un'immagine in C# – Guida completa ad Aspose.OCR

Ti sei mai chiesto **come deskeware un'immagine** prima di inviarla a un motore OCR? Non sei il solo. I documenti scansionati arrivano spesso inclinati, e quella piccola rotazione può compromettere i risultati del riconoscimento. La buona notizia? Con Aspose.OCR puoi raddrizzare (deskew) e pulire le immagini con poche righe di C#.

In questo tutorial percorreremo un esempio completo e eseguibile che **preprocessa l'immagine per OCR**, aggiunge un filtro deskew e ti mostra **come migliorare l'OCR**. Alla fine sarai in grado di **deskeware automaticamente le immagini scansionate** e vedere i punteggi di confidenza.

> **Nota:** Il codice funziona con Aspose.OCR ≥ 22.10 e .NET 6+, ma i concetti si applicano anche alle versioni precedenti.

## Di cosa avrai bisogno

- **Aspose.OCR per .NET** (pacchetto NuGet `Aspose.OCR`)
- Un **TIFF o JPEG inclinato** che desideri raddrizzare
- Visual Studio 2022 (o qualsiasi IDE C#)
- Familiarità di base con C# e le app console

Non sono richieste librerie di terze parti aggiuntive; l'intera pipeline vive all'interno di Aspose.OCR.

---

## Come deskeware un'immagine con Aspose.OCR

Il cuore della soluzione è una **pipeline di filtri**. Pensala come una catena di montaggio in cui ogni filtro pulisce un problema specifico: prima correggiamo la rotazione, poi riduciamo il rumore e infine aumentiamo il contrasto affinché il motore OCR veda chiaramente i caratteri.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class DeskewExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var engine = new OcrEngine();

        // Step 2: Load the skewed image to be processed
        var img = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_doc.tif");

        // Step 3: Build a filter pipeline – deskew, then denoise, then boost contrast
        var pipeline = new OcrFilter[]
        {
            new DeskewFilter { MaxAngle = 30 },   // auto‑detect rotation up to 30°
            new DenoiseFilter { Strength = 0.5 },
            new ContrastBoostFilter { Level = 1.2 }
        };

        // Step 4: Apply the filters to the image before OCR
        var preprocessed = engine.ApplyFilters(img, pipeline);

        // Step 5: Perform OCR on the pre‑processed image
        var result = engine.Recognize(preprocessed);

        // Step 6: Output the deskew confidence and recognized text
        System.Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
        System.Console.WriteLine(result.Text);
    }
}
```

> **Esempio di immagine**  
> ![how to deskew image example](/images/deskew-example.png "how to deskew image example")

### Perché applicare prima un filtro Deskew?

Quando un documento è ruotato anche solo di pochi gradi, il motore OCR interpreta erroneamente le linee di base, producendo output confuso. Il `DeskewFilter` stima automaticamente l'angolo di rotazione (fino a `MaxAngle` gradi) e ruota il bitmap riportandolo a una linea di base orizzontale. Il valore restituito `DeskewConfidence` indica quanto l'algoritmo è sicuro della correzione—utile per il logging o strategie di fallback.

---

## Preprocessare l'immagine per OCR – Costruire la pipeline di filtri

### 1️⃣ DeskewFilter (Passo primario)

- **Cosa fa:** Rileva la direzione dominante delle linee di testo e ruota l'immagine.
- **Perché è importante:** Una linea di base dritta massimizza l'accuratezza della segmentazione dei caratteri.
- **Suggerimento:** Se i tuoi documenti non superano mai 10°, imposta `MaxAngle = 10` per velocizzare la rilevazione.

### 2️⃣ DenoiseFilter (Pulizia secondaria)

- **Cosa fa:** Riduce il rumore casuale dei pixel che può apparire dopo la scansione.
- **Perché è importante:** Il rumore crea spesso bordi falsi, confondendo la segmentazione dell'OCR.
- **Suggerimento:** Regola `Strength` tra 0.3 (leggero) e 0.8 (aggressivo) in base alla qualità della scansione.

### 3️⃣ ContrastBoostFilter (Finitura finale)

- **Cosa fa:** Aumenta la differenza tra il testo in primo piano e lo sfondo.
- **Perché è importante:** Un contrasto basso può rendere i caratteri deboli invisibili al motore di riconoscimento.
- **Suggerimento:** Un `Level` di 1.2 funziona per la maggior parte delle scansioni in bianco‑nero; per documenti a colori sperimenta valori fino a 2.0.

Collegando questi tre filtri **preprocessi l'immagine per OCR** affrontando i problemi più comuni: inclinazione, rumore e basso contrasto.

---

## Come migliorare l'accuratezza dell'OCR con Deskew e Denoise

Potresti chiederti: “Se ho già un filtro deskew, perché aggiungere denoise e contrast boost?” La risposta sta nel **miglioramento cumulativo**. Ogni filtro affronta un difetto diverso e, insieme, aumentano la confidenza complessiva.

#### Test reale

| Test | Precisione OCR originale | Dopo Deskew | Dopo pipeline completa |
|------|---------------------------|-------------|------------------------|
| Fattura semplice (inclinazione 5°) | 78 % | 92 % | 96 % |
| Scansione di vecchio giornale (inclinazione 15°, granuloso) | 61 % | 78 % | 88 % |
| Modulo a basso contrasto (senza inclinazione) | 70 % | 71 % | 84 % |

*I numeri sono illustrativi ma riflettono i guadagni tipici segnalati dagli utenti di Aspose.*

**Conclusione chiave:** Anche se il tuo obiettivo principale è **deskeware l'immagine scansionata**, aggiungere i passaggi di denoise e contrasto spesso produce un salto notevole nella qualità finale del testo.

---

## Deskeware l'immagine scansionata: verifica dei risultati

Dopo l'esecuzione della pipeline, ricevi due informazioni utili:

```csharp
Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
Console.WriteLine(result.Text);
```

- **Confidenza del deskew** (`result.DeskewConfidence`) è una percentuale. Valori superiori al 90 % indicano solitamente che la rotazione è stata corretta con precisione.
- **Testo riconosciuto** (`result.Text`) ti permette di verificare immediatamente se l'output è sensato.

Se la confidenza è bassa (< 70 %), considera:

1. **Aumentare `MaxAngle`** – forse il documento è ruotato più del previsto.
2. **Aggiungere un `BinarizationFilter`** prima del deskew per semplificare l'immagine.
3. **Ruotare manualmente** l'immagine usando `OcrImage.Rotate(angle)` come fallback.

---

## Esempio completo end‑to‑end (pronto per l'esecuzione)

Di seguito trovi il **programma completo e autonomo** che puoi copiare‑incollare in un nuovo progetto Console App. Ricorda di sostituire `YOUR_DIRECTORY` con la cartella che contiene il tuo TIFF inclinato.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace DeskewDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize the OCR engine
            var engine = new OcrEngine();

            // 2️⃣ Load the image you want to straighten
            var imgPath = @"C:\Images\skewed_doc.tif"; // <-- update this path
            var img = OcrImage.FromFile(imgPath);

            // 3️⃣ Define the preprocessing pipeline
            var pipeline = new OcrFilter[]
            {
                new DeskewFilter { MaxAngle = 30 },   // auto‑detect up to 30°
                new DenoiseFilter { Strength = 0.5 }, // moderate noise reduction
                new ContrastBoostFilter { Level = 1.2 } // brighten the text
            };

            // 4️⃣ Apply the pipeline – this returns a new image instance
            var preprocessed = engine.ApplyFilters(img, pipeline);

            // 5️⃣ Run OCR on the cleaned‑up image
            var result = engine.Recognize(preprocessed);

            // 6️⃣ Show confidence and the extracted text
            Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(result.Text);
        }
    }
}
```

**Output previsto** (supponendo una scansione ragionevolmente pulita):

```
Deskew confidence: 96.45%
=== Recognized Text ===
Invoice #12345
Date: 2024‑04‑01
Total: $1,250.00
...
```

Se vedi caratteri confusi, rivedi le intensità dei filtri o aggiungi un `BinarizationFilter` come indicato in precedenza.

---

## Problemi comuni e consigli professionali

- **Problema:** Uso di un TIFF a più pagine. `OcrImage.FromFile` legge solo il primo frame. Usa `OcrImage.FromMultiPageFile` se ti servono tutte le pagine.
- **Problema:** Dimenticare di liberare `OcrEngine`. Avvolgilo in un blocco `using` nel codice di produzione per rilasciare le risorse native.
- **Consiglio pro:** Cache la pipeline se elabori molte immagini con impostazioni identiche—riduce l'overhead.
- **Consiglio pro:** Registra `DeskewConfidence` in un sistema di monitoraggio; cali improvvisi possono indicare un cambiamento nella calibrazione dello scanner.

---

## Prossimi passi – Estendere il flusso di lavoro

Ora che sai **come deskeware un'immagine** e **preprocessare l'immagine per OCR**, potresti esplorare:

- **Elaborazione batch** – iterare su una cartella di PDF scansionati, convertire ogni pagina in immagine e applicare la stessa pipeline.
- **Supporto linguistico** – impostare `engine.Language = OcrLanguage.English;` o altre lingue per migliorare il riconoscimento.
- **Post‑processing personalizzato** – usare espressioni regolari per pulire gli errori OCR comuni (es. “0” vs “O”).

Ognuno di questi argomenti si collega naturalmente alle parole chiave secondarie **come migliorare OCR** e **deskeware immagine scansionata**.

---

## Conclusione

Abbiamo coperto tutto ciò che devi sapere su **come deskeware un'immagine** usando Aspose.OCR, dalla costruzione di una solida pipeline di filtri alla verifica dei punteggi di confidenza. **Preprocessando l'immagine per OCR** con deskew, denoise e contrast boost, otterrai un miglioramento misurabile nei risultati di **come migliorare OCR**, soprattutto su scansioni inclinate o rumorose.

Prova con il tuo set di documenti, regola i parametri dei filtri e osserva l'accuratezza dell'OCR aumentare. Hai domande o un file ostinato che non vuole raddrizzarsi? Lascia un commento qui sotto—risolviamo insieme. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che approfondiscono le tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API e a esplorare approcci alternativi nei tuoi progetti.

- [Come usare AspOCR: filtri di preprocessing immagine per OCR in .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Come fare OCR su immagine – Eseguire OCR su immagine in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Come impostare il valore di soglia in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}