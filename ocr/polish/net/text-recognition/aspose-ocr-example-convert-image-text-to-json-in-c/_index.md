---
category: general
date: 2026-04-17
description: Poznaj przykład Aspose OCR do odczytu pliku obrazu w C#, wyodrębniania
  tekstu z obrazu w C# i zapisu pliku JSON w C#. Kompletny, krok po kroku, tutorial
  OCR w C#.
draft: false
keywords:
- aspose ocr example
- write json file c#
- read image file c#
- extract text image c#
- c# ocr tutorial
language: pl
og_description: Opanuj przykład Aspose OCR, aby odczytać obraz, wyodrębnić tekst i
  zapisać plik JSON przy użyciu C#. Skorzystaj z tego zwięzłego samouczka OCR w C#.
og_title: przykład aspose ocr – konwersja tekstu z obrazu do JSON w C#
tags:
- Aspose
- OCR
- C#
- JSON
title: przykład aspose ocr – konwersja tekstu obrazu do JSON w C#
url: /pl/net/text-recognition/aspose-ocr-example-convert-image-text-to-json-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# aspose ocr example – Konwersja tekstu z obrazu do JSON w C#

Kiedykolwiek potrzebowałeś **aspose ocr example**, które nie tylko odczytuje obraz, ale także generuje schludny JSON do dalszego przetwarzania? Nie jesteś sam. W wielu projektach — automatyzacja faktur, skanowanie paragonów czy nawet proste archiwizowanie dokumentów — programiści napotykają ten sam problem: „Jak uzyskać wynik OCR w formacie, który moja API akceptuje?”

Dobre wieści? Dzięki Aspose.OCR możesz to zrobić w kilku linijkach, a ja pokażę Ci dokładnie jak. Po przeczytaniu tego przewodnika będziesz wiedział, jak **read image file C#**, **extract text image C#**, oraz **write JSON file C#** — wszystko w czystym, wielokrotnego użytku tutorialu C# OCR.

## Czego będziesz potrzebował

- .NET 6.0 lub nowszy (kod kompiluje się także z .NET Core)  
- Pakiet NuGet Aspose.OCR dla .NET (`Install-Package Aspose.OCR`)  
- Obraz (`input.jpg`) zawierający wyraźny, maszynowo‑czytelny tekst  
- Edytor tekstu lub Visual Studio (dowolne IDE będzie odpowiednie)  

Brak dodatkowych plików konfiguracyjnych, żadnej ukrytej magii — tylko SDK i obraz.

## Krok 1 – Odczyt pliku obrazu C# przy użyciu Aspose.OCR

Na początek: musisz dostarczyć silnikowi OCR prawidłowy obraz. Aspose.OCR oczekuje obiektu `OcrImage`, który możesz utworzyć bezpośrednio z ścieżki pliku.

```csharp
using Aspose.OCR;
using System.IO;

// Path to the source picture
string imagePath = @"C:\MyProject\Images\input.jpg";

// Load the image – this is the “read image file C#” part
OcrImage ocrImage = OcrImage.FromFile(imagePath);
```

*Dlaczego to ważne:* Wczesne wczytanie obrazu pozwala zweryfikować istnienie pliku i wykryć problemy z formatem, zanim silnik zacznie przetwarzać piksele. Jeśli plik nie istnieje, `FromFile` rzuca czytelny wyjątek, który możesz obsłużyć dalej.

## Krok 2 – Inicjalizacja silnika Aspose OCR

Utworzenie silnika jest tanie, ale powinieneś owinąć je w instrukcję `using`, aby zasoby były zwalniane od razu.

```csharp
// Create the OCR engine – it holds all the recognition settings
using var ocrEngine = new OcrEngine();
```

*Pro tip:* Domyślny silnik działa dobrze dla większości tekstów opartych na alfabecie łacińskim. Jeśli potrzebujesz innego języka, możesz ustawić `ocrEngine.Language = Language.YourLanguage;` przed wywołaniem `Recognize`.

## Krok 3 – Ekstrakcja tekstu z obrazu C# – Wykonaj rozpoznawanie

Teraz odbywa się najcięższa część. Metoda `Recognize` zwraca obiekt `OcrResult`, który zawiera surowy tekst, oceny pewności oraz ramki ograniczające dla każdego słowa.

```csharp
// Run OCR – this is the “extract text image C#” step
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);
```

Zauważysz, że `ocrResult.Text` zawiera zwykły ciąg znaków, natomiast `ocrResult.Regions` dostarcza danych pozycyjnych, jeśli kiedykolwiek będziesz musiał podświetlić słowa w interfejsie użytkownika.

## Krok 4 – Zapis pliku JSON C# – Serializacja wyniku

Serializacja do JSON jest prosta przy użyciu `System.Text.Json`. Sformatujemy wyjście w czytelny sposób, aby było przyjazne dla człowieka.

```csharp
using System.Text.Json;

// Convert the OCR result to nicely formatted JSON
string json = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true });
```

*Dlaczego używamy `System.Text.Json`*: Jest wbudowany w .NET, szybki i nie wymaga dodatkowych zależności. Jeśli wolisz Newtonsoft, kod zmieni się tylko w kilku linijkach.

## Krok 5 – Zapisz JSON na dysku

Na koniec zapisz ciąg znaków do pliku. To kończy część **write json file c#**.

