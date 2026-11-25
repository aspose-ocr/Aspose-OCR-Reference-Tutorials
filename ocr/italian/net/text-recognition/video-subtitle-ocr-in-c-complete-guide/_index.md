---
category: general
date: 2026-06-03
description: Tutorial OCR per sottotitoli video che mostra come estrarre fotogrammi
  dal video e leggere il testo da file video come MP4 utilizzando Aspose.OCR.
draft: false
keywords:
- video subtitle ocr
- extract frames from video
- read text from video
- extract text from mp4
language: it
og_description: Impara l'OCR dei sottotitoli video con Aspose.OCR. Estrai i fotogrammi
  dal video, leggi il testo dal video e estrai il testo da MP4 in pochi minuti.
og_title: OCR dei sottotitoli video in C# – Guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  headline: Video Subtitle OCR in C# – Complete Guide
  type: TechArticle
- description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  name: Video Subtitle OCR in C# – Complete Guide
  steps:
  - name: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
    text: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
  - name: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
    text: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
  - name: Processes each frame with Aspose’s `VideoOcrProcessor`.
    text: Processes each frame with Aspose’s `VideoOcrProcessor`.
  - name: Prints the recognized subtitle text to the console.
    text: Prints the recognized subtitle text to the console.
  type: HowTo
tags:
- C#
- Aspose.OCR
- video-processing
title: OCR dei sottotitoli video in C# – Guida completa
url: /it/net/text-recognition/video-subtitle-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR dei sottotitoli video in C# – Guida completa

Hai mai avuto bisogno di **video subtitle ocr** ma non sapevi da dove cominciare? Non sei solo. Che tu stia digitalizzando registrazioni di lezioni, estraendo i sottotitoli da video di formazione, o semplicemente sia curioso di leggere il testo da un video, questo tutorial ti mostra esattamente come farlo con C# e Aspose.OCR.  

Nei prossimi minuti estrarremo i fotogrammi dal video, eseguiremo l'OCR su quei fotogrammi e infine visualizzeremo il testo dei sottotitoli fotogramma‑per‑fotogramma. Alla fine sarai in grado di **leggere il testo da file video**—inclusi MP4—senza dover cercare strumenti di terze parti.

## Cosa costruiremo

Creeremo una piccola applicazione console che:

1. Decodifica un MP4 (o qualsiasi formato supportato) in singoli fotogrammi `Bitmap`.  
2. Limita la regione OCR alla banda dei sottotitoli così il motore non è distratto dall’intera immagine.  
3. Elabora ogni fotogramma con `VideoOcrProcessor` di Aspose.  
4. Stampa il testo dei sottotitoli riconosciuto sulla console.

Niente fronzoli, solo un esempio end‑to‑end funzionante che puoi inserire in un progetto reale.

## Prerequisiti

- **.NET 6.0** o successivo (il codice funziona anche su .NET Framework 4.7+).  
- **Aspose.OCR for .NET** – installa via NuGet: `Install-Package Aspose.OCR`.  
- Un file video (MP4 funziona benissimo).  
- Un modo per decodificare i fotogrammi video – la demo usa un metodo placeholder, ma puoi collegare FFmpeg, OpenCV o qualsiasi libreria che restituisca oggetti `Bitmap`.  

> Pro tip: Se sei su Windows, il pacchetto `System.Drawing.Common` funziona bene per `Bitmap`. Su Linux/macOS avrai bisogno della dipendenza nativa `libgdiplus`.

## Passo 1 – Estrarre i fotogrammi dal video

Il primo ostacolo è trasformare un’immagine in movimento in immagini statiche. Il metodo `GetVideoFrames` qui sotto è lasciato intenzionalmente vuoto; sostituiscilo con il decoder che preferisci. Ecco uno schizzo rapido usando FFmpeg‑Core (solo per illustrare la forma dei dati):

```csharp
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

/// <summary>
/// Extracts every frame from the supplied video file and yields it as a Bitmap.
/// You can swap this implementation for OpenCV, MediaToolkit, etc.
/// </summary>
static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
{
    // Create a temporary folder for the extracted PNGs
    string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
    Directory.CreateDirectory(tempDir);

    // FFmpeg command: -i input -vf fps=1 output_%04d.png (1 fps for demo)
    var startInfo = new ProcessStartInfo
    {
        FileName = "ffmpeg",
        Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
        RedirectStandardOutput = true,
        UseShellExecute = false,
        CreateNoWindow = true
    };
    Process ffmpeg = Process.Start(startInfo);
    ffmpeg.WaitForExit();

    foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
    {
        using var bmp = new Bitmap(file);
        // Clone the bitmap so the file can be deleted later
        yield return new Bitmap(bmp);
    }

    // Clean up
    Directory.Delete(tempDir, true);
}
```

> **Perché è importante:** Estrarre i fotogrammi fornisce al motore OCR un’immagine statica su cui lavorare, migliorando drasticamente l’accuratezza rispetto al tentativo di leggere direttamente dallo stream video.

## Passo 2 – Configurare il VideoOcrProcessor

Ora che abbiamo una sequenza di oggetti `Bitmap`, possiamo passarli ad Aspose.OCR. Il `VideoOcrProcessor` ci permette di definire una **Region of Interest (ROI)** – perfetta per i sottotitoli che di solito si trovano in alto o in basso al fotogramma.

```csharp
using Aspose.OCR.Video;
using System.Drawing;

// Create the processor and focus on the top 200 pixels (typical subtitle band)
var ocrProcessor = new VideoOcrProcessor
{
    // ROI = new Rectangle(x, y, width, height)
    Roi = new Rectangle(0, 0, 1920, 200)   // adjust width/height to your video resolution
};
```

