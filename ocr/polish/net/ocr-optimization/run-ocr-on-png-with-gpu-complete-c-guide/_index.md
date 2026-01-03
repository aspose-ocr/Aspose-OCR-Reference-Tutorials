---
category: general
date: 2026-01-02
description: Szybko wykonuj OCR na plikach PNG przy użyciu Aspose OCR i wsparcia GPU.
  Dowiedz się, jak rozpoznawać tekst z obrazu, wyodrębniać tekst z obrazu i ustawiać
  limit pamięci GPU.
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: pl
og_description: Uruchom OCR na plikach PNG wydajnie, wykorzystując Aspose OCR i przyspieszenie
  GPU. Ten samouczek pokazuje, jak rozpoznawać tekst z obrazu, wyodrębniać tekst z
  obrazu i kontrolować zużycie pamięci GPU.
og_title: Uruchom OCR na PNG z GPU – Kompletny przewodnik C#
tags:
- OCR
- C#
- GPU
title: Uruchom OCR na PNG z GPU – Kompletny przewodnik C#
url: /pl/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uruchom OCR na PNG z GPU – Kompletny przewodnik C#

Kiedykolwiek potrzebowałeś **uruchomić OCR na PNG** i czułeś się zablokowany na granicy wydajności? Nie jesteś jedyny. W wielu rzeczywistych przepływach pracy pojedynczy wysokiej rozdzielczości PNG może spowolnić silnik OCR działający wyłącznie na CPU, zamieniając to, co powinno być szybkim odczytem, w minutowe oczekiwanie.  

Dobre wieści są takie, że Aspose OCR dostarcza rozszerzenia GPU, które pozwalają **rozpoznawać tekst z obrazu** w ułamku czasu. W tym samouczku przeprowadzimy praktyczny przykład, który pokaże dokładnie, jak **uruchomić OCR na PNG** przy użyciu C#, jak **wyodrębnić tekst z obrazu**, a nawet jak **ustawić limit pamięci GPU**, aby pozostać w granicach budżetu sprzętowego.  

Omówimy także „jak” i „dlaczego” każdego kroku, abyś wyszedł z solidnym modelem mentalnym — nie tylko fragmentem kodu do kopiowania i wklejania.

## Czego się nauczysz

- Wymagania wstępne do korzystania z wsparcia GPU w Aspose OCR.  
- Jak załadować PNG do `Bitmap` i przekazać go do silnika OCR.  
- Jak skonfigurować `GpuDevice` i `GpuMemoryLimitMb` dla optymalnej wydajności.  
- Jak **rozpoznawać tekst z obrazu** i uzyskać wynik w postaci czystego tekstu.  
- Wskazówki dotyczące obsługi typowych przypadków brzegowych, takich jak GPU z małą ilością pamięci lub wielostronicowe PNG.  

Po zakończeniu tego przewodnika będziesz w stanie **uruchomić OCR na PNG** z prędkością GPU i pewnie kontrolować zużycie pamięci przez zadania OCR.

![Diagram pokazujący uruchomienie OCR na PNG z przyspieszeniem GPU](run-ocr-on-png-diagram.png "przykład uruchomienia OCR na PNG")

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz:

1. .NET 6.0 lub nowszy (kod działa również z .NET Core i .NET Framework).  
2. Kartę NVIDIA GPU z obsługą CUDA (przykład wybiera indeks urządzenia 0).  
3. Pakiet NuGet Aspose.OCR oraz jego rozszerzenia GPU (`Aspose.OCR.Extensions`).  
4. Przykładowy PNG (`input.png`) umieszczony w folderze, do którego możesz odwołać się w swoim projekcie.  

Jeśli któreś z tych zagadnień jest Ci nieznane, nie martw się — podamy alternatywy tam, gdzie to istotne.

---

## Krok 1 – Zainstaluj Aspose OCR i rozszerzenia GPU

Najpierw najważniejsze. Bez odpowiednich bibliotek reszta kodu nie skompiluje się.

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

Pakiet `Aspose.OCR.Extensions` pobiera natywne pliki binarne CUDA niezbędne do przyspieszenia GPU.  
*Wskazówka:* Jeśli pracujesz na maszynie bez GPU, nadal możesz skompilować projekt; po prostu ustaw później `PreferGpu = false`.

---

## Krok 2 – Załaduj PNG, który chcesz przetworzyć

Teraz faktycznie **uruchamiamy OCR na PNG**, ładując go do `Bitmap`. Ten krok jest prosty, ale warto dodać krótką uwagę: `Bitmap` oczekuje ścieżki do pliku, więc upewnij się, że ścieżka jest poprawna względem Twojego pliku wykonywalnego.

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

Jeśli PNG jest wyjątkowo duży (np. > 5000 px po jednej stronie), możesz najpierw zmniejszyć jego skalę, aby uniknąć wyczerpania pamięci GPU. Wtedy przydatna będzie opcja **ustaw limit pamięci GPU**.

