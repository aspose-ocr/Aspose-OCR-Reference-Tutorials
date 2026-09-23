---
category: general
date: 2026-01-15
description: Dowiedz się, jak rozpoznawać tekst arabski i rozpoznawać tekst hindi
  przy użyciu Aspose OCR. Ten przewodnik krok po kroku pokazuje, jak wydobywać tekst
  z obrazu i efektywnie konwertować obraz na tekst.
draft: false
keywords:
- how to ocr arabic
- recognize arabic text
- extract text from image
- convert image to text
- recognize hindi text
language: pl
og_description: jak przeprowadzić OCR arabskiego tekstu i rozpoznać tekst hindi w
  jednym programie C#. Skorzystaj z tego kompletniego przewodnika, aby wyodrębnić
  tekst z obrazu i przekształcić obraz w tekst.
og_title: jak wykonać OCR arabskiego i hindi tekstu przy użyciu Aspose OCR
tags:
- Aspose OCR
- C#
- Multilingual OCR
title: jak wykonać OCR arabskiego i hindi tekstu przy użyciu Aspose OCR
url: /pl/net/text-recognition/how-to-ocr-arabic-and-hindi-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak wykonać OCR arabskiego i hindi przy użyciu Aspose OCR

Zastanawiałeś się kiedyś **jak wykonać OCR arabskich** znaków, które czytane są od prawej do lewej, a jednocześnie wyodrębnić hinduskie glify z paragonu? Nie jesteś sam. Wielu programistów napotyka ten sam problem, gdy muszą **rozpoznawać tekst arabski** i **rozpoznawać tekst hindi** w tym samym procesie.  

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład w C#, który pokazuje, jak **wyodrębnić tekst z plików obrazu**, **konwertować obraz na tekst** oraz obsłużyć zarówno skrypty arabskie, jak i hindi przy użyciu Aspose OCR. Bez niejasnych odwołań — tylko kod, który możesz skopiować‑wkleić, oraz wyjaśnienie każdego wiersza.

> **Pro tip:** Jeśli nigdy nie używałeś Aspose OCR, najpierw zainstaluj pakiet NuGet `Aspose.OCR`. To jednorazowa operacja w Visual Studio, a pakiet pobiera wszystkie niezbędne natywne pliki binarne potrzebne do rozpoznawania na CPU.

---

![jak wykonać OCR arabskiego przykład](/images/arabic-ocr-sample.png "jak wykonać OCR arabskiego – przykładowy znak arabski")

*Image alt text:* **jak wykonać OCR arabskiego – przykładowy znak arabski**  

---

## jak wykonać OCR arabskiego – przygotowanie środowiska

Zanim przejdziemy do kodu, upewnijmy się, że środowisko programistyczne jest gotowe.

1. **Docelowy framework** – .NET 6.0 lub nowszy. Starsze wersje nadal się skompilują, ale nie będą zawierały najnowszych funkcji języka.  
2. **Pakiet** – Uruchom `dotnet add package Aspose.OCR` w terminalu lub użyj interfejsu NuGet Package Manager.  
3. **Obrazy** – Umieść dwa przykładowe obrazy w folderze, do którego możesz odwołać się, np. `C:\OCRSamples\arabic_sign.jpg` i `C:\OCRSamples\hindi_receipt.png`. Obraz arabski powinien zawierać wyraźne, wysokokontrastowe znaki arabskie; obraz hindi może być zeskanowanym paragonem lub zdjęciem znaku.  

To wszystko — bez dodatkowych plików konfiguracyjnych, bez sterowników GPU, po prostu prosty silnik OCR działający na CPU.

---

## Rozpoznawanie tekstu arabskiego – ładowanie i przetwarzanie

Teraz faktycznie **rozpoznamy tekst arabski**. Kluczowe jest poinformowanie silnika, jakiego języka się spodziewa; w przeciwnym razie domyślnie przyjmie znaki łacińskie i otrzymasz zniekształcony wynik.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class MultiLangDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine (CPU‑based by default)
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load an image that contains Arabic script
        var arabicImage = OcrImage.FromFile(@"C:\OCRSamples\arabic_sign.jpg");

        // 3️⃣ Recognize the Arabic text – note the Language.Arabic enum
        var arabicResult = ocrEngine.Recognize(arabicImage, Language.Arabic);

        // 4️⃣ Print the result to the console
        System.Console.WriteLine("Arabic: " + arabicResult.Text);
