---
category: general
date: 2026-02-09
description: Szybko wyodrębniaj tekst z obrazów w C#, ustawiając maksymalny stopień
  równoległości dla wsadowego OCR – dowiedz się, jak konwertować zeskanowane strony,
  obsługiwać OCR wielu obrazów i efektywnie odczytywać tekst z plików PNG.
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: pl
og_description: wyodrębniaj tekst z obrazów w C# ustawiając maksymalny stopień równoległości.
  Ten samouczek pokazuje, jak konwertować zeskanowane strony, uruchamiać wielokrotne
  OCR obrazów i odczytywać tekst z plików PNG przy użyciu Aspose OCR.
og_title: Wyodrębniaj tekst z obrazów PNG w C# – Kompletny przewodnik po wsadowym
  OCR
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: Wyodrębnianie tekstu z obrazów PNG w C# – wsadowe OCR przy użyciu Aspose OCR
url: /pl/net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

ensure we didn't miss any markdown links. There are none besides maybe code placeholders. No URLs.

Check for any other formatting like bold, etc. Keep bold.

Now produce final output with all content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# wyodrębnianie tekstu z obrazów PNG w C# – Batch OCR przy użyciu Aspose OCR

Czy kiedykolwiek potrzebowałeś **wyodrębnić tekst z obrazów** z folderu zeskanowanych PNG, ale utknąłeś przy pytaniu „jak to przyspieszyć?”? Nie jesteś sam. W wielu rzeczywistych projektach programiści muszą **ustawiać maksymalny stopień równoległości**, aby dziesiątki stron były przetwarzane w sekundach zamiast minut.  

W tym przewodniku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który **konwertuje zeskanowane strony**, wykonuje **OCR na wielu obrazach**, i w końcu **odczytuje tekst z PNG** bez wysiłku. Bez niejasnych odnośników „zobacz dokumentację” — tylko kod, który możesz skopiować‑wkleić, wyjaśnienia, dlaczego każda linia ma znaczenie, oraz wskazówki, jak uniknąć typowych pułapek.

> **Pro tip:** Jeśli już używasz Aspose OCR w innym miejscu, zauważysz, że ta sama klasa `OcrEngine` pojawia się tutaj, ale dostosujemy jej konfigurację do prawdziwego przetwarzania równoległego.

---

## Czego będziesz potrzebować

- **.NET 6+** (lub .NET Framework 4.6+). API działa tak samo, ale nowsze środowiska uruchomieniowe zapewniają lepsze zarządzanie wątkami.  
- **Aspose.OCR for .NET** – zainstaluj przez NuGet: `Install-Package Aspose.OCR`.  
- Folder zawierający kilka skanów PNG (`page1.png`, `page2.png`, …).  
- IDE lub edytor, z którym czujesz się komfortowo (Visual Studio, Rider, VS Code…).

To wszystko. Bez dodatkowych usług, bez kluczy do chmury, tylko czyste przetwarzanie lokalne.

---

## wyodrębnianie tekstu z obrazów – Ustawianie maksymalnej równoległości dla Batch OCR

Kiedy uruchamiasz OCR na kilku plikach, silnik domyślnie używa jednego wątku. To jest bezpieczne, ale wyjątkowo wolne. Konfigurując `MaxDegreeOfParallelism`, informujesz silnik, ile wątków może uruchomić jednocześnie.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**Dlaczego 4?**  
Cztery to optymalny punkt na większości nowoczesnych laptopów — wystarczająca liczba rdzeni, aby CPU było zajęte, ale nie tak wiele, by deprywować inne procesy. Jeśli uruchamiasz to na serwerze z 16 rdzeniami, zwiększ liczbę do 12 lub 14, aby zauważalnie przyspieszyć.

---

## Konwertowanie zeskanowanych stron – Tworzenie kolekcji Image Stream

Aspose oczekuje każdy obraz jako `ImageStream`. Pomocnicza metoda `FromFile` odczytuje plik, przechowuje go w pamięci i przekazuje silnikowi OCR. Możesz również podać `MemoryStream`, jeśli obrazy pochodzą z bazy danych lub odpowiedzi HTTP.

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**Przypadek brzegowy:** Jeśli którykolwiek plik jest brakujący lub uszkodzony, `FromFile` rzuci `FileNotFoundException`. Owiń konstrukcję w `try/catch`, jeśli spodziewasz się niepewnego wejścia.

