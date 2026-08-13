---
category: general
date: 2026-03-05
description: Jak używać OCR w C#, aby wyodrębnić tekst z obrazów paragonów. Dowiedz
  się, jak załadować obraz do OCR i rozpoznać obraz paragonu w kilka minut.
draft: false
keywords:
- how to use OCR
- extract text from receipt
- load image for OCR
- recognize receipt image
language: pl
og_description: jak używać OCR w C# do wyodrębniania tekstu z paragonów. Postępuj
  zgodnie z tym przewodnikiem krok po kroku, aby wczytać obraz do OCR i skutecznie
  rozpoznawać obraz paragonu.
og_title: jak używać OCR w C# – szybkie wyodrębnianie tekstu z paragonu
tags:
- OCR
- C#
- Aspose
- Receipt Processing
title: Jak używać OCR w C# – szybko wyodrębniaj tekst z paragonów
url: /pl/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-receipts-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak używać OCR w C# – Szybko wyodrębniaj tekst z paragonów

Zastanawiałeś się kiedyś **jak używać OCR**, aby wyciągnąć dane prosto ze zdjęcia paragonu spożywczego? Nie jesteś jedyny. W wielu aplikacjach małych firm wąskim gardłem jest przekształcenie rozmytego PNG w ustrukturyzowany tekst, z którym naprawdę można pracować.  

Dobre wieści? Kilka linijek C# i Aspose.OCR pozwala **załadować obraz do OCR**, uruchomić silnik i **rozpoznać obraz paragonu** w mniej niż minutę. Poniżej zobaczysz kompletny, gotowy do uruchomienia przykład oraz wskazówki dotyczące trudnych fragmentów, które pomijają większość tutoriali.

## Co obejmuje ten przewodnik

Przejdziemy przez wszystko, co musisz wiedzieć:

* Instalacja pakietu NuGet Aspose.OCR.  
* Konfiguracja silnika OCR – rdzeń **jak używać OCR** poprawnie.  
* Ładowanie pliku paragonu (to jest krok **load image for OCR**).  
* Uruchomienie procesu rozpoznawania i wyciągnięcie danych układu w formacie JSON i XML.  
* Radzenie sobie z typowymi problemami, takimi jak brak licencji lub nieobsługiwane formaty obrazów.  

Po zakończeniu będziesz mieć samodzielny program, który wyodrębnia tekst z dowolnego paragonu umieszczonego w folderze. Bez zewnętrznych usług, bez ukrytej magii.

## Wymagania wstępne

* .NET 6 SDK lub nowszy (kod kompiluje się również z .NET Core).  
* Ważny plik licencji Aspose.OCR (`Aspose.OCR.lic`). Możesz uzyskać darmową wersję próbną od Aspose, jeśli jeszcze jej nie masz.  
* Przykładowy obraz paragonu – `receipt.png` działa, ale każdy popularny format rastrowy się sprawdzi.  

Jeśli już je masz, świetnie – zanurzmy się.

