---
category: general
date: 2026-04-04
description: Jak szybko włączyć GPU w Aspose OCR. Dowiedz się, jak wyodrębnić tekst
  z obrazu, załadować obraz do OCR i rozpoznać tekst przy użyciu C#.
draft: false
keywords:
- how to enable gpu
- extract text from image
- how to extract text
- how to recognize text
- load image for ocr
language: pl
og_description: Jak szybko włączyć GPU w Aspose OCR. Postępuj zgodnie z tym samouczkiem,
  aby wyodrębnić tekst z obrazu, załadować obraz do OCR i rozpoznać tekst przy użyciu
  C#.
og_title: Jak włączyć GPU dla OCR w C# – Kompletny przewodnik
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Jak włączyć GPU dla OCR w C# – Przewodnik krok po kroku
url: /pl/net/ocr-configuration/how-to-enable-gpu-for-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak włączyć GPU dla OCR w C# – Kompletny przewodnik

Zastanawiałeś się kiedyś **jak włączyć GPU** przy używaniu Aspose OCR? Być może napotkałeś barierę wydajności przetwarzając setki paragonów, a CPU po prostu nie nadąża. Dobrą wiadomością jest to, że włączenie przyspieszenia GPU jest dziecinnie proste, a po jego włączeniu zobaczysz, jak silnik OCR przetwarza obrazy w mgnieniu oka.

W tym samouczku nie tylko przełączymy GPU, ale także pokażemy, jak **załadować obraz do OCR**, **rozpoznać tekst** i ostatecznie **wyodrębnić tekst z obrazu** przy użyciu przejrzystego przykładu w C#. Po zakończeniu będziesz mieć gotowy do uruchomienia program, który wyciąga czysty tekst z dowolnego obsługiwanego obrazu — bez konieczności korzystania z zewnętrznych usług.

## Czego będziesz potrzebować

- .NET 6+ (lub .NET Framework 4.7.2 i nowszy).  
- Aspose.OCR for .NET, wersja 24.2.0 lub nowsza (flaga GPU została dodana w tej wersji).  
- Maszyna z włączonym GPU i odpowiednimi sterownikami (NVIDIA CUDA 11+ działa świetnie).  
- Plik obrazu, który chcesz przetworzyć — np. zeskanowany paragon, sfotografowaną fakturę lub odręczną notatkę.

Jeśli już je masz, świetnie — zanurzmy się.

## Krok 1: Jak włączyć GPU – Konfiguracja silnika OCR

Pierwszą rzeczą, którą musisz zrobić, jest poinformowanie Aspose OCR, aby używał GPU. Robi się to poprzez ustawienie właściwości `UseGpu` w instancji `OcrEngine`. Właściwość domyślnie ma wartość `false`, więc włączamy ją explicite.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // <-- GPU module namespace

// Create the OCR engine and enable GPU acceleration (available from version 24.2.0)
var ocrEngine = new OcrEngine
{
    // Enabling GPU can speed up recognition by 2‑5× on a modern card
    UseGpu = true
};
```

**Dlaczego to ważne:** Gdy `UseGpu` jest ustawione na `true`, biblioteka przenosi ciężkie obliczenia macierzowe na procesor graficzny. Na skromnym RTX 3060 zauważysz spadek opóźnienia z kilku sekund na obraz do ułamka sekundy.

> **Porada:** Jeśli uruchamiasz w środowisku CI bez interfejsu graficznego, upewnij się, że sterownik GPU jest zainstalowany i konto serwisowe ma uprawnienia do dostępu do urządzenia. W przeciwnym razie silnik cicho przełączy się w tryb CPU.

## Krok 2: Załaduj obraz do OCR – skieruj silnik na swój plik

Następnie musimy **załadować obraz do OCR**. Aspose OCR akceptuje każdy format obrazu obsługiwany przez System.Drawing (PNG, JPEG, BMP, TIFF itp.). Pomocnicza metoda `ImageStream.FromFile` opakowuje plik w wymagany obiekt strumienia.

```csharp
// Replace the path with the location of your receipt or document
string imagePath = @"C:\MyImages\receipt.jpg";

ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Jeśli wolisz ładować z `byte[]` (np. gdy obraz pochodzi z bazy danych), możesz użyć `ImageStream.FromBytes(byteArray)` — ten sam rezultat, tylko inne źródło.

## Krok 3: Jak rozpoznać tekst – uruchom proces OCR

Teraz, gdy silnik jest skonfigurowany i obraz załadowany, czas **rozpoznać tekst**. Metoda `Recognize` wykonuje całą ciężką pracę i zwraca obiekt `OcrResult`, który zawiera czysty tekst, wyniki pewności oraz nawet ramki ograniczające, jeśli będą potrzebne później.

```csharp
// Run the recognition process (English is the default language)
OcrResult ocrResult = ocrEngine.Recognize();
```

Możesz również zmienić język, ustawiając `ocrEngine.Language = OcrLanguage.French;` przed wywołaniem `Recognize()`. Przyspieszenie GPU działa niezależnie od załadowanego pakietu językowego.

