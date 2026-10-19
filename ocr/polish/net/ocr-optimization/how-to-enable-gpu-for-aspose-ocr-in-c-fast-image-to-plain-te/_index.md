---
category: general
date: 2026-02-24
description: Jak włączyć GPU w przykładzie Aspose OCR w C# – szybka konwersja obrazu
  na zwykły tekst. Zawiera ustawienie identyfikatora urządzenia GPU oraz przewodnik
  C# dotyczący odczytu tekstu z obrazu.
draft: false
keywords:
- how to enable gpu
- image to plain text
- aspose ocr example
- set gpu device id
- read image text c#
language: pl
og_description: Jak włączyć GPU w przykładzie Aspose OCR w C#. Dowiedz się, jak ustawić
  identyfikator urządzenia GPU i efektywnie odczytywać tekst z obrazu w C#.
og_title: Jak włączyć GPU dla Aspose OCR w C# – szybkie przetwarzanie obrazu na tekst
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Jak włączyć GPU w Aspose OCR w C# – szybkie przetwarzanie obrazu na tekst
url: /pl/net/ocr-optimization/how-to-enable-gpu-for-aspose-ocr-in-c-fast-image-to-plain-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak włączyć GPU dla Aspose OCR w C# – szybkie przekształcanie obrazu w zwykły tekst

Zastanawiałeś się kiedyś **jak włączyć GPU** podczas używania Aspose OCR do przekształcenia obrazu w edytowalny tekst? Nie jesteś sam — wielu programistów napotyka na ograniczenia wydajności przy przetwarzaniu dużych faktur lub zeskanowanych umów. Dobra wiadomość? Przekształcenie obrazu w zwykły tekst może być błyskawiczne, gdy wykorzystasz swoją kartę graficzną.

W tym przewodniku przeprowadzimy Cię przez kompletny **przykład Aspose OCR**, który pokaże dokładnie, jak włączyć GPU, ustawić identyfikator urządzenia GPU oraz **odczytać tekst z obrazu w C#**. Po zakończeniu będziesz mieć działający program, który wyodrębnia tekst z dowolnego obsługiwanego obrazu w ułamku czasu potrzebnego przy podejściu wyłącznie CPU.

## Co będzie potrzebne

