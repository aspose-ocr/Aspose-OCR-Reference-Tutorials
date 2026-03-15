---
category: general
date: 2026-03-15
description: Jak używać Aspose OCR do wyodrębniania tekstu z obrazów i konwertowania
  obrazu na JSON w C#. Dowiedz się, jak rozpoznawać tekst z plików PNG i szybko uzyskać
  ustrukturyzowany wynik.
draft: false
keywords:
- how to use aspose
- convert image to json
- extract text from image
- recognize text from png
- how to extract ocr
language: pl
og_description: Jak używać Aspose OCR do wyodrębniania tekstu z obrazów i konwertowania
  obrazu na JSON w C#. Ten przewodnik prowadzi Cię krok po kroku przez rozpoznawanie
  tekstu z plików PNG i uzyskiwanie strukturalnego wyniku.
og_title: Jak używać Aspose OCR do konwersji obrazu na JSON
tags:
- Aspose
- OCR
- C#
- JSON
title: Jak używać Aspose OCR do konwertowania obrazu na JSON
url: /pl/net/text-recognition/how-to-use-aspose-ocr-to-convert-image-to-json/
---

.

Let's assemble.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać Aspose OCR do konwertowania obrazu na JSON

Jak używać Aspose OCR to częste pytanie, gdy programiści muszą wyodrębnić tekst ze zdjęć. Jeśli chcesz **convert image to JSON** lub **recognize text from PNG**, ten przewodnik ma wszystko, czego potrzebujesz — bez zbędnych informacji, tylko praktyczne, kompleksowe rozwiązanie.

W ciągu kilku minut przeprowadzimy Cię przez wszystko, czego potrzebujesz: instalację biblioteki, konfigurację silnika do wyjścia w formacie JSON, wczytanie pliku PNG z paragonem, uruchomienie OCR oraz zapisanie wyniku do pliku `.json`. Po zakończeniu będziesz w stanie **extract text from image** plików jednym wywołaniem metody i zrozumiesz, dlaczego każdy krok ma znaczenie.

> **Pro tip:** Aspose OCR działa z szeroką gamą formatów obrazów (PNG, JPEG, BMP, TIFF). Ten sam kod poniżej obsłuży je wszystkie, więc nie musisz pisać logiki specyficznej dla formatu.

## Czego będziesz potrzebować

- .NET 6.0 lub nowszy (kod działa również na .NET Framework 4.6+)  
- Ważny pakiet Aspose.OCR NuGet (bezpłatna wersja próbna lub licencjonowana)  
- Plik obrazu, który chcesz przetworzyć (np. `receipt.png`)  
- Visual Studio, VS Code lub dowolny edytor C#, którego preferujesz  

To wszystko — bez dodatkowych zależności, bez usług zewnętrznych. Gotowy? Zanurzmy się.

![how to use aspose OCR engine](image-placeholder.png "how to use aspose OCR engine")

## Jak używać Aspose OCR – Konfiguracja wyjścia JSON

Pierwszą rzeczą, którą musisz zrobić, gdy **how to use aspose** dla OCR, jest stworzenie instancji `OcrEngine` i ustawienie jej na emitowanie JSON. Ten mały przełącznik konfiguracyjny oszczędza Ci ręcznego serializowania wyniku później.

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that does the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell Aspose to give us JSON instead of plain text.
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Load the image you want to recognize.
        var inputImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // 4️⃣ Run the OCR process.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Save the JSON payload to disk.
        File.WriteAllText(@"YOUR_DIRECTORY/receipt.json", ocrResult.Text);

        // 6️⃣ Let the developer know we’re done.
        Console.WriteLine("JSON saved.");
    }
}
```

**Why this matters:** Ustawienie `OutputFormat` na `Json` oznacza, że silnik OCR już strukturyzuje tekst w hierarchię stron, linii i słów. Nie musisz później parsować surowych ciągów, co sprawia, że przetwarzanie dalsze — np. wprowadzanie danych do bazy danych — jest znacznie czystsze.

## Konwertuj obraz na JSON przy użyciu Aspose OCR

Teraz, gdy silnik jest skonfigurowany, porozmawiajmy o części **convert image to JSON** bardziej szczegółowo.

1. **Load the image** – `Image.FromFile` działa dla każdego obsługiwanego formatu. Jeśli pracujesz ze strumieniem (np. przesłanym plikiem), możesz użyć `Image.FromStream`.  
2. **Run `Recognize`** – ta metoda zwraca obiekt `OcrResult`. Ponieważ ustawiliśmy wyjście na JSON, `ocrResult.Text` już zawiera ciąg JSON.  
3. **Write the file** – `File.WriteAllText` jest najprostszym sposobem na zapisanie JSON. Jeśli musisz przechowywać go w chmurze, po prostu zamień tę linię na odpowiednie wywołanie SDK.

### Oczekiwany wynik JSON

Typowy ładunek JSON wygląda tak (przycięty dla zwięzłości):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Words": [
            { "Text": "Total", "Confidence": 0.99 },
            { "Text": "$12.34", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Możesz teraz przekazać tę strukturę do dowolnego systemu downstream — czy to narzędzia raportującego, modelu uczenia maszynowego, czy prostego pliku logu.

## Wyodrębnij tekst z obrazu przy użyciu Aspose OCR

Jeśli potrzebujesz tylko surowego ciągu (tj. nie zależy Ci na JSON), po prostu przełącz format wyjścia z powrotem na zwykły tekst:

```csharp
ocrEngine.Configuration.OutputFormat = OutputFormat.PlainText;
var plainResult = ocrEngine.Recognize(inputImage);
Console.WriteLine(plainResult.Text);
```

**When to choose plain text?**  
- Szybkie debugowanie lub wyjście w konsoli.  
- Scenariusze, w których zastosujesz własne przetwarzanie po‑OCR (np. wyodrębnianie przy pomocy wyrażeń regularnych).

Jednak pamiętaj, że **extract text from image** przy użyciu JSON dostarcza danych pozycyjnych — przydatnych do podświetlania tekstu w interfejsie UI lub dopasowywania do pól formularza.

## Rozpoznawaj tekst z plików PNG

PNG jest formatem bezstratnym, co często daje lepszą dokładność OCR w porównaniu do mocno skompresowanych JPEG‑ów. Oto szybka lista kontrolna, aby zapewnić najlepsze wyniki przy **recognize text from PNG**:

| Pozycja listy kontrolnej | Dlaczego to pomaga |
|--------------------------|--------------------|
| Użyj DPI 300+ | Wyższa rozdzielczość daje silnikowi więcej pikseli do pracy. |
| Utrzymaj obraz w odcieniach szarości | Redukuje szumy; Aspose OCR automatycznie konwertuje, ale wstępne przetwarzanie może przyspieszyć działanie. |
| Usuń niepotrzebne elementy tła | Czyste tło poprawia wyniki pewności. |

Jeśli napotkasz niskie wyniki pewności, spróbuj zwiększyć DPI lub zastosować prosty filtr progowy przed przekazaniem obrazu do Aspose.

## Jak wyodrębnić wyniki OCR programowo

Poza samym zapisem JSON, możesz chcieć programowo odczytać konkretne pola — np. całkowitą kwotę na paragonie. Ponieważ JSON zawiera hierarchię, możesz go zdeserializować do obiektu C#:

```csharp
using System.Text.Json;

