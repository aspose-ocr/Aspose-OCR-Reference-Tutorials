---
category: general
date: 2025-12-30
description: Jak włączyć GPU w Aspose OCR do przetwarzania wsadowego OCR i wyodrębniania
  tekstu OCR. Dowiedz się, jak ustawić urządzenie GPU i jak efektywnie korzystać z
  Aspose.
draft: false
keywords:
- how to enable gpu
- batch ocr processing
- ocr text extraction
- set gpu device
- how to use aspose
language: pl
og_description: Jak włączyć GPU w Aspose OCR. Postępuj zgodnie z tym przewodnikiem,
  aby przetwarzać OCR wsadowo, wyodrębniać tekst OCR, ustawić urządzenie GPU i dowiedzieć
  się, jak korzystać z Aspose.
og_title: Jak włączyć GPU dla Aspose OCR – Kompletny samouczek
tags:
- Aspose
- OCR
- GPU
- C#
title: Jak włączyć GPU dla Aspose OCR – przewodnik krok po kroku
url: /pl/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak włączyć GPU dla Aspose OCR – Kompletny poradnik

Zastanawiałeś się kiedyś **jak włączyć GPU** przy użyciu Aspose OCR? Nie jesteś jedyny — programiści przetwarzający ogromne ilości dokumentów często napotykają na problemy wydajnościowe, ponieważ silnik OCR jest zablokowany na CPU. Dobra wiadomość? Włączenie przyspieszenia GPU jest dość proste i może zaoszczędzić sekundy na każdej stronie. W tym przewodniku przejdziemy przez **jak włączyć GPU**, uruchomimy **przetwarzanie OCR wsadowe**, wyodrębnimy rozpoznany tekst i nawet wybierzemy odpowiednie urządzenie GPU. Po zakończeniu będziesz wiedział **jak używać Aspose** do błyskawicznego wyodrębniania tekstu OCR.

## Co obejmuje ten poradnik

Zaczniemy od skonfigurowania biblioteki Aspose OCR, następnie włączymy obsługę GPU, a na końcu uruchomimy wsad obrazów TIFF w silniku. Po drodze wyjaśnimy, dlaczego możesz chcieć **ustawić urządzenie GPU** ręcznie, na jakie pułapki zwrócić uwagę i jak zweryfikować, że wyodrębnianie tekstu rzeczywiście zadziałało. Bez zewnętrznych dokumentacji, tylko kompletny, gotowy do skopiowania i wklejenia kod, który możesz uruchomić już dziś.

