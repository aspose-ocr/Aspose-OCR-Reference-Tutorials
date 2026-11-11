---
category: general
date: 2026-09-13
description: Jak wykonywać wsadowe OCR przy użyciu Aspose OCR GPU w C# i .NET. Dowiedz
  się, jak rozpoznawać tekst na obrazach, wyodrębniać tekst z plików TIFF oraz przyspieszyć
  przetwarzanie dzięki wsparciu GPU.
draft: false
keywords:
- aspose ocr gpu
- process multiple images
- how to batch ocr
- install aspose ocr
lastmod: 2026-09-13
og_description: Jak wykonywać wsadowe OCR przy użyciu Aspose OCR GPU w C# i .NET.
  Ten przewodnik pokazuje, jak rozpoznawać tekst na obrazach, wyodrębniać tekst z
  plików TIFF oraz wykorzystać przyspieszenie GPU do wysokowydajnego przetwarzania.
og_image_alt: Screenshot of Aspose OCR GPU batch processing console output in C#
og_title: Jak wykonywać wsadowe OCR przy użyciu Aspose OCR GPU w C# i .NET
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: How to batch OCR with Aspose OCR GPU in C# using .NET. Learn to recognize
    text from images, extract text from TIFF files, and accelerate processing with
    GPU support.
  headline: How to batch OCR with Aspose OCR GPU in C# using .NET
  type: TechArticle
- questions:
  - answer: Yes, as long as the server has a CUDA‑compatible GPU and the appropriate
      driver libraries installed; no display is required.
    question: Can I run the GPU version on a headless Linux server?
  - answer: Absolutely. The engine treats each page as a separate image and returns
      concatenated text, preserving page order.
    question: Does Aspose OCR support multi‑page TIFF files out of the box?
  - answer: Benchmarks show Aspose OCR achieves ≥ 96 % character accuracy on clean
      printed documents and ≥ 90 % on low‑contrast scans, matching leading SaaS providers
      while keeping data on‑premises.
    question: How accurate is the OCR output compared with cloud services?
  - answer: The library imposes no hard limit; practical limits are driven by available
      disk space and GPU memory. Processing 10 000 pages on an RTX 3080 typically
      stays under 2 GB of GPU memory.
    question: Is there a limit to the number of files I can process in one run?
  - answer: Yes, set `ocrEngine.Language = OcrLanguage.Spanish` (or any supported
      language) before calling `Recognize`. The engine supports 30+ languages, including
      Arabic, Chinese, and Hindi.
    question: Can I customize the language model for non‑English scripts?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- GPU
title: Jak wykonywać wsadowe OCR przy użyciu Aspose OCR GPU w C# i .NET
url: /pl/net/ocr-optimization/how-to-batch-ocr-in-c-with-aspose-ocr-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonywać wsadowe OCR przy użyciu Aspose OCR GPU w C# w .NET

Jeśli potrzebujesz **wsadowego OCR** setek zeskanowanych stron szybko, silnik Aspose OCR GPU zapewnia szybki, niezawodny sposób rozpoznawania tekstu z obrazów i plików TIFF w jednym przebiegu. W tym przewodniku zobaczysz, jak skonfigurować projekt .NET, włączyć przyspieszenie GPU i przetworzyć cały folder obrazów bez pisania żadnego kodu szablonowego.

## Szybkie odpowiedzi
- **Co oznacza „wsadowe OCR”?** To automatyczne przetwarzanie wielu plików graficznych w jednej operacji, zwracające wyodrębniony tekst dla każdego pliku.  
- **Czy mogę używać wersji GPU na dowolnym komputerze?** Tak, pod warunkiem że system ma kompatybilną z CUDA kartę graficzną i odpowiedni sterownik.  
- **Czy potrzebna jest licencja do rozwoju?** Licencja trial działa w trybie testowym; licencja komercyjna jest wymagana w produkcji.  
- **Jakie wersje .NET są wspierane?** .NET 6.0 i nowsze są w pełni wspierane; .NET 5 także działa przy drobnych modyfikacjach.  
- **Czy silnik jest wątkowo‑bezpieczny przy równoległych uruchomieniach?** Silnik CPU jest wątkowo‑bezpieczny; silnik GPU wymaga jednej instancji na wątek lub kontrolowanej strategii równoległości.