## Krok 4: Jak wyodrębnić tekst z obrazu – wyświetl wynik

Na koniec **wyodrębniamy tekst z obrazu** odczytując właściwość `Text` obiektu wyniku. Dla celów demonstracyjnych po prostu wypiszemy go na konsolę, ale możesz zapisać go do pliku, bazy danych lub przekazać do innej usługi.

```csharp
// Output the extracted plain‑text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(ocrResult.Text);
```

**Oczekiwany wynik** (twój rzeczywisty tekst będzie się różnił w zależności od obrazu):

```
=== OCR RESULT ===
Store: Coffee Corner
Date: 03/28/2026
Item          Qty   Price
Latte          2    $5.00
Muffin         1    $2.50
Total                 $12.50
```

Jeśli potrzebujesz surowych wartości pewności, możesz iterować po `ocrResult.Regions` i sprawdzać każdą `Region.Confidence`.

## Pełny działający przykład – jeden plik, gotowy do uruchomienia

Poniżej znajduje się kompletny program. Skopiuj i wklej go do nowego projektu konsolowego, przywróć pakiet NuGet Aspose.OCR i naciśnij **F5**.

```csharp
// ------------------------------------------------------------
// How to enable gpu for OCR in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU module namespace

class Program
{
    static void Main()
    {
        // -------- Step 1: Enable GPU ----------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true   // <-- crucial for acceleration
        };

        // -------- Step 2: Load image ----------
        // Make sure the file exists; otherwise an exception is thrown.
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------- Step 3: Recognize text -------
        OcrResult ocrResult = ocrEngine.Recognize();

        // -------- Step 4: Extract text ----------
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Uwaga:** Zamień `YOUR_DIRECTORY/receipt.jpg` na rzeczywistą ścieżkę do swojego obrazu. Jeśli program zgłosi `FileNotFoundException`, sprawdź ponownie ścieżkę i uprawnienia do pliku.

## Częste pytania i przypadki brzegowe

### Co zrobić, gdy GPU nie zostanie wykryte?

Aspose OCR automatycznie przełączy się na tryb CPU i zapisze ostrzeżenie w logu. Aby sprawdzić, który tryb jest aktywny, sprawdź `ocrEngine.IsGpuEnabled` po konstrukcji — zwraca `true` tylko wtedy, gdy sterownik GPU został pomyślnie załadowany.

### Czy mogę przetwarzać wiele obrazów w pętli?

Oczywiście. Po prostu przenieś linię `ocrEngine.Image = …` do wewnątrz pętli `foreach (var file in files)`. Utrzymuj tę samą instancję `OcrEngine`; ponowne jej użycie eliminuje narzut związany z wielokrotnym przydzielaniem zasobów GPU.

```csharp
foreach (var file in Directory.GetFiles(@"C:\MyImages", "*.jpg"))
{
    ocrEngine.Image = ImageStream.FromFile(file);
    var result = ocrEngine.Recognize();
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Length} characters");
}
```

### Jak obsłużyć języki nie‑angielskie?

Ustaw język przed wywołaniem `Recognize()`:

```csharp
ocrEngine.Language = OcrLanguage.Spanish;   // or any supported language enum
```

Przyspieszenie GPU działa w ten sam sposób; zmienia się tylko model językowy.

### Co z dużymi, wysokiej rozdzielczości zdjęciami?

Jeśli napotkasz błędy braku pamięci, najpierw zmniejsz rozmiar obrazu. Aspose OCR udostępnia `ImageHelper.Resize` — szybki sposób na zmniejszenie bez utraty zbyt wielu szczegółów.

```csharp
ocrEngine.Image = ImageHelper.Resize(
    ImageStream.FromFile(imagePath), 
    maxWidth: 2000, 
    maxHeight: 2000);
```

## Podsumowanie

Omówiliśmy **jak włączyć GPU** dla Aspose OCR, pokazaliśmy, jak **załadować obraz do OCR**, przeprowadziliśmy **rozpoznawanie tekstu**, oraz zademonstrowaliśmy **wyodrębnianie tekstu z obrazu** przy użyciu zwięzłego, gotowego do produkcji programu w C#. Przełączając flagę `UseGpu`, uzyskasz zauważalny przyrost wydajności, szczególnie przy przetwarzaniu partii paragonów, faktur lub dowolnego strumienia dokumentów o dużej objętości.

Gotowy na kolejny krok? Spróbuj połączyć ten pipeline OCR z bazą danych, aby przechowywać wyodrębnione paragony, lub przekazać czysty tekst do modelu przetwarzania języka naturalnego w celu kategoryzacji wydatków. Możesz także zbadać kolekcję `OcrResult.Regions`, aby uzyskać współrzędne ramki ograniczającej i zbudować interfejs, który podświetla każde słowo na oryginalnym obrazie.

Szczęśliwego kodowania i ciesz się dodatkową mocą, jaką przyspieszenie GPU wnosi do Twoich zadań OCR!

---

![ilustracja jak włączyć gpu](gpu-ocr-diagram.png "ilustracja jak włączyć gpu")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}