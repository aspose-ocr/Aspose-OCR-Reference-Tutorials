---
category: general
date: 2026-03-13
description: Jak wykonać OCR w C# i wyodrębnić tekst z obrazu przy użyciu OcrEngine.
  Dowiedz się, jak szybko przekształcić obraz w tekst dzięki kompletnemu przewodnikowi
  krok po kroku.
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- read text from picture
- how to extract text
language: pl
og_description: Jak wykonać OCR w C#? Ten przewodnik pokazuje, jak wyodrębnić tekst
  z obrazu, przekształcić obraz w tekst oraz odczytać tekst ze zdjęcia przy użyciu
  OcrEngine.
og_title: Jak wykonać OCR w C# – wyodrębnić tekst z obrazu
tags:
- OCR
- C#
- Image Processing
title: Jak wykonać OCR w C# – wyodrębnić tekst z obrazu
url: /pl/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonać OCR w C# – wyodrębnić tekst z obrazu

Jak wykonać OCR w C# to częste pytanie wśród programistów, którzy muszą **odczytywać tekst z obrazów**. W tym przewodniku przeprowadzimy Cię przez proces wyodrębniania tekstu z obrazu przy użyciu biblioteki `OcrEngine`, zamieniając obrazy w przeszukiwalne ciągi znaków w kilku linijkach kodu.  

Jeśli kiedykolwiek patrzyłeś na zeskanowaną fakturę, odręczną notatkę lub zrzut ekranu i zastanawiałeś się *„jak wyodrębnić tekst?”*, jesteś w właściwym miejscu. Poruszymy także temat konwersji obrazu na tekst w trybie wsadowym, abyś mógł zautomatyzować cały przepływ pracy.

---

## Czego będziesz potrzebować

- **.NET 6.0 lub nowszy** (API, którego używamy, działa z .NET Standard 2.0+)
- Pakiet NuGet **OcrEngine** (lub dowolna kompatybilna biblioteka OCR udostępniająca właściwości `Language`, `Image`, `Recognize` i `Text`)
- Przykładowy plik obrazu, np. `hindi_page.jpg`, umieszczony w folderze, do którego możesz odwołać się w kodzie
- Podstawowa znajomość składni C# – nie są potrzebne zaawansowane triki

To wszystko. Bez zewnętrznych usług, bez kluczy API, tylko lokalna biblioteka, która wykonuje ciężką pracę.

---

## Implementacja krok po kroku

Poniżej dzielimy proces na logiczne części. Każda sekcja ma wyraźny nagłówek, krótki fragment kodu i wyjaśnienie **dlaczego** dany krok jest ważny — nie tylko **co** robi.

### Jak wykonać OCR – podstawowe kroki

Cały przepływ można podsumować w pięciu działaniach:

1. **Utwórz** instancję silnika OCR
2. **Wybierz** język, który chcesz rozpoznać
3. **Załaduj** obraz zawierający tekst
4. **Uruchom** algorytm rozpoznawania
5. **Odczytaj** wyodrębniony tekst

To szkielet; sekcje poniżej rozwijają go.

---

### Wyodrębnij tekst z obrazu – utwórz silnik

Najpierw potrzebujemy obiektu, który potrafi komunikować się z silnikiem OCR.

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

*Dlaczego to ważne:* Inicjalizacja `OcrEngine` przydziela wszystkie wewnętrzne bufory i ładuje niezbędne natywne pliki DLL do analizy obrazu. Pominięcie tego kroku pozostawi Cię bez rozpoznawacza, którego można wywołać później.

> **Wskazówka:** Jeśli planujesz przetwarzać wiele obrazów kolejno, utrzymuj tę samą instancję `ocrEngine`. Ponownie wykorzystuje modele językowe i przyspiesza kolejne wywołania.

---

### Konwertuj obraz na tekst – wybierz język

Dokładność OCR zależy w dużym stopniu od modelu językowego, który mu dostarczysz. Dla hindi, tamilskiego lub dowolnego innego pisma ustaw właściwość `Language` odpowiednio.

```csharp
// Step 2: Select the language of the text to recognize (e.g., Hindi)
ocrEngine.Language = Language.Hindi;   // You can also use Language.Tamil, Language.English, etc.
```

*Dlaczego to ważne:* Silnik używa zestawów znaków i modeli statystycznych specyficznych dla języka. Podanie niewłaściwego języka często skutkuje zniekształconym wynikiem, szczególnie w przypadku skryptów niełacińskich.

> **Przypadek szczególny:** Jeśli potrzebujesz obsługi wielu języków, niektóre biblioteki pozwalają ustawić listę awaryjną, np. `ocrEngine.Language = Language.Multilingual;`.

---

### Odczytaj tekst z obrazu – załaduj źródłowy obraz

Teraz wskazujemy silnik na plik, który zawiera tekst wizualny.

```csharp
// Step 3: Load the image that contains the text
ocrEngine.Image = ImageStream.FromFile(@"C:\OCR\Samples\hindi_page.jpg");
```

*Dlaczego to ważne:* `ImageStream.FromFile` konwertuje surowy plik do formatu bitmapy, który rdzeń OCR może zrozumieć. Dostarczenie uszkodzonego lub nieobsługiwanego formatu (np. SVG) spowoduje wyjątek.

> **Uwaga:** Duże obrazy mogą zużywać dużo pamięci. Jeśli przetwarzasz skany wysokiej rozdzielczości, rozważ zmniejszenie ich rozmiaru przy użyciu `Image.Resize` przed przekazaniem do silnika.

---

### Konwertuj obraz na tekst – uruchom rozpoznawanie

