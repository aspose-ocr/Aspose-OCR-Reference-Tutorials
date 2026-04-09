---
category: general
date: 2026-04-08
description: Twórz szybkie przeszukiwalne PDF i dowiedz się, jak kompresować obrazy
  w PDF, osadzać czcionki w PDF oraz rozpoznawać tekst na obrazie w C# przy użyciu
  Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- compress pdf images
- embed fonts pdf
- image to searchable pdf
- recognize text image
language: pl
og_description: Szybko twórz przeszukiwalne PDF za pomocą Aspose.OCR. Dowiedz się,
  jak kompresować obrazy w PDF, osadzać czcionki w PDF oraz rozpoznawać tekst na obrazach
  w jednym samouczku.
og_title: Utwórz przeszukiwalny PDF – Kompletny przewodnik C#
tags:
- Aspose.OCR
- C#
- PDF Generation
title: Utwórz przeszukiwalny PDF – Kompletny przewodnik C# konwersja obrazu na PDF
url: /pl/net/text-recognition/create-searchable-pdf-complete-c-guide-for-image-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz przeszukiwalny PDF – Kompletny przewodnik C#

Potrzebujesz **utworzyć przeszukiwalny pdf** z zeskanowanego obrazu? Nie jesteś jedyną osobą, która patrzyła na gigantyczny PNG i zastanawiała się, jak przekształcić go w lekki, tekstowo‑przeszukiwalny dokument. Dobra wiadomość jest taka, że z Aspose.OCR możesz zrobić to w kilku linijkach, a także nauczysz się **kompresować obrazy PDF**, **osadzać czcionki PDF** i **rozpoznawać tekst na obrazie** bez wysiłku.

W tym samouczku przeprowadzimy Cię przez cały proces: od wczytania obrazu, uruchomienia OCR, dostosowania opcji zapisu PDF, po ostateczne zapisanie przeszukiwalnego PDF na dysku. Po zakończeniu będziesz mieć gotową metodę, którą możesz wstawić do dowolnego projektu .NET, oraz kilka profesjonalnych wskazówek dotyczących przypadków brzegowych, które mogą się pojawić później.

## Czego będziesz potrzebować

- **.NET 6+** (kod działa również na .NET Framework 4.7, ale skierujemy się na .NET 6 dla nowoczesnej składni).  
- **Aspose.OCR for .NET** – zainstaluj przez NuGet: `Install-Package Aspose.OCR`.  
- Plik obrazu (PNG, JPEG, TIFF) zawierający tekst, który chcesz uczynić przeszukiwalnym.  
- Umiarkowana dawka ciekawości – reszta jest opisana poniżej.

> **Pro tip:** Jeśli planujesz przetwarzać dziesiątki stron, rozważ ponowne użycie jednej instancji `OcrEngine`, aby uniknąć kosztów wielokrotnego ładowania danych językowych.

## Krok 1: Skonfiguruj silnik OCR – Rozpoznawanie tekstu na obrazie

Pierwszą rzeczą, której potrzebujemy, jest silnik OCR, który potrafi odczytać znaki z bitmapy źródłowej. Aspose.OCR pozwala określić język (English, French, itp.) i zwraca obiekt `OcrResult`, który zawiera zarówno surowy tekst, jak i dane obrazu.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

