---
category: general
date: 2026-04-26
description: Szybko wyodrębnij tekst z plików PNG przy użyciu C#. Dowiedz się, jak
  konwertować obrazy na tekst, odczytywać pliki PNG, iterować po obrazach i przetwarzać
  obrazy OCR w partiach w ciągu kilku minut.
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: pl
og_description: Szybko wyodrębnij tekst z plików PNG przy użyciu C#. Ten przewodnik
  pokazuje, jak konwertować obrazy na tekst, odczytywać pliki PNG, iterować po obrazach
  i przetwarzać obrazy metodą OCR w partiach.
og_title: Wyodrębnij tekst z PNG – Kompletny samouczek OCR wsadowego w C#
tags:
- C#
- OCR
- Aspose
title: Wyodrębnij tekst z PNG – Kompletny samouczek OCR wsadowego w C#
url: /pl/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tekstu z PNG – Kompletny samouczek C# Batch OCR

Czy kiedykolwiek potrzebowałeś **wyodrębnić tekst z plików PNG**, ale nie wiedziałeś od czego zacząć? Nie jesteś sam — wielu programistów napotyka tę przeszkodę, gdy po raz pierwszy próbują OCR na folderze zrzutów ekranu. Dobrą wiadomością jest to, że kilka linijek C# i Aspose OCR pozwala konwertować obrazy na tekst, odczytywać pliki PNG, iterować po obrazach i przetwarzać wszystko w trybie wsadowym.

W tym samouczku przeprowadzimy Cię przez gotową do uruchomienia aplikację konsolową, która robi dokładnie to. Po zakończeniu będziesz mieć samodzielne rozwiązanie, które wyciąga tekst z każdego PNG w katalogu i zapisuje pasujący plik `.txt` obok każdego obrazu. Bez dodatkowych skryptów, bez ręcznego kopiowania‑wklejania — po prostu czysty kod.

## Czego będziesz potrzebować

- **.NET 6 SDK** (lub dowolna nowsza wersja .NET). Jest darmowy, szybki i działa wszędzie.
- **Aspose.OCR for .NET** (pakiet NuGet). Biblioteka zawiera przyspieszenie GPU, jeśli posiadasz kompatybilną kartę graficzną, ale automatycznie przełącza się na CPU.
- Folder z kilkoma **obrazami PNG**, które chcesz przetworzyć.  
- Edytor tekstu lub IDE — Visual Studio, VS Code, Rider — cokolwiek wolisz.

To wszystko. Jeśli już masz te elementy, możesz zaczynać.

![przykład wyodrębniania tekstu z png](image.png "zrzut ekranu demonstracji wyodrębniania tekstu z png")

*Tekst alternatywny obrazu: “wyodrębnianie tekstu z png przy użyciu C# batch OCR”*

## Krok 1 – Konfiguracja projektu i instalacja Aspose.OCR

Najpierw utwórz nowy projekt konsolowy i dodaj pakiet Aspose OCR.

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

Dlaczego używamy aplikacji konsolowej? To najprostszy host dla zadań wsadowych i możesz ją uruchamiać z wiersza poleceń lub planować za pomocą harmonogramu zadań. Jeśli później będziesz potrzebować interfejsu UI, możesz po prostu przenieść logikę do biblioteki klas.

## Krok 2 – Inicjalizacja silnika OCR przyspieszanego GPU (lub awaryjny CPU)

Aspose oferuje `GpuOcrEngine`, który automatycznie wykrywa obsługiwane GPU. Jeśli nie zostanie znalezione, przełącza się na standardowy silnik CPU — bez dodatkowego kodu.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine – GPU if available, otherwise CPU
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;   // Latin covers most Western alphabets

        // The rest of the code lives in a separate method for clarity
        ProcessFolder(ocrEngine, @"C:\MyPngFolder");
    }

    // …
}
```

**Wskazówka:** Jeśli pracujesz na serwerze bez głowy (headless) bez GPU, możesz zamienić `GpuOcrEngine` na `OcrEngine` i kod zachowa się dokładnie tak samo.

## Krok 3 – Iteracja po obrazach w docelowym katalogu

Musimy **iterować po obrazach** i wybierać wyłącznie pliki PNG. Metoda `Directory.GetFiles` wykonuje ciężką pracę, a my zabezpieczymy się przed pustym folderem.

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    if (!Directory.Exists(folderPath))
    {
        Console.WriteLine($"❌ Folder not found: {folderPath}");
        return;
    }

    // Grab every *.png file – this is the “read png files” part
    string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

    if (pngFiles.Length == 0)
    {
        Console.WriteLine("⚠️ No PNG files found. Make sure the folder contains .png images.");
        return;
    }

    foreach (var pngPath in pngFiles)
    {
        Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
        ExtractAndSave(engine, pngPath);
    }
}
```

Zauważ użycie `SearchOption.TopDirectoryOnly`. Jeśli później będziesz potrzebować rekurencji w podfolderach, po prostu przełącz na `AllDirectories`. Ta mała zmiana pozwala **konwertować obrazy na tekst** w całym drzewie przy użyciu jednej linii.

