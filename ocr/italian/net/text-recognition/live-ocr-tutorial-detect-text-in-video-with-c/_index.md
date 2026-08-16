---
category: general
date: 2026-03-13
description: Il tutorial live di OCR mostra come impostare la lingua OCR e rilevare
  i flussi video di testo in tempo reale usando Aspose.OCR. Segui la guida passo passo.
draft: false
keywords:
- live ocr tutorial
- set OCR language
- detect text video
- Aspose OCR live processing
- real‑time text detection
language: it
og_description: Il tutorial Live OCR spiega come impostare la lingua OCR e rilevare
  i flussi video di testo usando Aspose.OCR Live in C#. Codice completo incluso.
og_title: 'Tutorial OCR in diretta: Rilevamento del testo in tempo reale nei video'
tags:
- OCR
- C#
- Aspose
- Video Processing
title: 'Tutorial OCR in tempo reale: Rileva il testo nel video con C#'
url: /it/net/text-recognition/live-ocr-tutorial-detect-text-in-video-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial OCR in tempo reale: Rileva il testo in video con C#

Hai mai avuto bisogno di un **tutorial OCR in tempo reale** che funzioni davvero su un flusso video? Forse stai creando un'app per fotocamere intelligenti o una sovrapposizione di traduzione in tempo reale e sei bloccato su “come estrarre il testo da ogni fotogramma?”. La buona notizia è che non devi reinventare la ruota. In questa guida percorreremo un esempio completo e eseguibile che **imposta la lingua OCR**, acquisisce fotogrammi da una fotocamera e **rileva il testo nei video** al volo.

Useremo la classe `LiveOcr` di Aspose.OCR, progettata appositamente per scenari a bassa latenza. Alla fine di questo articolo avrai un'app console che stampa il primo pezzo di testo che vede e poi termina—perfetta come punto di partenza per pipeline più sofisticate.

## Prerequisiti

- .NET 6.0 SDK (o qualsiasi versione recente di .NET)  
- Visual Studio 2022 o VS Code (il tuo IDE preferito)  
- Pacchetto NuGet `Aspose.OCR` (installa tramite `dotnet add package Aspose.OCR`)  
- Una webcam o qualsiasi sorgente video che possa fornire fotogrammi `Bitmap`  

Non sono richieste librerie native aggiuntive; Aspose.OCR include tutto il necessario.

## Passo 1: Installa Aspose.OCR e aggiungi i namespace

Prima di scrivere qualsiasi codice, assicurati che la libreria Aspose OCR sia referenziata. Apri un terminale nella cartella del tuo progetto ed esegui:

```bash
dotnet add package Aspose.OCR
```

Quindi, nella parte superiore del tuo `Program.cs`, importa i namespace che utilizzeremo:

```csharp
using Aspose.OCR;
using Aspose.OCR.Live;
using System.Drawing;
using System.Threading;
```

> **Suggerimento professionale:** Se usi Visual Studio, l'IDE suggerirà automaticamente le istruzioni `using` dopo aver digitato i nomi delle classi.

## Passo 2: Crea e configura l'istanza LiveOcr

Il cuore del tutorial è l'oggetto `LiveOcr`. Dobbiamo indicargli quale lingua cercare e, facoltativamente, applicare filtri di pre‑elaborazione (come il deskew) per migliorare l'accuratezza.

```csharp
// Step 2: Initialize LiveOcr with English language and a deskew filter
LiveOcr liveOcr = new LiveOcr
{
    // This is where we **set OCR language** to English.
    Language = Language.English,

    // Pre‑processing helps when the camera isn’t perfectly aligned.
    PreProcessingFilters = new FilterPipeline { new DeskewFilter() }
};
```

Perché impostare la lingua? I motori OCR utilizzano dizionari e modelli di caratteri specifici per lingua; specificare l'inglese riduce i falsi positivi e velocizza il riconoscimento. Se ti serve un'altra lingua, basta sostituire `Language.English` con `Language.Spanish`, `Language.French`, ecc.

## Passo 3: Acquisisci i fotogrammi dalla tua fotocamera

