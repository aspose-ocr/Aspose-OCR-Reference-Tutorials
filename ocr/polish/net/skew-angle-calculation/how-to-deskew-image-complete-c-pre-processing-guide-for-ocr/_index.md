---
category: general
date: 2026-01-13
description: Jak prostować obraz i usuwać szumy obrazu w C# – dowiedz się, jak zwiększyć
  kontrast obrazu, przygotować go do OCR oraz zastosować wiele filtrów obrazu.
draft: false
keywords:
- how to deskew image
- remove image noise
- increase image contrast
- preprocess image ocr
- multiple image filters
language: pl
og_description: jak prostować obraz i usuwać szumy obrazu w C# – dowiedz się, jak
  zwiększyć kontrast obrazu, przygotować OCR obrazu oraz zastosować wiele filtrów
  obrazu
og_title: Jak wyprostować obraz – Kompletny przewodnik po przetwarzaniu wstępnym w
  C# dla OCR
tags:
- OCR
- C#
- Image Processing
title: Jak wyprostować obraz – Kompletny przewodnik po przetwarzaniu wstępnym w C#
  dla OCR
url: /pl/net/skew-angle-calculation/how-to-deskew-image-complete-c-pre-processing-guide-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak wyrównać obraz – Kompletny przewodnik przetwarzania wstępnego C# dla OCR

Zastanawiałeś się kiedyś **jak wyrównać obraz** przed przekazaniem go do silnika OCR? Nie jesteś sam. W wielu rzeczywistych scenariuszach — zeskanowane umowy, paragony czy stare fotokopie — tekst jest lekko pochyły, obraz jest ziarnisty, a kontrast jest nierównomierny. Dobra wiadomość? Kilka linijek kodu C# może wyprostować ten kąt, usunąć szumy obrazu i zwiększyć kontrast, dając Twojemu OCR solidną bazę.

W tym samouczku przejdziemy przez **kompletny, gotowy do uruchomienia przykład**, który pokaże dokładnie, jak wyrównać obraz, usunąć szumy, zwiększyć kontrast, a następnie wykonać OCR przy użyciu Aspose.OCR. Na końcu będziesz mieć wielokrotnego użytku pipeline, który stosuje **wiele filtrów obrazu** w jednym, płynnym wywołaniu — bez zgadywania.

## Czego będziesz potrzebować

- **.NET 6+** (lub dowolna nowsza wersja .NET; API działa tak samo)
- Pakiet NuGet **Aspose.OCR for .NET** (`Aspose.OCR` i `Aspose.OCR.Filters`)
- Przykładowy zeskanowany obraz (np. `skewed_noisy.png`) wykazujący pochylenie, szumy i niski kontrast
- Ulubione IDE (Visual Studio, Rider, VS Code — wybierz to, co jest dla Ciebie wygodne)

Jeśli masz już projekt, po prostu dodaj odwołanie NuGet:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Filters
```

> **Porada:** Aspose oferuje darmową wersję próbną z ograniczoną liczbą stron — idealną do wypróbowania poniższego kodu.

## Krok 1: Utwórz instancję silnika OCR

Pierwszą rzeczą, którą robimy, jest uruchomienie `OcrEngine`. Pomyśl o nim jak o mózgu, który później odczyta tekst. Nic skomplikowanego, ale to podstawa wszystkiego, co nastąpi.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();
```

> **Dlaczego to ważne:** Inicjalizacja silnika raz i ponowne jego użycie dla wielu obrazów eliminuje koszt wielokrotnego ładowania danych językowych.

## Krok 2: Załaduj surowy zeskanowany obraz

Następnie pobieramy obraz z dysku. Metoda `OcrImage.FromFile` odczytuje plik do formatu, którym Aspose może manipulować.

```csharp
        // Step 2: Load the raw scanned image (skewed, noisy, low‑contrast)
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");
```

> **Przypadek brzegowy:** Jeśli Twój obraz jest w niestandardowym formacie (TIFF, BMP), Aspose i tak go obsłuży, ale możesz chcieć najpierw przekonwertować go na PNG dla spójności.

## Krok 3: Zbuduj pipeline przetwarzania wstępnego (Wyrównanie → Usuwanie szumów → Kontrast)

Tutaj odpowiadamy na główne pytanie **jak wyrównać obraz** oraz **usunąć szumy obrazu** i **zwiększyć kontrast obrazu**. Płynne API Aspose pozwala łączyć filtry razem, dzięki czemu kod czyta się jak zdanie.

```csharp
        // Step 3: Apply Deskew, Denoise, and Contrast filters in one pipeline
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())      // Corrects rotation
            .ApplyFilter(new DenoiseFilter())     // Reduces grainy artifacts
            .ApplyFilter(new ContrastFilter());   // Boosts foreground/background separation
```

### Co robi każdy filtr

| Filtr | Cel | Typowy wpływ |
|--------|---------|----------------|
| **DeskewFilter** | Wykrywa kąt linii tekstu i obraca obraz, aby były poziome. | Usuwa pochylenie, które myli OCR, często obniżając wskaźnik błędów o 30‑50 %. |
| **DenoiseFilter** | Stosuje algorytm wygładzania zachowujący krawędzie, jednocześnie usuwający losowy szum pikseli. | Czyści zeskanowane paragony lub zdjęcia przy słabym oświetleniu, sprawiając, że znaki są wyraźniejsze. |
| **ContrastFilter** | Rozciąga histogram, tak że ciemne obszary stają się ciemniejsze, a jasne jaśniejsze. | Poprawia rozróżnienie tekstu i tła, szczególnie przy przygasłych dokumentach. |

