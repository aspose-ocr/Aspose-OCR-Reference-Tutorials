---
category: general
date: 2026-02-13
description: Jak używać OCR w C#, aby wyodrębnić tekst z obrazu, rozpoznać tekst ze
  zdjęcia lub JPG oraz uruchomić OCR na obrazie bez internetu.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from photo
- recognize text from jpg
- run OCR on image
language: pl
og_description: Jak używać OCR w C#, aby wyodrębnić tekst z obrazu, rozpoznać tekst
  ze zdjęcia i uruchomić OCR na obrazie, z kompletnym, działającym przykładem.
og_title: Jak używać OCR w C# – wyodrębnianie tekstu z obrazu
tags:
- OCR
- C#
- Image Processing
title: Jak używać OCR w C# – wyodrębniaj tekst z obrazu i rozpoznawaj tekst ze zdjęcia
url: /pl/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-and-recognize-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać OCR w C# – wyodrębniać tekst z obrazu i rozpoznawać tekst ze zdjęcia

Zastanawiałeś się kiedyś **jak używać OCR**, aby wyciągnąć słowa ze zrzutu ekranu, zeskanowanego paragonu lub przypadkowego zdjęcia zrobionego telefonem? Nie jesteś jedyny. W wielu rzeczywistych aplikacjach musimy zamienić obrazy na tekst przeszukiwalny, a robienie tego lokalnie—bez niestabilnego połączenia internetowego—może przypominać zagadkę.

To dlatego ten przewodnik pokazuje krok po kroku, jak **wyodrębnić tekst z obrazu** przy użyciu silnika OCR w C#, a także jak **rozpoznać tekst ze zdjęcia**, **rozpoznać tekst z JPG** i **uruchomić OCR na obrazie** znajdującym się bezpośrednio na dysku. Po zakończeniu będziesz mieć kompletny program gotowy do kopiowania i wklejania, który działa od razu.

## Czego się nauczysz

- Jak skonfigurować silnik OCR dla chińskiego uproszczonego (lub dowolnego języka, który podłączysz).  
- Dokładny kod potrzebny do **załadowania zasobów** z lokalnego folderu—bez konieczności wywołań sieciowych.  
- Jak **rozpoznać tekst ze zdjęcia** w plikach takich jak JPEG, PNG lub BMP.  
- Wskazówki dotyczące obsługi typowych przypadków brzegowych, takich jak brakujące pliki modelu lub nieobsługiwane formaty obrazów.  
- Pełny, działający przykład, który możesz wkleić do Visual Studio i od razu zobaczyć wyniki.

### Wymagania wstępne

- .NET 6.0 lub nowszy (API użyte tutaj celuje w .NET Standard 2.0, więc starsze wersje również działają).  
- Podstawowa znajomość C# i Visual Studio (lub dowolnego ulubionego IDE).  
- Biblioteka OCR, której używasz (fragment zakłada fikcyjną klasę `OcrEngine`, dostarczaną z modelami językowymi).  
- Folder zawierający wymagane pliki modeli językowych — można go traktować jako „mózg”, którego silnik używa do odczytywania chińskich znaków.

> **Pro tip:** Jeśli nie masz jeszcze chińskich plików modelu, pobierz je raz ze strony dostawcy i umieść w folderze takim jak `C:\OcrResources`. Silnik nigdy nie będzie musiał ponownie łączyć się z internetem.

---

![Diagram pokazujący proces OCR na zdjęciu](path/to/ocr-diagram.png "Diagram pokazujący proces OCR na zdjęciu")

## Jak używać OCR: konfiguracja silnika

Pierwszą rzeczą, której potrzebujesz, jest instancja silnika OCR, skonfigurowana dla wybranego języka. W tym tutorialu celujemy w **chiński uproszczony**, ale zamiana `OcrLanguage.ChineseSimplified` na `OcrLanguage.English` (lub dowolną inną wartość wyliczenia) to tylko jednowierszowa zmiana.

