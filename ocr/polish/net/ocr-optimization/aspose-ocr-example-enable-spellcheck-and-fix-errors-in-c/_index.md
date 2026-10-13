---
category: general
date: 2026-03-07
description: Przykład Aspose OCR pokazujący, jak włączyć sprawdzanie pisowni, dodać
  własny słownik, wczytać OCR obrazu i szybko naprawić błędy OCR.
draft: false
keywords:
- aspose ocr example
- how to enable spellcheck
- how to add dictionary
- load image ocr
- how to fix ocr errors
language: pl
og_description: Przykład Aspose OCR, który krok po kroku pokazuje, jak włączyć sprawdzanie
  pisowni, dodać własny słownik, załadować obraz do OCR oraz naprawić typowe błędy
  OCR.
og_title: Przykład Aspose OCR – Włącz sprawdzanie pisowni i napraw błędy
tags:
- Aspose
- OCR
- C#
- SpellCheck
title: Przykład Aspose OCR – Włącz sprawdzanie pisowni i napraw błędy w C#
url: /pl/net/ocr-optimization/aspose-ocr-example-enable-spellcheck-and-fix-errors-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Przykład Aspose OCR – Włącz sprawdzanie pisowni i napraw błędy w C#

Czy kiedykolwiek potrzebowałeś **przykładu Aspose OCR**, który nie tylko odczytuje tekst z obrazu, ale także usuwa te uciążliwe błędy ortograficzne? Nie jesteś jedyny. W wielu projektach rzeczywistych surowe wyniki OCR są pełne literówek, szczególnie gdy źródłowy obraz zawiera mało kontrastowe czcionki lub odręczne notatki.  

Dobre wieści? Dzięki Aspose.OCR możesz **włączyć sprawdzanie pisowni**, podłączyć własny słownik i uzyskać dopracowany ciąg znaków w zaledwie kilku linijkach kodu. Poniżej zobaczysz dokładnie **jak włączyć sprawdzanie pisowni**, **jak dodać słownik** oraz **jak załadować obraz OCR**, aby w końcu **naprawić błędy OCR** bez wyrywania sobie włosów.

W tym samouczku omówimy wszystko, czego potrzebujesz — od instalacji NuGet po kompletny, uruchamialny program, który wypisuje poprawiony tekst. Po zakończeniu będziesz mieć solidny **przykład Aspose OCR**, który możesz od razu wstawić do dowolnego projektu .NET.

## Wymagania wstępne

- .NET 6.0 SDK lub nowszy (kod działa również z .NET Core i .NET Framework)
- Visual Studio 2022 lub dowolne IDE kompatybilne z C#
- Plik obrazu (`typed_text.png`) zawierający wyraźny, wydrukowany tekst po angielsku
- Dostęp do Internetu w celu pobrania pakietu NuGet Aspose.OCR

Nie są wymagane żadne inne biblioteki firm trzecich.

---

## Krok 1 – Zainstaluj pakiet NuGet Aspose.OCR (Załaduj obraz OCR)

Zanim będziemy mogli napisać jakikolwiek kod, potrzebujemy biblioteki napędzającej silnik OCR.

```bash
dotnet add package Aspose.OCR
```

> **Porada:** Jeśli używasz Visual Studio, kliknij prawym przyciskiem projektu → *Manage NuGet Packages* → wyszukaj **Aspose.OCR** i naciśnij *Install*.  

Zainstalowanie pakietu daje dostęp do `OcrEngine`, `ImageStream` oraz wbudowanych narzędzi sprawdzania pisowni, które wykorzystamy później. Gdy pakiet jest już zainstalowany, możesz **załadować obraz OCR**.

## Krok 2 – Utwórz instancję silnika OCR

Utworzenie silnika to pierwszy konkretny krok w każdym **przykładzie Aspose OCR**. Traktuj `OcrEngine` jako mózg, który przeanalizuje bitmapę i zwróci tekst.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Step 2: Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

Konstruktor `OcrEngine` nie wymaga żadnych parametrów, co czyni go prostym i schludnym do szybkich prototypów.

## Krok 3 – Jak włączyć sprawdzanie pisowni (i dlaczego ma to znaczenie)

Surowe wyniki OCR często zawierają błędnie rozpoznane słowa, takie jak „teh” zamiast „the”. Włączenie wbudowanego sprawdzania pisowni pozwala Aspose automatycznie zamienić te błędy na najbardziej prawdopodobną poprawną pisownię.

```csharp
// Step 3: Turn on spell checking and set the language to English
ocrEngine.Settings.SpellCheck.Enabled = true;
ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;
```

> **Dlaczego włączyć sprawdzanie pisowni?**  
> - **Dokładność:** Sprawdzanie pisowni w post‑procesie może zwiększyć ogólną dokładność tekstu o 10‑15 % w przypadku dokumentów drukowanych.  
> - **Doświadczenie użytkownika:** Czysty tekst oznacza mniej dodatkowego czyszczenia, gdy przekazujesz wynik do indeksów wyszukiwania lub potoków analitycznych.

## Krok 4 – Jak dodać słownik (niestandardowe słowa)

Czasami domyślny słownik nie zna nazw Twoich marek, kodów produktów ani żargonu specyficznego dla domeny. Wtedy przydaje się **dodawanie słownika**.

```csharp
// Step 4: Add custom words that the spell checker should accept
ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
{
    "AsposeOCR",   // our library name
    "OCRify",      // a fictional product
    "CSharpify"    // another custom term
});
```