## Co to jest Aspose OCR GPU?
Silnik `Aspose.OCR` GPU to wysokowydajna biblioteka OCR, która przenosi pracę analizy obrazu na kartę graficzną z obsługą CUDA, zapewniając do 4× szybszy przepustowość w porównaniu z czystym przetwarzaniem CPU. Obsługuje szeroką gamę formatów obrazów, dostarcza wbudowane modele językowe i może być zintegrowany z dowolną aplikacją .NET przy minimalnych zmianach kodu.

## Dlaczego warto używać Aspose OCR GPU do przetwarzania wsadowego?
Aspose OCR obsługuje **ponad 30 formatów obrazów** (w tym PNG, JPEG, BMP i wielostronicowy TIFF) i może obsługiwać pliki do **2 GB** każdy bez ładowania całego dokumentu do pamięci. Po włączeniu przyspieszenia GPU typowe strony TIFF 300 dpi są przetwarzane w mniej niż 0,2 sekundy na stronę na nowoczesnej karcie RTX 3080.

## Wymagania wstępne
- .NET 6.0 SDK (lub nowszy) zainstalowany na maszynie deweloperskiej.  
- Pakiet NuGet Aspose.OCR dla .NET – wybierz pakiet `Aspose.OCR.Gpu`, jeśli masz kompatybilny GPU, w przeciwnym razie zainstaluj `Aspose.OCR`.  
- Folder zawierający obrazy do przetworzenia (TIFF, PNG, JPEG itp.).  
- Visual Studio 2022, Rider lub dowolny edytor umożliwiający budowanie aplikacji konsolowych .NET.

> **Pro tip:** Zweryfikuj, że masz zainstalowane CUDA 11+ i że `nvidia-smi` raportuje Twoją kartę jako „compatible”. Biblioteka automatycznie przełączy się na CPU, jeśli nie znajdzie odpowiedniego GPU.

## Jak skonfigurować projekt i zainstalować Aspose OCR
Utwórz nową aplikację konsolową .NET, dodaj pakiet NuGet Aspose OCR i przywróć zależności. To przygotowuje lekki projekt, który można skompilować i uruchomić na dowolnej platformie obsługującej .NET 6 lub nowszy. Po zainstalowaniu pakietu możesz odwoływać się do klas OCR bezpośrednio w kodzie, umożliwiając wsadowe przetwarzanie bez dodatkowej konfiguracji.

```bash
dotnet new console -n GpuBatchDemo
cd GpuBatchDemo
dotnet add package Aspose.OCR --version 23.12
```

Jeśli posiadasz licencję z obsługą GPU, zainstaluj zamiast tego pakiet specyficzny dla GPU. Ta wersja zawiera natywne powiązania CUDA, które pozwalają silnikowi działać na karcie graficznej, dostarczając opisany wcześniej przyrost wydajności.

```bash
dotnet add package Aspose.OCR.GPU --version 23.12
```

Twój projekt teraz odwołuje się do biblioteki OCR wymagalnej do **wsadowego OCR**.

