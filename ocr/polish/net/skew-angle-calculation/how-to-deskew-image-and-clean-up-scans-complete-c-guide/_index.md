---
category: general
date: 2026-03-18
description: Jak prostować obraz i redukować szumy w zeskanowanych plikach. Dowiedz
  się, jak wczytać obraz z pliku, wyodrębnić tekst z pliku TIFF oraz rozpoznać tekst
  z obrazu przy użyciu Aspose OCR.
draft: false
keywords:
- how to deskew image
- how to reduce noise
- recognize text from image
- load image from file
- extract text from tiff
language: pl
og_description: Jak szybko prostować obraz przy użyciu Aspose OCR. Ten przewodnik
  pokazuje, jak redukować szumy, wczytywać obraz z pliku i wyodrębniać tekst z pliku
  TIFF w języku C#.
og_title: Jak prostować obraz – Pełny samouczek OCR w C#
tags:
- OCR
- C#
- Image Processing
title: Jak wyprostować obraz i oczyścić skany – Kompletny przewodnik C#
url: /pl/net/skew-angle-calculation/how-to-deskew-image-and-clean-up-scans-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak prostować obraz – Pełny samouczek OCR w C#

Zastanawiałeś się kiedyś, **jak prostować obraz** plików, które wyglądają, jakby zostały zeskanowane przy użyciu chwiejnego skanera? Nie jesteś sam. Większość programistów napotyka ten problem, gdy źródłowy plik TIFF jest nieco przekrzywiony, a wyniki OCR są bałaganem. Dobra wiadomość? Kilka linijek C# pozwala wyprostować obraz, usunąć ziarniste tło i wydobyć czysty, przeszukiwalny tekst prosto z pliku.

W tym przewodniku przejdziemy przez **jak redukować szum**, **ładowanie obrazu z pliku**, oraz w końcu **rozpoznawanie tekstu z obrazu** przy użyciu Aspose OCR. Po zakończeniu będziesz w stanie **wyodrębnić tekst z dokumentów TIFF** bez wysiłku.

> **Porada:** Jeśli już używasz Aspose OCR w innych projektach, możesz dodać te filtry bez dodatkowych problemów licencyjnych.

## Czego będziesz potrzebować

- .NET 6 lub nowszy (kod działa również na .NET Core)  
- Pakiet NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Zeskanowany plik TIFF, który jest lekko obrócony lub zaszumiony (użyjemy `skewed_scanned_doc.tif` jako przykładu)  
- Edytor tekstu lub IDE (Visual Studio, VS Code, Rider – wybierz, co wolisz)

Nie są wymagane dodatkowe biblioteki; filtry, które użyjemy, są wbudowane w Aspose OCR.

## Krok 1 – Utworzenie silnika OCR (Jak prostować obraz)

Pierwszą rzeczą, którą robisz, jest uruchomienie `OcrEngine`. Traktuj go jak mózg, który później odczyta znaki za Ciebie.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this object holds all settings
        var ocrEngine = new OcrEngine();
```

Dlaczego tworzyć silnik od razu? Daje to jedno miejsce, w którym możesz podłączyć filtry wstępnego przetwarzania, pakiety językowe i opcje wyjściowe. Jeśli pominiesz ten krok i wywołasz `OcrEngine.Recognize` bezpośrednio, tracisz możliwość najpierw wyczyszczenia obrazu, co jest dokładnie powodem, dla którego zależy nam na prostowaniu.

## Krok 2 – Dodanie filtrów prostowania i redukcji szumu (Jak redukować szum)

Teraz dołączamy dwa filtry:

| Filter | What it does | Why it matters |
|--------|--------------|----------------|
| `AutoDeskewFilter` | Detects and corrects rotation | Straightens text lines so the OCR engine can read them correctly |
| `NoiseReductionFilterV2` | Removes speckles and background grain | Cleaner pixels mean fewer mis‑recognitions |

```csharp
        // Add filters to improve OCR accuracy
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // corrects rotation
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduces background noise
```

Możesz zamienić `NoiseReductionFilterV2` na starszą wersję, ale algorytm v2 lepiej radzi sobie z nowoczesnymi skanerami. Jeśli Twój dokument jest już idealnie płaski, filtr prostujący po prostu przepuści obraz bez zmian — nie zaszkodzi.

## Krok 3 – Ładowanie obrazu z pliku (Load Image from File)

Aspose udostępnia przydatny pomocnik `ImageStream.FromFile`, który odczytuje różne formaty, w tym TIFF, JPEG, PNG i BMP. Oto jak wczytujemy plik do pamięci:

```csharp
        // Load the scanned image you want to preprocess
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");
```

Zastąp `YOUR_DIRECTORY` rzeczywistą ścieżką na swoim komputerze. Jeśli używasz ścieżki względnej, upewnij się, że plik znajduje się obok Twojego pliku wykonywalnego lub ustaw odpowiednio katalog roboczy.

## Krok 4 – Uruchomienie OCR na przetworzonym obrazie (Rozpoznawanie tekstu z obrazu)

Po ustawieniu filtrów i wczytaniu obrazu, w końcu prosimy Aspose o odczytanie znaków:

```csharp
        // Perform OCR – the engine will automatically apply the filters first
        var ocrResult = ocrEngine.Recognize(image);
