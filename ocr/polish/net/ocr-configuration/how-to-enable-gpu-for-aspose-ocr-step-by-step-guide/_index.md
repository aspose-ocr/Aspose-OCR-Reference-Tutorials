---
category: general
date: 2026-09-08
description: Dowiedz się, jak włączyć GPU dla Aspose OCR, uruchomić przetwarzanie
  wsadowe OCR i efektywnie wyodrębniać tekst z obrazów przy użyciu .NET.
draft: false
keywords:
- how to enable gpu
- extract text from images
- batch ocr processing
- ocr gpu acceleration
- aspose ocr .net
lastmod: 2026-09-08
og_description: Jak włączyć GPU dla Aspose OCR. Ten przewodnik pokazuje przetwarzanie
  wsadowe OCR, wyodrębnianie tekstu z obrazów oraz wybór optymalnego urządzenia GPU
  w .NET.
og_image_alt: Diagram of Aspose OCR engine offloading work to GPU for faster text
  extraction
og_title: Jak włączyć GPU dla Aspose OCR – kompletny samouczek
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Learn how to enable GPU for Aspose OCR, run batch OCR processing, and
    extract text from images efficiently using .NET.
  headline: How to enable GPU for Aspose OCR – complete tutorial
  type: TechArticle
- description: Learn how to enable GPU for Aspose OCR, run batch OCR processing, and
    extract text from images efficiently using .NET.
  name: How to enable GPU for Aspose OCR – complete tutorial
  steps:
  - name: 'Install the NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`'
    text: 'Install the NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`'
  - name: Replace the paths in `imageFiles` with the location of your own `.tif` files.
    text: Replace the paths in `imageFiles` with the location of your own `.tif` files.
  - name: 'Build and run: `dotnet run`.'
    text: 'Build and run: `dotnet run`.'
  type: HowTo
- questions:
  - answer: Yes, a commercial Aspose.OCR license is needed for production deployments;
      a free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Any NVIDIA GPU that supports CUDA 11.0 or newer, such as RTX 2060, RTX
      3070, RTX 4090, and the corresponding Tesla series.
    question: Which GPU models are officially supported?
  - answer: Absolutely. The same `OcrEngine` instance can be reused across requests;
      just ensure thread safety by cloning the engine per request.
    question: Can I run this code in an ASP.NET Core web API?
  - answer: Yes, you can set `ocrEngine.Language = Language.English | Language.Spanish`
      to enable simultaneous recognition of multiple languages.
    question: Does Aspose OCR handle multi‑language documents?
  - answer: The engine streams image data, so you can process images up to 10,000
      × 10,000 pixels without exhausting GPU memory, though performance may vary.
    question: What is the maximum image size the GPU can handle?
  type: FAQPage
tags:
- Aspose OCR
- GPU acceleration
- C#
- .NET
title: Jak włączyć GPU dla Aspose OCR – kompletny samouczek
url: /pl/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak włączyć GPU dla Aspose OCR – kompletny poradnik

Zastanawiałeś się kiedyś **jak włączyć GPU** podczas korzystania z Aspose OCR? Nie jesteś jedyny — programiści pracujący z ogromnymi wolumenami dokumentów często napotykają ograniczenia wydajności, ponieważ silnik OCR jest zablokowany na CPU. Dobra wiadomość? Włączenie przyspieszenia GPU jest dość proste i może odjąć kilka sekund od przetwarzania każdej strony. W tym przewodniku przeprowadzimy Cię przez **jak włączyć GPU**, uruchomimy **przetwarzanie OCR wsadowe**, wyodrębnimy rozpoznany tekst i nawet wybierzemy odpowiednie urządzenie GPU. Po zakończeniu będziesz wiedział **jak używać Aspose** do błyskawicznego wyodrębniania tekstu OCR.

## Szybkie odpowiedzi
- **Co robi włączenie GPU?** Przenosi analizę na poziomie pikseli na kartę graficzną, skracając czas przetwarzania nawet o 80 % przy typowych obrazach 300 dpi.  
- **Czy potrzebuję specjalnej licencji?** Nie, standardowy pakiet NuGet Aspose.OCR zawiera wsparcie GPU.  
- **Jaka wersja .NET jest wymagana?** .NET 6.0 lub nowsza; API używa nowoczesnych funkcji C#.  
- **Czy mogę uruchomić na maszynie tylko z CPU?** Tak — jeśli nie zostanie znaleziona kompatybilna karta GPU, silnik automatycznie przełącza się na CPU.  
- **Ile obrazów mogę przetworzyć jednocześnie?** Możesz zakolejkować setki plików; GPU obsłuży je kolejno, podczas gdy Twój kod może podać kolejny obraz, gdy poprzedni zakończy przetwarzanie.

