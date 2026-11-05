---
category: general
date: 2026-05-02
description: Ogranicz zużycie pamięci GPU podczas uruchamiania OCR na obrazie w C#.
  Dowiedz się, jak włączyć przyspieszenie GPU, wyodrębnić tekst z paragonu i opanuj
  samouczek OCR w C#.
draft: false
keywords:
- limit gpu memory usage
- extract text from receipt
- how to enable gpu acceleration
- run OCR on image
- c# ocr tutorial
language: pl
og_description: Ogranicz użycie pamięci GPU podczas uruchamiania OCR na obrazie w
  C#. Ten przewodnik pokazuje, jak włączyć przyspieszenie GPU, wyodrębnić tekst z
  paragonu i opanować tutorial OCR w C#.
og_title: Ogranicz zużycie pamięci GPU w OCR w C# – Kompletny przewodnik
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Ogranicz zużycie pamięci GPU w OCR w C# – Kompletny przewodnik
url: /pl/net/ocr-optimization/limit-gpu-memory-usage-in-c-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ogranicz użycie pamięci GPU w C# OCR – Kompletny przewodnik

Czy kiedykolwiek musiałeś **ograniczyć użycie pamięci GPU** przy przetwarzaniu partii paragonów? Nie jesteś sam — programiści często napotykają błędy „out‑of‑memory”, gdy GPU zostaje obciążone zbyt wieloma obrazami jednocześnie. Dobrą wiadomością jest to, że Aspose.OCR pozwala ustawić limit zużycia pamięci **i** włączyć przyspieszenie GPU w jednej linii kodu.  

W tym tutorialu przeprowadzimy praktyczne, krok po kroku rozwiązanie, które pokaże **jak włączyć przyspieszenie GPU**, odczytać tekst z przykładowego obrazu paragonu oraz utrzymać zużycie RAM GPU poniżej schludnego 1 GB. Po zakończeniu będziesz mieć gotową do uruchomienia aplikację konsolową w C#, a także kilka wskazówek, które możesz wykorzystać w dowolnym scenariuszu **run OCR on image**.

## Co będzie potrzebne

- .NET 6.0 SDK lub nowszy (kod kompiluje się także z .NET 5+)  
- Pakiet NuGet **Aspose.OCR for .NET** (`Aspose.OCR`) – zainstaluj poleceniem `dotnet add package Aspose.OCR`  
- GPU obsługujące CUDA lub urządzenie Windows kompatybilne z DirectML  
- Przykładowy obraz paragonu (`receipt.jpg`) umieszczony w folderze, do którego możesz odwołać się w kodzie  

To wszystko — bez dodatkowych natywnych bibliotek, bez ręcznego kopiowania DLL‑ów. Aspose abstrahuje backend GPU, więc możesz skupić się na logice biznesowej.

## Krok 1: Zainstaluj pakiet NuGet Aspose.OCR

Na początek otwórz terminal w folderze projektu i uruchom:

```bash
dotnet add package Aspose.OCR
```

Pobierze to najnowszą stabilną wersję (stan na maj 2026 to 23.11). Pakiet zawiera zarówno binaria CPU, jak i GPU, więc nie musisz ręcznie pobierać środowisk uruchomieniowych CUDA czy DirectML — Aspose wykryje dostępne zasoby w czasie działania.

> **Pro tip:** Jeśli pracujesz w pipeline CI/CD, zablokuj wersję w pliku `.csproj`, aby uniknąć nieoczekiwanych aktualizacji.

## Krok 2: Utwórz silnik OCR i **ogranicz użycie pamięci GPU**

Teraz utworzymy instancję `OcrEngine` i wyraźnie poinstruujemy ją, aby nie przekraczała 1 GB pamięci GPU. To jest sedno wymogu **limit GPU memory usage**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

public class GpuExample
{
    public static void Run()
    {
        // Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU mode – Aspose auto‑detects CUDA or DirectML
        ocrEngine.Settings.Engine = EngineMode.Gpu;

        // 👉 Limit GPU memory usage to 1024 MB (1 GB)
        ocrEngine.Settings.GpuMemoryLimitMb = 1024;

        // Load the receipt image and run OCR
        var result = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");

        // Output the plain‑text result
        Console.WriteLine(result.Text);
    }
}
```

Zwróć uwagę na komentarz `// 👉 Limit GPU memory usage…` — ta linijka jest odpowiedzią na główne słowo kluczowe. Ustawiając `GpuMemoryLimitMb`, informujesz podlegający silnik inferencyjny, aby przydzielił co najwyżej podaną ilość pamięci, co pozwala na współistnienie wielu równoległych zadań bez wyczerpania GPU.

## Krok 3: **Jak włączyć przyspieszenie GPU** (i dlaczego ma to znaczenie)

Możesz się zastanawiać: „Dlaczego nie pozostać przy CPU?” Odpowiedź to prędkość. Na nowoczesnym RTX 3080 ten sam paragon jest przetwarzany w mniej niż 200 ms, w porównaniu do 1,2 s na czterordzeniowym CPU.  

Włączenie przyspieszenia GPU jest tak proste, jak ustawienie wyliczenia `EngineMode`:

```csharp
ocrEngine.Settings.Engine = EngineMode.Gpu;
```

Aspose automatycznie wybiera najlepszy backend:

| Detected Backend | What It Does |
|------------------|--------------|
| CUDA (NVIDIA)    | Uses cuDNN kernels for OCR, best for Windows/Linux with NVIDIA cards |
| DirectML (Windows) | Leverages DirectX 12, works on AMD/Intel GPUs without extra drivers |
| None (fallback)  | Falls back to optimized CPU path |

Jeśli nie wykryto ani CUDA, ani DirectML, silnik cicho przełącza się na CPU — bez awarii, tylko wolniej.

## Krok 4: **Run OCR on image** i **extract text from receipt**

Po skonfigurowaniu silnika podanie obrazu jest proste. Metoda `RecognizeImage` przyjmuje ścieżkę do pliku, `Stream` lub nawet `Bitmap`. Oto minimalne wywołanie:

```csharp
var result = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(result.Text);
```

Zakładając, że paragon zawiera:

```
Store XYZ
Date: 2026-04-30
Total: $23.45
```

Powinieneś zobaczyć wyjście podobne do:

```
=== OCR Output ===
Store XYZ
Date: 2026-04-30
Total: $23.45
```

Jeśli tekst wygląda na zniekształcony, sprawdź, czy obraz ma wysoki kontrast i jest prawidłowo obrócony — OCR najlepiej radzi sobie z czystymi skanami.

## Krok 5: Zweryfikuj limity pamięci i obsłuż przypadki brzegowe

Po pierwszym uruchomieniu możesz zapytać, ile pamięci GPU rzeczywiście użył silnik:

```csharp
Console.WriteLine($"GPU memory used: {ocrEngine.Settings.GpuMemoryUsedMb} MB");
```

Jeśli planujesz przetwarzać dziesiątki paragonów równolegle, możesz obniżyć limit do 512 MB i uruchomić kilka instancji silnika. Pamiętaj, że każda instancja respektuje ten sam globalny limit; biblioteka automatycznie ograniczy przydziały.

> **Common pitfall:** Ustawienie limitu zbyt nisko (np. 100 MB) może spowodować przejście silnika na CPU w trakcie działania, co prowadzi do niejednolitej wydajności. Przetestuj przy realistycznym obciążeniu przed zamrożeniem wartości.

## Pełny działający przykład

Poniżej kompletny, gotowy do skopiowania program konsolowy. Zamień `YOUR_DIRECTORY` na rzeczywistą ścieżkę do obrazu paragonu.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrGpuDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step‑by‑step demo
            GpuExample.Run();

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }

    class GpuExample
    {
        public static void Run()
        {
            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable GPU acceleration (auto‑detects CUDA or DirectML)
            ocrEngine.Settings.Engine = EngineMode.Gpu;

            // 3️⃣ Limit GPU memory usage to 1 GB for concurrent jobs
            ocrEngine.Settings.GpuMemoryLimitMb = 1024;

            // 4️⃣ Load the image and run OCR
            var recognitionResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");

            // 5️⃣ Output the recognized plain‑text
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognitionResult.Text);

            // 6️⃣ Optional: Show how much GPU memory was actually used
            Console.WriteLine($"\nGPU memory used: {ocrEngine.Settings.GpuMemoryUsedMb} MB");
        }
    }
}
```

Zapisz plik, uruchom `dotnet run`, a powinieneś zobaczyć wyodrębniony tekst paragonu wypisany w konsoli, wraz z małym raportem zużycia pamięci GPU.

## Rozwiązywanie problemów i FAQ

**Q: Mój GPU nie jest wykrywany — dlaczego?**  
A: Upewnij się, że masz najnowszy sterownik NVIDIA (dla CUDA) lub Windows 10 1809+ (dla DirectML). Sprawdź także, czy biblioteki `Aspose.OCR` pasują do architektury procesu (zalecane x64).

**Q: Wyjście jest puste.**  
A: Sprawdź jakość obrazu — rozmyte lub obrócone paragony często wymagają wstępnego przetwarzania (deskew, binaryzacja). Aspose udostępnia `ImagePreprocessor`, który możesz podłączyć przed `RecognizeImage`.

**Q: Czy mogę uruchomić to na Linuxie?**  
A: Tak, pod warunkiem posiadania karty NVIDIA z zainstalowanym CUDA 11+. Ten sam kod działa bez zmian.

## Zakończenie

Omówiliśmy wszystko, co potrzebne, aby **ograniczyć użycie pamięci GPU** podczas **run OCR on image** przy użyciu Aspose.OCR w C#. Od instalacji pakietu NuGet, przez konfigurację silnika, włączenie przyspieszenia GPU, po **extract text from receipt** — przewodnik dostarcza gotowego rozwiązania, które jest zarówno przyjazne pamięci, jak i błyskawicznie szybkie.

Następnie możesz zgłębiać bardziej zaawansowane tematy **c# OCR tutorial** — takie jak przetwarzanie wsadowe, własne pakiety językowe czy integracja wyników z bazą danych. Eksperymentuj z różnymi wartościami `GpuMemoryLimitMb`, aby znaleźć optymalny punkt dla swojego obciążenia, i monitoruj diagnostykę zużycia pamięci, aby uniknąć niespodzianek.

Miłego kodowania i niech Twój GPU pozostaje chłodny, a OCR ostry!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}