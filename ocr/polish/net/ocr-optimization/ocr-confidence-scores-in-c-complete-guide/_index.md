---
category: general
date: 2026-05-31
description: Dowiedz się, jak uzyskać wyniki pewności OCR w C# podczas wyodrębniania
  tekstu z obrazu i odczytywania obrazu paragonu przy użyciu Aspose OCR.
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: pl
og_description: Wyniki pewności OCR pozwalają ocenić dokładność; ten przewodnik pokazuje,
  jak wyodrębnić tekst z obrazu, uzyskać ramki ograniczające oraz odczytać obraz paragonu
  przy użyciu Aspose OCR.
og_title: Wyniki pewności OCR w C# – Kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Wyniki pewności OCR w C# – Kompletny przewodnik
url: /pl/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR confidence scores w C# – Kompletny przewodnik

Zastanawiałeś się kiedyś, jak uzyskać **OCR confidence scores**, gdy potrzebujesz *extract text from image*? Może próbujesz **read receipt image** w celu śledzenia wydatków i chcesz wiedzieć, które znaki silnik rozpoznaje z niepewnością. Dobre wieści? Dzięki Aspose.OCR możesz pobrać procenty pewności, bounding boxes i zwykły tekst z pliku JPG w zaledwie kilku linijkach C#.

W tym tutorialu przejdziemy przez wszystko, co musisz wiedzieć: instalację biblioteki, konfigurację silnika do **perform OCR on JPG**, pobieranie wyników pewności oraz interpretację **OCR bounding boxes**, które pokazują, gdzie każdy znak znajduje się na stronie. Na koniec będziesz mieć gotową do uruchomienia aplikację konsolową, która wypisuje każdy znak, jego pewność i położenie — idealną do weryfikacji paragonów lub dowolnego zeskanowanego dokumentu.

## Co się nauczysz

- Zainstaluj Aspose.OCR za pomocą NuGet i skonfiguruj podstawowy silnik OCR.  
- Skonfiguruj `OcrOptions`, aby żądać wyjścia plain‑text **with confidence scores** i **bounding boxes**.  
- Przeglądaj `OcrResult`, aby **extract text from image** wiersz po wierszu i znak po znaku.  
- Radź sobie z typowymi problemami, takimi jak brakujące pliki, znaki o niskiej pewności i formaty nie‑JPG.  
- Rozszerz przykład, aby przetwarzać wiele obrazów paragonów w folderze.

Nie wymagana jest wcześniejsza znajomość Aspose; wystarczy działające środowisko .NET oraz obraz paragonu (JPG), który chcesz przetestować.

---

## Krok 1 – Instalacja Aspose.OCR i przygotowanie projektu

Na początek potrzebujesz pakietu NuGet Aspose.OCR. Otwórz terminal w folderze projektu i uruchom:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Darmowa wersja próbna działa do 200 stron, co jest więcej niż wystarczające do testowania skanowania paragonów.

Po zainstalowaniu pakietu, utwórz nowy projekt konsolowy (jeśli jeszcze go nie masz):

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

Teraz możesz otworzyć wygenerowany plik `Program.cs` i dodać dyrektywy using:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

Te przestrzenie nazw dają dostęp do `OcrEngine`, `OcrOptions` oraz typów wyników, których będziemy potrzebować później.

## Krok 2 – Pobieranie OCR confidence scores i OCR bounding boxes

To jest serce tutorialu. Skonfigurujemy silnik tak, aby każdy rozpoznany znak posiadał **confidence score** i **bounding box** (prostokąt obejmujący glif). Sam nagłówek H2 zawiera główne słowo kluczowe, spełniając wymóg SEO.

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**Dlaczego uwzględniać confidence scores?**  
Wynik pewności (0‑100%) informuje, jak pewny jest silnik co do każdego znaku. Jeśli przekazujesz wynik do dalszej logiki — np. procesu zatwierdzania wydatków — możesz automatycznie odrzucać lub oznaczać symbole o niskiej pewności.

**Dlaczego żądać bounding boxes?**  
Bounding boxes są niezbędne, gdy musisz podświetlić tekst na oryginalnym obrazie, wyodrębnić podobszary lub dopasować wyniki OCR do nakładki UI. Każdy `character.Bounds` podaje współrzędne X, Y, szerokość i wysokość w pikselach.