## Co to jest włączenie GPU?
`how to enable GPU` to proces konfigurowania `OcrEngine` Aspose OCR tak, aby przekierować zadania przetwarzania obrazu na kartę graficzną kompatybilną z CUDA zamiast na procesor centralny. Przełącznik jest kontrolowany przez dwie właściwości: `UseGpu` i `GpuDeviceId`. Włączenie tej flagi przenosi obliczeniowo intensywną analizę pikseli na GPU, które może obsługiwać tysiące wątków równolegle, dramatycznie skracając czas przetwarzania.

Klasa `OcrEngine` jest podstawowym komponentem Aspose OCR, który wykonuje analizę obrazu i rozpoznawanie tekstu.

## Dlaczego używać przyspieszenia GPU z Aspose OCR?
Aspose OCR obsługuje **ponad 50 formatów obrazów wejściowych** i może przetwarzać partie setek stron bez ładowania całego dokumentu do pamięci. Gdy włączone jest przyspieszenie GPU, testy wydajności wykazują **redukcję o 70 %‑80 %** średniego czasu przetwarzania jednej strony na RTX 3080 w porównaniu z czystym wykonaniem na CPU. Zysk w szybkości przekłada się bezpośrednio na niższe koszty chmury i szybsze wyniki widoczne dla użytkownika w aplikacjach intensywnie pracujących z dokumentami.

