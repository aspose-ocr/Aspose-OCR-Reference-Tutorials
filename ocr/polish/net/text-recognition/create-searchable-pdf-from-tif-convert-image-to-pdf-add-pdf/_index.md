---
category: general
date: 2026-04-04
description: Utwórz przeszukiwalny PDF z obrazu TIF w C# – dowiedz się, jak konwertować
  obraz na PDF, dodać metadane PDF i wygenerować przeszukiwalny dokument przy użyciu
  Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- add metadata to pdf
- add pdf metadata
- create pdf from tif
language: pl
og_description: Utwórz przeszukiwalny PDF z pliku TIF przy użyciu C#. Konwertuj obraz
  na PDF, dodaj metadane PDF i stwórz przeszukiwalny dokument za pomocą Aspose.OCR.
og_title: Utwórz przeszukiwalny PDF z pliku TIF – przewodnik krok po kroku
tags:
- Aspose.OCR
- C#
- PDF generation
title: Utwórz przeszukiwalny PDF z pliku TIF – konwertuj obraz na PDF, dodaj metadane
  PDF
url: /pl/net/text-recognition/create-searchable-pdf-from-tif-convert-image-to-pdf-add-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz przeszukiwalny PDF z pliku TIF – Pełny przewodnik C#

Kiedykolwiek potrzebowałeś **utworzyć przeszukiwalny PDF** ze skanowanej faktury, ale nie byłeś pewien, jak zachować możliwość wyszukiwania tekstu i uporządkować metadane pliku? Nie jesteś sam. W wielu projektach automatyzacji PDF musi być zarówno czytelny dla maszyn, jak i odpowiednio otagowany informacjami takimi jak tytuł, autor i progi pewności.

W tym przewodniku przeprowadzimy Cię przez kompletną rozwiązanie, które **konwertuje obraz do PDF**, wstawia **metadane PDF** i filtruje wyniki OCR o niskiej pewności — wszystko przy użyciu biblioteki Aspose.OCR. Po zakończeniu będziesz mieć gotowy fragment kodu, który możesz wkleić do dowolnego projektu .NET, oraz kilka wskazówek dotyczących obsługi przypadków brzegowych.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również na .NET Framework 4.6+)  
- Pakiet NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Obraz TIF, który chcesz zamienić w przeszukiwalny PDF (np. `input.tif`)  
- Podstawowa znajomość C# i Visual Studio (lub ulubionego IDE)

Żadne dodatkowe usługi zewnętrzne nie są wymagane — cały proces odbywa się lokalnie.

## Krok 1 – Konfiguracja silnika OCR (Create Searchable PDF Core)

Pierwszą rzeczą, której potrzebujemy, jest instancja `OcrEngine`, która wie, jaki język rozpoznawać. W większości scenariuszy biznesowych wystarczy język angielski, ale możesz zamienić `Language.English` na dowolny obsługiwany język.

```csharp
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑related extensions

// Initialize OCR engine with English language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**Dlaczego to ważne:** Silnik OCR wykonuje najcięższą pracę, przekształcając piksele rastrowe w tekst Unicode. Poprawne ustawienie języka zwiększa dokładność i zmniejsza liczbę słów o niskiej pewności, które później zostaną odfiltrowane.

> **Pro tip:** Jeśli przetwarzasz dokumenty wielojęzyczne, utwórz wiele silników lub użyj `Language.Multilingual`, aby Aspose automatycznie wykrywał język.

## Krok 2 – Wczytanie obrazu TIF (Create PDF from TIF)

Teraz wskazujemy silnikowi plik źródłowy. Pomocnicza metoda `ImageStream.FromFile` odczytuje obraz do strumienia, który silnik OCR może przetworzyć.

```csharp
// Load the TIF image you want to make searchable
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.tif");
```

Możesz się zastanawiać, *„Czy mogę podać JPEG lub PNG zamiast?”* Oczywiście — Aspose.OCR obsługuje większość formatów rastrowych. Wystarczy zmienić rozszerzenie pliku i gotowe.

## Krok 3 – Konfiguracja opcji PDF (Add Metadata to PDF)

Przed konwersją definiujemy obiekt `PdfOptions`. To tutaj **dodajemy metadane PDF**, takie jak tytuł i autor, oraz określamy, aby silnik odrzucał słowa, których pewność jest niższa niż określony próg.

```csharp
PdfOptions searchablePdfOptions = new PdfOptions
{
    Title = "Invoice #12345",
    Author = "MyCompany",
    // Hide words with confidence lower than 0.8 (80%)
    MinConfidence = 0.8f
};
```

**Co się tutaj dzieje?**  
- `Title` i `Author` stają się częścią słownika informacji o dokumencie PDF, co ułatwia indeksowanie pliku w systemach zarządzania dokumentami.  
- `MinConfidence` to zabezpieczenie: OCR często błędnie odczytuje słabe znaki; ich odfiltrowanie utrzymuje warstwę przeszukiwalną w czystości i poprawia późniejsze wyodrębnianie tekstu.

Jeśli potrzebujesz własnych metadanych (np. `Subject`, `Keywords`), możesz je ustawić poprzez `PdfOptions.CustomProperties`.

## Krok 4 – Konwersja obrazu do przeszukiwalnego PDF (Convert Image to PDF)

Po przygotowaniu silnika i opcji, ostatnie wywołanie wykonuje konwersję. Zapisuje przeszukiwalny PDF na dysku, osadzając warstwę tekstu OCR pod oryginalnym obrazem.

```csharp
ocrEngine.ConvertToSearchablePdf(
    outputPath: @"YOUR_DIRECTORY/output.pdf",
    pdfOptions: searchablePdfOptions);
