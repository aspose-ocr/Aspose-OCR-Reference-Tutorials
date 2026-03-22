---
category: general
date: 2026-03-21
description: Jak prosto wykonywać OCR wsadowo w C# — dowiedz się, jak wyodrębniać
  tekst z obrazów, konwertować obrazy na tekst i zapisywać OCR jako tekst z ustawieniami
  języka.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert images to text
- save OCR as text
- set OCR language
language: pl
og_description: Jak wykonywać OCR wsadowo w C# pozwala na wyodrębnianie tekstu z obrazów,
  konwertowanie obrazów na tekst oraz zapisywanie OCR jako tekstu przy jednoczesnym
  łatwym ustawianiu języka OCR.
og_title: Jak wykonać wsadowe OCR w C# – szybki przewodnik
tags:
- OCR
- C#
- Aspose
title: Jak wykonać wsadowe OCR w C# – Szybkie wyodrębnianie tekstu z obrazów
url: /pl/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonywać OCR wsadowo w C# – Szybko wyodrębniać tekst z obrazów

Zastanawiałeś się kiedyś **jak wykonywać OCR wsadowo**, gdy masz setki zdjęć leżących w folderze? Nie jesteś sam — programiści ciągle pytają, jak wyodrębnić tekst z obrazów bez pisania pętli dla każdego pliku. Dobrą wiadomością jest to, że Aspose.OCR zapewnia czysty, gotowy do równoległego przetwarzania sposób na **konwertowanie obrazów na tekst** w zaledwie kilku linijkach C#.

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokaże, jak **zapisać OCR jako tekst**, wybrać odpowiedni język i zwiększyć wydajność przetwarzania równoległego. Po zakończeniu będziesz mieć samodzielne rozwiązanie, które możesz wstawić do dowolnego projektu .NET.

## Czego będziesz potrzebować

- .NET 6 lub nowszy (API działa z .NET Core i .NET Framework)
- Aspose.OCR dla .NET (pakiet NuGet `Aspose.OCR`)
- Folder z obrazami, które chcesz przetworzyć (PNG, JPEG, TIFF itp.)
- Trochę ciekawości dotyczącej programowania równoległego (opcjonalne, ale przydatne)

Bez dodatkowych usług, bez kluczy do chmury — tylko czysty kod C#, który działa lokalnie.

---

![how to batch OCR workflow](placeholder.png){alt="diagram przepływu OCR wsadowego"}

## Krok 1: Skonfiguruj projekt i zainstaluj Aspose.OCR

Na początek, uruchom aplikację konsolową (lub użyj istniejącej) i dodaj pakiet Aspose.OCR:

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Wskazówka:** Jeśli używasz Visual Studio, kliknij prawym przyciskiem projektu → *Manage NuGet Packages* → wyszukaj *Aspose.OCR* i zainstaluj najnowszą stabilną wersję.

Daje to dostęp do `OcrBatchProcessor`, `OcrEngineSettings` oraz wyliczenia `Language`.

## Krok 2: Zdefiniuj foldery wejściowy i wyjściowy

Procesor wsadowy musi wiedzieć, gdzie znajdują się obrazy źródłowe i gdzie mają być zapisywane wyodrębnione pliki tekstowe. Utrzymuj ścieżki jako absolutne lub względne względem katalogu głównego projektu — po prostu upewnij się, że foldery istnieją przed uruchomieniem kodu.

```csharp
var inputPath  = @"C:\MyImages\BatchInput";
var outputPath = @"C:\MyImages\BatchResults";

// Ensure the output directory exists
if (!Directory.Exists(outputPath))
    Directory.CreateDirectory(outputPath);
```

> **Dlaczego to ważne:** Jeśli folder wyjściowy nie istnieje, procesor zgłosi wyjątek, przerywając całą operację wsadową. Utworzenie go wcześniej zapewnia płynne działanie.