```

W tle silnik uruchamia algorytm prostowania, wygładza szum, a następnie używa rozpoznawacza opartego na sieci neuronowej. Wynik jest opakowany w obiekt `OcrResult`, który dostarcza surowy tekst, wskaźniki pewności oraz ewentualne ramki ograniczające, jeśli będą potrzebne później.

## Krok 5 – Wyświetlenie lub zapis wyodrębnionego tekstu (Wyodrębnianie tekstu z TIFF)

Dla szybkiej demonstracji po prostu wypisujemy tekst w konsoli, ale możesz zapisać go do pliku, bazy danych lub przekazać do dalszego procesu.

```csharp
        // Show the recognized text in the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Oczekiwany wynik** (przykład, będzie się różnić w zależności od dokumentu):

```
Invoice #12345
Date: 2023‑04‑01
Total: $1,250.00
Thank you for your business!
```

Jeśli wynik nadal zawiera zniekształcone znaki, sprawdź ponownie, czy oryginalny TIFF nie ma zbyt niskiej rozdzielczości (zalecane minimum 300 dpi) oraz czy język jest poprawnie ustawiony w `ocrEngine.Settings.Language`.

## Pełny działający przykład (Wszystkie kroki w jednym miejscu)

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do nowego projektu konsolowego i od razu uruchomić.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // deskew image
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduce noise

        // 3️⃣ Load the image file (TIFF, JPEG, etc.)
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");

        // 4️⃣ Recognize text – filters run automatically
        var ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Zapisz plik jako `Program.cs`, uruchom `dotnet run`, a w terminalu powinien pojawić się wyczyszczony tekst.

## Najczęściej zadawane pytania i przypadki brzegowe

### Co zrobić, jeśli mój TIFF ma wiele stron?

Aspose OCR może przetwarzać obrazy wielostronicowe, iterując po `image.GetPages()` (lub używając `image.Pages`). Każda strona zwraca własny `OcrResult`. Połącz je przy pomocy `StringBuilder`, jeśli potrzebujesz jednego ciągu znaków.

### Czy filtr prostujący działa na mocno obróconych obrazach?

Obsługuje rotacje do około ±15°. Powyżej tego może być konieczne wstępne ręczne obrócenie obrazu przy użyciu biblioteki graficznej (np. `System.Drawing` lub `SkiaSharp`) przed przekazaniem go do Aspose.

### Jak mogę poprawić dokładność dla tekstu nie‑angielskiego?

Set the language explicitly:

```csharp
ocrEngine.Settings.Language = Language.English; // or Language.French, etc.
```

Możesz także załadować własne pakiety językowe, jeśli wbudowane nie obejmują Twojego alfabetu.

### Czy mogę uruchomić to na Linuksie?

Oczywiście. Aspose OCR jest wieloplatformowy; wystarczy upewnić się, że natywne zależności są dostępne (zwykle brak dla czystej wersji .NET). Użyj `dotnet publish -r linux-x64`, aby uzyskać samodzielny plik binarny.

## Bonus: Wizualizacja wyprostowanego obrazu

Jeśli chcesz zobaczyć poprawiony obraz przed OCR, możesz zapisać go z powrotem na dysk:

```csharp
// After OCR, the filtered image is stored in ocrEngine.Settings.FiltersResult
var corrected = ocrEngine.Settings.FiltersResult;
corrected.Save(@"output/deskewed_cleaned.tif");
```

![przykład prostowania obrazu](https://example.com/deskew-demo.png "przykład prostowania obrazu")

*Tekst alternatywny obrazu:* **przykład prostowania obrazu** – pokazuje przed/po obróceniu TIFF skorygowanym przez AutoDeskewFilter.

## Podsumowanie

Omówiliśmy **jak prostować obraz** plików, **jak redukować szum**, oraz cały proces **rozpoznawania tekstu z obrazu**, **ładowania obrazu z pliku** i **wyodrębniania tekstu z TIFF** przy użyciu Aspose OCR w C#. Najważniejsze? Dodanie zaledwie dwóch filtrów wstępnego przetwarzania może zamienić nieostre, ziarniste skany w wyraźny, przeszukiwalny dokument bez żadnych zewnętrznych narzędzi.

Gotowy na kolejny krok? Spróbuj zamienić `AutoDeskewFilter` na `AutoRotateFilter`, jeśli Twoje dokumenty są do góry nogami, lub poeksperymentuj z `ContrastEnhancementFilter` w przypadku wyblakłych wydruków. Ten sam schemat — silnik → filtry → ładowanie → rozpoznawanie — obowiązuje we wszystkich scenariuszach Aspose OCR, więc możesz ponownie wykorzystać tę bazę dla PDF‑ów, PNG‑ów czy nawet zdjęć z aparatu.

Miłego kodowania i niech Twój OCR zawsze będzie precyzyjny!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}