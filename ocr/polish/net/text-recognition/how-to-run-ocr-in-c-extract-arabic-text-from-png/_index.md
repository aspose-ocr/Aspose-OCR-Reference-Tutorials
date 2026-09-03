---
category: general
date: 2026-01-10
description: Jak szybko uruchomić OCR i wyodrębnić arabski tekst z obrazu. Dowiedz
  się, jak konwertować obraz na tekst, odczytywać tekst z pliku PNG i zobacz, jak
  wyodrębnić tekst za pomocą Aspose OCR.
draft: false
keywords:
- how to run OCR
- extract arabic text
- convert image to text
- read text from png
- how to extract text
language: pl
og_description: Jak uruchomić OCR w C# i wyodrębnić arabski tekst z obrazu PNG. Ten
  przewodnik pokazuje, jak przekształcić obraz w tekst i odczytać tekst z PNG krok
  po kroku.
og_title: Jak uruchomić OCR w C# – wyodrębnić arabski tekst z PNG
tags:
- OCR
- C#
- Aspose
title: Jak uruchomić OCR w C# – wyodrębnić arabski tekst z PNG
url: /pl/net/text-recognition/how-to-run-ocr-in-c-extract-arabic-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uruchomić OCR w C# – Wyodrębnić arabski tekst z PNG

Zastanawiałeś się kiedyś **jak uruchomić OCR** na zdjęciu zawierającym arabskie znaki? Nie jesteś sam. Wielu programistów napotyka problem, gdy muszą **wyodrębnić arabski tekst** z PNG, ale nie wiedzą, która biblioteka poradzi sobie ze skryptami od prawej do lewej bez problemów.  

W tym samouczku przeprowadzimy Cię przez wszystko, co musisz wiedzieć, aby **konwertować obraz na tekst**, **czytać tekst z PNG**, a w końcu **jak wyodrębnić tekst** przy użyciu Aspose.OCR w czystej aplikacji konsolowej C#. Po zakończeniu będziesz mieć gotowy do uruchomienia program, który wypisze arabski ciąg znaków bezpośrednio w Twoim terminalu.

## Co się nauczysz

- Zainstaluj i odwołaj się do pakietu NuGet Aspose.OCR.  
- Skonfiguruj silnik OCR pod wsparcie języka arabskiego.  
- Załaduj obraz PNG i uruchom proces rozpoznawania.  
- Pobierz i wyświetl wyodrębniony tekst.  
- Dostosuj ustawienia dla lepszej dokładności i obsłuż typowe pułapki.

Nie wymagana jest wcześniejsza znajomość OCR, wystarczy podstawowa znajomość C# oraz środowiska programistycznego .NET (Visual Studio, Rider lub `dotnet` CLI będą wystarczające).

---

## Jak uruchomić OCR – Konfiguracja Aspose OCR

### Krok 1: Dodaj pakiet NuGet Aspose.OCR

Pierwszą rzeczą, której potrzebujemy, jest sama biblioteka OCR. Aspose.OCR jest produktem komercyjnym, ale oferuje darmową wersję próbną, która doskonale sprawdza się w celach edukacyjnych.

```bash
# Using the .NET CLI
dotnet add package Aspose.OCR
```

Alternatywnie, otwórz **NuGet Package Manager** w Visual Studio, wyszukaj **Aspose.OCR** i kliknij **Install**.

> **Pro tip:** Jeśli planujesz używać biblioteki w pipeline CI, dodaj flagę `-v`, aby zablokować wersję, np. `dotnet add package Aspose.OCR -v 23.10`.

