---
category: general
date: 2026-03-13
description: Samouczek na żywo OCR pokazuje, jak ustawić język OCR i wykrywać tekst
  w strumieniach wideo w czasie rzeczywistym przy użyciu Aspose.OCR. Postępuj zgodnie
  z przewodnikiem krok po kroku.
draft: false
keywords:
- live ocr tutorial
- set OCR language
- detect text video
- Aspose OCR live processing
- real‑time text detection
language: pl
og_description: Samouczek Live OCR wyjaśnia, jak ustawić język OCR i wykrywać tekst
  w strumieniach wideo przy użyciu Aspose.OCR Live w C#. Pełny kod w zestawie.
og_title: 'Samouczek OCR na żywo: Wykrywanie tekstu w czasie rzeczywistym w wideo'
tags:
- OCR
- C#
- Aspose
- Video Processing
title: 'Samouczek OCR na żywo: wykrywanie tekstu w wideo w C#'
url: /pl/net/text-recognition/live-ocr-tutorial-detect-text-in-video-with-c/
---

table format.

Translate "Question" to "Pytanie", "Answer" to "Odpowiedź". Then translate each question and answer.

Also translate bullet list items.

Make sure to keep code block placeholders unchanged.

Also keep the "TL;DR" heading.

Let's produce.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Live OCR Tutorial: Detect Text in Video with C#

Czy kiedykolwiek potrzebowałeś **samouczka live OCR**, który naprawdę działa na strumieniu wideo? Być może tworzysz aplikację smart‑camera lub nakładkę tłumaczenia w czasie rzeczywistym i utknąłeś przy pytaniu „jak pobrać tekst z każdej klatki?”. Dobra wiadomość – nie musisz wymyślać koła od nowa. W tym przewodniku przejdziemy przez kompletny, gotowy do uruchomienia przykład, który **ustawia język OCR**, pobiera klatki z kamery i **wykrywa tekst w strumieniu wideo** w locie.

Użyjemy klasy `LiveOcr` z Aspose.OCR, stworzonej z myślą o scenariuszach o niskiej latencji. Po przeczytaniu tego artykułu będziesz mieć aplikację konsolową, która wypisze pierwszy wykryty fragment tekstu i zakończy działanie – idealny punkt wyjścia do bardziej zaawansowanych potoków.

## Prerequisites

- .NET 6.0 SDK (lub dowolna nowsza wersja .NET)  
- Visual Studio 2022 lub VS Code (ulubione IDE)  
- Pakiet NuGet `Aspose.OCR` (instalacja przez `dotnet add package Aspose.OCR`)  
- Kamera internetowa lub dowolne źródło wideo, które może dostarczyć klatki `Bitmap`  

Nie są wymagane dodatkowe biblioteki natywne; Aspose.OCR zawiera wszystko, czego potrzebujesz.

## Step 1: Install Aspose.OCR and Add Namespaces

Zanim napiszesz jakikolwiek kod, upewnij się, że biblioteka Aspose OCR jest dodana jako odwołanie. Otwórz terminal w folderze projektu i uruchom:

```bash
dotnet add package Aspose.OCR
```

Następnie, na początku pliku `Program.cs`, zaimportuj przestrzenie nazw, których będziemy używać:

```csharp
using Aspose.OCR;
using Aspose.OCR.Live;
using System.Drawing;
using System.Threading;
```

> **Pro tip:** Jeśli używasz Visual Studio, IDE automatycznie zasugeruje instrukcje `using` po wpisaniu nazw klas.

## Step 2: Create and Configure the LiveOcr Instance

Serce tego samouczka to obiekt `LiveOcr`. Musimy powiedzieć mu, w jakim języku ma szukać tekstu i opcjonalnie zastosować filtry wstępnego przetwarzania (np. prostowanie), aby zwiększyć dokładność.

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

Dlaczego ustawiamy język? Silniki OCR korzystają ze słowników i modeli znaków specyficznych dla języka; podanie angielskiego zmniejsza liczbę fałszywych trafień i przyspiesza rozpoznawanie. Jeśli potrzebujesz innego języka, zamień `Language.English` na `Language.Spanish`, `Language.French` itp.

## Step 3: Capture Frames from Your Camera

W prawdziwym projekcie zamienisz metodę zastępczą `CaptureFrameFromCamera()` na rzeczywistą logikę przechwytywania – być może przy użyciu `AForge.Video`, `OpenCvSharp` lub Windows Media Capture API. Dla potrzeb tego samouczka pozostawimy metodę abstrakcyjną, ale pokażemy szybki przykład z użyciem `AForge`.

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

