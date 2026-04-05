---
category: general
date: 2026-04-04
description: Dowiedz się, jak wyodrębniać tekst z plików TIFF przy użyciu przykładu
  silnika OCR w C#. Przewodnik krok po kroku z wyjściem w formacie JSON i XML.
draft: false
keywords:
- extract text from tiff
- ocr engine example
- Aspose OCR C#
- multi‑page TIFF OCR
- JSON OCR result
language: pl
og_description: Wyodrębnij tekst z plików TIFF przy użyciu silnika OCR – przykład
  w C#. Szczegółowe kroki, kompletny kod oraz wskazówki dotyczące wyjścia w formacie
  JSON/XML.
og_title: Wyodrębnij tekst z pliku TIFF przy użyciu silnika OCR Aspose – pełny przewodnik
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Wyodrębnianie tekstu z pliku TIFF przy użyciu silnika OCR Aspose – kompletny
  przykład
url: /pl/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-engine-complete-examp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnij tekst z TIFF – Pełny przykład silnika OCR w C#

Czy kiedykolwiek potrzebowałeś **wyodrębnić tekst z TIFF** obrazów, ale nie byłeś pewien, która biblioteka poradzi sobie z plikami wielostronicowymi bez mnóstwa obejść? Nie jesteś jedyny. W wielu starszych systemach dokumenty przychodzą jako skany wielostronicowych TIFF‑ów, a wyciągnięcie surowego tekstu jest niezbędną funkcją dla wyszukiwania, zgodności lub automatyzacji wprowadzania danych.

Dobre wieści? Z Aspose OCR możesz zrobić to w kilku linijkach — bez kombinowania z niskopoziomowymi buforami pikseli. Ten tutorial przeprowadzi Cię przez **kompletny przykład silnika OCR**, który ładuje wielostronicowy TIFF, rozpoznaje każdą stronę i wypisuje zarówno ładnie sformatowany JSON, jak i opcjonalny XML. Po zakończeniu będziesz mieć gotową do uruchomienia aplikację konsolową w C#, która wyodrębnia tekst z plików TIFF w kilka sekund.

## Czego się nauczysz

- Jak skonfigurować silnik Aspose OCR w projekcie .NET.  
- Dokładny kod potrzebny do **wyodrębnienia tekstu z TIFF** plików, w tym obsługa wielu stron.  
- Dlaczego możesz wybrać wyjście JSON zamiast XML i jak wygenerować oba formaty.  
- Wskazówki dotyczące rozwiązywania typowych problemów (np. DPI obrazu, zużycie pamięci).  

### Wymagania wstępne

- .NET 6.0 SDK lub nowszy (kod działa z .NET Core i .NET Framework).  
- Ważna licencja Aspose OCR (lub klucz wersji próbnej).  
- Visual Studio 2022 lub dowolny edytor C#, którego używasz.  
- Przykładowy wielostronicowy plik TIFF (nazwany `multi-page.tiff` w przykładzie).  

> **Pro tip:** Jeśli masz ograniczony budżet, wersja próbna nadal pozwala wyodrębnić tekst z maksymalnie 100 stron miesięcznie — idealne do testów.

---

## Krok 1 – Inicjalizacja silnika OCR (ocr engine example)

Zanim będziemy mogli **wyodrębnić tekst z TIFF**, potrzebujemy instancji silnika OCR. Ten obiekt przechowuje całą konfigurację, którą możesz później dostosować (język, rozdzielczość itp.).

```csharp
using Aspose.OCR;
using System.IO;

// Create a new OCR engine – this is the core of our ocr engine example
var ocrEngine = new OcrEngine();

// Optional: set language if you know the document’s language
// ocrEngine.Language = Language.English;
```

*Dlaczego to ważne:* Klasa `OcrEngine` ukrywa ciężką pracę. Utworzenie jej raz i ponowne użycie dla wielu obrazów jest bardziej efektywne pamięciowo niż tworzenie nowego silnika dla każdej strony.

---

## Krok 2 – Załaduj wielostronicowy TIFF (extract text from TIFF)