> **Wymagania wstępne**  
> - .NET 6.0 lub nowszy (kod używa nowoczesnej składni C#)  
> - Pakiet NuGet Aspose.OCR dla .NET (wersja 23.10 lub nowsza)  
> - GPU kompatybilne z CUDA z odpowiednim sterownikiem zainstalowanym  
> - Folder z kilkoma przykładowymi plikami `.tif` do uruchomienia wsadu  

Jeśli masz już te podstawy, zanurzmy się.

## Jak włączyć GPU w Aspose OCR

Pierwszą rzeczą, którą musisz zrobić, jest poinformowanie `OcrEngine`, aby używał GPU. Odbywa się to poprzez dwie proste właściwości: `UseGpu` oraz opcjonalnie `GpuDeviceId`. Ustawienie `UseGpu` na `true` przełącza silnik w tryb GPU, natomiast `GpuDeviceId` pozwala wybrać, które GPU (jeśli masz ich więcej niż jedno) ma wykonać ciężką pracę.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;
using System.Collections.Generic;

// Step 1: Create the OCR engine and enable GPU acceleration
var ocrEngine = new OcrEngine
{
    // Turn on GPU support – this is the core of “how to enable gpu”
    UseGpu = true,

    // (optional) Choose GPU index 0; change if you have multiple devices
    GpuDeviceId = 0
};
```

> **Dlaczego to ważne** – Wersja CPU przetwarza każdy piksel kolejno, co może stać się wąskim gardłem przy obrazach wysokiej rozdzielczości. Wersja GPU uruchamia tysiące wątków równolegle, dramatycznie skracając czas na stronę.

### Przegląd wizualny  

![Diagram przedstawiający, jak silnik OCR przekazuje pracę do GPU, gdy “how to enable gpu” jest ustawione](/images/enable-gpu-diagram.png){: .center .responsive alt="how to enable gpu"}

*(Jeśli nie widzisz obrazu, wyobraź sobie diagram przepływu, w którym silnik OCR przekazuje bufor obrazu do rdzenia CUDA.)*

## Przetwarzanie OCR wsadowe z Aspose

Teraz, gdy silnik jest gotowy na GPU, podajmy mu listę plików. Przetwarzanie wsadowe jest tak proste, jak iteracja po `List<string>` zawierającej ścieżki do obrazów. Ponieważ używamy GPU, silnik automatycznie umieści każdy obraz w kolejce do urządzenia, utrzymując pipeline zajęty.

```csharp
// Step 2: Define the image files you want to process
var imageFiles = new List<string>
{
    @"C:\OCRSamples\page1.tif",
    @"C:\OCRSamples\page2.tif",
    @"C:\OCRSamples\page3.tif"
};

// Step 3: Process each image and report the character count
foreach (var imagePath in imageFiles)
{
    // Recognize the image – the GPU does the heavy lifting behind the scenes
    var ocrResult = ocrEngine.Recognize(imagePath);

    // Show how many characters were extracted – a quick sanity check
    Console.WriteLine($"{imagePath}: {ocrResult.Text.Length} characters");
}
```

> **Wskazówka** – Dla naprawdę dużych wsadów rozważ użycie `Parallel.ForEach` razem z `ocrEngine.Clone()`, aby uniknąć problemów z bezpieczeństwem wątków. Metoda `Clone` tworzy płytką kopię silnika, która nadal wskazuje na ten sam kontekst GPU.

### Oczekiwany wynik

```
C:\OCRSamples\page1.tif: 1245 characters
C:\OCRSamples\page2.tif: 1130 characters
C:\OCRSamples\page3.tif: 1389 characters
```

Jeśli liczby wyglądają rozsądnie, twoje **przetwarzanie OCR wsadowe** działa i GPU jest wykorzystywane.

## Wyodrębnianie tekstu OCR – uzyskiwanie wyników

Metoda `Recognize` zwraca obiekt `OcrResult`, który zawiera surowy tekst, wyniki pewności oraz nawet ramki ograniczające, jeśli są potrzebne. Wyciągnijmy czysty tekst i zapiszmy go do pliku, abyś mógł zweryfikować wyodrębnianie.

```csharp
foreach (var imagePath in imageFiles)
{
    var ocrResult = ocrEngine.Recognize(imagePath);
    var extractedText = ocrResult.Text;

    // Save the text to a .txt file with the same base name
    var outputPath = System.IO.Path.ChangeExtension(imagePath, ".txt");
    System.IO.File.WriteAllText(outputPath, extractedText);

    Console.WriteLine($"Extracted text saved to {outputPath}");
}
```

> **Dlaczego wyodrębniać do pliku?** – Przechowywanie tekstu OCR umożliwia dalsze przetwarzanie (indeksowanie wyszukiwania, data mining itp.) bez ponownego uruchamiania silnika. Daje także trwały zapis do debugowania.

## Ustawienie urządzenia GPU dla optymalnej wydajności

Jeśli twoja stacja robocza posiada wiele GPU — na przykład dedykowany RTX do ML i zintegrowaną kartę graficzną — będziesz chciał upewnić się, że używasz właściwego. Właściwość `GpuDeviceId` przyjmuje liczbę całkowitą, która odpowiada indeksowi urządzenia zwróconemu przez `CudaDeviceInfo.GetDevices()`.

```csharp
using Aspose.OCR.Gpu;

// List all available GPU devices
var devices = CudaDeviceInfo.GetDevices();
for (int i = 0; i < devices.Length; i++)
{
    Console.WriteLine($"Device {i}: {devices[i].Name} (Compute Capability {devices[i].ComputeCapability})");
}

// Suppose you want to use the second GPU (index 1)
ocrEngine.GpuDeviceId = 1;
Console.WriteLine($"Switched to GPU device {ocrEngine.GpuDeviceId}");
```

> **Przypadek brzegowy** – Niektóre starsze GPU nie obsługują wymaganego wersji CUDA. W takim scenariuszu `UseGpu = true` przełączy się cicho na CPU, więc zawsze sprawdzaj `ocrEngine.IsGpuEnabled` po inicjalizacji.

## Jak używać Aspose OCR w rzeczywistym projekcie

Łącząc wszystko razem, oto kompaktowa, gotowa do uruchomienia aplikacja konsolowa, która demonstruje **jak włączyć GPU**, uruchamia **przetwarzanie OCR wsadowe**, wyodrębnia tekst i pozwala wybrać urządzenie GPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine with GPU support
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true,
            GpuDeviceId = 0 // change if you have multiple GPUs
        };

        // -------------------------------------------------
        // 2️⃣ (Optional) Show available GPU devices
        // -------------------------------------------------
        var devices = CudaDeviceInfo.GetDevices();
        Console.WriteLine("Available GPU devices:");
        for (int i = 0; i < devices.Length; i++)
        {
            Console.WriteLine($"  [{i}] {devices[i].Name} – Compute {devices[i].ComputeCapability}");
        }

        // -------------------------------------------------
        // 3️⃣ Define the batch of images to process
        // -------------------------------------------------
        var imageFiles = new List<string>
        {
            @"C:\OCRSamples\page1.tif",
            @"C:\OCRSamples\page2.tif",
            @"C:\OCRSamples\page3.tif"
        };

        // -------------------------------------------------
        // 4️⃣ Process each image, extract text, and save it
        // -------------------------------------------------
        foreach (var imagePath in imageFiles)
        {
            var result = ocrEngine.Recognize(imagePath);
            var text = result.Text;

            var txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, text);

            Console.WriteLine($"{Path.GetFileName(imagePath)} → {Path.GetFileName(txtPath)} ({text.Length} chars)");
        }

        Console.WriteLine("All done! GPU‑accelerated OCR batch completed.");
    }
}
```

### Uruchamianie przykładu

1. Zainstaluj pakiet NuGet: `dotnet add package Aspose.OCR --version 23.10.0`  
2. Zamień ścieżki w `imageFiles` na lokalizację własnych plików `.tif`.  
3. Zbuduj i uruchom: `dotnet run`.  

Powinieneś zobaczyć listę GPU, a następnie linię dla każdego obrazu z liczbą znaków i ścieżką do wygenerowanego pliku `.txt`.

## Częste pytania i pułapki

- **Czy to działa na maszynie tylko z CPU?**  
  Tak — jeśli `UseGpu` jest `true`, ale nie zostanie znalezione kompatybilne GPU, Aspose przełącza się na CPU. Możesz zweryfikować tryb poprzez `ocrEngine.IsGpuEnabled`.

- **Co zrobić, gdy pojawi się błąd „CUDA driver version is insufficient”?**  
  Zaktualizuj sterownik NVIDIA do najnowszej wersji, która pasuje do zestawu narzędzi CUDA dołączonego do Aspose. Biblioteka wymaga co najmniej CUDA 11.0 dla najnowszych funkcji GPU.

- **Czy mogę przetwarzać PDF-y bezpośrednio?**  
  Aspose OCR działa na obrazach rastrowych. Najpierw skonwertuj strony PDF do obrazów (np. przy użyciu Aspose.PDF), a następnie podaj je silnikowi OCR.

- **Jak poprawić dokładność przy szumnych skanach?**  
  Włącz opcje przetwarzania wstępnego, takie jak `ocrEngine.Preprocess = true`, lub podawaj obrazy o wyższej rozdzielczości (300 dpi lub więcej). Przyspieszenie GPU nadal obowiązuje.

## Podsumowanie

Omówiliśmy **jak włączyć GPU** dla Aspose OCR, przeszliśmy przez **przetwarzanie OCR wsadowe**, zademonstrowaliśmy **wyodrębnianie tekstu OCR** i pokazaliśmy, jak **ustawić urządzenie GPU** dla optymalnej wydajności. Postępując zgodnie z kompletnym przykładem kodu, możesz teraz zintegrować szybkie, oparte na GPU OCR w dowolnym projekcie .NET i pewnie odpowiedzieć na wieczne pytanie „jak używać Aspose”.

Gotowy na kolejny krok? Spróbuj dodać wykrywanie języka, przekazać wyodrębniony tekst do indeksu wyszukiwania lub eksperymentować ze skalowaniem wielogpu dla ogromnych archiwów dokumentów. Nie ma granic, gdy połączysz solidne API Aspose z surową mocą współczesnych GPU.

Szczęśliwego kodowania i niech twoje zadania OCR działają tak szybko, jak pozwala na to twoje GPU!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}