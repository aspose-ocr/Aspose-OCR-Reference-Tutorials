---
category: general
date: 2026-10-11
description: Dowiedz się, jak wykonać OCR obrazu w C# przy użyciu Aspose.OCR, w tym
  instalację System.Drawing.Common oraz wyodrębnianie tekstu z plików JPG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: pl
lastmod: 2026-10-11
og_description: Wykonaj OCR obrazu w C# przy użyciu Aspose.OCR. Ten przewodnik pokazuje,
  jak zainstalować System.Drawing.Common, wczytać obraz do OCR i wyodrębnić tekst
  z pliku JPG.
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: Wykonaj OCR na obrazie w C# – przewodnik krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Jak wykonać OCR na obrazie w C# przy użyciu Aspose.OCR
url: /pl/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonać OCR na obrazie w C# przy użyciu Aspose.OCR

Jeśli potrzebujesz **wykonywać OCR na obrazie** w aplikacji .NET, ten przewodnik pokaże Ci kompletne rozwiązanie. Korzystając z Aspose.OCR możesz szybko **rozpoznawać tekst ze zdjęcia** w plikach takich jak JPG i wyświetlić wynik w oknie konsoli.

Nauczysz się, jak:

* **zainstalować pakiet System.Drawing.Common** – biblioteka dostarczająca klasę `Image`,
* **ładować obraz do OCR** – odczytać JPEG lub PNG do pamięci,
* skonfigurować model językowy,
* **wykonywać OCR na obrazie** i w końcu,
* **wyodrębnić tekst z JPG** i wyświetlić go.

Kroki są napisane dla .NET 6+, ale działają również z .NET Framework 4.6.1 lub nowszym.

---

## Wymagania wstępne

| Wymaganie | Dlaczego jest ważne |
|-------------|----------------|
| .NET 6 SDK (or .NET Framework 4.6.1+) | Zapewnia środowisko uruchomieniowe dla aplikacji konsolowej C#. |
| Visual Studio 2022 (or any IDE) | Umożliwia łatwe dodawanie pakietów NuGet i uruchamianie programu. |
| Internet connection (first run only) | Aspose.OCR automatycznie pobiera moduł językowy. |
| Przykładowy obraz zawierający tekst cyrylicą lub łaciński (np. `sample_cyrillic.jpg`) | Używany do demonstracji **wyodrębnić tekst z JPG**. |

---

## Krok 1: Zainstaluj pakiet System.Drawing.Common

Pakiet NuGet `System.Drawing.Common` dostarcza klasę `Image`, którą będziesz **ładować obraz do OCR**. Otwórz konsolę Menedżera Pakietów i uruchom:

```powershell
Install-Package System.Drawing.Common
```

> **Pro tip:** Ustaw docelowy framework `net6.0-windows` lub dodaj `<UseWindowsForms>true</UseWindowsForms>` do pliku projektu, jeśli napotkasz ostrzeżenia specyficzne dla platformy na Linux/macOS.

---

## Krok 2: Dodaj pakiet NuGet Aspose.OCR

Aspose.OCR zawiera silnik OCR oraz modele językowe. Zainstaluj go za pomocą:

```powershell
Install-Package Aspose.OCR
```

Pakiet jest lekki; wymagane dane językowe (np. cyrylica) są pobierane przy pierwszym ustawieniu `OcrEngine.Language`.

---

## Krok 3: Jak załadować obraz do OCR

Załadowanie obrazu jest pierwszym konkretnym krokiem, zanim będziesz mógł **wykonywać OCR na obrazie**. Metoda `Image.FromFile` odczytuje każdy format obsługiwany przez GDI+, w tym JPG, PNG, BMP i TIFF.

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*Jeśli plik nie istnieje, zostanie rzucony `FileNotFoundException` – w kodzie produkcyjnym otocz wywołanie blokiem try/catch.*

---

## Krok 4: Skonfiguruj silnik i **wykonywać OCR na obrazie**

Utwórz instancję `OcrEngine`, wybierz model językowy, przypisz załadowany obraz i wywołaj `Recognize()`.

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

Metoda `Recognize()` zwraca obiekt `OcrResult`, który zawiera wyodrębniony tekst, wyniki pewności oraz ramki ograniczające. Moduł językowy jest pobierany automatycznie przy pierwszym użyciu, więc nie są potrzebne dodatkowe pliki.

---

## Krok 5: **Wyodrębnić tekst z JPG** i wyświetlić go

Teraz możesz **rozpoznawać tekst ze zdjęcia** i wyświetlić wynik. Właściwość `Text` obiektu `OcrResult` zawiera zwykły ciąg znaków.

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### Oczekiwany wynik w konsoli

```
Recognized text:
Пример текста на кириллице
```

Jeśli źródłowy obraz zawiera tekst po angielsku, wynik będzie angielskim zdaniem, które umieściłeś na obrazie.

---

## Przypadki brzegowe i wskazówki najlepszych praktyk

| Sytuacja | Zalecenie |
|-----------|----------------|
| **Large images ( > 5 MB )** | Zmień rozmiar obrazu do ≤ 2000 px po najdłuższym boku przed OCR, aby zmniejszyć zużycie pamięci i przyspieszyć działanie. |
| **Multiple languages in one picture** | Wywołaj `ocrEngine.AddLanguage(OcrLanguage.English)` oprócz cyrylicy, a następnie ustaw `ocrEngine.Language = OcrLanguage.Multilingual`. |
| **Low‑contrast scans** | Zwiększ kontrast przy użyciu `System.Drawing.Graphics` przed przekazaniem bitmapy do silnika. |
| **Running on Linux/macOS** | Upewnij się, że zależność natywna `libgdiplus` jest zainstalowana (`sudo apt-get install -y libgdiplus`). |
| **Repeated OCR calls** | Ponownie używaj tej samej instancji `OcrEngine` i jedynie zamieniaj `ocrEngine.Image`, aby uniknąć wielokrotnego ładowania modułu. |

---

## Pełny, działający program

Poniżej znajduje się kompletny program konsolowy, który zawiera wszystkie poprzednie kroki. Skopiuj kod do nowego projektu konsolowego C#, zamień ścieżkę do obrazu i uruchom go.

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Uruchomienie programu** wypisuje rozpoznany ciąg znaków w konsoli, potwierdzając, że pomyślnie **wykonywałeś OCR na obrazie** i **wyodrębniłeś tekst z JPG**.

---

## Zakończenie

Teraz wiesz, jak **wykonywać OCR na obrazie** w C# przy użyciu Aspose.OCR, od instalacji wymaganego **pakietu System.Drawing.Common** po **ładowanie obrazu do OCR**, wybór odpowiedniego języka i w końcu **wyodrębnić tekst z JPG**. Ten kompleksowy przykład daje solidne podstawy do budowania bardziej zaawansowanych przepływów przetwarzania dokumentów, takich jak przetwarzanie wsadowe folderów ze zdjęciami czy integracja OCR z interfejsem web API.

### Co dalej?

* Zbadaj **rozpoznawać tekst ze zdjęcia** w plikach PDF, najpierw konwertując każdą stronę na obraz.
* Eksperymentuj z właściwościami `OcrEngine` takimi jak `Resolution`, `Threshold` i `MaxProcessingTime`, aby dopasować dokładność przy szumnych skanach.
* Połącz wynik OCR z biblioteką przetwarzania języka naturalnego, aby automatycznie kategoryzować wyodrębnioną treść.

Śmiało dostosowuj kod do innych formatów obrazów, dodawaj obsługę błędów lub integruj go w większych aplikacjach. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Extract Text from Image in C# – Complete Aspose OCR Guide](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}