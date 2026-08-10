---
category: general
date: 2026-03-02
description: Dowiedz się, jak zapisać JSON podczas wyodrębniania tekstu z obrazu przy
  użyciu Aspose OCR. Zawiera kod zapisu pliku JSON, wskazówki dotyczące ładowania
  obrazu bitmapowego oraz pełny przykład w C#.
draft: false
keywords:
- how to save json
- extract text from image
- write json file
- how to extract text
- load bitmap image
language: pl
og_description: Odkryj, jak zapisać JSON podczas wyodrębniania tekstu z obrazu za
  pomocą Aspose OCR. Pełny kod C#, kroki zapisu pliku JSON oraz praktyczne wskazówki.
og_title: Jak zapisać JSON z OCR w C# – Pełny poradnik programistyczny
tags:
- C#
- OCR
- Aspose
- JSON
title: Jak zapisać JSON z OCR w C# – Kompletny przewodnik krok po kroku
url: /pl/net/ocr-configuration/how-to-save-json-from-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zapisać JSON z OCR w C# – Kompletny przewodnik krok po kroku

Zastanawiałeś się kiedyś **jak zapisać JSON**, który zawiera tekst właśnie wyciągnięty z obrazu? Nie jesteś jedyny. Wielu programistów napotyka problem, gdy muszą *wyodrębnić tekst z obrazu* i następnie zachować te informacje w starannie sformatowanym pliku JSON. Dobra wiadomość? Rozwiązanie jest dość proste, gdy masz odpowiednie elementy.

W tym samouczku przeprowadzimy Cię przez realistyczny scenariusz: użycie Aspose.OCR do **wyodrębnienia tekstu z obrazu**, następnie **zapisania pliku JSON**, a w końcu **zapisania JSON** na dysku. Po drodze pokażemy, jak **załadować obraz bitmapowy** poprawnie oraz omówimy kilka przypadków brzegowych, na które możesz natrafić. Na koniec będziesz mieć samodzielną aplikację konsolową C#, która robi wszystko – od wczytania obrazu po wygenerowanie gotowego dokumentu JSON.

## Czego będziesz potrzebować

- .NET 6.0 lub nowszy (kod działa również z .NET Core i .NET Framework)
- Aspose.OCR dla .NET (możesz pobrać darmowy pakiet próbny z NuGet)
- Przykładowy obraz PNG lub JPG zawierający tekst w języku angielskim
- Visual Studio, VS Code lub dowolne IDE obsługujące C#

Nie są wymagane dodatkowe biblioteki – wystarczy standardowa przestrzeń nazw `System.Drawing` do obsługi bitmap oraz `System.Text.Json` do serializacji.

---

## Krok 1 – Załaduj obraz bitmapowy (część „load bitmap image”)

Zanim jakiekolwiek OCR może się odbyć, musisz wczytać obraz do pamięci jako `Bitmap`. Pomyśl o tym jak o otwarciu książki przed rozpoczęciem czytania jej stron.

```csharp
using System.Drawing;

// Replace the placeholder with the actual path to your image file
string imagePath = @"C:\Images\sample-page.png";

// Load the image – this is the “load bitmap image” step
Bitmap bitmapImage = new Bitmap(imagePath);
```

> **Pro tip:** Jeśli obraz jest duży, rozważ najpierw jego zmniejszenie, aby poprawić wydajność. Silnik OCR działa szybciej na obrazach poniżej 2 MB.

---

## Krok 2 – Skonfiguruj silnik Aspose OCR

Teraz, gdy bitmapa jest gotowa, potrzebujemy `OcrEngine`. Ten obiekt wie, jak **wyodrębnić tekst z obrazu** i opcjonalnie dostarczyć dane geometryczne, takie jak ramki ograniczające.

```csharp
using Aspose.OCR;

// Create the OCR engine with English language and enable bounding boxes
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,
    ExportBoundingBoxes = true // adds geometry info to the result
};
```

Dlaczego włączyć `ExportBoundingBoxes`? Jeśli kiedykolwiek będziesz musiał podświetlić słowa w interfejsie użytkownika, te współrzędne są bezcenne. Jeśli ich nie potrzebujesz, możesz ustawić flagę na `false`, a JSON będzie nieco mniejszy.

---

## Krok 3 – Wykonaj OCR i uzyskaj ustrukturyzowany wynik

Po skonfigurowaniu silnika następnym krokiem jest właściwa operacja **wyodrębniania tekstu**. Metoda `RecognizeToOcrResult` zwraca rozbudowany obiekt, który zawiera rozpoznany tekst, oceny pewności oraz opcjonalne dane układu.

```csharp
// Run OCR – this is the core “how to extract text” call
var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);
```

Zmienna `ocrResult` zawiera teraz wszystko, czego potrzebujesz. Jeśli przyjrzysz się jej w debugerze, zobaczysz hierarchię obiektów `Page`, `Paragraph`, `Line` i `Word`, z których każdy ma własną właściwość `Text`.

---

## Krok 4 – Serializuj wynik do sformatowanego ciągu JSON

Tutaj naprawdę zaczyna się magia **jak zapisać json**. Użyjemy `System.Text.Json`, ponieważ jest wbudowany, szybki i obsługuje ładne formatowanie od razu.

```csharp
using System.Text.Json;

// Serialize with indentation for readability
string jsonResult = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true }
);
```

Jeśli potrzebujesz innej konwencji nazewnictwa (np. camelCase), po prostu dodaj `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` do opcji.

