---
category: general
date: 2026-04-29
description: come correggere l'inclinazione dell'immagine e migliorare l'accuratezza
  OCR con Aspose OCR – impara a rimuovere il rumore, aumentare il contrasto dell'immagine
  ed estrarre il testo dalle immagini.
draft: false
keywords:
- how to deskew image
- remove noise from image
- boost image contrast
- extract text from image
- improve ocr accuracy
language: it
og_description: come correggere l'inclinazione di un'immagine e migliorare l'accuratezza
  OCR. Questo tutorial mostra come rimuovere il rumore dall'immagine, aumentare il
  contrasto dell'immagine ed estrarre il testo dall'immagine usando Aspose OCR.
og_title: come correggere l'inclinazione dell'immagine – Guida completa a Aspose OCR
tags:
- Aspose OCR
- C#
- Image preprocessing
title: come raddrizzare l'immagine – Guida alla pre‑elaborazione OCR di Aspose
url: /it/net/ocr-optimization/how-to-deskew-image-aspose-ocr-preprocessing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# come correggere l'inclinazione di un'immagine – Guida completa Aspose OCR

Ti sei mai chiesto **come correggere l'inclinazione di un'immagine** prima di inviarla a un motore OCR? Non sei il solo. Una scansione storta o una foto scattata di lato può compromettere il riconoscimento del testo, lasciandoti con un output incomprensibile.  

In questo tutorial percorreremo una soluzione completa, end‑to‑end, che non solo **come correggere l'inclinazione di un'immagine** ma anche **rimuovere il rumore dall'immagine**, **aumentare il contrasto dell'immagine**, e infine **estrarre testo dall'immagine** con Aspose OCR. Alla fine vedrai come **migliorare la precisione OCR** senza dover setacciare la documentazione.

> **Cosa otterrai:** un'app console C# pronta all'uso, una spiegazione chiara di ogni passaggio di pre‑elaborazione e una serie di consigli pratici da copiare‑incollare nei tuoi progetti.

## Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche con .NET Core e .NET Framework)  
- Pacchetto NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Un'immagine di esempio che sia inclinata, rumorosa o a basso contrasto (ad es., `skewed_noisy.jpg`)  
- Visual Studio, VS Code o qualsiasi editor C# tu preferisca  

Non sono richieste librerie native aggiuntive – Aspose gestisce tutto in‑process.

---

## Come correggere l'inclinazione di un'immagine con Aspose OCR

La prima cosa di cui abbiamo bisogno è un filtro di correzione dell'inclinazione che aggiusti l'angolo di rotazione. Aspose OCR include `FilterDeskew`, che analizza le linee di base del testo e ruota il bitmap di conseguenza.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that will later recognize text.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Build an image‑processing pipeline.
        //    The order matters: deskew → denoise → contrast boost.
        ImageProcessingPipeline processingPipeline = new ImageProcessingPipeline();
        processingPipeline.Add(new FilterDeskew());          // ✅ how to deskew image
        processingPipeline.Add(new FilterDenoise());         // ✅ remove noise from image
        processingPipeline.Add(new FilterContrastBoost());   // ✅ boost image contrast

        // 3️⃣ Load your source picture.
        var sourceImage = OcrEngine.LoadImage(@"YOUR_DIRECTORY/skewed_noisy.jpg");

        // 4️⃣ Apply the pipeline – the image is now straight, cleaner, and sharper.
        var processedImage = processingPipeline.Apply(sourceImage);

        // 5️⃣ Run OCR on the cleaned‑up bitmap.
        var ocrResult = ocrEngine.Recognize(processedImage);

        // 6️⃣ Print the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Perché iniziare con la correzione dell'inclinazione:**  
Se le linee di testo non sono orizzontali, il motore OCR interpreterà i caratteri inclinati come glifi diversi, riducendo drasticamente **migliorare la precisione OCR**. La correzione allinea le linee di base, fornendo al riconoscitore una tela pulita.

> *Consiglio professionale:* Se conosci in anticipo l'angolo di rotazione (ad es., tutte le scansioni sono di 90°), puoi saltare il filtro e ruotare manualmente – è un piccolo guadagno di prestazioni.

---

## Rimuovere il rumore dall'immagine – Pulire la scansione

Il rumore appare come macchie nere o bianche casuali (il classico pattern “sale‑e‑pepe”) e può confondere la segmentazione dei caratteri. `FilterDenoise` applica un filtro mediano che li smussa mantenendo i bordi.

```csharp
// Inside the pipeline we already added FilterDenoise.
// If you need a custom strength, you can instantiate it like:
var denoise = new FilterDenoise { Strength = 2 }; // 1‑3 are typical values
processingPipeline.Add(denoise);
```

**Quando regolare l'intensità:**  
- **Strength = 1** – Granello leggero, elaborazione rapida.  
- **Strength = 3** – Scansioni molto rumorose (ad es., documenti fax).  

Aumentare troppo l'intensità può sfocare i tratti sottili, il che potrebbe *danneggiare* **migliorare la precisione OCR**. Prova un paio di valori su un campione rappresentativo.

