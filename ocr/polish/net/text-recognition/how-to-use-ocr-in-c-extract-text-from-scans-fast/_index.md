---
category: general
date: 2026-03-13
description: Jak używać OCR w C#, aby wyodrębnić tekst ze skanów. Dowiedz się, jak
  konwertować pliki TIFF na tekst przy użyciu Aspose OCR, przyspieszenia GPU i krok
  po kroku kodu.
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: pl
og_description: Jak używać OCR w C#, aby wyodrębniać tekst ze skanów. Ten przewodnik
  pokazuje, jak konwertować pliki TIFF na tekst przy użyciu Aspose OCR i przyspieszenia
  GPU.
og_title: Jak używać OCR w C# – Szybko wyodrębniaj tekst ze skanów
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Jak korzystać z OCR w C# – Szybko wyodrębniaj tekst ze skanów
url: /pl/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać OCR w C# – szybkie wyodrębnianie tekstu ze skanów

Zastanawiałeś się kiedyś **jak używać OCR**, aby wyciągnąć czytelny tekst ze stosu zeskanowanych plików TIFF? Nie jesteś sam. W wielu rzeczywistych projektach — myśl o cyfryzacji faktur, archiwizacji dokumentów historycznych lub po prostu udostępnianiu PDF‑ów do wyszukiwania — programiści potrzebują niezawodnego sposobu na **wyodrębnianie tekstu ze skanów** bez zbędnego wysiłku.

Dobra wiadomość? Z Aspose OCR i kilkoma liniami C# możesz przekonwertować TIFF na tekst w ciągu kilku sekund, nawet na skromnym komputerze. Poniżej znajdziesz kompletny, gotowy do uruchomienia przykład oraz uzasadnienie każdego wyboru, abyś mógł dostosować go do własnego przepływu pracy.

## Czego będziesz potrzebować

Zanim przejdziemy dalej, upewnij się, że masz pod ręką następujące elementy:

| Wymaganie | Dlaczego jest ważne |
|--------------|----------------|
| .NET 6+ (lub .NET Framework 4.7+) | Pakiet NuGet Aspose OCR jest skierowany do nowoczesnych środowisk .NET. |
| Visual Studio 2022 (lub dowolne IDE) | Zapewnia IntelliSense i łatwe debugowanie. |
| Karta graficzna kompatybilna z CUDA i sterownik (opcjonalnie) | Umożliwia `ocrEngine.UseGpu = true` dla zauważalnego przyspieszenia przy dużych partiach. |
| Folder z obrazami TIFF, które chcesz przetworzyć | Ten samouczek używa plików `*.tif`, ale możesz dostosować wzorzec. |
| Pakiet NuGet Aspose.OCR (`Install-Package Aspose.OCR`) | Biblioteka, która wykonuje całą ciężką pracę. |

Jeśli czegoś brakuje, zdobądź to teraz — nie ma sensu czytać dalej, aby później natrafić na brakującą zależność.

## Przegląd rozwiązania

Na wysokim poziomie program wykonuje trzy rzeczy:

1. **Utworzenie silnika OCR** i opcjonalne włączenie przyspieszenia GPU.  
2. **Iteracja po każdym pliku TIFF** w katalogu, uruchomienie rozpoznawania i zapisanie uzyskanego tekstu.  
3. **Zapis tekstu** do pliku `.txt` znajdującego się obok oryginalnego obrazu.

To wszystko. Kod jest celowo mały, a jednocześnie demonstruje dobre praktyki, takie jak jawny wybór języka, prawidłowe zwalnianie zasobów i obsługa błędów w najczęstszych przypadkach brzegowych.

