---
category: general
date: 2026-02-11
description: Dowiedz się, jak uruchomić OCR na wielostronicowym pliku TIFF w C# przy
  użyciu Aspose OCR. Konwertuj TIFF na tekst, wyodrębnij tekst z TIFF i szybko rozpoznaj
  tekst z obrazu.
draft: false
keywords:
- how to run OCR
- recognize text from image
- convert tiff to text
- extract text from tiff
- perform OCR on image
language: pl
og_description: Jak uruchomić OCR na wielostronicowym pliku TIFF przy użyciu Aspose
  OCR w C#. Przewodnik krok po kroku, jak konwertować TIFF na tekst, wyodrębniać tekst
  z TIFF oraz rozpoznawać tekst z obrazu.
og_title: Jak uruchomić OCR na wielostronicowych obrazach TIFF – Kompletny samouczek
  C#
tags:
- OCR
- C#
- Aspose
- TIFF
title: Jak uruchomić OCR na wielostronicowych obrazach TIFF przy użyciu Aspose OCR
  – przewodnik C#
url: /pl/net/text-recognition/how-to-run-ocr-on-multi-page-tiff-images-with-aspose-ocr-c-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uruchomić OCR na wielostronicowych obrazach TIFF przy użyciu Aspose OCR

Zastanawiałeś się kiedyś **jak uruchomić OCR** na zeskanowanym pliku TIFF, który zawiera kilka stron? Nie jesteś sam — wielu programistów napotyka ten problem, gdy muszą wydobyć przeszukiwalny tekst ze starych dokumentów. Dobra wiadomość? Dzięki Aspose OCR możesz rozpoznawać tekst z plików graficznych w zaledwie kilku linijkach kodu C#, a otrzymasz zwykły, połączony tekst gotowy do indeksowania lub dalszego przetwarzania.

W tym samouczku przeprowadzimy Cię przez cały proces: od instalacji pakietu Aspose OCR, przez wczytanie wielostronicowego pliku TIFF, po konwersję TIFF na tekst i w końcu wyświetlenie wyodrębnionej zawartości. Po zakończeniu będziesz potrafił **wyodrębnić tekst z plików TIFF**, **rozpoznawać tekst z obrazów** oraz zautomatyzować proces dla dziesiątek plików w zadaniu wsadowym. Bez magii, tylko jasne, praktyczne kroki.

## Czego się nauczysz

- Jak skonfigurować silnik Aspose OCR do rozpoznawania języka angielskiego.  
- Dokładny kod potrzebny do **konwersji TIFF na tekst** przy użyciu klasy `OcrEngine`.  
- Wskazówki dotyczące obsługi wielostronicowych obrazów i zapewnienia prawidłowego oddzielenia każdej strony.  
- Typowe pułapki (np. brakujące natywne zależności) i jak ich unikać.  

