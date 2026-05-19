---
category: general
date: 2026-03-07
description: Wyodrębnij tekst z plików PNG przy użyciu C#. Dowiedz się, jak konwertować
  obraz na tekst w C# i szybko odczytywać tekst ze skanowanych obrazów.
draft: false
keywords:
- extract text from png
- convert image to text c#
- read text from scanned images
- how to run ocr on images
language: pl
og_description: Wyodrębnij tekst z plików PNG przy użyciu C#. Ten przewodnik pokazuje,
  jak konwertować obraz na tekst w C# oraz odczytywać tekst ze skanowanych obrazów
  za pomocą Aspose OCR.
og_title: Wyodrębnij tekst z PNG w C# – Pełny przewodnik OCR
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Wyodrębnianie tekstu z PNG w C# – Pełny przewodnik OCR
url: /pl/net/text-recognition/extract-text-from-png-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tekstu z PNG w C# – Kompletny przewodnik OCR

Kiedykolwiek potrzebowałeś **wyodrębnić tekst z PNG** plików, ale nie wiedziałeś, od czego zacząć? Nie jesteś sam — większość programistów napotyka ten problem, gdy po raz pierwszy ma do czynienia ze zeskanowanymi grafikami lub zrzutami ekranu, które muszą stać się przeszukiwalnym tekstem. Dobra wiadomość? Kilka linijek C# i Aspose OCR pozwoli zamienić dowolny PNG w edytowalne ciągi znaków w mgnieniu oka.

W tym samouczku przeprowadzimy Cię przez cały proces: od znajdowania plików PNG na dysku, uruchamiania zadań OCR równolegle, po wyświetlenie schludnego podglądu każdego wyniku. Po zakończeniu będziesz wiedział, jak **convert image to text C#** w stylu, będziesz mógł **read text from scanned images** efektywnie, a także zobaczysz najlepszy sposób na **run OCR on images** bez przeciążania wątku UI.

## Co będziesz potrzebował

- .NET 6.0 lub nowszy (kod działa również na .NET Core i .NET Framework)  
- Pakiet NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Folder pełen plików *.png*, które chcesz przetworzyć  
- Dowolne IDE (Visual Studio, VS Code, Rider…)

Nie wymagana jest dodatkowa konfiguracja; biblioteka dostarcza wszystko, co potrzebne do dekodowania PNG, JPEG, TIFF, i tak dalej.

## Krok 1: Znajdź wszystkie pliki PNG – Rozpoczyna się „Extract Text from PNG”

Najpierw musimy znaleźć każdy PNG, na którym zamierzamy wykonać OCR. Użycie `Directory.GetFiles` jest szybkie i niezawodne.

```csharp
// Step 1: Find all PNG images in the input folder
string[] imageFiles = Directory.GetFiles("YOUR_DIRECTORY", "*.png");

// Quick sanity check – throw if nothing was found
if (imageFiles.Length == 0)
    throw new FileNotFoundException("No PNG files found in the specified folder.");
```

*Dlaczego to ważne:* Jednorazowe przeszukanie katalogu utrzymuje resztę potoku prostą, a wczesna kontrola zapobiega cichej sytuacji „brak wyniku”, którą później trudno debugować.

## Krok 2: Uruchom równoległe zadania OCR – Efektywne **run OCR on images**

Wykonywanie OCR sekwencyjnie jest w porządku przy kilku plikach, ale w rzeczywistych projektach często mamy do czynienia z dziesiątkami lub setkami. Uruchamiając `Task` dla każdego obrazu, utrzymujemy procesor zajęty, podczas gdy biblioteka wykonuje ciężką pracę.

```csharp
// Step 2: Prepare a list to hold OCR tasks (one per image)
var ocrTasks = new List<Task<string>>();

// Step 3: Launch a parallel task for each image
foreach (var filePath in imageFiles)
{
    ocrTasks.Add(Task.Run(() =>
    {
        // Load the image and run OCR
        var engine = new OcrEngine();
        engine.Image = ImageStream.FromFile(filePath);
        engine.Recognize();
        return engine.Text;          // This is the extracted string
    }));
}
```

*Wskazówka:* `Task.Run` przenosi pracę do puli wątków, co oznacza, że Twoje UI (jeśli je masz) pozostaje responsywne. Jeśli działasz na serwerze, ten sam wzorzec ładnie skaluje się na wiele rdzeni.

## Krok 3: Oczekuj na wszystkie zadania – Zbierz wyniki

Teraz czekamy, aż każde działanie OCR zakończy się. `Task.WhenAll` zwraca tablicę, która odpowiada pierwotnemu kolejności plików, co ułatwia dopasowanie wyników do nazw plików.

```csharp
// Step 4: Await all tasks and gather the recognized texts
string[] ocrResults = await Task.WhenAll(ocrTasks);
```

*Uwaga o przypadkach brzegowych:* Jeśli którykolwiek pojedynczy obraz zgłosi błąd (uszkodzony plik, nieobsługiwany format), cały `WhenAll` podniesie wyjątek. Możesz owinąć wewnętrzny `Task.Run` w try/catch i zwrócić pusty ciąg lub komunikat diagnostyczny, jeśli potrzebujesz odporności na błędy.

## Krok 4: Pokaż podgląd – Zweryfikuj wynik **convert image to text C#**

Szybki podgląd pomaga potwierdzić, że OCR zadziałało, zanim zaczniesz zapisywać dane w innym miejscu.

```csharp
// Step 5: Show a short preview of each result
for (int i = 0; i < ocrResults.Length; i++)
{
    string fileName = Path.GetFileName(imageFiles[i]);
    string preview = ocrResults[i].Length > 100
        ? ocrResults[i][..100] + "..."
        : ocrResults[i];
    Console.WriteLine($"{fileName}: {preview}");
}
```

