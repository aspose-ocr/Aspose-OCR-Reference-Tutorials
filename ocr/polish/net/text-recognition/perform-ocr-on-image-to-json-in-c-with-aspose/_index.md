---
category: general
date: 2026-04-08
description: Naucz się, jak wykonać OCR na obrazie i zapisać plik JSON w C# przy użyciu
  Aspose OCR. Ten samouczek Aspose OCR w C# pokazuje konwersję obrazu OCR do JSON
  z wartościami pewności.
draft: false
keywords:
- perform OCR on image
- write JSON file C#
- OCR image to JSON
- Aspose OCR C# tutorial
language: pl
og_description: Wykonaj OCR na obrazie i wyeksportuj wyniki do pliku JSON w C#. Ten
  samouczek obejmuje pełny przepływ pracy Aspose OCR w C#, w tym oceny pewności.
og_title: Wykonaj OCR obrazu do JSON w C# – Przewodnik Aspose OCR
tags:
- Aspose
- OCR
- C#
- JSON
title: Wykonaj OCR obrazu do JSON w C# z Aspose
url: /pl/net/text-recognition/perform-ocr-on-image-to-json-in-c-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wykonaj OCR na obrazie i uzyskaj JSON w C# z Aspose

Czy kiedykolwiek potrzebowałeś **wykonać OCR na plikach obrazu**, ale nie wiedziałeś, jak uzyskać wyniki w ustrukturyzowanym formacie? Nie jesteś sam — programiści często pytają: „Jak zamienić zeskanowany obraz na użyteczne dane?” Dobra wiadomość jest taka, że Aspose.OCR robi to banalnie proste, a dodatkowo możesz **zapisz plik JSON w stylu C#** z uwzględnieniem współczynników pewności.

W tym przewodniku przeprowadzimy Cię przez kompletny **aspose OCR C# tutorial**, który obejmuje wszystko, od wczytania obrazu po wyeksportowanie rozpoznanego tekstu jako JSON. Po zakończeniu będziesz mieć działającą aplikację konsolową, która **wykonuje OCR na obrazie**, konwertuje wynik na JSON (wraz z wartościami pewności) i zapisuje go jedną linijką kodu. Bez ukrytych kroków, bez zewnętrznych skryptów — czyste C#.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz:

- .NET 6.0 SDK lub nowszy (kod działa również z .NET Core i .NET Framework)
- Visual Studio 2022 (lub dowolny edytor, którego używasz)
- Ważną licencję **Aspose.OCR for .NET** lub darmową licencję tymczasową (bezpłatna wersja próbna wystarczy do testów)
- Plik obrazu (`input.png`), który chcesz przetworzyć (dowolny popularny format — PNG, JPG, BMP — będzie odpowiedni)

To wszystko. Jeśli czegoś brakuje, zdobądź to teraz; dalsza część tutorialu zakłada, że wszystkie elementy są już gotowe.

## Krok 1: Zainstaluj pakiet NuGet Aspose.OCR

Na początek dodaj bibliotekę do projektu. Otwórz terminal w folderze projektu i uruchom:

```bash
dotnet add package Aspose.OCR
```

Spowoduje to pobranie najnowszej wersji (na kwiecień 2026 to 23.12) i dodanie niezbędnych DLL‑ów do folderu `bin`. Nie wymaga dodatkowej konfiguracji.

## Krok 2: Zainicjalizuj silnik OCR (Perform OCR on Image)

Teraz tworzymy instancję `OcrEngine` i określamy, jakiego języka użyć. Angielski (`"en"`) jest najczęstszy, ale możesz zamienić go na `"fr"`, `"de"` lub dowolny obsługiwany język.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Path to your input image – change as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        // Path where the JSON will be saved
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // Step 2: Initialize the OCR engine – this is where we **perform OCR on image**
        var ocrEngine = new OcrEngine
        {
            Language = "en"               // Set language; you can use ISO‑639‑1 codes
        };

        // Optional: tweak recognition options (speed vs. accuracy)
        // ocrEngine.RecognitionMode = RecognitionMode.LargeText; // Uncomment for large blocks
```

**Dlaczego inicjalizujemy tutaj:** `OcrEngine` przechowuje całą konfigurację potrzebną do procesu rozpoznawania. Ustawienie języka z góry zapewnia, że silnik użyje właściwego zestawu znaków, co znacząco podnosi dokładność.

## Krok 3: Rozpoznaj obraz i przechwyć współczynnik pewności

Po przygotowaniu silnika podajemy mu plik obrazu. Metoda `RecognizeImage` zwraca obiekt `OcrResult`, który zawiera zarówno wyodrębniony tekst, jak i współczynnik pewności dla każdego słowa.

```csharp
        // Step 3: Perform OCR on the image file
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Verify that the result is not null
        if (ocrResult == null)
        {
            Console.WriteLine("OCR failed – check the file path and format.");
            return;
        }

        // For debugging: print the plain text to the console
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
```

**Co się dzieje „pod maską”?** Aspose uruchamia rozpoznawacz oparty na sieci neuronowej, który analizuje każdy blok pikseli, dopasowuje go do modelu językowego i dołącza wartość pewności (0‑100), informującą, jak bardzo jest pewny co do każdego słowa.

## Krok 4: Konwertuj wynik na JSON (OCR Image to JSON)

Aspose upraszcza konwersję. Przekazując `includeConfidence: true`, otrzymujemy ładunek JSON wyglądający tak:

```json
{
  "Text": "Hello world",
  "Words": [
    { "Value": "Hello", "Confidence": 97.3 },
    { "Value": "world", "Confidence": 95.8 }
  ]
}
```

Oto kod, który generuje łańcuch JSON:

```csharp
        // Step 4: Convert OCR result to JSON, including confidence values
        string jsonResult = ocrResult.ToJson(includeConfidence: true);
