---
category: general
date: 2026-03-04
description: Jak używać OCR do odczytywania plików PNG i szybkiego wyodrębniania tekstu.
  Naucz się przetwarzania OCR wsadowego i konwertowania obrazów na tekst za pomocą
  Aspose OCR w C#.
draft: false
keywords:
- how to use OCR
- batch ocr processing
- extract text png
- read png files
- convert images to text
language: pl
og_description: Jak używać OCR do odczytywania plików PNG, przetwarzania OCR wsadowego
  i konwertowania obrazów na tekst w jednym, łatwym do śledzenia przewodniku.
og_title: 'Jak używać OCR: wsadowe wyodrębnianie tekstu z PNG w C#'
tags:
- C#
- OCR
- Aspose
- Image Processing
title: 'Jak korzystać z OCR: wsadowe wyodrębnianie tekstu z PNG w C#'
url: /pl/net/text-recognition/how-to-use-ocr-batch-png-text-extraction-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać OCR: wsadowa ekstrakcja tekstu z PNG w C#

Zastanawiałeś się kiedyś **jak używać OCR** na folderze pełnym zrzutów ekranu? Może masz góry plików PNG – paragony, faktury lub zeskanowane formularze – i potrzebujesz tekstu bez ręcznego otwierania każdego pliku. Dobra wiadomość? Kilka linijek C# i Aspose OCR pozwoli Ci **odczytać pliki PNG**, **wyodrębnić tekst PNG**‑po‑PNG i **konwertować obrazy na tekst** równolegle – bez problemu.

W tym tutorialu przeprowadzimy Cię przez kompletną, gotową do uruchomienia aplikację, która pokazuje **wsadowe przetwarzanie OCR** od początku do końca. Po zakończeniu będziesz mieć aplikację konsolową, która skanuje katalog, wyciąga każdy ciąg znaków i wyświetla szybki raport postępu. Bez zewnętrznych skryptów, bez ukrytej magii – tylko przejrzysty kod i wyjaśnienia, które możesz skopiować‑wkleić od razu.

---

## Czego będziesz potrzebować

- .NET 6 (lub nowszy) – aktualna wersja LTS na rok 2026.  
- Pakiet NuGet Aspose.OCR – zainstaluj poleceniem `dotnet add package Aspose.OCR`.  
- Folder pełen obrazów PNG, które chcesz przetworzyć.  
- Dowolne IDE (Visual Studio, VS Code, Rider…).

To wszystko. Jeśli masz te elementy, możesz zaczynać.

---

## Jak używać OCR: przygotowanie projektu

Najpierw utwórz nowy projekt konsolowy i dodaj bibliotekę Aspose OCR.

```bash
dotnet new console -n OcrBatchDemo
cd OcrBatchDemo
dotnet add package Aspose.OCR
```

Teraz otwórz `Program.cs`. Zastąpimy domyślną zawartość pełnym przykładem, który demonstruje **wsadowe przetwarzanie OCR** i **wyodrębnianie tekstu png** w sposób wydajny.

---

## Krok 1 – Znalezienie wszystkich obrazów PNG w katalogu

Wyszukiwanie plików to najprostsza część, ale kluczowa, aby **odczytać pliki PNG** niezawodnie na każdym systemie.

```csharp
using System;
using System.Collections.Concurrent;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static async Task Main(string[] args)
    {
        // 👉 Change this path to where your PNGs live
        string sourceFolder = @"C:\Images\ToProcess";
        if (!Directory.Exists(sourceFolder))
        {
            Console.WriteLine($"Folder not found: {sourceFolder}");
            return;
        }

        // Step 1: Locate all PNG images in the source folder
        string[] imagePaths = Directory.GetFiles(sourceFolder, "*.png", SearchOption.AllDirectories);
        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found. Make sure the folder contains .png images.");
            return;
        }

        // Continue to the next steps…
```

> **Dlaczego to ważne:** Użycie `SearchOption.AllDirectories` pozwala **odczytać pliki PNG** nawet wtedy, gdy są zagnieżdżone w podkatalogach, co oszczędza późniejsze ręczne przeszukiwanie.

---

## Krok 2 – Przygotowanie wątkowo‑bezpiecznej kolekcji na wyniki

Ponieważ będziemy uruchamiać OCR na wielu rdzeniach, potrzebujemy kontenera, który obsłuży równoczesne zapisy.

```csharp
        // Step 2: Prepare a thread‑safe bag to store extracted text
        ConcurrentBag<string> extractedTexts = new ConcurrentBag<string>();
```

> **Pro tip:** `ConcurrentBag<T>` jest bezblokowy i idealny do gromadzenia wyników, gdy kolejność nie ma znaczenia. Jeśli potrzebujesz zachować kolejność, przejdź na `ConcurrentQueue<T>`.

---

## Krok 3 – Konfiguracja silnika OCR do przetwarzania wsadowego

Tutaj dzieje się magia **wsadowego przetwarzania OCR**. Ustawiamy język, włączamy optymalne równoległe przetwarzanie i ponownie używamy tej samej instancji silnika dla każdego obrazu.

```csharp
        // Step 3: Set up the OCR batch processor with English language and optimal parallelism
        OcrBatchProcessor ocrBatchProcessor = new OcrBatchProcessor
        {
            Engine = new OcrEngine { Language = Language.English },
            MaxDegreeOfParallelism = Environment.ProcessorCount // uses all logical cores
        };
```

> **Dlaczego warto ponownie używać silnika?** Tworzenie nowego `OcrEngine` dla każdego obrazu generuje dodatkowy narzut. Ponowne użycie zmniejsza zużycie pamięci i przyspiesza cały **wsadowy proces OCR**.

