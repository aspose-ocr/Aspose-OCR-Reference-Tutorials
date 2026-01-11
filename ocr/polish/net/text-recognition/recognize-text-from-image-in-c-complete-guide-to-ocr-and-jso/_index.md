---
category: general
date: 2026-01-10
description: Dowiedz się, jak rozpoznawać tekst z obrazu, wyodrębniać współrzędne
  tekstu i konwertować paragon na JSON przy użyciu Aspose OCR w C#. Samouczek krok
  po kroku.
draft: false
keywords:
- recognize text from image
- how to extract text
- extract text coordinates
- convert receipt to json
language: pl
og_description: Rozpoznaj tekst z obrazu w C# przy użyciu Aspose OCR. Ten przewodnik
  pokazuje, jak wyodrębnić tekst, uzyskać współrzędne i przekształcić paragon do formatu
  JSON.
og_title: rozpoznawanie tekstu z obrazu – Pełny samouczek OCR w C#
tags:
- OCR
- C#
- Aspose
title: rozpoznawanie tekstu z obrazu w C# – Kompletny przewodnik po OCR i JSON
url: /pl/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznawanie tekstu z obrazu – Pełny samouczek OCR w C#

Kiedykolwiek potrzebowałeś rozpoznać tekst z obrazu, ale nie wiedziałeś, której biblioteki użyć? Nie jesteś sam. W wielu rzeczywistych aplikacjach — monitorach wydatków, skanerach paragonów czy archiwizatorach dokumentów — wyodrębnienie tekstu w sposób niezawodny jest pierwszą przeszkodą.  

W tym samouczku przejdziemy przez **sposób wyodrębniania tekstu**, pobieranie jego prostokątów ograniczających oraz w końcu **konwersję paragonu do JSON** przy użyciu Aspose.OCR dla .NET. Po zakończeniu będziesz mieć samodzielny projekt C#, który przyjmuje zdjęcie paragonu i generuje schludny plik JSON z ocenami pewności i współrzędnymi.

## Co będzie potrzebne

Zanim zaczniemy, upewnij się, że masz na swoim komputerze następujące elementy:

- **.NET 6.0 SDK** (lub nowszą wersję). Starsze frameworki też działają, ale .NET 6 to optymalny wybór dla nowoczesnych bibliotek.
- **Visual Studio 2022** lub VS Code z rozszerzeniem C#.
- **Aspose.OCR for .NET** pakiet NuGet (`Aspose.OCR` i `Aspose.OCR.Output`). Możesz go zainstalować za pomocą Package Manager Console:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Output
```

- Przykładowy obraz paragonu (np. `receipt.jpg`) umieszczony w folderze, do którego odwołasz się później.

To wszystko — żadnych dodatkowych SDK, żadnych natywnych binarek, tylko czysty kod zarządzany.

## Krok 1: Utwórz nowy projekt konsolowy

Na początek, uruchom aplikację konsolową. To najszybszy sposób na przetestowanie OCR bez nakładów UI.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later.
        }
    }
}
```

> **Wskazówka:** Utrzymuj folder projektu w porządku; utwórz podfolder o nazwie `Resources` i wrzuć tam `receipt.jpg`. Ułatwi to obsługę ścieżek.

## Krok 2: Załaduj obraz paragonu

Teraz faktycznie **rozpoznajemy tekst z obrazu**. Pierwszy krok to wskazanie silnikowi OCR pliku.

```csharp
// Inside Main()
string imagePath = @"Resources/receipt.jpg";
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Image = ImageStream.FromFile(imagePath)
};

Console.WriteLine("✅ Image loaded successfully.");
```

Dlaczego otaczamy ładowanie prostą kontrolą istnienia? Ponieważ w produkcji często masz do czynienia z przesyłanymi przez użytkownika plikami, które mogą być brakujące lub uszkodzone. Wczesne wykrycie problemu chroni przed niejasnymi wyjątkami później.

## Krok 3: Wykonaj OCR – **rozpoznawanie tekstu z obrazu**

Mając obraz w pamięci, prosimy Aspose o **rozpoznanie tekstu z obrazu**. Operacja jest synchroniczna i zwraca bogaty zestaw wyników.

