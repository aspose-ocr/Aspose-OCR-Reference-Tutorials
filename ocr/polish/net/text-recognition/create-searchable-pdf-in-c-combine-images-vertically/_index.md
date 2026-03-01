---
category: general
date: 2026-02-28
description: Utwórz przeszukiwalny PDF w C# poprzez łączenie obrazów pionowo. Dowiedz
  się, jak układać obrazy w pionie i konwertować zeskanowane strony PDF przy użyciu
  Aspose OCR.
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: pl
og_description: Utwórz przeszukiwalny PDF w C# poprzez łączenie obrazów w pionie.
  Ten przewodnik pokazuje, jak układać obrazy pionowo i konwertować zeskanowane strony
  PDF przy użyciu Aspose OCR.
og_title: Utwórz przeszukiwalny PDF w C# – Połącz obrazy pionowo
tags:
- Aspose OCR
- C#
- PDF generation
title: Utwórz przeszukiwalny PDF w C# – Łącz obrazy pionowo
url: /pl/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz przeszukiwalny PDF w C# – Łączenie obrazów pionowo

Czy kiedykolwiek potrzebowałeś **utworzyć przeszukiwalny PDF** z kilku zeskanowanych plików PNG, ale nie wiedziałeś, od czego zacząć? Nie jesteś sam. W wielu projektach automatyzacji dokumentów największym problemem jest przekształcenie stosu plików graficznych w jeden schludny, przeszukiwalny PDF, który możesz indeksować i udostępniać.  

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokaże Ci **jak układać obrazy pionowo**, **łączyć obrazy pionowo**, a w końcu **konwertować zeskanowane strony PDF** do jednego przeszukiwalnego dokumentu przy użyciu silnika przyspieszanego GPU od Aspose.OCR. Po zakończeniu będziesz mieć samodzielny program, który możesz wstawić do dowolnego rozwiązania .NET.

> **Czego się nauczysz**
> - Zainicjalizuj silnik OCR z obsługą GPU.
> - Przetwarzaj partię obrazów równolegle.
> - **Łącz obrazy pionowo**, aby naśladować skan wielostronicowy.
> - Eksportuj przeszukiwalny PDF oraz szczegółowy raport JSON do dalszej analizy.

## Wymagania wstępne

- .NET 6+ (kod kompiluje się z .NET 6, .NET 7 lub .NET 8)
- Pakiet NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Maszyna z obsługą GPU, jeśli chcesz zachować ustawienie `ProcessingMode.Gpu` (fallback na CPU również działa)
- Folder z kilkoma zeskanowanymi plikami PNG/JPEG (demo używa `page1.png`, `page2.png`, `page3.png`)

Brak zewnętrznych usług, brak ukrytych plików konfiguracyjnych — tylko czysty C#.

## Krok 1 – Skonfiguruj silnik OCR do **utworzenia przeszukiwalnego PDF**

Najpierw tworzymy `OcrEngine`, włączamy przyspieszenie GPU, wybieramy język angielski i dodajemy kilka filtrów wstępnego przetwarzania. Filtry te poprawiają dokładność, prostując przechylone strony (`DeskewFilter`) i usuwając szumy (`DenoiseFilter`).

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**Dlaczego to ważne:** Silnik OCR wykonuje najcięższą pracę polegającą na rozpoznawaniu tekstu. Włączenie `ProcessingMode.Gpu` może skrócić czas rozpoznawania o połowę na nowoczesnej karcie graficznej, a filtry redukują typowe artefakty skanowania, które w przeciwnym razie generowałyby nieczytelny wynik.

## Krok 2 – Skonfiguruj przetwarzanie wsadowe do **konwersji zeskanowanych stron PDF** efektywnie

Przetwarzanie każdej strony pojedynczo jest w porządku przy kilku obrazach, ale w rzeczywistych projektach często mamy do czynienia z dziesiątkami lub setkami stron. `OcrBatchProcessor` z Aspose.OCR pozwala nam uruchamiać rozpoznawanie równolegle, co dramatycznie przyspiesza krok **konwersji zeskanowanych stron pdf**.

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**Wskazówka:** Jeśli korzystasz z maszyny tylko z CPU, ustaw `ProcessingMode = ProcessingMode.Cpu`. Przetwarzanie wsadowe nadal będzie respektować `MaxDegreeOfParallelism`, więc możesz je dostosować, aby nie przeciążać maszyny.

## Krok 3 – Uruchom OCR na partii i zbierz wyniki

Teraz faktycznie rozpoznajemy tekst. Metoda `Recognize` zwraca listę obiektów `OcrResult`, z których każdy zawiera zarówno oryginalny obraz, jak i wyodrębniony tekst.

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

W tym momencie masz wszystko, co potrzebne do **utworzenia przeszukiwalnego PDF**: obrazy (wciąż w pamięci) oraz powiązane warstwy tekstowe.

## Krok 4 – **Łącz obrazy pionowo** i wygeneruj przeszukiwalny PDF

Większość zeskanowanych dokumentów to wielostronicowe PDF‑y, więc musimy połączyć poszczególne obrazy stron w jeden wysoki obraz, który odzwierciedla fizyczny stos. Aspose.OCR udostępnia `Image.CombineVertical` właśnie do tego celu.

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

