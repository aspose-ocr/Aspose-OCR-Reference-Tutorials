---
category: general
date: 2026-01-15
description: Konwertuj obraz na JSON przy użyciu Aspose OCR w C#. Dowiedz się, jak
  wyodrębnić tekst z obrazu, uzyskać ramki ograniczające w formacie JSON i rozpoznać
  obraz paragonu.
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: pl
og_description: Konwertuj obraz na JSON przy użyciu Aspose OCR w C#. Przewodnik krok
  po kroku, jak wyodrębnić tekst z obrazu, rozpoznać paragon i uzyskać ramki ograniczające
  w formacie JSON.
og_title: Konwertuj obraz na JSON przy użyciu Aspose OCR w C# – przewodnik
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: Konwertuj obraz na JSON przy użyciu Aspose OCR C# – przewodnik
url: /pl/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwertowanie obrazu do JSON przy użyciu Aspose OCR C# – przewodnik

Kiedykolwiek potrzebowałeś **konwertować obraz do JSON**, ale nie byłeś pewien, która biblioteka może dostarczyć zarówno surowy tekst, jak i dokładne współrzędne słów? Nie jesteś sam. Wielu programistów napotyka ten problem, gdy próbują wyodrębnić tekst z plików graficznych — szczególnie paragonów — jednocześnie potrzebując maszynowo czytelnego ładunku JSON do dalszego przetwarzania.

W tym samouczku przeprowadzimy Cię przez kompletny **przykład Aspose OCR C#**, który pokaże, jak wyodrębnić tekst z obrazu, rozpoznać obraz paragonu i wygenerować **JSON bounding boxes** dla każdego słowa. Po zakończeniu będziesz mieć gotową do uruchomienia aplikację konsolową, która wypisze ładnie sformatowany ciąg JSON, który możesz przekazać do dowolnego API, bazy danych lub potoku analitycznego.

> **Co zyskasz**  
> • W pełni funkcjonalny projekt C#, który **konwertuje obraz do JSON**  
> • Wgląd w to, dlaczego włączamy `IncludeBoundingBoxes` (to klucz do `json bounding boxes`)  
> • Wskazówki dotyczące obsługi różnych formatów obrazów i języków  

Zaczynajmy.

---

## Czego będziesz potrzebować

Zanim zanurzymy się w kod, upewnij się, że masz zainstalowane następujące wymagania wstępne:

- **.NET 6.0 SDK** (lub nowszą wersję) – kod jest skierowany do .NET 6, ale działa również na .NET Framework 4.7+.
- **Aspose.OCR for .NET** pakiet NuGet – możesz go pobrać za pomocą `dotnet add package Aspose.OCR`.
- Przykładowy obraz paragonu (`receipt.jpg`) umieszczony w folderze, który możesz odwołać w swoim projekcie.
- Visual Studio 2022, VS Code lub dowolne IDE, które preferujesz.

Nie są wymagane żadne inne usługi zewnętrzne; wszystko działa lokalnie.

---

## Konwertowanie obrazu do JSON – przegląd

Podstawowa idea jest prosta: załaduj obraz, powiedz Aspose OCR, aby rozpoznał język angielski (lub dowolny obsługiwany język), poproś o dołączenie bounding boxes i na końcu poproś o wynik w formacie **JSON**. Biblioteka wykonuje całą ciężką pracę — OCR, analizę układu i serializację JSON.

Oto diagram wysokiego poziomu przepływu (wyobraź sobie mały obrazek):

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

Ten mały diagram przedstawia cały pipeline, który zaimplementujemy.

---

## Krok 1: Skonfiguruj projekt i zainstaluj Aspose OCR

Najpierw utwórz nowy projekt konsolowy i dodaj pakiet Aspose OCR.

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Jeśli używasz Visual Studio, kliknij prawym przyciskiem projektu → *Manage NuGet Packages* → wyszukaj **Aspose.OCR** i zainstaluj najnowszą stabilną wersję (obecnie 23.12).

---

## Krok 2: Załaduj obraz, który chcesz rozpoznać

Użyjemy metody `OcrImage.FromFile`, aby odczytać obraz paragonu. Upewnij się, że ścieżka wskazuje na istniejący plik; w przeciwnym razie otrzymasz `FileNotFoundException`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Jeśli Twój obraz znajduje się obok pliku `.csproj`, możesz po prostu użyć `"receipt.jpg"`.

---

## Krok 3: Skonfiguruj opcje OCR dla JSON Bounding Boxes

