---
category: general
date: 2026-02-14
description: Wczytaj plik obrazu i wyodrębnij tekst z paragonu przy użyciu silnika
  Aspose OCR GPU. Dowiedz się, jak ustawić maksymalną pamięć GPU, skonfigurować pamięć
  GPU i wydajnie uruchomić OCR na obrazie.
draft: false
keywords:
- load image file
- extract text from receipt
- set max gpu memory
- run OCR on image
- configure gpu memory
language: pl
og_description: Wczytaj plik obrazu i wyodrębnij tekst z paragonu przy użyciu silnika
  Aspose OCR GPU. Ten przewodnik pokazuje, jak ustawić maksymalną pamięć GPU i uruchomić
  OCR na obrazie w C#.
og_title: Wczytaj plik obrazu i wyodrębnij tekst paragonu przy użyciu OCR na GPU w
  C#
tags:
- C#
- OCR
- Aspose
- GPU
title: Wczytaj plik obrazu i wyodrębnij tekst paragonu przy użyciu GPU OCR w C#
url: /pl/net/ocr-configuration/load-image-file-extract-receipt-text-with-gpu-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Załaduj plik obrazu i wyodrębnij tekst paragonu przy użyciu GPU OCR w C#

Kiedykolwiek potrzebowałeś **load image file** i wyciągnąć dokładny tekst z paragonu, ale utknąłeś na etapie OCR? Nie jesteś jedyny. W wielu rzeczywistych aplikacjach — trackerach wydatków, systemach inwentaryzacji czy nawet prostych botach skanujących paragony — możliwość szybkiego odczytania obrazu paragonu może być przełomowa.  

Dobre wieści? Dzięki silnikowi przyspieszonemu GPU od Aspose.OCR możesz **load image file**, **set max GPU memory** i **run OCR on image** w kilku zgrabnych linijkach C#. Poniżej przeprowadzimy cały proces, od konfiguracji GPU po wypisanie wyodrębnionego tekstu.

## Co się nauczysz

* **Load image file** z dysku przy użyciu `ImageStream` Aspose.
* **Configure GPU memory**, aby silnik nigdy nie zużywał więcej pamięci RAM niż pozwolisz.
* **Run OCR on image** i wyciągnąć każdy znak z paragonu.
* Radzić sobie ze typowymi pułapkami — takimi jak błędy out‑of‑memory lub rozmyte skany.
* Zweryfikować wynik i dostroić ustawienia dla lepszej dokładności.

Bez zewnętrznych usług, bez niejasnych sztuczek — po prostu czysty kod C#, który możesz wkleić do dowolnego projektu .NET 6+.

---

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz:

* .NET 6 SDK lub nowszy zainstalowany.
* Ważną licencję Aspose.OCR (lub możesz użyć trybu darmowej oceny).
* Pakiety NuGet `Aspose.OCR` i `Aspose.OCR.Gpu` dodane do projektu.
* Przykładowy obraz paragonu (`receipt.png`) gotowy na dysku.

Jeśli coś z tego jest nieznane, zatrzymaj się na chwilę i zainstaluj pakiety:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

To wszystko — nie są potrzebne dodatkowe natywne biblioteki, ponieważ wsparcie GPU jest wbudowane bezpośrednio w pakiet NuGet.

---

## Załaduj plik obrazu i przygotuj silnik GPU

Pierwszą rzeczą, którą musisz zrobić, jest **load image file** do `ImageStream`. Ten obiekt abstrahuje szczegóły systemu plików i daje silnikowi OCR czystą, pamięciową reprezentację.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Step 1️⃣: Initialize the GPU‑accelerated engine.
var gpuEngine = new GpuEngine
{
    // Step 2️⃣: Set a safety net for GPU RAM usage.
    // Here we limit the engine to 1024 MB (1 GB). Adjust as needed.
    MaxDeviceMemory = 1024 // MB
};

// Step 3️⃣: Load the receipt image from disk.
var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

// At this point the image is ready for OCR.
```

**Dlaczego to ważne:**  
*Loading the image file* za pomocą `ImageStream.FromFile` gwarantuje, że silnik widzi dokładne dane pikseli, zachowując DPI i głębię kolorów. Pominięcie tego kroku lub podanie uszkodzonego strumienia spowoduje, że OCR pominie znaki lub rzuci wyjątki.

> **Pro tip:** Jeśli masz do czynienia z plikami przesyłanymi przez użytkowników, otocz wywołanie `FromFile` blokiem try‑catch i najpierw zwaliduj rozmiar pliku. Duże obrazy mogą zalać pamięć GPU, jeśli nie **configured GPU memory** prawidłowo.

---

## Ustaw maksymalną pamięć GPU dla optymalnej wydajności

Zasoby GPU są cenne, szczególnie na współdzielonych serwerach lub laptopach z ograniczoną pamięcią VRAM. Właściwość `MaxDeviceMemory` informuje Aspose, ile pamięci GPU może bezpiecznie przydzielić.

```csharp
// Example: Restrict to 512 MB for low‑end GPUs.
gpuEngine.MaxDeviceMemory = 512; // MB
```

Gdy **set max GPU memory**, silnik automatycznie przełączy się na przetwarzanie CPU, jeśli nie będzie w stanie spełnić żądania — zapobiegając awariom. To najbezpieczniejszy sposób na **configure GPU memory** bez twardego kodowania limitów specyficznych dla urządzenia.

**Kiedy dostosować:**  
* Jeśli zauważysz `OutOfMemoryException` podczas intensywnego przetwarzania wsadowego, obniż limit.  
* Jeśli Twoje paragony są wysokiej rozdzielczości (300 DPI+), podnieś go do 2 GB, aby utrzymać wysoką prędkość.

---

## Uruchom OCR na obrazie, aby wyodrębnić tekst z paragonu

Teraz najciekawsza część — faktycznie **run OCR on image** i wyciągnąć tekst z paragonu. Metoda `Recognize` zwraca obiekt `OcrResult`, który zawiera właściwość `Text` z wyjściem w postaci zwykłego tekstu.

```csharp
// Step 4️⃣: Perform OCR.
OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