Teraz wskazujemy silnikowi nasz plik źródłowy. `ImageStream.FromFile` obsługuje TIFF, JPEG, PNG i wiele innych, ale w tym tutorialu skupiamy się na TIFF.

```csharp
// Load the multi‑page TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi-page.tiff");
```

> **Uwaga:** Zamień `YOUR_DIRECTORY` na rzeczywistą ścieżkę folderu na swoim komputerze.  
> **Wskazówka:** Jeśli Twój TIFF ma niskie DPI (poniżej 150), rozważ wstępne przetworzenie obrazu, aby poprawić dokładność OCR.

---

## Krok 3 – Rozpoznaj wszystkie strony

Wywołanie `Recognize()` uruchamia algorytm OCR na **każdej stronie** w TIFF. Obiekt wynikowy zawiera surowy tekst, oceny pewności i segmentację stron.

```csharp
// Run OCR on the loaded image – this extracts text from all pages
var ocrResult = ocrEngine.Recognize();
```

*Co otrzymujesz:* `ocrResult` zawiera kolekcję obiektów `PageResult`. Tekst każdej strony można odczytać przez `ocrResult.Pages[i].Text`. Silnik dostarcza także poziomy pewności, które mogą być przydatne przy kontroli jakości.

---

## Krok 4 – Zapisz wyniki jako JSON (i opcjonalny XML)

Większość nowoczesnych pipeline’ów preferuje JSON, ale starsze systemy wciąż korzystają z XML. Oto jak wygenerować oba formaty, ładnie sformatowane.

```csharp
// Convert the recognition result to pretty‑printed JSON
string jsonResult = ocrResult.ToJson(prettyPrint: true);
File.WriteAllText(@"YOUR_DIRECTORY/result.json", jsonResult);

// Optional: also output XML for older workflows
string xmlResult = ocrResult.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY/result.xml", xmlResult);
```

### Przykładowy wynik JSON (skrócony)

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
      "Confidence": 0.97
    },
    {
      "PageNumber": 2,
      "Text": "Itemized List\n1. Widget A – $500.00\n2. Widget B – $750.00",
      "Confidence": 0.95
    }
  ]
}
```

JSON jest czytelny dla człowieka, co ułatwia debugowanie. XML odzwierciedla tę samą strukturę, jeśli go potrzebujesz.

---

## Krok 5 – Zweryfikuj wyodrębnianie (extract text from TIFF)

Po zapisaniu plików szybka kontrola zapewnia, że nic nie poszło nie tak.

```csharp
// Load the JSON back just to confirm it was saved correctly
string loadedJson = File.ReadAllText(@"YOUR_DIRECTORY/result.json");
Console.WriteLine("First 200 characters of JSON output:");
Console.WriteLine(loadedJson.Substring(0, Math.Min(200, loadedJson.Length)));
```

Jeśli zobaczysz wydrukowany fragment, pomyślnie **wyodrębniłeś tekst z TIFF** i zapisałeś go. Od tego momentu możesz przekazać JSON do indeksu wyszukiwania, bazy danych lub dowolnej usługi downstream.

---

## Dlaczego warto używać Aspose OCR do wyodrębniania tekstu z TIFF?

- **Obsługa wielu stron od razu** – nie musisz ręcznie dzielić TIFF‑a.  
- **Wysoka dokładność** dzięki własnym modelom sieci neuronowych.  
- **Cross‑platform** – działa na Windows, Linux i macOS w środowiskach .NET.  
- **Bogate formaty wyjściowe** (JSON, XML, plain text), które pasują zarówno do nowoczesnych, jak i starszych stosów technologicznych.  

Jeśli nadal się wahasz, wypróbuj wersję próbną na przykładowym dokumencie. Zauważysz szybkość i prostotę w porównaniu z otwarto‑źródłowymi alternatywami, które często wymagają dodatkowego przetwarzania obrazu.

---

## Typowe problemy i jak ich unikać

| Problem | Objaw | Rozwiązanie |
|---------|-------|-------------|
| Niska rozdzielczość TIFF | Brakujące znaki, niska pewność | Zwiększ rozdzielczość obrazu do ≥150 DPI przed OCR (`ocrEngine.Image = ImageStream.FromFile(...).Resize(150)` ) |
| Nieprawidłowy język | Zniekształcone słowa, szczególnie w tekstach nie‑angielskich | Ustaw `ocrEngine.Language = Language.Spanish` (lub odpowiedni) przed `Recognize()` |
| Brak pamięci przy dużych plikach | `OutOfMemoryException` | Przetwarzaj strony w partiach: iteruj po `ocrEngine.Image.Pages` i wywołuj `RecognizePage(i)` |
| Licencja nie została zastosowana | Znak wodny „Evaluation” w wyniku | Zarejestruj licencję: `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Pełny działający przykład (gotowy do kopiowania)

