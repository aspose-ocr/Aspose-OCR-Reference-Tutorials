---
category: general
date: 2026-04-06
description: Rozpoznawaj tekst na obrazie przy użyciu Aspose OCR w C#. Dowiedz się,
  jak wyodrębnić tekst, wczytać plik obrazu w C# i zapisać JSON w C# w prostym przykładzie
  krok po kroku.
draft: false
keywords:
- recognize image text
- how to extract text
- write json in c#
- load image file c#
language: pl
og_description: Rozpoznawaj tekst na obrazie za pomocą Aspose OCR w C#. Ten przewodnik
  pokazuje, jak wyodrębnić tekst, załadować plik obrazu w C# i szybko zapisać JSON
  w C#.
og_title: Rozpoznawanie tekstu na obrazie w C# – Kompletny przewodnik krok po kroku
tags:
- OCR
- C#
- Aspose
title: Rozpoznawanie tekstu z obrazu w C# – Kompletny przewodnik z eksportem JSON
url: /pl/net/text-recognition/recognize-image-text-in-c-full-guide-with-json-export/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznawanie tekstu na obrazie w C# – Kompletny przewodnik krok po kroku

Kiedykolwiek potrzebowałeś **rozpoznać tekst na obrazie** ze zeskanowanego paragonu, ale nie wiedziałeś, której biblioteki użyć? Nie jesteś sam. W wielu rzeczywistych aplikacjach — monitorach wydatków, przetwarzaniu faktur, a nawet narzędziach dostępności — wyciągnięcie słów z obrazu to pierwsza przeszkoda.  

W tym tutorialu przeprowadzimy Cię przez praktyczne rozwiązanie, które **rozpoznaje tekst na obrazie** przy użyciu biblioteki Aspose OCR, pokazuje **jak wyodrębnić tekst**, demonstruje **ładowanie pliku obrazu c#** poprawnie oraz w końcu **zapisuje json w c#**, abyś mógł przechowywać lub przesyłać wyniki. Po zakończeniu będziesz mieć gotową do uruchomienia aplikację konsolową, która zamieni dowolny PNG w schludny ładunek JSON.

---

## Czego będziesz potrzebować

- **.NET 6+** (kod działa także z .NET Framework 4.8, ale .NET 6 to optymalne rozwiązanie).
- Pakiet NuGet **Aspose.OCR for .NET**. Zainstaluj go poleceniem `dotnet add package Aspose.OCR`.
- Przykładowy obraz (`input.png`) umieszczony w miejscu, które aplikacja może odczytać.  
- Visual Studio 2022 lub dowolny edytor, którego używasz — nie są potrzebne żadne zaawansowane sztuczki IDE.

> Pro tip: Trzymaj pliki obrazów w folderze o nazwie `Resources` wewnątrz projektu; ułatwia to zarządzanie ścieżkami i zapobiega problemom „plik nie znaleziony”.

---

## Krok 1: rozpoznawanie tekstu na obrazie – Ładowanie pliku obrazu

Zanim silnik OCR wykona swoją magię, musisz **ładować plik obrazu c#** w bezpieczny sposób. Metoda `Image.FromFile` rzuca wyjątek, jeśli ścieżka jest nieprawidłowa lub plik nie jest obsługiwanym formatem, więc zabezpieczymy się przed tym.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // Verify the image exists
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // Load the image – this is the “load image file c#” step
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // Continue to OCR...
        }
    }
}
```

*Dlaczego to ważne*: Ładowanie obrazu wewnątrz bloku `using` zapewnia szybkie zwolnienie niezarządzanych zasobów GDI+, co zapobiega wyciekom pamięci w długotrwale działających usługach.

---

## Krok 2: Jak wyodrębnić tekst przy użyciu Aspose OCR

Teraz, gdy bitmapa znajduje się w pamięci, przekazujemy ją silnikowi **rozpoznawania tekstu na obrazie**. `OcrEngine` od Aspose jest prosty: tworzysz instancję, wywołujesz `Recognize` i otrzymujesz obiekt `OcrResult`, który zawiera surowy tekst, wyniki pewności oraz nawet ramki ograniczające.

```csharp
// Inside the using block from Step 1
var ocrEngine = new OcrEngine();

// Perform OCR – this is the core “how to extract text” operation
OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

// Quick sanity check
if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
{
    Console.WriteLine("⚠️ No text detected. Try a clearer image.");
    return;
}
Console.WriteLine("✅ OCR succeeded. Extracted text:");
Console.WriteLine(ocrResult.Text);
```

*Wyjaśnienie*: Metoda `Recognize` uruchamia wbudowaną sieć neuronową. Działa najlepiej przy obrazach o wysokim kontraście i rozdzielczości 300 DPI. Jeśli podasz rozmyte zdjęcie, wskaźnik pewności spadnie — rozważ wstępne przetwarzanie (prostowanie, binaryzacja) w kodzie produkcyjnym.

---

## Krok 3: Zapisz JSON w C# – Eksport wyniku OCR

Większość API oczekuje JSON, więc **zapiszemy json w c#** używając `JsonExport` z Aspose. Biblioteka serializuje cały `OcrResult`, zachowując informacje o liniach i wartościach pewności.

```csharp
// Still inside the same using block
string jsonResult = JsonExport.ToJson(ocrResult);

