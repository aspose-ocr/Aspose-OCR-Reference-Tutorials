---
category: general
date: 2026-05-28
description: Samouczek OCR języka koreańskiego przy użyciu Aspose w C#. Dowiedz się,
  jak wczytać obraz ze strumienia, wyodrębnić zwykły tekst, przekonwertować obraz
  na PDF i wyeksportować przeszukiwalny PDF.
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: pl
og_description: OCR języka koreańskiego w C# przy użyciu Aspose. Przewodnik krok po
  kroku, jak wczytać obraz ze strumienia, wyodrębnić zwykły tekst, przekonwertować
  obraz na PDF i wyeksportować przeszukiwalny PDF.
og_title: OCR języka koreańskiego – konwertuj obraz na PDF i wyodrębnij tekst (poradnik
  C#)
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: 'OCR języka koreańskiego przy użyciu Aspose: konwertuj obraz do PDF i wyodrębnij
  tekst w C#'
url: /pl/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR języka koreańskiego z Aspose: konwersja obrazu do PDF i wyodrębnianie tekstu w C#

Zastanawiałeś się kiedyś, jak uruchomić **Korean Language OCR** na zdjęciu, nie wysyłając nic do chmury? Nie jesteś jedyny. Niezależnie od tego, czy digitalizujesz znaki drogowe, przetwarzasz paragony, czy budujesz wielojęzyczny indeks wyszukiwania, możliwość rozpoznawania koreańskich znaków lokalnie może zaoszczędzić Ci czas, pieniądze i problemy z prywatnością.

W tym tutorialu przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokaże, jak **load image from stream**, **extract plain text**, **convert image to PDF**, a na koniec **export searchable PDF** — wszystko przy użyciu Aspose.OCR i kilku linii C#. Bez zewnętrznych usług, bez ukrytej magii — po prostu czysty kod .NET, który możesz wkleić do dowolnej aplikacji konsolowej.

## Co zdobędziesz po przeczytaniu

- Działający program konsolowy, który odczytuje plik JPEG poprzez strumień plikowy.  
- Tekst w języku koreańskim wyodrębniony jako zwykłe ciągi Unicode.  
- Szczegółowy raport w formacie JSON z przebiegu OCR, przydatny do debugowania lub analiz.  
- Przeszukiwalny PDF, który możesz otworzyć w dowolnym czytniku PDF i rzeczywiście zaznaczyć koreańskie słowa.  

**Prerequisites**  
- .NET 6.0 lub nowszy (kod działa również na .NET Framework 4.7+).  
- Pakiet NuGet Aspose.OCR for .NET zainstalowany (`Install-Package Aspose.OCR`).  
- Folder zawierający `korean_sign.jpg` oraz miejsce, w którym można zapisać pliki wyjściowe.  

Jeśli już masz te elementy, świetnie — przejdźmy do praktyki.

## Krok 1: Inicjalizacja silnika OCR dla języka koreańskiego

Pierwszą rzeczą, której potrzebujesz, jest instancja `OcrEngine`. Włączenie GPU (jeśli je posiadasz) przyspiesza rozpoznawanie znacząco, a wyłączenie automatycznego pobierania zasobów zmusza bibliotekę do użycia offline'owych pakietów językowych, które dostarczysz.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **Dlaczego to ważne:**  
> *GPU acceleration* może skrócić czas przetwarzania z sekund do milisekund przy dużych partiach. Ustawienie `AutomaticResourceDownload` na `false` zapewnia, że demo działa offline — kluczowy wymóg w wielu środowiskach korporacyjnych.

## Krok 2: Ładowanie obrazu ze strumienia

Odczyt obrazu przez strumień daje elastyczność: możesz pobierać pliki z dysku, udziałów sieciowych lub nawet z pamięci podręcznej blobów. Tutaj otwieramy lokalny plik JPEG, ale ten sam wzorzec działa dla dowolnego `Stream`.

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **Pro tip:** Jeśli kiedykolwiek będziesz musiał przetwarzać obrazy przesyłane przez API webowe, po prostu zamień `File.OpenRead` na `IFormFile.OpenReadStream()` — reszta pozostaje identyczna.

## Krok 3: Wybór języka koreańskiego i zastosowanie filtrów wstępnego przetwarzania

Aspose.OCR obsługuje kilka kroków wstępnego przetwarzania, które czyszczą obraz przed rozpoznaniem. Dla znaków koreańskich zazwyczaj wystarczają deskew i denoise.

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **Co się dzieje pod maską?**  
> Filtr `Deskew` prostuje obrócony tekst, a `Denoise` usuwa szumy, które mogą mylić klasyfikator znaków. Pomijanie tych kroków często prowadzi do zniekształconego wyniku, szczególnie przy zdjęciach o niskiej rozdzielczości.

## Krok 4: Asynchroniczne wyodrębnianie czystego tekstu

Nadszedł moment prawdy — prosimy silnik o rozpoznanie znaków i zwrócenie nam czystego ciągu. Użycie `RecognizeAsync` utrzymuje responsywność UI, jeśli wbudujesz to w aplikację desktopową lub webową.

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

Po uruchomieniu programu powinieneś zobaczyć coś w rodzaju:

```
OCR complete. Extracted text:
서울시청
```

> **Dlaczego async?**  
> OCR może być intensywny pod względem CPU. Asynchroniczne wykonanie zapobiega blokowaniu wątku, co jest szczególnie przydatne w ASP.NET Core, gdzie niedobór wątków jest realnym problemem.

## Krok 5: Uzyskanie szczegółowego wyniku rozpoznania i zapis jako JSON

Czasami potrzebujesz więcej niż sam surowy ciąg — np. oceny pewności, ramki ograniczające lub oryginalne dane obrazu. Metoda `RecognizeDetailed` zwraca obiekt `RecognitionResult`, który można zserializować do JSON w celu późniejszej analizy.

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

Otwierając `korean_ocr.json` zobaczysz strukturę podobną do:

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **Kiedy to używać?**  
> Jeśli budujesz indeks wyszukiwania, wartości pewności pozwalają odfiltrować wyniki niskiej jakości. Jeśli potrzebujesz podświetlić tekst w UI, ramki ograniczające są Twoją mapą.

## Krok 6: Konwersja obrazu do PDF i eksport przeszukiwalnego PDF

Aspose sprawia, że przejście od rastra do wektora jest bezwysiłkowe. Ustawiając `OutputFormat` na `SearchablePdf`, biblioteka osadza oryginalny obraz i nakłada niewidoczną warstwę tekstową zawierającą wynik OCR. Powstały PDF można przeszukiwać, kopiować i indeksować tak, jak każdy natywny PDF.

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

Otwórz `korean_searchable.pdf` w Adobe Reader lub dowolnym przeglądarce PDF, naciśnij **Ctrl+F**, wpisz koreańskie słowo i zobacz, jak przeskakuje do dokładnego miejsca na stronie. To moc przeszukiwalnego PDF.

> **Dodatkowa wskazówka:** Jeśli potrzebujesz jedynie wizualnego PDF bez ukrytej warstwy tekstowej, zmień `OutputFormat` na `Pdf`.

## Pełny działający przykład

Poniżej znajduje się kompletny program — skopiuj, wklej, zamień `YOUR_DIRECTORY` na rzeczywistą ścieżkę i naciśnij **F5**.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### Oczekiwany wynik w konsoli

```
OCR complete. Extracted text:
서울시청
```

I znajdziesz trzy nowe pliki obok obrazu źródłowego:

- `korean_ocr.json` – pełne dane rozpoznania.  
- `korean_searchable.pdf` – PDF, który możesz przeszukiwać.  
- (opcjonalnie) dowolne pośrednie logi, które zdecydujesz się dodać.

## Częste pytania i sytuacje brzegowe

**Co jeśli nie mam GPU?**  
Ustaw `EnableGpu = false`; fallback na CPU jest w zupełności wystarczający dla małych partii.

**Czy mogę przetwarzać wiele obrazów w jednym uruchomieniu?**  
Oczywiście. Owiń logikę w pętlę `foreach (var file in Directory.GetFiles(...))` i przy każdej iteracji przypisuj `ocrEngine.Image` na nowy obraz.

**Jak obsłużyć inne języki razem z koreańskim?**  
Aspose.OCR pozwala ustawić `Language = Language.AutoDetect` lub połączyć języki operatorem bitowym OR (np. `Language.Korean | Language.English`).

**Co zrobić, gdy pewność OCR jest niska?**  
Sprawdź `detailedResult.Pages[0].Words` i odfiltruj wpisy z `Confidence < 0.7`. Możesz też dostroić filtry wstępnego przetwarzania — spróbuj dodać `PreprocessFilter.ContrastEnhancement`.

## Podsumowanie

Właśnie zobaczyłeś, jak wykonać **Korean Language OCR** od początku do końca, od **loading image from stream**, przez **extract plain text**, **convert image to PDF**, aż po **export searchable PDF**. Podejście jest modularne, więc możesz podmienić źródło obrazu, zmienić format wyjścia lub podłączyć JSON do dowolnego downstreamowego pipeline’u.

Co dalej


## Powiązane tutoriale

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}