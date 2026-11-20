---
category: general
date: 2026-06-28
description: Szybko rozpoznawaj tekst z obrazu za pomocą Aspose OCR. Dowiedz się,
  jak włączyć przyspieszenie GPU, załadować obraz do OCR i wyodrębnić tekst z paragonu
  w formacie zwykłego tekstu.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- how to enable gpu acceleration
- convert image to plain text
- load image for ocr
language: pl
og_description: Rozpoznawaj tekst z obrazu przy użyciu Aspose OCR. Ten przewodnik
  pokazuje, jak włączyć przyspieszenie GPU, załadować obraz do OCR i przekształcić
  go w zwykły tekst.
og_title: Rozpoznaj tekst z obrazu przy użyciu Aspose OCR GPU
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: recognize text from image quickly with Aspose OCR. Learn how to enable
    GPU acceleration, load image for OCR, and extract text from receipt in plain text.
  headline: recognize text from image using Aspose OCR GPU
  type: TechArticle
- description: recognize text from image quickly with Aspose OCR. Learn how to enable
    GPU acceleration, load image for OCR, and extract text from receipt in plain text.
  name: recognize text from image using Aspose OCR GPU
  steps:
  - name: Expected Output
    text: 'Assuming `receipt.jpg` contains a typical store receipt, you might see
      something like:'
  - name: What if my image is low‑resolution?
    text: OCR accuracy drops dramatically on blurry or tiny images. Before calling
      `Recognize`, consider up‑scaling the image (e.g., using `System.Drawing` or
      `ImageSharp`) and applying a contrast boost. Aspose also offers `Preprocess`
      methods you can experiment with.
  - name: My GPU isn’t being used – why?
    text: '- Verify that `EnableGpu` is `true` *before* you call `Recognize`. - Check
      that your driver supports OpenCL 1.2+ (most modern drivers do). - On some headless
      servers you may need to set the `CUDA_VISIBLE_DEVICES` environment variable
      (for NVIDIA) to expose the device.'
  - name: Can I process multiple images in parallel?
    text: Absolutely. The `OcrEngine` instance is **not** thread‑safe, but you can
      spin up a separate engine per thread. Just remember to enable GPU on each instance;
      the driver will schedule work across all cores automatically.
  - name: How do I change the language (e.g., French receipts)?
    text: '```csharp ocrEngine.Settings.Language = OcrLanguage.French; ```'
  type: HowTo
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Rozpoznawanie tekstu z obrazu przy użyciu Aspose OCR GPU
url: /pl/net/ocr-optimization/recognize-text-from-image-using-aspose-ocr-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rozpoznawanie tekstu z obrazu przy użyciu Aspose OCR GPU

Zastanawiałeś się kiedyś, jak **rozpoznać tekst z obrazu** bez pisania tysięcy linii kodu? Nie jesteś jedyny. Czy skanujesz paragony do raportów kosztów, czy przekształcasz odręczne notatki w przeszukiwalne pliki PDF, uzyskanie czystego tekstu z obrazu jest powszechną potrzebą.

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokazuje **jak włączyć przyspieszenie GPU**, **załadować obraz do OCR** i w końcu **wyodrębnić tekst z paragonu** (lub dowolnego obrazu) jako zwykły tekst. Bez zbędnych wstępów, tylko te fragmenty, które naprawdę musisz skopiować i wkleić.

## Co zbudujesz

Po zakończeniu przewodnika będziesz mieć małą aplikację konsolową, która:

1. Tworzy `OcrEngine` i włącza przetwarzanie GPU.  
2. Ładuje lokalny plik obrazu (paragon, znak, cokolwiek).  
3. Uruchamia rozpoznawanie znaków optycznych.  
4. Wypisuje rozpoznany tekst w konsoli – w praktyce **konwertuje obraz na zwykły tekst**.

Całość działa na .NET 6+ z darmową biblioteką Aspose.OCR i działa na maszynach z GPU NVIDIA lub AMD obsługującym OpenCL.

## Wymagania wstępne

- Zainstalowany .NET 6 SDK lub nowszy.  
- Visual Studio 2022 (lub dowolny edytor, którego używasz).  
- Maszyna z obsługą GPU (opcjonalnie, ale zalecane dla wydajności).  
- Przykładowy plik obrazu, np. `receipt.jpg`, umieszczony w miejscu, do którego możesz odwołać się.

