---
category: general
date: 2026-02-14
description: Jak używać OCR w C#, aby szybko wyodrębniać tekst z plików PNG. Dowiedz
  się, jak przetwarzać obrazy OCR w trybie wsadowym, obsługiwać wiele obrazów i korzystać
  z Aspose OCR w C# w jednym przewodniku.
draft: false
keywords:
- how to use OCR
- extract text png
- batch OCR images
- process multiple images
- aspose OCR c#
language: pl
og_description: Jak używać OCR w C# z Aspose OCR C#. Ten samouczek pokazuje, jak wyodrębniać
  tekst z plików PNG, przetwarzać obrazy w trybie wsadowym OCR oraz efektywnie obsługiwać
  wiele obrazów.
og_title: Jak używać OCR w C# – wsadowe wyodrębnianie tekstu z PNG
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Jak używać OCR w C# – przetwarzanie wsadowe obrazów PNG za pomocą Aspose OCR
url: /pl/net/text-recognition/how-to-use-ocr-in-c-batch-process-png-images-with-aspose-ocr/
---

serve you well in any image‑processing pipeline."

Translate.

"Happy coding, and may your OCR jobs be fast and error‑free!" translate.

Then closing shortcodes.

Make sure to keep shortcodes exactly.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać OCR w C# – Przetwarzanie wsadowe obrazów PNG za pomocą Aspose OCR

Zastanawiałeś się kiedyś **jak używać OCR**, aby wyciągnąć tekst z wielu plików PNG bez pisania osobnej procedury dla każdego z nich? Nie jesteś sam. Wielu programistów napotyka trudności, gdy muszą **wyodrębnić tekst z PNG** w dużej skali, szczególnie gdy obrazy znajdują się w folderze i trzeba uruchamiać silnik OCR dla każdego pliku.  

W tym przewodniku przeprowadzimy Cię przez kompletną, gotową do uruchomienia rozwiązanie, które **przetwarza wsadowo obrazy OCR**, **przetwarza wiele obrazów** równolegle i wykorzystuje potężną bibliotekę **Aspose OCR C#**. Po zakończeniu będziesz mieć pojedynczy plik wykonywalny, który odczyta dowolną liczbę plików PNG, wyodrębni ich tekst i wypisze wyniki w konsoli — wszystko w kilku linijkach kodu.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również z .NET Core i .NET Framework)  
- Ważna licencja Aspose.OCR dla .NET (lub wersja próbna) – możesz ją pobrać ze strony Aspose.  
- Folder zawierający pliki PNG, które chcesz odczytać.  
- Visual Studio 2022 (lub dowolne IDE kompatybilne z C#).  

Nie są wymagane dodatkowe pakiety NuGet poza `Aspose.OCR`.

## Krok 1: Jak używać OCR – Inicjalizacja silnika Aspose OCR

Pierwszą rzeczą, której potrzebujesz, jest instancja klasy `Engine`. Ten obiekt abstrahuje podstawową technologię OCR i może działać na CPU lub GPU, w zależności od Twojego sprzętu i licencji.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

// Create an OCR engine (CPU by default; GPU can be enabled via EngineSettings if licensed)
var ocrEngine = new Engine();
```

*Dlaczego to ważne:* Inicjalizacja silnika raz i ponowne użycie go w wielu wątkach oszczędza pamięć i eliminuje narzut związany z wielokrotnym ładowaniem modeli OCR. Zapewnia także spójne ustawienia dla wszystkich obrazów.

## Krok 2: Wyodrębnij tekst z PNG – Zbierz ścieżki do obrazów

Następnie potrzebujemy kolekcji ścieżek do plików. W prawdziwym projekcie możesz odczytywać katalog dynamicznie, ale dla przejrzystości wymienimy kilka przykładowych plików.

```csharp
// List the PNG files you want to process
var imagePaths = new List<string>
{
    "YOUR_DIRECTORY/img1.png",
    "YOUR_DIRECTORY/img2.png",
    "YOUR_DIRECTORY/img3.png"
};
```

*Wskazówka:* Zamień `YOUR_DIRECTORY` na absolutną lub względną ścieżkę do swoich obrazów. Jeśli masz dziesiątki plików, możesz zastąpić ręczną listę wywołaniem `Directory.GetFiles("YOUR_DIRECTORY", "*.png")`.

## Krok 3: Przetwarzanie wsadowe obrazów OCR – Uruchom rozpoznawanie równolegle

Przetwarzanie obrazów jeden po drugim jest proste, ale wolne. Korzystając z `Parallel.ForEach`, możemy **przetwarzać wiele obrazów** jednocześnie, wykorzystując wielordzeniowe procesory.

```csharp
// Helper method that performs the parallel recognition
static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
{
    var resultsBag = new ConcurrentBag<OcrResult>();

    Parallel.ForEach(paths, path =>
    {
        // Load the image stream (Aspose handles various formats)
        var image = ImageStream.FromFile(path);
        // Perform OCR
        OcrResult result = engine.Recognize(image);
        // Store the result safely for later use
        resultsBag.Add(result);
    });

    return resultsBag.ToArray();
}

// Execute the parallel OCR
var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);
```

*Dlaczego równolegle?* Każde wywołanie OCR jest intensywne pod kątem CPU, ale niezależne, więc ich jednoczesne uruchomienie może znacząco skrócić całkowity czas wykonania, szczególnie na maszynie z 4‑rdzeniowym lub wyższym procesorem.

## Krok 4: Przetwarzanie wielu obrazów – Wyświetl wyodrębniony tekst

Teraz, gdy mamy kolekcję obiektów `OcrResult`, możemy iterować po nich i wypisywać rozpoznany tekst. To miejsce, w którym normalnie zapisałbyś wynik w bazie danych lub do plików, ale wyjście w konsoli utrzymuje przykład zwięzły.

```csharp
int index = 1;
foreach (var result in ocrResults)
{
    Console.WriteLine($"--- Image {index++} ---");
    Console.WriteLine(result.Text);
}
```

**Oczekiwany wynik w konsoli (przykład):**

```
--- Image 1 ---
Hello world! This is the first image.
--- Image 2 ---
Invoice #12345
Total: $250.00
--- Image 3 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