> **Dlaczego łączyć?** Najpierw wyrównanie zapewnia, że filtr odszumiania działa na prawidłowo skierowanym obrazie; podniesienie kontrastu na końcu sprawia, że wyczyszczony tekst „wyskakuje” przed silnikiem OCR.

## Krok 4: Wykonaj OCR na przetworzonym obrazie

Teraz, gdy obraz jest prosty, czysty i o wysokim kontraście, przekazujemy go silnikowi OCR. Użyjemy danych językowych angielskiego, ale Aspose obsługuje ponad 150 języków.

```csharp
        // Step 4: Recognize text using the English language pack
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);
```

Jeśli potrzebujesz innego języka, po prostu zamień `OcrLanguage.English` na odpowiednią wartość wyliczenia (np. `OcrLanguage.Spanish`).

## Krok 5: Wyświetl rozpoznany tekst

Na koniec wypisujemy wynik na konsolę. W prawdziwej aplikacji możesz zapisać go do pliku, bazy danych lub przekazać do dalszych pipeline’ów NLP.

```csharp
        // Step 5: Display the recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Oczekiwany wynik

Uruchomienie pełnego programu na typowym pochyłym paragonie daje coś w stylu:

```
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
Thank you for your business!
```

Jeśli wynik jest zniekształcony, sprawdź oryginalny obraz — nadmierne rozmycie lub skrajna ciemność mogą wymagać dodatkowego przetwarzania (np. filtru SharpenFilter).

![przykład jak wyrównać obraz](images/deskewed_example.png "jak wyrównać obraz – przed i po przetworzeniu")

*Powyższy obraz pokazuje oryginalny, pochyły skan po lewej oraz poprawioną, odszumioną i o wysokim kontraście wersję po prawej.*

## Dodatkowe wskazówki i typowe pułapki

### 1. Gdy kąt pochylenia jest skrajny

Jeśli dokument jest nachylony o więcej niż 30°, `DeskewFilter` może mieć trudności. W takim wypadku obróć obraz ręcznie:

```csharp
var manuallyRotated = rawImage.Rotate(45); // rotates 45 degrees clockwise
var processed = manuallyRotated.ApplyFilter(new DeskewFilter());
```

### 2. Obsługa obrazów kolorowych

Filtry działają wewnętrznie na odcieniach szarości, ale możesz wymusić konwersję:

```csharp
var grayImage = rawImage.ConvertToGrayscale();
var processed = grayImage.ApplyFilter(new DeskewFilter());
```

### 3. Dostosowywanie siły odszumiania

`DenoiseFilter` przyjmuje opcjonalny parametr `strength` (0‑100). Wyższe wartości usuwają więcej szumu, ale mogą rozmywać drobne szczegóły.

```csharp
.ApplyFilter(new DenoiseFilter(strength: 70))
```

### 4. Używanie wielu filtrów obrazu poza podstawowymi

Aspose dostarcza wiele dodatkowych filtrów: `SharpenFilter`, `BinarizeFilter`, `ResizeFilter` itd. Możesz je mieszać, tworząc własny pipeline dopasowany do konkretnego typu dokumentu.

```csharp
var processed = rawImage
    .ApplyFilter(new DeskewFilter())
    .ApplyFilter(new DenoiseFilter())
    .ApplyFilter(new BinarizeFilter())
    .ApplyFilter(new SharpenFilter());
```

## Pełny działający przykład (Gotowy do kopiowania)

Poniżej znajduje się cały program, gotowy do wstawienia do projektu konsolowego.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Load the original scanned image
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");

        // Build preprocessing pipeline: Deskew → Denoise → Contrast
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())
            .ApplyFilter(new DenoiseFilter())
            .ApplyFilter(new ContrastFilter());

        // Run OCR using English language
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);

        // Output recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

Uruchom program poleceniem `dotnet run`. Jeśli wszystko jest poprawnie skonfigurowane, konsola wyświetli czysty, czytelny tekst wyodrębniony z pierwotnie pochyłego i zaszumionego obrazu.

## Zakończenie

Właśnie omówiliśmy **jak wyrównać obraz** w C# jednocześnie **usuwając szumy**, **zwiększając kontrast** i **przetwarzając obraz pod OCR** przy użyciu łańcucha **wielu filtrów obrazu**. Najważniejszą lekcją jest to, że dobrze uporządkowany pipeline przetwarzania wstępnego może dramatycznie poprawić dokładność OCR — często zamieniając ledwo czytelny skan w perfekcyjnie czytelny tekst.

Gotowy na kolejny krok? Spróbuj zamienić `ContrastFilter` na `BinarizeFilter`, aby zobaczyć, jak konwersja do trybu czarno‑białego wpływa na wyniki, lub poeksperymentuj z `ResizeFilter`, aby podać silnikowi obraz o wyższej rozdzielczości. Ten sam wzorzec działa niezależnie od wybranych filtrów, więc masz elastyczną bazę dla wszystkich przyszłych projektów OCR.

Masz pytania dotyczące obsługi PDF‑ów, wielojęzycznego OCR lub integracji tego rozwiązania w API ASP.NET? Zostaw komentarz poniżej i powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}