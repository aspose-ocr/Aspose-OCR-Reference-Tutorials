---
category: general
date: 2025-12-30
description: Jak szybko wyrównać obraz i dowiedzieć się, jak zwiększyć kontrast podczas
  wyodrębniania tekstu z obrazu w celu poprawy dokładności OCR.
draft: false
keywords:
- how to deskew image
- how to boost contrast
- extract text from image
- recognize text image
- improve ocr accuracy
language: pl
og_description: Jak szybko prostować obraz i dowiedzieć się, jak zwiększyć kontrast
  podczas wyodrębniania tekstu z obrazu, aby poprawić dokładność OCR.
og_title: Jak wyprostować obraz i zwiększyć kontrast dla lepszej dokładności OCR
tags:
- OCR
- C#
- Image Processing
title: Jak wyprostować obraz i zwiększyć kontrast dla lepszej dokładności OCR
url: /pl/net/ocr-optimization/how-to-deskew-image-and-boost-contrast-for-better-ocr-accura/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak prostować obraz i zwiększyć kontrast dla lepszej dokładności OCR

Zastanawiałeś się kiedyś, **jak prostować obraz** pochodzący ze skanera lub smartfona?  
Nie jesteś sam — większość programistów napotyka ten problem, gdy źródłowe zdjęcie jest nieco przechylone lub zaszumione, a wynik OCR jest nieczytelny.  

Dobrą wiadomością jest to, że kilka linijek C# pozwala wyprostować obraz, oczyścić tło i nawet podnieść kontrast, aby silnik czytał tekst jak profesjonalista. W tym przewodniku pokażemy również, jak **wyodrębnić tekst z obrazu** oraz **rozpoznawać treść obrazu tekstowego** przy użyciu Aspose.OCR, jednocześnie koncentrując się na **poprawie dokładności OCR**.

## Czego będziesz potrzebować

- **.NET 6.0** lub nowszy (kod kompiluje się również na .NET Framework 4.7+)  
- Pakiet NuGet **Aspose.OCR** (wersja 23.12 lub nowsza) – zainstaluj za pomocą `dotnet add package Aspose.OCR`  
- Przykładowy obraz, który jest jednocześnie obrócony i zaszumiony (np. `noisy_rotated.jpg`)  
- Visual Studio, VS Code lub dowolne IDE, które preferujesz  

To wszystko — bez dodatkowych natywnych bibliotek, bez ciężkich powiązań OpenCV. Tylko czysty kod zarządzany.

---

## Krok 1: Konfiguracja projektu i importowanie przestrzeni nazw

Najpierw utwórz nową aplikację konsolową i wprowadź wymagane przestrzenie nazw do zasięgu. Ten krok jest fundamentem dla wszystkiego, co nastąpi.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later
        }
    }
}
```

**Dlaczego to ważne:**  
`Aspose.OCR` udostępnia klasę `OcrEngine`, natomiast `Aspose.OCR.Filters` zapewnia przydatne filtry wstępnego przetwarzania, takie jak `DeskewFilter` i `ContrastBoostFilter`. Importowanie ich na początku utrzymuje kod w porządku i sygnalizuje kompilatorowi, co zamierzamy używać.

---

## Krok 2: Inicjalizacja silnika OCR i dodanie filtra prostowania

Teraz faktycznie **jak prostować obraz**. `DeskewFilter` automatycznie wykrywa kąt obrotu (do maksymalnej wartości, którą ustawisz) i obraca bitmapę z powrotem do poziomu.

```csharp
// Inside Main()
var ocrEngine = new OcrEngine();

// Deskew: correct up to 15 degrees of rotation
ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });
```

**Co się dzieje w tle?**  
Filtr przeszukuje obraz w poszukiwaniu najdłuższej poziomej linii tekstu, szacuje przechylenie i stosuje odwrotny obrót. Ograniczając `MaxAngle` do 15°, unikamy nadmiernej korekcji obrazów, które już są proste.

> **Wskazówka:** Jeśli Twoje obrazy źródłowe mogą być do góry nogami, zwiększ `MaxAngle` do 180° — filtr nadal znajdzie właściwą orientację.

---

## Krok 3: Redukcja szumu za pomocą filtra odszumiania

Zaszumione skany mogą oszukać nawet najinteligentniejszy silnik OCR. Dodanie `DenoiseFilter` wygładza plamki bez usuwania drobnych szczegółów.

```csharp
// Denoise: strength ranges from 0 (off) to 1 (max)
ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });
```

**Dlaczego jest potrzebny:**  
Szum tworzy fałszywe krawędzie, które algorytm OCR interpretuje jako znaki. Siła `0.7` jest optymalna dla większości zeskanowanych dokumentów; możesz ją dostosować dla bardzo czystych lub bardzo brudnych wejść.

---

## Krok 4: Zwiększanie kontrastu – „Jak zwiększyć kontrast” w praktyce

Tutaj odpowiadamy na drugie słowo kluczowe **jak zwiększyć kontrast**. `ContrastBoostFilter` wzmacnia różnicę między ciemnym tekstem a jasnym tłem, sprawiając, że litery wyróżniają się.

```csharp
// Contrast boost: level > 1 increases contrast
ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });
```

**Uzasadnienie:**  
Wyższy kontrast zmniejsza ryzyko pominięcia słabych kresek. Poziom `1.3` sprawdza się dobrze w typowych dokumentach czarno‑białych; w przypadku zdjęć kolorowych może być potrzebny `1.5` lub więcej.

---

## Krok 5: Uruchomienie OCR i wyodrębnienie tekstu

Po wstępnym przetworzeniu obrazu w końcu **wyodrębniamy tekst z obrazu** przy użyciu metody `Recognize`. Metoda zwraca obiekt `OcrResult`, który zawiera surowy ciąg znaków oraz wyniki pewności.

```csharp
// Perform OCR on the prepared image
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/noisy_rotated.jpg");