In un progetto reale sostituiresti il metodo segnaposto `CaptureFrameFromCamera()` con una logica di acquisizione effettiva—magari usando `AForge.Video`, `OpenCvSharp` o l'API Windows Media Capture. Per il tutorial manterremo il metodo astratto, ma mostreremo un rapido esempio usando `AForge`.

```csharp
// Simple wrapper that returns a Bitmap from the default webcam.
// You can replace this with any library that gives you a Bitmap.
static Bitmap CaptureFrameFromCamera()
{
    // NOTE: This is a minimal example. In production you should
    // manage the video source lifecycle and dispose objects properly.
    var videoSource = new AForge.Video.DirectShow.VideoCaptureDevice(
        new AForge.Video.DirectShow.FilterInfoCollection(
            AForge.Video.DirectShow.FilterCategory.VideoInputDevice)[0].MonikerString);

    Bitmap frame = null;
    var waitHandle = new AutoResetEvent(false);

    videoSource.NewFrame += (sender, eventArgs) =>
    {
        frame = (Bitmap)eventArgs.Frame.Clone();
        waitHandle.Set(); // signal that we have a frame
    };

    videoSource.Start();
    waitHandle.WaitOne(1000); // wait up to 1 second for a frame
    videoSource.SignalToStop();
    videoSource.WaitForStop();

    return frame;
}
```

> **Caso limite:** Se la fotocamera non è disponibile, `CaptureFrameFromCamera` restituirà `null`. Assicurati sempre di gestire questo caso nel codice di produzione.

## Passo 4: Elabora ogni fotogramma finché non trovi del testo

Ora iteriamo su un numero fisso di fotogrammi (o indefinitamente) e inviamo ogni bitmap a `LiveOcr.ProcessFrame`. Non appena otteniamo una stringa non vuota, la stampiamo e usciamo dal ciclo.

```csharp
// Step 4: Scan up to 100 frames or until text appears
for (int frameIndex = 0; frameIndex < 100; frameIndex++)
{
    Bitmap cameraFrame = CaptureFrameFromCamera();

    // Guard against a failed capture
    if (cameraFrame == null)
    {
        Console.WriteLine("Failed to capture a frame. Retrying...");
        Thread.Sleep(100);
        continue;
    }

    // Run OCR on the current frame
    string recognizedText = liveOcr.ProcessFrame(cameraFrame);

    // If we detected something, show it and stop
    if (!string.IsNullOrEmpty(recognizedText))
    {
        Console.WriteLine($"Detected text: {recognizedText}");
        break;
    }

    // Small pause to avoid hammering the CPU
    Thread.Sleep(30);
}
```

### Perché una pausa?

`Thread.Sleep(30)` concede una pausa al driver della fotocamera e riduce l'uso della CPU. In scenari ad alte prestazioni potresti sostituirlo con un controller di frequenza dei fotogrammi più sofisticato.

## Passo 5: Raggruppa tutto in un'applicazione console

Mettendo tutto insieme, ecco il programma completo, pronto per il copia‑incolla. Salvalo come `Program.cs` all'interno di un nuovo progetto console (`dotnet new console`) ed esegui `dotnet run`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Live;
using System;
using System.Drawing;
using System.Threading;

// Optional: using AForge for demo capture (install AForge.Video via NuGet)
// using AForge.Video.DirectShow;

class Program
{
    static void Main()
    {
        // Initialize LiveOcr – **set OCR language** to English
        LiveOcr liveOcr = new LiveOcr
        {
            Language = Language.English,
            PreProcessingFilters = new FilterPipeline { new DeskewFilter() }
        };

        Console.WriteLine("Starting live OCR… Press Ctrl+C to abort.");

        // Loop through frames – **detect text video** in real time
        for (int i = 0; i < 100; i++)
        {
            Bitmap frame = CaptureFrameFromCamera();

            if (frame == null)
            {
                Console.WriteLine("No frame captured, retrying...");
                Thread.Sleep(100);
                continue;
            }

            string text = liveOcr.ProcessFrame(frame);

            if (!string.IsNullOrEmpty(text))
            {
                Console.WriteLine($"Detected text: {text}");
                break; // stop after first successful detection
            }

            Thread.Sleep(30); // throttle loop
        }

        Console.WriteLine("Live OCR session ended.");
    }