---

## OCR wielu obrazów – Wykonywanie Batch OCR

Teraz odbywa się najcięższa praca. `RecognizeBatch` uruchamia do liczby wątków, którą ustawiłeś wcześniej, przetwarza każdy obraz i zwraca listę obiektów `OcrResult`.

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

Za kulisami każdy wątek ładuje swój obraz, uruchamia sieć neuronową i wyodrębnia zwykły tekst. Kolejność wyników odpowiada kolejności listy wejściowej, więc możesz bezpiecznie mapować strona 1 → wynik 0 i tak dalej.

---

## odczytywanie tekstu PNG – Wyświetlanie wyodrębnionej zawartości

Na koniec iterujemy wyniki i wypisujemy zwykły tekst na konsolę. To miejsce, w którym możesz przekierować wyjście do pliku, bazy danych lub nawet dalszej usługi NLP.

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### Oczekiwany wynik w konsoli

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

Jeśli zobaczysz puste sekcje, sprawdź ponownie, czy PNG nie są czystymi białymi obrazami — OCR potrzebuje pewnego kontrastu.

---

## Praktyczne wskazówki i typowe pułapki

| Sytuacja | Co zrobić |
|-----------|------------|
| **Presja pamięci** przy dużych partiach | Przetwarzaj obrazy w partiach po 10‑20 plików, a następnie wywołaj `GC.Collect()`, jeśli zauważysz skoki. |
| **Nieprawidłowe wykrywanie języka** | Ustaw `ocrEngine.Configuration.Language = OcrLanguage.English;` (lub wybrany język) przed wywołaniem `RecognizeBatch`. |
| **Wolna wydajność pomimo równoległości** | Sprawdź, czy Twój SSD nie ogranicza I/O; najpierw wczytaj wszystkie pliki do pamięci (tak jak robimy to za pomocą `ImageStream.FromFile`). |
| **Brakujące znaki** | Zwiększ `ocrEngine.Configuration.DPI = 300;` dla przetwarzania w wyższej rozdzielczości. |

---

## Rozszerzanie przykładu – Z PNG do PDF lub DOCX

Jeśli ostatecznie będziesz potrzebował **konwertować zeskanowane strony** na przeszukiwalne PDF‑y, po prostu przekaż `ocrResults[i].PlainText` do biblioteki PDF (np. Aspose.PDF) i nałóż tekst jako niewidoczną warstwę. Ten sam trik z równoległością działa tam również.

---

## Pełny kod źródłowy (gotowy do kopiowania‑wklejania)

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

Zapisz to jako `BatchExample.cs`, uruchom `dotnet run` i obserwuj, jak Twoja konsola wypełnia się tekstem, który wcześniej był ukryty w tych skanach PNG.

---

## Podsumowanie wizualne

![extract text images example](images/ocr-batch.png){alt="przykład wyodrębniania tekstu z obrazów"}

Diagram przedstawia przepływ: **Pliki PNG → kolekcja ImageStream → OcrEngine (maksymalna równoległość) → wyniki OCR → Konsola / dalsze przechowywanie**.

---

## Zakończenie

Masz teraz solidny, kompleksowy przepis, jak **wyodrębniać tekst z obrazów** w C# przy **ustawianiu maksymalnej równoległości**, **konwertowaniu zeskanowanych stron**, obsłudze **OCR wielu obrazów** oraz **odczytywaniu tekstu PNG** efektywnie. Kod jest samodzielny, wyjaśnienia obejmują zarówno „jak”, jak i „dlaczego”, a wskazówki chronią przed typowymi problemami.

Co dalej? Spróbuj zamienić listę PNG na dynamiczną pętlę `Directory.GetFiles`, eksperymentuj z różnymi liczbami wątków lub przekieruj wynik do przeszukiwalnego PDF‑a. Ten sam wzorzec skaluje się do setek stron przy zaledwie jednej dodatkowej linii kodu.

Masz pytania lub trudny przypadek brzegowy? zostaw komentarz poniżej i szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}