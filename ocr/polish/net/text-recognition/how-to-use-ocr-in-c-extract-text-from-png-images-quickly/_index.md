---
category: general
date: 2026-03-29
description: Jak używać OCR z Aspose do wyodrębniania tekstu z plików PNG i konwertowania
  obrazów na tekst. Naucz się krok po kroku asynchronicznego OCR w C#.
draft: false
keywords:
- how to use OCR
- extract text from png
- convert images to text
- extract text from images
language: pl
og_description: Jak używać OCR z Aspose w C#, aby wyodrębnić tekst z plików PNG. Ten
  przewodnik przeprowadzi Cię przez asynchroniczny OCR, kod i wskazówki.
og_title: Jak używać OCR w C# – wyodrębnianie tekstu z obrazów PNG
tags:
- OCR
- C#
- Aspose
title: Jak używać OCR w C# – Szybko wyodrębniaj tekst z obrazów PNG
url: /pl/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-png-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać OCR w C# – Szybko wyodrębniaj tekst z obrazów PNG

Zastanawiałeś się kiedyś **jak używać OCR**, aby wyciągnąć tekst z kilku zrzutów ekranu PNG? Może masz zeskanowane paragony, faktury lub makiety UI i potrzebujesz tego tekstu w formacie przeszukiwalnym. Dobre wieści? Dzięki Aspose.OCR możesz konwertować obrazy na tekst w zaledwie kilku linijkach asynchronicznego kodu C#.

W tym samouczku pokażemy dokładnie, jak wyodrębnić tekst z plików PNG, wyjaśnimy, dlaczego każdy krok ma znaczenie, i dostarczymy gotowy do uruchomienia program, który wypisuje rozpoznany tekst dla każdej strony. Po zakończeniu będziesz w stanie **wyodrębniać tekst z obrazów** bez przeszukiwania dokumentacji.

## Co się nauczysz

- Zainstaluj i odwołaj się do pakietu NuGet Aspose.OCR.  
- Zainicjalizuj silnik OCR i ustaw język (angielski w tym przykładzie).  
- Przekaż tablicę plików PNG do `RecognizeImagesAsync` w celu szybkiego, nieblokującego przetwarzania.  
- Przejdź przez obiekty `OcrResult` i wypisz wyodrębnione ciągi znaków.  

Bez zewnętrznych usług, bez skomplikowanych wywołań zwrotnych — po prostu czysty, asynchroniczny C#, który działa na .NET 6+.

---

## Wymagania wstępne

| Wymaganie | Powód |
|-------------|--------|
| .NET 6 SDK (or later) | Nowoczesne funkcje językowe, takie jak `async Main`. |
| Visual Studio 2022 or VS Code | IDE do kompilacji i uruchamiania kodu. |
| Aspose.OCR NuGet package (`Aspose.OCR`) | Dostarcza klasę `OcrEngine` używaną w przykładzie. |
| A few PNG images (`page1.png`, `page2.png`, …) | Pliki wejściowe dla procesu OCR. |

Jeśli już masz projekt .NET, po prostu uruchom `dotnet add package Aspose.OCR`. W przeciwnym razie utwórz nową aplikację konsolową za pomocą `dotnet new console -n OcrDemo`.

---

## Krok 1: Zainstaluj Aspose.OCR i skonfiguruj projekt

Najpierw dodaj bibliotekę OCR do swojego projektu:

```bash
dotnet add package Aspose.OCR
```

Dlaczego to ważne: Aspose.OCR zawiera natywny silnik OCR, pakiety językowe oraz prostą API. Pobierając go przez NuGet zapewniasz zgodność wersji i automatyczne aktualizacje.

---

## Krok 2: Zainicjalizuj silnik OCR i wybierz język

Silnik musi wiedzieć, jakiego języka szukać. Angielski jest najczęstszy, ale możesz zamienić na `Language.Spanish`, `Language.French` itd.

```csharp
using Aspose.OCR;

// ...

// Step 2: Create the engine and set the language to English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // Change this if you need a different language
};
```

> **Porada:** Zawsze ustawiaj język explicite; pozostawienie domyślnego może obniżyć dokładność i wydłużyć czas przetwarzania.

---

## Krok 3: Przygotuj listę plików PNG

Możesz podać pojedynczy plik lub tablicę. Dostarczenie tablicy pozwala silnikowi przetwarzać je wsadowo asynchronicznie, co jest idealne dla kilku stron.

```csharp
// Step 3: Define the image files you want to process
string[] imagePaths = { "page1.png", "page2.png", "page3.png" };
```

Jeśli Twoje obrazy znajdują się w podfolderze, po prostu poprzedź je ścieżką względną (`"images/page1.png"`). Silnik wyrzuci wyraźny `FileNotFoundException`, jeśli ścieżka jest nieprawidłowa — więc sprawdź dwukrotnie nazwy plików.

---

## Krok 4: Uruchom asynchroniczny OCR na wszystkich obrazach

Metoda `RecognizeImagesAsync` zwraca tablicę `OcrResult`. Ponieważ jest asynchroniczna, Twój interfejs (lub konsola) pozostaje responsywny, podczas gdy OCR działa w tle.

```csharp
// Step 4: Perform async OCR on every image
OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);
```

