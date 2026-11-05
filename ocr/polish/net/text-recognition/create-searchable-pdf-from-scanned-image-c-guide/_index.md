---
category: general
date: 2026-04-26
description: Utwórz przeszukiwalny PDF ze zeskanowanego obrazu przy użyciu Aspose
  OCR w C#. Dowiedz się, jak konwertować zeskanowany obraz, wyodrębniać tekst i szybko
  generować przeszukiwalny PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned image
- extract text from image
- how to ocr document
- convert tiff to pdf
language: pl
og_description: Utwórz przeszukiwalny PDF ze skanowanego obrazu przy użyciu Aspose
  OCR. Krok po kroku kod C#, który konwertuje, wyodrębnia tekst i generuje przeszukiwalny
  PDF.
og_title: Utwórz przeszukiwalny PDF ze zeskanowanego obrazu – przewodnik C#
tags:
- Aspose OCR
- C#
- PDF
- OCR
title: Utwórz przeszukiwalny PDF ze zeskanowanego obrazu – przewodnik C#
url: /pl/net/text-recognition/create-searchable-pdf-from-scanned-image-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie przeszukiwalnego PDF z zeskanowanego obrazu – przewodnik C#

Kiedykolwiek potrzebowałeś **utworzyć przeszukiwalny PDF** z papierowych umów, paragonów lub starych archiwów? Nie jesteś sam — większość programistów napotyka ten problem, gdy klient przekazuje stertę skanów TIFF i oczekuje przeszukiwalnego PDF jako finalnego produktu.  

W tym samouczku pokażemy dokładnie **jak wykonać OCR dokumentu** i zamienić zeskanowany obraz w **przeszukiwalny PDF** przy użyciu Aspose OCR dla .NET. Po zakończeniu będziesz w stanie **konwertować pliki ze zeskanowanymi obrazami**, **wyodrębniać tekst z obrazu** oraz obsługiwać wielostronicowe TIFF‑y bez problemu.

## Co będzie potrzebne

Zanim przejdziemy dalej, upewnij się, że masz:

* .NET 6.0 lub nowszy (API działa z .NET Core, .NET Framework i .NET 5+).  
* Ważną licencję Aspose OCR lub akceptujesz znak wodny wersji ewaluacyjnej.  
* Zainstalowany pakiet NuGet `Aspose.OCR` (`dotnet add package Aspose.OCR`).  
* Przykładowy plik TIFF (np. `contract_scan.tif`), który chcesz zamienić w przeszukiwalny PDF.

To wszystko — żadnych dodatkowych bibliotek, żadnej szalonej konfiguracji. Gotowy? Zaczynamy.

![Przykład tworzenia przeszukiwalnego PDF](create-searchable-pdf.png "przykład tworzenia przeszukiwalnego pdf")

## Krok 1 – Inicjalizacja silnika OCR (Create Searchable PDF)

Na początek potrzebujesz instancji `OcrEngine`. Ten obiekt jest „kołem zamachowym”, które odczytuje bitmapę, rozpoznaje znaki i zwraca tekst.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine which language to look for – Latin works for most English documents
ocrEngine.Language = Language.Latin;
```

**Dlaczego ustawiamy język?**  
Jeśli pozostawisz domyślne ustawienie, Aspose będzie próbował wszystkie pakiety językowe, co spowalnia działanie. Określenie `Language.Latin` mówi silnikowi, aby skupił się na alfabecie łacińskim, co przyspiesza proces i daje dokładniejsze wyniki dla kontraktów w języku angielskim.

## Krok 2 – Załaduj zeskanowany obraz (Convert Scanned Image)

Teraz przekazujemy silnikowi obraz, który ma zostać przetworzony. Aspose może odczytać ścieżkę pliku, strumień lub nawet `byte[]`. Dla prostoty użyjemy `ImageStream.FromFile`.  

```csharp
// Load the TIFF (or any supported image format)
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\contract_scan.tif");
```

Jeśli kiedykolwiek będziesz musiał **konwertować TIFF na PDF**, pamiętaj, że wielostronicowe TIFF‑y są obsługiwane automatycznie — każda klatka staje się osobną stroną PDF.

## Krok 3 – Uruchom OCR i pobierz tekst (Extract Text From Image)

Uruchomienie OCR jest tak proste, jak wywołanie `Recognize`. Silnik zwróci `RecognitionResult`, który zawiera czysty tekst, oceny pewności i informacje o układzie.  

```csharp
// Perform the OCR operation
RecognitionResult result = ocrEngine.Recognize();

// The raw text is available via the Text property
string extractedText = result.Text;

// Quick sanity check – print the first 200 characters
Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**Wskazówka:** Jeśli potrzebujesz jedynie tekstu (bez PDF), możesz zatrzymać się tutaj i zapisać `extractedText` do pliku `.txt`. Jednak najczęściej naszym celem jest przeszukiwalny PDF, więc kontynuujemy.

## Krok 4 – Zapisz jako przeszukiwalny PDF (Create Searchable PDF)

