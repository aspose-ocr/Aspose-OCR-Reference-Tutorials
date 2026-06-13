---
category: general
date: 2026-03-17
description: samouczek OCR w C# – odkryj, jak wyodrębnić tekst z plików graficznych,
  odczytać tekst ze zdjęć WebP oraz konwertować obraz na tekst przy użyciu prostego
  OcrEngine.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: pl
og_description: Poradnik C# OCR pokazuje, jak wyodrębnić tekst z plików graficznych,
  odczytać tekst ze zdjęć WebP i przekształcić obraz w tekst przy użyciu kilku linijek
  kodu.
og_title: samouczek OCR w C# – wyodrębnij tekst z obrazów w kilka minut
tags:
- C#
- OCR
- Image Processing
title: 'Samouczek C# OCR: Wyodrębnianie tekstu z obrazów (WebP, zdjęcia) – Szybki
  przewodnik'
url: /pl/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Wyodrębnianie tekstu z obrazów (WebP, zdjęcie)

Czy kiedykolwiek potrzebowałeś **wyodrębnić tekst z obrazu** plików, ale nie wiedziałeś, od czego zacząć w C#? Może masz zrzut ekranu w formacie WebP, JPEG paragonu lub zeskanowaną stronę PDF i po prostu chcesz uzyskać znajdujące się w niej słowa. W tym **c# OCR tutorial** przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który odczytuje tekst ze zdjęcia, obsługuje WebP i inne nowoczesne formaty oraz konwertuje obraz na zwykły tekst — wszystko w kilku linijkach.

**Co z tego wynika?** Będziesz mógł przekształcić każde zdjęcie z tekstem w przeszukiwalne ciągi znaków, wprowadzić je do baz danych lub przekazać do kolejnych potoków AI. Bez magii, tylko solidny silnik OCR, kilka API .NET i jasne wyjaśnienia „dlaczego” każdego kroku.

## Co będziesz potrzebował

- **.NET 6 SDK** (lub nowszy). Poniższy kod kompiluje się z .NET 6+ i działa na Windows, Linux lub macOS.
- **Visual Studio 2022** lub dowolny edytor, którego preferujesz (VS Code również działa).
- Pakiet NuGet **`Microsoft.Windows.SDK.Contracts`** (udostępnia `Windows.Media.Ocr`). Zainstaluj za pomocą:

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- Plik obrazu, który chcesz przetworzyć – w tym samouczku użyjemy zdjęcia **WebP** o nazwie `photo.webp` umieszczonego w folderze o nazwie `YOUR_DIRECTORY`.

> Porada: Jeśli pracujesz na platformie nie‑Windows, możesz zamienić `OcrEngine` na bibliotekę wieloplatformową, taką jak **Tesseract**. Otaczający kod pozostaje praktycznie taki sam.

## Krok 1: Utwórz projekt C# OCR Tutorial

Najpierw utwórz nową aplikację konsolową. Otwórz terminal i uruchom:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Dodaj wymagany pakiet (jak pokazano powyżej) i otwórz projekt w swoim IDE. To szkielet daje nam czystą bazę dla **c# OCR tutorial**.

## Krok 2: Importuj przestrzenie nazw i przygotuj obraz

Potrzebujemy kilku dyrektyw `using`, aby kompilator wiedział, gdzie znaleźć `OcrEngine`, `SoftwareBitmap` i pomocnicze funkcje ładowania obrazów.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **Dlaczego te przestrzenie nazw?**  
> `Windows.Media.Ocr` zawiera klasę `OcrEngine`, która faktycznie wykonuje rozpoznawanie. `Windows.Graphics.Imaging` pozwala nam zdekodować obraz (w tym WebP) do `SoftwareBitmap`, który silnik może zrozumieć. Pomocniki `System.IO` i `Windows.Storage.Streams` ułatwiają ładowanie plików.

Teraz załaduj obraz. Wbudowany dekoder obsługuje WebP, HEIF, PNG, JPEG i inne, więc możesz **odczytać tekst z WebP** bez dodatkowych wtyczek.

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **Przypadek brzegowy:** Jeśli Twój obraz jest już czarno‑biały, możesz pominąć krok konwersji. Konwersja do odcieni szarości to niewielka poprawa wydajności i często zwiększa rozpoznawanie na zaszumionych zdjęciach.