```csharp
// Destination path for the JSON output
string jsonOutputPath = @"C:\MyProject\Output\ocrResult.json";

// Save the JSON – now you have a portable data file
File.WriteAllText(jsonOutputPath, json);

Console.WriteLine("OCR data saved as JSON.");
```

### Oczekiwany wynik JSON (przykład)

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑01\nTotal: $1,234.56",
  "Regions": [
    {
      "BoundingBox": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Confidence": 0.98,
      "Text": "Invoice #12345"
    },
    {
      "BoundingBox": { "X": 10, "Y": 60, "Width": 150, "Height": 30 },
      "Confidence": 0.96,
      "Text": "Date: 2024‑03‑01"
    },
    {
      "BoundingBox": { "X": 10, "Y": 100, "Width": 180, "Height": 30 },
      "Confidence": 0.99,
      "Text": "Total: $1,234.56"
    }
  ]
}
```

*Uwaga:* Konkretne liczby będą się różnić w zależności od obrazu, ale struktura pozostaje taka sama — idealna do wprowadzania do API, baz danych lub wizualizatorów front‑endu.

## Pełny tutorial C# OCR – Wszystkie kroki razem

Poniżej znajduje się kompletny, gotowy do kopiowania i wklejania program, który łączy wszystkie elementy. Brak brakujących części, brak skrótów typu „zobacz dokumentację”.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the image you want to process
        // -------------------------------------------------
        string imagePath = @"C:\MyProject\Images\input.jpg";
        var ocrImage = OcrImage.FromFile(imagePath);

        // -------------------------------------------------
        // Step 2: Create and configure the OCR engine
        // -------------------------------------------------
        using var ocrEngine = new OcrEngine();
        // Example: ocrEngine.Language = Language.English; // optional

        // -------------------------------------------------
        // Step 3: Perform OCR recognition
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // -------------------------------------------------
        // Step 4: Serialize the result to indented JSON
        // -------------------------------------------------
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // -------------------------------------------------
        // Step 5: Write the JSON to a file
        // -------------------------------------------------
        string jsonOutputPath = @"C:\MyProject\Output\output.json";
        File.WriteAllText(jsonOutputPath, json);

        // -------------------------------------------------
        // Step 6: Let the user know we’re done
        // -------------------------------------------------
        Console.WriteLine("OCR data saved as JSON.");
    }
}
```

### Uruchamianie kodu

1. Zastąp dwie ścieżki `@"C:\MyProject\…"` swoimi rzeczywistymi katalogami.  
2. Zbuduj projekt (`dotnet build`) i uruchom go (`dotnet run`).  
3. Otwórz `output.json` — powinieneś zobaczyć ładnie ustrukturyzowaną reprezentację tekstu z obrazu.

## Częste pytania i przypadki brzegowe

**Co jeśli mój obraz jest rozmyty?**  
Aspose.OCR oferuje opcje wstępnego przetwarzania, takie jak `ocrEngine.ImagePreprocessOptions.Deskew = true;`. Włącz je przed wywołaniem `Recognize`, aby poprawić dokładność.

**Czy mogę ograniczyć wynik tylko do czystego tekstu?**  
Oczywiście — po prostu serializuj `ocrResult.Text` zamiast całego obiektu:

```csharp
string plainJson = JsonSerializer.Serialize(
    new { Text = ocrResult.Text },
    new JsonSerializerOptions { WriteIndented = true });
```

**Czy muszę obsługiwać wielostronicowe PDF-y?**  
Przykład koncentruje się na pojedynczym obrazie, ale możesz iterować po każdym obrazie strony, wykonać te same kroki i zebrać wyniki w tablicę JSON.

## Porady i pułapki

- **Ścieżki plików:** Używaj `Path.Combine`, aby uniknąć twardo zakodowanych backslashy, szczególnie jeśli kiedykolwiek przejdziesz na Linux.  
- **Pamięć:** Przy ogromnych partiach, ponownie używaj jednej instancji `OcrEngine` zamiast tworzyć nową dla każdego obrazu.  
- **Rozmiar JSON:** Jeśli potrzebujesz tylko tekstu, usuń właściwość `Regions`, aby utrzymać ładunek mały.  
- **Sprawdzenie wersji:** Ten tutorial został przetestowany z Aspose.OCR 23.9.0; nowsze wersje zachowują tę samą powierzchnię API, ale zawsze sprawdzaj notatki wydania pod kątem zmian łamiących.

![Przykładowy wynik OCR JSON – aspose ocr example](https://example.com/sample-ocr-json.png "Podgląd JSON aspose ocr example")

## Podsumowanie

Przeszliśmy przez kompletny **aspose ocr example**, który odczytuje obraz, wyodrębnia jego tekst i zapisuje wynik do pliku JSON przy użyciu czystego C#. Rozwiązanie jest samodzielne, gotowe do produkcji i łatwe do rozszerzenia — niezależnie od tego, czy chcesz dodać obsługę języków, dostosować progi pewności, czy przekazać JSON do usługi downstream.

Jeśli szukasz kolejnego kroku, spróbuj połączyć ten tutorial z **C# OCR tutorial**, który przesyła JSON do Azure Cognitive Search, lub poeksperymentuj z wyodrębnianiem tabel z faktur. Nie ma ograniczeń, gdy masz już JSON w ręku.

Masz własny pomysł, którym chcesz się podzielić? Dodaj komentarz, fork repozytorium lub napisz do mnie na GitHubie. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}