> **Edge case:** Jeśli kamera nie jest dostępna, `CaptureFrameFromCamera` zwróci `null`. Zawsze zabezpiecz się przed tym w kodzie produkcyjnym.

## Step 4: Process Each Frame Until Text Is Found

Teraz iterujemy po określonej liczbie klatek (lub w nieskończoność) i przekazujemy każdy `Bitmap` do `LiveOcr.ProcessFrame`. Gdy otrzymamy niepusty ciąg znaków, wypisujemy go i przerywamy pętlę.

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

### Why a pause?

`Thread.Sleep(30)` daje sterownikowi kamery chwilę oddechu i zmniejsza zużycie CPU. W scenariuszach wysokiej wydajności możesz zastąpić to bardziej zaawansowanym kontrolerem liczby klatek na sekundę.

## Step 5: Wrap Everything in a Console Application

Łącząc wszystkie elementy, oto kompletny program gotowy do skopiowania i wklejenia. Zapisz go jako `Program.cs` w nowym projekcie konsolowym (`dotnet new console`) i uruchom `dotnet run`.

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

### Expected output

Gdy kamera zobaczy czytelny angielski tekst (np. wydrukowaną etykietę), zobaczysz coś w stylu:

```
Starting live OCR… Press Ctrl+C to abort.
Detected text: OpenAI
Live OCR session ended.
```

Jeśli nic nie będzie w polu widzenia, pętla zakończy się po 100 iteracjach i wypisze „Live OCR session ended.”. Możesz zwiększyć liczbę iteracji lub zamienić pętlę `for` na `while (true)`, aby monitorować nieprzerwanie.

## Common Questions & Gotchas

| Pytanie | Odpowiedź |
|----------|-----------|
| **Czy mogę przetwarzać wiele języków jednocześnie?** | Tak. Ustaw `Language = Language.English | Language.Spanish;` (operacja bitowa OR), aby włączyć słownik wielojęzyczny. |
| **Co zrobić, gdy moje klatki są duże i OCR działa wolno?** | Zmniejsz rozmiar bitmapy przed wywołaniem `ProcessFrame`. Przykład: `Bitmap small = new Bitmap(frame, new Size(320, 240));` |
| **Czy potrzebna jest licencja na Aspose.OCR?** | Tymczasowa licencja ewaluacyjna działa przez maksymalnie 30 dni. Do produkcji zakup licencję, aby usunąć znak wodny. |
| **Jak radzić sobie z obróconym tekstem?** | Filtr `DeskewFilter` koryguje niewielkie rotacje. W przypadku skrajnych kątów dodaj `RotateFilter` do potoku. |
| **Czy to podejście jest bezpieczne wątkowo?** | Instancje `LiveOcr` nie są thread‑safe. Utwórz jedną na każdy wątek lub zabezpiecz dostęp przy pomocy locka. |

## Extending the Tutorial

Teraz, gdy masz **podstawy live OCR**, rozważ następujące kroki:

1. **Strumieniowanie do UI** – wyświetlaj wideo na żywo z nałożonymi wynikami OCR przy użyciu `Windows Forms` lub `WPF`.  
2. **Przetwarzanie wsadowe** – kieruj klatki do kolejki i uruchamiaj OCR w tle na puli pracowników, aby zwiększyć przepustowość.  
3. **Wykrywanie języka** – zintegrować bibliotekę identyfikacji języka, aby dynamicznie przełączać `LiveOcr.Language`.  
4. **Trwałe zapisywanie wyników** – zapisuj wykryte ciągi do bazy danych lub pliku CSV w celach analitycznych.  

Każde z tych rozszerzeń opiera się na podstawowych koncepcjach, które omówiliśmy: inicjalizacja `LiveOcr`, **ustawianie języka OCR** oraz **wykrywanie tekstu w klatkach wideo** w czasie rzeczywistym.

---

### TL;DR

- Zainstaluj Aspose.OCR przez NuGet.  
- Utwórz obiekt `LiveOcr`, **ustaw język OCR** (w przykładzie angielski).  
- Przechwytuj klatki `Bitmap` z kamery.  
- Iteruj po klatkach, wywołuj `ProcessFrame` i zatrzymaj się, gdy pojawi się tekst.  
- Pełny program powyżej jest gotowy do uruchomienia i stanowi solidną bazę dla każdego projektu wykrywania tekstu w czasie rzeczywistym.

Spróbuj, dostosuj potok wstępnego przetwarzania i zobacz, jak Twoja aplikacja zaczyna czytać świat klatka po klatce. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}