Magia dzieje się, gdy włączymy `OutputFormat = OutputFormat.Json` **oraz** `IncludeBoundingBoxes = true`. Pierwsze mówi Aspose, aby serializował wynik jako JSON, a drugie dodaje `x`, `y`, `width` i `height` dla każdego słowa — dokładnie to, czego potrzebujesz do `json bounding boxes`.

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

Możesz również dostosować `ocrOptions.Dpi` lub `ocrOptions.Language`, jeśli potrzebujesz wyższej rozdzielczości lub innego języka.

---

## Krok 4: Wykonaj rozpoznawanie – wyodrębnij tekst z obrazu

Teraz wywołujemy `Recognize`. Metoda zwraca obiekt `OcrResult`, który zawiera ciąg JSON, surowy tekst i więcej.

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

Jeśli musisz obsłużyć inne języki, zamień `Language.English` na `Language.Spanish`, `Language.French` itp. Aspose obsługuje ponad 30 języków od razu.

---

## Krok 5: Wyświetl wynik – Twój ładunek JSON

Na koniec wypisujemy JSON w konsoli. W prawdziwej aplikacji prawdopodobnie zapiszesz go do pliku lub wyślesz do usługi.

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

Uruchomienie programu powinno wygenerować dokument JSON podobny do poniższego fragmentu.

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

Zauważ, że każde słowo ma teraz **JSON bounding box** — idealne do przekazania do nakładki UI lub parsera downstream.

---

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do skopiowania program. Bez ukrytych części, bez wywołań zewnętrznych — po prostu czysty C#.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **Uwaga:**  
> • **Błędy ścieżki pliku** – sprawdź podwójnie lokalizację obrazu.  
> • **Brak pakietu NuGet** – upewnij się, że `Aspose.OCR` jest odwołany.  
> • **Nieobsługiwane formaty obrazów** – trzymaj się JPEG, PNG, BMP lub TIFF dla najlepszych rezultatów.

---

## Częste pytania i przypadki brzegowe

### Czy mogę konwertować **stronę PDF** do JSON zamiast JPEG?

Tak. Najpierw skonwertuj stronę PDF na obraz (np. używając `Aspose.PDF`), a następnie podaj ten obraz do tego samego pipeline OCR. Wyjście JSON będzie identyczne, ponieważ krok OCR zależy tylko od danych rastrowych.

### Co jeśli paragon jest rozmazany?

Zwiększ DPI w `ocrOptions`. Na przykład:

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

Wyższe DPI może zwiększyć zużycie pamięci, więc zrównoważ jakość i wydajność.

### Potrzebuję **wielu języków** na tym samym paragonie (np. angielski + hiszpański).

Możesz przekazać tablicę języków:

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

Aspose spróbuje rozpoznać każdy język w podanej kolejności.

### Jak zapisać JSON do pliku?

Po prostu zamień linię `Console.WriteLine` na:

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

Teraz masz trwały plik, który możesz przekazać do innych usług.

---

## Podsumowanie wizualne

![przykład konwersji obrazu do json](convert-image-to-json.png "przykład konwersji obrazu do json")

*Zrzut ekranu pokazuje wyjściowy JSON po uruchomieniu demonstracji.*

---

## Podsumowanie

Właśnie pokazaliśmy, jak **konwertować obraz do JSON** przy użyciu Aspose OCR w C#. Konfigurując `OutputFormat` i `IncludeBoundingBoxes`, możesz **wyodrębnić tekst z obrazu**, **rozpoznać obraz paragonu** i uzyskać precyzyjne **JSON bounding boxes** dla każdego słowa. Pełny, uruchamialny kod znajduje się w powyższym fragmencie, więc możesz go wkleić do dowolnego projektu .NET już teraz.

Co dalej? Spróbuj przekazać JSON do front‑endowego podglądu, który podświetla każde słowo, lub przesłać dane do modelu uczenia maszynowego, który klasyfikuje pozycje na paragonach. Możesz także eksperymentować z innymi językami, wyższymi ustawieniami DPI lub przetwarzaniem wsadowym wielu obrazów w pętli.

Jeśli napotkasz problemy, pamiętaj o wskazówkach dotyczących ścieżek plików, DPI i tablic języków. Śmiało zostaw komentarz lub otwórz issue w repozytorium GitHub, które utworzysz dla tej demonstracji. Szczęśliwego kodowania i ciesz się przekształcaniem obrazów w ustrukturyzowany JSON!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}