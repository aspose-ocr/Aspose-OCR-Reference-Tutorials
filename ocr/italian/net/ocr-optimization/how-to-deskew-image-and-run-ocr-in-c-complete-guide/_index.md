---
category: general
date: 2026-03-07
description: Impara come correggere l'inclinazione dell'immagine, aumentare il contrasto
  ed estrarre il testo da una scansione usando Aspose OCR. Esegui l'OCR sull'immagine
  con un esempio completo in C# e carica facilmente l'immagine per l'OCR.
draft: false
keywords:
- how to deskew image
- extract text from scan
- how to boost contrast
- perform ocr on image
- load image for OCR
language: it
og_description: Scopri come raddrizzare l'immagine, aumentare il contrasto ed estrarre
  il testo dalla scansione usando Aspose OCR in C#. Esegui l'OCR sull'immagine con
  codice passo‑passo.
og_title: Come correggere l'inclinazione di un'immagine ed eseguire OCR in C# – Guida
  completa
tags:
- C#
- OCR
- Image Processing
title: Come correggere l'inclinazione di un'immagine ed eseguire OCR in C# – Guida
  completa
url: /it/net/ocr-optimization/how-to-deskew-image-and-run-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come correggere l'inclinazione di un'immagine ed eseguire OCR in C# – Guida completa

Se ti sei mai chiesto **come correggere l'inclinazione di un'immagine** prima di eseguire l'OCR, sei nel posto giusto. In questo tutorial ti guideremo attraverso l'aumento del contrasto, il caricamento di un'immagine per l'OCR e infine **estrarre il testo dalla scansione** con Aspose OCR.  

Che tu stia digitalizzando vecchie ricevute, pulendo contratti scansionati, o abbia semplicemente bisogno di un modo affidabile per leggere il testo da una foto inclinata, i passaggi seguenti coprono tutto ciò di cui hai bisogno. Niente fronzoli—solo un esempio funzionante che puoi copiare‑incollare in Visual Studio.  

## Cosa otterrai

* Correggere l'inclinazione fino a 30° (questa è la parte **come correggere l'inclinazione di un'immagine**).  
* Aumentare il contrasto dell'immagine per bordi dei caratteri più nitidi (**come aumentare il contrasto**).  
* Caricare la tua immagine nel motore OCR (**caricare immagine per OCR**).  
* Eseguire il processo di riconoscimento e **estrarre il testo dalla scansione**.  

Tutto ciò funziona con l'ultima versione del pacchetto NuGet Aspose.OCR .NET (v23.11 al momento della stesura).  

---

![Esempio di correzione dell'inclinazione dell'immagine](/images/deskew-example.png "come correggere l'inclinazione dell'immagine")

*L'immagine sopra mostra un documento scansionato prima e dopo la correzione dell'inclinazione.*

## Prerequisiti

* .NET 6.0 o versioni successive (il codice funziona anche su .NET Framework 4.7+).  
* Visual Studio 2022 (o qualsiasi IDE C# tu preferisca).  
* Pacchetto NuGet Aspose.OCR – installa tramite `dotnet add package Aspose.OCR`.  

Tutto qui. Nessun servizio esterno, nessuna chiave API.

---

## Come correggere l'inclinazione dell'immagine con Aspose OCR

La prima cosa che facciamo è creare un **ImageProcessingPipeline** e aggiungere un `DeskewFilter`. Il filtro rileva automaticamente l'angolo dominante della linea di testo e ruota l'immagine nuovamente in orizzontale.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Build a pipeline – Deskew is the first filter
var processingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { MaxAngle = 30 })   // how to deskew image up to 30°
    .Add(new DenoiseFilter { Level = DenoiseLevel.High }) // remove noise
    .Add(new ContrastBoostFilter { Strength = 1.5 })      // how to boost contrast
    .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize

// Attach the pipeline to the engine
ocrEngine.Settings.ImageProcessing = processingPipeline;
```

**Perché è importante:**  
Una scansione inclinata confonde il motore OCR perché i caratteri non sono più allineati alla linea di base. Il `DeskewFilter` analizza l'istogramma dell'immagine, trova l'angolo e la ruota, migliorando drasticamente l'accuratezza del riconoscimento.

> **Consiglio professionale:** Se sai che i tuoi documenti non superano un'inclinazione di 15°, imposta `MaxAngle = 15` per velocizzare l'elaborazione.

---

## Come aumentare il contrasto per un riconoscimento migliore

Dopo la correzione dell'inclinazione, il passo successivo è far risaltare il testo. Il `ContrastBoostFilter` estende l'intervallo di intensità dei pixel, il che è particolarmente utile per stampe sbiadite.

```csharp
// The ContrastBoostFilter is already in the pipeline above.
// You can tweak the Strength value (1.0 = no change, >1.0 = stronger boost)
.Add(new ContrastBoostFilter { Strength = 1.5 })
```

**Perché aiuta:**  
Le scansioni a basso contrasto producono caratteri grigi che il binarizzatore può interpretare come sfondo. Aumentare il contrasto rende i pixel scuri più scuri e quelli chiari più chiari, fornendo al successivo `BinarizationFilter` una tela più pulita.

---

## Eseguire OCR sull'immagine – Caricamento del file

Ora che l'immagine è pre‑elaborata, dobbiamo **caricare l'immagine per OCR**. Aspose offre un comodo helper `ImageStream.FromFile`.

```csharp
// Load the source image – replace the path with your own file
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Se la tua immagine è in uno stream (ad esempio, caricata tramite una web API), puoi usare `ImageStream.FromStream(yourStream)` al suo posto. Il motore accetta BMP, JPEG, PNG, TIFF e molti altri.

