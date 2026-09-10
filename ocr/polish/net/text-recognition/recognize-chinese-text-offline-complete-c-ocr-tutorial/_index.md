---
category: general
date: 2026-01-02
description: Dowiedz się, jak rozpoznawać chiński tekst i wyodrębniać tekst z plików
  PNG przy użyciu rozpoznawania tekstu offline w Aspose.OCR. Nie potrzebujesz internetu
  – wykonaj OCR obrazu w kilku prostych krokach.
draft: false
keywords:
- recognize chinese text
- extract text from png
- offline text recognition
- perform OCR on image
language: pl
og_description: Rozpoznawaj chiński tekst bez internetu. Ten samouczek pokazuje, jak
  wyodrębnić tekst z pliku PNG przy użyciu rozpoznawania tekstu offline i wykonać
  OCR na obrazie w C#.
og_title: rozpoznawanie chińskiego tekstu offline – przewodnik krok po kroku w C#
tags:
- OCR
- C#
- Aspose
title: Rozpoznawanie chińskiego tekstu offline – Kompletny samouczek OCR w C#
url: /pl/net/text-recognition/recognize-chinese-text-offline-complete-c-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznawanie chińskiego tekstu offline – Kompletny samouczek OCR w C#

Czy kiedykolwiek potrzebowałeś **rozpoznawać chiński tekst** ze zeskanowanego PNG, ale Twoja aplikacja działa na maszynie bez dostępu do internetu? Nie jesteś sam. W wielu scenariuszach korporacyjnych — pomyśl o serwerach odizolowanych od sieci lub urządzeniach polowych — poleganie na usługach w chmurze po prostu nie wchodzi w rachubę.  

W tym przewodniku przeprowadzimy Cię przez samodzielne rozwiązanie, które pozwala **wyodrębniać tekst z plików png**, uruchamiać **rozpoznawanie tekstu offline** oraz **wykonywać OCR na obrazach** przy użyciu Aspose.OCR. Po zakończeniu będziesz mieć gotowy do uruchomienia program konsolowy w C#, który wypisuje chińskie znaki bezpośrednio w konsoli.

## Prerequisites

- .NET 6 SDK (lub dowolna nowsza wersja .NET) zainstalowana lokalnie.  
- Visual Studio 2022 lub VS Code — cokolwiek wolisz.  
- Kopia pakietu NuGet Aspose.OCR dla .NET (`Aspose.OCR`).  
- Pliki zasobów językowych dla angielskiego i uproszczonego chińskiego (samouczek pokazuje, jak pobrać je automatycznie).  
- Obraz o nazwie `chinese_doc.png` umieszczony w folderze, do którego możesz odwołać się (`placeholder YOUR_DIRECTORY`).  

No additional services, no API keys—just a local DLL and a couple of resource files.

---

## Krok 1 – Pobierz wymagane zasoby językowe (raz)

Aspose.OCR przechowuje pakiety językowe na dysku. Przy pierwszym uruchomieniu aplikacji musisz je pobrać. Wywołanie `ResourceManager.DownloadResources` robi dokładnie to, a ponieważ przekazujemy zarówno angielski, jak i uproszczony chiński, silnik może później przełączać się między nimi bez dodatkowego ruchu sieciowego.

```csharp
using Aspose.OCR;

// Download English and Simplified Chinese language packs (run once)
ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);
```

> **Wskazówka:** Przechowuj pobrany folder (`Aspose.OCR.Resources`) w systemie kontroli wersji, jeśli potrzebujesz odtwarzalnych kompilacji na wielu maszynach.

## Krok 2 – Zainicjalizuj silnik OCR w trybie offline

Ustawienie `OfflineMode = true` informuje bibliotekę, aby unikała jakichkolwiek wywołań HTTP. To klucz do prawdziwego **rozpoznawania tekstu offline**.

```csharp
// Initialise the OCR engine for offline use
var ocrEngine = new OcrEngine()
{
    OfflineMode = true   // Guarantees no network traffic
};
```

> **Dlaczego to ważne:** Niektóre biblioteki OCR przełączają się na usługi w chmurze, gdy brakuje pakietu językowego. Wymuszając tryb offline, zapewniamy deterministyczną wydajność i zgodność z politykami prywatności danych.

## Krok 3 – Załaduj PNG, który chcesz przetworzyć

Użyjemy `System.Drawing.Bitmap` do odczytania obrazu. Jeśli Twój projekt celuje w .NET 6+ na platformach nie‑Windows, rozważ `SkiaSharp` jako alternatywę, ale w większości wdrożeń skoncentrowanych na Windows `Bitmap` działa bez problemu.

```csharp
using System.Drawing;

// Load the PNG that contains Chinese characters
var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
var image = new Bitmap(imagePath);
```

> **Przypadek brzegowy:** Jeśli PNG jest bardzo duży (powyżej 5 MP), możesz najpierw zmniejszyć jego rozmiar, aby przyspieszyć rozpoznawanie i zmniejszyć zużycie pamięci:

```csharp
// Optional downscale for huge images
if (image.Width * image.Height > 5_000_000)
{
    var scaled = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
    image.Dispose();
    image = scaled;
}
```

## Krok 4 – Uruchom rozpoznawanie z językiem chińskim uproszczonym

Tutaj informujemy silnik, którego języka dokładnie użyć. Obiekt `RecognitionOptions` pozwala również dostosować takie opcje jak `DetectOrientation` czy `PreserveFormatting`, ale domyślne ustawienia działają dobrze dla większości drukowanych dokumentów.

```csharp
using Aspose.OCR;

// Perform OCR using Simplified Chinese language pack
var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
{
    Language = Language.ChineseSimplified
});
```

## Krok 5 – Wyświetl (lub dalej przetwórz) wyodrębniony tekst

Właściwość `OcrResult.Text` zawiera reprezentację w postaci zwykłego tekstu. Możesz ją wypisać w konsoli, zapisać do pliku lub przekazać do dalszego potoku NLP.

```csharp
// Output the recognized Chinese text to the console
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

### Oczekiwany wynik

Jeśli `chinese_doc.png` zawiera frazę „你好，世界！”, konsola wyświetli:

```
=== Recognized Chinese Text ===
你好，世界！
```

> **Uwaga:** Dokładność OCR zależy od jakości obrazu, czytelności czcionki i kontrastu. Dla najlepszych rezultatów używaj skanów o wysokiej rozdzielczości (300 dpi lub wyższej) i upewnij się, że tekst nie jest pochyły.

---

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do skopiowania program. Zapisz go jako `Program.cs` w nowym projekcie konsolowym i uruchom `dotnet run`. Wszystkie kroki są połączone, więc możesz zobaczyć przepływ od pobrania zasobów po ostateczny wynik.

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;

class OfflineExample
{
    static void Main()
    {
        // 1️⃣ Download language resources (only needed once)
        ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);

        // 2️⃣ Initialise OCR engine in offline mode
        var ocrEngine = new OcrEngine()
        {
            OfflineMode = true
        };

        // 3️⃣ Load the PNG image
        var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
        using var image = new Bitmap(imagePath);

        // 4️⃣ Recognise Simplified Chinese text
        var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
        {
            Language = Language.ChineseSimplified
        });

        // 5️⃣ Print the result
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Wskazówka:** Owiń wywołanie `ResourceManager.DownloadResources` w blok `try/catch`, jeśli chcesz elegancko obsłużyć sytuację, gdy internet jest naprawdę niedostępny. W przeciwnym razie metoda rzuci `NetworkException`.

---

## Najczęściej zadawane pytania (FAQ)

| Question | Answer |
|----------|--------|
| **Czy mogę rozpoznawać tradycyjny chiński?** | Tak — zamień `Language.ChineseSimplified` na `Language.ChineseTraditional` i pobierz odpowiedni pakiet. |
| **Co jeśli muszę wyodrębnić tekst z JPEG zamiast PNG?** | Ten sam kod działa; wystarczy zmienić rozszerzenie pliku. `Bitmap` obsługuje większość popularnych formatów rastrowych. |
| **Czy istnieje sposób, aby uzyskać ramki ograniczające dla każdego znaku?** | Ustaw `RecognitionOptions.DetectRegions = true`. `OcrResult` będzie wtedy zawierał obiekty `Region` z współrzędnymi. |
| **Jak uruchomić to na Linuksie?** | Użyj pakietu `System.Drawing.Common` (1.0+). Na Linuksie bez interfejsu graficznego może być potrzebna natywna zależność `libgdiplus`. |
| **Czy mogę przetwarzać wsadowo folder obrazów?** | Oczywiście — otocz logikę rozpoznawania w pętlę `foreach (var file in Directory.GetFiles(folder, "*.png"))`. |

## Kolejne kroki i powiązane tematy

- **Popraw dokładność**: eksperymentuj z `RecognitionOptions.PreprocessImage = true`, aby silnik automatycznie zwiększał kontrast.  
- **Łącz języki**: możesz przekazać tablicę języków do `ResourceManager.DownloadResources` i pozwolić silnikowi automatycznie wykrywać.  
- **Zintegruj z interfejsem UI**: przenieś kod konsolowy do aplikacji WinForms lub WPF i wyświetl wynik OCR w polu tekstowym.  
- **Poznaj inne biblioteki Aspose**: `Aspose.PDF` do generowania PDF, `Aspose.Slides` do automatyzacji slajdów, itp.  

Jeśli interesuje Cię wyodrębnianie tekstu z innych formatów obrazów, ten sam schemat ma zastosowanie — po prostu zamień ścieżkę pliku i ewentualnie dostosuj opcje przetwarzania wstępnego. Szczęśliwego kodowania!

![przykład rozpoznawania chińskiego tekstu](/images/recognize-chinese-text.png "Zrzut ekranu pokazujący wynik rozpoznawania chińskiego tekstu w konsoli")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}