**Wymagania wstępne** – potrzebujesz .NET 6 lub nowszego, Visual Studio (lub dowolnego edytora C#) oraz połączenia internetowego do funkcji automatycznego pobierania zasobów. To wszystko; nie musisz walczyć z dodatkowymi natywnymi bibliotekami.

---

## Krok 1 – Zainstaluj pakiet NuGet Aspose OCR

Zanim będziesz mógł **wykonywać OCR na obrazach**, musisz dodać bibliotekę do swojego projektu.

```bash
dotnet add package Aspose.OCR
```

> **Wskazówka:** Jeśli pracujesz w Visual Studio, możesz także kliknąć prawym przyciskiem projektu → *Zarządzaj pakietami NuGet* → wyszukać „Aspose.OCR” i kliknąć *Zainstaluj*.

Pakiet zawiera wszystko, czego potrzebujesz, a przy ustawieniu `AutomaticResourceDownload = true` silnik pobierze pakiety językowe w locie.

---

## Krok 2 – Zainicjalizuj silnik OCR (Jak uruchomić OCR)

Teraz, gdy pakiet jest już dodany, tworzymy i konfigurowamy instancję `OcrEngine`. To jest serce **jak uruchomić OCR** w naszym scenariuszu.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;   // For Image class
using System;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // Recognize English text
    AutomaticResourceDownload = true,        // Auto‑download language data
    OutputFormat = OcrOutputFormat.Text      // Get plain concatenated text
};
```

**Dlaczego to ważne:** Ustawienie `Language` informuje silnik, jakiego zestawu znaków się spodziewać, natomiast `AutomaticResourceDownload` oszczędza ręcznego umieszczania plików językowych na serwerze. `OutputFormat` ustawiony na `Text` daje nam prosty ciąg znaków — idealny do **konwersji TIFF na tekst**.

---

## Krok 3 – Wczytaj wielostronicowy TIFF (Rozpoznaj tekst z obrazu)

Plik TIFF może zawierać wiele klatek, z których każda reprezentuje stronę. Klasa `System.Drawing.Image` abstrahuje to dla nas.

```csharp
// Step 3: Load the multi‑page image to be processed
using (var image = Image.FromFile("YOUR_DIRECTORY/multi_page.tiff"))
{
    // Step 4: Run OCR on the image
    var ocrResult = ocrEngine.Recognize(image);

    // Step 5: Display the extracted text
    Console.WriteLine(ocrResult.Text);
}
```

> **Co jeśli plik nie znajduje się w tym samym folderze?** Po prostu podaj pełną ścieżkę absolutną lub użyj `Path.Combine` z `AppContext.BaseDirectory`.  
> **A co z użyciem pamięci?** Instrukcja `using` zwalnia obraz po przetworzeniu, zapobiegając wyciekom — co jest kluczowe przy przetwarzaniu wsadowym dziesiątek dużych plików TIFF.

`Wywołanie` Recognize automatycznie iteruje po każdej stronie w pliku TIFF, łącząc wyniki z podziałem na linie. Dlatego zobaczysz, że każda strona jest oddzielona, gdy wydrukujesz `ocrResult.Text`.

---

## Krok 4 – Pełny działający przykład (Wszystkie kroki w jednym pliku)

Poniżej znajduje się kompletny, gotowy do uruchomienia program konsolowy. Skopiuj i wklej go do nowego projektu .NET console i naciśnij **F5**.

```csharp
// File: Program.cs
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Configure the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English,
                AutomaticResourceDownload = true,
                OutputFormat = OcrOutputFormat.Text
            };

            // 2️⃣ Load your multi‑page TIFF (replace with your actual path)
            const string tiffPath = @"YOUR_DIRECTORY\multi_page.tiff";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            // 3️⃣ Perform OCR
            using (var image = Image.FromFile(tiffPath))
            {
                var result = ocrEngine.Recognize(image);

                // 4️⃣ Output the extracted text
                Console.WriteLine("=== OCR RESULT ===");
                Console.WriteLine(result.Text);
                Console.WriteLine("==================");
            }

            // Keep console open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Oczekiwany wynik** (skrócony dla zwięzłości):

```
=== OCR RESULT ===
Page 1: The quick brown fox jumps over the lazy dog.
Page 2: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
==================
Press any key to exit...
```

Każda strona pojawia się w osobnej linii, ponieważ `OcrOutputFormat.Text` wstawia podział linii między klatkami. Jeśli potrzebujesz innego separatora, możesz przetworzyć `result.Text` przy użyciu `String.Replace`.

---

## Krok 5 – Obsługa typowych przypadków brzegowych

### 5.1 Duże pliki TIFF  
Podczas pracy z plikami TIFF o rozmiarze gigabajtowym ładowanie całego pliku do pamięci może być problematyczne. Obejściem jest przetwarzanie każdej klatki osobno:

```csharp
using (var image = Image.FromFile(tiffPath))
{
    for (int i = 0; i < image.GetFrameCount(FrameDimension.Page); i++)
    {
        image.SelectActiveFrame(FrameDimension.Page, i);
        var pageResult = ocrEngine.Recognize(image);
        Console.WriteLine($"--- Page {i + 1} ---");
        Console.WriteLine(pageResult.Text);
    }
}
```

### 5. Dokumenty nie‑angielskie  
Jeśli potrzebujesz **rozpoznawać tekst z obrazu** w języku hiszpańskim lub francuskim, po prostu zmień właściwość `Language`:

```csharp
ocrEngine.Language = OcrLanguage.Spanish; // or OcrLanguage.French
```

Aspose automatycznie pobierze odpowiednie zasoby językowe.

### 5. Zapisywanie wyniku  
Często będziesz chciał **konwertować TIFF na tekst** i zapisać wynik w pliku `.txt`:

```csharp
System.IO.File.WriteAllText("output.txt", ocrResult.Text);
```

Możesz także podzielić wynik na strony używając `String.Split(Environment.NewLine)` i zapisać każdy fragment do osobnego pliku.

---

## Porady i pułapki

- **AutomaticResourceDownload** działa przy pierwszym uruchomieniu aplikacji; kolejne uruchomienia są offline.  
- Jeśli widzisz zniekształcone znaki, sprawdź dwukrotnie ustawienie `Language`; niepasujące pakiety językowe powodują błędne rozpoznawanie.  
- Dla plików PDF, które zostały rasteryzowane do TIFF, możesz zwiększyć `ocrEngine.Dpi` (domyślnie 300) w celu uzyskania lepszej dokładności.  
- Zawsze otaczaj `Image.FromFile` blokiem `using`; w przeciwnym razie zablokujesz plik i nie będziesz mógł go później usunąć lub przenieść.

---

## Najczęściej zadawane pytania

**P: Czy to działa z jednostronicowymi plikami TIFF?**  
**O:** Zdecydowanie tak. Silnik traktuje jednoklatkowy TIFF tak samo; otrzymasz po prostu jedną linię tekstu.

**P: Czy mogę przetwarzać pliki PNG lub JPEG w ten sam sposób?**  
**O:** Tak — wystarczy zmienić rozszerzenie pliku. Metoda `Recognize` akceptuje dowolny format `System.Drawing.Image`.

**P: Co zrobić, jeśli potrzebuję wyniku OCR jako PDF zamiast zwykłego tekstu?**  
**O:** Ustaw `OutputFormat = OcrOutputFormat.Pdf`, a `ocrResult` będzie zawierał tablicę bajtów PDF, którą możesz zapisać na dysku.

---

## Zakończenie

Masz teraz kompletną, kompleksową metodę **jak uruchomić OCR** na wielostronicowych plikach TIFF przy użyciu Aspose OCR w C#. Konfigurując silnik, wczytując obraz i wywołując `Recognize`, możesz **wyodrębnić tekst z TIFF**, **konwertować TIFF na tekst** oraz **rozpoznawać tekst z obrazu** przy użyciu kilku linijek kodu. Śmiało dostosuj język, format wyjścia lub przetwarzanie klatka po klatce, aby dopasować je do własnych potrzeb przetwarzania wsadowego.

Gotowy na kolejny krok? Spróbuj połączyć to podejście z usługą monitorującą folder, aby automatycznie **wykonywać OCR na obrazach**, gdy pojawią się w folderze docelowym, lub zintegrować wynik z indeksem wyszukiwania dla natychmiastowego pełnotekstowego przeszukiwania. Możliwości są nieograniczone, a kod, który właśnie zobaczyłeś, stanowi solidną podstawę.

Jeśli napotkasz jakiekolwiek problemy, zostaw komentarz poniżej lub napisz do mnie na GitHubie. Szczęśliwego kodowania i ciesz się przekształcaniem uciążliwych plików TIFF w przeszukiwalny tekst!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}