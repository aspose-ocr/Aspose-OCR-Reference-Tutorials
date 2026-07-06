---
category: general
date: 2026-02-20
description: Naucz się odczytywać paragon w C# poprzez wyodrębnianie tekstu z obrazu
  i konwertowanie go na JSON. Kod krok po kroku z użyciem Aspose OCR.
draft: false
keywords:
- how to read receipt
- extract text from image
- convert image to json
- load image file c#
- OCR receipt C#
- Aspose OCR tutorial
language: pl
og_description: Odkryj, jak odczytać paragon w C# poprzez wczytanie pliku obrazu,
  wyodrębnienie tekstu za pomocą Aspose OCR i konwersję wyniku do JSON. Pełny przykład
  kodu.
og_title: Jak odczytać paragon w C# – wyodrębnić tekst, konwertować do JSON
tags:
- C#
- OCR
- Image Processing
- JSON
title: Jak odczytać paragon w C# – Kompletny przewodnik po wyodrębnianiu tekstu z
  obrazu
url: /pl/net/text-recognition/how-to-read-receipt-in-c-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak odczytać paragon w C# – Kompletny przewodnik

Zastanawiałeś się kiedyś, **jak odczytać paragon** ze zdjęcia programistycznie? Być może tworzysz aplikację do śledzenia wydatków i potrzebujesz wyciągnąć pozycje z fotografii paragonu spożywczego. Z mojego doświadczenia największym problemem jest przekształcenie rozmytego pliku JPEG w ustrukturyzowane dane, które naprawdę możesz wykorzystać. Dobra wiadomość? Kilka linijek C# i Aspose OCR pozwoli Ci **wyodrębnić tekst z obrazu**, a następnie **przekształcić obraz do JSON** w sposób, który wydaje się prawie magiczny.

W tym samouczku otrzymasz gotowe rozwiązanie, które **wczytuje plik obrazu C#**, uruchamia OCR i zwraca szczegółowy ładunek JSON. Bez zewnętrznych usług, bez skomplikowanych wywołań REST — po prostu czysty kod .NET, który możesz wkleić do dowolnego projektu konsolowego lub ASP.NET. Po zakończeniu zrozumiesz, dlaczego każdy krok ma znaczenie, jak radzić sobie z typowymi przypadkami brzegowymi (np. niestandardowe rozmiary paragonów) oraz jak naprawdę wygląda wynikowy JSON.

## Co będzie potrzebne

- **.NET 6.0 lub nowszy** – kod korzysta z `System.Drawing.Common`, które jest obsługiwane na Windows, Linux i macOS.  
- **Aspose.OCR for .NET** – możesz pobrać darmowy pakiet NuGet (`Aspose.OCR`) lub użyć licencjonowanej wersji, jeśli ją posiadasz.  
- **Przykładowy obraz paragonu** (`receipt.jpg`) umieszczony w miejscu dostępnym dla aplikacji.  
- Dowolne IDE (Visual Studio, Rider, VS Code).  

To wszystko. Bez dodatkowej konfiguracji, bez kluczy API.

---

## Krok 1 – Wczytaj plik obrazu C# (Primary Keyword in Action)

Zanim silnik OCR wykona swoją magię, musisz wczytać obraz do pamięci. To klasyczny krok „load image file C#”, który wielu programistom umyka.

```csharp
using System.Drawing;          // Required for Image
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to your receipt image – adjust as needed
string imagePath = @"C:\Receipts\receipt.jpg";

// Load the image into a System.Drawing.Image object
Image receiptImage = Image.FromFile(imagePath);
```

**Dlaczego to ważne:**  
`Image.FromFile` odczytuje plik *jednokrotnie* i utrzymuje otwarty uchwyt, co jest idealne przy szybkiej analizie OCR. Jeśli przetwarzasz wiele paragonów w pętli, rozważ użycie `Image.FromStream`, aby uniknąć blokowania pliku.

> **Wskazówka:** Jeśli napotkasz *FileNotFoundException*, sprawdź dokładnie ścieżkę i upewnij się, że obraz rzeczywiście istnieje. Ścieżki względne działają (`"./receipt.jpg"`), ale ścieżki bezwzględne są bezpieczniejsze w środowiskach produkcyjnych.

