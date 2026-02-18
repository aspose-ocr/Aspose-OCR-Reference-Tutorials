---
category: general
date: 2026-02-17
description: Scopri come eseguire l'OCR di un'immagine usando Aspose OCR su GPU. Codice
  passo‑passo per riconoscere il testo dall'immagine, caricare un'immagine ad alta
  risoluzione, impostare l'ID del dispositivo GPU ed estrarre il testo con Aspose.
draft: false
keywords:
- how to ocr image
- recognize text from image
- load high resolution image
- set gpu device id
- extract text using aspose
language: it
og_description: Come eseguire OCR su un'immagine con Aspose OCR su GPU. Segui il tutorial
  completo in C# per riconoscere il testo da un'immagine, caricare un'immagine ad
  alta risoluzione, impostare l'ID del dispositivo GPU ed estrarre il testo usando
  Aspose.
og_title: Come fare OCR di un'immagine con Aspose OCR – Guida C# accelerata GPU
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Come fare OCR di un'immagine con Aspose OCR – Guida C# accelerata da GPU
url: /it/net/ocr-optimization/how-to-ocr-image-with-aspose-ocr-gpu-accelerated-c-guide/
---

: keep **bold** etc.

Proceed.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come fare OCR su un'immagine con Aspose OCR – Guida C# accelerata da GPU

Ti sei mai chiesto **come fare OCR su un'immagine** quando il file è una scansione enorme, a 300 DPI, e hai bisogno dei risultati in pochi secondi? Non sei solo—gli sviluppatori combattono costantemente motori OCR lenti basati solo su CPU, soprattutto su immagini ad alta risoluzione. La buona notizia? Aspose OCR ti permette di sfruttare la tua GPU, riducendo drasticamente i tempi di elaborazione mantenendo alta l'accuratezza.

In questo tutorial vedremo un esempio completo e eseguibile che **recognizes text from image**, ti mostra come **load high resolution image**, ti consente di **set GPU device ID** e infine **extract text using Aspose**. Alla fine avrai un programma autonomo che potrai inserire in qualsiasi progetto .NET.

## Cosa ti servirà

- **.NET 6.0** o successivo (il codice funziona anche su .NET Framework 4.7+)
- **Aspose.OCR for .NET** pacchetto NuGet (versione 23.11 o più recente)
- Una macchina con GPU abilitata e CUDA 11+ (opzionale ma consigliato)
- Un JPEG/PNG ad alta risoluzione che vuoi OCRare (ad es., `highres_scan.jpg`)

Se ti manca qualcuno di questi, ottieni il pacchetto NuGet con:

```bash
dotnet add package Aspose.OCR
```

Non sono richieste librerie native aggiuntive; Aspose include il runtime CUDA per te.