---

## Krok 4 – Asynchroniczne przetwarzanie każdego obrazu i zbieranie tekstu

Teraz faktycznie uruchamiamy OCR. Metoda `ProcessAsync` przyjmuje listę plików, przetwarza każdy obraz w osobnym wątku i wywołuje zwrotną funkcję z wynikiem.

```csharp
        // Step 4: Process each image asynchronously, collect the text, and report progress
        await ocrBatchProcessor.ProcessAsync(imagePaths, (imagePath, ocrResult) =>
        {
            // Store the extracted string
            extractedTexts.Add(ocrResult.Text);

            // Simple progress line – shows how many characters we got
            Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        });

        // All done – let's show a quick summary
        Console.WriteLine($"\nFinished! Processed {imagePaths.Length} PNG files.");
        Console.WriteLine($"Total extracted text blocks: {extractedTexts.Count}");
    }
}
```

> **Co widzisz:** Konsola wypisuje linię dla każdego pliku, np. `invoice123.png → 342 znaki`. To przydatna kontrola, że OCR rzeczywiście coś odczytał.

---

## Pełny działający przykład (gotowy do kopiowania)

Jeśli wolisz pobrać wszystko naraz, oto kompletny program:

```csharp
using System;
using System.Collections.Concurrent;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static async Task Main(string[] args)
    {
        // 👉 Adjust this to your own folder
        string sourceFolder = @"C:\Images\ToProcess";

        if (!Directory.Exists(sourceFolder))
        {
            Console.WriteLine($"Folder not found: {sourceFolder}");
            return;
        }

        // Step 1: Locate all PNG images in the source folder
        string[] imagePaths = Directory.GetFiles(sourceFolder, "*.png", SearchOption.AllDirectories);
        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found. Place some .png images in the folder and try again.");
            return;
        }

        // Step 2: Prepare a thread‑safe bag to store extracted text
        ConcurrentBag<string> extractedTexts = new ConcurrentBag<string>();

        // Step 3: Set up the OCR batch processor with English language and optimal parallelism
        OcrBatchProcessor ocrBatchProcessor = new OcrBatchProcessor
        {
            Engine = new OcrEngine { Language = Language.English },
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };

        // Step 4: Process each image asynchronously, collect the text, and report progress
        await ocrBatchProcessor.ProcessAsync(imagePaths, (imagePath, ocrResult) =>
        {
            extractedTexts.Add(ocrResult.Text);
            Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        });

        // Summary
        Console.WriteLine($"\nFinished! Processed {imagePaths.Length} PNG files.");
        Console.WriteLine($"Total extracted text blocks: {extractedTexts.Count}");
    }
}
```

### Oczekiwany wynik

```
receipt001.png → 128 chars
invoice_2025.png → 342 chars
menu.png → 57 chars

Finished! Processed 3 PNG files.
Total extracted text blocks: 3
```

Jeśli któryś obraz jest nieczytelny, Aspose OCR zwróci pusty ciąg – w konsoli zobaczysz `0 znaków`, co jest sygnałem, by sprawdzić jakość tego pliku.

---

## Obsługa przypadków brzegowych i typowe pułapki

### Obrazy nie‑PNG

Nasza maska `*.png` ignoruje inne formaty. Jeśli potrzebujesz także JPEG‑ów lub BMP‑ów, zmień linię wyszukiwania na:

```csharp
string[] imagePaths = Directory.GetFiles(sourceFolder, "*.*", SearchOption.AllDirectories)
                               .Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase) ||
                                           f.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) ||
                                           f.EndsWith(".bmp", StringComparison.OrdinalIgnoreCase))
                               .ToArray();
```

### Bardzo duże pliki

Olbrzymie obrazy mogą wyczerpać pamięć. Szybkim rozwiązaniem jest zmniejszenie ich rozmiaru przed przekazaniem do silnika OCR:

```csharp
ocrBatchProcessor.Engine.ImageSize = new Size(2000, 0); // keep aspect ratio, max width 2000px
```

### Błędy OCR

Jeśli otrzymujesz zniekształcony tekst, rozważ:

- Zmianę `Language` na właściwą lokalizację (`Language.Spanish`, itp.).  
- Włączenie `Engine.Preprocess`, aby poprawić kontrast.  
- Ustawienie `Engine.DetectOrientation = true` dla obróconych skanów.

---

## Pro Tips for Faster **Batch OCR Processing**

1. **Rozgrzej silnik** – przetwórz jedną małą grafikę przed pętlą; załaduje to natywne DLL‑y i zmniejszy opóźnienie przy pierwszym uruchomieniu.  
2. **Unikaj wąskich gardeł konsoli** – wypisywanie linii dla każdego pliku może spowolnić działanie przy tysiącach obrazów. Zakomentuj `Console.WriteLine` wewnątrz zwrotu, jeśli potrzebujesz tylko podsumowania.  
3. **Trwałe zapisywanie wyników** – zamiast `ConcurrentBag` zapisuj każdy wynik OCR od razu do bazy danych lub pliku CSV. Dzięki temu nie utracisz danych, jeśli proces się zawiesi.

---

## Rozszerzenie przykładu: zapisywanie wyodrębnionego tekstu do plików

Jeśli wolisz mieć plik `.txt` dla każdego obrazu, zmodyfikuj zwrotną funkcję:

```csharp
await ocrBatchProcessor.ProcessAsync(imagePaths, (imagePath, ocrResult) =>
{
    string txtPath = Path.ChangeExtension(imagePath, ".txt");
    File

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}