// Persist the JSON to disk
File.WriteAllText(outputPath, jsonResult);
Console.WriteLine($"💾 JSON written to {outputPath}");
```

### Oczekiwany wynik JSON

```json
{
  "Text": "Total: $12.34\r\nDate: 2026-04-01\r\n...",
  "Words": [
    { "Text": "Total", "Confidence": 0.98, "Rectangle": { "X": 10, "Y": 15, "Width": 50, "Height": 12 } },
    { "Text": "$12.34", "Confidence": 0.96, "Rectangle": { "X": 70, "Y": 15, "Width": 45, "Height": 12 } }
    // … more words …
  ]
}
```

*Dlaczego JSON?* Jest językowo neutralny, łatwy do deserializacji i zachowuje szczegółowe metadane OCR, które mogą być potrzebne przy dalszej walidacji.

---

## Krok 4: Pełny, uruchamialny program

Łącząc wszystkie elementy, oto kompletny program konsolowy. Skopiuj‑wklej, przywróć pakiety NuGet i naciśnij **F5**.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Configuration – adjust these paths as needed
        // -------------------------------------------------
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // -------------------------------------------------
        // Validate input file
        // -------------------------------------------------
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // -------------------------------------------------
        // Load image (load image file c#)
        // -------------------------------------------------
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // -------------------------------------------------
            // Initialize OCR engine and recognize text
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("⚠️ No text detected. Try a clearer image.");
                return;
            }

            Console.WriteLine("✅ OCR succeeded. Sample output:");
            Console.WriteLine(ocrResult.Text.Substring(0, Math.Min(100, ocrResult.Text.Length)) + "...");

            // -------------------------------------------------
            // Convert result to JSON (write json in c#)
            // -------------------------------------------------
            string jsonResult = JsonExport.ToJson(ocrResult);
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"💾 JSON written to {outputPath}");
        }
    }
}
```

Uruchom program i otwórz `Resources/output.json` — powinieneś zobaczyć ładnie sformatowaną reprezentację JSON wszystkiego, co silnik rozpoznał.

---

## Obsługa typowych przypadków brzegowych

| Sytuacja | Co zrobić | Dlaczego |
|-----------|------------|-----|
| **Obraz jest null lub uszkodzony** | Owiń `Image.FromFile` w `try/catch` i zaloguj wyjątek. | Zapobiega awarii aplikacji i dostarcza czytelny komunikat o błędzie. |
| **Niskie wyniki pewności** | Sprawdź `ocrResult.Words[i].Confidence`. Jeśli jest poniżej 0.75, rozważ wstępne przetwarzanie (zwiększ DPI, wyostrz). | Poprawia niezawodność w procesach downstream, takich jak wyodrębnianie kwot. |
| **Duże pliki (>10 MB)** | Zmniejsz skalę obrazu przed OCR (`receiptImage = new Bitmap(receiptImage, new Size(width/2, height/2))`). | Redukuje obciążenie pamięci i przyspiesza rozpoznawanie. |
| **Dokumenty wielojęzyczne** | Ustaw `ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;` | Umożliwia silnikowi wykrywanie znaków z obu języków. |

---

## Bonus: Wizualizacja wyniku OCR (opcjonalnie)

Jeśli chcesz zobaczyć, gdzie każde słowo znajduje się na obrazie, możesz narysować ramki ograniczające:

```csharp
using (Graphics g = Graphics.FromImage(receiptImage))
{
    foreach (var word in ocrResult.Words)
    {
        var rect = new Rectangle(word.Rectangle.X, word.Rectangle.Y,
                                 word.Rectangle.Width, word.Rectangle.Height);
        g.DrawRectangle(Pens.Red, rect);
    }
    receiptImage.Save(Path.Combine("Resources", "annotated.png"));
}
```

Wynikowy `annotated.png` pokaże czerwone prostokąty wokół każdego rozpoznanego słowa — przydatne przy debugowaniu.

---

## Zakończenie

Właśnie **rozpoznaliśmy tekst na obrazie** w C# od początku do końca: ładowanie pliku obrazu, wywołanie Aspose OCR aby **jak wyodrębnić tekst**, i w końcu **zapisaliśmy json w c#**, aby dane mogły trafić w dowolne miejsce. Pełny przykład działa od razu, a dodatkowe wskazówki pomogą Ci radzić sobie z rozmytymi paragonami, dużymi plikami czy skanami wielojęzycznymi.

Co dalej? Spróbuj zamienić Aspose na inny silnik (Tesseract, Microsoft OCR) i porównać wyniki pewności, albo wprowadź JSON do bazy danych do raportowania wydatków. Możesz także rozbudować aplikację konsolową do ASP .NET Core Web API, które przyjmuje przesyłane obrazy i natychmiast zwraca JSON.

Masz pytania o skalowanie, obsługę błędów lub integrację z Azure Functions? Zostaw komentarz lub napisz do mnie na GitHubie. Szczęśliwego kodowania i niech Twój OCR zawsze będzie wyraźny! 

---

![Zrzut ekranu wyniku OCR w formacie JSON – przykład rozpoznawania tekstu na obrazie](https://example.com/ocr-example.png "przykład rozpoznawania tekstu na obrazie")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}