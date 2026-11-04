---
category: general
date: 2026-01-13
description: Dowiedz się, jak szybko rozpoznawać tekst z obrazu i wyodrębniać tekst
  z paragonu przy użyciu Aspose OCR. Zawiera kroki ładowania obrazu do OCR oraz ustawiania
  identyfikatora urządzenia GPU.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for ocr
- set gpu device id
language: pl
og_description: Rozpoznawaj tekst z obrazu natychmiast za pomocą Aspose OCR. Postępuj
  zgodnie z tym przewodnikiem krok po kroku, aby wczytać obraz do OCR, ustawić identyfikator
  urządzenia GPU i wyodrębnić tekst z paragonu.
og_title: Rozpoznawanie tekstu z obrazu – Kompletny przewodnik po C# z przyspieszeniem
  GPU
tags:
- Aspose OCR
- C#
- GPU computing
title: Rozpoznawanie tekstu z obrazu przy użyciu Aspose OCR – przyspieszony GPU tutorial
  C#
url: /pl/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznawanie tekstu z obrazu – Kompletny przewodnik C# przyspieszony GPU

Czy kiedykolwiek potrzebowałeś **rozpoznawać tekst z obrazu**, ale wersja CPU była wyjątkowo wolna? Może próbujesz **wyodrębnić tekst z paragonu** i opóźnienia psują doświadczenie użytkownika. Dobrą wiadomością jest to, że nie musisz godzić się na niską wydajność — pakiet GPU Aspose OCR może przyspieszyć proces, a kod zajmuje zaledwie kilka linii.

W tym samouczku przeprowadzimy Cię przez pełny, działający przykład, który pokazuje, jak **załadować obraz do OCR**, skonfigurować GPU za pomocą **set GPU device ID**, a na koniec pobrać wynik w postaci czystego tekstu. Po zakończeniu będziesz mieć gotowy fragment kodu, który działa na dowolnym nowoczesnym systemie Windows lub Linux z obsługiwaną kartą NVIDIA.

---

## Czego będziesz potrzebować

- **.NET 6+** (lub .NET Framework 4.7.2+) – API działa z obiema wersjami.  
- **Aspose.OCR** pakiet NuGet **plus** dodatek **Aspose.OCR.Gpu**.  
- Karta graficzna NVIDIA z co najmniej 2 GB VRAM (demo ogranicza użycie do 1 GB).  
- Przykładowy obraz, np. zeskanowany paragon (`receipt.jpg`).

Jeśli już masz projekt, po prostu uruchom `dotnet add package Aspose.OCR` i `dotnet add package Aspose.OCR.Gpu`. Nie są wymagane dodatkowe biblioteki natywne; SDK dostarcza niezbędne pliki binarne CUDA.

---

## Implementacja krok po kroku

### ## Jak rozpoznawać tekst z obrazu przy użyciu Aspose OCR i GPU

Poniżej znajduje się **kompletny, samodzielny program**. Skopiuj‑wklej go do nowego projektu konsolowego i naciśnij `Ctrl+F5`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑accelerated namespace

class GpuOcrDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize a GPU‑enabled OCR engine
        // -------------------------------------------------
        var ocrEngine = new GpuOcrEngine();

        // -------------------------------------------------
        // Step 2: (Optional) Select the GPU device and limit memory usage
        // -------------------------------------------------
        ocrEngine.DeviceId = 0;        // set GPU device ID – first GPU in the system
        ocrEngine.MaxMemoryMb = 1024;  // cap at 1 GB to avoid OOM on shared machines

        // -------------------------------------------------
        // Step 3: Load the image you want to recognize
        // -------------------------------------------------
        var receiptImage = OcrImage.FromFile(@"YOUR_DIRECTORY/receipt.jpg");

        // -------------------------------------------------
        // Step 4: Perform OCR – here we extract text from receipt (English)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);

        // -------------------------------------------------
        // Step 5: Output the recognized plain text
        // -------------------------------------------------
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

> **Pro tip:** Jeśli Twój komputer ma wiele GPU, zmień `DeviceId` na `1`, `2` itd., aby wybrać mniej obciążoną kartę. SDK zgłosi wyraźny `GpuDeviceNotFoundException`, jeśli podany identyfikator jest poza zakresem.

### ### Krok 1: Załaduj obraz do OCR

Wywołanie `OcrImage.FromFile` robi więcej niż tylko odczyt bitmapy — wstępnie przetwarza obraz (prostowanie, binaryzacja) na podstawie wewnętrznych heurystyk. Dlatego **load image for OCR** jest osobnym krokiem: możesz podmienić na `MemoryStream`, jeśli obraz znajduje się w bazie danych.

```csharp
var receiptImage = OcrImage.FromFile(@"C:\Invoices\receipt.jpg");
```