---

## Krok 2 – Utwórz i skonfiguruj silnik OCR

Aspose OCR dostarcza gotowy `OcrEngine`. Nie musisz trenować modelu; biblioteka już wie, jak czytać drukowany tekst, czyli dokładnie to, co znajduje się na większości paragonów.

```csharp
// Instantiate the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Optional: tweak recognition settings if your receipts are low‑contrast
ocrEngine.Config.Language = OcrLanguage.English;
ocrEngine.Config.DetectOrientation = true;   // Handles rotated receipts
```

**Dlaczego ustawiamy te opcje:**  
`DetectOrientation` nakazuje silnikowi automatycznie obrócić obraz, jeśli paragon został zeskanowany do góry nogami. Ustawienie języka zawęża zestaw znaków, co może zwiększyć dokładność — szczególnie gdy potrzebujesz jedynie angielskich danych alfanumerycznych.

---

## Krok 3 – Rozpoznaj obraz i przekształć do JSON

Teraz przychodzi najciekawsza część: **extract text from image** i **convert image to JSON** w jednym wywołaniu.

```csharp
// Perform OCR and get the result as a JSON string
string jsonResult = ocrEngine.RecognizeToJson(receiptImage);
```

Metoda `RecognizeToJson` zwraca rozbudowaną strukturę JSON, która zawiera:

- `Text`: zwykły, połączony tekst.  
- `Lines`: tablicę obiektów linii z współrzędnymi.  
- `Words`: każde słowo wraz z oceną pewności.  
- `Regions`: prostokąty otaczające wykryte bloki tekstu.

Możesz zdeserializować ten JSON do obiektu C#, jeśli potrzebujesz typowanego dostępu, ale w wielu scenariuszach wystarczy po prostu wypisać surowy JSON.

---

## Krok 4 – Wyświetl JSON (lub zapisz go)

Zobaczmy wynik i omówmy, co z nim zrobić.

```csharp
// Write the JSON to the console – perfect for quick debugging
Console.WriteLine(jsonResult);

// Bonus: Save the JSON to a file for later processing
File.WriteAllText("receipt_output.json", jsonResult);
```

### Przykładowy wynik

```json
{
  "Text":"Walmart\n123 Main St\nItem A  $2.99\nItem B  $5.49\nTotal   $8.48",
  "Lines":[
    {"Text":"Walmart","BoundingBox":{"X":10,"Y":15,"Width":200,"Height":30}},
    {"Text":"123 Main St","BoundingBox":{"X":10,"Y":50,"Width":180,"Height":25}},
    {"Text":"Item A  $2.99","BoundingBox":{"X":10,"Y":85,"Width":210,"Height":28}},
    {"Text":"Item B  $5.49","BoundingBox":{"X":10,"Y":120,"Width":210,"Height":28}},
    {"Text":"Total   $8.48","BoundingBox":{"X":10,"Y":155,"Width":210,"Height":30}}
  ],
  "Words":[
    {"Text":"Walmart","Confidence":0.99,"BoundingBox":{...}},
    …
  ]
}
```

**Co dalej?**  
Przeanalizuj tablicę `Lines`, aby wyodrębnić kwotę `Total`, albo przekaż JSON do downstreamowego serwisu, który zapisuje wpisy wydatków. Ponieważ wynik jest już w formacie JSON, możesz go podłączyć bezpośrednio do dowolnej bazy NoSQL, Azure Function czy przepływu Power Automate.

---

## Krok 5 – Obsługa typowych przypadków brzegowych

Nawet najlepsze silniki OCR potykają się o pewne problemy. Poniżej znajdziesz scenariusze, które możesz napotkać, ucząc się **how to read receipt**.