Gdy silnik jest gotowy, a obraz załadowany, w końcu wywołujemy proces OCR.

```csharp
// Step 4: Perform the OCR operation
ocrEngine.Recognize();
```

*Dlaczego to ważne:* `Recognize` uruchamia szereg wewnętrznych kroków — wstępne przetwarzanie, segmentację, klasyfikację znaków i przetwarzanie końcowe. Wywołanie jest blokujące, co oznacza, że wątek czeka, aż tekst będzie gotowy.

> **Uwaga o wydajności:** Na typowym komputerze rozpoznanie strony 300 dpi zajmuje < 1 sekundę. Na serwerze możesz chcieć uruchomić to w zadaniu w tle, aby uniknąć zacięć interfejsu.

---

### Jak wyodrębnić tekst – pobierz wynik

Po zakończeniu rozpoznawania silnik zapisuje wynik w postaci zwykłego tekstu w właściwości `Text`.

```csharp
// Step 5: Output the recognized text
Console.WriteLine(ocrEngine.Text);
```

*Dlaczego to ważne:* Właściwość `Text` dostarcza czysty ciąg UTF‑8, który możesz zapisać do pliku, wprowadzić do bazy danych lub przekazać do kolejnych etapów przetwarzania NLP.

> **Oczekiwany wynik:** Dla przykładowej strony w języku hindi możesz zobaczyć coś takiego  
> `यह एक उदाहरण पाठ है जो OCR द्वारा पहचाना गया है।`  
> (Dokładny wynik zależy od jakości obrazu i modelu językowego.)

---

## Dodatkowe uwagi dla projektów produkcyjnych

Poniżej znajdują się niektóre scenariusze „co‑jeśli”, z którymi prawdopodobnie się spotkasz, gdy będziesz **wyodrębniać tekst z obrazu** w produkcji.

### Obsługa wielu obrazów w pętli

Jeśli musisz **konwertować obraz na tekst** dla dziesiątek plików, otocz kroki w pętli `foreach` i ponownie użyj tej samej instancji `ocrEngine`:

```csharp
string[] files = Directory.GetFiles(@"C:\OCR\Batch\", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    ocrEngine.Recognize();
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), ocrEngine.Text);
}
```

### Radzenie sobie z niskiej jakości skanami

- **Wstępne przetwarzanie** przy użyciu binaryzacji (`Image.Binarize()`), usuwania szumów lub prostowania.
- **Zwiększ DPI** przy skanowaniu (300 dpi to bezpieczna podstawa).
- **Wybierz model językowy**, który obsługuje ligatury danego pisma (np. Devanagari dla hindi).

### Odczytywanie tekstu z obrazu w sieci

Gdy obraz pochodzi z adresu URL, najpierw pobierz go do strumienia pamięci:

```csharp
using (HttpClient client = new())
{
    byte[] data = await client.GetByteArrayAsync(imageUrl);
    using var ms = new MemoryStream(data);
    ocrEngine.Image = ImageStream.FromStream(ms);
    ocrEngine.Recognize();
    Console.WriteLine(ocrEngine.Text);
}
```

### Bezpieczeństwo wątków i równoległość

Większość bibliotek OCR **nie** jest domyślnie bezpieczna wątkowo. Jeśli planujesz **odczytywać tekst z obrazu** równocześnie, uruchom oddzielne instancje `OcrEngine` na każdy wątek lub użyj kolejki producent‑konsument do serializacji dostępu.

---

## Kompletny działający przykład

Łącząc wszystko razem, oto gotowa do uruchomienia aplikacja konsolowa, która demonstruje **jak wykonać OCR**, **wyodrębnić tekst z obrazu** i **odczytać tekst z obrazu** w jednym spójnym programie.

```csharp
using System;
using OcrLibrary;               // Adjust to your OCR library's namespace
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Choose the language (Hindi in this case)
        ocrEngine.Language = Language.Hindi;

        // Load the image file
        string imagePath = @"C:\OCR\Samples\hindi_page.jpg";
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }

        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // Run the recognition process
        ocrEngine.Recognize();

        // Output the extracted text
        string result = ocrEngine.Text;
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(result);

        // Optional: Save to a .txt file
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, result);
        Console.WriteLine($"Text saved to {txtPath}");
    }
}
```

**Co powinieneś zobaczyć:** Konsola wypisuje zdanie w języku hindi wyodrębnione z `hindi_page.jpg`, a następnie potwierdzenie, że plik tekstowy został utworzony. Jeśli obraz jest czysty, wynik będzie praktycznie identyczny z oryginalnym wydrukowanym tekstem.

---

## Podsumowanie

Teraz wiesz **jak wykonać OCR** w C# od początku do końca, jak **wyodrębnić tekst z obrazu**, **konwertować obraz na tekst** i **odczytać tekst z obrazu** przy użyciu prostego przepływu `OcrEngine`. Wzorzec pięciu kroków — utwórz, ustaw język, załaduj, rozpoznaj, odczytaj — obejmuje większość przypadków użycia, a dodatkowe wskazówki pomogą Ci radzić sobie z zadaniami wsadowymi, niskiej jakości skanami i źródłami internetowymi.

Gotowy na kolejne wyzwanie? Spróbuj zamienić język na angielski, podać stronę PDF renderowaną jako obraz lub połączyć wynik OCR z pipeline'em indeksowania wyszukiwania. Nie ma granic, gdy opanujesz podstawy OCR w C#.

Masz pytania lub trudny obraz, który nie współpracuje? Dodaj komentarz poniżej, a wspólnie rozwiążemy problem. Szczęśliwego kodowania!  

![przykład wykonania OCR](images/ocr-example.png "przykład wykonania OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}