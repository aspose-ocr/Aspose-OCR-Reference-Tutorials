---
category: general
date: 2026-04-29
description: jak wyprostować obraz i zwiększyć dokładność OCR przy użyciu Aspose OCR
  – dowiedz się, jak usunąć szumy, zwiększyć kontrast obrazu i wyodrębnić tekst z
  obrazów.
draft: false
keywords:
- how to deskew image
- remove noise from image
- boost image contrast
- extract text from image
- improve ocr accuracy
language: pl
og_description: Jak prostować obraz i poprawić dokładność OCR. Ten tutorial pokazuje,
  jak usunąć szumy z obrazu, zwiększyć kontrast obrazu i wyodrębnić tekst z obrazu
  przy użyciu Aspose OCR.
og_title: jak wyprostować obraz – Kompletny przewodnik Aspose OCR
tags:
- Aspose OCR
- C#
- Image preprocessing
title: Jak wyprostować obraz – przewodnik przetwarzania wstępnego Aspose OCR
url: /pl/net/ocr-optimization/how-to-deskew-image-aspose-ocr-preprocessing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak prostować obraz – Kompletny przewodnik Aspose OCR

Zastanawiałeś się kiedyś **jak prostować obraz** przed przekazaniem go do silnika OCR? Nie jesteś jedyny. Krzywy skan lub zdjęcie zrobione pod kątem może zaburzyć rozpoznawanie tekstu, pozostawiając Cię z nieczytelnym wynikiem.  

W tym samouczku przeprowadzimy Cię przez kompletną, kompleksową (end‑to‑end) rozwiązanie, które nie tylko **jak prostować obraz**, ale także **usuwać szum z obrazu**, **zwiększać kontrast obrazu**, a ostatecznie **wyodrębniać tekst z obrazu** przy użyciu Aspose OCR. Po zakończeniu zobaczysz, jak **poprawić dokładność OCR** bez przeszukiwania dokumentacji.

> **Co otrzymasz:** gotową do uruchomienia aplikację konsolową C#, jasne wyjaśnienie każdego kroku przetwarzania wstępnego oraz garść praktycznych wskazówek, które możesz skopiować i wkleić do własnych projektów.

## Prerequisites

- .NET 6.0 lub nowszy (kod działa również z .NET Core i .NET Framework)  
- Pakiet NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Przykładowy obraz, który jest przechylony, zaszumiony lub o niskim kontraście (np. `skewed_noisy.jpg`)  
- Visual Studio, VS Code lub dowolny edytor C#, którego preferujesz  

Nie są wymagane dodatkowe natywne biblioteki – Aspose obsługuje wszystko w procesie.

---

## Jak prostować obraz przy użyciu Aspose OCR

Pierwszą rzeczą, której potrzebujemy, jest filtr prostujący kąt obrotu. Aspose OCR dostarcza `FilterDeskew`, który analizuje linie bazowe tekstu i odpowiednio obraca bitmapę.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that will later recognize text.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Build an image‑processing pipeline.
        //    The order matters: deskew → denoise → contrast boost.
        ImageProcessingPipeline processingPipeline = new ImageProcessingPipeline();
        processingPipeline.Add(new FilterDeskew());          // ✅ how to deskew image
        processingPipeline.Add(new FilterDenoise());         // ✅ remove noise from image
        processingPipeline.Add(new FilterContrastBoost());   // ✅ boost image contrast

        // 3️⃣ Load your source picture.
        var sourceImage = OcrEngine.LoadImage(@"YOUR_DIRECTORY/skewed_noisy.jpg");

        // 4️⃣ Apply the pipeline – the image is now straight, cleaner, and sharper.
        var processedImage = processingPipeline.Apply(sourceImage);

        // 5️⃣ Run OCR on the cleaned‑up bitmap.
        var ocrResult = ocrEngine.Recognize(processedImage);

        // 6️⃣ Print the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Dlaczego zaczynamy od prostowania:**  
Jeśli linie tekstu nie są poziome, silnik OCR spróbuje interpretować pochyłe znaki jako inne glify, co dramatycznie obniża **poprawić dokładność OCR**. Prostowanie wyrównuje linie bazowe, dając rozpoznawaczowi czyste płótno.

> *Pro tip:* Jeśli znasz kąt obrotu z góry (np. wszystkie skany są odchylone o 90°), możesz pominąć filtr i obrócić ręcznie – to mały zysk wydajności.

---

## Usuwanie szumu z obrazu – Czyszczenie skanu

Szum pojawia się jako losowe czarne lub białe plamki (klasyczny wzór „sól i pieprz”) i może mylić segmentację znaków. `FilterDenoise` stosuje filtr medianowy, który wygładza je, zachowując krawędzie.

```csharp
// Inside the pipeline we already added FilterDenoise.
// If you need a custom strength, you can instantiate it like:
var denoise = new FilterDenoise { Strength = 2 }; // 1‑3 are typical values
processingPipeline.Add(denoise);
```

**Kiedy dostosować siłę:**  
- **Strength = 1** – Lekka ziarnistość, szybkie przetwarzanie.  
- **Strength = 3** – Bardzo zaszumione skany (np. dokumenty faksowane).  

Zbyt duże zwiększenie siły może rozmyć cienkie kreski, co może *zaszkodzić* **poprawić dokładność OCR**. Przetestuj kilka wartości na reprezentatywnej próbce.