![przykład użycia OCR](https://example.com/ocr-receipt.png "przykład użycia OCR")

## Krok 1: Zainstaluj Aspose.OCR i utwórz nowy projekt

Na początek potrzebujesz biblioteki, która naprawdę wykonuje ciężką pracę. Otwórz terminal w folderze projektu i uruchom:

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

To polecenie tworzy szkielet aplikacji konsolowej i pobiera najnowszy pakiet Aspose.OCR. Z mojego doświadczenia wynika, że krótkie nazwy projektu ułatwiają czytanie wygenerowanych ścieżek, zwłaszcza gdy zaczynasz obsługiwać wiele aplikacji demonstracyjnych.

## Krok 2: Zainicjalizuj silnik OCR – serce **jak używać OCR**

Teraz napiszemy kod, który odpowiada na pytanie „**jak używać OCR** w C#”. Otwórz `Program.cs` i zamień jego zawartość na poniższy fragment. Zwróć uwagę na komentarze – wyjaśniają *dlaczego* za każdą linijką, nie tylko *co*.

```csharp
using System;
using System.IO;
using Aspose.OCR;          // Aspose OCR namespace
using Aspose.OCR.Image;   // For loading images

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create and configure the OCR engine.
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // Why set a license? Without it the engine runs in evaluation mode,
        // which adds a watermark to the output and limits batch size.
        ocrEngine.SetLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Load the receipt image – this is the **load image for OCR** step.
        // -------------------------------------------------
        // Change the path to point at your own receipt file.
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");

        // The ImageStream class abstracts file I/O and supports many formats.
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣ Run the recognition process – this is where we **recognize receipt image**.
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Export the layout information as JSON.
        // -------------------------------------------------
        string jsonResult = ocrResult.ToJson();
        File.WriteAllText("receipt.json", jsonResult);
        Console.WriteLine("✅ JSON saved to receipt.json");

        // -------------------------------------------------
        // 5️⃣ Export the same layout information as XML.
        // -------------------------------------------------
        string xmlResult = ocrResult.ToXml();
        File.WriteAllText("receipt.xml", xmlResult);
        Console.WriteLine("✅ XML saved to receipt.xml");

        // -------------------------------------------------
        // 6️⃣ Quick preview – print the plain text to console.
        // -------------------------------------------------
        Console.WriteLine("\n--- Extracted Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Dlaczego to działa

* **`OcrEngine`** jest punktem wejścia; przechowuje całą konfigurację, którą możesz później dostosować (język, DPI itp.).  
* **`SetLicense`** usuwa znak wodny wersji ewaluacyjnej – kluczowy krok, gdy planujesz dystrybuować kod.  
* **`ImageStream.FromFile`** wykonuje zadanie **load image for OCR**, obsługując PNG, JPEG, BMP, TIFF i inne.  
* **`Recognize()`** to metoda, która faktycznie **recognize receipt image**. W tle wykonuje binaryzację, segmentację i klasyfikację znaków.  
* Eksport do JSON i XML zapewnia zarówno czytelny dla człowieka zrzut, jak i strukturę przyjazną maszynie, którą możesz przekazać do kolejnych parserów.

## Krok 3: Uruchom demo i zweryfikuj wynik

Skompiluj i uruchom:

```bash
dotnet run
```

Jeśli wszystko jest poprawnie podłączone, zobaczysz coś podobnego do:

```
✅ JSON saved to receipt.json
✅ XML saved to receipt.xml

--- Extracted Text ---
Walmart Supercenter
Date: 03/04/2026
Item    Qty   Price
Milk    2     2.58
Bread   1     1.99
Total   4.57
```

Konsola wypisuje czysty tekst, podczas gdy `receipt.json` i `receipt.xml` zawierają szczegółowe informacje o układzie (współrzędne, współczynniki pewności itp.). Te pliki są przydatne, jeśli później musisz dopasować każdą linię do pola w bazie danych.

## Przypadki brzegowe i porady profesjonalne

### 1️⃣ Brak lub nieprawidłowa licencja

Jeśli `SetLicense` nie powiedzie się, silnik przełączy się w tryb próbny i w wyniku pojawi się znak wodny. Umieść wywołanie w bloku try/catch i zaloguj przyjazny komunikat:

```csharp
try { ocrEngine.SetLicense("Aspose.OCR.lic"); }
catch (Exception ex)
{
    Console.WriteLine("⚠️ License not found – running in trial mode.");
    Console.WriteLine(ex.Message);
}
```

### 2️⃣ Nieobsługiwane formaty obrazów

Aspose.OCR obsługuje większość formatów rastrowych, ale jeśli podasz mu PDF lub wielostronicowy TIFF, najpierw musisz przekonwertować interesującą Cię stronę na obraz. Biblioteka `Aspose.PDF` może wykonać tę konwersję.

### 3️⃣ Duże paragony i wydajność

Przetwarzanie obrazu o wielkości 10 MB może być wolne. Zmniejsz rozdzielczość przed przekazaniem go do silnika:

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath).Resize(1024, 0);
```

Metoda `Resize` zachowuje proporcje (`0` dla wysokości) i znacznie zmniejsza rozmiar pliku, nie poświęcając dokładności OCR dla typowych paragonów.

### 4️⃣ Problemy z językiem i czcionką

Paragony mogą zawierać znaki specjalne (€, ¥ itp.). Ustaw język explicite, jeśli znasz lokalizację:

```csharp
ocrEngine.Language = Language.English; // or Language.Spanish, etc.
```

W przypadku paragonów wielojęzycznych możesz włączyć tryb wielojęzyczny:

```csharp
ocrEngine.Language = Language.English | Language.French;
```

### 5️⃣ Ekstrahowanie danych ustrukturyzowanych

Surowy tekst jest przydatny, ale większość aplikacji potrzebuje ustrukturyzowanych pól (data, suma, pozycje). Układ JSON zawiera współrzędne `BoundingBox` dla każdego słowa. Możesz go przetworzyć w ten sposób:

```csharp
var layout = Newtonsoft.Json.Linq.JObject.Parse(jsonResult);
foreach (var word in layout["Words"])
{
    string text = (string)word["Text"];
    // Simple heuristics: look for "$" or "Total"
}
```

Ten fragment pokazuje koncepcję; w produkcji prawdopodobnie użyjesz wyrażenia regularnego lub małego silnika reguł.

## Najczęściej zadawane pytania

**Q: Czy mogę uruchomić to na Linuxie?**  
A: Oczywiście. Aspose.OCR jest wieloplatformowy; wystarczy zainstalować środowisko .NET na swoim serwerze Linux i ten sam kod będzie działał.

**Q: Co zrobić, jeśli muszę przetwarzać dziesiątki paragonów na minutę?**  
A: Uruchom pętlę `Parallel.ForEach` i używaj jednego obiektu `OcrEngine` – jest on bezpieczny wątkowo dla operacji tylko do odczytu. Pamiętaj o obsłudze limitów jednoczesności licencji.

**Q: Czy to działa z mobilnymi zdjęciami zrobionymi pod kątem?**  
A: Silnik zawiera podstawowe prostowanie, ale przy mocno nachylonych obrazach warto najpierw przetworzyć je przy użyciu biblioteki do przetwarzania obrazów (np. OpenCV), aby wyprostować paragon.

## Pełny działający przykład (kopiuj‑wklej)

Poniżej znajduje się *cały* program, który możesz wkleić do `Program.cs`. Nie są potrzebne żadne inne pliki poza licencją i obrazem paragonu.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        try
        {
            ocrEngine.SetLicense("Aspose.OCR.lic");
        }
        catch (Exception)
        {
            Console.WriteLine("⚠️ Running in trial mode – license not found.");
        }

        // Load the image to be processed (load image for OCR)
        string imagePath = Path.Combine(Environment.CurrentDirectory, "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}