Aspose upraszcza ostatni krok: po prostu wywołaj `Save` z `SaveFormat.PdfSearchable`. Biblioteka wstawia wyodrębniony tekst jako niewidoczną warstwę, zachowując jednocześnie oryginalny wygląd obrazu.  

```csharp
// Save the result as a searchable PDF
ocrEngine.Save(@"C:\Docs\contract_searchable.pdf", SaveFormat.PdfSearchable);
```

Gdy otworzysz `contract_searchable.pdf` w dowolnym przeglądarce PDF, będziesz mógł zaznaczać, kopiować i wyszukiwać tekst — dokładnie to, czego klient oczekuje od „przeszukiwalnego PDF”.

## Obsługa wielostronicowych TIFF‑ów (Convert Tiff to PDF)

Jeśli plik źródłowy zawiera kilka stron, Aspose automatycznie potraktuje każdą klatkę jako osobną stronę. Nie są potrzebne dodatkowe pętle. Możesz jednak chcieć kontrolować DPI lub jakość obrazu dla każdej strony:

```csharp
// Optional: tweak image processing settings before OCR
ocrEngine.ImageProcessingOptions.Dpi = 300; // higher DPI improves accuracy
ocrEngine.ImageProcessingOptions.Compression = ImageCompression.Jpeg;
```

Po ustawieniu tych opcji, powtórz **Krok 2** dla każdej klatki lub po prostu wskaż `ImageStream.FromFile` na wielostronicowy TIFF i pozwól Aspose wykonać ciężką pracę.

## Typowe pułapki i jak je naprawić

| Objaw | Prawdopodobna przyczyna | Rozwiązanie |
|-------|--------------------------|-------------|
| Tekst jest zniekształcony lub brak go | Nieprawidłowy język | Ustaw `ocrEngine.Language` na właściwy pakiet językowy (np. `Language.German`). |
| PDF jest ogromny (10 MB dla jednosktronicowego skanu) | Domyślna kompresja obrazu jest niska | Dostosuj `ocrEngine.ImageProcessingOptions.Compression` na `Jpeg` i ustaw rozsądną wartość `Quality` (0‑100). |
| OCR działa bardzo wolno | Używanie domyślnego wykrywania języka `Auto` | Jawnie ustaw oczekiwany język. |
| Brak warstwy przeszukiwalnej | Zapisano z `SaveFormat.Pdf` zamiast `PdfSearchable` | Użyj `PdfSearchable`. |

## Pełny przykład od początku do końca

Łącząc wszystko w jedną całość, oto gotowa aplikacja konsolowa, którą możesz skopiować i wkleić do Visual Studio:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.Latin,
                // Optional: improve accuracy for low‑resolution scans
                ImageProcessingOptions = { Dpi = 300, Compression = ImageCompression.Jpeg }
            };

            // 2️⃣ Load the scanned image (convert scanned image)
            string inputPath = @"C:\Docs\contract_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Run OCR and extract text (extract text from image)
            RecognitionResult result = ocrEngine.Recognize();
            Console.WriteLine("First 200 characters of extracted text:");
            Console.WriteLine(result.Text.Substring(0, Math.Min(200, result.Text.Length)));

            // 4️⃣ Save as searchable PDF (create searchable pdf)
            string outputPath = @"C:\Docs\contract_searchable.pdf";
            ocrEngine.Save(outputPath, SaveFormat.PdfSearchable);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Co zobaczysz:**  
* Okno konsoli wypisujące fragment tekstu po OCR.  
* Plik `contract_searchable.pdf` leżący obok oryginalnego TIFF‑a. Otwórz go, naciśnij **Ctrl + F** i wyszukaj dowolne słowo, które znajdowało się w pierwotnym skanie — gotowe, działa.

## Kolejne kroki i powiązane tematy

* **Jak wykonywać OCR dokumentów** wsadowo – otocz powyższy kod pętlą `foreach` i przetwarzaj cały folder.  
* **Konwertuj zeskanowane obrazy** innych formatów niż TIFF (PNG, JPEG) – to samo API działa; wystarczy zmienić rozszerzenie pliku.  
* **Wyodrębniaj tekst z obrazu** do dalszej analizy – przekaż `result.Text` do potoku przetwarzania języka naturalnego.  
* **Optymalizuj rozmiar PDF** – zapoznaj się z `PdfSaveOptions`, aby dalej kompresować obrazy lub osadzać czcionki tylko w razie potrzeby.  

Eksperymentuj z tymi pomysłami, a szybko staniesz się osobą, do której wszyscy zwracają się z prośbą o „przekształcenie tego skanu w przeszukiwalny PDF”.

---

### TL;DR

Teraz wiesz, jak **tworzyć przeszukiwalne PDF** z zeskanowanych obrazów przy użyciu Aspose OCR w C#. Proces wygląda tak: inicjalizujesz silnik, ładujesz obraz, uruchamiasz OCR i zapisujesz z `PdfSearchable`. Dostosuj ustawienia języka, DPI i kompresji, aby radzić sobie z trudnymi przypadkami, i jesteś gotowy do **konwertowania zeskanowanych obrazów**, **wyodrębniania tekstu z obrazu** oraz nawet **konwertowania TIFF‑ów na PDF** w dużej skali. Powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}