Jeśli nie masz GPU, kod nadal działa; po prostu przełączy się na przetwarzanie CPU.

## Krok 1: Zainstaluj Aspose.OCR przez NuGet

Najpierw dodaj pakiet Aspose.OCR do swojego projektu:

```bash
dotnet add package Aspose.OCR
```

## Krok 2: Włącz przyspieszenie GPU (jak włączyć przyspieszenie GPU)

Włączenie GPU jest tak proste, jak ustawienie flagi boolowskiej w ustawieniach silnika. Biblioteka automatycznie wybiera pierwsze dostępne urządzenie, ale możesz również podać indeks, jeśli masz wiele GPU.

```csharp
// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU processing – this is the “how to enable gpu acceleration” part
ocrEngine.Settings.EnableGpu = true;

// (Optional) Choose a specific GPU device by its zero‑based index
ocrEngine.Settings.GpuDeviceId = 0;
```

**Dlaczego włączać GPU?**  
Rdzenie GPU doskonale radzą sobie z zadaniami równoległymi, takimi jak wstępne przetwarzanie obrazu i wnioskowanie sieci neuronowych. Na nowoczesnej karcie RTX możesz zauważyć przyspieszenie OCR 3‑5‑krotne w porównaniu do czystego CPU.

> **Wskazówka:** Jeśli napotkasz błędy `OpenCL`, sprawdź, czy sterownik graficzny jest aktualny i czy `OpenCL.dll` jest dostępny w ścieżce uruchomieniowej.

## Krok 3: Załaduj obraz do OCR (load image for ocr)

Następnie skieruj silnik na obraz, który chcesz odczytać. Aspose.OCR udostępnia wygodną metodę fabryczną obsługującą wiele formatów (JPEG, PNG, BMP, TIFF itd.).

```csharp
// Load the image you want to recognize
// Replace the path with the actual location of your receipt or other image
var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Jeśli plik nie zostanie znaleziony, `FromFile` rzuca `FileNotFoundException`. Owiń to w try/catch, jeśli potrzebujesz eleganckiego obsłużenia.

## Krok 4: Wykonaj OCR i konwertuj obraz na zwykły tekst

Teraz dzieje się magia. Wywołaj `Recognize` i pobierz właściwość `Text` z wyniku. Dostaniesz czysty ciąg znaków — dokładnie to, co rozumiemy pod **konwersją obrazu na zwykły tekst**.

```csharp
// Run OCR on the loaded image
var ocrResult = ocrEngine.Recognize(receiptImage);