```

**Dlaczego to działa:**  
* `OcrEngine` zajmuje się całą ciężką pracą — wstępnym przetwarzaniem, segmentacją i klasyfikacją znaków.  
* Przekazując `Language.Arabic`, aktywujemy silnik obsługujący układ od prawej do lewej oraz zestaw znaków arabskich. Bez tego silnik potraktowałby obraz jako tekst łaciński od lewej do prawej, co prowadzi do brakujących diakrytyków i zepsutych słów.  

**Oczekiwany wynik** (twój rzeczywisty tekst będzie się różnił w zależności od obrazu):

```
Arabic: مرحبا بكم في متجرنا
```

Jeśli zobaczysz puste ciągi, sprawdź, czy obraz nie jest zbyt ciemny oraz czy ścieżka do pliku jest poprawna.  

---

## wyodrębnić tekst z obrazu – obsługa skryptów od prawej do lewej

Arabski nie jest jedynym skryptem wymagającym specjalnego traktowania. Języki od prawej do lewej (RTL) wymagają, aby silnik OCR odwrócił kolejność wizualną po rozpoznaniu. Aspose robi to automatycznie, gdy określisz `Language.Arabic`, ale warto o tym pamiętać przy przyszłych rozszerzeniach (np. hebrajski).

*Tip:* Gdy później wyświetlasz wynik OCR w interfejsie użytkownika, upewnij się, że kontrolka obsługuje renderowanie RTL; w przeciwnym razie tekst będzie wyglądał na pomieszany.

---

## konwertować obraz na tekst – praca z hindi

Przechodząc do innego języka, **konwertujemy obraz na tekst** dla hinduskiego paragonu. Proces jest podobny do arabskiego, ale używamy `Language.Hindi`.

```csharp
        // 5️⃣ Load the Hindi (Devanagari) image
        var hindiImage = OcrImage.FromFile(@"C:\OCRSamples\hindi_receipt.png");

        // 6️⃣ Recognize Hindi text – Language.Hindi tells the engine to use Devanagari models
        var hindiResult = ocrEngine.Recognize(hindiImage, Language.Hindi);

        // 7️⃣ Output the Hindi OCR result
        System.Console.WriteLine("Hindi: " + hindiResult.Text);
    }
}
```

**Dlaczego ponownie używamy tego samego obiektu `ocrEngine`:**  
Tworzenie nowego silnika dla każdego języka marnowałoby pamięć i czas inicjalizacji. Silnik Aspose jest bezpieczny wątkowo przy kolejnych wywołaniach, więc jego ponowne użycie jest zarówno wydajne, jak i schludne.

**Przykładowy wynik w konsoli** (znowu zależy od twojego obrazu):

```
Hindi: कुल राशि: ₹ 1,250.00
```

Jeśli tekst hindi wygląda jak zniekształcone znaki łacińskie, prawdopodobnie pominąłeś enum języka lub rozdzielczość obrazu jest zbyt niska (<300 dpi). Zwiększenie rozdzielczości obrazu lub zastosowanie prostego filtru binaryzacji może znacząco poprawić dokładność.

---

## rozpoznawanie tekstu hindi – typowe problemy i przypadki brzegowe

Nawet przy prawidłowym flagowaniu języka, kilka trudności może cię zaskoczyć:

| Problem | Objaw | Rozwiązanie |
|-------|---------|-----|
| Niski kontrast | Wiele znaków zamienia się w „?” lub jest pomijanych | Wstępnie przetwórz za pomocą `OcrImage.AdjustContrast(1.5)` |
| Przechylony obraz | Tekst jest obrócony, OCR zwraca pusty ciąg | Wywołaj `ocrEngine.PreprocessImage(arabicImage, ImageProcessingOptions.Rotate)` |
| Mieszane języki | Linia arabska, a potem liczby po angielsku | Wykonaj dwa przebiegi: najpierw z `Language.Arabic`, potem z `Language.English` na tym samym obrazie i połącz wyniki |
| Duży rozmiar pliku | Wolne rozpoznawanie lub błędy pamięci | Zmniejsz rozmiar do maksymalnie 2000 px szerokości przy pomocy `OcrImage.Resize(2000, 0)` |

Te wskazówki pomogą ci **wyodrębnić tekst z obrazu**, który nie jest idealnie zeskanowany, co jest powszechne w rzeczywistych projektach.

---

## Złożenie wszystkiego razem – kompletny działający przykład

Poniżej znajduje się pełny program, który możesz skopiować bezpośrednio do nowego projektu konsolowego. Brak ukrytych zależności, brak dodatkowej konfiguracji — po prostu czysty C#.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class MultiLangDemo
{
    static void Main()
    {
        // Initialize the OCR engine (CPU‑based)
        var ocrEngine = new OcrEngine();

        // -------------------- Arabic --------------------
        var arabicPath = @"C:\OCRSamples\arabic_sign.jpg";
        var arabicImage = OcrImage.FromFile(arabicPath);
        var arabicResult = ocrEngine.Recognize(arabicImage, Language.Arabic);
        System.Console.WriteLine("Arabic: " + arabicResult.Text);

        // -------------------- Hindi --------------------
        var hindiPath = @"C:\OCRSamples\hindi_receipt.png";
        var hindiImage = OcrImage.FromFile(hindiPath);
        var hindiResult = ocrEngine.Recognize(hindiImage, Language.Hindi);
        System.Console.WriteLine("Hindi: " + hindiResult.Text);
    }
}
```

**Uruchomienie programu** wypisze zarówno ciągi arabskie, jak i hindi w konsoli, potwierdzając, że udało ci się **rozpoznać tekst arabski** oraz **rozpoznać tekst hindi** w jednym przebiegu.  

---

## Zakończenie

Masz teraz solidną, kompleksową odpowiedź na pytanie **jak wykonać OCR arabskiego**, jednocześnie obsługując hindi. Tworząc pojedynczy `OcrEngine`, ładując każdy obraz i przekazując odpowiedni enum `Language`, możesz **wyodrębnić tekst z obrazu**, **konwertować obraz na tekst** oraz **rozpoznawać tekst arabski** i **rozpoznawać tekst hindi** bez dodatkowych bibliotek.  

Od tego miejsca możesz rozważyć:

* **Przetwarzanie wsadowe** – iteracja po folderze obrazów i zapisywanie wyników w bazie danych.  
* **Post‑processing** – użycie wyrażeń regularnych do czyszczenia symboli walutowych w hinduskich paragonach.  
* **Hybrydowe wykrywanie języka** – przekazanie surowego bitmapu do modelu identyfikacji języka przed wyborem odpowiedniego enumu.  

Spróbuj, dostosuj kroki wstępnego przetwarzania i zobacz, jak szybko rośnie dokładność OCR. Jeśli napotkasz jakiekolwiek problemy, daj znać.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}