---

## Eseguire il processo di riconoscimento ed estrarre il testo dalla scansione

Con tutto collegato, chiamare `Recognize()` fa il lavoro pesante. Dopo la chiamata, il testo riconosciuto è disponibile tramite `ocrEngine.Text`.

```csharp
// Run OCR
ocrEngine.Recognize();

// Output the result
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrEngine.Text);
```

**Output previsto** (esempio per una semplice fattura):

```
=== Extracted Text ===
Invoice #12345
Date: 03/05/2026
Total: $1,250.00
Thank you for your business!
```

Se l'output appare confuso, ricontrolla l'ordine della pipeline—prima la correzione dell'inclinazione, poi la riduzione del rumore, l'aumento del contrasto e infine la binarizzazione. Scambiarli può degradare i risultati.

---

## Problemi comuni e casi particolari

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| **Risultato vuoto** | L'immagine è troppo scura o troppo chiara per il metodo di binarizzazione predefinito. | Aumentare `ContrastBoostFilter.Strength` o passare a `BinarizationMethod.Otsu`. |
| **Testo parziale mancante** | Il rumore rimane dopo la riduzione del rumore. | Usare `DenoiseLevel.Medium` per immagini più delicate, o aggiungere un secondo `DenoiseFilter`. |
| **Direzione di rotazione errata** | Il documento ha orientamento misto (ad esempio, una foto di una pagina ruotata). | Impostare manualmente `DeskewFilter.MaxAngle` più basso e pre‑ruotare l'immagine con `ImageProcessor.Rotate`. |
| **Rallentamento delle prestazioni** | Grande batch di immagini ad alta risoluzione. | Ridimensionare le immagini (`ImageProcessor.Resize`) prima della pipeline, o elaborare in parallelo (`Parallel.ForEach`). |

---

## Esempio completo funzionante (pronto per copia‑incolla)

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build image‑processing pipeline
        var processingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { MaxAngle = 30 })                     // how to deskew image up to 30°
            .Add(new DenoiseFilter { Level = DenoiseLevel.High })       // remove high‑level noise
            .Add(new ContrastBoostFilter { Strength = 1.5 })            // how to boost contrast
            .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize image

        // 3️⃣ Attach pipeline to OCR settings
        ocrEngine.Settings.ImageProcessing = processingPipeline;

        // 4️⃣ Load the image you want to OCR
        // Replace the path with the location of your own file
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition engine
        ocrEngine.Recognize();

        // 6️⃣ Display the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

Salva questo come `Program.cs`, esegui `dotnet run` e osserva la console stampare il risultato di **estrarre il testo dalla scansione**.  

---

## Prossimi passi e argomenti correlati

* **Elaborazione batch** – Avvolgi la logica sopra in un ciclo per gestire decine di file.  
* **Pacchetti linguistici personalizzati** – Se devi leggere script non latini, carica un modello linguistico tramite `ocrEngine.Settings.Language = OcrLanguage.ChineseSimplified;`.  
* **Output PDF** – Combina Aspose.PDF con OCR per incorporare testo ricercabile direttamente in un file PDF.  
* **Ottimizzazione delle prestazioni** – Sperimenta l'ordine di `ImageProcessingPipeline`; a volte la riduzione del rumore prima della correzione dell'inclinazione produce risultati più rapidi su foto rumorose.  

Tutti questi si basano sui concetti fondamentali trattati: **come correggere l'inclinazione dell'immagine**, **come aumentare il contrasto**, **caricare l'immagine per OCR**, **eseguire OCR sull'immagine**, e infine **estrarre il testo dalla scansione**.

---

## Conclusione

Abbiamo appena dimostrato un modo completo e pronto per la produzione per **correggere l'inclinazione dell'immagine** ed eseguire OCR in C#. Concatenando un filtro di correzione dell'inclinazione, un passo di riduzione del rumore, un aumento del contrasto e un binarizzatore, ottieni un input pulito che permette ad Aspose OCR di **estrarre il testo dalla scansione** in modo affidabile.  

Prova il codice, regola i parametri dei filtri per i tuoi documenti e vedrai quanto rapidamente migliora l'accuratezza del riconoscimento. Hai domande? Lascia un commento e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}