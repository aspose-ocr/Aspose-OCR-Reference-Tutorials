---
category: general
date: 2026-04-04
description: Jak szybko i bezpiecznie korzystać z OCR. Dowiedz się, jak wyodrębnić
  tekst z obrazu, konwertować DJVU na tekst oraz wczytywać obraz do OCR przy użyciu
  Aspose.OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert djvu to text
- load image for OCR
- extract text from djvu
language: pl
og_description: Jak używać OCR w C#, aby wyodrębnić tekst z plików graficznych i dokumentów
  DJVU. Samouczek krok po kroku z pełnym kodem.
og_title: Jak korzystać z OCR w C# – Kompletny przewodnik
tags:
- OCR
- C#
- Aspose
title: Jak używać OCR w C# – wyodrębniaj tekst z obrazów i plików DJVU
url: /pl/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-and-djvu-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać OCR w C# – Wyodrębnianie tekstu z obrazów i plików DJVU

Zastanawiałeś się kiedyś **jak używać OCR**, aby wyciągnąć słowa ze zeskanowanej strony bez ręcznego wpisywania? Nie jesteś jedyny. W wielu projektach — czy to digitalizujesz stare książki, czy wyciągasz dane z paragonów — uzyskanie tekstu z obrazu jest codziennym problemem. Dobra wiadomość? Z Aspose.OCR możesz to zrobić w kilku linijkach, nawet gdy źródłem jest plik DJVU.

W tym przewodniku przejdziemy przez wszystko, co potrzebne, aby **wyodrębnić tekst z obrazu**, **załadować obraz do OCR** i nawet **przekształcić DJVU na tekst** przy użyciu C#. Po zakończeniu będziesz mieć gotową do uruchomienia aplikację konsolową, która wypisuje rozpoznany tekst bezpośrednio w konsoli. Bez tajemnic, bez dodatkowych zależności, tylko czysty C# i Aspose.

## Co się nauczysz

- Jak zainstalować i odwołać się do biblioteki Aspose.OCR.
- Dokładny kod potrzebny do **załadowania obrazu do OCR**, niezależnie czy to PNG, JPEG, czy strona DJVU.
- Jak wywołać silnik i pobrać wynik.
- Wskazówki dotyczące obsługi dużych dokumentów i typowych pułapek.
- Pełny, uruchamialny przykład, który możesz skopiować‑wkleić do Visual Studio.

> **Wymagania wstępne:** .NET 6.0 lub nowszy oraz ważna licencja Aspose.OCR (lub darmowa wersja próbna). Jeśli jeszcze nie masz biblioteki, pobierz ją z NuGet za pomocą `dotnet add package Aspose.OCR`.

---

## Jak używać OCR z Aspose w C#

To jest kluczowy krok, w którym faktycznie odpowiadamy na pytanie **jak używać OCR** w projekcie C#. Poniższy kod to pełny program; możesz go wkleić do nowej aplikacji konsolowej i nacisnąć F5.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create the OCR engine instance.
            var ocrEngine = new OcrEngine();

            // Step 2: Load the image (or DJVU page) you want to analyze.
            // Replace the path with your own file location.
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book-page.djvu");

            // Step 3: Run the recognition process.
            OcrResult ocrResult = ocrEngine.Recognize();

            // Step 4: Output the extracted text.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Why this works:**  
- `OcrEngine` jest punktem wejścia; abstrahuje ciężkie operacje wstępnego przetwarzania obrazu, wykrywania języka i klasyfikacji znaków.  
- `ImageStream.FromFile` obsługuje wiele formatów, w tym DJVU, co oznacza, że możesz **przekształcić DJVU na tekst** bez dodatkowego kroku konwersji.  
- `Recognize()` zwraca obiekt `OcrResult`, który zawiera wynikowy tekst, wyniki pewności oraz nawet ramki ograniczające, jeśli będą potrzebne później.

Uruchomienie programu wypisuje coś podobnego do:

```
=== OCR Result ===
In the beginning God created the heavens and the earth.
```

To wszystko — twoja pierwsza udana operacja **wyodrębniania tekstu z DJVU**.

![jak używać OCR przykład](/images/ocr-demo.png "Zrzut ekranu pokazujący, jak używać OCR w aplikacji konsolowej C#")

*Tekst alternatywny: „jak używać OCR” zrzut ekranu wyjścia konsoli.*

## Załaduj obraz do OCR

Zanim silnik będzie mógł coś odczytać, musisz **załadować obraz do OCR** prawidłowo. Aspose obsługuje większość formatów rastrowych od razu, ale kilka wskazówek może usprawnić rozpoznawanie:

- **Zmień rozmiar dużych obrazów** do maksymalnie 2000 px po najdłuższym boku. Zbyt duże pliki zwiększają zużycie pamięci i mogą spowolnić silnik.
- **Konwertuj obrazy kolorowe na odcienie szarości**, jeśli zauważysz szumy w tle. Użyj `ocrEngine.Image = ImageStream.FromFile(path).ConvertToGrayscale();`.
- **Ustaw DPI ręcznie** dla skanów o niskiej rozdzielczości (`ocrEngine.Image.DpiX = 300; ocrEngine.Image.DpiY = 300;`).