Poniżej znajduje się kompletny program, który możesz wkleić do nowego projektu konsolowego. Zawiera wszystkie elementy, o których rozmawialiśmy — inicjalizację, ładowanie, rozpoznawanie i zapisywanie.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine (ocr engine example)
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // Optional: set license if you have one
            // var license = new License();
            // license.SetLicense("Aspose.OCR.lic");

            // -------------------------------------------------
            // 2️⃣  Load the multi‑page TIFF (extract text from TIFF)
            // -------------------------------------------------
            string tiffPath = @"YOUR_DIRECTORY/multi-page.tiff";
            if (!File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -------------------------------------------------
            // 3️⃣  Recognize every page
            // -------------------------------------------------
            var ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // 4️⃣  Save JSON (pretty) and optional XML
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/result.json";
            string jsonResult = ocrResult.ToJson(prettyPrint: true);
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"JSON saved to {jsonPath}");

            // Optional XML output
            string xmlPath = @"YOUR_DIRECTORY/result.xml";
            string xmlResult = ocrResult.ToXml();
            File.WriteAllText(xmlPath, xmlResult);
            Console.WriteLine($"XML saved to {xmlPath}");

            // -------------------------------------------------
            // 5️⃣  Quick verification (extract text from TIFF)
            // -------------------------------------------------
            string preview = jsonResult.Length > 200 ? jsonResult.Substring(0, 200) + "..." : jsonResult;
            Console.WriteLine("\nPreview of JSON output:");
            Console.WriteLine(preview);
        }
    }
}
```

Zapisz plik jako `Program.cs`, uruchom `dotnet run` i obserwuj, gdzie konsola wskaże lokalizację plików JSON i XML. To wszystko — właśnie ukończyłeś **przykład silnika OCR**, który wyodrębnia tekst z TIFF.

---

## Kolejne kroki i powiązane tematy

- **Przetwarzanie wsadowe:** Owiń powyższą logikę w pętlę `foreach`, aby automatycznie obsługiwać dziesiątki plików TIFF.  
- **Integracja z wyszukiwaniem:** Przekaż JSON do Elasticsearch lub Azure Cognitive Search, aby umożliwić pełnotekstowe wyszukiwanie w zeskanowanych dokumentach.  
- **Wstępne przetwarzanie obrazu:** Zbadaj API `ImageProcessing` Aspose, aby prostować, odszumiewać lub regulować kontrast przed OCR.  
- **Alternatywne wyjście:** Użyj `ocrResult.ToPlainText()`, jeśli potrzebujesz tylko surowych ciągów znaków bez metadanych.  

Jeśli interesują Cię inne formaty obrazów, ten sam schemat działa dla PDF‑ów (wystarczy zmienić plik źródłowy) lub PNG. Kluczowa lekcja: po skonfigurowaniu silnika reszta to powtarzalny pipeline.

---

## Podsumowanie

Przeszliśmy przez **kompletny przykład silnika OCR**, który pozwala **wyodrębnić tekst z TIFF** przy użyciu Aspose OCR, generując czysty JSON i opcjonalny XML dla dowolnego downstreamowego przepływu pracy. Kod jest samodzielny, a wyjaśnienia opisują „dlaczego” każdego kroku.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}