```csharp
using System;
using YourOcrLibrary;   // Replace with the actual namespace of your OCR SDK

// Step 1: Create and configure the OCR engine for Simplified Chinese
var ocrEngine = new OcrEngine
{
    // Primary keyword appears here naturally
    Language = OcrLanguage.ChineseSimplified,

    // Point to a folder that already contains the Chinese model files
    ResourceFolder = @"C:\OcrResources"
};
```

**Dlaczego to ważne:**  
Ustawienie właściwości `Language` informuje silnik, jakiego zestawu znaków się spodziewać. `ResourceFolder` to miejsce, w którym silnik szuka wag sieci neuronowej i słowników językowych — można to traktować jako bank pamięci mózgu. Jeśli wskażesz niewłaściwy folder, silnik wyrzuci `FileNotFoundException` i utkniesz.

## Wyodrębnianie tekstu z obrazu – ładowanie zasobów

Zanim silnik będzie mógł faktycznie coś odczytać, musisz załadować te pliki modelu do pamięci. Ten krok jest **kluczowy**, ponieważ unika wywołań sieciowych przy każdym przetwarzaniu obrazu.

```csharp
// Step 2: Load the language resources from the specified folder (no internet required)
try
{
    ocrEngine.LoadResources();
    Console.WriteLine("Resources loaded successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to load OCR resources: {ex.Message}");
    // In a real app you might fallback to a default language or abort gracefully
}
```

**Co może pójść nie tak?**  
Jeśli ścieżka folderu jest nieprawidłowa lub pliki są uszkodzone, `LoadResources()` zgłosi wyjątek. Powyższy blok `try/catch` demonstruje elegancką obsługę błędów — coś, czego często potrzebujesz w produkcji.

## Rozpoznawanie tekstu ze zdjęcia – uruchamianie OCR

Teraz najciekawsza część: podanie pliku obrazu do silnika i otrzymanie rozpoznanego tekstu. To jest sedno scenariuszy **uruchamiania OCR na obrazie**, niezależnie od tego, czy obraz jest JPEG, PNG, czy nawet BMP.

```csharp
// Step 3: Recognize text from an image file
string imagePath = @"C:\OcrResources\photo.jpg";

try
{
    var recognitionResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(recognitionResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
}
```

Metoda `RecognizeImage` zwraca `RecognitionResult` (lub cokolwiek twoje SDK tak nazywa), który zazwyczaj zawiera:

- `Text` – transkrypcję w postaci zwykłego tekstu.  
- `Confidence` – liczbową ocenę wskazującą, jak pewny jest silnik co do każdej linii.  
- `BoundingBoxes` – opcjonalne współrzędne określające, gdzie każde słowo znajduje się na obrazie.

**Dlaczego możesz się interesować pewnością:**  
Jeśli budujesz narzędzie do automatyzacji wprowadzania danych, możesz ustawić próg (np. 0.85) i poprosić użytkownika o potwierdzenie linii o niskiej pewności. To znacząco poprawia ogólną dokładność.

## Rozpoznawanie tekstu z JPG – obsługa różnych formatów

Wielu programistów zakłada, że OCR działa tylko z PNG, ale nowoczesne silniki radzą sobie doskonale z plikami **JPG**. Jedyną pułapką jest to, że kompresja JPEG może wprowadzać artefakty, które dezorientują model.

```csharp
// Bonus: Recognize text from a JPG with optional preprocessing
string jpgPath = @"C:\OcrResources\scanned_doc.jpg";

// Optional: use a simple image‑preprocess step to improve accuracy
var preprocessed = ImageHelper.DenoiseAndDeskew(jpgPath); // pseudo‑method
var result = ocrEngine.RecognizeImage(preprocessed);
Console.WriteLine($"Detected text ({result.Confidence:P0} confidence):");
Console.WriteLine(result.Text);
```

Jeśli nie masz pomocnika `DenoiseAndDeskew`, wiele bibliotek (np. OpenCvSharp) udostępnia te funkcje. Najważniejsze wnioski: **uruchamiaj OCR na obrazie** po krótkim oczyszczeniu, jeśli pochodzą ze skanera lub kamery telefonu.

