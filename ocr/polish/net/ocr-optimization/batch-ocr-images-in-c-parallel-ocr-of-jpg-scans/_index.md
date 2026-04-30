---
category: general
date: 2026-04-29
description: Szybko przetwarzaj obrazy metodą OCR w partiach przy użyciu Aspose OCR
  w C#. Dowiedz się, jak wyodrębniać tekst z plików jpg, odczytywać tekst ze skanów
  i przetwarzać listę obrazów równolegle.
draft: false
keywords:
- batch OCR images
- extract text from jpg
- read text from scans
- parallel OCR processing
- process image list
language: pl
og_description: Szybko przetwarzaj obrazy OCR w partiach za pomocą Aspose OCR. Ten
  przewodnik pokazuje, jak wyodrębnić tekst z plików jpg, odczytać tekst ze skanów
  i przetwarzać listę obrazów równolegle.
og_title: Wsadowkie OCR obrazów w C# – Równoległe OCR skanów JPG
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Wsadowe OCR obrazów w C# – równoległe OCR skanów JPG
url: /pl/net/ocr-optimization/batch-ocr-images-in-c-parallel-ocr-of-jpg-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wsadowkie OCR obrazów w C# – Równoległe OCR skanów JPG

Kiedykolwiek potrzebowałeś **batch OCR images**, ale nie byłeś pewien, jak skalować pracę na wiele plików? Nie jesteś sam — programiści często napotykają problem, gdy próbują odczytywać tekst ze skanów pojedynczo. Dobrą wiadomością jest to, że z Aspose OCR możesz **extract text from jpg** files, **read text from scans**, oraz **process image list** items równolegle przy użyciu kilku linii C#.

W tym tutorialu przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który dokładnie pokazuje, jak to zrobić. Po zakończeniu będziesz mieć samodzielną aplikację konsolową, która rozpoznaje folder ze skanami JPEG, wypisuje tekst każdej strony i podaje, jak długo trwała każda operacja. Bez zewnętrznych dokumentów do ścigania, bez półwypełnionych fragmentów kodu — po prostu pełne rozwiązanie, które możesz wrzucić do Visual Studio i uruchomić.

## Czego będziesz potrzebować

- **.NET 6.0** lub nowszy (kod kompiluje się także na .NET Framework 4.6+).
- **Aspose.OCR** pakiet NuGet (`Install-Package Aspose.OCR`)
- Kilka plików JPG lub zeskanowanych obrazów, które chcesz przetworzyć
- Dowolne IDE, które lubisz; używam Visual Studio 2022, ale VS Code również działa dobrze

To wszystko. Jeśli masz już pakiet NuGet, możesz zaczynać.

## Krok 1 – Inicjalizacja silnika OCR (Ustawienia wsadowkiego OCR obrazów)

Pierwszą rzeczą, którą robimy, jest stworzenie instancji `OcrEngine` i określenie, jakiego języka szukać. W większości przypadków wystarczy angielski, ale możesz zamienić `OcrLanguage.English` na dowolny obsługiwany język.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine and set the language to English
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };
```

*Dlaczego to ważne:* Inicjalizacja silnika raz i ponowne użycie go dla wszystkich obrazów jest znacznie bardziej wydajne niż tworzenie nowej instancji dla każdego pliku. Pozwala to także Aspose na współdzielenie zasobów wewnętrznych, co jest kluczowe dla **parallel OCR processing**.

## Krok 2 – Budowanie listy obrazów (Przetwarzanie listy obrazów)

Następnie definiujemy kolekcję ścieżek plików, które chcemy przekazać do wsadowego rozpoznawania. Możesz generować tę listę dynamicznie przy użyciu `Directory.GetFiles`, ale dla przejrzystości zakodujemy kilka pozycji na stałe.

```csharp
        // Step 2: Define the image files that will be processed
        var imagePaths = new List<string>
        {
            @"YOUR_DIRECTORY/page1.jpg",
            @"YOUR_DIRECTORY/page2.jpg",
            @"YOUR_DIRECTORY/page3.jpg"
        };
```

*Wskazówka:* Jeśli masz tysiące skanów, rozważ użycie `Directory.EnumerateFiles` z filtrem takim jak `*.jpg`, aby uniknąć ładowania całej listy do pamięci jednocześnie.

## Krok 3 – Uruchomienie wsadowego rozpoznawania (Równoległe przetwarzanie OCR)

Teraz dochodzi do sedna sprawy: wywołanie `BatchRecognize`. Metoda przyjmuje argument `maxDegreeOfParallelism`, który kontroluje, ile wątków Aspose uruchomi. Domyślnie używa czterech wątków, ale możesz zwiększyć tę liczbę, jeśli Twój procesor ma więcej rdzeni.

```csharp
        // Step 3: Run batch recognition (4 parallel threads by default)
        var recognitionResults = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);