---

## Krok 5 – Zapisz JSON na dysku (krok „write json file”)

Na koniec faktycznie **zapisujemy plik JSON** w systemie plików. To konkretna odpowiedź na pytanie **jak zapisać json** w środowisku C#.

```csharp
using System.IO;

// Choose where you want the JSON output
string jsonPath = @"C:\Images\sample-page.json";

// Save the JSON string – this completes the “how to save json” workflow
File.WriteAllText(jsonPath, jsonResult);
```

Po wykonaniu tej linii znajdziesz ładnie wcięty plik `sample-page.json` obok oryginalnego obrazu. Otwórz go w dowolnym edytorze tekstu lub przekaż do innej usługi – Twoje dane OCR są teraz przenośne.

---

## Krok 6 – Zweryfikuj wynik (Co powinieneś zobaczyć?)

Uruchomienie programu powinno wypisać krótkie potwierdzenie w konsoli:

```csharp
Console.WriteLine("OCR result saved as JSON.");
```

Otwórz wygenerowany plik JSON i zobaczysz coś w stylu:

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello, world!",
          "Words": [
            { "Text": "Hello,", "Confidence": 0.99 },
            { "Text": "world!", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Jeśli flaga `ExportBoundingBoxes` była ustawiona na true, każde słowo będzie również zawierało współrzędne `Rectangle`. To przydatne przy dalszej pracy nad UI.

---

## Często zadawane pytania i przypadki brzegowe

### Co zrobić, gdy ścieżka do obrazu jest nieprawidłowa?

Umieść wczytywanie bitmapy w bloku `try/catch` i wyświetl czytelny błąd:

```csharp
try
{
    Bitmap bitmapImage = new Bitmap(imagePath);
}
catch (FileNotFoundException)
{
    Console.Error.WriteLine($"Image not found: {imagePath}");
    return;
}
```

### Jak obsłużyć języki nie‑angielskie?

Po prostu zmień właściwość `Language`:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Aspose obsługuje ponad 50 języków, więc wybierz ten, który odpowiada Twojemu materiałowi źródłowemu.

### Czy muszę zwolnić obiekty `Bitmap`?

Tak. `Bitmap` implementuje `IDisposable`, więc otocz go instrukcją `using`, aby szybko zwolnić zasoby natywne.

```csharp
using (Bitmap bitmapImage = new Bitmap(imagePath))
{
    // OCR code here
}
```

### Co zrobić, gdy chcę zwarty JSON bez wcięć?

Zamień opcje `JsonSerializerOptions`:

```csharp
new JsonSerializerOptions { WriteIndented = false }
```

To zmniejsza rozmiar pliku – przydatne w scenariuszach o ograniczonej przepustowości.

---

## Pełny działający przykład (gotowy do kopiowania i wklejenia)

Poniżej znajduje się kompletny program, który łączy wszystkie kroki, obsługę błędów i najlepsze praktyki omówione powyżej. Zapisz go jako `Program.cs` i uruchom z wiersza poleceń lub w swoim IDE.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1 – Load the bitmap image (load bitmap image)
        // -------------------------------------------------
        string imagePath = @"C:\Images\page.png";
        string jsonPath  = @"C:\Images\page.json";

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Error: Image file not found at {imagePath}");
            return;
        }

        using Bitmap bitmapImage = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2 – Configure the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ExportBoundingBoxes = true // optional, adds geometry info
        };

        // -------------------------------------------------
        // Step 3 – Perform OCR (how to extract text)
        // -------------------------------------------------
        var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);

        // -------------------------------------------------
        // Step 4 – Serialize to JSON (how to save json)
        // -------------------------------------------------
        string jsonResult = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true }
        );

        // -------------------------------------------------
        // Step 5 – Write JSON file (write json file)
        // -------------------------------------------------
        try
        {
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"OCR result saved as JSON at {jsonPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to write JSON file: {ex.Message}");
        }
    }
}
```

**Co robi ten kod:**  
1. Sprawdza, czy obraz istnieje.  
2. Ładuje go bezpiecznie w bloku `using`.  
3. Uruchamia OCR, aby **wyodrębnić tekst z obrazu**.  
4. Serializuje wynik do ładnie wciętego ciągu JSON.  
5. Zapisuje ten ciąg na dysku, odpowiadając na kluczowe pytanie **jak zapisać json**.

Uruchom `dotnet run` (lub naciśnij F5 w Visual Studio) i zobaczysz komunikat potwierdzający po zapisaniu pliku.

---

## Zakończenie

Masz teraz kompletny, gotowy do produkcji przepis na **jak zapisać JSON** pochodzący z wyodrębniania tekstu opartego na OCR. Od załadowania obrazu bitmapowego po zapis czystego pliku JSON, każdy krok został wyjaśniony wraz z „dlaczego” stojącym za kodem, dzięki czemu możesz dostosować rozwiązanie do własnych projektów.

Jeśli ciekawi Cię kolejny krok, rozważ:

- **Jak wyodrębnić tekst** z plików PDF, najpierw konwertując każdą stronę na obraz.  
- Wykorzystanie danych o ramkach ograniczających do podświetlania słów w UI WPF lub WinForms.  
- Strumieniowanie JSON bezpośrednio do API internetowego zamiast zapisywania pliku (użyj `HttpClient`).

Wypróbuj, dostosuj opcje i niech dane OCR napędzają każdą aplikację, którą tworzysz. Masz pytania? zostaw komentarz i powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}