```csharp
// Still inside Main()
try
{
    ocrEngine.Recognize();
    Console.WriteLine("🧠 OCR completed.");
}
catch (Exception ex)
{
    Console.WriteLine($"❗ OCR failed: {ex.Message}");
    return;
}
```

Za kulisami Aspose uruchamia sieć neuronową wytrenowaną na milionach znaków. Silnik wypełnia `ocrEngine.Text`, `ocrEngine.RecognitionResult` oraz kolekcję obiektów `OcrRegion` zawierających współrzędne. To dokładnie to, czego potrzebujemy do kolejnego kroku.

## Krok 4: **Jak wyodrębnić tekst** – Pobieranie surowego ciągu znaków

Jeśli interesuje Cię tylko czysty tekst (np. do szybkiego wyszukiwania), możesz go pobrać bezpośrednio z silnika:

```csharp
string plainText = ocrEngine.Text;
Console.WriteLine("\n--- Extracted Text ---");
Console.WriteLine(plainText);
```

Zauważysz znaki nowej linii tam, gdzie OCR wykrył granice akapitów. W wielu scenariuszach skanowania paragonów surowy ciąg wystarcza, aby wyciągnąć sumy, daty czy nazwy sprzedawców przy użyciu prostych wyrażeń regularnych.

## Krok 5: **wyodrębnianie współrzędnych tekstu** – Prostokąty ograniczające dla każdego słowa

Często potrzebujesz wiedzieć, *gdzie* na obrazie znajduje się konkretny fragment tekstu — na przykład, aby podświetlić kwotę końcową w interfejsie. Aspose udostępnia to poprzez obiekty `OcrRegion`.

```csharp
Console.WriteLine("\n--- Text Coordinates (extract text coordinates) ---");
foreach (var region in ocrEngine.RecognitionResult.Regions)
{
    // Each region represents a word or a line depending on the engine settings.
    string word = region.Text;
    var bounds = region.BoundingBox; // X, Y, Width, Height
    Console.WriteLine($"Word: \"{word}\" | Box: X={bounds.X}, Y={bounds.Y}, W={bounds.Width}, H={bounds.Height}");
}
```

Zauważ, że iterujemy po **wyodrębnianiu współrzędnych tekstu** dla każdego rozpoznanego segmentu. Współrzędne są względem oryginalnego obrazu, więc możesz je nakładać na płótno graficzne lub element HTML `<canvas>`.

## Krok 6: **konwersja paragonu do JSON** – Zapisywanie szczegółowych wyników

Teraz przychodzi część, która łączy wszystko razem: potrzebujemy struktury czytelnej dla maszyn, zawierającej tekst, oceny pewności i prostokąty ograniczające. Aspose dostarcza `JsonSaveOptions`, co czyni to zadanie bajecznie prostym.

```csharp
// Define where the JSON will be saved
string jsonPath = @"Resources/receipt.json";

// Configure JSON options to keep confidence and bounding boxes
JsonSaveOptions jsonOptions = new JsonSaveOptions
{
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};

// Save the OCR result
ocrEngine.Save(jsonPath, jsonOptions);
Console.WriteLine($"\n💾 Detailed OCR results saved to {jsonPath}");
```

Powstały plik wygląda mniej więcej tak (skrócony dla przejrzystości):

```json
{
  "Regions": [
    {
      "Text": "Store",
      "Confidence": 0.99,
      "BoundingBox": { "X": 45, "Y": 120, "Width": 80, "Height": 20 }
    },
    {
      "Text": "Total",
      "Confidence": 0.97,
      "BoundingBox": { "X": 300, "Y": 560, "Width": 70, "Height": 22 }
    }
    // ... more regions ...
  ]
}
```

Masz teraz artefakt **konwersji paragonu do JSON**, który może być przekazany do usług downstream — myśl o API raportów wydatków, potokach analitycznych lub prostym UI rysującym prostokąty wokół każdego słowa.

## Pełny działający przykład