```

Po wykonaniu tego wiersza, `output.pdf` zawiera:
- Oryginalny obraz TIF jako tło wizualne  
- Niewidoczną warstwę tekstową, którą mogą odczytać wyszukiwarki i operacje kopiuj‑wklej  
- Metadane zdefiniowane wcześniej (tytuł, autor itp.)

### Oczekiwany rezultat

Otwórz wygenerowany PDF w Adobe Reader lub dowolnym przeglądarce PDF i spróbuj zaznaczyć tekst. Powinieneś móc skopiować zdania, które odpowiadają oryginalnemu skanowi. Dialog **Properties** pokaże tytuł „Invoice #12345” i autora „MyCompany”.

## Krok 5 – Weryfikacja filtrowania pewności (Why MinConfidence Helps)

Warto potwierdzić, że słowa o niskiej pewności rzeczywiście zostały usunięte. Możesz sprawdzić ukryty tekst PDF przy pomocy narzędzia takiego jak `pdftotext`:

```bash
pdftotext output.pdf - | grep -i "unlikelyword"
```

Jeśli słowo nie pojawia się, filtr `MinConfidence` działał zgodnie z zamierzeniami. Dostosuj próg (np. `0.7f`), jeśli potrzebujesz bardziej agresywnego lub łagodnego filtrowania.

## Krok 6 – Obsługa wielu stron (Create Searchable PDF from Multi‑Page TIF)

Wiele faktur jest dostarczanych jako wielostronicowe pliki TIFF. Aspose.OCR traktuje każdą klatkę jako osobną stronę automatycznie. Wystarczy wskazać silnikowi plik wielostronicowy; to samo wywołanie `ConvertToSearchablePdf` wygeneruje wielostronicowy przeszukiwalny PDF.

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
ocrEngine.ConvertToSearchablePdf(@"YOUR_DIRECTORY/multi_output.pdf", searchablePdfOptions);
```

**Przypadek brzegowy:** Jeśli strona jest pusta, OCR może nadal wygenerować pustą warstwę tekstową, co nie szkodzi. Możesz jednak pominąć puste strony, sprawdzając `ocrEngine.HasText` przed konwersją.

## Krok 7 – Pakowanie pełnego przykładu (All Steps Together)

Poniżej znajduje się kompletny, gotowy do uruchomienia program, który łączy wszystkie kroki. Zamień `YOUR_DIRECTORY` na rzeczywistą ścieżkę folderu na swoim komputerze.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load the TIF image (create pdf from tif)
        string inputPath = @"YOUR_DIRECTORY/input.tif";
        ocrEngine.Image = ImageStream.FromFile(inputPath);

        // 3️⃣ Set PDF metadata and confidence filter
        PdfOptions pdfOptions = new PdfOptions
        {
            Title = "Invoice #12345",
            Author = "MyCompany",
            MinConfidence = 0.8f
        };

        // 4️⃣ Convert to searchable PDF (convert image to pdf)
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ConvertToSearchablePdf(outputPath, pdfOptions);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

Uruchom program (`dotnet run` lub naciśnij **F5** w Visual Studio) i zobacz komunikat potwierdzający. Wygenerowany PDF znajdzie się obok obrazu źródłowego, gotowy do indeksacji lub archiwizacji.

## Częste pytania i pułapki

| Pytanie | Odpowiedź |
|----------|--------|
| **Czy mogę dodać własną czcionkę do warstwy przeszukiwalnej?** | Warstwa OCR używa Unicode; wygląd wizualny jest determinowany przez podkład obrazu, więc dodatkowe osadzanie czcionek nie jest wymagane. |
| **Co jeśli mój TIF jest kolorowy?** | Aspose.OCR automatycznie konwertuje obrazy kolorowe na odcienie szarości dla OCR, ale możesz zachować oryginalne kolory w PDF, ustawiając `PdfOptions.PreserveColor = true`. |
| **Czy biblioteka jest bezpieczna wątkowo?** | Każda instancja `OcrEngine` powinna być używana przez pojedynczy wątek. Do przetwarzania równoległego twórz osobny silnik dla każdego wątku. |
| **Jak zaszyfrować PDF?** | Użyj `PdfOptions.Security`, aby ustawić hasło i uprawnienia po konwersji OCR. |

## Kolejne kroki (Rozbuduj swój zestaw narzędzi PDF)

- **Przetwarzanie wsadowe:** Przejdź pętlą po folderze TIFF‑ów i wygeneruj przeszukiwalny PDF dla każdego z nich.  
- **Post‑processing:** Skorzystaj z Aspose.PDF, aby połączyć wygenerowane PDF‑y w jeden dokument główny.  
- **Zaawansowane metadane:** Wypełnij własne pola XMP, aby lepiej integrować się z SharePoint lub systemami ECM.  

Wszystkie te rozszerzenia opierają się na podstawowym wzorcu, który właśnie omówiliśmy: **utwórz przeszukiwalny PDF**, **konwertuj obraz do PDF** i **dodaj metadane PDF**.

---

*Miłego kodowania! Jeśli napotkasz problemy, zostaw komentarz poniżej lub sprawdź dokumentację Aspose.OCR pod kątem najnowszych aktualizacji API.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}