Jeśli potrzebujesz **rozpoznawać tekst z obrazu**, który już znajduje się w pamięci:

```csharp
using (var ms = new MemoryStream(File.ReadAllBytes(@"receipt.jpg")))
{
    var receiptImage = OcrImage.FromStream(ms);
}
```

### ### Krok 2: Ustaw identyfikator urządzenia GPU i limity pamięci

Zasoby GPU są ograniczone. Udostępniając `DeviceId` i `MaxMemoryMb`, Aspose pozwala bezpiecznie **set GPU device ID**, zapobiegając jednemu procesowi zajmowanie całej karty.

```csharp
ocrEngine.DeviceId = 0;        // first GPU
ocrEngine.MaxMemoryMb = 1024; // 1 GB ceiling
```

Jeśli przekroczysz limit pamięci, silnik automatycznie przełączy się na pamięć systemową RAM, co jest wolniejsze, ale zapobiega awariom.

### ### Krok 3: Wyodrębnij tekst z paragonu (rozpoznawanie tekstu z obrazu)

Metoda `Recognize` wykonuje najcięższą pracę. Możesz podać dowolny język obsługiwany przez Aspose OCR; dla paragonów najczęściej wystarcza angielski, ale możesz także dodać `OcrLanguage.Spanish` lub własny pakiet językowy.

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);
Console.WriteLine(ocrResult.Text);
```

**Oczekiwany wynik** (przykład):

```
Store: QuickMart
Date: 2025-12-01
Total: $23.45
Thank you for shopping!
```

---

## Wspólne warianty i przypadki brzegowe

| Sytuacja | Co zmienić | Dlaczego |
|----------|------------|----------|
| **Wiele paragonów na jednym obrazie** | Wywołaj `ocrEngine.Recognize` na każdym przyciętym regionie (użyj `OcrImage.Crop`) | Poprawia dokładność, ponieważ silnik widzi mniejszy, czystszy obszar. |
| **Skanowanie o niskiej rozdzielczości (<150 dpi)** | Zwiększ rozdzielczość przy pomocy `receiptImage.Resize(2.0)` przed rozpoznaniem | Wyższa gęstość pikseli dostarcza GPU więcej danych do przetworzenia. |
| **Paragony w języku innym niż angielski** | Przekaż `OcrLanguage.French` (lub własny plik `.traineddata`) | Modele specyficzne dla języka zmniejszają liczbę fałszywych trafień. |
| **GPU niedostępne** | Użyj `OcrEngine` (CPU) w bloku try‑catch | Gwarantuje, że aplikacja działa na serwerach bez graficznego interfejsu. |

```csharp
try
{
    var gpuEngine = new GpuOcrEngine();
    // configure GPU as shown earlier …
    var result = gpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
catch (GpuDeviceNotFoundException)
{
    // Graceful fallback
    var cpuEngine = new OcrEngine();
    var result = cpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
```

---

## Wskazówki dla OCR gotowego do produkcji

- **Przetwarzanie wsadowe:** Owiń pętlę rozpoznawania w `Parallel.ForEach`, ale ogranicz stopień równoległości do liczby strumieni GPU, które możesz przydzielić (zwykle 1‑2 na kartę).  
- **Higiena pamięci:** Niezwłocznie zwalniaj obiekty `OcrImage` (`receiptImage.Dispose()`), szczególnie przy przetwarzaniu tysięcy paragonów.  
- **Logowanie:** Zapisuj `ocrResult.Confidence` dla każdej linii; niska pewność może wywołać ręczny proces weryfikacji.  
- **Bezpieczeństwo:** Przy obsłudze wrażliwych paragonów, przechowuj pliki obrazów w zaszyfrowanych folderach tymczasowych i usuwaj je po przetworzeniu.  

---

## Podsumowanie

Masz teraz **kompletny, działający przykład**, który pokazuje, jak **rozpoznawać tekst z obrazu** przy użyciu przyspieszenia GPU Aspose OCR, **załadować obraz do OCR**, **ustawić identyfikator urządzenia GPU**, a na koniec **wyodrębnić tekst z paragonu** w kilku zwięzłych krokach. Kod jest gotowy do skopiowania, a wyjaśnienia dostarczają wystarczającego kontekstu, aby dostosować go do scenariuszy wielojęzycznych, wielokartowych lub o wysokiej przepustowości.

Gotowy na kolejne wyzwanie? Spróbuj podać strumień wideo na żywo do `GpuOcrEngine` w celu skanowania paragonów w czasie rzeczywistym lub zintegrować wynik z API księgowym. Nie ma granic, gdy połączysz szybki OCR GPU z czystym projektem w C#.

*Miłego kodowania i niech Twój OCR będzie zawsze szybki!* 

![zrzut ekranu demonstracji rozpoznawania tekstu z obrazu](placeholder-image.png "przykład rozpoznawania tekstu z obrazu")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}