### Krok 2: Utwórz nowy projekt konsolowy (jeśli go nie masz)

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
```

Teraz masz świeży plik `Program.cs` gotowy do naszego kodu.

---

## Wyodrębnianie arabskiego tekstu – Pisanie kodu OCR

Poniżej znajduje się kompletny, gotowy do uruchomienia program. Zapisz go jako `Program.cs` (lub zastąp automatycznie wygenerowany plik).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Choose the language for recognition.
            // Here we use Arabic. You can swap this for
            // OcrLanguage.Korean, OcrLanguage.SerbianCyrillic, etc.
            // -------------------------------------------------
            ocrEngine.Language = OcrLanguage.Arabic;

            // -------------------------------------------------
            // Step 3: Load the image containing the text.
            // Replace the path with the location of your PNG.
            // -------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // Step 4: Run the OCR process.
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Display the extracted text.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### Dlaczego każdy wiersz ma znaczenie

- **`OcrEngine`**: Centralna klasa koordynująca ładowanie obrazu, wybór języka i rozpoznawanie.  
- **`Language = OcrLanguage.Arabic`**: Arabski używa skryptu od prawej do lewej i unikalnych glifów; ustawienie języka informuje silnik, aby zastosował odpowiednie modele znaków.  
- **`ImageStream.FromFile`**: Obsługuje PNG, JPEG, BMP i wiele innych formatów. Jeśli kiedykolwiek będziesz musiał odczytać z `MemoryStream` (np. przesłany plik), zamień to wywołanie odpowiednio.  
- **`Recognize()`**: Wykonuje ciężką pracę — analizę pikseli, segmentację i klasyfikację znaków.  
- **`ocrEngine.Text`**: Końcowy ciąg Unicode, gotowy do dalszego przetwarzania, przechowywania lub wyświetlania.

### Oczekiwany wynik

Jeśli `arabic_sample.png` zawiera frazę „مرحبا بالعالم” (Hello World), konsola wypisze:

```
=== Extracted Arabic Text ===
مرحبا بالعالم
```

Jeśli wynik wygląda na zniekształcony, sprawdź ponownie, czy obraz jest wyraźny, język ustawiony na arabski oraz czy wersja silnika OCR odpowiada dokumentacji.

---

## Konwersja obrazu na tekst – Dostosowywanie dokładności

Chociaż domyślne ustawienia działają dla większości czystych skanów, obrazy w rzeczywistych warunkach często wymagają dodatkowej troski.

| Ustawienie | Co robi | Kiedy używać |
|------------|----------|---------------|
| `ocrEngine.Config.Preprocess = true` | Włącza automatyczną binaryzację i usuwanie szumów. | Skanowane dokumenty z cieniami. |
| `ocrEngine.Config.Deskew = true` | Obraca obraz, aby skorygować niewielkie przechylenie. | Zdjęcia zrobione pod kątem. |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock` | Traktuje cały obraz jako jedną blok tekstu. | Proste podpisy lub jednowierszowe etykiety. |
| `ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزس شصضطظعغفقكلمنهوية"` | Ogranicza rozpoznawanie wyłącznie do znaków arabskich. | Zmniejsza liczbę fałszywych trafień na stronach wielojęzycznych. |

Możesz dodać te linie zaraz po utworzeniu silnika:

```csharp
ocrEngine.Config.Preprocess = true;
ocrEngine.Config.Deskew = true;
ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزسشصضطظعغفقكلمنهوية";
```

---

## Odczytywanie tekstu z PNG – Obsługa różnych źródeł obrazu

Czasami PNG znajduje się w bazie danych lub pochodzi z żądania sieciowego. Oto szybka wersja, która odczytuje z `byte[]`:

```csharp
byte[] pngBytes = File.ReadAllBytes("YOUR_DIRECTORY/arabic_sample.png");
using var ms = new MemoryStream(pngBytes);
ocrEngine.Image = ImageStream.FromStream(ms);
ocrEngine.Recognize();
Console.WriteLine(ocrEngine.Text);
```

Reszta przepływu pozostaje identyczna, co oznacza, że **jak wyodrębnić tekst** jest spójne niezależnie od źródła.

---

## Jak wyodrębnić tekst – Zaawansowane opcje i przypadki brzegowe

### 1. Wielostronicowe PDF‑y lub TIFF‑y

Jeśli potrzebujesz wykonać OCR na wielostronicowym dokumencie, przeiteruj każdą stronę:

```csharp
var pdfDoc = new Aspose.Pdf.Document("multi_page.pdf");
foreach (var page in pdfDoc.Pages)
{
    using var img = page.ConvertToImage();
    ocrEngine.Image = ImageStream.FromBitmap(img);
    ocrEngine.Recognize();
    Console.WriteLine($"Page {page.Number}: {ocrEngine.Text}");
}
```

> **Uwaga:** Do tego fragmentu będziesz potrzebował pakietu `Aspose.PDF`.

### 2. Automatyczne wykrywanie języka

Aspose.OCR oferuje także auto‑detekcję, ale jest wolniejsza. Jeśli nie jesteś pewien, czy obraz zawiera arabski czy inny skrypt, włącz ją:

```csharp
ocrEngine.Language = OcrLanguage.AutoDetect;
```

Silnik wypróbuje każdy model językowy i wybierze najlepsze dopasowanie.

### 3. Wskazówki dotyczące wydajności

- **Ponowne użycie obiektu `OcrEngine`** dla wielu obrazów; tworzenie nowej instancji za każdym razem zwiększa narzut.  
- **Uruchamianie równolegle** tylko wtedy, gdy masz osobne instancje silnika na wątek — współdzielenie jednej instancji powoduje warunki wyścigu.

---

## Podsumowanie

Omówiliśmy **jak uruchomić OCR** w C# od początku do końca, pokazując jak **wyodrębnić arabski tekst**, **konwertować obraz na tekst**, **odczytać tekst z PNG**, oraz odpowiedzieć na **jak wyodrębnić tekst** w różnych scenariuszach. Przykładowy kod jest kompletny, samodzielny i gotowy do wklejenia w dowolnym projekcie konsolowym .NET.

Kolejne kroki? Spróbuj zamienić `OcrLanguage.Arabic` na koreański lub serbski cyryliczny, aby zobaczyć wielojęzyczną moc biblioteki. Eksperymentuj z flagami przetwarzania wstępnego, aby zwiększyć dokładność przy szumnych skanach, lub zintegrować procedurę OCR z API webowym, aby użytkownicy mogli przesyłać obrazy i otrzymywać natychmiastowe wyniki tekstowe.

Miłego kodowania i niech wyniki OCR zawsze będą krystalicznie czyste!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}