Jeśli którykolwiek obraz nie uda się załadować, Aspose zgłosi wyjątek; możesz otoczyć wywołanie `engine.Recognize` blokiem try/catch, aby logować błędy bez przerywania całej partii.

## Krok 5: Pełny działający przykład – Wszystkie elementy razem

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do nowego projektu konsolowego C#. Zawiera wszystko, od dyrektyw `using` po końcową pętlę wyjścia.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new Engine();

        // Step 2: Define the PNG files to process
        var imagePaths = new List<string>
        {
            "YOUR_DIRECTORY/img1.png",
            "YOUR_DIRECTORY/img2.png",
            "YOUR_DIRECTORY/img3.png"
        };

        // Step 3: Run OCR in parallel
        var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);

        // Step 4: Output the recognized text
        int index = 1;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"--- Image {index++} ---");
            Console.WriteLine(result.Text);
        }
    }

    // Helper method for parallel OCR
    static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
    {
        var resultsBag = new ConcurrentBag<OcrResult>();

        Parallel.ForEach(paths, path =>
        {
            try
            {
                var image = ImageStream.FromFile(path);
                OcrResult result = engine.Recognize(image);
                resultsBag.Add(result);
            }
            catch (Exception ex)
            {
                // Log the error but keep the batch running
                Console.Error.WriteLine($"Error processing {path}: {ex.Message}");
            }
        });

        return resultsBag.ToArray();
    }
}
```

### Uruchamianie przykładu

1. Utwórz nowy projekt **Console App** w Visual Studio.  
2. Dodaj pakiet NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`).  
3. Zamień `YOUR_DIRECTORY` na ścieżkę, w której znajdują się Twoje pliki PNG.  
4. Zbuduj i uruchom – powinieneś zobaczyć wyodrębniony tekst wypisany w konsoli.

## Porady profesjonalne i przypadki brzegowe

- **Przyspieszenie GPU:** Jeśli masz kompatybilny GPU i licencjonowany Aspose OCR, włącz je poprzez `EngineSettings` przed utworzeniem silnika. To może zaoszczędzić sekundy przy każdym obrazie.  
- **Duże pliki:** Dla obrazów większych niż 10 MB rozważ ich wstępne zmniejszenie, aby zmniejszyć obciążenie pamięci.  
- **Obsługa języków:** Domyślnie silnik zakłada język angielski. Ustaw `engine.Language = Language.French;` (lub dowolny obsługiwany język), aby poprawić dokładność przy tekstach nieanglojęzycznych.  
- **Obsługa błędów:** `try/catch` wewnątrz pętli równoległej zapewnia, że uszkodzony plik nie przerwie całej partii. Możesz także logować niepowodzenia do pliku w celu późniejszej analizy.  
- **Przechowywanie wyników:** Zamiast wypisywać, możesz zapisać `result.Text` do pliku `.txt` używając `File.WriteAllText(Path.ChangeExtension(path, ".txt"))`.

## Zakończenie

Teraz wiesz **jak używać OCR** w C# do **wyodrębniania tekstu z plików PNG**, **przetwarzania wsadowego obrazów OCR** i **efektywnego przetwarzania wielu obrazów** przy użyciu Aspose OCR C#. Rozwiązanie jest w pełni samodzielne, działa równolegle i może być rozszerzone do obsługi setek lub tysięcy plików przy minimalnych zmianach.

Gotowy na kolejny krok? Spróbuj zamienić wyjście konsoli na raport CSV, poeksperymentuj z przyspieszeniem GPU lub podaj tekst OCR do indeksu wyszukiwania. Możliwości są nieograniczone, a podstawowy wzorzec — inicjalizuj raz, uruchamiaj równolegle, obsługuj błędy elegancko — przyda się w każdym potoku przetwarzania obrazów.

Miłego kodowania i niech Twoje zadania OCR będą szybkie i wolne od błędów!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}