![diagramma di come fare OCR su un'immagine](image-placeholder.png "Diagramma che illustra la pipeline OCR accelerata da GPU – come fare OCR su un'immagine")

## Passo 1: Crea il motore OCR e imposta l'ID del dispositivo GPU  

La prima cosa da fare è dire ad Aspose di eseguire sull GPU. È qui che entra in gioco **set GPU device ID**—se hai più GPU puoi scegliere quella più adatta al tuo carico di lavoro.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialize the OCR engine with GPU processing mode
var ocrEngine = new OcrEngine(new OcrEngineSettings
{
    ProcessingMode = ProcessingMode.Gpu, // Enable GPU acceleration
    GpuDeviceId = 0                     // Choose GPU #0 (change if you have several)
});
```

> **Perché è importante:** L'elaborazione su GPU scarica il lavoro pesante di analisi dell'immagine sui core paralleli, offrendoti un incremento di velocità di 3‑5× su scansioni tipiche. Se non imposti `GpuDeviceId`, Aspose usa il primo dispositivo per impostazione predefinita, il che va bene per configurazioni a singola GPU.

## Passo 2: Carica un'immagine ad alta risoluzione  

Successivamente, **load high resolution image** i dati in un formato che il motore OCR comprende. Aspose fornisce `ImageStream.FromFile`, che legge il file in memoria senza conversioni inutili.

```csharp
// Path to your high‑resolution scan (300 DPI or more)
string imagePath = @"YOUR_DIRECTORY/highres_scan.jpg";

// Load the image; ImageStream handles large files efficiently
var image = ImageStream.FromFile(imagePath);
```

> **Suggerimento:** Se la tua immagine è in un bucket cloud, puoi anche fornire direttamente uno `Stream`—basta sostituire `FromFile` con `FromStream(yourStream)`. Il motore la tratterà comunque come sorgente ad alta risoluzione.

## Passo 3: Riconosci il testo dall'immagine  

Ora che il motore è pronto e l'immagine è caricata, possiamo **recognize text from image**. Il metodo `Recognize` restituisce un oggetto `OcrResult` contenente testo semplice, punteggi di confidenza e persino bounding box se ti servono in seguito.

```csharp
// Perform OCR; this call is where the GPU does its magic
OcrResult recognitionResult = ocrEngine.Recognize(image);

// For debugging, you can also inspect recognitionResult.Regions
```

> **Caso limite:** Se l'immagine è troppo scura o ha molto rumore, considera di pre‑processarla (ad es., aumentare il contrasto) prima di chiamare `Recognize`. Aspose offre un'API `Preprocess`, ma per la maggior parte delle scansioni pulite il valore predefinito funziona bene.

## Passo 4: Estrai il testo usando Aspose e visualizzalo  

Infine, **extract text using Aspose** leggendo semplicemente la proprietà `Text` del risultato. Stampiamolo sulla console, ma potresti anche scriverlo su un file o in un database.

```csharp
// Output the plain‑text result
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(recognitionResult.Text);
```

**Output previsto** (esempio per una fattura scansionata):

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,254.00
Thank you for your business!
```

Se vedi caratteri illeggibili, verifica che l'immagine sia davvero ad alta risoluzione e che la lingua corretta sia impostata in `OcrEngineSettings` (ad es., `Language = Language.English`).

## Esempio completo funzionante  

Mettendo tutto insieme, ecco il programma completo che puoi copiare‑incollare in un nuovo progetto console:

```csharp
// ------------------------------------------------------------
// Full OCR example – Aspose OCR with GPU acceleration
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine for GPU
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            ProcessingMode = ProcessingMode.Gpu, // GPU acceleration
            GpuDeviceId = 0                      // Change if you have multiple GPUs
        });

        // 2️⃣ Load a high‑resolution image
        string imagePath = @"YOUR_DIRECTORY/highres_scan.jpg";
        var image = ImageStream.FromFile(imagePath);

        // 3️⃣ Recognize text from the image
        OcrResult result = ocrEngine.Recognize(image);

        // 4️⃣ Extract and display the plain text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(result.Text);
    }
}
```

Esegui il programma con `dotnet run`. Su una GPU decente dovresti vedere il risultato OCR apparire in meno di un secondo, anche per una scansione da 5 MB, 300 DPI.

## Domande comuni e consigli professionali  

### E se non ho una GPU?  
Puoi comunque usare Aspose OCR sulla CPU impostando `ProcessingMode = ProcessingMode.Cpu`. L'API rimane identica; cambia solo le prestazioni.

### Come gestire più lingue?  
Aggiungi `Language = Language.Multilingual` (o un enum specifico come `Language.French`) dentro `OcrEngineSettings`. Aspose caricherà automaticamente i pacchetti linguistici appropriati.

### Posso elaborare PDF direttamente?  
Sì—Aspose OCR può estrarre le immagini dai PDF prima, quindi eseguire OCR su ogni pagina. Combina `Aspose.PDF` con lo stesso `OcrEngine` per una pipeline senza interruzioni.

### Quando dovrei regolare `GpuDeviceId`?  
Se il tuo server esegue sia elaborazione di immagini sia carichi di lavoro di machine learning, potresti dedicare la GPU 1 all'OCR (`GpuDeviceId = 1`) e tenere libera la GPU 0 per le attività di inferenza.

### Come migliorare l'accuratezza su scansioni rumorose?  
Pre‑processa l'immagine:  
```csharp
image = image.AdjustContrast(1.2f).ApplyThreshold(0.5f);
```
Questi metodi fanno parte delle utility di image‑processing di Aspose.

## Conclusione  

Ora sai **how to OCR image** usando Aspose OCR con accelerazione GPU, come **recognize text from image**, il modo corretto per **load high resolution image**, come **set GPU device ID**, e infine come **extract text using Aspose** in un programma C# pulito e pronto per la produzione.  

Prova il codice su diversi file—una ricevuta sfocata, un volantino lucido o anche una nota scritta a mano. Sperimenta con le impostazioni della lingua e i passaggi di pre‑processing per vedere come varia l'accuratezza.  

Successivamente, potresti esplorare **batch processing** (ciclo su una cartella di scansioni) o integrare il risultato OCR in un **search index** per un recupero rapido dei documenti. Entrambi gli argomenti si basano naturalmente sui concetti trattati qui e sono ottimi progetti di follow‑up.

Buona programmazione, e che le tue pipeline OCR siano veloci e impeccabili!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}