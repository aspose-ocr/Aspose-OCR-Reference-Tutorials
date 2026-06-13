---
category: general
date: 2026-03-17
description: Wyodrębnij tekst z pliku PNG przy użyciu Aspose OCR w C#. Naucz się odczytywać
  tekst z obrazu, przetwarzać OCR paragonów i tworzyć silnik OCR z przyspieszeniem
  GPU.
draft: false
keywords:
- extract text from png
- read text from image
- ocr receipt image
- process receipt ocr
- create ocr engine
language: pl
og_description: Wyodrębnij tekst z pliku PNG przy użyciu Aspose OCR. Ten przewodnik
  pokazuje, jak odczytać tekst z obrazu, przetworzyć OCR paragonu i efektywnie stworzyć
  silnik OCR.
og_title: Wyodrębnij tekst z PNG – Odczytaj tekst z obrazu za pomocą OCR
tags:
- OCR
- CSharp
- Aspose
title: Wyodrębnij tekst z PNG – Odczytaj tekst z obrazu za pomocą OCR
url: /pl/net/text-recognition/extract-text-from-png-read-text-from-image-with-ocr/
---

produce final.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tekstu z PNG – Odczytywanie tekstu z obrazu przy użyciu OCR

Czy kiedykolwiek potrzebowałeś **wyodrębnić tekst z PNG**, ale nie byłeś pewien, która biblioteka da Ci niezawodne wyniki? Nie jesteś sam — programiści ciągle pytają: „Jak odczytać tekst z plików obrazów, takich jak paragony, bez pisania własnej sieci neuronowej?” Dobra wiadomość jest taka, że Aspose OCR wykonuje ciężką pracę za Ciebie, a dodatkowo możesz uruchomić GPU, aby przyspieszyć działanie.

W tym tutorialu przejdziemy przez wszystko, co potrzebne do **przetwarzania OCR paragonów**, od instalacji pakietu NuGet po stworzenie silnika OCR, który rozumie Twój plik PNG. Na koniec będziesz mieć samodzielną aplikację konsolową, która odczytuje obraz paragonu, wypisuje rozpoznany tekst i pokazuje, jak dostroić silnik do różnych scenariuszy. Bez zewnętrznej dokumentacji, tylko czysty kod i przejrzyste wyjaśnienia.

## Wymagania wstępne

- .NET 6.0 SDK (lub dowolna nowsza wersja .NET)  
- Visual Studio 2022 lub VS Code z rozszerzeniami C#  
- Obsługiwany GPU NVIDIA z najnowszym sterownikiem (opcjonalnie, ale zalecane dla trybu GPU)  
- Pakiet NuGet **Aspose.OCR** (`dotnet add package Aspose.OCR`)  

Jeśli nie masz GPU, możesz nadal uruchomić przykład w trybie CPU — po prostu pomiń linie konfiguracyjne GPU.

## Krok 1: Zainstaluj Aspose.OCR i skonfiguruj projekt

Najpierw utwórz nowy projekt konsolowy i dodaj bibliotekę Aspose OCR.

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Dlaczego to ważne: pakiet `Aspose.OCR` zawiera silnik OCR, ładowarki obrazów oraz opcjonalne wsparcie GPU. Dodanie go przez NuGet zapewnia najnowszą stabilną wersję (stan na marzec 2026 to 23.10).

## Krok 2: Importuj przestrzenie nazw i utwórz silnik OCR

Otwórz **Program.cs** i dodaj wymagane dyrektywy `using`. Następnie zainicjalizuj silnik.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Optional: Enable GPU acceleration if a compatible GPU is present
            // This dramatically speeds up processing of high‑resolution PNGs
            ocrEngine.Config.EngineMode = EngineMode.Gpu;   // <-- primary way to "process receipt ocr" fast
            ocrEngine.Config.GpuDeviceId = 0; // selects the first GPU in the system

            // The rest of the code follows...
```

**Wskazówka:** Jeśli napotkasz `System.DllNotFoundException` na maszynach bez GPU, po prostu zakomentuj dwie linie ustawiające `EngineMode` i `GpuDeviceId`. Silnik automatycznie przełączy się na CPU.

## Krok 3: Załaduj obraz PNG, z którego chcesz wyodrębnić tekst

Aspose OCR potrafi czytać obrazy bezpośrednio z ścieżki pliku, strumienia lub nawet tablicy bajtów. W tym demo załadujemy lokalny obraz paragonu.

```csharp
            // Step 3: Load the image (replace the path with your own PNG file)
            string imagePath = @"C:\Images\receipt.png";

            // Validate the file exists to avoid runtime surprises
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }

            // Load the image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Zauważ, że zabezpieczamy się przed brakiem pliku. W rzeczywistych aplikacjach prawdopodobnie wyświetlisz przyjazny komunikat UI zamiast po prostu kończyć działanie.

## Krok 4: Wykonaj rozpoznanie OCR

Rzeczywiste wyodrębnianie tekstu odbywa się jednym wywołaniem metody. Silnik zwraca obiekt `OcrResult`, który zawiera surowy ciąg znaków, wyniki pewności i informacje o układzie.

```csharp
            // Step 4: Run the OCR process
            OcrResult ocrResult = ocrEngine.Recognize();

            // Check if the engine succeeded
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }
```

Dlaczego sprawdzamy `ocrResult.Text`: czasami niskiej jakości PNG zwraca pusty ciąg, a lepiej poinformować użytkownika niż cicho nic nie wypisać.

