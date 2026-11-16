---
category: general
date: 2026-03-05
description: Konwertuj pliki TIFF na tekst w C# przy użyciu Aspose OCR — szybko wyodrębnij
  tekst ze zeskanowanych obrazów i dowiedz się, jak wczytać plik obrazu w C# do przetwarzania
  OCR.
draft: false
keywords:
- convert TIFF to text
- extract text scanned image
- load image file C#
language: pl
og_description: Konwertuj pliki TIFF na tekst w C# przy użyciu Aspose OCR. Poznaj
  pełny proces wyodrębniania tekstu ze skanowanych obrazów i efektywnego ładowania
  plików graficznych.
og_title: Konwertuj TIFF na tekst w C# – wyodrębnij tekst ze zeskanowanego obrazu
tags:
- OCR
- C#
- Aspose
title: Konwertuj TIFF na tekst w C# – wyodrębnij tekst ze zeskanowanego obrazu
url: /pl/net/text-recognition/convert-tiff-to-text-in-c-extract-scanned-image-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwertuj TIFF na Tekst w C# – Wyodrębnij Tekst ze Skanowanego Obrazu

Potrzebujesz **konwertować TIFF na tekst w C#**? Nie jesteś jedynym, który zmaga się z wielostronicowymi zeskanowanymi obrazami, które uparcie odmawiają przekształcenia w przeszukiwalne ciągi znaków.  
W tym przewodniku przeprowadzimy Cię przez kompletną, gotową do uruchomienia rozwiązanie, które przyjmuje plik TIFF, przekazuje go do Aspose OCR i zwraca czysty tekst — bez dodatkowych usług, bez ukrytej magii.

> **Wskazówka:** Jeśli pracujesz z wysokiej rozdzielczości skanami, włączenie przetwarzania GPU może zaoszczędzić sekundy przy każdej stronie.

Pokażemy Ci również, jak **wyodrębnić tekst ze zeskanowanego obrazu** oraz najlepszy sposób **załadowania pliku obrazu w C#** do silnika OCR, abyś mógł wbudować tę logikę w dowolny projekt .NET już dziś.

---

## Czego będziesz potrzebować

Zanim zaczniemy, upewnij się, że masz następujące elementy na swoim komputerze:

| Wymaganie | Powód |
|-------------|--------|
| .NET 6.0+ (or .NET Framework 4.7.2+) | Nowoczesne środowisko uruchomieniowe, obsługuje `Span<T>` i asynchroniczny I/O |
| Aspose.OCR for .NET (pakiet NuGet `Aspose.OCR`) | Silnik OCR, którego użyjemy |
| Ważny plik licencji Aspose OCR (`Aspose.OCR.lic`) | Bez niego napotkasz ograniczenia wersji próbnej |
| Plik TIFF (jednostronicowy lub wielostronicowy) do testów | Używany przykład: `scanned_multi_page.tif` |
| GPU z CUDA 11+ (opcjonalnie) | Przyspiesza rozpoznawanie, gdy `EngineMode = Gpu` |

Jeśli brakuje Ci któregoś z nich, pobierz pakiet NuGet już teraz:

```bash
dotnet add package Aspose.OCR
```

## Krok 1: Skonfiguruj projekt i zaimportuj przestrzenie nazw

Utwórz nową aplikację konsolową (lub dodaj kod do istniejącego projektu). Pierwszą rzeczą, którą robimy, jest importowanie potrzebnych klas.

```csharp
using System;
using Aspose.OCR;          // Core OCR classes
using Aspose.OCR.Image;   // ImageStream helper
```

> **Dlaczego to ważne:** Importowanie `Aspose.OCR.Image` zapewnia fabrykę `ImageStream`, która może odczytywać pliki TIFF bezpośrednio z dysku lub strumienia. Pominięcie tego kroku spowoduje błąd kompilacji.

## Krok 2: Zainicjalizuj silnik OCR i wybierz tryb przetwarzania

Silnik OCR musi być skonfigurowany **przed** przypisaniem jakiegokolwiek obrazu. Tutaj decydujemy, czy uruchomić go na CPU, czy wykorzystać GPU.

```csharp
// Step 2: Initialize the OCR engine and enable GPU processing (must be set before any OCR work)
OcrEngine ocrEngine = new OcrEngine();

// Choose the processing mode that fits your environment.
// Options: Cpu (default) | Gpu | Auto
ocrEngine.EngineMode = OcrEngineMode.Gpu;   // Switch to Cpu if you don’t have a compatible GPU
```

*Jeśli pracujesz na serwerze bez graficznej karty, zmień `Gpu` na `Cpu` lub `Auto`.*  
Tryb silnika wpływa na przydział pamięci i szybkość; tryb GPU może być 2‑3× szybszy przy dużych, wysokiej rozdzielczości plikach TIFF.