---

## Krok 3 – Utwórz i skonfiguruj silnik OCR do użycia GPU

Oto serce samouczka: konfigurowanie silnika OCR, aby **rozpoznawał tekst z obrazu** przy użyciu GPU. Dwie właściwości są kluczowe:

- `GpuDevice` – wybiera, które urządzenie CUDA użyć.  
- `GpuMemoryLimitMb` – ogranicza ilość pamięci GPU, którą silnik może przydzielić.

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**Dlaczego ustawiać limit pamięci?** Niektóre GPU współdzielą pamięć z wyświetlaczem lub uruchamiają jednocześnie wiele zadań. Ograniczając przydział, zapobiegasz awariom z powodu braku pamięci, szczególnie przy przetwarzaniu wielu PNG równocześnie.

---

## Krok 4 – Zdefiniuj opcje rozpoznawania (język i preferencja GPU)

Obiekt `RecognitionOptions` informuje silnik, jakiego języka szukać i czy **preferować GPU** nawet dla małych obrazów. Dla większości angielskich dokumentów jest to wystarczające, ale możesz zamienić `Language.English` na inne obsługiwane języki.

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

Jeśli kiedykolwiek będziesz musiał **wyodrębnić tekst z obrazu** w języku innym niż angielski, po prostu zmień enum `Language`. Biblioteka obsługuje dziesiątki języków od razu.

---

## Krok 5 – Uruchom OCR i pobierz wynik

Po podłączeniu wszystkiego, ostateczne wywołanie to pojedyncza linia, która faktycznie **uruchamia OCR na PNG** i zwraca bogaty obiekt wyniku.

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

`OcrResult` zawiera nie tylko czysty tekst (`ocrResult.Text`), ale także wyniki pewności, ramki ograniczające oraz nawet oryginalny obraz z podświetlonymi słowami — przydatne, jeśli musisz debugować lub wizualizować ekstrakcję.

**Oczekiwany wynik** (dla przykładowego PNG z napisem „Hello World”):

```
=== OCR Output ===
Hello World
```

Jeśli tekst jest zniekształcony, sprawdź dwukrotnie, czy PNG nie jest uszkodzony i czy limit pamięci GPU nie jest zbyt niski dla rozmiaru obrazu.

---

## Krok 6 – Obsługa przypadków brzegowych i najlepsze praktyki

### GPU z małą ilością pamięci

Jeśli pojawi się wyjątek taki jak `CudaException: out of memory`, obniż `GpuMemoryLimitMb` lub podziel PNG na kafelki przed przetwarzaniem. Kafelkowanie można wykonać przy użyciu `Graphics.DrawImage` na klonie `Bitmap`.

### Wiele PNG w partii

Podczas przetwarzania folderu PNG, używaj tego samego egzemplarza `OcrEngine` — jednorazowa inicjalizacja oszczędza przełączania kontekstu GPU.

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### Powrót do CPU

Jeśli GPU nie jest dostępne, po prostu ustaw `PreferGpu = false`. Silnik automatycznie przełączy się na CPU bez żadnych zmian w kodzie.

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## Pełny działający przykład

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do nowego projektu konsolowego. Zawiera wszystkie powyższe kroki oraz kilka dodatkowych sprawdzeń bezpieczeństwa.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Zapisz plik jako `Program.cs`, uruchom `dotnet run`, a powinieneś zobaczyć wyodrębniony tekst wypisany w konsoli.

---

## Zakończenie

Właśnie pokazaliśmy, jak **uruchomić OCR na PNG** przy użyciu rozszerzeń GPU Aspose OCR, jak **rozpoznawać tekst z obrazu** oraz jak **wyodrębnić tekst z obrazu**, kontrolując jednocześnie **ustawienie limitu pamięci GPU**. Konfigurując `GpuDevice` i `GpuMemoryLimitMb`, utrzymujesz aplikację szybką i stabilną, nawet na skromnych GPU.

Od tego momentu możesz:

- Eksperymentować z innymi językami (`Language.French`, `Language.Spanish`).  
- Zintegrować krok OCR z większym potokiem przetwarzania dokumentów.  
- Dodać przetwarzanie końcowe, takie jak sprawdzanie pisowni lub ekstrakcja encji, aby dopracować surowy tekst.  

Pamiętaj, kluczem nie jest tylko kod, ale zrozumienie, dlaczego każde ustawienie ma znaczenie. Gdy wiesz, jak **ustawić limit pamięci GPU** i kiedy przejść na CPU, tworzysz rozwiązania OCR, które skalują się płynnie.  

Masz pytania dotyczące konkretnego rozmiaru PNG, wielostronicowych TIFF‑ów lub rozwiązywania problemów z GPU? Dodaj komentarz poniżej i powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}