![Przykład użycia OCR w C#](/images/how-to-use-ocr-csharp.png "Ilustracja użycia OCR w C# do wyodrębniania tekstu ze skanów")

## Krok 1: Inicjalizacja silnika OCR (Jak używać OCR)

Pierwszą rzeczą, której potrzebujesz, jest instancja `OcrEngine`. Ten obiekt jest bramą do całej funkcjonalności Aspose OCR. Domyślnie działa na CPU, ale ustawienie `UseGpu = true` instruuje bibliotekę, aby przeniosła ciężkie obliczenia macierzowe na kartę graficzną — pod warunkiem, że masz zainstalowany sterownik kompatybilny z CUDA.

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**Dlaczego to jest ważne:**  
- **Przyspieszenie GPU** może skrócić czas przetwarzania nawet o 70 % przy skanach wysokiej rozdzielczości.  
- **Jawny wybór języka** zapobiega zgadywaniu przez silnik i zwiększa dokładność, szczególnie w przypadku skryptów niełacińskich.

## Krok 2: Wskazanie silnikowi lokalizacji skanów (Konwersja TIFF na tekst)

Następnie informujemy program, gdzie szukać obrazów. Użycie `Directory.GetFiles` z filtrem `*.tif` utrzymuje logikę prostą i zapobiega pobieraniu niepowiązanych plików, takich jak `.jpg` czy `.png`.

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**Uwaga dotycząca przypadków brzegowych:** Jeśli katalog jest pusty, pętla poniżej po prostu się nie wykona, co jest w pełni dopuszczalne. Później zobaczysz przyjazny komunikat „No files found”.

## Krok 3: Przetwarzanie każdego pliku TIFF (Wyodrębnianie tekstu ze skanów)

Teraz serce programu: wczytanie obrazu, uruchomienie OCR i zapis wyniku. Pomocnicza metoda `ImageStream.FromFile` strumieniuje plik bezpośrednio do pamięci, co jest wydajniejsze niż najpierw ładowanie `Bitmap`.

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**Dlaczego każdy iterację otaczamy w `try/catch`:**  
Przetwarzanie partii dokumentów bywa nieprzewidywalne; uszkodzony TIFF lub chwilowy brak pamięci nie powinny przerywać całego działania. Blok catch loguje problem i przechodzi dalej, utrzymując pipeline odpornym.

### Oczekiwany wynik

Dla każdego `example.tif` znajdziesz sąsiedni plik `example.txt` zawierający coś w stylu:

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

Jeśli silnik OCR nie odczyta linii, po prostu pozostawi pustą linię lub nieczytelny znak — nie spowoduje to awarii.

## Krok 4: Sprzątanie i zwalnianie zasobów (Najlepsza praktyka)

`OcrEngine` implementuje `IDisposable`, więc grzecznie jest zwolnić zasoby natywne po zakończeniu pracy. W krótkiej aplikacji konsolowej można polegać na GC, ale jawne zwolnienie to nawyk, który warto wyrobić.

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## Pełny działający przykład (gotowy do kopiowania i wklejania)

Poniżej znajduje się kompletny program, który możesz wkleić do nowego projektu aplikacji konsolowej. Kompiluje się od razu, pod warunkiem że dodałeś pakiet NuGet Aspose.OCR.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### Szybka lista kontrolna

- **Flaga GPU** – usuń lub ustaw na `false`, jeśli nie masz sterownika CUDA.  
- **Język** – zamień `Language.English` na dowolny inny obsługiwany język.  
- **Wzorzec plików** – zmień `"*.tif"` na `"*.png"` lub `"*.*"` jeśli skany są w innym formacie.  

## Typowe pułapki i wskazówki (samouczek OCR w C#)

| Pułapka | Jak jej uniknąć |
|---------|-----------------|
| **Błędy out‑of‑memory** przy ogromnych partiach | Przetwarzaj pliki w mniejszych partiach lub wywołuj `GC.Collect()` po każdych 50 plikach (rzadko potrzebne). |
| **GPU nie wykryte**, ale `UseGpu = true` | Silnik cicho przełącza się na CPU, ale możesz sprawdzić `ocrEngine.IsGpuAvailable` po konstrukcji. |
| **Zły pakiet językowy** powoduje nieczytelny wynik | Zawsze ustaw `ocrEngine.Language` jawnie; domyślnie może to być `Language.Unknown`. |
| **Ścieżka pliku zawiera znaki Unicode** | Użyj `Path.GetFullPath` do normalizacji lub poprzedź `@"\\?\"` w Windows, jeśli ścieżki przekraczają limit. |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}