## Zwiększanie kontrastu obrazu – Podkreślanie słabych znaków

Obrazy o niskim kontraście (np. wyblakłe paragony) często powodują, że silnik OCR pomija lekkie glify. `FilterContrastBoost` rozciąga histogram, tak aby ciemne piksele stały się ciemniejsze, a jasne jaśniejsze.

```csharp
var contrast = new FilterContrastBoost { ContrastLevel = 1.5f }; // 1.0 = no change
processingPipeline.Add(contrast);
```

**Dlaczego kontrast ma znaczenie:**  
Wyższy kontrast poprawia stosunek sygnału do szumu, ułatwiając rozpoznawaczowi neuronowemu Aspose odróżnienie „I” od „l”. Jednak nadmierne zwiększenie może nasycić obraz, zamieniając płynne gradienty w ostre krawędzie wyglądające jak artefakty. Dąż do równowagi; 1.5‑2.0 to dobry punkt wyjścia.

## Wyodrębnianie tekstu z obrazu – Ostateczny krok OCR

Teraz, gdy obraz jest prosty, czysty i wyraźny, silnik OCR może wykonać swoją pracę. Metoda `Recognize` zwraca obiekt `OcrResult` zawierający surowy tekst, wyniki pewności oraz nawet ramki ograniczające, jeśli są potrzebne.

```csharp
var ocrResult = ocrEngine.Recognize(processedImage);
Console.WriteLine(ocrResult.Text);
```

**Przykładowe wyjście** (zakładając, że źródłowy obraz zawiera „Invoice #12345”):

```
=== OCR Output ===
Invoice #12345
Date: 04/28/2026
Total: $1,234.56
```

Jeśli zauważysz brakujące znaki, ponownie sprawdź pipeline przetwarzania wstępnego – być może obraz nadal wymaga silniejszego odszumiania lub innego poziomu kontrastu.  

> *Częste pytanie:* „Co jeśli muszę rozpoznawać język inny niż angielski?”  
> Po prostu ustaw `ocrEngine.Language = Language.English;` na inny obsługiwany język (np. `Language.French`). Kroki przetwarzania wstępnego pozostają takie same.

## Poprawa dokładności OCR – Dodatkowe ustawienia

Nawet przy idealnym pipeline, kilka dodatkowych ustawień może jeszcze bardziej zwiększyć **poprawić dokładność OCR**:

| Tip | Kiedy używać | Jak |
|-----|--------------|-----|
| **Binary Thresholding** | Very dark or very light scans | `processingPipeline.Add(new FilterBinarize());` |
| **Resize Image** | Small fonts (<10 pt) | `processedImage = OcrEngine.Resize(processedImage, 2.0);` |
| **Specify Character Set** | Known alphabet (digits only, etc.) | `ocrEngine.Characters = "0123456789";` |
| **Multi‑page PDFs** | Batch processing | Loop over each page and reuse the same pipeline. |

Pamiętaj: każdy dodatkowy filtr zwiększa czas przetwarzania, więc włączaj tylko te, które naprawdę potrzebujesz.

---

## Pełny działający przykład (gotowy do kopiowania i wklejania)

Poniżej znajduje się cały program, gotowy do kompilacji. Zastąp `YOUR_DIRECTORY` folderem, w którym znajduje się `skewed_noisy.jpg`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Build preprocessing pipeline
        ImageProcessingPipeline pipeline = new ImageProcessingPipeline();
        pipeline.Add(new FilterDeskew());                     // how to deskew image
        pipeline.Add(new FilterDenoise { Strength = 2 });    // remove noise from image
        pipeline.Add(new FilterContrastBoost { ContrastLevel = 1.8f }); // boost image contrast

        // Load source image
        var sourcePath = @"YOUR_DIRECTORY/skewed_noisy.jpg";
        var sourceImage = OcrEngine.LoadImage(sourcePath);

        // Apply pipeline
        var cleanImage = pipeline.Apply(sourceImage);

        // Perform OCR
        var result = ocrEngine.Recognize(cleanImage);

        // Output
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(result.Text);
    }
}
```

**Oczekiwany wynik:** Czysty, wyprostowany tekst wydrukowany w konsoli, z znacznie mniejszą liczbą błędów rozpoznawania niż podanie surowego pliku bezpośrednio do `ocrEngine.Recognize`.

---

## Zakończenie

Omówiliśmy **jak prostować obraz**, jak **usuwać szum z obrazu**, jak **zwiększać kontrast obrazu**, a w końcu jak **wyodrębniać tekst z obrazu** przy użyciu Aspose OCR. Łącząc te filtry, zauważysz wyraźny wzrost **poprawić dokładność OCR**, szczególnie przy skanach niskiej jakości.

Gotowy na kolejne wyzwanie? Spróbuj podać wielostronicowy PDF do tego samego pipeline lub eksperymentuj z własnymi progami binaryzacji. Te same zasady obowiązują – prostuj, czyść, rozjaśniaj, a potem rozpoznawaj.

Masz pytania lub nietypowy przypadek? Dodaj komentarz, a wspólnie rozwiążemy problem. Szczęśliwego kodowania!  

![przykład prostowania obrazu](deskew-example.png "przykład prostowania obrazu")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}