Możesz podać tablicę, listę lub nawet odczytać z pliku, jeśli masz duży niestandardowy zasób słownictwa. Sprawdzanie pisowni będzie teraz traktować te wpisy jako prawidłowe, zapobiegając błędnym korektom.

## Krok 5 – Załaduj obraz do OCR (Załaduj obraz OCR)

Teraz, gdy silnik jest skonfigurowany, musimy skierować go na obraz, który chcemy odczytać. Pomocnicza metoda `ImageStream.FromFile` ukrywa szczegóły odczytu pliku.

```csharp
// Step 5: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");
```

> **Wskazówka:** Jeśli Twój obraz znajduje się w podfolderze projektu, ustaw jego właściwość *Copy to Output Directory* na *Copy always*, aby ścieżka była prawidłowo rozwiązywana w czasie wykonywania.

## Krok 6 – Wykonaj rozpoznawanie i napraw błędy OCR

Gdy wszystko jest gotowe, pojedyncze wywołanie `Recognize()` uruchamia potok OCR, stosuje sprawdzanie pisowni i zapisuje oczyszczony wynik w `ocrEngine.Text`.

```csharp
// Step 6: Run OCR and let the spell checker clean the output
ocrEngine.Recognize();

// Step 7: Output the corrected text to the console
Console.WriteLine("Corrected text:");
Console.WriteLine(ocrEngine.Text);
```

### Oczekiwany wynik

Zakładając, że `typed_text.png` zawiera zdanie `The quick brown fox jumps over teh lazy dog`, konsola wyświetli:

```
Corrected text:
The quick brown fox jumps over the lazy dog
```

Zauważ, że „teh” zostało automatycznie poprawione na „the”. Gdybyś dodał „OCRify” do niestandardowego słownika i obraz zawierał to słowo, silnik pozostawiłby je niezmienione.

---

## Pełny działający przykład (gotowy do kopiowania i wklejania)

Poniżej znajduje się kompletny program, który możesz wkleić do nowego projektu konsolowego. Zawiera wszystkie powyższe kroki oraz kilka komentarzy dla przejrzystości.

```csharp
// ---------------------------------------------------------------
// Aspose OCR Example – Enable Spellcheck and Fix Errors
// ---------------------------------------------------------------

using System;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable spell checking (how to enable spellcheck)
            ocrEngine.Settings.SpellCheck.Enabled = true;
            ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;

            // 3️⃣ Add custom words (how to add dictionary)
            ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
            {
                "AsposeOCR",
                "OCRify",
                "CSharpify"
            });

            // 4️⃣ Load the image (load image OCR)
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");

            // 5️⃣ Run OCR – this also fixes common OCR errors (how to fix ocr errors)
            ocrEngine.Recognize();

            // 6️⃣ Show the corrected result
            Console.WriteLine("Corrected text:");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

Zapisz to jako `Program.cs`, uruchom `dotnet run` i powinieneś zobaczyć poprawione zdanie wypisane w konsoli.

---

## Najczęściej zadawane pytania i przypadki brzegowe

| Question | Answer |
|----------|--------|
| **Co jeśli obraz jest wielostronicowym PDF?** | Aspose.OCR może obsługiwać strony PDF jako obrazy. Użyj `ocrEngine.Image = ImageStream.FromPdf("file.pdf", pageNumber: 1);` i iteruj po stronach. |
| **Czy mogę zmienić język na inny niż angielski?** | Oczywiście. Ustaw `ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.French;` (lub dowolny obsługiwany język). |
| **Mój niestandardowy słownik jest ogromny — czy wpłynie to na wydajność?** | Dodanie tysięcy słów powoduje niewielki koszt początkowy, ale wyszukiwanie jest O(1) dzięki zastosowaniu zestawu hash pod maską. W przypadku bardzo dużych słowników rozważ ich wczytanie raz przy uruchomieniu aplikacji. |
| **Co jeśli silnik OCR zgłosi wyjątek przy uszkodzonym obrazie?** | Otocz `Recognize()` blokiem try‑catch i sprawdź `ocrEngine.LastError`. Możesz także wstępnie zweryfikować wymiary obrazu przy użyciu `ocrEngine.Image.Width` i `Height`. |
| **Czy potrzebuję licencji do użytku produkcyjnego?** | Darmowa wersja ewaluacyjna działa do testów, ale licencja komercyjna usuwa znak wodny ewaluacji i odblokowuje pełną wydajność. |

---

## Zakończenie

Masz teraz **kompletny przykład Aspose OCR**, który pokazuje **jak włączyć sprawdzanie pisowni**, **jak dodać słownik**, **załadować obraz OCR** oraz **jak naprawić błędy OCR** w czysty, gotowy do produkcji sposób. Konfigurując sprawdzanie pisowni i podając własną listę słów, znacząco poprawiasz jakość wyodrębnionego tekstu bez konieczności pisania własnej logiki post‑procesingu.

Gotowy na kolejny krok? Spróbuj zmienić język na hiszpański, podać wielostronicowy PDF lub zintegrować wynik z przeszukiwalnym indeksem Azure Cognitive Search. Ten sam schemat ma zastosowanie — wystarczy dostosować flagę języka i ewentualnie rozszerzyć niestandardowy słownik.

Jeśli ten przewodnik okazał się przydatny, wystaw mu gwiazdkę na GitHubie, podziel się nim z zespołem lub zostaw komentarz poniżej. Szczęśliwego kodowania i niech wyniki OCR zawsze będą wolne od błędów!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}