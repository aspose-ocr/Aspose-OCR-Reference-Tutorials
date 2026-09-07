---
category: general
date: 2026-09-06
description: konwersja obrazu OCR do JSON w C# przy użyciu Aspose.OCR – krok po kroku
  przewodnik, jak wyodrębnić tekst z obrazu i uzyskać wynik w formacie JSON.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- ocr image to json
- extract text from image
- convert image to text
- recognize text from photo
- load image for ocr
language: pl
lastmod: 2026-09-06
og_description: OCR obrazu do JSON w C# z Aspose.OCR. Dowiedz się, jak załadować obraz
  do OCR, rozpoznać tekst ze zdjęcia i przekonwertować wynik na JSON.
og_image_alt: Screenshot of C# code that converts an OCR image to JSON using Aspose.OCR
og_title: Konwertuj obraz OCR na JSON w C# – kompletny przewodnik Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-09-06'
  description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  headline: How to convert an OCR image to JSON in C# with Aspose.OCR
  type: TechArticle
- description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  name: How to convert an OCR image to JSON in C# with Aspose.OCR
  steps:
  - name: Place an image named `input.jpg` in the project root.
    text: Place an image named `input.jpg` in the project root.
  - name: Execute `dotnet run`.
    text: Execute `dotnet run`.
  - name: Observe the console output and open `output.json` to see the structured
      data.
    text: Observe the console output and open `output.json` to see the structured
      data.
  type: HowTo
- questions:
  - answer: Yes. Use `ocrEngine.SaveJson(Stream)` to write directly to a `MemoryStream`,
      then call `stream.ToArray()`.
    question: Can I get the OCR result as a byte array instead of a file?
  - answer: Aspose.OCR can accept PDF pages converted to images via Aspose.PDF, but
      the OCR engine itself works on raster images. Convert PDFs to images first,
      then **load image for ocr**.
    question: Does the engine support PDF input?
  - answer: 'Set `ocrEngine.Language = OcrLanguage.Arabic`. The JSON includes the
      correct text direction, which you can render in UI frameworks that support RTL.
      ## Conclusion You now have a complete solution for **ocr image to json** in
      C#. By loading an image, configuring the language, running the OCR engine, '
    question: How do I handle right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- JSON
- Image processing
title: Jak przekonwertować obraz OCR na JSON w C# przy użyciu Aspose.OCR
url: /pl/net/text-recognition/how-to-convert-an-ocr-image-to-json-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak przekonwertować obraz OCR na JSON w C# z Aspose.OCR

Jeśli potrzebujesz **ocr image to json** w aplikacji .NET, ten przewodnik pokaże Ci, jak to zrobić przy użyciu Aspose.OCR. Przejdziemy przez ładowanie obrazu do OCR, rozpoznawanie tekstu ze zdjęcia oraz konwersję wyniku do JSON, abyś mógł wykorzystać dane w API lub bazach danych.

Ekstrahowanie tekstu z plików graficznych to powszechne wymaganie przy przetwarzaniu faktur, skanowaniu paragonów i projektach archiwizacyjnych. Po zakończeniu tego tutorialu będziesz w stanie **convert image to text**, uzyskać wynik w postaci zwykłego tekstu oraz wygenerować ustrukturyzowany payload JSON zachowujący informacje o układzie.

## Prerequisites

Zanim rozpoczniesz, upewnij się, że masz:

- .NET 6.0 SDK lub nowszy zainstalowany  
- Visual Studio 2022 (lub dowolny edytor obsługujący .NET)  
- Pakiet NuGet Aspose.OCR (`Aspose.OCR`) dodany do projektu  
- Przykładowy obraz (`input.jpg`) umieszczony w folderze, do którego możesz odwołać się w kodzie  

Nie potrzebujesz dodatkowych silników OCR; Aspose.OCR radzi sobie z ciężką pracą wewnętrznie.

## Step 1: Install the Aspose.OCR NuGet package

Otwórz terminal w folderze projektu i uruchom:

```bash
dotnet add package Aspose.OCR
```

Pakiet zawiera klasę `Aspose.OCR.OcrEngine`, która udostępnia metody do **load image for ocr**, wyboru języka oraz eksportu wyniku.

## Step 2: Create a new C# console project

Jeśli nie masz jeszcze projektu, utwórz go:

```bash
dotnet new console -n OcrToJsonDemo
cd OcrToJsonDemo
```

Dodaj dyrektywy `using`, które będą potrzebne:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;
```

## Step 3: Load the image and configure the OCR engine

Poniższy kod demonstruje, jak **load image for ocr**, ustawić język i przygotować silnik do przetwarzania. W tym przykładzie używamy cyrylicy, ale możesz przełączyć się na `OcrLanguage.English`, `OcrLanguage.French` itp., w zależności od języka źródłowego.

```csharp
// Step 3: Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Choose the language that matches the text in the image.
// Replace OcrLanguage.Cyrillic with the language you need.
ocrEngine.Language = OcrLanguage.Cyrillic;

// Load the image file. The ImageStream class abstracts file, stream, or byte[] sources.
string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **Why this matters:** Ustawienie właściwego języka znacząco poprawia dokładność, gdy **recognize text from photo**. Silnik korzysta ze słowników i zestawów znaków specyficznych dla języka.

## Step 4: Run the OCR process and retrieve results

Teraz uruchom silnik OCR. Jeśli proces zakończy się sukcesem, możesz **extract text from image** jako zwykły tekst, HTML lub JSON. Aspose.OCR udostępnia metodę `SaveJson`, która zapisuje ustrukturyzowany wynik do pliku.