## Jak zainicjować silnik OCR (CPU lub GPU)
Klasa `OcrEngine` jest głównym punktem wejścia do wykonywania operacji OCR. Abstrahuje ona podległy sprzęt i udostępnia prosty interfejs API zarówno dla wykonania na CPU, jak i GPU. Załaduj silnik OCR i określ, czy ma używać GPU:

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class GpuBatchDemo
{
    static void Main()
    {
        // Create the OCR engine. It works with both CPU and GPU builds.
        var ocrEngine = new OcrEngine();

        // OPTIONAL: Force GPU usage if a compatible device is present.
        // Setting this to true won’t break on CPU‑only machines—it simply tries GPU first.
        ocrEngine.Settings.UseGpu = true;
```

**Dlaczego to ważne:** Ustawienie `UseGpu` pozwala Aspose wybrać najszybszą ścieżkę wykonania. Gdy dostępna jest kompatybilna karta, silnik działa na GPU; w przeciwnym razie przełącza się na CPU bez rzucania błędem, zapewniając, że Twoje zadanie wsadowe nie zawiedzie z powodu brakującego sprzętu.

## Jak zebrać pliki do przetworzenia
Zbieranie docelowych obrazów to pierwszy krok w każdym przepływie wsadowym. Zbuduj listę ścieżek plików pasujących do obsługiwanych rozszerzeń, a następnie przekaż tę listę do pętli OCR. Takie podejście utrzymuje kod prostym i ułatwia późniejsze filtrowanie.

```csharp
        // Prepare a list of image files (TIFF, PNG, JPEG, etc.).
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // You could also populate the list dynamically:
        // var imageFiles = Directory.GetFiles(@"C:\OCR\Input", "*.tif").ToList();
```

**Uwaga o przypadkach brzegowych:** Jeśli Twój folder zawiera mieszane formaty, zamień wzorzec wyszukiwania na `"*.*"` i filtruj po rozszerzeniu wewnątrz pętli. Dzięki temu wsad pozostaje elastyczny i nie pomija plików.

## Jak przetworzyć każdy obraz i wyświetlić podgląd
Dla każdego pliku wywołaj silnik OCR, pobierz rozpoznany tekst i wyświetl krótki fragment w konsoli. Pokazywanie podglądu pomaga zweryfikować, że wsad działa poprawnie, bez otwierania każdego pliku wyjściowego.

```csharp
        // Loop through each file, run OCR, and print a short preview.
        foreach (var filePath in imageFiles)
        {
            // Load the image into Aspose's OcrImage object.
            var ocrImage = OcrImage.FromFile(filePath);

            // Run recognition.
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Display the first 50 characters of the recognized text.
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");
        }
    }
}
```

**Co zobaczysz:** Dla każdego obrazu konsola wypisze pierwsze 100 znaków rozpoznanego tekstu, potwierdzając, że wsad zakończył się sukcesem bez ręcznego otwierania plików.

## Jak zapisać wyniki OCR (opcjonalnie, ale przydatne)
Zachowanie pełnego wyniku OCR umożliwia dalsze indeksowanie, analizę AI lub konwersję do przeszukiwalnych PDF‑ów. Zapisz tekst do pliku `.txt` leżącego obok źródłowego obrazu, używając tej samej nazwy bazowej dla łatwej korelacji.

```csharp
            // Define an output path based on the source file name.
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
```

Teraz każdy obraz ma towarzyszący plik tekstowy zawierający kompletny wynik OCR, gotowy dla wyszukiwarek, modeli językowych lub własnych potoków analitycznych.

## Jak uruchomić demonstrację i zweryfikować wynik
Zbuduj i uruchom aplikację konsolową, aby zobaczyć wsadowy proces w akcji. Krok budowania kompiluje kod, a krok uruchomienia przetwarza każdy obraz w docelowym folderze i wypisuje linie podglądu w konsoli. Jeśli włączyłeś opcjonalny krok zapisu, znajdziesz również plik `.txt` dla każdego obrazu źródłowego.

1. Zbuduj projekt: `dotnet build`.  
2. Uruchom program: `dotnet run --project GpuBatchDemo.csproj`.

Powinieneś zobaczyć linie podglądu w konsoli oraz, jeśli dodałeś opcjonalny krok, serię plików `.txt` obok swoich obrazów źródłowych.

## Typowe pułapki i jak je naprawić
| Objaw | Prawdopodobna przyczyna | Rozwiązanie |
|---------|--------------|-----|
| **Pusty `ocrResult.Text`** | Obraz zbyt ciemny lub niska rozdzielczość DPI | Wstępnie przetwórz obrazy (zwiększ kontrast, podnieś rozdzielczość) lub włącz `ocrEngine.Settings.PreprocessImage = true`. |
| **Błąd GPU „CUDA driver version is insufficient”** | Przestarzały sterownik | Zaktualizuj sterownik GPU lub ustaw `UseGpu = false`, aby wymusić przetwarzanie na CPU. |
| **Wyjątek „File not found”** | Nieprawidłowy separator ścieżki w systemie Linux/macOS | Użyj `Path.Combine` lub ukośników (`/`). |

## Jak skalować poza kilka plików
Gdy przechodzisz od dziesiątek do tysięcy obrazów, rozważ następujące strategie: używaj przetwarzania równoległego z oddzielnymi instancjami silnika na wątek, ładuj obrazy w zarządzalnych partiach i loguj postęp do pliku dla łatwej odnowy. Te techniki utrzymują niskie zużycie pamięci i wysoką przepustowość.

```csharp
Parallel.ForEach(imageFiles, filePath =>
{
    // Same OCR logic as before, but each thread gets its own engine.
    var engine = new OcrEngine { Settings = { UseGpu = true } };
    // ... rest of the code
});
```

> **Pamiętaj:** Pamięć GPU jest współdzielona w całym procesie. Uruchamianie zbyt wielu równoległych zadań GPU może wyczerpać pamięć i faktycznie spowolnić wsad. Zacznij od 2‑4 wątków i monitoruj wykorzystanie GPU.

## Najczęściej zadawane pytania

**Q: Czy mogę uruchomić wersję GPU na bezgłowym serwerze Linux?**  
A: Tak, pod warunkiem że serwer ma kompatybilną z CUDA kartę graficzną i zainstalowane odpowiednie biblioteki sterownika; wyświetlacz nie jest wymagany.

**Q: Czy Aspose OCR obsługuje wielostronicowe pliki TIFF od razu?**  
A: Absolutnie. Silnik traktuje każdą stronę jako osobny obraz i zwraca połączony tekst, zachowując kolejność stron.

**Q: Jak dokładny jest wynik OCR w porównaniu z usługami chmurowymi?**  
A: Testy wykazują, że Aspose OCR osiąga ≥ 96 % dokładności znaków w czystych dokumentach drukowanych i ≥ 90 % przy skanach o niskim kontraście, dorównując czołowym dostawcom SaaS przy zachowaniu danych on‑premises.

**Q: Czy istnieje limit liczby plików, które mogę przetworzyć w jednym uruchomieniu?**  
A: Biblioteka nie narzuca sztywnego limitu; praktyczne ograniczenia zależą od dostępnego miejsca na dysku i pamięci GPU. Przetworzenie 10 000 stron na RTX 3080 zazwyczaj nie przekracza 2 GB pamięci GPU.

**Q: Czy mogę dostosować model językowy dla skryptów nie‑angielskich?**  
A: Tak, ustaw `ocrEngine.Language = OcrLanguage.Spanish` (lub dowolny obsługiwany język) przed wywołaniem `Recognize`. Silnik wspiera ponad 30 języków, w tym arabski, chiński i hindi.

## Podsumowanie
Masz teraz kompletną, end‑to‑end rozwiązanie dla **wsadowego OCR z Aspose OCR GPU w C#**. Tutorial obejmował konfigurację projektu, aktywację GPU, enumerację plików, przetwarzanie pojedynczych obrazów, opcjonalne zapisywanie wyników oraz techniki skalowania dla dużych obciążeń. Dzięki tej bazie możesz przekazywać wyniki OCR do indeksów wyszukiwania, modeli językowych lub budować własne potoki przetwarzania dokumentów.

Gotowy na kolejny krok? Spróbuj połączyć tekst OCR z Aspose .PDF, aby generować przeszukiwalne PDF‑y, lub zintegrować wynik z Azure Cognitive Search, aby uzyskać natychmiastowe pełnotekstowe wyszukiwanie wśród tysięcy zeskanowanych dokumentów.

---

**Ostatnia aktualizacja:** 2026-09-13  
**Testowano z:** Aspose.OCR 24.5 dla .NET (pakiety CPU & GPU)  
**Autor:** Aspose  

```
C:\OCR\Input\doc1.tif: The quick brown fox jumps over the laz...
C:\OCR\Input\doc2.tif: Invoice #12345
Date: 2023-11-01
Total: $1,250.00
...
```
```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1 – Create OCR engine (CPU or GPU)
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.UseGpu = true; // Try GPU, fallback to CPU automatically

        // Step 2 – List of TIFF files to process
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // Step 3 – Process each file
        foreach (var filePath in imageFiles)
        {
            var ocrImage = OcrImage.FromFile(filePath);
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Show a short preview
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");

            // Optional: Save full text to a .txt file
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
        }
    }
}
```

## Powiązane samouczki

- [How To Use Ocr In C Extract Text From Images With Gpu Accele](/ocr/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/)
- [Recognize Text From Image With Aspose Ocr Gpu Accelerated C](/ocr/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}