// Step 5️⃣: Output the extracted text.
Console.WriteLine("=== Receipt Text ===");
Console.WriteLine(ocrResult.Text);
```

Konsola wyświetli coś podobnego do:

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

**Dlaczego to działa:**  
Silnik GPU uruchamia model deep‑learningowy, który został wytrenowany na różnych układach dokumentów. Dostarczając czysty, prawidłowo załadowany obraz, dajesz modelowi najlepszą szansę na **extract text from receipt** dokładnie.

---

## Zweryfikuj wynik i typowe problemy

Nawet przy potężnym silniku OCR nie jest magią. Oto kilka rzeczy, na które warto zwrócić uwagę:

| Problem | Przyczyna | Rozwiązanie |
|-------|-------|-----|
| Zniekształcone znaki | Niska kontrastowość lub rozmyty obraz | Wstępnie przetwórz za pomocą `ImageProcessor` Aspose, aby zwiększyć kontrast |
| Brakujące linie | Obraz przycięty zbyt mocno | Upewnij się, że paragon w pełni mieści się w granicach obrazu |
| Błędy out‑of‑memory | `MaxDeviceMemory` zbyt niski dla rozmiaru obrazu | Zwiększ `MaxDeviceMemory` lub najpierw zmniejsz rozmiar obrazu |
| Nieprawidłowy język | Paragon zawiera tekst nie‑angielski | Ustaw `gpuEngine.Language = OcrLanguage.Spanish;` (lub odpowiedni) |

Jeśli napotkasz którykolwiek z nich, szybkim obejściem jest zmiana rozmiaru obrazu do mniej niż 2000 px po najdłuższym boku — to znacząco zmniejsza obciążenie GPU bez utraty czytelności w większości paragonów.

---

## Pełny działający przykład (gotowy do kopiowania i wklejania)

Poniżej znajduje się cały program, gotowy do kompilacji. Zamień ścieżkę pliku na własną lokalizację paragonu.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class ReceiptOcrDemo
{
    static void Main()
    {
        // 1️⃣ Create GPU‑accelerated engine with a safe memory cap.
        var gpuEngine = new GpuEngine
        {
            MaxDeviceMemory = 1024 // MB – adjust for your hardware
        };

        // 2️⃣ Load the receipt image from disk.
        //    Make sure the path points to a valid PNG/JPEG file.
        var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

        // 3️⃣ Run OCR – this will automatically use the GPU if available.
        OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

        // 4️⃣ Print the extracted text.
        Console.WriteLine("=== Receipt Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Oczekiwany wynik w konsoli** (twój paragon będzie oczywiście inny):

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

Uruchom program poleceniem `dotnet run`. Jeśli zobaczysz wydrukowany tekst, gratulacje — udało Ci się **load image file**, **set max GPU memory** i **run OCR on image**, aby **extract text from receipt**.

---

## Najczęściej zadawane pytania

**P: Czy to działa na maszynach bez dedykowanego GPU?**  
O: Tak. Aspose.OCR elegancko przełączy się w tryb CPU, jeśli nie wykryje kompatybilnego GPU. Nadal będziesz mógł **load image file** i **run OCR on image**, choć nieco wolniej.

**P: Czy mogę przetwarzać wiele paragonów w partii?**  
O: Oczywiście. Otocz kod rozpoznawania pętlą `foreach`, ale pamiętaj, aby ponownie używać tej samej instancji `GpuEngine` — to unika ponownego inicjowania zasobów GPU dla każdego pliku.

**P: Co jeśli mój paragon jest w języku innym niż angielski?**  
O: Ustaw język przed wywołaniem `Recognize`:

```csharp
gpuEngine.Language = OcrLanguage.French;
```

---

## Kolejne kroki i powiązane tematy

Teraz, gdy opanowałeś podstawy, rozważ dalsze eksploracje:

* **Fine‑tuning OCR accuracy** – eksperymentuj z `gpuEngine.RecognitionOptions`, takimi jak `EnableDeskew` lub `ContrastEnhancement`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}