## Krok 3: Skonfiguruj ustawienia OCR (w tym język)

Tutaj **ustawiasz język OCR** dla całego wsadu. Aspose.OCR obsługuje dziesiątki języków; domyślnie jest to angielski, ale możesz przełączyć na francuski, hiszpański itp., zmieniając wartość wyliczenia `Language`.

```csharp
var ocrSettings = new OcrEngineSettings
{
    Language = Language.English   // Change to Language.French, Language.Spanish, etc.
};
```

Jeśli kiedykolwiek będziesz potrzebował przetwarzać różne języki dla poszczególnych obrazów, możesz później nadpisać to ustawienie dla każdego pliku — więcej na ten temat później.

## Krok 4: Zbuduj obiekt `OcrBatchProcessor`

Teraz łączymy wszystko razem. `OcrBatchProcessor` pozwala określić folder wejściowy, folder wyjściowy, format wyjścia, opcje równoległości oraz wspólne ustawienia, które właśnie stworzyliśmy.

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System.Threading.Tasks;

var batch = new OcrBatchProcessor
{
    InputFolder   = inputPath,
    OutputFolder  = outputPath,
    OutputFormat  = OcrOutputFormat.PlainText, // **save OCR as text** in .txt files
    ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 }, // up to 4 threads
    Settings = ocrSettings
};
```

> **Dlaczego równoległość?** Gdy masz dziesiątki lub setki obrazów, przetwarzanie ich jeden po drugim może być żmudne. Ustawienie `MaxDegreeOfParallelism` na 4 pozwala środowisku uruchomieniowemu używać czterech rdzeni CPU jednocześnie, dramatycznie skracając całkowity czas na typowej stacji roboczej.

## Krok 5: Uruchom operację wsadową

Po skonfigurowaniu procesora, wykonanie to pojedyncze wywołanie metody. Biblioteka automatycznie obsługuje enumerację plików, OCR i zapisywanie wyników.

```csharp
batch.Execute();
Console.WriteLine("Batch OCR completed.");
```

Gdy konsola wyświetli *„Batch OCR completed.”*, znajdziesz plik `.txt` obok każdego oryginalnego obrazu w folderze `BatchResults`. Każdy plik tekstowy zawiera surowe znaki wyodrębnione z obrazu źródłowego — dokładnie to, czego potrzebujesz, aby **wyodrębnić tekst z obrazów** do dalszego przetwarzania.

### Oczekiwany wynik

```
C:\MyImages\BatchResults\image1.txt
C:\MyImages\BatchResults\image2.txt
...
```

Otwórz dowolny z tych plików, a zobaczysz zwykłą tekstową reprezentację zawartości obrazu.

## Krok 6: Zweryfikuj wyniki (opcjonalnie)

Dobrym nawykiem jest podwójne sprawdzenie kilku plików, aby upewnić się, że OCR działa zgodnie z oczekiwaniami. Szybkim sposobem jest odczytanie pierwszej linii każdego wygenerowanego pliku i wypisanie jej w konsoli:

```csharp
foreach (var txtFile in Directory.GetFiles(outputPath, "*.txt"))
{
    var firstLine = File.ReadLines(txtFile).FirstOrDefault();
    Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
}
```

Jeśli zauważysz zniekształcone znaki, rozważ zmianę ustawienia `Language` lub dostosowanie jakości obrazu (np. zwiększyć DPI, skonwertować do odcieni szarości).

## Zaawansowane warianty i przypadki brzegowe

### 1. Nadpisywanie języka per‑plik

Czasami wsad zawiera dokumenty wielojęzyczne. Możesz sprawdzić nazwę każdego obrazu i przypisać język w locie:

```csharp
batch.Settings = new OcrEngineSettings(); // default settings