```

*Co się dzieje w tle?* Aspose dzieli kolekcję `imagePaths` na fragmenty, przekazuje każdy fragment do osobnego wątku i agreguje wyniki. To najwydajniejszy sposób na **extract text from jpg** files, gdy masz **process image list**, którą można przetwarzać równocześnie.

## Krok 4 – Wyświetlanie wyników (Odczyt tekstu ze skanów)

Na koniec iterujemy po kolekcji `recognitionResults` i wypisujemy tekst oraz czas przetwarzania każdego pliku. Obiekt `OcrResult` podaje również nazwę pliku źródłowego, co pomaga przy logowaniu lub przechowywaniu wyników.

```csharp
        // Step 4: Output the results for each image
        foreach (var result in recognitionResults)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

**Oczekiwany wynik (przykład):**

```
File: C:\Scans\page1.jpg
Time: 1.34s
The quick brown fox jumps over the lazy dog.
----------------------------------------
File: C:\Scans\page2.jpg
Time: 1.27s
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----------------------------------------
File: C:\Scans\page3.jpg
Time: 1.41s
Invoice #12345
Total: $1,250.00
----------------------------------------
```

Zauważ, że każdy blok podaje nazwę pliku, czas trwania OCR oraz wyodrębniony tekst. To dokładnie informacje, których potrzebujesz, gdy **reading text from scans** w środowisku produkcyjnym.

## Obsługa typowych przypadków brzegowych

| Situation | What to Watch For | Quick Fix |
|-----------|-------------------|-----------|
| **Brakujący plik** | `FileNotFoundException` wyrzucony wewnątrz `BatchRecognize` | Zweryfikuj ścieżki przy użyciu `File.Exists` przed dodaniem do `imagePaths`. |
| **Nieobsługiwany format** | Aspose obsługuje tylko obrazy rastrowe (JPG, PNG, BMP, TIFF). | Najpierw skonwertuj PDF‑y na obrazy (użyj Aspose.PDF) lub pomiń te pliki. |
| **Presja pamięci** | Bardzo duże obrazy mogą wyczerpać RAM przy wielu wątkach. | Obniż `maxDegreeOfParallelism` lub zmniejsz rozmiar obrazów przed OCR. |
| **Tekst nie‑angielski** | Ustawiony język na angielski pominie inne skrypty. | Zmień `Language = OcrLanguage.French` (lub kombinację wielojęzyczną). |

Te wskazówki utrzymują Twoje wsadowe zadanie w stabilnym stanie, szczególnie gdy **processing an image list** pochodzi z przesyłek użytkowników lub archiwum skanów.

## Pro Tip – Dostosowywanie równoległości

Jeśli uruchomisz to na maszynie z 8‑rdzeniowym procesorem, zwiększ równoległość do 6 lub 8 i obserwuj przyspieszenie. Pamiętaj jednak, że każdy wątek zużywa pamięć na bitmapę. Dobre przybliżenie to:

```csharp
int cores = Environment.ProcessorCount;
int maxThreads = Math.Max(1, cores - 1); // leave one core free for UI/OS
```

Wstaw `maxThreads` do `BatchRecognize`, aby uzyskać dynamiczną, zależną od maszyny konfigurację.

## Pełny działający przykład (Gotowy do kopiowania i wklejenia)

Poniżej znajduje się kompletny program, gotowy do kompilacji. Wystarczy zamienić `YOUR_DIRECTORY` na ścieżkę, w której znajdują się Twoje skany JPG.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine – English language
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };

        // 2️⃣ Build the list of image files to process
        var imagePaths = new List<string>();
        string folder = @"C:\Scans"; // <-- change this
        foreach (var file in Directory.EnumerateFiles(folder, "*.jpg"))
        {
            imagePaths.Add(file);
        }

        if (imagePaths.Count == 0)
        {
            Console.WriteLine("No JPG files found in the specified folder.");
            return;
        }

        // 3️⃣ Run batch OCR – let the library use 4 threads (adjust as needed)
        var results = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);

        // 4️⃣ Output each result
        foreach (var result in results)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

> **Uwaga:** Linia `using System.IO;` jest wymagana dla pomocnika `Directory`. Kod wypisuje przyjazny komunikat, jeśli nie znajdzie żadnych JPG‑ów, zapobiegając cichej awarii.

## Zakończenie

Właśnie przedstawiliśmy czysty przepływ pracy **batch OCR images**, który **extracts text from jpg** files, **reads text from scans**, i efektywnie **processes an image list** przy użyciu **parallel OCR processing**. Pełny, uruchamialny przykład pokazuje dokładnie, jak skonfigurować silnik, podać mu kolekcję plików i obsłużyć wyniki — wszystko przy zachowaniu kontroli nad zużyciem pamięci i liczbą wątków.

Gotowy na kolejny krok? Spróbuj zamienić język na francuski, dodać konwersję PDF‑na‑obraz lub zapisać tekst OCR w bazie danych. Wzorzec pozostaje ten sam: inicjalizuj raz, podaj listę i pozwól Aspose wykonać ciężką pracę równolegle.

Masz pytania lub chcesz podzielić się własnymi modyfikacjami? Dodaj komentarz poniżej i powodzenia w kodowaniu! 

![Batch OCR images processing flow](https://example.com/placeholder.png "Diagram illustrating batch OCR images workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}