## Krok 3: Uruchom silnik OCR – Rozpoznaj tekst ze zdjęcia

Oto serce **c# OCR tutorial**. Tworzymy instancję `OcrEngine`, podajemy jej bitmapę i wyciągamy rozpoznany tekst.

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Co się dzieje?**  
- `TryCreateFromUserProfileLanguages()` wybiera język(i) ustawione w profilu użytkownika Windows, co zazwyczaj obejmuje angielski, hiszpański itp. Jeśli potrzebujesz konkretnego języka, użyj `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))`.  
- `RecognizeAsync` wykonuje ciężką pracę w tle, zwracając `OcrResult`, który zawiera surowy ciąg znaków, ramki ograniczające słowa oraz wyniki pewności.  
- Na koniec wypisujemy `ocrResult.Text`, dając Ci wynik **convert image to text**, który możesz przekazać dalej.

## Krok 4: Pełny, uruchamialny przykład

Łącząc wszystko razem, oto samodzielny program, który możesz skopiować i wkleić do `Program.cs`. Kompiluje się, uruchamia i wypisuje tekst wyodrębniony z `photo.webp`.

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### Oczekiwany wynik

Jeśli `photo.webp` zawiera zdanie „Hello, world! This is a test.” zobaczysz coś podobnego:

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

Dokładne podziały linii zależą od układu obrazu źródłowego, ale wynik **extract text from image** będzie zawsze zwykłym ciągiem znaków, który możesz dalej przetwarzać.

## Częste pytania i przypadki brzegowe

### Czy to działa z innymi formatami obrazów?

Zdecydowanie tak. Używany dekoder (`BitmapDecoder`) automatycznie wykrywa JPEG, PNG, BMP, GIF, **WebP**, HEIF i inne. Dzięki temu możesz **odczytać tekst z WebP**, JPEG lub nawet TIFF bez zmiany kodu.

### Co zrobić, gdy silnik OCR zwraca niską pewność?

Możesz sprawdzić `ocrResult.Lines` oraz każdy `OcrWord` pod kątem `ConfidenceScore`. Jeśli wynik jest poniżej progu (np. 0.6), rozważ:

- Wstępne przetworzenie obrazu (zwiększenie kontrastu, wyostrzenie, prostowanie).  
- Użycie obrazu źródłowego o wyższej rozdzielczości.  
- Przejście na dedykowaną bibliotekę, taką jak **Tesseract**, dla wsparcia wielu języków.

### Jak obsłużyć wiele języków na jednym obrazie?

Utwórz osobne instancje `OcrEngine` dla każdego języka i uruchom je kolejno, lub użyj biblioteki obsługującej wykrywanie mieszanych języków. Dla wbudowanego silnika możesz przekazać obiekt `Language`:

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### Czy mogę uruchomić to na Linux/macOS?

API `Windows.Media.Ocr` jest dostępne tylko na Windows. Na platformach nie‑Windows zamień sekcję OCR na **Tesseract** (poprzez `Tesseract.Net.SDK`). Kod ładowania i wstępnego przetwarzania pozostaje identyczny, więc reszta tego **c# OCR tutorial** nadal ma zastosowanie.

## Porady pro dla lepszej dokładności

- **Resize** duże obrazy do maksymalnie 2000 px po najdłuższej stronie – silniki OCR działają szybciej przy umiarkowanych rozmiarach.  
- **Denoise** używając prostego rozmycia Gaussa, jeśli zdjęcie jest ziarniste.  
- **Deskew** bitmapę, jeśli tekst nie jest idealnie poziomy; `SoftwareBitmap` można obrócić przed przekazaniem do `OcrEngine`.  
- **Cache** instancję `OcrEngine`, jeśli przetwarzasz wiele obrazów w partii; wielokrotne tworzenie jej zwiększa narzut.

## Powiązane tematy do zbadania

- **Convert image to text** przy użyciu **Tesseract** dla projektów wieloplatformowych.  
- **Extract text from PDF** poprzez renderowanie każdej strony do obrazu najpierw.  
- **Batch OCR**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}