// Assuming ocrResult.Text contains the JSON string
var ocrData = JsonSerializer.Deserialize<OcrResponse>(ocrResult.Text);

// Example class definitions (simplified)
public class OcrResponse
{
    public Page[] Pages { get; set; }
}
public class Page
{
    public int PageNumber { get; set; }
    public Line[] Lines { get; set; }
}
public class Line
{
    public Word[] Words { get; set; }
}
public class Word
{
    public string Text { get; set; }
    public double Confidence { get; set; }
}
```

Teraz możesz zapytać `ocrData` przy użyciu LINQ:

```csharp
var totalLine = ocrData.Pages
    .SelectMany(p => p.Lines)
    .FirstOrDefault(l => l.Words.Any(w => w.Text.Equals("Total", StringComparison.OrdinalIgnoreCase)));

if (totalLine != null)
{
    var amount = totalLine.Words
        .FirstOrDefault(w => w.Text.StartsWith("$"))
        ?.Text;
    Console.WriteLine($"Extracted amount: {amount}");
}
```

**Why this works:** JSON już informuje, gdzie każde słowo znajduje się na stronie, więc możesz niezawodnie zlokalizować pola, nawet jeśli układ nieco się zmieni.

## Przypadki brzegowe i typowe pułapki

- **Null Result:** Jeśli `ocrEngine.Recognize` zwraca `null`, obraz może być nieobsługiwany lub uszkodzony. Zawsze zabezpiecz się przed tym:

  ```csharp
  var ocrResult = ocrEngine.Recognize(inputImage);
  if (ocrResult == null) throw new InvalidOperationException("OCR failed – check the image path.");
  ```

- **Large Files:** W przypadku obrazów wielokrotnych megabajtów rozważ strumieniowanie obrazu lub zmianę jego rozmiaru przed OCR, aby uniknąć nadmiernego zużycia pamięci.

- **License Issues:** Wersja próbna dodaje znak wodny do wyniku. Upewnij się, że wczytujesz licencję na początku programu:

  ```csharp
  Aspose.OCR.License license = new Aspose.OCR.License();
  license.SetLicense("Aspose.OCR.lic");
  ```

- **Non‑Latin Scripts:** Aspose OCR obsługuje wiele języków, ale musisz odpowiednio ustawić właściwość `Language` (np. `ocrEngine.Configuration.Language = Language.English;`).

## Pełny działający przykład (gotowy do kopiowania i wklejania)

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Load your Aspose license (optional for trial)
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set output to JSON – this is the key step for convert image to JSON
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Optional: improve accuracy for PNG files
        ocrEngine.Configuration.Dpi = 300; // higher DPI = better results

        // 4️⃣ Load the image you want to process
        var inputImagePath = @"YOUR_DIRECTORY/receipt.png";
        if (!File.Exists(inputImagePath))
            throw new FileNotFoundException($"Image not found: {inputImagePath}");

        var inputImage = Image.FromFile(inputImagePath);

        // 5️⃣ Run OCR – this is where we actually extract text from image
        var ocrResult = ocrEngine.Recognize(inputImage);
        if (ocrResult == null)
            throw new InvalidOperationException("OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}