**Dlaczego async?**  
Jeśli integrujesz OCR z API webowym lub aplikacją desktopową, nie chcesz, aby wątek był zablokowany podczas skanowania każdego piksela przez silnik. `await` zwalnia wątek z powrotem do puli wątków, zwiększając skalowalność.

---

## Krok 5: Wyświetl wyodrębniony tekst dla każdej strony

Teraz, gdy mamy wyniki, iteruj po nich i wypisz rozpoznany tekst. Właściwość `Text` zawiera wynik w postaci zwykłego tekstu, gotowego do dalszego przetwarzania (np. zapisu w bazie danych).

```csharp
// Step 5: Output the recognized text for every page
for (int i = 0; i < ocrResults.Length; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

### Oczekiwany wynik

Zakładając, że `page1.png` zawiera „Invoice #12345”, a `page2.png` zawiera „Total: $89.99”, zobaczysz coś w rodzaju:

```
--- Page 1 ---
Invoice #12345
Date: 03/28/2026
--- Page 2 ---
Total: $89.99
Paid by: Credit Card
```

Jeśli OCR nie znajdzie żadnego tekstu, właściwość `Text` będzie pustym ciągiem — obsłuż ten przypadek w kodzie produkcyjnym, sprawdzając `string.IsNullOrWhiteSpace`.

---

## Pełny działający przykład

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do `Program.cs`. Zawiera wszystkie dyrektywy using, asynchroniczny `Main` oraz komentarze wyjaśniające każdy krok.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    // Async Main is supported from C# 7.1 onward
    static async Task Main()
    {
        // Step 1: Initialize the OCR engine and set the language to English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Step 2: Define the image files to be processed
        string[] imagePaths = { "page1.png", "page2.png", "page3.png" };

        // Step 3: Perform asynchronous OCR on all images
        OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);

        // Step 4: Output the recognized text for each page
        for (int i = 0; i < ocrResults.Length; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].Text);
        }
    }
}
```

Zapisz plik, umieść swoje PNG‑y obok pliku wykonywalnego (lub dostosuj ścieżki) i uruchom:

```bash
dotnet run
```

Powinieneś zobaczyć wyodrębniony tekst wypisany w konsoli, co potwierdza, że pomyślnie **przekonwertowałeś obrazy na tekst**.

---

## Obsługa typowych przypadków brzegowych

| Sytuacja | Co zrobić |
|-----------|------------|
| **Low‑resolution PNG** | Zwiększ `ocrEngine.ImageProcessingOptions.Dpi` przed rozpoznaniem. |
| **Multiple languages** | Ustaw `ocrEngine.Language = Language.English | Language.Spanish;` (operacja bitowa OR). |
| **Large batch (hundreds of files)** | Przetwarzaj w partiach (np. 20 plików na wywołanie `RecognizeImagesAsync`), aby uniknąć skoków pamięci. |
| **Need the confidence score** | Użyj `ocrResults[i].Confidence` (liczba zmiennoprzecinkowa od 0 do 1), aby odfiltrować wyniki niskiej jakości. |

Te drobne poprawki utrzymują Twój pipeline OCR w dobrej kondycji, szczególnie gdy przechodzisz od demonstracji do produkcji.

---

## Bonus: Zapisywanie wyników do pliku tekstowego

Jeśli wolisz trwałą kopię zamiast wyjścia w konsoli, dodaj mały pomocnik:

```csharp
using System.IO;

// After the for‑loop:
File.WriteAllLines("OcrOutput.txt", ocrResults.Select(r => r.Text));
Console.WriteLine("All pages saved to OcrOutput.txt");
```

Teraz masz pojedynczy plik, który **wyodrębnia tekst z obrazów** do dalszego przetwarzania — idealny do indeksowania, wyszukiwania lub podawania do modelu językowego.

---

## Zakończenie

Przeszliśmy przez **jak używać OCR** w C# z Aspose, aby **wyodrębniać tekst z plików PNG** i **konwertować obrazy na tekst** efektywnie. Podejście async zapewnia, że Twoja aplikacja pozostaje responsywna, a prosta API utrzymuje kod czytelnym i łatwym w utrzymaniu.

Wypróbuj to na własnych dokumentach, eksperymentuj z różnymi językami i może nawet połącz wynik z indeksem wyszukiwania lub usługą podsumowującą. Nie ma granic, gdy możesz niezawodnie zamienić obrazy w przeszukiwalne ciągi znaków.

### Kolejne kroki i powiązane tematy

- **Wyodrębniaj tekst z obrazów** w innych formatach (JPEG, TIFF) — po prostu zmień rozszerzenia plików.  
- **Przetwarzanie wsadowe przy użyciu Parallel.ForEach** dla ogromnych obciążeń.  
- **Czyszczenie po OCR** przy użyciu wyrażeń regularnych w celu normalizacji dat, kwot lub identyfikatorów.  
- **Integracja z Azure Cognitive Services** jeśli potrzebujesz OCR w chmurze z dodatkowymi funkcjami.  

Śmiało zostaw komentarz, jeśli napotkasz problemy, lub podziel się, jak rozbudowałeś ten podstawowy przepływ. Szczęśliwego kodowania!   (Image: ![OCR result screenshot showing extracted text](/images/ocr-result.png){.align-center alt="jak używać OCR przykład wyjścia"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}