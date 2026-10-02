---
category: general
date: 2026-02-13
description: Dowiedz się, jak używać OCR w C#, aby wyodrębniać tekst z plików graficznych,
  włączać przetwarzanie na GPU i szybko konwertować skany na tekst.
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: pl
og_description: Jak używać OCR w C#? Ten przewodnik pokazuje, jak wyodrębnić tekst
  z plików graficznych, włączyć przetwarzanie GPU oraz konwertować skany na tekst.
og_title: Jak używać OCR w C# – wyodrębniaj tekst z obrazów przy użyciu GPU
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: Jak używać OCR w C# – wyodrębniaj tekst z obrazów przy użyciu GPU
url: /pl/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać OCR w C# – Wyodrębniaj tekst z obrazów przy użyciu GPU

Zastanawiałeś się kiedyś **jak używać OCR**, aby wyciągnąć tekst ze zeskanowanego dokumentu bez wysiłku? Nie jesteś jedyny — programiści ciągle pytają: „Jak mogę efektywnie wyodrębnić tekst z plików obrazów?” Dobrą wiadomością jest to, że z Aspose.OCR możesz zrobić dokładnie to, a nawet **włączyć przetwarzanie GPU**, co zapewnia zauważalny przyrost szybkości na obsługiwanym sprzęcie.

W tym samouczku przeprowadzimy Cię przez kompletny, end‑to‑end przykład, który pokaże Ci **jak używać OCR**, jak **wyodrębnić tekst z obrazu**, jak **przekształcić skan w tekst**, oraz co zrobić, gdy GPU nie jest dostępne. Po zakończeniu będziesz mieć gotową do uruchomienia aplikację konsolową C#, która wypisze rozpoznany tekst i poinformuje, czy GPU zostało faktycznie użyte.

## Czego będziesz potrzebować

- .NET 6 SDK lub nowszy (kod działa również z .NET Core)  
- Visual Studio 2022 lub dowolny edytor, którego preferujesz  
- Pakiet Aspose.OCR dla .NET (dostępny przez NuGet)  
- Plik obrazu wysokiej rozdzielczości (np. `highres_scan.tif`) do testów  

Nie wymaga skomplikowanej konfiguracji — wystarczy kilka poleceń NuGet i możesz zacząć.

## Krok 1: Zainstaluj Aspose.OCR i przygotuj projekt

Na początek. Musisz dodać bibliotekę OCR do swojego projektu. Otwórz terminal w folderze rozwiązania i uruchom:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

To tworzy nowy projekt konsolowy o nazwie **OcrDemo** i dodaje pakiet NuGet `Aspose.OCR`. Biblioteka zawiera klasę `OcrEngine`, której będziemy używać.

> **Pro tip:** Jeśli pracujesz na maszynie z dedykowanym GPU, upewnij się, że zainstalowano najnowszy sterownik graficzny; w przeciwnym razie biblioteka automatycznie przełączy się w tryb CPU.

## Krok 2: Napisz kompletny kod OCR

Teraz otwórz `Program.cs` i zamień jego zawartość na poniższą. Każda linia jest skomentowana, abyś mógł zobaczyć *dlaczego* robimy to, co robimy.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Dlaczego to działa

- **ProcessingMode = Gpu** informuje silnik, aby najpierw spróbował użyć GPU. Biblioteka ukrywa niskopoziomowe wywołania CUDA/OpenCL, więc nie musisz sam zarządzać kontekstami urządzenia.  
- **IsGpuEnabled** jest wartością boolowską, która potwierdza, czy ścieżka GPU zakończyła się sukcesem. Jeśli zobaczysz `false`, silnik automatycznie przełączy się na CPU — nie ma powodów do paniki.  
- **RecognizeImage** wykonuje całą ciężką pracę: ładuje obraz, uruchamia model OCR i zwraca wynik w postaci zwykłego tekstu. Nie ma potrzeby ręcznego wstępnego przetwarzania bitmapy, chyba że masz specjalne wymagania (np. prostowanie).