## Krok 3 – Wykonanie OCR na JPG i extract text from image

Teraz faktycznie uruchamiamy silnik. Wywołanie `Recognize()` wykonuje całą ciężką pracę i zwraca obiekt `OcrResult`.

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

Jeśli ścieżka do obrazu jest nieprawidłowa lub plik nie jest w obsługiwanym formacie, Aspose rzuca `FileNotFoundException` lub `UnsupportedImageFormatException`. W kodzie produkcyjnym otocz wywołanie blokiem try/catch, aby elegancko obsłużyć te przypadki.

### Pobieranie plain text

Jeśli potrzebujesz tylko połączonego tekstu, możesz odczytać `ocrResult.Text`:

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

Jednak ponieważ poprosiliśmy również o confidence scores i bounding boxes, przeiterujemy strukturę, aby zobaczyć szczegóły każdego znaku.

## Krok 4 – Iteracja przez linie, symbole i wyświetlanie OCR confidence scores

Oto pętla, która wypisuje każdy znak, jego pewność i jego prostokąt. To miejsce, w którym przykład **read receipt image** naprawdę błyszczy.

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

Przykładowe wyjście może wyglądać tak:

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**Interpretacja liczb:**  
- **Confidence ≥ 90%** – zazwyczaj bezpieczne do akceptacji.  
- **Confidence 70‑89%** – warto podwójnie sprawdzić, szczególnie cyfry w kwotach.  
- **Confidence < 70%** – rozważ oznaczenie do ręcznej weryfikacji.

## Krok 5 – Pełny działający przykład (z obsługą błędów)

Łącząc wszystko razem, oto kompletny program, który możesz skopiować i wkleić do `Program.cs`. Zawiera prostą kontrolę brakujących plików i wyświetla przyjazny komunikat, jeśli OCR się nie powiedzie.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Oczekiwane wyjście

Gdy uruchomisz `dotnet run`, konsola najpierw wyświetli połączony tekst paragonu, a następnie listę każdego znaku z jego wynikiem pewności i bounding box. Jeśli pewność znaku jest niska, zobaczysz procent poniżej 80, co jest sygnałem, aby ręcznie zweryfikować tę część paragonu.

## Bonus: Przetwarzanie wielu paragonów w folderze

Jeśli masz zestaw plików JPG z paragonami, otocz powyższą logikę pętlą `foreach (var file in Directory.GetFiles(folder, "*.jpg"))`. Pamiętaj, aby zresetować `OcrEngine` dla każdego pliku lub utworzyć nową instancję wewnątrz pętli, aby uniknąć wycieków stanu.

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

Przetwarzanie wsadowe jest przydatne przy nocnych importach wydatków.

---

## Podsumowanie

Masz teraz solidne, kompleksowe rozwiązanie do uzyskiwania **OCR confidence scores** w C#, **extracting text from image** i pobierania **OCR bounding boxes**, podczas **perform OCR on JPG** plików, takich jak **read receipt image**. Kod jest w pełni samodzielny, działa z najnowszą wersją Aspose.OCR (stan na 2026‑05‑31) i dostarcza szczegółowych danych potrzebnych do budowy wiarygodnych pipeline'ów przetwarzania dokumentów.

Co dalej? Spróbuj zwizualizować bounding boxes na oryginalnym paragonie przy użyciu `System.Drawing` lub biblioteki UI, albo przekazać znaki o niskiej pewności do dodatkowej usługi weryfikacji. Możesz także eksperymentować z różnymi językami, ustawiając `ocrEngine.Options.Language = OcrLanguage.French;` — API obsługuje wiele lokalizacji.

Miłego kodowania i niech Twoje wyniki pewności zawsze pozostają wysokie! 

![Wyjście konsoli pokazujące OCR confidence scores i bounding boxes dla paragonu

## Co powinieneś nauczyć się dalej?

- [Wyodrębnianie tekstu z obrazu w C# z wyborem języka przy użyciu Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Jak uzyskać wybory znaków OCR dla rozpoznanych znaków w rozpoznawaniu obrazu](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [Jak używać Aspose OCR do uzyskania wyniku JSON w rozpoznawaniu obrazu](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}