public static OcrResult LoadAndRecognize(string imagePath)
{
    // Initialize the OCR engine – “en” is the ISO code for English.
    var ocrEngine = new OcrEngine { Language = "en" };

    // Recognize the image and get the result.
    OcrResult result = ocrEngine.RecognizeImage(imagePath);

    // Quick sanity check – throw if nothing was detected.
    if (string.IsNullOrWhiteSpace(result.Text))
        throw new InvalidOperationException("No text was recognized in the image.");

    return result;
}
```

**Dlaczego to ma znaczenie:**  
- Ustawienie języka znacząco zwiększa dokładność; silnik w tle ładuje słowniki specyficzne dla języka.  
- Obiekt `OcrResult` nie tylko przechowuje wyodrębniony ciąg znaków, ale także bazowy bitmap, który później osadzimy w PDF, aby dokument pozostał wizualnie identyczny z oryginalnym skanem.

## Krok 2: Skonfiguruj opcje zapisu PDF – Kompresja obrazów PDF i osadzanie czcionek

Przeszukiwalny PDF to w zasadzie zwykły PDF z niewidoczną warstwą tekstową na wierzchu zeskanowanego obrazu. Jeśli pominiesz kompresję, ostateczny plik może być ogromny. Klasa `PdfSaveOptions` daje precyzyjną kontrolę nad jakością obrazu, osadzaniem czcionek i tym, czy czcionki mają być podzestawiane.

```csharp
public static PdfSaveOptions GetPdfSaveOptions()
{
    return new PdfSaveOptions
    {
        // Reduce file size by compressing the raster image.
        CompressImages = true,

        // ImageQuality ranges from 0 (worst) to 100 (best). 75 is a good balance.
        ImageQuality = 75,

        // Embedding fonts ensures the text layer looks the same on any machine.
        EmbedFonts = true,

        // Subsetting keeps only the glyphs we actually use – another size saver.
        FontSubset = true
    };
}
```

**Dlaczego warto osadzać czcionki w PDF:**  
Gdy PDF zostanie otwarty na systemie, który nie posiada dokładnie tej czcionki użytej w warstwie OCR, tekst może wyglądać na zniekształcony. Osadzanie zapewnia wizualną wierność na wszystkich platformach, co jest kluczowe dla dokumentów prawnych lub archiwalnych.

## Krok 3: Zapisz wynik jako przeszukiwalny PDF – Obraz do przeszukiwalnego PDF

Teraz łączymy wszystko: bierzemy `OcrResult`, stosujemy nasze `PdfSaveOptions` i zapisujemy plik. Metoda `SaveAsSearchablePdf` wykonuje ciężką pracę — tworzy ukrytą warstwę tekstową, która odzwierciedla wynik OCR, jednocześnie zachowując oryginalny obraz.

```csharp
public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
{
    // Step 1: Recognize the image.
    OcrResult ocrResult = LoadAndRecognize(inputImage);

    // Step 2: Prepare PDF options.
    PdfSaveOptions pdfOptions = GetPdfSaveOptions();

    // Step 3: Write the searchable PDF.
    ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);

    Console.WriteLine($"Searchable PDF created at: {outputPdf}");
}
```

### Pełny działający przykład

Poniżej znajduje się samodzielny program konsolowy, który możesz skopiować i wkleić do nowego projektu .NET console. Zakłada, że obraz znajduje się w folderze o nazwie `YOUR_DIRECTORY` względem pliku wykonywalnego.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

class Program
{
    static void Main()
    {
        string inputPath = "YOUR_DIRECTORY/input.png";
        string outputPath = "YOUR_DIRECTORY/output.pdf";

        try
        {
            CreateCompressedSearchablePdf(inputPath, outputPath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }

    // --- Methods from the previous steps -------------------------------------------------
    public static OcrResult LoadAndRecognize(string imagePath)
    {
        var ocrEngine = new OcrEngine { Language = "en" };
        OcrResult result = ocrEngine.RecognizeImage(imagePath);
        if (string.IsNullOrWhiteSpace(result.Text))
            throw new InvalidOperationException("OCR did not detect any text.");
        return result;
    }

    public static PdfSaveOptions GetPdfSaveOptions()
    {
        return new PdfSaveOptions
        {
            CompressImages = true,
            ImageQuality = 75,
            EmbedFonts = true,
            FontSubset = true
        };
    }

    public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
    {
        OcrResult ocrResult = LoadAndRecognize(inputImage);
        PdfSaveOptions pdfOptions = GetPdfSaveOptions();
        ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);
        Console.WriteLine("Searchable PDF created.");
    }
}
```

Uruchomienie programu wygeneruje `output.pdf`, który możesz otworzyć w Adobe Reader, Foxit lub dowolnym przeglądarce PDF i natychmiast przeszukać pod kątem słów, które pierwotnie znajdowały się tylko na obrazie.