---

## Aumentare il contrasto dell'immagine – Evidenziare i caratteri deboli

Le immagini a basso contrasto (pensa a ricevute sbiadite) spesso fanno sì che il motore OCR perda i glifi leggeri. `FilterContrastBoost` allunga l'istogramma in modo che i pixel scuri diventino più scuri e quelli chiari più chiari.

```csharp
var contrast = new FilterContrastBoost { ContrastLevel = 1.5f }; // 1.0 = no change
processingPipeline.Add(contrast);
```

**Perché il contrasto è importante:**  
Un contrasto più elevato migliora il rapporto segnale‑rumore, facilitando il riconoscitore neurale di Aspose nel distinguere “I” da “l”. Tuttavia, un eccessivo potenziamento può saturare l'immagine, trasformando gradienti morbidi in bordi netti che sembrano artefatti. Mira a un equilibrio; 1.5‑2.0 è un buon punto di partenza.

---

## Estrarre testo dall'immagine – L'ultimo passo OCR

Ora che l'immagine è dritta, pulita e vivida, il motore OCR può fare il suo lavoro. Il metodo `Recognize` restituisce un oggetto `OcrResult` contenente il testo grezzo, i punteggi di confidenza e persino le bounding box se ti servono.

```csharp
var ocrResult = ocrEngine.Recognize(processedImage);
Console.WriteLine(ocrResult.Text);
```

**Esempio di output** (supponendo che l'immagine di origine contenga “Invoice #12345”):

```
=== OCR Output ===
Invoice #12345
Date: 04/28/2026
Total: $1,234.56
```

Se noti caratteri mancanti, ricontrolla la pipeline di pre‑elaborazione – forse l'immagine necessita ancora di una denoise più forte o di un livello di contrasto diverso.  

> *Domanda frequente:* “E se devo riconoscere una lingua diversa dall'inglese?”  
> Basta impostare `ocrEngine.Language = Language.English;` a un'altra lingua supportata (ad es., `Language.French`). I passaggi di pre‑elaborazione rimangono gli stessi.

---

## Migliorare la precisione OCR – Ottimizzazioni aggiuntive

Anche con una pipeline perfetta, qualche ulteriore impostazione può spingere **migliorare la precisione OCR** ancora più in là:

| Suggerimento | Quando usarlo | Come |
|-----|--------------|-----|
| **Soglia binaria** | Scansioni molto scure o molto chiare | `processingPipeline.Add(new FilterBinarize());` |
| **Ridimensionare l'immagine** | Font piccoli (<10 pt) | `processedImage = OcrEngine.Resize(processedImage, 2.0);` |
| **Specificare il set di caratteri** | Alfabeto noto (solo cifre, ecc.) | `ocrEngine.Characters = "0123456789";` |
| **PDF multi‑pagina** | Elaborazione batch | Loop su ogni pagina e riutilizza la stessa pipeline. |

Ricorda: ogni filtro aggiuntivo incrementa il tempo di elaborazione, quindi abilita solo ciò di cui hai realmente bisogno.

---

## Esempio completo funzionante (pronto da copiare‑incollare)

Di seguito trovi l'intero programma, pronto per la compilazione. Sostituisci `YOUR_DIRECTORY` con la cartella che contiene `skewed_noisy.jpg`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Build preprocessing pipeline
        ImageProcessingPipeline pipeline = new ImageProcessingPipeline();
        pipeline.Add(new FilterDeskew());                     // how to deskew image
        pipeline.Add(new FilterDenoise { Strength = 2 });    // remove noise from image
        pipeline.Add(new FilterContrastBoost { ContrastLevel = 1.8f }); // boost image contrast

        // Load source image
        var sourcePath = @"YOUR_DIRECTORY/skewed_noisy.jpg";
        var sourceImage = OcrEngine.LoadImage(sourcePath);

        // Apply pipeline
        var cleanImage = pipeline.Apply(sourceImage);

        // Perform OCR
        var result = ocrEngine.Recognize(cleanImage);

        // Output
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(result.Text);
    }
}
```

**Risultato atteso:** testo pulito e dritto stampato sulla console, con molte meno errori di riconoscimento rispetto all'invio del file grezzo direttamente a `ocrEngine.Recognize`.

---

## Conclusione

Abbiamo coperto **come correggere l'inclinazione di un'immagine**, come **rimuovere il rumore dall'immagine**, come **aumentare il contrasto dell'immagine** e infine come **estrarre testo dall'immagine** usando Aspose OCR. Concatenando questi filtri vedrai un salto notevole in **migliorare la precisione OCR**, soprattutto su scansioni di bassa qualità.

Pronto per la prossima sfida? Prova a inviare un PDF multi‑pagina nella stessa pipeline, o sperimenta soglie personalizzate per la binarizzazione. Gli stessi principi valgono – raddrizza, pulisci, illumina, poi riconosci.

Hai domande o un caso limite strano? Lascia un commento e risolviamo insieme. Buon coding!  

![how to deskew image example](deskew-example.png "how to deskew image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}