```csharp
// Step 4: Execute the OCR process
if (ocrEngine.Process())
{
    // Plain‑text output
    string plainText = ocrEngine.Text;
    Console.WriteLine("=== Plain Text ===");
    Console.WriteLine(plainText);

    // JSON output – includes bounding boxes, confidence scores, and line information
    string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
    ocrEngine.SaveJson(jsonPath);
    Console.WriteLine($"\nJSON result saved to: {jsonPath}");
}
else
{
    Console.WriteLine("OCR processing failed. Check the image path and format.");
}
```

### Expected JSON structure

Typowy plik `output.json` wygląda tak (sformatowany dla czytelności):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Пример текста",
          "Confidence": 0.96,
          "Rect": { "X": 45, "Y": 120, "Width": 210, "Height": 30 }
        },
        {
          "Text": "Еще одна строка",
          "Confidence": 0.93,
          "Rect": { "X": 45, "Y": 160, "Width": 230, "Height": 28 }
        }
      ]
    }
  ]
}
```

Payload JSON zawiera tekst każdej linii, współczynnik pewności oraz prostokąt obejmujący linię na oryginalnym zdjęciu. Dzięki temu łatwo jest odwzorować wynik OCR na elementy UI lub pola bazy danych.

## Step 5: Full source code for the demo

Poniżej znajduje się kompletny, gotowy do uruchomienia program, który realizuje workflow **ocr image to json**. Skopiuj go do `Program.cs` i uruchom `dotnet run`.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrToJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Select the language (Cyrillic in this example)
            ocrEngine.Language = OcrLanguage.Cyrillic;

            // 3️⃣ Load the image you want to process
            string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found: {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Run the OCR process
            if (ocrEngine.Process())
            {
                // 5️⃣ Retrieve plain text (optional)
                string plainText = ocrEngine.Text;
                Console.WriteLine("=== Plain Text ===");
                Console.WriteLine(plainText);

                // 6️⃣ Save the result as JSON
                string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
                ocrEngine.SaveJson(jsonPath);
                Console.WriteLine($"\nJSON result saved to: {jsonPath}");
            }
            else
            {
                Console.WriteLine("OCR processing failed. Verify the image format and language settings.");
            }
        }
    }
}
```

### Running the example

1. Umieść obraz o nazwie `input.jpg` w katalogu głównym projektu.  
2. Wykonaj `dotnet run`.  
3. Obserwuj wyjście w konsoli i otwórz `output.json`, aby zobaczyć ustrukturyzowane dane.

## Pro tips and common pitfalls

| Situation | Recommendation |
|-----------|----------------|
| **Low‑resolution photos** | Increase DPI before processing or use `ocrEngine.Image = ImageStream.FromFile(path, 300)` to force 300 DPI. |
| **Mixed languages** | Set `ocrEngine.Language = OcrLanguage.Multilingual` and optionally supply a language list via `ocrEngine.Language = new[] { OcrLanguage.English, OcrLanguage.Cyrillic }`. |
| **Large documents** | Process one page at a time to keep memory usage low; the engine supports multi‑page TIFFs. |
| **Incorrect characters** | Verify that the correct `OcrLanguage` is selected; using the wrong language reduces accuracy when you **convert image to text**. |
| **JSON missing fields** | Ensure you are using Aspose.OCR version 23.6 or later; older releases did not expose the `SaveJson` method. |

## Frequently asked questions

**Q: Czy mogę otrzymać wynik OCR jako tablicę bajtów zamiast pliku?**  
A: Tak. Użyj `ocrEngine.SaveJson(Stream)`, aby zapisać bezpośrednio do `MemoryStream`, a następnie wywołaj `stream.ToArray()`.

**Q: Czy silnik obsługuje wejście w formacie PDF?**  
A: Aspose.OCR może przyjmować strony PDF przekonwertowane na obrazy za pomocą Aspose.PDF, ale sam silnik OCR działa na obrazach rastrowych. Najpierw skonwertuj PDF‑y na obrazy, a potem **load image for ocr**.

**Q: Jak obsłużyć skrypty od prawej do lewej, takie jak arabski?**  
A: Ustaw `ocrEngine.Language = OcrLanguage.Arabic`. JSON zawiera prawidłowy kierunek tekstu, który możesz renderować w frameworkach UI obsługujących RTL.

## Conclusion

Masz teraz kompletną metodę na **ocr image to json** w C#. Ładując obraz, konfigurując język, uruchamiając silnik OCR i eksportując wynik jako JSON, możesz **extract text from image**, **convert image to text** oraz **recognize text from photo** w jednym, usprawnionym procesie.  

Od tego momentu możesz rozważyć:

- Integrację wyjścia JSON z Web API (`ASP.NET Core`)  
- Przechowywanie wyniku w bazie NoSQL, takiej jak MongoDB  
- Dodanie post‑processingu w celu korekty typowych błędów OCR  

Śmiało eksperymentuj z różnymi językami, formatami obrazów i opcjami wyjścia, aby dopasować rozwiązanie do potrzeb projektu. Powodzenia w kodowaniu!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [rozpoznaj tekst z obrazu w C# – Kompletny przewodnik po OCR i JSON](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/)
- [Konwertuj obraz na tekst w C# z Aspose OCR – Przewodnik krok po kroku](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [Jak wyodrębnić tekst z obrazu przy użyciu Aspose.OCR dla .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}