---
category: general
date: 2026-01-02
description: Wyodrębnij tekst z obrazu przy użyciu Aspose OCR w C#. Dowiedz się, jak
  szybko i niezawodnie konwertować obraz do formatu JSONL.
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: pl
og_description: Wyodrębnij tekst z obrazu za pomocą Aspose OCR i przekonwertuj go
  do formatu JSONL. Pełny, krok po kroku, tutorial C# dla programistów.
og_title: Wyodrębnij tekst z obrazu – konwertuj do JSONL w C#
tags:
- C#
- OCR
- Aspose
- JSONL
title: Wyodrębnij tekst z obrazu i konwertuj do JSONL – przewodnik C#
url: /pl/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tekstu z obrazu i konwersja do JSONL – Kompletny samouczek C#

Czy kiedykolwiek potrzebowałeś **wyodrębnić tekst z obrazu**, ale nie byłeś pewien, która biblioteka zapewni czyste, ustrukturyzowane wyniki? Nie jesteś sam. W wielu projektach przetwarzania paragonów lub digitalizacji dokumentów wąskim gardłem jest przekształcenie bitmapy w przeszukiwalny tekst *oraz* format czytelny dla maszyn.  

Dobre wieści? Dzięki Aspose OCR możesz **wyodrębnić tekst z obrazu** i, w kilku linijkach kodu, **przekonwertować obraz do JSONL** dla dalszych analiz. Ten przewodnik przeprowadzi Cię przez cały proces, od wczytania pliku PNG po zapisanie pliku JSON‑Lines, który może być strumieniowany do potoku danych.

> **Wskazówka:** Jeśli już używasz .NET 6 lub nowszego, ten sam kod działa bez dodatkowej konfiguracji.

## Wymagania wstępne — Czego będziesz potrzebować

- **.NET 6 SDK** (lub dowolna nowsza wersja .NET)
- **Aspose.OCR** pakiet NuGet  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json** do serializacji  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- Przykładowy obraz (np. `receipt.png`) umieszczony w folderze, do którego możesz odwołać się.
- IDE lub edytor według wyboru — Visual Studio, VS Code, Rider itp.

Bez skomplikowanej konfiguracji, bez zewnętrznych usług, tylko garść pakietów NuGet.

