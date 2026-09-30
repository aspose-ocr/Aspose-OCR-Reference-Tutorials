---
category: general
date: 2026-02-09
description: Dowiedz się, jak wykonać OCR w C#, aby wyodrębnić tekst z obrazu, rozpoznać
  tekst z pliku PNG i szybko zapisać plik JSON w C#.
draft: false
keywords:
- how to perform OCR
- extract text from image
- recognize text from png
- write json file c#
language: pl
og_description: Jak wykonać OCR w C#? Skorzystaj z tego przewodnika krok po kroku,
  aby wyodrębnić tekst z obrazu, rozpoznać tekst z pliku PNG i efektywnie zapisać
  plik JSON w C#.
og_title: Jak wykonać OCR w C# – wyodrębnić tekst i zapisać JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: Jak wykonać OCR w C# – wyodrębnić tekst i zapisać JSON
url: /pl/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonać OCR w C# – Kompletny przewodnik

Wykonywanie OCR w C# to powszechna przeszkoda, gdy trzeba **extract text from image** plików. W tym przewodniku przeprowadzimy rozpoznawanie tekstu z PNG, wyeksportujemy szczegółowy wynik do ciągu JSON, a na koniec **write JSON file C#** w stylu C#. Czy kiedykolwiek patrzyłeś na zeskanowany formularz i zastanawiałeś się, jak zamienić te zarysy w przeszukiwalny tekst? Nie jesteś sam; wielu programistów napotyka ten problem na wczesnym etapie.

Użyjemy biblioteki Aspose.OCR, ponieważ dostarcza ona pewność na poziomie symbolu od razu i dobrze współpracuje z projektami .NET 6+. Po zakończeniu tego samouczka będziesz mieć gotową do uruchomienia aplikację konsolową, która wczyta PNG, wyciągnie każdy znak i zapisze schludny plik JSON, który możesz wprowadzić do bazy danych lub modelu AI. Bez tajemniczych skrótów „zobacz dokumentację” — po prostu samodzielne rozwiązanie.

## Czego będziesz potrzebować

- **.NET 6 SDK** (lub nowszy) – aktualna wersja LTS w momencie pisania.
- **Aspose.OCR for .NET** pakiet NuGet – `Install-Package Aspose.OCR`.
- Obraz PNG, który chcesz zeskanować (np. `form.png`).  
- IDE lub edytor – Visual Studio, VS Code, Rider – cokolwiek jest dla Ciebie wygodne.

To wszystko. Jeśli masz te elementy, możesz zaczynać.

![Przykład wykonania OCR](ocr-example.png "How to perform OCR in C#")

*Tekst alternatywny obrazu: ilustracja jak wykonać OCR pokazująca aplikację konsolową C# przetwarzającą PNG.*

## Krok 1: Konfiguracja projektu i dodanie zależności

Najpierw utwórz nowy projekt konsolowy i pobierz bibliotekę Aspose OCR.

```csharp
// Create a new console app (run in terminal)
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo

// Add Aspose.OCR NuGet package
dotnet add package Aspose.OCR
```

> **Pro tip:** Użyj flagi `--framework net6.0`, jeśli chcesz jawnie zablokować docelowy framework.

Dlaczego ten krok ma znaczenie: pakiet NuGet zawiera klasy `OcrEngine`, `ImageStream` i `JsonExporter`, na które będziemy polegać. Bez nich kompilator nie będzie miał pojęcia, co oznacza „OCR”.

## Krok 2: Napisz podstawową logikę OCR

Otwórz `Program.cs` (lub utwórz nowy plik) i zamień jego zawartość na poniższą. Każda sekcja jest skomentowana, abyś mógł zobaczyć, dlaczego jest potrzebna.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Export;
using System;