## Krok 5: Wyświetl rozpoznany tekst

Na koniec wypisz wyodrębniony ciąg znaków na konsolę. Możesz go także zapisać do pliku, bazy danych lub przekazać do innej usługi.

```csharp
            // Step 5: Display the recognized text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Gdy uruchomisz program (`dotnet run`), powinieneś zobaczyć coś w stylu:

```
=== Extracted Text from PNG ===
Store: Coffee Corner
Date: 03/15/2026
Item      Qty   Price
Latte      2    $5.40
Muffin     1    $2.30
Total            $7.70
=== End of Output ===
```

To **kompletne rozwiązanie do wyodrębniania tekstu z plików PNG** przy użyciu Aspose OCR, a Ty właśnie nauczyłeś się **odczytywać tekst z obrazów**, które wyglądają jak paragony.

## Opcjonalnie: Dostosowywanie silnika OCR (zaawansowane)

Jeśli potrzebujesz wyższej dokładności dla konkretnych czcionek lub zaszumionego tła, rozważ zmianę następujących ustawień:

```csharp
// Enable language detection (default is English)
ocrEngine.Config.Language = Language.English;

// Turn on automatic image preprocessing (deskew, binarization)
ocrEngine.Config.EnableImagePreprocessing = true;

// Set a confidence threshold if you only want high‑certainty results
ocrEngine.Config.ConfidenceThreshold = 0.75f;
```

Te drobne korekty są szczególnie przydatne, gdy **przetwarzasz OCR paragonów** w zadaniach wsadowych, w których niektóre skany nie są idealne.

## Typowe pułapki i jak ich unikać

| Problem | Dlaczego się pojawia | Rozwiązanie |
|---------|----------------------|-------------|
| **Brak sterownika GPU** | Silnik próbuje załadować CUDA, ale nie może znaleźć DLL. | Zainstaluj najnowszy sterownik NVIDIA lub przełącz się na tryb CPU, usuwając linię `EngineMode.Gpu`. |
| **Niepoprawna ścieżka obrazu** | `ImageStream.FromFile` rzuca wyjątek, gdy plik nie istnieje. | Zawsze waliduj ścieżkę (patrz Krok 3) lub używaj `Path.Combine` dla bezpieczeństwa międzyplatformowego. |
| **Niska pewność przy rozmazanych paragony** | Silnik OCR nie potrafi odróżnić znaków. | Włącz `EnableImagePreprocessing` i opcjonalnie zwiększ DPI obrazu przed przekazaniem go do silnika. |
| **Wycieki pamięci w długotrwałych usługach** | Każdy `OcrEngine` trzyma niezarządzane zasoby. | Zniszcz silnik po użyciu: `using var ocrEngine = new OcrEngine();` |

## Pełny działający przykład (kopiuj‑wklej)

Poniżej znajduje się **cały program**, który możesz wkleić do `Program.cs`. Zawiera wszystkie opcjonalne ulepszenia, zakomentowane dla łatwej aktywacji.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            using var ocrEngine = new OcrEngine();

            // Enable GPU acceleration if you have a supported card
            ocrEngine.Config.EngineMode = EngineMode.Gpu;
            ocrEngine.Config.GpuDeviceId = 0;

            // Optional fine‑tuning (uncomment as needed)
            //ocrEngine.Config.Language = Language.English;
            //ocrEngine.Config.EnableImagePreprocessing = true;
            //ocrEngine.Config.ConfidenceThreshold = 0.75f;

            // Load PNG image
            string imagePath = @"C:\Images\receipt.png";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize();

            // Verify result
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }

            // Output the extracted text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Zapisz, uruchom `dotnet run` i zobacz zawartość paragonu wypisaną w konsoli.

![wyodrębnianie tekstu z przykładu png](receipt.png "wyodrębnianie tekstu z przykładu png")

*Powyższy obraz przedstawia przykładowy plik PNG paragonu, który kod może przetworzyć.*

## Podsumowanie

Omówiliśmy, jak **wyodrębnić tekst z plików PNG** przy użyciu Aspose OCR, pokazaliśmy, jak **odczytywać tekst z obrazów**, oraz przeprowadziliśmy kompletny **proces OCR paragonów**, w tym opcjonalne przyspieszenie GPU. Tworząc własny **silnik OCR**, zyskujesz pełną kontrolę nad konfiguracją, wydajnością i obsługą błędów.

## Co dalej?

- **Przetwarzanie wsadowe**: iteruj po katalogu z plikami PNG paragonów i zapisz każdy wynik do pliku CSV.  
- **Integracja z Azure Functions**: przekształć tę aplikację konsolową w endpoint serverless przyjmujący przesyłane obrazy.  
- **Wsparcie wielojęzyczne**: zamień `Language.English` na `Language.Spanish` lub dodaj własne słowniki.  
- **Post‑processing**: użyj wyrażeń regularnych, aby wyodrębnić pola takie jak kwota całkowita, data czy NIP z surowego ciągu OCR.

Eksperymentuj — OCR to niezwykle elastyczne narzędzie, gdy znasz właściwe pokrętła. Jeśli napotkasz problemy, zostaw komentarz poniżej lub zajrzyj do dokumentacji API Aspose OCR po bardziej szczegółowe informacje.

Miłego kodowania i przyjemności z zamieniania uciążliwych PNG‑paragonów w przeszukiwalny tekst!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}