![Extract text from image using C#](https://example.com/assets/ocr-sample.png)

*Alt text: wyodrębnić tekst z obrazu przy użyciu C# z Aspose OCR*

## Krok 1: Załaduj obraz, który chcesz przetworzyć  

Pierwszą rzeczą, którą robisz, gdy chcesz **wyodrębnić tekst z obrazu**, jest przekazanie silnikowi OCR bitmapy. Użycie `System.Drawing.Bitmap` jest proste i działa dla większości formatów rastrowych.

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **Dlaczego to ważne:** Ładowanie obrazu jako `Bitmap` daje silnikowi OCR bezpośredni dostęp do pikseli, co poprawia szybkość rozpoznawania i dokładność w porównaniu ze strumieniowaniem surowych bajtów.

## Krok 2: Skonfiguruj Aspose OCR do wyjścia w formacie JSON‑Lines  

Aspose OCR pozwala określić język, format wyjścia oraz kilka poprawek wydajnościowych. Tutaj żądamy **JSON‑Lines** (jeden obiekt JSON na linię), ponieważ jest to idealne do późniejszego przetwarzania linia po linii.

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

> **Pro tip:** Jeśli potrzebujesz wielojęzycznych paragonów, ustaw `Language = Language.Multilingual` lub przekaż tablicę wartości `Language`.

## Krok 3: Uruchom OCR i przechwyć wynik  

Teraz faktycznie **wyodrębniamy tekst z obrazu**. Metoda `Recognize` zwraca obiekt `OcrResult`, który zawiera kolekcję obiektów `OcrLine`, z których każdy reprezentuje linię rozpoznanego tekstu wraz z jej ramką ograniczającą.

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

W tym momencie `ocrResult.Lines` zawiera wszystko, czego potrzebujesz — surowy tekst, oceny pewności i współrzędne.

## Krok 4: Serializuj linie do JSON‑Lines  

Przekształcimy kolekcję w ładnie wcięty ciąg JSON. Mimo że JSON‑Lines są zazwyczaj kompaktowe, dodanie wcięć ułatwia przeglądanie pliku podczas rozwoju.

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

Zmienna `jsonLines` wygląda mniej więcej tak (skrócona dla zwięzłości):

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

Każda linia kończy się znakiem nowej linii, co daje prawdziwy plik **JSONL** (JSON‑Lines).

## Krok 5: Zapisz JSON‑Lines na dysku  

Na koniec zapisujemy wynik, aby inne usługi — takie jak Spark, Logstash czy prosty skrypt Bash — mogły go przetwarzać linia po linii.

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

Gdy otworzysz `receipt.jsonl`, zobaczysz jeden obiekt JSON na linię, gotowy do strumieniowania.

## Krok 6: Zweryfikuj eksport  

Szybka kontrola poprawności zaoszczędzi Ci godziny debugowania później. Odczytajmy kilka pierwszych linii i wypiszmy je na konsolę.

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

Typowy wynik w konsoli:

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

Jeśli widzisz coś podobnego, gratulacje — udało Ci się **wyodrębnić tekst z obrazu** i **przekonwertować obraz do JSONL**.

## Typowe pułapki i jak ich uniknąć  

| Problem | Dlaczego się pojawia | Rozwiązanie |
|-------|----------------|-----|
| **Pusty wynik** | Nieprawidłowa ścieżka obrazu lub plik nieczytelny. | Użyj `File.Exists(imagePath)` przed utworzeniem bitmapy. |
| **Niskie oceny pewności** | Obraz jest rozmyty lub ma niski kontrast. | Wstępnie przetwórz obraz (np. `Bitmap.RotateFlip`, `Graphics.Clear`) lub zwiększ DPI. |
| **Nieprawidłowy język** | OCR domyślnie używa angielskiego, ale paragon jest w innym języku. | Ustaw `options.Language = Language.Spanish` (lub odpowiedni enum). |
| **JSONL pojawia się jako pojedyncza tablica JSON** | Użyto `Formatting.None` bez obsługi znaków nowej linii. | Upewnij się, że każdy zserializowany obiekt kończy się `Environment.NewLine`. |

## Pełny działający przykład  

Poniżej znajduje się kompletny, gotowy do uruchomienia program. Wklej go do projektu konsolowego i naciśnij **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**Oczekiwany wynik:** Plik `receipt.jsonl` zawierający jeden obiekt JSON na linię, każdy z polami `Text`, `Confidence` i `BoundingBox`. Teraz możesz wprowadzić ten plik do dowolnego potoku analitycznego, który konsumuje JSONL.

## Kolejne kroki – wyjście poza podstawowy OCR  

- **Przetwarzanie wsadowe:** Owiń powyższą logikę w pętlę `foreach`, aby obsługiwać całe foldery z paragonami.  
- **Równoległość:** Użyj `Parallel.ForEach` dla przyspieszenia na wielu rdzeniach przy przetwarzaniu tysięcy obrazów.  
- **Post‑processing:** Usuń linie o niskiej pewności (`Confidence < 0.9`) przed zapisaniem.  
- **Integracja:** Prześlij JSONL bezpośrednio do Azure Blob Storage lub AWS S3 przy użyciu odpowiednich SDK.  
- **Alternatywne formaty:** Zmień `OutputFormat` na `PlainText` lub `Xml`, jeśli Twój system downstream preferuje te formaty.  

## Zakończenie  

Masz teraz solidne, kompleksowe rozwiązanie do **wyodrębniania tekstu z obrazu** i **konwersji obrazu do JSONL** przy użyciu Aspose OCR w C#. Samouczek obejmował wszystko, od ładowania bitmapy po weryfikację wyniku, a także kilka praktycznych wskazówek, które utrzymają Twój potok danych w dobrej kondycji.  

Wypróbuj go na własnych paragonach, fakturach lub zeskanowanych formularzach — zobacz, jak silnik OCR przekształca piksele w przeszukiwalne, liniowo ustrukturyzowane dane w ciągu kilku sekund. Jeśli napotkasz przypadki brzegowe (np. skośne skany lub tekst wielojęzyczny), wróć do sekcji *RecognitionOptions* i dostosuj język lub kroki wstępnego przetwarzania.  

Szczęśliwego kodowania i niech Twoje potoki danych będą zawsze czyste!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}