// Output the recognized text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**Co otrzymujesz:**  
`ocrResult.Text` zawiera tekstową reprezentację wszystkiego, co silnik mógł odczytać. Jeśli potrzebujesz pewności na poziomie słowa, przyjrzyj się `ocrResult.Regions` — każdy region zawiera właściwość `Confidence`.

---

## Pełny działający przykład (gotowy do kopiowania i wklejenia)

Poniżej znajduje się kompletny program, który możesz wkleić do `Program.cs`. Upewnij się, że ścieżka do obrazu wskazuje na rzeczywisty plik w Twoim systemie.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Deskew – correct up to 15° rotation
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });

            // 3️⃣ Denoise – smooth out speckles (strength 0.7)
            ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });

            // 4️⃣ Contrast boost – make text pop (level 1.3)
            ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });

            // 5️⃣ Recognize the image
            var imagePath = @"YOUR_DIRECTORY\noisy_rotated.jpg";
            var ocrResult = ocrEngine.Recognize(imagePath);

            // 6️⃣ Show the result
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Oczekiwany wynik (przykład):**

```
=== OCR Output ===
Invoice #12345
Date: 2024-09-30
Total Amount: $1,250.00
Thank you for your business!
```

Jeśli wynik wygląda na zniekształcony, sprawdź jakość obrazu, dostosuj `Strength` lub `Level`, albo zwiększ `MaxAngle` dla bardziej agresywnego prostowania.

---

## Częste pytania i przypadki brzegowe

### Co zrobić, gdy obraz jest do góry nogami?

Ustaw `MaxAngle = 180` w `DeskewFilter`. Filtr wykryje obrót o 180° i poprawnie go odwróci.

### Mój dokument jest kolorowy (np. zeskanowany formularz z niebieskimi podświetleniami).

Spróbuj dodać `ColorFilter` przed zwiększeniem kontrastu lub ręcznie przekonwertować obraz na odcienie szarości:

```csharp
ocrEngine.Filters.Add(new GrayscaleFilter());
```

### Muszę przetworzyć wiele plików w partii.

Umieść logikę OCR w pętli `foreach`, która iteruje po katalogu:

```csharp
foreach (var file in Directory.GetFiles(@"C:\Scans", "*.jpg"))
{
    var result = ocrEngine.Recognize(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), result.Text);
}
```

### Jak sprawdzić pewność OCR?

Sprawdź `ocrResult.Regions`:

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"Text: {region.Text} – Confidence: {region.Confidence:P2}");
}
```

Wyższe wartości pewności (bliskie 100%) zazwyczaj oznaczają, że kroki wstępnego przetwarzania zakończyły się sukcesem.

---

## Wskazówki zwiększające dokładność OCR

| Wskazówka | Dlaczego pomaga |
|-----|--------------|
| **Używaj bezstratnych formatów obrazu** (PNG, TIFF) | Kompresja JPEG może rozmywać krawędzie, co utrudnia rozpoznawanie. |
| **Utrzymuj DPI na poziomie 300+** | Więcej pikseli na znak daje silnikowi więcej danych do analizy. |
| **Przytnij nieistotne marginesy** | Redukuje szum i przyspiesza przetwarzanie. |
| **Zastosuj progowanie binarne** (czarno‑białe) po zwiększeniu kontrastu dla czystych dokumentów tekstowych | Upraszcza obraz do dwóch kolorów, co większość silników OCR uwielbia. |
| **Najpierw przetestuj na małej próbce** | Pozwala precyzyjnie dostroić `Strength` i `Level` przed skalowaniem. |

---

## Podsumowanie

Przeszliśmy przez **jak prostować obraz** pliki, **jak zwiększyć kontrast** oraz pełny proces **wyodrębniania tekstu z obrazu** przy użyciu Aspose.OCR. Łącząc `DeskewFilter`, `DenoiseFilter` i `ContrastBoostFilter` przed wywołaniem `Recognize`, zauważysz wyraźny wzrost **poprawy dokładności OCR** dla większości rzeczywistych skanów.

Uruchom kod, dostosuj parametry filtrów do własnych specyficznych dokumentów i w krótkim czasie będziesz wyciągać czysty tekst nawet z najbardziej niechlujnych zdjęć. Chcesz iść dalej? Spróbuj dodać słowniki specyficzne dla języka lub poddać wynik sprawdzaniu pisowni w post‑processingu.

Szczęśliwego kodowania i niech wyniki OCR będą zawsze krystalicznie czyste! 

--- 

![przykład prostowania obrazu](deskew_example.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}