Powstały plik (`combined_searchable.pdf`) zawiera wybieralny, przeszukiwalny tekst pod każdym obrazem strony — dokładnie to, czego potrzebujesz, aby **utworzyć przeszukiwalny PDF** ze skanowanych źródeł.

![Przykład tworzenia przeszukiwalnego PDF](/images/create-searchable-pdf.png "przykład tworzenia przeszukiwalnego pdf")

*Tekst alternatywny obrazu: przykład tworzenia przeszukiwalnego pdf pokazujący połączony PDF z przeszukiwalnym tekstem.*

**Dlaczego układanie pionowo?** Wiele bibliotek OCR traktuje każdy obraz jako osobną stronę. Łącząc je, zachowujemy kolejność stron w PDF‑ie, jednocześnie wykorzystując pojedyncze przejście OCR dla całego dokumentu.

## Krok 5 – Eksportuj szczegółowy JSON dla pierwszej strony (świetny do dalszych przepływów pracy)

Czasami potrzebujesz czegoś więcej niż PDF; być może chcesz przekazać dane OCR do bazy danych lub potoku uczenia maszynowego. Aspose.OCR umożliwia serializację każdego `OcrResult` do JSON, zachowując ramki ograniczające, wyniki pewności i inne informacje.

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**Oczekiwany fragment JSON (skrócony):**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

Teraz możesz wprowadzić ten JSON do dowolnego systemu downstream — niezależnie od tego, czy indeksujesz tekst w Elasticsearch, czy przekazujesz go do własnego panelu analitycznego.

---

## Jak **układać obrazy pionowo** – szybkie podsumowanie

Jeśli zastanawiasz się **jak układać obrazy pionowo** bez Aspose, możesz użyć `System.Drawing` do stworzenia nowego bitmapa i rysowania kolejnych stron jedna po drugiej. Jednak wbudowane w Aspose `Image.CombineVertical` obsługuje DPI, format pikseli i zarządzanie pamięcią, co czyni je najpewniejszym wyborem dla kodu produkcyjnego.

### Alternatywa: użycie `System.Drawing` (tylko z ciekawości)

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

Ręczne podejście działa, ale tracisz wygodę automatycznej obsługi DPI oraz możliwość bezpośredniego przekazania wyniku z powrotem do `RecognizeToPdf`. Trzymaj się `CombineVertical`, chyba że masz bardzo specyficzne wymagania.

## Typowe pułapki i jak ich unikać

| Problem | Dlaczego się pojawia | Rozwiązanie |
|-------|----------------|-----|
| **Błędy braku pamięci** przy przetwarzaniu dziesiątek skanów wysokiej rozdzielczości | Każdy obraz pozostaje w pamięci aż do zapisania PDF | Zwolnij obiekty `Image` natychmiast po użyciu (bloki `using`) lub zmniejsz rozdzielczość obrazów przed łączeniem |
| **Śmieciowy tekst** po OCR | Przechylone skany lub niski kontrast | Zachowaj `DeskewFilter` i `DenoiseFilter`; rozważ dodanie `ContrastFilter`, jeśli to konieczne |
| **Brak warstwy przeszukiwalnej** | Użyto `Recognize` zamiast `RecognizeToPdf` | Upewnij się, że wywołujesz `ocrEngine.RecognizeToPdf` na połączonym obrazie |
| **Awaria fallbacku GPU** na maszynach bez odpowiednich sterowników | `ProcessingMode.Gpu` zgłasza wyjątek | Otocz tworzenie silnika blokiem try/catch i przełącz się na `ProcessingMode.Cpu` |

## Kolejne kroki – rozszerzanie przepływu pracy

Teraz, gdy wiesz, jak **utworzyć przeszukiwalny PDF**, możesz chcieć:

- **Przetwarzać wsadowo całe foldery** używając `Directory.GetFiles` i pętli `foreach`.
- **Dodawać znaki wodne** do każdej strony przed łączeniem (użyj `ImageProcessor` z Aspose.Imaging).
- **Podzielić przeszukiwalny PDF z powrotem na pojedyncze strony** jeśli później potrzebujesz PDF‑ów per strona (`PdfDocument.Split` z Aspose.PDF).
- **Zintegrować z Azure Blob Storage** aby pobierać obrazy z chmury i wysyłać finalny PDF z powrotem.

Wszystkie te rozszerzenia naturalnie opierają się na tych samych podstawowych koncepcjach: konfiguracja OCR, obsługa obrazów i eksport PDF.

## Zakończenie

Omówiliśmy wszystko, co potrzebne, aby **utworzyć przeszukiwalny PDF** z zestawu zeskanowanych obrazów w C#. Inicjalizując silnik `OcrEngine` z obsługą GPU, uruchamiając równoległe przetwarzanie wsadowe przy użyciu `OcrBatchProcessor`, **łącząc obrazy pionowo** i na koniec wywołując `RecognizeToPdf`, otrzymujesz schludny, przeszukiwalny dokument gotowy do archiwizacji lub indeksowania. Dodatkowy eksport JSON zapewnia pełną widoczność wyników OCR, otwierając możliwości analizy lub niestandardowych przepływów pracy.

Wypróbuj to, eksperymentuj z różnymi filtrami i obserwuj, jak Twój pipeline automatyzacji dokumentów staje się znacznie płynniejszy. Jeśli napotkasz jakiekolwiek problemy, zostaw komentarz — miłego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}