## Krok 3: Uruchom aplikację i zweryfikuj wynik

Skompiluj i uruchom:

```bash
dotnet run
```

Jeśli wszystko jest poprawnie skonfigurowane, zobaczysz coś podobnego do:

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

Jeśli GPU nie jest dostępne, pierwsza linia będzie brzmieć `GPU used: False`, ale wyodrębniony tekst nadal się pojawi — dzięki eleganckiemu przełączeniu na CPU.

> **Common question:** *Co jeśli mój obraz jest w formacie JPEG zamiast TIFF?*  
> Metoda `RecognizeImage` akceptuje każdy format obsługiwany przez `System.Drawing` w .NET (JPEG, PNG, BMP, itp.). Wystarczy zmienić rozszerzenie pliku w `imagePath`.

## Krok 4: Opcjonalnie – Dostosuj ustawienia dla lepszej dokładności

Aspose.OCR oferuje kilka ustawień, które możesz dostosować:

| Ustawienie | Co robi | Kiedy używać |
|------------|----------|---------------|
| `ocrEngine.Language` | Wymusza konkretny język (np. `OcrLanguage.English`) | Jeśli znasz język dokumentu |
| `ocrEngine.PageSegMode` | Kontroluje, jak silnik dzieli strony na bloki | Dla układów wielokolumnowych |
| `ocrEngine.DetectOrientation` | Automatycznie obraca tekst, który nie jest pionowy | Skanów, które mogą być do góry nogami |

Możesz ustawić te właściwości przed wywołaniem `RecognizeImage`. Na przykład:

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## Krok 5: Zwizualizuj przepływ (Obraz z tekstem alternatywnym)

Poniżej znajduje się prosty diagram ilustrujący **jak używać OCR** z opcjonalnym przyspieszeniem GPU. Nie jest wymagany do działania kodu, ale pomaga zobaczyć ogólny obraz.

![Diagram przedstawiający jak używać OCR z przetwarzaniem GPU](/images/ocr-gpu-flow.png)

*Alt text:* *Diagram przedstawiający jak używać OCR z przetwarzaniem GPU, podkreślający przejście na CPU w razie potrzeby.*

## Przypadki brzegowe i rozwiązywanie problemów

1. **Out‑of‑Memory on GPU** – Bardzo duże obrazy mogą przekroczyć pamięć GPU. W takim przypadku biblioteka automatycznie przełączy się na CPU. Możesz wstępnie skalować obraz, aby utrzymać niskie zużycie pamięci.  
2. **Unsupported Image Format** – Jeśli `RecognizeImage` zgłosi *NotSupportedException*, sprawdź rozszerzenie pliku i upewnij się, że obraz nie jest uszkodzony. Konwersja do PNG często rozwiązuje problem.  
3. **Low Confidence Scores** – Gdy wynik OCR zawiera wiele nieczytelnych znaków, rozważ wstępne przetwarzanie (binaryzację, usuwanie szumów) lub przejście na skan o wyższej rozdzielczości.  

## Podsumowanie: Co osiągnęliśmy

Omówiliśmy właśnie **jak używać OCR** w aplikacji konsolowej C#, zademonstrowaliśmy jak **wyodrębnić tekst z plików obrazu** oraz pokazaliśmy jak **włączyć przetwarzanie GPU** dla szybszych wyników. Teraz wiesz, jak **przekształcić skan w tekst**, sprawdzić, czy GPU zostało faktycznie użyte, oraz dostosować kilka ustawień dla scenariuszy brzegowych.

### Kolejne kroki

- Spróbuj wprowadzić wynik do **indeksu wyszukiwania** (np. Elasticsearch), aby Twoje zeskanowane PDF-y stały się przeszukiwalne.  
- Eksperymentuj z **przetwarzaniem wsadowym** — przeiteruj folder z obrazami i zapisz każdy wynik do pliku `.txt`.  
- Połącz OCR z **API tłumaczeń**, aby automatycznie tłumaczyć zeskanowane dokumenty w obcym języku.  

Masz więcej pytań? zostaw komentarz i powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}