## Krok 4 – Wykonaj OCR i zapisz wynik

Teraz przychodzi serce przepływu **batch OCR images**. Ładujemy każdy PNG, wywołujemy `Recognize()`, i zapisujemy wyodrębniony ciąg do pliku `.txt` o tej samej nazwie bazowej.

```csharp
static void ExtractAndSave(OcrEngine engine, string imagePath)
{
    try
    {
        // Load the PNG into the engine
        engine.Image = ImageStream.FromFile(imagePath);

        // Run recognition – this returns a RecognitionResult object
        RecognitionResult result = engine.Recognize();

        // Build the output path (same name, .txt extension)
        string txtPath = Path.ChangeExtension(imagePath, ".txt");

        // Write the OCR text to disk
        File.WriteAllText(txtPath, result.Text);

        Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        // Edge case: corrupted PNG or unsupported format
        Console.WriteLine($"❗ Error processing {Path.GetFileName(imagePath)}: {ex.Message}");
    }
}
```

**Dlaczego opakować to w try/catch?** W rzeczywistych partiach obrazów często pojawia się uszkodzony plik lub PNG używający nietypowego profilu kolorów. Przechwycenie wyjątku zapobiega awarii całego procesu i pozwala kontynuować przetwarzanie pozostałych plików.

## Krok 5 – Uruchom aplikację i zweryfikuj wynik

Zbuduj i uruchom aplikację:

```bash
dotnet run
```

Powinieneś zobaczyć log konsoli podobny do:

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

Otwórz dowolny z wygenerowanych plików `.txt` — znajdziesz w nim wyodrębniony tekst. Jeśli plik jest pusty, sprawdź jakość obrazu; OCR działa najlepiej przy wyraźnym, wysokokontrastowym tekście.

### Szybki skrypt weryfikacyjny (opcjonalnie)

Jeśli chcesz mieć pewność, że każdy PNG ma odpowiadający plik tekstowy, uruchom ten mały jednowierszowy skrypt PowerShell:

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## Typowe warianty i przypadki brzegowe

| Sytuacja | Co zmienić |
|-----------|----------------|
| **Języki niełacińskie** (np. cyrylica) | Ustaw `ocrEngine.Language = Language.Cyrillic;` |
| **Duży zestaw obrazów (>10 000 plików)** | Użyj `Parallel.ForEach`, aby przyspieszyć przetwarzanie, ale monitoruj zużycie pamięci GPU. |
| **Konieczność zachowania pierwotnej kolejności obrazów** | Posortuj `pngFiles` przed `foreach` (`Array.Sort(pngFiles);`). |
| **Uruchamianie na serwerze CI bez GPU** | Zamień `GpuOcrEngine` na `OcrEngine`, aby uniknąć błędów inicjalizacji GPU. |
| **Chcesz przetwarzać tylko pliki zawierające określone słowo kluczowe** | Po pobraniu `result.Text` sprawdź `result.Text.Contains("Invoice")` przed zapisem pliku. |

Te drobne zmiany pozwalają dostosować **pipeline konwertowania obrazów na tekst** do niemal każdej sytuacji, z jaką możesz się spotkać.

## Pełny kod źródłowy (gotowy do kopiowania)

```csharp
// ------------------------------------------------------------
// Extract Text from PNG – Batch OCR using Aspose.OCR (C#)
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine (GPU if possible)
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;

        // 2️⃣ Define the folder that holds your PNG files
        string targetFolder = @"C:\MyPngFolder";   // <-- change to your path

        // 3️⃣ Process every PNG in the folder
        ProcessFolder(ocrEngine, targetFolder);
    }

    static void ProcessFolder(OcrEngine engine, string folderPath)
    {
        if (!Directory.Exists(folderPath))
        {
            Console.WriteLine($"❌ Folder not found: {folderPath}");
            return;
        }

        string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

        if (pngFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No PNG files found.");
            return;
        }

        foreach (var pngPath in pngFiles)
        {
            Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
            ExtractAndSave(engine, pngPath);
        }
    }

    static void ExtractAndSave(OcrEngine engine, string imagePath)
    {
        try
        {
            engine.Image = ImageStream.FromFile(imagePath);
            RecognitionResult result = engine.Recognize();

            string txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, result.Text);

            Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❗ Error on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

Zapisz to jako `Program.cs`, uruchom `dotnet run` i obserwuj magię w działaniu.

## Zakończenie

Masz teraz **kompletny, gotowy do produkcji sposób wyodrębniania tekstu z plików PNG** przy użyciu C#. Samouczek obejmował wszystko — od konfiguracji projektu, inicjalizacji silnika OCR przyspieszanego GPU, **iteracji po obrazach**, po **batch OCR images** i zapisywanie wyników jako zwykły tekst.

Jeśli jesteś ciekawy kolejnych kroków, wypróbuj:

- **Konwertuj obrazy na tekst** dla innych formatów (JPG, BMP

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}