namespace OcrJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialize the OCR engine – this prepares the
            //    internal models and allocates native resources.
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣ Load the image you want to process.
            //    Replace the path with your own PNG file.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/form.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR recognition – the heavy lifting.
            //    The result includes text, per‑symbol confidence,
            //    and layout information.
            // -------------------------------------------------
            RecognitionResult ocrResult = ocrEngine.Recognize(image);

            // -------------------------------------------------
            // 4️⃣ Export the result to a JSON string.
            //    JsonExporter respects the confidence values.
            // -------------------------------------------------
            JsonExporter jsonExporter = new JsonExporter();
            string jsonContent = jsonExporter.ExportToString(ocrResult);

            // -------------------------------------------------
            // 5️⃣ Write the JSON to disk – this is how we
            //    **write JSON file C#** style.
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/form.json";
            System.IO.File.WriteAllText(jsonPath, jsonContent);

            // -------------------------------------------------
            // 6️⃣ Let the user know we succeeded.
            // -------------------------------------------------
            Console.WriteLine($"JSON file saved successfully at {jsonPath}");
        }
    }
}
```

### Dlaczego każdy element jest ważny

- **OcrEngine**: Traktuj go jak mózg operacji. Ładuje modele językowe i konfiguruje pipeline inferencji.
- **ImageStream.FromFile**: Obsługuje dowolny PNG, JPEG, BMP itp. Abstrahuje szczegóły I/O plików.
- **RecognitionResult**: Przechowuje surowy tekst oraz wyniki pewności. To miejsce, gdzie otrzymujesz szczegółowe dane potrzebne do dalszej walidacji.
- **JsonExporter**: Konwertuje bogaty `RecognitionResult` na czysty ładunek JSON, idealny dla API.
- **File.WriteAllText**: Prosty sposób w .NET do **write JSON file C#** bez dodatkowych zależności.

## Krok 3: Uruchom aplikację i zweryfikuj wynik

Skompiluj i uruchom program:

```bash
dotnet run
```

Powinieneś zobaczyć komunikat w konsoli podobny do:

```
JSON file saved successfully at YOUR_DIRECTORY/form.json
```

Otwórz `form.json` – znajdziesz coś podobnego do:

```json
{
  "Text": "Sample Form\nName: John Doe\nDate: 2026-02-09",
  "Symbols": [
    { "Char": "S", "Confidence": 0.99, "X": 12, "Y": 8 },
    { "Char": "a", "Confidence": 0.98, "X": 22, "Y": 8 },
    // … more symbols …
  ]
}
```

Krok **extract text from image** zakończył się sukcesem i masz teraz maszynowo‑czytelną reprezentację JSON każdego znaku.

## Krok 4: Obsługa typowych przypadków brzegowych

### Brakujące lub uszkodzone pliki

Jeśli ścieżka PNG jest nieprawidłowa, `ImageStream.FromFile` rzuca `FileNotFoundException`. Owiń kod ładowania w blok try‑catch:

```csharp
try
{
    ImageStream image = ImageStream.FromFile(imagePath);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"Could not find image: {ex.Message}");
    return;
}
```

### Niskie wyniki pewności

Czasami OCR zwraca niską pewność przy zaszumionych skanach. Możesz odfiltrować symbole przed eksportem:

```csharp
ocrResult.Symbols.RemoveAll(s => s.Confidence < 0.6);
```

To zapewnia, że JSON zawiera tylko stosunkowo wiarygodne znaki — przydatne, gdy wprowadzasz dane do kolejnych potoków walidacji.

### Duże pliki i pamięć

Przetwarzanie wielomegabajtowego PNG może zwiększyć zużycie pamięci. Rozważ strumieniowanie obrazu w fragmentach lub użycie `OcrEngine.RecognizeAsync` (dostępne w nowszych wersjach Aspose), aby UI pozostało responsywne.

## Krok 5: Rozszerzenie rozwiązania (opcjonalnie)

- **Batch processing**: Przejdź przez katalog PNG i wygeneruj odpowiadający JSON dla każdego pliku.
- **Database storage**: Wstaw JSON do kolumny SQL `NVARCHAR(MAX)` w celu późnej analizy.
- **Language selection**: Ustaw `ocrEngine.Language = OcrLanguage.Spanish;`, jeśli potrzebujesz wsparcia dla języka innego niż angielski.

Wszystkie te rozszerzenia podążają za tym samym wzorcem **how to perform OCR**, który ustaliliśmy — inicjalizacja, rozpoznawanie, eksport i przechowywanie.

## Najczęściej zadawane pytania

**Q: Czy to działa z JPG lub TIFF?**  
A: Zdecydowanie tak. `ImageStream.FromFile` automatycznie wykrywa format, więc możesz zamienić PNG na dowolny obsługiwany obraz rastrowy.

**Q: Co zrobić, jeśli muszę **extract text from a PDF**?**  
A: Najpierw skonwertuj każdą stronę PDF na obraz (np. przy użyciu `Aspose.PDF`), a następnie podaj PNG do przepływu OCR opisanego tutaj.

**Q: Czy mogę otrzymać wynik OCR jako XML zamiast JSON?**  
A: Tak. Aspose.OCR dostarcza również `XmlExporter`. Zamień `JsonExporter` na `XmlExporter` i dostosuj rozszerzenie pliku.

## Zakończenie

Przeszliśmy przez **how to perform OCR** w C# od początku do końca, pokazując jak **extract text from image**, **recognize text from PNG** oraz **write JSON file C#** bez problemów. Pełny, działający przykład znajduje się w powyższych fragmentach kodu, a Ty rozumiesz, dlaczego każdy krok jest potrzebny — inicjalizacja silnika, obsługa przypadków brzegowych i przechowywanie wyników.

Następnie możesz zbadać przetwarzanie wsadowe OCR, zintegrować wynik JSON z Azure Cognitive Search lub eksperymentować z własnymi modelami językowymi. Nie ma ograniczeń, gdy opanujesz podstawy OCR w C#.

Jeśli napotkasz jakiekolwiek problemy lub masz pomysły na dalsze rozszerzenia, zostaw komentarz poniżej. Szczęśliwego kodowania i ciesz się przekształcaniem pikselowych skanów w czyste, przeszukiwalne dane!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}