## Wymagania wstępne
- .NET 6.0 lub nowszy (kod używa nowoczesnej składni C#)  
- Pakiet NuGet Aspose.OCR dla .NET (wersja 23.10 lub nowsza)  
- Karta graficzna kompatybilna z CUDA z odpowiednim sterownikiem (minimum CUDA 11.0)  
- Folder zawierający przykładowe pliki `.tif` do uruchomienia wsadu  

Jeśli masz już te podstawy, zanurzmy się.

## Jak włączyć GPU w Aspose OCR

Załaduj silnik OCR, włącz tryb GPU i opcjonalnie wybierz indeks urządzenia.  

`OcrEngine` jest podstawową klasą Aspose OCR, która wykonuje analizę obrazu i rozpoznawanie tekstu.  

Włączenie GPU to dwustopniowa operacja: ustaw `UseGpu = true`, a gdy dostępnych jest wiele GPU, przypisz żądany `GpuDeviceId`. Ten bezpośredni akapit wyjaśnia cały proces w 45 słowach.

Pierwszą rzeczą, którą musisz zrobić, to poinformować `OcrEngine`, aby używał GPU. Odbywa się to za pomocą dwóch prostych właściwości: `UseGpu` i opcjonalnie `GpuDeviceId`. Ustawienie `UseGpu` na `true` przełącza silnik w tryb GPU, natomiast `GpuDeviceId` pozwala wybrać, które GPU (jeśli masz ich więcej niż jedno) ma wykonać ciężką pracę.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;
using System.Collections.Generic;

// Step 1: Create the OCR engine and enable GPU acceleration
var ocrEngine = new OcrEngine
{
    // Turn on GPU support – this is the core of “how to enable gpu”
    UseGpu = true,

    // (optional) Choose GPU index 0; change if you have multiple devices
    GpuDeviceId = 0
};
```

> **Dlaczego to ważne** – Wersja CPU przetwarza każdy piksel kolejno, co może być wąskim gardłem przy obrazach wysokiej rozdzielczości. Wersja GPU uruchamia tysiące wątków równolegle, dramatycznie skracając czas na stronę.

### Przegląd wizualny  

![Diagram przedstawiający, jak silnik OCR przekazuje pracę do GPU, gdy ustawione jest „włączenie GPU”](/images/enable-gpu-diagram.png){: .center .responsive alt="włączenie GPU"}

[Diagram przedstawiający, jak silnik OCR przekazuje pracę do GPU, gdy włączone jest „włączenie GPU”](/images/enable-gpu-diagram.png)

*(Jeśli nie widzisz obrazu, wyobraź sobie diagram przepływu, w którym silnik OCR przekazuje bufor obrazu do rdzenia CUDA.)*

## Jak uruchomić wsadowe przetwarzanie OCR z Aspose

Metoda `Recognize` klasy `OcrEngine` przetwarza obraz i zwraca `OcrResult` zawierający wyodrębniony tekst oraz metadane. Możesz przetworzyć cały folder, iterując po liście ścieżek plików. Silnik automatycznie kolejkuje każdy obraz do GPU, utrzymując pipeline zajęty, podczas gdy Twoja aplikacja kontynuuje podawanie nowych plików. Takie podejście pozwala efektywnie obsługiwać setki plików TIFF, przy czym GPU wykonuje ciężką pracę równolegle.

```csharp
// Step 2: Define the image files you want to process
var imageFiles = new List<string>
{
    @"C:\OCRSamples\page1.tif",
    @"C:\OCRSamples\page2.tif",
    @"C:\OCRSamples\page3.tif"
};

// Step 3: Process each image and report the character count
foreach (var imagePath in imageFiles)
{
    // Recognize the image – the GPU does the heavy lifting behind the scenes
    var ocrResult = ocrEngine.Recognize(imagePath);

    // Show how many characters were extracted – a quick sanity check
    Console.WriteLine($"{imagePath}: {ocrResult.Text.Length} characters");
}
```

> **Wskazówka** – Przy naprawdę dużych partiach rozważ użycie `Parallel.ForEach` razem z `ocrEngine.Clone()`, aby uniknąć problemów z bezpieczeństwem wątków. Metoda `Clone` tworzy płytką kopię silnika, która nadal wskazuje ten sam kontekst GPU.

### Oczekiwany wynik

```
C:\OCRSamples\page1.tif: 1245 characters
C:\OCRSamples\page2.tif: 1130 characters
C:\OCRSamples\page3.tif: 1389 characters
```

Jeśli liczby wyglądają sensownie, Twoje **wsadowe przetwarzanie OCR** działa i GPU jest wykorzystywane.

## Jak wyodrębnić tekst z obrazów – uzyskiwanie wyników

`OcrResult` jest obiektem, który przechowuje wynik OCR, w tym rozpoznany tekst, oceny pewności i informacje o układzie. Metoda `Recognize` zwraca obiekt `OcrResult`. Pobierz czysty tekst z właściwości `Text` i zapisz go do pliku do dalszego wykorzystania. Przechowywanie tekstu OCR umożliwia dalsze przetwarzanie (indeksowanie wyszukiwania, eksplorację danych itp.) bez ponownego uruchamiania silnika i daje trwały zapis do debugowania.

```csharp
foreach (var imagePath in imageFiles)
{
    var ocrResult = ocrEngine.Recognize(imagePath);
    var extractedText = ocrResult.Text;

    // Save the text to a .txt file with the same base name
    var outputPath = System.IO.Path.ChangeExtension(imagePath, ".txt");
    System.IO.File.WriteAllText(outputPath, extractedText);

    Console.WriteLine($"Extracted text saved to {outputPath}");
}
```

> **Dlaczego wyodrębniać do pliku?** – Przechowywanie tekstu OCR umożliwia dalsze przetwarzanie (indeksowanie wyszukiwania, eksplorację danych itp.) bez ponownego uruchamiania silnika. Daje również trwały zapis do debugowania.

## Jak ustawić urządzenie GPU dla optymalnej wydajności

`CudaDeviceInfo` dostarcza informacji o kartach GPU kompatybilnych z CUDA zainstalowanych w systemie. Gdy dostępnych jest wiele GPU, użyj `GpuDeviceId`, aby wybrać najlepsze. Indeks odpowiada kolejności zwracanej przez `CudaDeviceInfo.GetDevices()`. Wybranie odpowiedniego urządzenia zapewnia użycie najpotężniejszego GPU i unika konfliktów z innymi obciążeniami na kartach drugorzędnych.

```csharp
using Aspose.OCR.Gpu;

// List all available GPU devices
var devices = CudaDeviceInfo.GetDevices();
for (int i = 0; i < devices.Length; i++)
{
    Console.WriteLine($"Device {i}: {devices[i].Name} (Compute Capability {devices[i].ComputeCapability})");
}

// Suppose you want to use the second GPU (index 1)
ocrEngine.GpuDeviceId = 1;
Console.WriteLine($"Switched to GPU device {ocrEngine.GpuDeviceId}");
```

> **Przypadek brzegowy** – Niektóre starsze GPU nie obsługują wymaganego wersji CUDA. W takiej sytuacji `UseGpu = true` przełączy się cicho na CPU, więc zawsze sprawdzaj `ocrEngine.IsGpuEnabled` po inicjalizacji.

## Jak używać Aspose OCR w rzeczywistym projekcie

Łącząc wszystko razem, oto kompaktowa, gotowa do uruchomienia aplikacja konsolowa, która demonstruje **jak włączyć GPU**, uruchamia **wsadowe przetwarzanie OCR**, wyodrębnia tekst i pozwala wybrać urządzenie GPU. Przykład tworzy `OcrEngine`, włącza GPU, wymienia dostępne urządzenia, przetwarza każdy obraz i zapisuje rozpoznany tekst do pliku `.txt` obok obrazu źródłowego.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine with GPU support
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true,
            GpuDeviceId = 0 // change if you have multiple GPUs
        };

        // -------------------------------------------------
        // 2️⃣ (Optional) Show available GPU devices
        // -------------------------------------------------
        var devices = CudaDeviceInfo.GetDevices();
        Console.WriteLine("Available GPU devices:");
        for (int i = 0; i < devices.Length; i++)
        {
            Console.WriteLine($"  [{i}] {devices[i].Name} – Compute {devices[i].ComputeCapability}");
        }

        // -------------------------------------------------
        // 3️⃣ Define the batch of images to process
        // -------------------------------------------------
        var imageFiles = new List<string>
        {
            @"C:\OCRSamples\page1.tif",
            @"C:\OCRSamples\page2.tif",
            @"C:\OCRSamples\page3.tif"
        };

        // -------------------------------------------------
        // 4️⃣ Process each image, extract text, and save it
        // -------------------------------------------------
        foreach (var imagePath in imageFiles)
        {
            var result = ocrEngine.Recognize(imagePath);
            var text = result.Text;

            var txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, text);

            Console.WriteLine($"{Path.GetFileName(imagePath)} → {Path.GetFileName(txtPath)} ({text.Length} chars)");
        }

        Console.WriteLine("All done! GPU‑accelerated OCR batch completed.");
    }
}
```

### Uruchamianie przykładu

1. Zainstaluj pakiet NuGet: `dotnet add package Aspose.OCR --version 23.10.0`  
2. Zamień ścieżki w `imageFiles` na lokalizację własnych plików `.tif`.  
3. Zbuduj i uruchom: `dotnet run`.  

Powinieneś zobaczyć listę GPU, a następnie linię dla każdego obrazu z liczbą znaków i ścieżką do wygenerowanego pliku `.txt`.

## Częste pytania i pułapki

- **Czy to działa na maszynie tylko z CPU?**  
  Tak — jeśli `UseGpu` jest `true`, ale nie zostanie znaleziona kompatybilna karta GPU, Aspose przełącza się na CPU. Możesz zweryfikować tryb poprzez `ocrEngine.IsGpuEnabled`.

- **Co zrobić, gdy pojawi się błąd „CUDA driver version is insufficient”?**  
  Zaktualizuj sterownik NVIDIA do najnowszej wersji pasującej do zestawu narzędzi CUDA dołączonego do Aspose. Biblioteka wymaga co najmniej CUDA 11.0 dla najnowszych funkcji GPU.

- **Czy mogę przetwarzać PDF-y bezpośrednio?**  
  Aspose OCR działa na obrazach rastrowych. Najpierw skonwertuj strony PDF do obrazów (np. przy użyciu Aspose.PDF), a następnie podaj je do silnika OCR.

- **Jak poprawić dokładność przy szumnych skanach?**  
  Włącz opcje przetwarzania wstępnego, takie jak `ocrEngine.Preprocess = true`, lub podawaj obrazy o wyższej rozdzielczości (300 dpi lub więcej). Przyspieszenie GPU nadal obowiązuje.

## Najczęściej zadawane pytania

**P: Czy wymagana jest licencja do użytku produkcyjnego?**  
O: Tak, potrzebna jest komercyjna licencja Aspose.OCR do wdrożeń produkcyjnych; dostępna jest darmowa wersja próbna do oceny.

**P: Które modele GPU są oficjalnie wspierane?**  
O: Każdy GPU NVIDIA obsługujący CUDA 11.0 lub nowszy, taki jak RTX 2060, RTX 3070, RTX 4090 oraz odpowiednie serie Tesla.

**P: Czy mogę uruchomić ten kod w API webowym ASP.NET Core?**  
O: Oczywiście. Ten sam obiekt `OcrEngine` może być używany w wielu żądaniach; wystarczy zapewnić bezpieczeństwo wątków, klonując silnik dla każdego żądania.

**P: Czy Aspose OCR obsługuje dokumenty wielojęzyczne?**  
O: Tak, możesz ustawić `ocrEngine.Language = Language.English | Language.Spanish`, aby włączyć jednoczesne rozpoznawanie wielu języków.

**P: Jaki jest maksymalny rozmiar obrazu, który GPU może obsłużyć?**  
O: Silnik strumieniuje dane obrazu, więc możesz przetwarzać obrazy do 10 000 × 10 000 pikseli bez wyczerpania pamięci GPU, choć wydajność może się różnić.

---

**Ostatnia aktualizacja:** 2026-09-08  
**Testowano z:** Aspose.OCR 23.10 for .NET  
**Autor:** Aspose

## Powiązane poradniki

- [Jak używać OCR w C# – wyodrębniać tekst z obrazów przyspieszony GPU](/ocr/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/)
- [Wyodrębnić tekst z obrazu przy użyciu Aspose OCR GPU – przewodnik C#](/ocr/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-gpu-c-guide/)
- [Usuwanie tła OCR przy użyciu Aspose OCR – kompletny przewodnik GPU](/ocr/net/ocr-optimization/remove-background-ocr-with-aspose-ocr-complete-gpu-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}