- .NET 6.0 lub nowszy (API działa z .NET Core i .NET Framework)
- Karta graficzna kompatybilna z CUDA z zainstalowanym najnowszym sterownikiem
- Licencja Aspose.OCR dla .NET (lub darmowa wersja próbna, która działa w fazie rozwoju)
- Visual Studio 2022 (lub dowolny edytor C#, którego preferujesz)

Nie są wymagane dodatkowe pakiety NuGet poza `Aspose.OCR` — wystarczy sama biblioteka.

---

## Krok 1 – Zainstaluj pakiet NuGet Aspose OCR

Na początek dodaj oficjalną bibliotekę Aspose OCR do swojego projektu. Otwórz konsolę Package Manager i uruchom:

```powershell
Install-Package Aspose.OCR
```

To pobiera `Aspose.OCR.dll` oraz wszystkie jego zależności. Jeśli wolisz interfejs graficzny, kliknij prawym przyciskiem na projekt → **Manage NuGet Packages** → wyszukaj *Aspose.OCR* i kliknij **Install**.  

*Pro tip:* Po instalacji sprawdź, czy folder `Aspose.OCR` pojawił się pod **Dependencies** w Solution Explorer.

---

## Krok 2 – Utwórz prostą szkieletową aplikację konsolową

Zbudujemy małą aplikację konsolową, która pokaże cały przepływ. Utwórz nowy projekt:

```bash
dotnet new console -n GpuOcrDemo
cd GpuOcrDemo
```

Zastąp wygenerowany plik `Program.cs` pełnym kodem pokazanym później. Ten szkielet zapewnia czysty punkt wejścia i pozwala skupić się na logice OCR.

---

## Krok 3 – Jak włączyć GPU i ustawić identyfikator urządzenia GPU

Teraz najważniejsza część: **jak włączyć GPU** w Aspose OCR. Biblioteka udostępnia obiekt `OcrSettings`, w którym możesz przełączyć `UseGpu` i opcjonalnie wybrać konkretną kartę CUDA za pomocą `GpuDeviceId`. Poniżej znajduje się dokładny fragment kodu, który wstawisz do swojego programu:

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration – this is the crucial “how to enable gpu” step
        ocrEngine.Settings = new OcrSettings()
        {
            UseGpu = true,          // Turn on GPU processing
            GpuDeviceId = 0         // Optional: select the first CUDA‑compatible device
        };

        // 3️⃣ Recognise text from an image (any supported format)
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/large_invoice.png");

        // 4️⃣ Output the plain‑text result to the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Dlaczego włączać GPU?

Włączenie GPU przenosi ciężkie obliczenia — przetwarzanie pikseli, segmentację znaków i wnioskowanie sieci neuronowych — na kartę graficzną. Na skromnym GTX 1650 możesz zauważyć **2‑3‑krotny przyrost wydajności** w porównaniu z trybem wyłącznie CPU, szczególnie przy dokumentach wysokiej rozdzielczości.

### Wybór identyfikatora urządzenia

Jeśli Twój komputer ma wiele GPU, `GpuDeviceId` pozwala wybrać konkretną kartę. `0` wybiera pierwsze urządzenie; `1` drugie, i tak dalej. Dostępne identyfikatory możesz sprawdzić za pomocą narzędzia NVIDIA `nvidia-smi` lub odpytywając klasę `GpuInfo` Aspose (nie pokazano tutaj ze względu na zwięzłość).

---

## Krok 4 – Pełny działający przykład (gotowy do kopiowania i wklejenia)

Poniżej znajduje się kompletny, gotowy do uruchomienia program. Wklej go do `Program.cs`, zamień ścieżkę do obrazu na rzeczywisty plik na dysku i naciśnij **F5**.

```csharp
// Program.cs – Complete Aspose OCR GPU example
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Validate the input argument (optional but handy)
            if (args.Length == 0)
            {
                Console.WriteLine("Usage: dotnet run <image_path>");
                return;
            }

            string imagePath = args[0];

            // Initialise the OCR engine
            var ocrEngine = new OcrEngine();

            // -------------------- How to Enable GPU --------------------
            // Turn on GPU acceleration and optionally pick a device
            ocrEngine.Settings = new OcrSettings()
            {
                UseGpu = true,          // Enables GPU processing
                GpuDeviceId = 0         // Selects the first CUDA‑compatible GPU
            };
            // ---------------------------------------------------------

            try
            {
                // Recognise the image – this is the “image to plain text” core
                var ocrResult = ocrEngine.RecognizeImage(imagePath);

                // Display the extracted text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Graceful error handling – helpful when the GPU is unavailable
                Console.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

### Oczekiwany wynik

Jeśli podany obraz zawiera wiersz *„Invoice #12345 – Total $1,250.00”*, konsola wyświetli:

```
=== Extracted Text ===
Invoice #12345 – Total $1,250.00
```

Wynik jest zwykłym tekstem, gotowym do dalszego przetwarzania (np. wstawienia do bazy danych lub parsera języka naturalnego).

---

## Krok 5 – Zweryfikuj wykorzystanie GPU (opcjonalnie)

Aby upewnić się, że GPU jest naprawdę wykorzystywane, otwórz narzędzie monitorujące GPU (np. **NVIDIA‑Smi** lub **GPU‑Z**) podczas działania programu. Powinieneś zobaczyć skok w użyciu obliczeniowym wybranego urządzenia. Jeśli widzisz tylko aktywność CPU, sprawdź ponownie:

- Sterownik GPU jest aktualny.
- Flaga `UseGpu` jest ustawiona na `true`.
- Format Twojego obrazu jest obsługiwany (PNG, JPEG, TIFF, itp.).

---

## Typowe problemy i jak ich uniknąć

| Problem | Dlaczego się pojawia | Szybka naprawa |
|-------|----------------|-----------|
| **GPU not detected** | Nieaktualny sterownik lub brak środowiska CUDA | Zainstaluj najnowszy sterownik NVIDIA oraz zestaw narzędzi CUDA |
| **`Aspose.OCR` throws “GPU not supported”** | Uruchomiono na GPU nieobsługującym CUDA (np. starszy AMD) | Ustaw `UseGpu = false` lub przełącz się na kompatybilne GPU |
| **Incorrect image path** | Ścieżka względna wskazuje niewłaściwy folder | Użyj ścieżki bezwzględnej lub przekaż ścieżkę jako argument wiersza poleceń |
| **License not applied** | Tryb ewaluacji może ograniczać użycie GPU | Zarejestruj licencję za pomocą `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Rozszerzenie przykładu: przetwarzanie wsadowe z GPU

Jeśli musisz przetworzyć dziesiątki faktur, otocz wywołanie rozpoznawania pętlą. Ponieważ GPU pozostaje rozgrzane, kolejne obrazy korzystają z **cachowania rozgrzewki**, co skraca o kolejne milisekundy każdy przebieg.

```csharp
string[] files = Directory.GetFiles(@"C:\Invoices\", "*.png");
foreach (var file in files)
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Trim()}");
}
```

Pamiętaj, aby używać tej samej instancji `OcrEngine` — tworzenie nowego silnika dla każdego pliku ponownie inicjalizowałoby kontekst GPU i drastycznie obniżyło wydajność.

---

## Podsumowanie

Masz teraz solidny, kompleksowy **przykład Aspose OCR**, który pokazuje **jak włączyć GPU**, jak **ustawić identyfikator urządzenia GPU** oraz jak **odczytać tekst z obrazu w C#**. Przełączając `UseGpu` i wskazując właściwe urządzenie, zamieniasz wolne zadanie OCR oparte na CPU w wydajny potok, który radzi sobie z dużymi fakturami, paragonami czy dowolnym zeskanowanym dokumentem.

Śmiało eksperymentuj: wypróbuj różne formaty obrazów, dostosuj `GpuDeviceId` w konfiguracjach z wieloma GPU lub połącz to z innymi bibliotekami Aspose do generowania PDF. Nie ma ograniczeń, gdy GPU jest w użyciu.

---

<img src="gpu-ocr.png" alt="jak włączyć GPU z Aspose OCR w C# – szybkie konwertowanie obrazu na zwykły tekst">

*Miłego kodowania! Jeśli napotkasz problemy, zostaw komentarz poniżej lub sprawdź oficjalne forum Aspose, aby uzyskać bardziej szczegółowe informacje.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}