| Sytuacja | Rozwiązanie / Rekomendacja |
|-----------|----------------------|
| **Paragon o niskiej rozdzielczości (≤ 150 dpi)** | Najpierw zwiększ rozdzielczość obrazu przy użyciu `Bitmap` i `Graphics` (`InterpolationMode.HighQualityBicubic`). |
| **Obrócony lub pochyły paragon** | Pozostaw `DetectOrientation = true`. W przypadku silnego pochylenia, wstępnie przetwórz obraz metodą `Image.RotateFlip` lub użyj biblioteki trzeciej strony, takiej jak OpenCV. |
| **Kolorowe tło (np. paragon na stole)** | Przekonwertuj na skalę szarości i zwiększ kontrast przed OCR (`ImageAttributes`). |
| **Wiele paragonów na jednym zdjęciu** | Ręcznie wytnij każdy region paragonu lub użyj `ocrEngine.Config.RecognizeMultipleRegions = true`. |
| **Duże pliki powodujące OutOfMemory** | Używaj instrukcji `using`, aby szybko zwalniać obiekty `Image`, lub przetwarzaj w partiach. |

```csharp
// Example: simple grayscale conversion
using (Bitmap bmp = new Bitmap(receiptImage))
{
    for (int y = 0; y < bmp.Height; y++)
        for (int x = 0; x < bmp.Width; x++)
        {
            Color c = bmp.GetPixel(x, y);
            int gray = (int)(c.R * 0.3 + c.G * 0.59 + c.B * 0.11);
            bmp.SetPixel(x, y, Color.FromArgb(gray, gray, gray));
        }
    receiptImage = (Image)bmp.Clone();
}
```

---

## Krok 6 – Pełny działający przykład (Gotowy do kopiowania)

Poniżej znajduje się *kompletny* program, który możesz od razu skompilować. Zawiera wszystkie kroki, właściwe dyrektywy `using` oraz elegancką obsługę błędów.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptReaderDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image file C#
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\receipt.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found: {imagePath}");
                return;
            }

            Image receiptImage;
            try
            {
                receiptImage = Image.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ Failed to load image: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Create and configure OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine
            {
                Config =
                {
                    Language = OcrLanguage.English,
                    DetectOrientation = true
                }
            };

            // -------------------------------------------------
            // 3️⃣ Recognize and convert to JSON
            // -------------------------------------------------
            string jsonResult;
            try
            {
                jsonResult = ocrEngine.RecognizeToJson(receiptImage);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"🛑 OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 4️⃣ Output results
            // -------------------------------------------------
            Console.WriteLine("🗂️ OCR JSON Result:");
            Console.WriteLine(jsonResult);

            // Optionally persist the JSON
            string outputPath = Path.Combine(
                Path.GetDirectoryName(imagePath) ?? ".", "receipt_output.json");
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"✅ JSON saved to {outputPath}");
        }
    }
}
```

**Uruchomienie:**  
`dotnet run` w katalogu projektu. Jeśli wszystko jest poprawnie skonfigurowane, zobaczysz JSON wypisany w konsoli oraz zapisany obok obrazu paragonu.

---

## Zakończenie

Właśnie przeszliśmy przez **how to read receipt** w C# od początku do końca. Ładując obraz, konfigurując Aspose OCR i wywołując `RecognizeToJson`, możesz **extract text from image** i **convert image to JSON** praktycznie bez dodatkowego kodu szkieletowego. Podejście skaluje się — od jednego demo‑paragonu po przetwarzanie setek paragonów w nocy.

Kolejne kroki, które możesz rozważyć:

- **Parsowanie JSON** w celu wyciągnięcia dat, sum i pozycji (użyj `System.Text.Json` lub `Newtonsoft.Json`).  
- **Integracja z bazą danych** (SQL, Cosmos DB) w celu automatycznego zapisywania rekordów wydatków.  
- **Dodanie interfejsu UI** (WinForms, WPF lub Blazor), aby użytkownicy mogli przeciągać i upuszczać paragony.  
- **Zamiana Aspose OCR** na inny silnik (Tesseract, Microsoft Azure OCR), jeśli licencjonowanie jest problemem — zachowaj ten sam wzorzec „load image file C#”.

Eksperymentuj, łam rzeczy, a potem wróć po odświeżenie. Jeśli napotkasz problem, społeczność (oraz fora Aspose) to świetne miejsca, by poprosić o pomoc. Szczęśliwego kodowania i miłego przekształcania papierowych paragonów w czyste, przeszukiwalne dane!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}