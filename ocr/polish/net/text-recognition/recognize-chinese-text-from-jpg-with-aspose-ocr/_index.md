---
category: general
date: 2026-04-08
description: Dowiedz się, jak rozpoznawać chiński tekst z obrazów JPG przy użyciu
  Aspose OCR. Ten przewodnik krok po kroku pokaże Ci również, jak szybko wyodrębnić
  tekst z obrazu.
draft: false
keywords:
- recognize chinese text
- extract text from image
- recognize text from jpg
- Aspose OCR C#
- offline OCR resources
language: pl
og_description: rozpoznawaj chiński tekst z obrazów JPG przy użyciu Aspose OCR. Postępuj
  zgodnie z tym kompletnym przewodnikiem, aby wyodrębnić tekst z obrazu offline.
og_title: rozpoznaj chiński tekst z JPG przy użyciu Aspose OCR
tags:
- OCR
- C#
- Aspose
title: Rozpoznaj chiński tekst z JPG za pomocą Aspose OCR
url: /pl/net/text-recognition/recognize-chinese-text-from-jpg-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznawanie chińskiego tekstu z JPG przy użyciu Aspose OCR

Czy kiedykolwiek potrzebowałeś **rozpoznać chiński tekst** z pliku JPG, ale nie wiedziałeś, od czego zacząć? Nie jesteś sam — wielu programistów napotyka ten problem przy tworzeniu wielojęzycznych aplikacji skanujących. Dobrą wiadomością jest to, że Aspose OCR czyni to dziecinnie prostym, nawet gdy musisz pracować offline.

W tym samouczku przeprowadzimy Cię przez cały proces wyodrębniania tekstu z obrazu, w stylu **extract text from image**, i pokażemy dokładnie, jak **rozpoznać tekst z jpg** przy użyciu C#. Po zakończeniu będziesz mieć działający program, który odczytuje obraz w języku chińskim i wypisuje rozpoznane znaki w konsoli.

## Czego będziesz potrzebować

- .NET 6.0 lub nowszy (dowolna aktualna wersja działa)
- Pakiet NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Plik zasobów języka chińskiego (samouczek pokazuje, jak załadować go offline)
- Plik obrazu o nazwie `chinese_sample.jpg` umieszczony w folderze, którym zarządzasz

Nie potrzebujesz żadnych sztuczek w IDE — Visual Studio, Rider, czy nawet VS Code wystarczą.

## Krok 1: Skonfiguruj projekt i zainstaluj Aspose OCR

Najpierw utwórz nowy projekt konsolowy i dodaj bibliotekę Aspose OCR.

```bash
dotnet new console -n ChineseOcrDemo
cd ChineseOcrDemo
dotnet add package Aspose.OCR
```

> **Wskazówka:** Jeśli pracujesz za korporacyjnym proxy, dodaj flagę `--no-cache`, aby wymusić pobranie najnowszej wersji.

## Krok 2: Wyłącz automatyczne pobieranie zasobów

Aspose OCR może pobierać pakiety językowe w locie, ale w produkcji zazwyczaj chcesz dostarczyć pliki razem z aplikacją. Wyłączenie automatycznego pobierania zapobiega nieoczekiwanym wywołaniom sieciowym.

```csharp
using Aspose.Ocr;

// Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Turn off the auto‑download feature
ocrEngine.Options.EnableAutomaticResourceDownload = false;
```

Dlaczego to robimy? Przechowywanie zasobów lokalnie zapewnia spójną wydajność i pozwala uruchamiać aplikację na maszynach bez dostępu do Internetu.

## Krok 3: Załaduj zasoby języka chińskiego offline

Aspose dostarcza dane językowe jako osobne pliki. Zakładając, że umieściłeś chiński pakiet (`zh`) w folderze `Resources` obok swojego pliku wykonywalnego, załaduj go w ten sposób:

```csharp
// Path to the folder that contains the language files
string resourcePath = Path.Combine(AppContext.BaseDirectory, "Resources");

// Tell the engine where to look for resources
ocrEngine.Options.ResourcesFolder = resourcePath;

// Load the Simplified Chinese resources (offline = true)
ocrEngine.LoadLanguageResources("zh", offline: true);
```

> **Uwaga:** Jeśli ścieżka jest nieprawidłowa, otrzymasz `FileNotFoundException`. Sprawdź dokładnie nazwę folderu i uwzględnij wielkość liter w systemie Linux.

## Krok 4: Ustaw język silnika na chiński

Teraz, gdy dane są załadowane, skieruj silnik na właściwy kod języka.

```csharp
ocrEngine.Language = "zh"; // “zh” = Simplified Chinese
```

Ustawienie języka explicite zwiększa dokładność, ponieważ OCR nie będzie tracić czasu na zgadywanie skryptów.

## Krok 5: Rozpoznaj tekst z obrazu JPG