## Uruchamianie OCR na obrazie – wskazówki, przypadki brzegowe i najlepsze praktyki

### 1. Zarządzanie pamięcią
Ładowanie dużych modeli językowych może zużywać setki megabajtów. Zwalniaj silnik po zakończeniu:

```csharp
ocrEngine.Dispose(); // or using statement if the SDK implements IDisposable
```

### 2. Przetwarzanie wsadowe
Jeśli musisz przetworzyć dziesiątki zdjęć, załaduj zasoby raz, a potem iteruj:

```csharp
string[] files = Directory.GetFiles(@"C:\BatchPhotos", "*.jpg");
foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), res.Text);
}
```

### 3. Scenariusze wielojęzykowe
Możesz przełączać języki w locie, przypisując `ocrEngine.Language` i ponownie wywołując `LoadResources()`. Pamiętaj jednak o dodatkowym czasie ładowania.

### 4. Obsługa pustych wyników
Czasami silnik zwraca pusty ciąg znaków. Zwykle oznacza to, że obraz jest zbyt rozmyty lub kolor tekstu stapia się z tłem. Szybka kontrola:

```csharp
if (string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text detected – consider increasing image contrast.");
}
```

### 5. Aspekty bezpieczeństwa
Nigdy nie podawaj plików przesłanych przez użytkownika bezpośrednio do silnika OCR bez walidacji. Przynajmniej sprawdź rozszerzenie pliku i jego rozmiar oraz rozważ skanowanie pod kątem malware.

---

## Kompletny działający przykład

Poniżej znajduje się pojedynczy, samodzielny program, który możesz skopiować do nowego projektu aplikacji konsolowej. Demonstruje **jak używać OCR**, **wyodrębnić tekst z obrazu**, **rozpoznać tekst ze zdjęcia**, **rozpoznać tekst z JPG** oraz **uruchomić OCR na obrazie** — wszystko w jednym kroku.

```csharp
// File: Program.cs
using System;
using System.IO;
using YourOcrLibrary; // Replace with actual namespace

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // ------------------------------
            // 1️⃣ Configure the OCR engine
            // ------------------------------
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified,
                ResourceFolder = @"C:\OcrResources"
            };

            // Load language resources (no internet needed)
            try
            {
                ocrEngine.LoadResources();
                Console.WriteLine("Resources loaded.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Failed to load resources: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Recognize text from a photo (JPG in this case)
            // -------------------------------------------------
            string imagePath = @"C:\OcrResources\photo.jpg";

            if (!File.Exists(imagePath))
            {
                Console.Error.WriteLine($"Image not found: {imagePath}");
                return;
            }

            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("\n=== OCR Output ===");
                Console.WriteLine(result.Text);
                Console.WriteLine($"\nConfidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"OCR error: {ex.Message}");
            }

            // Clean up
            ocrEngine.Dispose();
        }
    }
}
```

**Oczekiwany wynik (przykład):**

```
Resources loaded.

=== OCR Output ===
中华人民共和国
北京
2026年02月13日

Confidence: 92.45%
```

Twój rzeczywisty tekst będzie się różnił w zależności od zawartości obrazu, ale powinieneś zobaczyć blok znaków Unicode wydrukowany w konsoli wraz z procentem pewności.

---

## Podsumowanie

Przeszliśmy przez **jak używać OCR** w C# od początku do końca — konfigurację silnika, ładowanie zasobów językowych i w końcu **rozpoznawanie tekstu ze zdjęcia** lub **JPG** bez konieczności łączenia się z internetem. Postępując zgodnie z powyższymi krokami, możesz **wyodrębnić tekst z obrazu**, **uruchomić OCR na obrazie** oraz radzić sobie z najczęstszymi pułapkami, które napotykają początkujący.

Gotowy na kolejne wyzwanie? Spróbuj podać silnikowi stronę PDF przekonwertowaną na obraz lub poeksperymentuj z innym pakietem językowym, aby zobaczyć, jak zmieniają się wyniki pewności. Możesz

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}