    // -----------------------------------------------------------------
    // Replace this stub with your own capture logic.
    // -----------------------------------------------------------------
    static Bitmap CaptureFrameFromCamera()
    {
        // Placeholder implementation – returns a solid‑color bitmap.
        // In a real app you would pull frames from a webcam or video file.
        Bitmap dummy = new Bitmap(640, 480);
        using (Graphics g = Graphics.FromImage(dummy))
        {
            g.Clear(Color.Black);
            g.DrawString(DateTime.Now.ToString("hh:mm:ss"), 
                new Font("Arial", 24), Brushes.White, new PointF(10, 10));
        }
        return dummy;
    }
}
```

### Output previsto

Quando la fotocamera rileva testo inglese leggibile (ad esempio un'etichetta stampata), vedrai qualcosa del genere:

```
Starting live OCR… Press Ctrl+C to abort.
Detected text: OpenAI
Live OCR session ended.
```

Se non c'è nulla in vista, il ciclo terminerà dopo 100 iterazioni e stamperà “Live OCR session ended.” Puoi aumentare il conteggio delle iterazioni o sostituire il ciclo `for` con un `while (true)` per un monitoraggio continuo.

## Domande comuni e insidie

| Domanda | Risposta |
|----------|--------|
| **Posso elaborare più lingue simultaneamente?** | Sì. Imposta `Language = Language.English | Language.Spanish;` (OR bitwise) per abilitare un dizionario multilingue. |
| **Cosa succede se i miei fotogrammi sono grandi e l'OCR è lento?** | Ridimensiona il bitmap prima di chiamare `ProcessFrame`. Esempio: `Bitmap small = new Bitmap(frame, new Size(320, 240));` |
| **Ho bisogno di una licenza per Aspose.OCR?** | Una licenza di valutazione temporanea funziona fino a 30 giorni. Per la produzione, acquista una licenza per rimuovere la filigrana. |
| **Come gestisco il testo ruotato?** | Il `DeskewFilter` corregge già le rotazioni minori. Per angoli estremi, aggiungi un `RotateFilter` al pipeline. |
| **Questo approccio è thread‑safe?** | Le istanze `LiveOcr` non sono thread‑safe. Creane una per thread o proteggi l'accesso con un lock. |

## Estendere il tutorial

Ora che hai una base di **tutorial OCR in tempo reale**, considera i seguenti passi successivi:

1. **Trasmetti a un'interfaccia UI** – visualizza il video in tempo reale con i risultati OCR sovrapposti usando `Windows Forms` o `WPF`.  
2. **Elaborazione batch** – invia i fotogrammi in una coda ed esegui l'OCR su un pool di worker in background per maggiore throughput.  
3. **Rilevamento della lingua** – integra una libreria di identificazione della lingua per cambiare `LiveOcr.Language` al volo.  
4. **Persisti i risultati** – scrivi le stringhe rilevate in un database o in un file CSV per analisi.  

Ognuna di queste estensioni si basa ancora sui concetti fondamentali trattati: inizializzare `LiveOcr`, **impostare la lingua OCR**, e **rilevare i fotogrammi video di testo** in tempo reale.

### TL;DR

- Installa Aspose.OCR tramite NuGet.  
- Crea un oggetto `LiveOcr`, **imposta la lingua OCR** (inglese nell'esempio).  
- Acquisisci fotogrammi `Bitmap` da una fotocamera.  
- Itera sui fotogrammi, chiama `ProcessFrame` e interrompi quando appare del testo.  
- Il programma completo sopra è pronto per l'esecuzione e costituisce una solida base per qualsiasi progetto di rilevamento del testo in tempo reale.

Provalo, modifica la pipeline di pre‑elaborazione e guarda la tua app iniziare a leggere il mondo fotogramma per fotogramma. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}