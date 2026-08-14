---
category: general
date: 2026-02-20
description: Wstępnie przetwarzaj OCR obrazu za pomocą Aspose.OCR w C#. Dowiedz się,
  jak zastosować filtr medianowy, zredukować szum obrazu i efektywnie wyodrębnić tekst
  z obrazu.
draft: false
keywords:
- preprocess image OCR
- apply median filter
- extract text image
- reduce image noise
- c# ocr example
language: pl
og_description: Wstępne przetwarzanie obrazu OCR za pomocą Aspose.OCR. Ten samouczek
  pokazuje, jak zastosować filtr medianowy, zredukować szum obrazu i wyodrębnić tekst
  z obrazu przy użyciu C#.
og_title: Wstępne przetwarzanie obrazu OCR w C# – Kompletny przewodnik
tags:
- OCR
- C#
- Image Processing
title: Wstępne przetwarzanie obrazu OCR w C# – Kompletny przewodnik krok po kroku
url: /pl/net/ocr-optimization/preprocess-image-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Przetwarzanie wstępne obrazu OCR w C# – Kompletny przewodnik krok po kroku

Czy kiedykolwiek potrzebowałeś **przetworzyć wstępnie obraz OCR**, ponieważ zeskanowane zdjęcia zwracają zniekształcony tekst? Nie jesteś sam. W wielu rzeczywistych projektach — pomyśl o paragonach, dowodach tożsamości czy odręcznych notatkach — surowy obraz rzadko jest gotowy do natychmiastowego rozpoznawania. Dobra wiadomość? Kilka prostych kroków przetwarzania wstępnego może znacząco zwiększyć dokładność, a wszystko to możesz zrobić w C# z Aspose.OCR.

W tym samouczku przeprowadzimy praktyczny przykład, który pokaże, jak **zastosować filtr medianowy**, **zredukować szum obrazu**, a na końcu **wyodrębnić tekst z obrazu** uzyskując czysty, czytelny rezultat. Po zakończeniu będziesz mieć w pełni działającą aplikację konsolową w C#, którą możesz wstawić do dowolnego rozwiązania .NET. Bez niejasnych odniesień, tylko kod, którego potrzebujesz, oraz „dlaczego” za każdą linijką.

---

## What You’ll Need

- **Aspose.OCR for .NET** (najnowsza wersja w momencie pisania, 23.12). Możesz go pobrać przez NuGet: `Install-Package Aspose.OCR`.
- .NET 6.0 lub nowszy (przykład używa aplikacji konsolowej, ale ta sama logika działa w ASP.NET, WPF itp.).
- Przykładowy obraz wymagający czyszczenia — np. `skewed_photo.jpg`.  
- Trochę doświadczenia w C#; koncepcje są proste nawet dla młodszych programistów.

> **Pro tip:** Jeśli pracujesz na komputerze firmowym, upewnij się, że Twój feed NuGet jest skonfigurowany tak, aby zezwalał na zewnętrzne pakiety, w przeciwnym razie instalacja się nie powiedzie.

## Krok 1 – Utwórz instancję silnika OCR  

Pierwszą rzeczą, którą robisz, jest uruchomienie `OcrEngine`. Ten obiekt przechowuje ustawienia rozpoznawania i później przetworzy wstępnie przygotowaną bitmapę.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;   // For Image handling
using System;

class PreprocessExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is the core component that will read text.
        OcrEngine ocrEngine = new OcrEngine();

        // ... we’ll continue with loading and preprocessing the image below.
```

**Dlaczego?**  

Utworzenie silnika raz i ponowne jego użycie dla wielu obrazów zmniejsza narzut. Pozwala także dostosować język lub tryby rozpoznawania później, bez konieczności przebudowy całej linii przetwarzania.

## Krok 2 – Wczytaj obraz źródłowy  

Potrzebujesz obiektu `System.Drawing.Image`, który wskazuje na Twój surowy plik. W prawdziwym projekcie możesz przyjmować strumień, ale dla przejrzystości odczytamy go z dysku.

```csharp
        // Load the image that requires preprocessing.
        Image sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_photo.jpg");