## Krok 3: Zastosuj swoją licencję Aspose OCR

Uruchamianie bez licencji ogranicza Cię do kilku stron i znaków wodnych. Załaduj licencję wcześnie, aby każde kolejne działanie było nieograniczone.

```csharp
// Step 3: Apply the Aspose OCR license (replace with your own license file if needed)
ocrEngine.SetLicense("Aspose.OCR.lic");
```

> **Typowy błąd:** Umieszczenie `SetLicense` po wywołaniu `Recognize()` spowoduje, że silnik przełączy się w tryb próbny dla tego wywołania.

## Krok 4: Załaduj plik TIFF – Obsługa obrazów jednopostaciowych i wielostronicowych

Aspose OCR potrafi odczytywać wielostronicowe pliki TIFF od razu, ale musisz podać właściwy strumień. Oto solidny wzorzec, który działa w obu scenariuszach.

```csharp
// Step 4: Load the image to be recognized
string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

using (var imageStream = ImageStream.FromFile(tiffPath))
{
    // Step 5: Assign the image to the engine
    ocrEngine.Image = imageStream;

    // Step 6: Perform the OCR operation
    OcrResult ocrResult = ocrEngine.Recognize();

    // Step 7: Output the recognized text
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
```

### Dlaczego używać `ImageStream.FromFile`?

- Abstrahuje podstawowy `FileStream`, obsługując wewnętrznie enumerację stron TIFF.  
- Działa również z `MemoryStream`, więc możesz ładować obrazy z bazy danych lub API internetowego bez dotykania systemu plików.

### Przypadek brzegowy: Bardzo duże pliki TIFF

Jeśli Twój plik TIFF przekracza 200 MB, rozważ ładowanie go strona po stronie, aby uniknąć wyjątków braku pamięci:

```csharp
int pageCount = ImageInfo.GetPageCount(tiffPath);
for (int i = 0; i < pageCount; i++)
{
    using var pageStream = ImageStream.FromFile(tiffPath, i);
    ocrEngine.Image = pageStream;
    var pageResult = ocrEngine.Recognize();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

## Krok 5: Zweryfikuj wynik

Po uruchomieniu programu powinieneś zobaczyć coś podobnego do:

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
Thank you for your business!
```

Jeśli tekst wygląda na zniekształcony, sprawdź ponownie:

1. **Rozdzielczość** – OCR działa najlepiej przy 300 dpi lub wyższej.  
2. **EngineMode** – Przełącz na `Cpu`, jeśli sterownik GPU jest przestarzały.  
3. **Licencja** – Upewnij się, że ścieżka do pliku licencji jest prawidłowa i plik jest czytelny.

## Najczęściej Zadawane Pytania (FAQ)

### Czy to działa z innymi formatami obrazów?

Oczywiście. `ImageStream.FromFile` obsługuje JPEG, PNG, BMP, a nawet PDF (przez Aspose.PDF). Wystarczy zamienić rozszerzenie pliku.

### Co zrobić, jeśli muszę przetwarzać obrazy przechowywane w bazie danych?

Odczytaj BLOB do `MemoryStream` i przekaż go do `ImageStream.FromStream(memoryStream)`. Silnik OCR traktuje go tak samo jak strumień oparty na pliku.

### Czy mogę uruchomić to na Linuxie?

Tak — Aspose OCR jest wieloplatformowy. Zainstaluj odpowiednie środowisko .NET i upewnij się, że dostępne są wymagane natywne biblioteki dla GPU (jeśli są używane).

## Pełny działający przykład (gotowy do kopiowania i wklejania)

Poniżej znajduje się cały program, gotowy do kompilacji. Zastąp `YOUR_DIRECTORY` oraz ścieżkę do pliku licencji rzeczywistymi lokalizacjami.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace TiffToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Choose processing mode: Gpu, Cpu, or Auto
            ocrEngine.EngineMode = OcrEngineMode.Gpu; // Change to Cpu if no GPU

            // Apply license (skip if you only need a trial)
            ocrEngine.SetLicense("Aspose.OCR.lic");

            // Path to the TIFF file
            string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

            // Load the TIFF (handles multi‑page automatically)
            using (var imageStream = ImageStream.FromFile(tiffPath))
            {
                // Assign image to engine
                ocrEngine.Image = imageStream;

                // Run OCR
                OcrResult result = ocrEngine.Recognize();

                // Display result
                Console.WriteLine("=== OCR Output ===");
                Console.WriteLine(result.Text);
            }

            // Optional: Process each page individually for huge files
            // int pages = ImageInfo.GetPageCount(tiffPath);
            // for (int i = 0; i < pages; i++) { ... }
        }
    }
}
```

Zapisz to jako `Program.cs`, uruchom `dotnet run` i obserwuj tekst

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}