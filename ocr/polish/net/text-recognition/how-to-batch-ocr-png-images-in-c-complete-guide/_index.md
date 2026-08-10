---
category: general
date: 2026-03-17
description: Jak szybko przeprowadzić OCR wielu obrazów PNG w C#. Dowiedz się, jak
  wyodrębnić tekst z plików PNG, konwertować PNG na tekst oraz odczytywać obrazy z
  katalogu za pomocą prostego skryptu.
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: pl
og_description: Jak przetwarzać wsadowo obrazy PNG za pomocą OCR w C# z kodem krok
  po kroku. Wyodrębniaj tekst z plików PNG, konwertuj PNG na tekst i łatwo odczytuj
  obrazy z katalogu.
og_title: Jak przetwarzać wsadowo obrazy PNG za pomocą OCR w C# – Kompletny przewodnik
tags:
- OCR
- C#
- Image Processing
title: Jak wykonać wsadowe OCR obrazów PNG w C# – Kompletny przewodnik
url: /pl/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

markdown syntax.

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak przetwarzać wsadowo obrazy PNG OCR w C# – Kompletny przewodnik

Zastanawiałeś się kiedyś **jak przetwarzać wsadowo OCR** folder pełen zrzutów ekranu bez ręcznego otwierania każdego pliku? Nie jesteś sam – programiści często pytają, jak wsadowo OCR‑ować duże kolekcje PNG, zwłaszcza gdy celem jest wyodrębnienie tekstu z plików PNG do dalszej analizy.  

W tym tutorialu przejdziemy krok po kroku przez gotowy przykład w C#, który **wyodrębnia tekst z plików PNG**, **konwertuje PNG na tekst** i pokazuje najlepszy sposób **czytania obrazów z katalogu**. Po zakończeniu będziesz mieć jeden skrypt, który tworzy plik `.txt` obok każdego obrazu, oszczędzając godziny ręcznego kopiowania‑wklejania.

## Co osiągniesz

- Zainicjalizujesz silnik OCR raz i będziesz go używać w całym wsadzie.  
- Przeskanujesz każdy `*.png` w podanym folderze bez konieczności pisania własnej pętli.  
- Zapiszesz każdy wynik OCR do osobnego pliku tekstowego, zachowując oryginalną nazwę pliku.  
- Poradzisz sobie z typowymi przypadkami brzegowymi, takimi jak puste foldery czy pliki nie‑obrazowe.

### Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa także na .NET Core i .NET Framework).  
- Biblioteka OCR udostępniająca typy `OcrEngine`, `ImageStream` i `OcrResult` (np. fikcyjny **FastOCR** SDK użyty w przykładach).  
- Podstawowa znajomość C# – nie są potrzebne zaawansowane wzorce.

---

## Jak przetwarzać wsadowo obrazy PNG OCR – przegląd

Poniżej znajduje się **kompletny, gotowy do uruchomienia program**. Skopiuj go do nowego projektu konsolowego, zamień ścieżki zastępcze i naciśnij **F5**.

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **Oczekiwany wynik:** Dla każdego `image01.png` znajdziesz plik `image01.txt` zawierający rozpoznane znaki. Konsola wypisze każdy plik w miarę jego zapisywania.

![How to batch OCR diagram](how-to-batch-ocr-diagram.png "Diagram illustrating how to batch OCR PNG images using C#")

---

## Wyjaśnienie krok po kroku

### 1. Inicjalizacja silnika OCR – serce procesu  

Linia `var ocrEngine = new OcrEngine();` tworzy jedną instancję silnika, którą będziesz używać w całym wsadzie. Ponowne użycie silnika jest **kluczowe**, ponieważ większość bibliotek OCR alokuje ciężkie zasoby (np. modele językowe) przy konstrukcji. Inicjalizacja raz znacznie poprawia wydajność – szczególnie przy dziesiątkach lub setkach PNG.

> **Porada:** Jeśli potrzebujesz języka innego niż angielski, ustaw `ocrEngine.Config.Language = Language.Spanish;` (lub dowolny obsługiwany enum).  

### 2. Czytanie obrazów z katalogu – znajdowanie każdego PNG  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` robi dokładnie to, co obiecuje drugie słowo kluczowe *read images from directory*. Zwraca tablicę pełnych ścieżek, które później przekazujemy silnikowi OCR.  

> **Dlaczego nie używać `SearchOption.AllDirectories`?** Jeśli obrazy są zagnieżdżone, możesz przełączyć się na `GetFiles(path, "*.png", SearchOption.AllDirectories)`. Pamiętaj jednak, że głębsze skanowanie może przynieść niechciane pliki, więc filtruj je odpowiednio.

### 3. Konwersja ścieżek plików na obiekty ImageStream  