## Krok 4: Zweryfikuj wynik – Czy wyszukiwanie działa?

Po wygenerowaniu pliku otwórz go i wypróbuj wbudowaną funkcję wyszukiwania (Ctrl + F). Jeśli uda Ci się znaleźć słowa takie jak „invoice”, „date” lub „total”, pomyślnie utworzyłeś **przeszukiwalny PDF**.

Jeśli wyszukiwanie nic nie zwraca:

1. **Sprawdź dokładność OCR** – być może źródłowy obraz ma niską rozdzielczość. Rozważ zwiększenie DPI przed OCR (Aspose pozwala ustawić `Resolution` w silniku).  
2. **Potwierdź osadzenie czcionek** – otwórz właściwości PDF i sprawdź sekcję *Fonts*; powinna tam być wymieniona osadzona czcionka.  
3. **Sprawdź kompresję obrazu** – bardzo niska wartość `ImageQuality` może sprawić, że warstwa wizualna stanie się nieczytelna, co czasem myli narzędzia downstream.

## Typowe warianty i przypadki brzegowe

| Scenariusz | Co dostosować | Dlaczego |
|------------|----------------|----------|
| **Multi‑page TIFF** | Iteruj po każdej klatce, wywołaj `RecognizeImage` dla każdej strony, a następnie użyj `PdfSaveOptions` z `AppendMode = true`. | Zachowuje każdą zeskanowaną stronę jako osobną przeszukiwalną stronę. |
| **Non‑English language** | Zmień `Language = "fr"` (lub odpowiedni kod ISO) i opcjonalnie podaj własny słownik. | Poprawia rozpoznawanie znaków diakrytycznych i glifów specyficznych dla języka. |
| **Very large images** | Zmniejsz rozmiar bitmapy przed OCR (`ocrEngine.Image = Image.FromFile(...).GetThumbnailImage(...)`). | Zmniejsza zużycie pamięci i przyspiesza OCR bez znacznej utraty dokładności. |
| **Need OCR confidence** | Uzyskaj dostęp do `ocrResult.RecognizedWords` i sprawdź właściwość `Confidence`. | Umożliwia oznaczenie słów o niskim poziomie pewności do ręcznej weryfikacji. |

## Wskazówki dotyczące wydajności

- **Ponownie używaj `OcrEngine`** przy przetwarzaniu partii plików – buforuje dane językowe.  
- **Równolegle** wykonuj krok rozpoznawania przy użyciu `Parallel.ForEach`, jeśli masz maszynę wielordzeniową, ale zapisy PDF wykonuj kolejno, aby uniknąć konfliktów dostępu do plików.  
- **Dostosuj `ImageQuality`**: 85‑90 daje obrazy prawie bezstratne, natomiast 60‑70 zwykle wystarcza dla dokumentów z dużą ilością tekstu.

## Podsumowanie

Omówiliśmy wszystko, co potrzebne, aby **utworzyć przeszukiwalny pdf** z obrazów przy użyciu Aspose.OCR, jednocześnie ucząc się **kompresować obrazy pdf**, **osadzać czcionki pdf** i efektywnie **rozpoznawać tekst na obrazie**. Pełny przykład kodu jest gotowy do wstawienia w dowolnym projekcie C#, a dodatkowe wskazówki pomogą dostosować rozwiązanie do większych obciążeń lub innych języków.

Gotowy na kolejny krok? Spróbuj dodać znak wodny, połączyć kilka przeszukiwalnych PDF‑ów lub zintegrować tę procedurę z API webowym, aby użytkownicy mogli przesyłać skany i natychmiast otrzymywać przeszukiwalne PDF‑y. Możliwości są nieograniczone, a dzięki solidnym podstawom łatwo rozbudujesz ten przepływ pracy.

Miłego kodowania i niech Twoje PDF‑y pozostaną małe, przeszukiwalne i idealnie renderowane!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}