Te poprawki są opcjonalne, ale często zwiększają dokładność, gdy **wyodrębniasz tekst z obrazu** w plikach takich jak zeskanowane paragony.

## Wyodrębnianie tekstu z obrazu – najlepsze praktyki

Gdy pracujesz z typowymi formatami obrazów (PNG, JPEG, BMP), kroki pozostają takie same, ale możesz dopasować silnik:

```csharp
ocrEngine.Image = ImageStream.FromFile("sample.png");

// Optional: enable language packs for better accuracy.
ocrEngine.Language = Language.English;

// Optional: set recognition mode to auto.
ocrEngine.RecognitionMode = RecognitionMode.Auto;
```

- **Wybór języka** ma znaczenie. Jeśli przetwarzasz dokumenty wielojęzyczne, ustaw `ocrEngine.Language = Language.Multilingual;`.
- **RecognitionMode** może być `Auto`, `Fast` lub `Accurate`. `Accurate` zapewnia wyższą jakość kosztem szybkości — używaj go do zadań archiwizacyjnych.

## Konwersja DJVU na tekst – obsługa plików wielostronicowych

Pliki DJVU często zawierają kilka stron. Aspose traktuje każdą stronę jako osobny strumień obrazu, więc możesz iterować po nich:

```csharp
using Aspose.OCR;
using System.Collections.Generic;

var ocrEngine = new OcrEngine();
List<string> allPagesText = new List<string>();

int pageCount = ImageStream.GetPageCount("book.djvu");
for (int i = 1; i <= pageCount; i++)
{
    ocrEngine.Image = ImageStream.FromFile("book.djvu", i); // Load page i
    OcrResult result = ocrEngine.Recognize();
    allPagesText.Add(result.Text);
}

// Combine all pages into a single string.
string fullText = string.Join("\n--- Page Break ---\n", allPagesText);
Console.WriteLine(fullText);
```

**Dlaczego iterować?**  
Pliki DJVU to w zasadzie stos obrazów. Iterując po każdej stronie, **wyodrębniasz tekst z DJVU** w kolejności, zachowując oryginalny przepływ dokumentu.

## Typowe pułapki i wskazówki profesjonalne

| Problem | Dlaczego się pojawia | Rozwiązanie |
|------|----------------|-----|
| **Zniekształcone znaki** | Niska DPI lub silna kompresja | Zwiększ rozdzielczość obrazu, ustaw `ocrEngine.Image.DpiX/Y = 300` |
| **Wolne przetwarzanie** | Używanie trybu `Accurate` na ogromnych plikach | Przełącz na tryb `Fast` dla zadań masowych |
| **Brak wsparcia językowego** | Domyślny język to tylko angielski | Załaduj dodatkowe pakiety językowe (`ocrEngine.Language = Language.Spanish;`) |
| **Błędy braku pamięci** | Ładowanie wielu stron wysokiej rozdzielczości jednocześnie | Przetwarzaj strony pojedynczo i zwalniaj zasoby (`ocrEngine.Dispose();`) |

Szybka **wskazówka profesjonalna**: zawsze wywołuj `ocrEngine.Dispose()` po zakończeniu pracy z daną stroną. Zwalnia to zasoby natywne i zapobiega subtelnym wyciekom pamięci, które mogą spowodować awarię długotrwałych usług.

## Testowanie potoku OCR

Aby zweryfikować, że wszystko działa, wypróbuj te proste kontrole:

1. **Wypisz długość** rozpoznanego ciągu: `Console.WriteLine($"Characters recognized: {ocrResult.Text.Length}");`
2. **Porównaj z znanym tekstem** używając prostej biblioteki diff, jeśli masz prawdziwy tekst.
3. **Zaloguj wyniki pewności** (`ocrResult.Confidence`), aby automatycznie wykrywać strony niskiej jakości.

Jeśli pewność jest konsekwentnie poniżej 0,7, wróć do kroków wstępnego przetwarzania obrazu wymienionych wcześniej.

## Kolejne kroki

Teraz, gdy wiesz **jak używać OCR**, rozważ rozszerzenie swojego przepływu pracy:

- **Przetwarzanie wsadowe**: Owiń pętlę w `Parallel.ForEach`, aby przyspieszyć przetwarzanie dużych zbiorów.
- **Eksport do PDF**: Użyj Aspose.PDF, aby osadzić rozpoznany tekst jako ukrytą warstwę w przeszukiwalnych plikach PDF.
- **Integracja z AI**: Przekaż wyodrębnione ciągi do modelu językowego w celu podsumowania lub ekstrakcji jednostek.

Wszystko to opiera się na tej samej podstawie, którą właśnie stworzyłeś, a każdy krok korzysta z tych samych zasad **wyodrębniania tekstu z obrazu**, które omówiliśmy.

Spróbuj, dostosuj ustawienia do swoich konkretnych dokumentów i w krótkim czasie zamienisz zeskanowane strony w przeszukiwalny tekst. Masz pytania lub trudny plik, który nie chce współpracować? zostaw komentarz — miłego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}