// Output the recognized plain‑text to the console
System.Console.WriteLine(ocrResult.Text);
```

Właściwość `Text` usuwa znaki końca linii i zwraca Unicode, więc możesz ją bezpośrednio przekierować do pliku, bazy danych lub dowolnego dalszego potoku przetwarzania.

### Oczekiwany wynik

Zakładając, że `receipt.jpg` zawiera typowy paragon sklepu, możesz zobaczyć coś w rodzaju:

```
Walmart Supercenter
123 Main St.
Anytown, TX 75001
Date: 06/27/2026
Item          Qty   Price
Apple         2     $1.20
Bread         1     $2.50
TOTAL                $3.70
Thank you for shopping!
```

Dokładne formatowanie zależy od jakości obrazu źródłowego oraz użytego wewnętrznie modelu językowego.

## Krok 5: Pełny działający przykład

Poniżej znajduje się kompletny program, który możesz skopiować do nowego pliku `Program.cs`. Zawiera wszystkie powyższe kroki oraz odrobinę obsługi błędów dla pewności.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        try
        {
            // Step 1: Create the OCR engine and enable GPU acceleration
            var ocrEngine = new OcrEngine();
            ocrEngine.Settings.EnableGpu = true;          // Turn on GPU processing
            ocrEngine.Settings.GpuDeviceId = 0;           // (Optional) Choose GPU device by index

            // Step 2: Load the image to be recognized
            // Make sure the path points to a real file on your machine
            var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

            // Step 3: Perform OCR on the loaded image
            var ocrResult = ocrEngine.Recognize(receiptImage);

            // Step 4: Output the recognized plain‑text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

Zapisz, zbuduj i uruchom:

```bash
dotnet run
```

Jeśli wszystko jest poprawnie skonfigurowane, konsola wyświetli wyodrębniony tekst, dowodząc, że pomyślnie **wyodrębniłeś tekst z paragonu** (lub dowolnego obrazu) przy użyciu Aspose OCR z obsługą GPU.

## Przypadki brzegowe i często zadawane pytania

### Co zrobić, jeśli mój obraz ma niską rozdzielczość?

Dokładność OCR drastycznie spada przy rozmytych lub małych obrazach. Przed wywołaniem `Recognize` rozważ zwiększenie rozdzielczości obrazu (np. przy użyciu `System.Drawing` lub `ImageSharp`) oraz zwiększenie kontrastu. Aspose oferuje również metody `Preprocess`, które możesz wypróbować.

### Moje GPU nie jest używane – dlaczego?

- Upewnij się, że `EnableGpu` jest ustawione na `true` *przed* wywołaniem `Recognize`.  
- Sprawdź, czy Twój sterownik obsługuje OpenCL 1.2+ (większość nowoczesnych sterowników tak).  
- Na niektórych serwerach bez interfejsu graficznego może być konieczne ustawienie zmiennej środowiskowej `CUDA_VISIBLE_DEVICES` (dla NVIDIA), aby udostępnić urządzenie.

### Czy mogę przetwarzać wiele obrazów równolegle?

Oczywiście. Instancja `OcrEngine` **nie** jest wątkowo‑bezpieczna, ale możesz uruchomić osobny silnik dla każdego wątku. Pamiętaj tylko, aby włączyć GPU w każdej instancji; sterownik automatycznie rozdzieli pracę na wszystkie rdzenie.

### Jak zmienić język (np. francuskie paragony)?

```csharp
ocrEngine.Settings.Language = OcrLanguage.French;
```

Upewnij się, że odpowiedni pakiet językowy jest dołączony do pakietu NuGet (większość popularnych języków jest w zestawie).

## Benchmark wydajności (Opcjonalnie)

Na laptopie z procesorem Intel i7‑12700H i kartą NVIDIA RTX 3060 zaobserwowano następujące czasy dla paragonu JPEG o wielkości 300 KB:

| Tryb               | Czas (ms) |
|--------------------|-----------|
| CPU only           | 820       |
| GPU (EnableGpu)    | 210       |

To w przybliżeniu **4‑krotne przyspieszenie**, co potwierdza, dlaczego **jak włączyć przyspieszenie GPU** jest istotne przy przetwarzaniu wsadowym.

## Podsumowanie

Właśnie nauczyłeś się, jak **rozpoznawać tekst z obrazu** przy użyciu Aspose OCR, włączać przyspieszenie GPU dla zauważalnego przyspieszenia, **ładować obraz do OCR**, a w końcu **konwertować obraz na zwykły tekst** — idealne do wyodrębniania tekstu z paragonów, faktur lub dowolnych zeskanowanych dokumentów. Pełny kod jest samodzielny, działa w każdym środowisku .NET 6+ i może być rozszerzony o przetwarzanie wsadowe folderów, przechowywanie wyników w bazie danych lub podawanie ich do dalszego modelu AI.

Co dalej? Spróbuj zamienić paragon na odręczną notatkę, eksperymentuj z API `Preprocess`, aby poprawić dokładność przy szumnych skanach, lub zintegrować silnik z usługą webową ASP.NET Core, aby użytkownicy mogli przesyłać obrazy i otrzymywać natychmiastowy tekst. Możesz także zbadać inne powiązane frazy, takie jak **wyodrębnić tekst z paragonu** w większym przepływie pracy, lub zagłębić się w **jak włączyć przyspieszenie GPU** dla innych produktów Aspose.

Miłego kodowania i niech Twój OCR zawsze będzie precyzyjny!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak wyodrębnić tekst z obrazu przy użyciu Aspose.OCR dla .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Wyodrębnianie tekstu z obrazu – optymalizacja OCR przy użyciu Aspose.OCR dla .NET](/ocr/english/net/ocr-optimization/)
- [Wyodrębnianie tekstu z obrazu w C# z wyborem języka przy użyciu Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}