Łącząc wszystkie elementy, oto kompletny `Program.cs`, który możesz skopiować i wkleić do swojego projektu:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image
            // -------------------------------------------------
            string imagePath = @"Resources/receipt.jpg";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            OcrEngine ocrEngine = new OcrEngine
            {
                Image = ImageStream.FromFile(imagePath)
            };
            Console.WriteLine("✅ Image loaded.");

            // -------------------------------------------------
            // 2️⃣ Run OCR – recognize text from image
            // -------------------------------------------------
            try
            {
                ocrEngine.Recognize();
                Console.WriteLine("🧠 OCR completed.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❗ OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 3️⃣ Extract plain text (how to extract text)
            // -------------------------------------------------
            Console.WriteLine("\n--- Extracted Text ---");
            Console.WriteLine(ocrEngine.Text);

            // -------------------------------------------------
            // 4️⃣ Get coordinates (extract text coordinates)
            // -------------------------------------------------
            Console.WriteLine("\n--- Text Coordinates ---");
            foreach (var region in ocrEngine.RecognitionResult.Regions)
            {
                var box = region.BoundingBox;
                Console.WriteLine($"Word: \"{region.Text}\" | Box: X={box.X}, Y={box.Y}, W={box.Width}, H={box.Height}");
            }

            // -------------------------------------------------
            // 5️⃣ Save detailed JSON (convert receipt to json)
            // -------------------------------------------------
            string jsonPath = @"Resources/receipt.json";
            JsonSaveOptions jsonOptions = new JsonSaveOptions
            {
                IncludeConfidence = true,
                IncludeBoundingBoxes = true
            };
            ocrEngine.Save(jsonPath, jsonOptions);
            Console.WriteLine($"\n💾 JSON saved at {jsonPath}");
        }
    }
}
```

Uruchom program (`dotnet run`) i obserwuj wyjście w konsoli. Otwórz `Resources/receipt.json`, aby zweryfikować strukturę.

## Częste pytania i sytuacje brzegowe

- **Co zrobić, gdy obraz jest rozmyty?**  
  Aspose OCR działa najlepiej przy 300 dpi lub wyższym. Jeśli otrzymujesz niskie oceny pewności, rozważ zastosowanie filtru wyostrzającego przed przekazaniem obrazu do silnika.

- **Czy mogę rozpoznawać wiele języków?**  
  Tak. Ustaw `ocrEngine.Language = Language.English | Language.Spanish;` przed wywołaniem `Recognize()`.

- **Jak ograniczyć wynik tylko do liczb (np. sum)?**  
  Po uzyskaniu czystego tekstu, uruchom wyrażenie regularne takie jak `\d+\.\d{2}` na `ocrEngine.Text`. Ponieważ masz już współrzędne, możesz odwzorować dopasowany ciąg na jego region w celu wizualnego podświetlenia.

- **Czy format JSON można dostosować?**  
  Klasa `JsonSaveOptions` udostępnia kilka flag. Jeśli potrzebujesz całkowicie własnego schematu, możesz przeiterować `ocrEngine.RecognitionResult.Regions` i samodzielnie serializować obiekty przy użyciu `System.Text.Json`.

## Zakończenie

Pokazaliśmy, jak **rozpoznawać tekst z obrazu** w C# przy użyciu Aspose.OCR, **wyodrębnić tekst**, pobrać **wyodrębnianie współrzędnych tekstu**, a na końcu **konwertować paragon do JSON**. Cały przepływ mieści się w jednej, łatwej do uruchomienia aplikacji konsolowej, co czyni go idealnym do prototypów lub jako element większych systemów.

Co dalej? Spróbuj podać JSON do front‑endu, który rysuje prostokąty, lub podłącz wynik do usługi raportowania wydatków. Możesz także eksperymentować z różnymi formatami obrazów (PNG, TIFF) lub przetwarzać wsadowo folder z paragonami.

Masz więcej pytań o OCR, Aspose lub obsługę JSON? Zostaw komentarz poniżej i powodzenia w kodowaniu! 

![Przykład obrazu paragonu dla rozpoznawania tekstu z obrazu](receipt.jpg "Przykład obrazu paragonu dla rozpoznawania tekstu z obrazu")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}