Typowy output konsoli wygląda tak:

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
```

Jeśli podgląd wyświetla bełkot, sprawdź jakość obrazu lub rozważ wstępne przetwarzanie (np. binaryzację) — ale dla większości czystych PNG Aspose OCR radzi sobie poprawnie już przy pierwszej próbie.

## Opcjonalnie: Zapisz wyniki do CSV — Przykład z życia wzięty

Większość projektów potrzebuje wyodrębnionego tekstu w ustrukturyzowanym formacie. Poniżej znajduje się mały pomocnik, który zapisuje nazwę pliku i pełny tekst OCR do pliku CSV.

```csharp
string csvPath = Path.Combine("YOUR_DIRECTORY", "ocr-results.csv");
using var writer = new StreamWriter(csvPath);
writer.WriteLine("FileName,ExtractedText");

for (int i = 0; i < imageFiles.Length; i++)
{
    string escaped = ocrResults[i].Replace("\"", "\"\"");
    writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
}
Console.WriteLine($"All results saved to {csvPath}");
```

Teraz możesz zaimportować CSV do Excela, Power BI lub dowolnego systemu downstream, który oczekuje **read text from scanned images**.

## Najczęściej zadawane pytania

**Co jeśli moje PNG są ogromne (powyżej 5 MB)?**  
Aspose OCR automatycznie zmniejsza duże obrazy, aby utrzymać zużycie pamięci w ryzach, ale możesz ręcznie zmienić rozmiar za pomocą `engine.Image = ImageStream.FromFile(filePath).Resize(2000, 0);` aby ograniczyć szerokość do 2000 px przy zachowaniu proporcji.

**Czy mogę uruchomić to na Linuxie?**  
Tak. Aspose OCR jest wieloplatformowy; wystarczy upewnić się, że natywne zależności (`libgdiplus` w niektórych dystrybucjach) są zainstalowane.

**Czy język OCR jest domyślnie ustawiony na angielski?**  
Tak. Jeśli potrzebujesz innego języka, ustaw `engine.Language = OcrLanguage.French;` (lub dowolny obsługiwany enum) przed wywołaniem `Recognize()`.

**Jak obsłużyć chronione hasłem pliki PDF zawierające PNG?**  
Najpierw skonwertuj strony PDF na obrazy (używając Aspose PDF lub innej biblioteki), a następnie podaj te PNG do tego samego potoku. Zasada **how to run OCR on images** pozostaje niezmieniona.

## Pełny działający przykład (Async Main)

Poniżej znajduje się samodzielny program, który możesz skopiować i wkleić do projektu konsolowego. Zawiera wszystkie powyższe elementy, plus mały pomocnik do walidacji folderu wejściowego.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // -------------------------------------------------
        // 1️⃣ Locate PNGs – the heart of “extract text from png”
        // -------------------------------------------------
        const string folder = @"YOUR_DIRECTORY";   // <-- change this
        if (!Directory.Exists(folder))
        {
            Console.WriteLine($"Folder not found: {folder}");
            return;
        }

        string[] imageFiles = Directory.GetFiles(folder, "*.png");
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to do.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Fire off OCR tasks – best way to “run OCR on images”
        // -------------------------------------------------
        var ocrTasks = new List<Task<string>>();
        foreach (var filePath in imageFiles)
        {
            ocrTasks.Add(Task.Run(() =>
            {
                var engine = new OcrEngine();
                engine.Image = ImageStream.FromFile(filePath);
                engine.Recognize();
                return engine.Text;
            }));
        }

        // -------------------------------------------------
        // 3️⃣ Await results
        // -------------------------------------------------
        string[] ocrResults = await Task.WhenAll(ocrTasks);

        // -------------------------------------------------
        // 4️⃣ Show previews
        // -------------------------------------------------
        for (int i = 0; i < ocrResults.Length; i++)
        {
            string fileName = Path.GetFileName(imageFiles[i]);
            string preview = ocrResults[i].Length > 100
                ? ocrResults[i][..100] + "..."
                : ocrResults[i];
            Console.WriteLine($"{fileName}: {preview}");
        }

        // -------------------------------------------------
        // 5️⃣ Optional: write CSV – perfect for “read text from scanned images”
        // -------------------------------------------------
        string csvPath = Path.Combine(folder, "ocr-results.csv");
        using var writer = new StreamWriter(csvPath);
        writer.WriteLine("FileName,ExtractedText");
        for (int i = 0; i < imageFiles.Length; i++)
        {
            string escaped = ocrResults[i].Replace("\"", "\"\"");
            writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
        }

        Console.WriteLine($"✅ OCR complete – results saved to {csvPath}");
    }
}
```

**Oczekiwany output** (przykład dla dwóch PNG):

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
✅ OCR complete – results saved to C:\MyImages\ocr-results.csv
```

## Podsumowanie

Omówiliśmy wszystko, co potrzebujesz, aby **extract text from PNG** przy użyciu C#. Od znajdowania plików, uruchamiania równoległych zadań OCR, podglądu ciągów, po zapisywanie ich w CSV — ten przewodnik dostarcza gotowego do produkcji wzorca dla scenariuszy **convert image to text C#**.  

Jeśli jesteś gotowy na kolejny krok, spróbuj podać do tego samego potoku pliki JPEG lub TIFF, eksperymentuj z różnymi językami OCR lub podłącz wyniki do indeksu wyszukiwania, aby móc **read text from scanned images** od razu.  

Masz pytania o przypadki brzegowe, optymalizację wydajności lub licencjonowanie? Zostaw komentarz lub napisz do społeczności Aspose — powodzenia w kodowaniu!  

![Extract text from PNG example](extract-text-png.png "Extract text from PNG using Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}