Oto sedno samouczka — podanie obrazu JPG do silnika i wyciągnięcie tekstu.

```csharp
// Full path to the image you want to process
string imagePath = Path.Combine(AppContext.BaseDirectory, "chinese_sample.jpg");

// Run the OCR operation
OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

// Output the raw result
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

Jeśli wszystko przebiegło pomyślnie, konsola wyświetli chińskie znaki, które znajdowały się w `chinese_sample.jpg`. Możesz także odczytać `ocrResult.Confidence`, aby uzyskać miarę jakości.

## Krok 6: Pełny działający przykład

Połączenie wszystkich elementów daje gotowy do uruchomienia program. Zapisz to jako `Program.cs` w folderze projektu.

```csharp
using System;
using System.IO;
using Aspose.Ocr;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // 2️⃣ Disable automatic resource download
        // -------------------------------------------------
        ocrEngine.Options.EnableAutomaticResourceDownload = false;

        // -------------------------------------------------
        // 3️⃣ Load Chinese language resources (offline)
        // -------------------------------------------------
        string resourcePath = Path.Combine(AppContext.BaseDirectory, "Resources");
        ocrEngine.Options.ResourcesFolder = resourcePath;
        ocrEngine.LoadLanguageResources("zh", offline: true);

        // -------------------------------------------------
        // 4️⃣ Set language to Simplified Chinese
        // -------------------------------------------------
        ocrEngine.Language = "zh";

        // -------------------------------------------------
        // 5️⃣ Recognize text from a JPG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppContext.BaseDirectory, "chinese_sample.jpg");
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // -------------------------------------------------
        // 6️⃣ Show the result
        // -------------------------------------------------
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine($"\nConfidence: {ocrResult.Confidence:P2}");
    }
}
```

### Oczekiwany wynik

```
=== Recognized Chinese Text ===
欢迎使用Aspose OCR示例
Confidence: 96.45%
```

Twoje dokładne wyjście będzie zależało od obrazu źródłowego, ale powinieneś zobaczyć blok chińskich znaków oraz procent pewności.

## Krok 7: Typowe wariacje i przypadki brzegowe

### Rozpoznawanie tekstu z PNG lub BMP

Metoda `RecognizeImage` akceptuje każdy format obsługiwany przez `System.Drawing` w .NET. Wystarczy zmienić rozszerzenie pliku:

```csharp
ocrEngine.RecognizeImage("sample.png");
```

### Obsługa wielu języków

Jeśli musisz **wyodrębnić tekst z obrazu**, który miesza angielski i chiński, załaduj oba pakiety językowe i ustaw `ocrEngine.Language = "zh,en";`. Silnik automatycznie przełączy się między skryptami.

### Radzenie sobie z obrazami o niskiej rozdzielczości

Niskie DPI może znacznie obniżyć dokładność OCR. Przed wywołaniem `RecognizeImage` możesz zwiększyć rozmiar obrazu:

```csharp
using System.Drawing;

Bitmap bmp = new Bitmap(imagePath);
Bitmap highRes = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
highRes.Save("highres.jpg");
ocrResult = ocrEngine.RecognizeImage("highres.jpg");
```

Pamiętaj, że zwiększanie rozmiaru nie doda magicznie szczegółów, ale może dać algorytmowi więcej pikseli do pracy.

## Krok 8: Testowanie i weryfikacja

Szybkie sprawdzenie to porównanie wyniku OCR z znanym ciągiem referencyjnym.

```csharp
string expected = "欢迎使用Aspose OCR示例";
bool matches = ocrResult.Text.Trim() == expected;
Console.WriteLine($"Match with expected? {matches}");
```

Jeśli `matches` jest `false`, rozważ dostosowanie obrazu (np. zwiększenie kontrastu) lub włączenie `ocrEngine.Options.UseAdvancedPreprocessing = true`.

## Zakończenie

Właśnie nauczyłeś się, jak **rozpoznać chiński tekst** z pliku JPG przy użyciu Aspose OCR, i teraz wiesz, jak **wyodrębnić tekst z obrazu** w pełni offline. Kompletny zestaw — inicjalizacja, ładowanie zasobów, wybór języka i przetwarzanie obrazu — mieści się w jednej, łatwej do uruchomienia aplikacji konsolowej.

Co dalej? Spróbuj przetworzyć partię obrazów tym samym silnikiem, eksperymentuj z różnymi pakietami językowymi lub zintegrować krok OCR z ASP .NET Web API, aby użytkownicy mogli przesyłać zdjęcia i otrzymywać przetłumaczony tekst w czasie rzeczywistym. Nie ma ograniczeń, gdy połączysz niezawodny OCR z nowoczesnymi narzędziami .NET.

Miłego kodowania i śmiało zostaw komentarz, jeśli napotkasz jakiekolwiek problemy!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}