> **Perché limitare la ROI?** Ignorando il resto dell’immagine riduciamo il rumore, diminuiamo i tempi di elaborazione e evitiamo falsi positivi da grafiche di sfondo.

## Passo 3 – Eseguire l'OCR sulla sequenza di fotogrammi

Con il processore pronto, alimentare i fotogrammi è una singola riga di codice. Il metodo `Process` restituisce un enumerable di oggetti `OcrResult`, ognuno contenente il testo riconosciuto per il relativo fotogramma.

```csharp
IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

// Execute OCR on every extracted frame
IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);
```

> **Cosa succede dietro le quinte?** Aspose.OCR normalizza internamente ogni bitmap, esegue un riconoscitore basato su rete neurale e poi post‑processa l’output per migliorare punteggiatura e interruzioni di riga.

## Passo 4 – Visualizzare il testo estratto

Infine, iteriamo sui risultati e stampiamo ogni riga di sottotitolo. Potresti anche scriverle in un file SRT, in un database, o inviarle a un servizio di traduzione.

```csharp
int frameIndex = 0;
foreach (var result in ocrResults)
{
    // result.Text contains the plain‑text subtitle for this frame
    Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
}
```

### Esempio completo funzionante

Mettendo tutto insieme otteniamo un programma console autonomo:

```csharp
using Aspose.OCR.Video;
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

class VideoSubtitleOcrDemo
{
    static void Main()
    {
        // 1️⃣ Extract frames from the MP4 (replace with your own decoder)
        IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

        // 2️⃣ Configure OCR – focus on the subtitle band
        var ocrProcessor = new VideoOcrProcessor
        {
            Roi = new Rectangle(0, 0, 1920, 200) // tweak for your video size
        };

        // 3️⃣ Run OCR across all frames
        IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);

        // 4️⃣ Output the recognized subtitle text
        int frameIndex = 0;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
        }
    }

    // --------------------------------------------------------------------
    // Helper: extract one‑frame‑per‑second PNGs using FFmpeg.
    // Replace this with any library that can return Bitmap objects.
    // --------------------------------------------------------------------
    static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
    {
        string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
        Directory.CreateDirectory(tempDir);

        var startInfo = new ProcessStartInfo
        {
            FileName = "ffmpeg",
            Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
            RedirectStandardOutput = true,
            UseShellExecute = false,
            CreateNoWindow = true
        };
        using var ffmpeg = Process.Start(startInfo);
        ffmpeg.WaitForExit();

        foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
        {
            using var bmp = new Bitmap(file);
            yield return new Bitmap(bmp);
        }

        Directory.Delete(tempDir, true);
    }
}
```

**Output previsto (esempio)**  

```
Frame 0: Welcome to the Introduction to Machine Learning.
Frame 1: In this lecture we will cover...
Frame 2: ...
```

Se l'OCR fatica con un fotogramma particolare, vedrai una stringa vuota – è un segnale per regolare la ROI o aumentare la frequenza di estrazione dei fotogrammi.

## Problemi comuni e come risolverli

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| **Caratteri spazzatura** | Fotogrammi a bassa risoluzione o compressione elevata | Estrarre i fotogrammi a bitrate più alto, o ingrandire il bitmap prima dell'OCR (`Bitmap.Clone(new Size(...), ...)`). |
| **Nessun testo restituito** | La ROI non copre effettivamente la banda dei sottotitoli | Verificare le coordinate del rettangolo (usa uno strumento di screenshot per misurare). |
| **Collo di bottiglia delle prestazioni** | Elaborare ogni fotogramma a 30 fps è eccessivo | Sottocampionare a 1‑2 fps per la maggior parte dei flussi di sottotitoli; puoi comunque catturare ogni cambiamento di sottotitolo. |
| **FFmpeg non trovato** | `ffmpeg.exe` non è nel `PATH` | Specificare il percorso completo in `ProcessStartInfo.FileName` o installare FFmpeg globalmente. |

## Estendere la soluzione

- **Esportare in SRT** – concatenare i timestamp con il testo OCR e scrivere un file SubRip.  
- **Supporto multilingua** – impostare `ocrProcessor.Language = OcrLanguage.Spanish` (o qualsiasi lingua supportata).  
- **Elaborazione in tempo reale** – inviare i fotogrammi direttamente da uno stream live invece di leggerli da disco.  

Tutte queste varianti ruotano ancora attorno alle idee chiave di **estrarre fotogrammi dal video**, **leggere testo dal video** e **estrarre testo da mp4**.

## Conclusione

Abbiamo appena percorso un flusso di lavoro completo di **video subtitle ocr** in C#. Estrarre i fotogrammi dal video, concentrare l'OCR sulla banda dei sottotitoli e iterare sui risultati ti permette di leggere in modo affidabile **testo da file video** come MP4. Il codice è pronto per il copia‑incolla, e il design modulare ti consente di sostituire qualsiasi decoder di fotogrammi tu preferisca.

Passi successivi? Prova a esportare i risultati in un file SRT, sperimenta con diverse dimensioni della ROI, o invia i sottotitoli a un’API di traduzione per didascalie multilingue. Il cielo è il limite una volta che hai padroneggiato le basi dell’estrazione di testo da video.

Buon coding, e che i tuoi sottotitoli siano sempre cristallini!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell’API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai testo da immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Estrai testo da immagine usando Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Estrai testo da immagine – Ottimizzazione OCR con Aspose.OCR per .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}