```

**Dlaczego dołączamy pewność?** Jeśli zamierzasz przekazać dane do dalszych procesów (np. walidacji, podświetlania w UI), znajomość słabych słów pozwala zdecydować, czy poprosić użytkownika o potwierdzenie.

## Krok 5: Zapisz plik JSON w stylu C#

Teraz naprawdę **zapisz JSON file C#**. Metoda `File.WriteAllText` jest atomowa i działa wieloplatformowo, co czyni ją idealną dla aplikacji konsolowych.

```csharp
        // Step 5: Save the JSON output to a file
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

To cały przepływ — pięć zwięzłych kroków, które **wykonują OCR na obrazie**, przekształcają wynik na JSON i zapisują go.

## Pełny działający przykład

Poniżej pełny program, który możesz skopiować do `Program.cs`. Upewnij się, że `input.png` znajduje się w tym samym folderze co skompilowany plik binarny lub dostosuj ścieżki odpowiednio.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------------
        // 1️⃣ Set up file locations (feel free to change paths)
        // -------------------------------------------------------
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // -------------------------------------------------------
        // 2️⃣ Initialize the OCR engine – this is where we **perform OCR on image**
        // -------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = "en" // English – replace with "fr", "es", etc. as needed
        };

        // -------------------------------------------------------
        // 3️⃣ Recognize the image and obtain confidence values
        // -------------------------------------------------------
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        if (ocrResult == null)
        {
            Console.WriteLine("❌ OCR failed – verify the image path and format.");
            return;
        }

        // Show plain text (optional)
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine();

        // -------------------------------------------------------
        // 4️⃣ Convert the result to JSON – **OCR image to JSON**
        // -------------------------------------------------------
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // -------------------------------------------------------
        // 5️⃣ Write the JSON file – **write JSON file C#** style
        // -------------------------------------------------------
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

### Oczekiwany wynik

Po uruchomieniu programu (`dotnet run`) zobaczysz coś w stylu:

```
=== Extracted Text ===
Hello world

✅ JSON with confidence saved to: C:\YourProject\output.json
```

A `output.json` będzie zawierał ustrukturyzowany JSON pokazany wcześniej, wraz z procentowymi wartościami pewności dla każdego słowa.

## Porady profesjonalne i przypadki brzegowe

- **Obsługa brakującego pliku:** Owiń wywołanie `RecognizeImage` w `try/catch` dla `FileNotFoundException`, jeśli spodziewasz się dynamicznych ścieżek.
- **Różne języki:** Ustaw `ocrEngine.Language = "fr"` dla francuskiego lub wczytaj własny pakiet językowy za pomocą `ocrEngine.LoadLanguage("custom.lang")`.
- **Duże dokumenty:** W przypadku wielostronicowych PDF‑ów, najpierw skonwertuj każdą stronę na obraz (np. przy użyciu `Aspose.PDF`) i przejdź pętlą przez kroki OCR.
- **Dostosowanie wydajności:** Jeśli potrzebujesz szybkich wyników, przełącz na `RecognitionMode.Fast` — tracisz nieco dokładności, ale zyskujesz prędkość.
- **Formatowanie JSON:** Chcesz ładnie sformatowany JSON? Użyj `JsonConvert.SerializeObject` z biblioteki Newtonsoft z opcją `Formatting.Indented` po deserializacji łańcucha JSON Aspose.

## Najczęściej zadawane pytania

**P: Czy to działa z .NET Framework?**  
O: Zdecydowanie tak. Ten sam pakiet NuGet celuje w .NET Standard 2.0, więc możesz go odwołać z .NET Framework 4.6.1 i nowszych.

**P: Co zrobić, jeśli potrzebuję pewności dla całego dokumentu, a nie dla każdego słowa?**  
O: `OcrResult` udostępnia także `OverallConfidence`. Możesz dodać ją ręcznie do JSON:

```csharp
var customObj = new
{
    Text = ocrResult.Text,
    OverallConfidence = ocrResult.OverallConfidence,
    Words = ocrResult.Words
};
string json = JsonConvert.SerializeObject(customObj, Formatting.Indented);
```

**P: Czy mogę strumieniowo przesłać JSON bezpośrednio do API webowego?**  
O: Tak. Zastąp `File.WriteAllText` wywołaniem POST przy użyciu `HttpClient`, które wyśle `jsonResult`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}