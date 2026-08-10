---
category: general
date: 2026-05-28
description: Utwórz przeszukiwalny PDF przy użyciu Aspose OCR w C#. Dowiedz się, jak
  uruchomić OCR na PDF, rozpoznać tekst w PDF i zamienić zeskanowany OCR PDF w przeszukiwalny
  PDF.
draft: false
keywords:
- create searchable pdf
- run ocr on pdf
- recognize text pdf
- ocr scanned pdf
- aspose ocr pdf
language: pl
og_description: Utwórz przeszukiwalny PDF przy użyciu Aspose OCR w C#. Postępuj zgodnie
  z tym przewodnikiem krok po kroku, aby wykonać OCR na PDF, rozpoznać tekst w PDF
  i obsłużyć zeskanowane pliki PDF z OCR.
og_title: Utwórz przeszukiwalny PDF przy użyciu Aspose OCR – Przeprowadź OCR w PDF
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  headline: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  type: TechArticle
- description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  name: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  steps:
  - name: Multiple Languages (OCR Scanned PDF)
    text: 'If your source PDF contains both English and Spanish text, combine languages:'
  - name: Password‑Protected PDFs
    text: 'When dealing with secured PDFs, supply the password before calling `Recognize`:'
  - name: Controlling Image Quality
    text: 'Higher DPI yields better OCR results but consumes more memory. Adjust the
      DPI if you notice garbled characters:'
  - name: License vs. Evaluation Mode
    text: 'In evaluation mode a watermark appears on each page. To remove it, apply
      your license before any OCR call:'
  - name: What’s Next?
    text: '- Explore the **aspose ocr pdf** API further: extract plain text, export
      to DOCX, or generate searchable PDFs in bulk. - Combine the searchable PDF output
      with Aspose.PDF to add bookmarks or watermarks. - Experiment with different
      DPI settings or custom OCR dictionaries for niche fonts.'
  type: HowTo
tags:
- Aspose
- OCR
- PDF
- C#
title: Utwórz przeszukiwalny PDF za pomocą Aspose OCR – Przeprowadź OCR na PDF
url: /pl/net/text-recognition/create-searchable-pdf-with-aspose-ocr-run-ocr-on-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie przeszukiwalnego PDF za pomocą Aspose OCR – Uruchamianie OCR na PDF

Kiedykolwiek potrzebowałeś **tworzyć przeszukiwalne PDF** z stosu zeskanowanych dokumentów? Nie jesteś sam. W wielu procesach biurowych jedyną rzeczą stojącą między tobą a w pełni przeszukiwalnym archiwum jest kilka linijek kodu, które uruchamiają OCR na stronach PDF.  

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokaże dokładnie, jak **tworzyć przeszukiwalne PDF** przy użyciu biblioteki Aspose OCR dla .NET. Po zakończeniu będziesz wiedział, jak *uruchomić OCR na PDF*, *rozpoznać tekst w PDF* oraz jak przekształcić *zeskany PDF z OCR* w wersję przeszukiwalną bez korzystania z usług osób trzecich.

> **Wymagania wstępne** – Aktualny .NET SDK (zalecany 6.0+), ważna licencja Aspose.OCR dla .NET (lub tymczasowy klucz ewaluacyjny) oraz PDF, który chcesz przetworzyć.

![Create searchable PDF diagram](alt="Diagram illustrating the create searchable pdf workflow using Aspose OCR")  

---

## Co obejmuje ten przewodnik

- Konfiguracja biblioteki Aspose OCR w projekcie C#.
- Ładowanie źródłowego PDF (dowolna liczba stron).
- Konfigurowanie silnika, aby generował **przeszukiwalny PDF**.
- Uruchamianie procesu OCR i zapisywanie wyniku.
- Wskazówki dotyczące obsługi dokumentów wielostronicowych, wyboru języka i typowych pułapek.

Jeśli wykonasz każdy krok, otrzymasz plik, który możesz otworzyć w Adobe Reader, nacisnąć **Ctrl + F** i natychmiast wyszukać dowolne słowo, które pojawiło się w oryginalnym skanie.

---

## Krok 1: Zainstaluj Aspose OCR dla .NET

Zanim napiszesz jakikolwiek kod, dodaj pakiet NuGet do swojego projektu:

```bash
dotnet add package Aspose.OCR
```

> **Porada:** Użyj flagi `--version`, aby zablokować najnowszą stabilną wersję (np. `Aspose.OCR 23.10`). Zapewnia to kompatybilność z .NET 6 i nowszymi.

---

## Krok 2: Utwórz instancję silnika OCR

Sercem procesu jest `OcrEngine`. Traktuj go jak mózg, który odczytuje obrazy i generuje tekst. Inicjalizacja jest prosta:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Instantiate the OCR engine
            var ocrEngine = new OcrEngine();
```

Obiekt `OcrEngine` będzie przechowywał zarówno strumień obrazu wejściowego, jak i konfigurację, która mówi Aspose, jak ma wyglądać wynik.

---

## Krok 3: Załaduj źródłowy PDF (Uruchom OCR na PDF)

Aspose OCR może bezpośrednio wczytać PDF; wewnętrznie wyodrębnia każdą stronę jako obraz. Zastąp ścieżkę zastępczą lokalizacją swojego zeskanowanego dokumentu:

```csharp
            // Step 3: Load the source PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);
```

> **Dlaczego to działa:** Metoda `ImageStream.FromFile` automatycznie wykrywa format PDF i przygotowuje reprezentację rastrową do OCR. Nie jest wymagany dodatkowy krok konwersji.

---

## Krok 4: Skonfiguruj format wyjściowy i język

Tutaj informujemy Aspose, co chcemy otrzymać. Ustawienie `OutputFormat` na `SearchablePdf` instruuje silnik, aby osadził rozpoznany tekst za oryginalnymi obrazami stron, tworząc **przeszukiwalny PDF**. Możesz także wybrać język, aby poprawić dokładność — domyślnie jest to angielski, ale możesz przełączyć się na francuski, niemiecki itp.

```csharp
            // Step 4: Choose output format and language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf; // creates searchable PDF
            ocrEngine.Configuration.Language = Language.English;               // *recognize text PDF* in English
```

Jeśli musisz przetworzyć dwujęzyczny dokument, możesz połączyć języki przy użyciu flag wyliczenia `Language`.

---

## Krok 5: Uruchom proces OCR – Rozpoznaj tekst w PDF

Teraz odbywa się najcięższa część. Metoda `Recognize` skanuje każdą stronę, wyodrębnia glify i buduje wewnętrzny strumień PDF, który zawiera zarówno oryginalny obraz, jak i niewidzialną warstwę tekstu. To jest krok, w którym *rozpoznajemy tekst w PDF*.

```csharp
            // Step 5: Execute OCR – this *recognizes text PDF* and builds the searchable stream
            ocrEngine.Recognize();
```

> **Częste pytanie:** *Co jeśli PDF ma 200 stron?*  
> Silnik przetwarza strony kolejno i strumieniu wyniki, więc zużycie pamięci pozostaje umiarkowane. Jednak przy bardzo dużych plikach możesz chcieć zwiększyć ustawienie `MemoryLimit` w `ocrEngine.Configuration`.

---

## Krok 6: Zapisz przeszukiwalny PDF

Na koniec zapisz wynik na dysku. Metoda `Save` zapisuje wewnętrzny strumień do nowego pliku, który możesz otworzyć dowolnym przeglądarką PDF.

```csharp
            // Step 6: Save the searchable PDF to disk
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

Uruchom program (`dotnet run`) i obserwuj, jak konsola potwierdza utworzenie pliku. Otwórz `handbook_searchable.pdf` i spróbuj wyszukać słowo, które wiesz, że występuje w oryginalnym skanie – powinieneś zobaczyć dopasowania natychmiast.

---

## Obsługa przypadków brzegowych i scenariuszy zaawansowanych

### Wiele języków (OCR zeskanowany PDF)

Jeśli Twój źródłowy PDF zawiera zarówno tekst po angielsku, jak i po hiszpańsku, połącz języki:

```csharp
ocrEngine.Configuration.Language = Language.English | Language.Spanish;
```

Aspose OCR przełączy słowniki w locie, zwiększając dokładność w dokumentach wielojęzykowych.

### PDF zabezpieczone hasłem

Podczas pracy z zabezpieczonymi PDF‑ami podaj hasło przed wywołaniem `Recognize`:

```csharp
ocrEngine.Image = ImageStream.FromFile(inputPath, "MySecretPassword");
```

Jeśli hasło jest nieprawidłowe, `Recognize` rzuca `InvalidPasswordException`; przechwycenie go pozwala poprosić użytkownika o poprawne hasło.

### Kontrola jakości obrazu

Wyższe DPI daje lepsze wyniki OCR, ale zużywa więcej pamięci. Dostosuj DPI, jeśli zauważysz zniekształcone znaki:

```csharp
ocrEngine.Configuration.Dpi = 300; // default is 200
```

### Licencja vs. tryb ewaluacji

W trybie ewaluacji na każdej stronie pojawia się znak wodny. Aby go usunąć, zastosuj licencję przed jakimkolwiek wywołaniem OCR:

```csharp
var license = new License();
license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");
```

---

## Porady profesjonalne dla zastosowań produkcyjnych

- **Przetwarzanie wsadowe:** Owiń główną logikę w pętlę `foreach`, która iteruje po liście PDF‑ów. Zwolnij `OcrEngine` po każdym pliku, aby zwolnić zasoby natywne.
- **Logowanie:** Użyj `ocrEngine.Configuration.Logger`, aby przechwycić szczegółowe statystyki OCR (np. rozpoznane znaki na sekundę). Jest to nieocenione przy rozwiązywaniu problemów z niską dokładnością.
- **Dostrajanie wydajności:** Na serwerach wielordzeniowych twórz osobne obiekty `OcrEngine` dla każdego wątku; biblioteka jest bezpieczna wątkowo, gdy każda instancja jest odizolowana.
- **Obsługa błędów:** Zawsze otaczaj `Recognize` i `Save` blokami `try/catch`. Typowe wyjątki to `FileNotFoundException`, `OutOfMemoryException` i `UnsupportedFormatException`.

---

## Pełny działający przykład (gotowy do kopiowania i wklejenia)

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Apply license (optional – removes evaluation watermark)
            // var license = new License();
            // license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");

            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Load PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Configure output as searchable PDF and set language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
            ocrEngine.Configuration.Language = Language.English;

            // 4️⃣ Run OCR – *recognize text PDF*
            ocrEngine.Recognize();

            // 5️⃣ Save the searchable PDF
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Oczekiwany wynik** (konsola):

```
Searchable PDF created at: C:\Docs\handbook_searchable.pdf
```

Otwórz powstały plik, naciśnij **Ctrl + F**, i będziesz mógł znaleźć każde słowo, które pojawiło się w oryginalnych zeskanowanych stronach. To magia przekształcania *zeskany PDF z OCR* w **przeszukiwalny PDF**.

---

## Zakończenie

Właśnie pokazaliśmy, jak **tworzyć przeszukiwalne PDF** przy użyciu Aspose OCR dla .NET, obejmując wszystko od instalacji pakietu po obsługę wielojęzycznych i zabezpieczonych hasłem PDF‑ów. Postępując zgodnie z tymi krokami, możesz niezawodnie *uruchamiać OCR na dokumentach PDF*, *rozpoznawać tekst w PDF* oraz konwertować każdy *zeskany PDF z OCR* w w pełni przeszukiwalny zasób.

### Co dalej?

- Zbadaj dalej API **aspose ocr pdf**: wyodrębnij czysty tekst, eksportuj do DOCX lub generuj przeszukiwalne PDF‑y masowo.
- Połącz wynik przeszukiwalnego PDF z Aspose.PDF, aby dodać zakładki lub znaki wodne.
- Eksperymentuj z różnymi ustawieniami DPI lub własnymi słownikami OCR dla specjalistycznych czcionek.

Śmiało modyfikuj przykład, włącz go do swojego potoku zarządzania dokumentami lub zadawaj pytania w komentarzach. Szczęśliwego kodowania i ciesz się przekształcaniem nieczytelnych skanów w przeszukiwalne złoto!

## Powiązane samouczki

- [Jak zrobić OCR PDF w .NET z Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Jak zrobić OCR PDF w .NET z Aspose.OCR](/ocr/spanish/net/text-recognition/recognize-pdf/)
- [Jak przeprowadzić OCR pliku PDF w .NET przy użyciu Aspose.OCR](/ocr/arabic/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}