```

> **Uwaga:** Zastąp `YOUR_DIRECTORY` rzeczywistą ścieżką folderu. Jeśli plik nie zostanie znaleziony, zostanie rzucony `FileNotFoundException` — przechwyć go, jeśli chcesz obsłużyć błąd w elegancki sposób.

## Krok 3 – Prostowanie i obrót obrazu  

Większość zeskanowanych dokumentów jest lekko nachylona. Filtr `DeskewAndRotate` automatycznie wykrywa kąt pochylenia i obraca obraz do pionowej orientacji.

```csharp
        // Correct orientation – crucial for accurate OCR.
        Image processedImage = sourceImage.Apply(Preprocess.DeskewAndRotate());
```

**Dlaczego to ważne?**  

Silniki OCR zakładają, że linie tekstu są poziome. Nawet nachylenie o 2 stopnie może obniżyć dokładność rozpoznawania o 15‑20 %. Prostowanie to najtańszy sposób na uzyskanie dużego zysku.

## Krok 4 – Zastosuj filtr medianowy, aby zredukować szum obrazu  

Szum pojawia się jako plamki lub losowe piksele, szczególnie w zdjęciach przy słabym oświetleniu. Filtr medianowy wygładza je, zachowując krawędzie, co jest dokładnie tym, czego potrzebujemy przed OCR.

```csharp
        // Reduce noise – radius of 2 is a good balance for most photos.
        processedImage = processedImage.Apply(Preprocess.MedianFilter(radius: 2));
```

**Dlaczego filtr medianowy?**  

W przeciwieństwie do filtru średniego (average), filtr medianowy zastępuje każdy piksel medianą wartości w jego otoczeniu. Oznacza to, że izolowany szum zostaje usunięty bez rozmywania kresek tekstu — klasyczna technika do **reduce image noise**.

## Krok 5 – Zwiększ kontrast metodą rozciągania  

Po usunięciu szumu następnym krokiem jest zwiększenie różnicy między tekstem a tłem. Rozciąganie kontrastu rozkłada intensywności pikseli na pełny zakres 0‑255.

```csharp
        // Stretch contrast to make dark text pop against a light background.
        processedImage = processedImage.Apply(Preprocess.ContrastStretch());
```

**Dlaczego rozciągać?**  

Silniki OCR polegają na wyraźnym oddzieleniu pierwszego planu od tła. Jeśli obraz jest wyblakły, silnik może traktować tekst jako tło. Rozciąganie kontrastu naprawia to bez konieczności ręcznego progowania.

## Krok 6 – Wykonaj OCR na przetworzonym obrazie  

Teraz, gdy obraz jest prosty, czysty i o wysokim kontraście, przekazujemy go silnikowi OCR.

```csharp
        // Recognize the text from the cleaned image.
        string extractedText = ocrEngine.Recognize(processedImage);
```

**Co otrzymujesz:**  

`extractedText` zawiera surowy ciąg Unicode wykryty przez Aspose.OCR. Możesz go dalej przetwarzać (przycinanie, wyrażenia regularne itp.), jeśli zajdzie taka potrzeba.

## Krok 7 – Wyświetl rozpoznany tekst  

Na koniec zapisz wynik do konsoli lub pliku — cokolwiek pasuje do Twojego przepływu pracy.

```csharp
        // Show the result in the console.
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

### Expected Output

Jeśli `skewed_photo.jpg` zawiera frazę „Hello World”, zobaczysz coś w rodzaju:

```
=== Extracted Text ===
Hello World
```

Jeśli obraz wciąż jest zaszumiony, możesz zauważyć zniekształcone znaki — wróć do Kroku 4 i zwiększ promień filtru medianowego lub poeksperymentuj z dodatkowymi filtrami, takimi jak `GaussianBlur`.

## Pełny działający przykład (gotowy do kopiowania i wklejenia)

Poniżej znajduje się cały program, gotowy do kompilacji. Brak brakujących elementów — wystarczy podmienić ścieżkę do pliku.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;
using System;

class PreprocessExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image that needs preprocessing
        Image sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_photo.jpg");

        // Step 3: Deskew and rotate the image to correct orientation
        Image processedImage = sourceImage.Apply(Preprocess.DeskewAndRotate());

        // Step 4: Reduce noise with a median filter (radius = 2)
        processedImage = processedImage.Apply(Preprocess.MedianFilter(radius: 2));

        // Step 5: Enhance contrast using contrast stretching
        processedImage = processedImage.Apply(Preprocess.ContrastStretch());

        // Step 6: Perform OCR on the preprocessed image
        string extractedText = ocrEngine.Recognize(processedImage);

        // Step 7: Output the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

> **Wskazówka dotycząca przypadków brzegowych:** Jeśli Twój obraz zawiera kolorowy tekst na kolorowym tle, rozważ konwersję do odcieni szarości przed zastosowaniem `ContrastStretch`. Możesz to zrobić za pomocą `Preprocess.Grayscale()` w pipeline.

## Częste pytania i warianty  

### Co zrobić, jeśli obraz jest do góry nogami?  
`DeskewAndRotate` automatycznie wykrywa obroty o 180 stopni, ale możesz wymusić obrót za pomocą `Preprocess.Rotate(angle: 180)` przed prostowaniem.

### Czy mogę pominąć filtr medianowy?  
Tak, ale prawdopodobnie zauważysz spadek korzyści z **reduce image noise**. W skanach wysokiej rozdzielczości filtr może być niepotrzebny; w zdjęciach telefonicznych przy słabym oświetleniu jest zazwyczaj niezbędny.

### Jak to się różni od prostego `Apply(Preprocess.Binarize())`?  
Binarizacja konwertuje obraz do czystej czerni i bieli, co może być surowe dla cienkich czcionek. Nasze podejście zachowuje szczegóły w odcieniach szarości, a następnie rozciąga kontrast — często daje lepsze wyniki dla czcionek o mieszanych rozmiarach.

### Czy istnieje sposób, aby **apply median filter** tylko na wybranym obszarze zainteresowania?  
`Apply` w Aspose.OCR działa na całej bitmapie, ale możesz najpierw przyciąć obraz (`sourceImage.Clone(new Rectangle(...), sourceImage.PixelFormat)`) i dopiero wtedy zastosować filtr na tym pod‑obrazie.

## Kolejne kroki – wyjście poza podstawowe przetwarzanie wstępne  

- **Pakiety językowe:** Jeśli potrzebujesz wyodrębnić francuskie lub japońskie znaki, załaduj odpowiedni model językowy poprzez `ocrEngine.Language = Language.French;`.
- **Własne progowanie:** W przypadku skanów o ekstremalnie niskim kontraście, po filtrze medianowym wypróbuj `Preprocess.AdaptiveThreshold()`.
- **Przetwarzanie wsadowe:** Owiń kroki w pętli `foreach (string file in Directory.GetFiles(...))` i zapisz każdy wynik do pliku `.txt`.  
- **Dostrajanie wydajności:** Ponownie używaj jednej instancji `OcrEngine` i wstępnie przydziel bufor `Bitmap`, aby uniknąć skoków GC przy przetwarzaniu tysięcy obrazów.

## Zakończenie  

Właśnie pokazaliśmy, jak **preprocess image OCR** w C# od początku do końca: wczytać obraz, prostować, **apply median filter**, zwiększyć kontrast i w końcu **extract text image** przy użyciu Aspose.OCR. Pełny fragment kodu jest gotowy do wstawienia w dowolnym projekcie, a wyjaśnienia dostarczają „dlaczego” za każdą transformacją — dzięki czemu możesz dostosować parametry do własnych przypadków brzegowych.

Wypróbuj to na kilku różnych zdjęciach, baw się promieniem filtru i obserwuj, jak rośnie dokładność rozpoznawania. Gdy poczujesz się pewnie, zgłęb kolejne udoskonalenia wymienione powyżej i zostaniesz osobą, do której zespół zwróci się po czyste potoki OCR.

Szczęśliwego kodowania i niech Twój OCR zawsze odczytuje czysto! 

![przykład przetwarzania obrazu OCR](/images/preprocess-image-ocr.png "przetwarzanie obrazu OCR – przed i po przetworzeniu")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}