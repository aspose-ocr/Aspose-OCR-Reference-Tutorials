---
category: general
date: 2026-02-09
description: Wyodrębnij tekst z obrazu przy użyciu offline OCR w C#. Kompletny przykład
  OCR w C# pokazuje, jak załadować obraz do OCR, rozpoznać tekst cyrylicą i wyodrębnić
  tekst z paszportu.
draft: false
keywords:
- extract text from image
- c# ocr example
- load image for ocr
- recognize cyrillic text
- recognize text from passport
language: pl
og_description: Wyodrębnij tekst z obrazu za pomocą offline OCR w C#. Poznaj krok
  po kroku przykład OCR w C#, który ładuje obraz do OCR, rozpoznaje tekst cyrylicą
  i wyodrębnia tekst z paszportu.
og_title: Wyodrębnianie tekstu z obrazu w C# – Przewodnik po OCR offline
tags:
- OCR
- C#
- Aspose
title: Wyodrębnianie tekstu z obrazu w C# – Przykład OCR offline
url: /pl/net/text-recognition/extract-text-from-image-in-c-offline-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tekstu z obrazu w C# – Przykład OCR offline

Kiedykolwiek potrzebowałeś **wyodrębnić tekst z obrazu**, ale utknąłeś przy zależnych od sieci API? Nie jesteś sam. Wielu programistów napotyka problem, gdy usługa OCR próbuje pobrać pakiety językowe w czasie działania, szczególnie w środowiskach o ograniczonym dostępie.

W tym przewodniku przeprowadzimy Cię przez **przykład c# ocr**, który działa w pełni offline, wczytuje obraz do OCR i rozpoznaje tekst cyrylicą z paszportu. Po zakończeniu będziesz mieć gotowy do uruchomienia program, który wypisuje zawartość tekstową dowolnego obsługiwanego obrazu bezpośrednio w konsoli.

## Czego się nauczysz

- Jak skonfigurować Aspose.OCR do przetwarzania offline.  
- Dokładny kod do **wczytania obrazu do OCR** z dysku.  
- Jak skonfigurować silnik do **rozpoznawania tekstu cyrylicą**.  
- Pełny, gotowy do skopiowania **przykład c# ocr**, który wyodrębnia tekst ze zdjęcia w stylu paszportu.  

Nie wymagana jest wcześniejsza znajomość Aspose; wystarczy .NET 6 (lub nowszy) SDK oraz Visual Studio 2022 (lub VS Code).

---

![Wyodrębnij tekst z obrazu przy użyciu Aspose OCR na zdjęciu paszportowym](/images/ocr-passport.jpg "wyodrębnij tekst z obrazu")

## Krok 1: Skonfiguruj projekt do wyodrębniania tekstu z obrazu

Zanim napiszesz jakikolwiek kod, upewnij się, że pakiet NuGet Aspose.OCR został dodany do Twojego projektu:

```bash
dotnet add package Aspose.OCR
```

> **Wskazówka:** Użyj flagi `--version`, aby zablokować najnowszą stabilną wersję (np. `13.9.0`). Zapewnia to kompatybilność z .NET 6.

Utworzenie nowej aplikacji konsolowej jest tak proste:

```bash
dotnet new console -n OfflineOcrDemo
cd OfflineOcrDemo
```

Teraz masz czystą bazę, w której **wyodrębnimy tekst z obrazu** bez potrzeby łączenia się z internetem.

## Krok 2: Wczytaj obraz do OCR – odczyt zdjęcia paszportowego

Pierwszą rzeczą, której potrzebuje silnik OCR, jest bitmapa lub strumień reprezentujący obraz. W naszym scenariuszu **wczytamy obraz do OCR** z lokalnego pliku o nazwie `cyrillic_passport.jpg`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 2: Load the image file (this is the “load image for ocr” part)
var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

// Validate the file exists – helpful when the path is wrong.
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// ImageStream abstracts the underlying format; it works with JPEG, PNG, etc.
var image = ImageStream.FromFile(imagePath);
```

> **Dlaczego to ważne:** Dostarczenie strumienia zamiast surowego `Bitmap` pozwala Aspose samodzielnie wykrywać format, co redukuje kod szablonowy i potencjalne błędy.

## Krok 3: Skonfiguruj tryb offline i wybierz język cyrylica

Aspose.OCR może pobierać modele językowe w locie, ale to podważa sens rozwiązania offline. Wyłącz wywołania sieciowe i wyraźnie poinformuj silnik, którego języka ma używać.

```csharp
// Step 3: Create the OCR engine and switch to offline mode
var ocrEngine = new OcrEngine
{
    Configuration =
    {
        OfflineMode = true,               // No network traffic – perfect for secure environments
        Language = new[] { OcrLanguage.Cyrillic } // We want to **recognize cyrillic text**
    }
};
```

> **Przypadek brzegowy:** Jeśli później będziesz potrzebował rozpoznawać znaki łacińskie w tym samym dokumencie, po prostu dodaj `OcrLanguage.English` do tablicy. Silnik automatycznie obsłuży wykrywanie wielu języków.

## Krok 4: Uruchom silnik OCR i rozpoznaj tekst cyrylicą

Teraz faktycznie **rozpoznajemy tekst ze zdjęć w stylu paszportu**. Metoda `Recognize` zwraca rozbudowany obiekt wyniku zawierający czysty tekst, oceny pewności oraz ramki ograniczające.

```csharp
// Step 4: Perform the OCR operation
OcrResult result = ocrEngine.Recognize(image);