Większość SDK‑ów OCR oczekuje strumienia zamiast surowej ścieżki. Wyrażenie LINQ `Select(path => ImageStream.FromFile(path)).ToList()` buduje **listę strumieni**, którą rozpoznawacz wsadowy może przetworzyć w jednym wywołaniu. Ten krok zapewnia także, że uchwyty plików są otwierane tylko raz, co zmniejsza obciążenie I/O.

> **Przypadek brzegowy:** Jeśli plik jest uszkodzony, `ImageStream.FromFile` może rzucić wyjątek. Owiń konwersję w `try/catch`, jeśli potrzebujesz odporności.

### 4. Rozpoznawanie tekstu w całym wsadzie  

`ocrEngine.RecognizeBatch(imageStreams)` to idealne rozwiązanie dla *how to batch OCR*. Zamiast iterować po każdym obrazie i wywoływać metodę jednego obrazu, przekazujemy całą kolekcję silnikowi. Biblioteka wewnętrznie może równolegle przetwarzać zadania, dając przyspieszenie na maszynach wielordzeniowych.

> **Wskazówka:** Jeśli Twoja biblioteka OCR nie udostępnia metody wsadowej, możesz uzyskać podobną wydajność, używając `Parallel.ForEach` wokół pojedynczej metody `Recognize`.

### 5. Zapis każdego wyniku OCR – konwersja PNG na tekst  

Ostatnia pętla `for` zapisuje `ocrResults[i].Text` do pliku `.txt`, którego nazwa odzwierciedla oryginalny PNG. To dokładnie to, co opisuje drugie słowo kluczowe *convert PNG to text*. Wywołanie `Path.Combine` zapewnia, że folder wyjściowy istnieje i zapobiega błędom związanym z traversją ścieżek.

> **Częsty błąd:** Zapomnienie o utworzeniu katalogu wyjściowego spowoduje `DirectoryNotFoundException`. Linia `Directory.CreateDirectory(outputFolder);` rozwiązuje to z wyprzedzeniem.

---

## Obsługa rzeczywistych wariantów

| Sytuacja | Co zmienić | Dlaczego |
|-----------|------------|----------|
| **Pusty folder wejściowy** | Zachowaj wczesny warunek `if (imagePaths.Length == 0)` | Zapobiega niepotrzebnemu wywołaniu OCR i wyświetla przyjazny komunikat |
| **Mieszane typy plików** | Użyj `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` | Gwarantuje przetwarzanie wyłącznie PNG, spełniając *extract text png* bez błędów |
| **Bardzo duże obrazy ( > 5 MB )** | Zmniejsz rozdzielczość przed przekazaniem do OCR: `ImageStream.FromFile(path).Resize(1920, 1080)` (jeśli API to obsługuje) | Redukuje obciążenie pamięci i często poprawia dokładność rozpoznawania |
| **Inny język OCR** | Ustaw `ocrEngine.Config.Language = Language.French;` | Dopasowuje silnik do języka źródłowych obrazów |

---

## Najczęściej zadawane pytania (FAQ)

**P: Czy to działa z plikami JPEG lub TIFF?**  
O: Logika pozostaje taka sama; wystarczy zmienić wzorzec wyszukiwania na `"*.jpg"` lub `"*.tif"` oraz upewnić się, że biblioteka OCR potrafi dekodować te formaty.

**P: Jak przetwarzać tysiące obrazów, nie wyczerpując pamięci?**  
O: Zastąp wywołanie wsadowe podejściem strumieniowym – przetwarzaj porcję, np. 50 obrazów naraz, zwalniaj strumienie, a potem wczytuj kolejną porcję.

**P: Potrzebuję wyniku zaufania OCR. Gdzie go znaleźć?**  
O: Większość obiektów `OcrResult` udostępnia właściwość `Confidence`. Możesz rozbudować krok zapisu:

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

---

## Podsumowanie

Właśnie omówiliśmy **jak przetwarzać wsadowo OCR** obrazy PNG w C# od początku do końca. Inicjalizując pojedynczy silnik, czytając obrazy z katalogu, konwertując je na strumienie, rozpoznając cały wsad i zapisując każdy wynik do pliku tekstowego, masz teraz solidny, gotowy do produkcji wzorzec dla zadań **extract text PNG**, **convert PNG to text** oraz **read images from directory**.

Co dalej? Spróbuj zamienić dostawcę OCR, dodaj wielowątkowe przetwarzanie post‑OCR (np. sprawdzanie pisowni) lub wprowadź pliki `.txt` do indeksu wyszukiwania. Niebo jest granicą, gdy opanujesz przepływ wsadowy.

Masz własny pomysł, którym chcesz się podzielić? Dodaj komentarz i powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}