batch.FileProcessing += (sender, args) =>
{
    if (args.FileName.Contains("_fr"))
        args.Settings.Language = Language.French;
    else if (args.FileName.Contains("_es"))
        args.Settings.Language = Language.Spanish;
    // otherwise keep the default (English)
};
```

### 2. Różne formaty wyjścia

Jeśli potrzebujesz przeszukiwalnych PDF‑ów zamiast zwykłego tekstu, zmień `OutputFormat`:

```csharp
batch.OutputFormat = OcrOutputFormat.SearchablePdf;
```

Spowoduje to **konwersję obrazów na tekst** wewnątrz kontenera PDF, zachowując oryginalny układ.

### 3. Obsługa dużych obrazów

Bardzo wysokiej rozdzielczości obrazy mogą zużywać dużo pamięci. Aby utrzymać proces lekki, włącz down‑sampling obrazu:

```csharp
batch.Settings.Dpi = 300; // lowers internal processing DPI
```

### 4. Logowanie błędów

Procesor zgłasza wyjątki dla nieczytelnych plików. Owiń `Execute` w blok try/catch i zaloguj problematyczne nazwy plików:

```csharp
try
{
    batch.Execute();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {ex.Data["FileName"]}: {ex.Message}");
}
```

## Pełny działający przykład

Łącząc wszystko razem, oto kompletny, gotowy do skopiowania i wklejenia program:

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System;
using System.IO;
using System.Linq;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        // 1️⃣ Input & output locations
        var inputFolder  = @"C:\MyImages\BatchInput";
        var outputFolder = @"C:\MyImages\BatchResults";

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ OCR settings – set OCR language
        var ocrSettings = new OcrEngineSettings
        {
            Language = Language.English // change as needed
        };

        // 3️⃣ Configure the batch processor
        var batch = new OcrBatchProcessor
        {
            InputFolder    = inputFolder,
            OutputFolder   = outputFolder,
            OutputFormat   = OcrOutputFormat.PlainText, // **save OCR as text**
            ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 },
            Settings       = ocrSettings
        };

        // 4️⃣ Run the batch job
        batch.Execute();

        // 5️⃣ Confirmation message
        Console.WriteLine("Batch OCR completed.");

        // 6️⃣ (Optional) Quick verification of a few results
        foreach (var txtFile in Directory.GetFiles(outputFolder, "*.txt").Take(5))
        {
            var firstLine = File.ReadLines(txtFile).FirstOrDefault();
            Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
        }
    }
}
```

Zapisz to jako `Program.cs`, zbuduj projekt i uruchom `dotnet run`. Zobaczysz w konsoli komunikat potwierdzający zakończenie, a następnie krótkie podgląd wyodrębnionego tekstu.

---

## Podsumowanie

Właśnie omówiliśmy **jak wykonywać OCR wsadowo** w C# przy użyciu Aspose.OCR, pokazując, jak **wyodrębnić tekst z obrazów**, **konwertować obrazy na tekst** i **zapisać OCR jako tekst**, jednocześnie **ustawiając język OCR** odpowiedni do Twojej treści. Przykład jest w pełni funkcjonalny, zawiera przetwarzanie równoległe dla szybkości i oferuje możliwości dla zaawansowanych scenariuszy, takich jak nadpisywanie języka per‑plik czy wyjście w formacie PDF.

Gotowy na kolejny krok? Spróbuj zamienić `OcrOutputFormat.PlainText` na `SearchablePdf` i zobacz, jak łatwo jest generować przeszukiwalne PDF‑y. Albo eksperymentuj z różnymi wartościami `MaxDegreeOfParallelism`, aby wycisnąć każdy ostatni milisekundę na maszynie wielordzeniowej.

Jeśli napotkasz problemy, sprawdź ponownie ścieżki folderów, upewnij się, że obrazy są czytelne i zweryfikuj, czy wyliczenie języka odpowiada tekstowi na Twoich zdjęciach. Szczęśliwego kodowania i niech Twoje wsady OCR będą szybkie i dokładne!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}