// Step 5: Output the plain text – this is where we finally **extract text from image**
Console.WriteLine("📝 Extracted Text:");
Console.WriteLine("-------------------");
Console.WriteLine(result.PlainText);
```

### Oczekiwany wynik w konsoli

```
📝 Extracted Text:
-------------------
ПАСПОРТ РФ
Иванов Иван Иванович
01.01.1990
...
```

Jeśli wynik wygląda na zniekształcony, sprawdź ponownie, czy obraz źródłowy jest wyraźny oraz czy pakiet językowy `OfflineMode` dla cyrylicy znajduje się w folderze instalacyjnym Aspose (zwykle `\Aspose.OCR\resources\languages`).

## Pełny przykład C# OCR – kompletny kod źródłowy

Poniżej znajduje się pełny **przykład c# ocr**. Skopiuj i wklej go do `Program.cs` i uruchom `dotnet run`. Wszystko, czego potrzebujesz do **wyodrębniania tekstu z obrazu**, znajduje się tutaj.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class OfflineExample
{
    static void Main()
    {
        // --------------------------------------------------------------
        // Step 1: Create the OCR engine (offline mode)
        // --------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Configuration =
            {
                OfflineMode = true,                     // No network calls
                Language = new[] { OcrLanguage.Cyrillic } // Recognize Cyrillic text
            }
        };

        // --------------------------------------------------------------
        // Step 2: Load the image for OCR (passport photo)
        // --------------------------------------------------------------
        var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ Image not found at {imagePath}");
            return;
        }

        var image = ImageStream.FromFile(imagePath);

        // --------------------------------------------------------------
        // Step 3: Recognize the text
        // --------------------------------------------------------------
        var result = ocrEngine.Recognize(image);

        // --------------------------------------------------------------
        // Step 4: Output the plain text (the final extraction)
        // --------------------------------------------------------------
        Console.WriteLine("📝 Extracted Text:");
        Console.WriteLine("-------------------");
        Console.WriteLine(result.PlainText);
    }
}
```

### Uruchamianie przykładu

```bash
dotnet run
```

Powinieneś zobaczyć, że konsola wypisuje dane paszportowe w cyrylicy. To moment, w którym wiesz, że Twój pipeline **wyodrębniania tekstu z obrazu** działa.

## Typowe problemy i jak je naprawić

| Objaw | Prawdopodobna przyczyna | Rozwiązanie |
|-------|--------------------------|-------------|
| Pusty `PlainText` | Nieprawidłowy model językowy lub obraz zbyt ciemny | Upewnij się, że język w `OfflineMode` zawiera `Cyrillic` i zwiększ kontrast obrazu |
| `System.DllNotFoundException` | Brak natywnych plików binarnych Aspose OCR | Ponownie zainstaluj pakiet NuGet lub skopiuj `Aspose.OCR.Native.dll` do folderu wyjściowego |
| Wolna wydajność przy dużych obrazach | Silnik przetwarza pełną rozdzielczość | Zmniejsz rozmiar obrazu do ≤ 1500 px szerokości przed przekazaniem go do `ImageStream` |
| Zniekształcone znaki | Obraz obrócony niepoprawnie | Użyj `Image.RotateFlip(RotateFlipType.Rotate90FlipNone)` przed utworzeniem strumienia |

## Kolejne kroki – Rozszerzanie przepływu OCR offline

- **Wczytaj obraz do OCR** z `MemoryStream` przy obsłudze przesłanych plików w ASP.NET Core.  
- Przejdź do **rozpoznawania tekstu z paszportu** w trybie wsadowym, iterując po folderze skanów paszportów.  
- Połącz wynik z **wyrażeniami regularnymi**, aby wyodrębnić pola takie jak numer paszportu czy data urodzenia.  
- Eksperymentuj z `ocrEngine.Configuration.UseParallelProcessing = true` dla przyspieszeń wielordzeniowych.

---

### Podsumowanie

Właśnie pokazaliśmy, jak **wyodrębnić tekst z obrazu** przy użyciu w pełni offline pipeline OCR w C#. Krótki, samodzielny **przykład c# ocr** wczytuje obraz, konfiguruje silnik do **rozpoznawania tekstu cyrylicą** i wypisuje wyodrębnione dane paszportowe — wszystko bez żadnych żądań sieciowych.

Śmiało modyfikuj kod, dodawaj kolejne języki lub podłącz wynik do bazy danych. Nie ma ograniczeń, gdy opanujesz podstawy wczytywania obrazu do OCR i rozpoznawania tekstu ze zdjęcia w stylu paszportu.

Masz pytania lub chcesz podzielić się własnymi modyfikacjami? zostaw komentarz poniżej i powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}