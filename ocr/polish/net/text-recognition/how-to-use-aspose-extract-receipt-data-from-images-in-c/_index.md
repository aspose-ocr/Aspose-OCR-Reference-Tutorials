---
category: general
date: 2026-04-04
description: Dowiedz się, jak używać Aspose do wyodrębniania danych z paragonu, ładowania
  obrazu paragonu i rozpoznawania obrazu paragonu (OCR) przy użyciu kompletnego przykładu
  w C#. Przewodnik krok po kroku dla programistów.
draft: false
keywords:
- how to use aspose
- extract receipt data
- how to extract receipt
- load receipt image
- ocr receipt image
language: pl
og_description: Jak używać Aspose do wyodrębniania danych z paragonu ze zeskanowanego
  obrazu paragonu. Pełny kod C#, wyjaśnienia i wskazówki dotyczące przetwarzania obrazu
  paragonu przy użyciu OCR.
og_title: Jak używać Aspose – wyodrębniać dane z paragonów z obrazów
tags:
- Aspose
- OCR
- C#
- Receipt Processing
title: Jak korzystać z Aspose – wyodrębniać dane z paragonów z obrazów w C#
url: /pl/net/text-recognition/how-to-use-aspose-extract-receipt-data-from-images-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać Aspose – wyodrębniać dane z paragonu z obrazów w C#

Zastanawiałeś się kiedyś **jak używać Aspose**, aby wyciągnąć ustrukturyzowane informacje ze zdjęcia paragonu? Nie jesteś sam. Niezależnie od tego, czy tworzysz aplikację do śledzenia wydatków, czy automatyzujesz wprowadzanie faktur, problem jest ten sam: masz plik PNG lub JPEG i potrzebujesz nazwy sklepu, daty oraz kwoty całkowitej bez ręcznego wpisywania.

Sprawa jest prosta — Aspose.OCR sprawia, że cały ten proces staje się dziecinnie prosty. W tym samouczku przeprowadzimy Cię przez ładowanie obrazu paragonu, uruchamianie OCR i w końcu wyodrębnianie danych paragonu kilkoma liniami C#. Na koniec będziesz mieć działający program konsolowy, który wypisze nazwę sklepu, datę i kwotę całkowitą bezpośrednio w konsoli.

> **Szybki wynik:** Jeśli potrzebujesz tylko kodu, przejdź do sekcji „Kompletny działający przykład” na końcu i skopiuj‑wklej.

## Czego będziesz potrzebować

- **.NET 6.0 lub nowszy** (API działa z .NET Core i .NET Framework)
- **Aspose.OCR for .NET** pakiet NuGet (`Install-Package Aspose.OCR`)
- Przykładowy obraz paragonu (PNG, JPG lub BMP) zapisany lokalnie
- Visual Studio 2022 lub dowolny edytor obsługujący projekty C#

Nie są wymagane żadne inne biblioteki firm trzecich. Jedynym warunkiem wstępnym jest podstawowa znajomość aplikacji konsolowych w C# — jeśli napisałeś „Hello World”, jesteś gotowy.

## Krok 1 – Zainstaluj i odwołaj się do Aspose.OCR

Aby **jak używać Aspose**, najpierw potrzebujesz biblioteki w swoim projekcie. Otwórz Konsolę Menedżera Pakietów i uruchom:

```powershell
Install-Package Aspose.OCR
```

Alternatywnie, użyj interfejsu NuGet UI i wyszukaj „Aspose.OCR”. Po zainstalowaniu dodaj wymagane przestrzenie nazw na początku pliku:

```csharp
using Aspose.OCR;
using Aspose.OCR.Structured;
```

> **Pro tip:** Aktualizuj pakiety NuGet na bieżąco. Na dzień dzisiejszy (kwiecień 2026) najnowsza stabilna wersja to 23.11.0, która zawiera ulepszenia wydajności OCR dla wysokiej rozdzielczości paragonów.

## Krok 2 – Załaduj obraz paragonu

Gdy **ładujesz obraz paragonu**, masz dwa typowe źródła: lokalną ścieżkę lub strumień z żądania sieciowego. Dla tego samouczka zachowamy prostotę i odczytamy plik z dysku:

```csharp
// Step 2: Load the receipt image to be processed
var ocrEngine = new OcrEngine
{
    Language = Language.English // set language for better accuracy
};

ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.png");
```

Zastąp `YOUR_DIRECTORY/receipt.png` rzeczywistą ścieżką do pliku paragonu. Jeśli obsługujesz przesyłane przez użytkownika pliki, możesz przekazać `MemoryStream` do `ImageStream.FromStream`.

> **Dlaczego to ważne:** Określenie języka (English) informuje silnik OCR, jakiego zestawu znaków się spodziewać, co zmniejsza liczbę błędnych rozpoznawań — szczególnie istotne, gdy **ocr receipt image** zawiera liczby i symbole.

## Krok 3 – Uruchom OCR i przechwyć informacje o układzie

Krok OCR robi więcej niż tylko zwrócić surowy tekst; przechwytuje także układ, co jest kluczowe dla późniejszego wyodrębniania strukturalnego.

```csharp
// Step 3: Run OCR to generate text and layout information (required for structured extraction)
ocrEngine.Recognize();
```

Po zakończeniu `Recognize()` obiekt `ocrEngine` zawiera zarówno zwykły tekst, jak i pozycje każdego słowa. To podstawa dla kolejnego kroku, w którym poprosimy Aspose o **jak wyodrębnić paragon** automatycznie.

## Krok 4 – Zainicjuj rozpoznawanie układu

Aspose udostępnia klasę `LayoutRecognizer`, która wie, jak typowo zorganizowane są paragony (sklep na górze, linia daty, suma na dole). Po prostu przekaż skonfigurowany silnik OCR:

```csharp
// Step 4: Initialize the layout recognizer with the OCR engine
var layoutRecognizer = new LayoutRecognizer(ocrEngine);
```

W tle rozpoznawacz stosuje zestaw heurystyk — np. szuka symboli walutowych lub wzorców dat — aby mapować surowy tekst na pola semantyczne.

## Krok 5 – Wyodrębnij ustrukturyzowane dane paragonu

Teraz najprzyjemniejsza część: **wyodrębnić dane paragonu**. Jedno wywołanie metody wykonuje całą ciężką pracę:

```csharp
// Step 5: Extract structured receipt data (merchant, date, total amount)
var receiptData = layoutRecognizer.ExtractReceiptData();
```

`receiptData` jest obiektem typu `ReceiptData` (zdefiniowanym w `Aspose.OCR.Structured`). Zawiera trzy główne właściwości:

- `Merchant` – nazwa sklepu
- `Date` – data zakupu jako `DateTime` (jeśli wykryta)
- `TotalAmount` – całkowita kwota jako `decimal`

Jeśli silnik nie znajdzie konkretnego pola, właściwość będzie `null` lub `0`. W razie potrzeby możesz dodać logikę awaryjną (np. poprosić użytkownika o potwierdzenie).

## Krok 6 – Wyświetl wyodrębnione informacje

Na koniec wypisz wyniki w konsoli. To moment, w którym zobaczysz efekty swojej pracy:

```csharp
// Step 6: Display the extracted information
Console.WriteLine($"Merchant: {receiptData.Merchant}");
Console.WriteLine($"Date:     {receiptData.Date:d}");
Console.WriteLine($"Total:    {receiptData.TotalAmount:C}");
```

Formatowanie ciągów (`:d` i `:C`) generuje krótką datę oraz ciąg walutowy, co czyni wyjście czytelnym dla człowieka.

### Oczekiwany wynik

Zakładając, że paragon należy do „Coffee Corner”, datowany jest na 2025‑12‑01, a suma wynosi $4.75, konsola pokaże:

```
Merchant: Coffee Corner
Date:     12/1/2025
Total:    $4.75
```

Jeśli którekolwiek pole będzie brakować, zobaczysz pustą linię lub wartość domyślną — idealne do debugowania.

## Przypadki brzegowe i typowe pułapki

### 1. Obrazy o niskiej rozdzielczości
Jeśli obraz paragonu jest rozmazany lub ma mniej niż 150 dpi, dokładność OCR drastycznie spada. Przeskalowanie obrazu prostym filtrem dwuliniowym przed przekazaniem go do Aspose może poprawić wyniki.

```csharp
ocrEngine.Image = ImageStream.FromFile("receipt.png")
    .Resize(2.0, InterpolationMode.Bilinear);
```

### 2. Paragony nie‑angielskie
Podstawowy przykład używa `Language.English`. Dla wielojęzycznych paragonów ustaw `Language` na odpowiedni enum (np. `Language.French`) lub użyj `Language.AutoDetect`, jeśli nie jesteś pewien.

### 3. Wiele paragonów na jednym obrazie
Rozpoznawacz układu Aspose zakłada pojedynczy paragon na obraz. Jeśli masz zdjęcie kilku paragonów obok siebie, musisz wstępnie przetworzyć obraz — przyciąć każdy paragon do osobnego pliku przed uruchomieniem OCR.

### 4. Brak symbolu waluty
Czasami suma pojawia się bez znaku `$`. Rozpoznawacz nadal wykrywa liczby, ale możesz potrzebować dodatkowo przetworzyć ciąg, aby zapewnić prawidłowe rozmieszczenie miejsc dziesiętnych.

```csharp
if (receiptData.TotalAmount == 0 && rawText.Contains("Total"))
{
    // fallback parsing logic here
}
```

## Pro tipy dla produkcji

- **Cache'uj silnik OCR**, jeśli przetwarzasz wiele paragonów w partii; ponowne użycie tej samej instancji zmniejsza narzut alokacji.
- **Loguj surowy tekst OCR** (`ocrEngine.Text`) dla celów audytu. Jest to przydatne, gdy pole nie zostanie wyodrębnione.
- **Otocz cały przepływ blokiem try/catch** i zwróć przyjazny komunikat o błędzie (np. „Nie udało się odczytać paragonu, proszę przesłać wyraźniejszy obraz”).

## Kompletny działający przykład

Poniżej znajduje się samodzielna aplikacja konsolowa, którą możesz skompilować i uruchomić „tak jak jest”. Wystarczy podmienić ścieżkę do obrazu i jesteś gotowy.

```csharp
// ------------------------------------------------------------
// How to Use Aspose – Extract Receipt Data from Images (C#)
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Structured;

namespace ReceiptExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create and configure the OCR engine for English language
            var ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the receipt image you want to process
            // 👉 Make sure the file exists; otherwise an exception will be thrown.
            const string imagePath = "YOUR_DIRECTORY/receipt.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Run OCR – this also captures layout information
            ocrEngine.Recognize();

            // 4️⃣ Initialize the layout recognizer with the OCR engine
            var layoutRecognizer = new LayoutRecognizer(ocrEngine);

            // 5️⃣ Extract structured receipt data (merchant, date, total amount)
            var receiptData = layoutRecognizer.ExtractReceiptData();

            // 6️⃣ Display the extracted information
            Console.WriteLine($"Merchant: {receiptData.Merchant ?? "Not detected"}");
            Console.WriteLine($"Date:     {(receiptData.Date == DateTime.MinValue ? "Not detected" : receiptData.Date.ToShortDateString())}");
            Console.WriteLine($"Total:    {(receiptData.TotalAmount == 0 ? "Not detected" : receiptData.TotalAmount.ToString("C"))}");

            // Keep the console window open when debugging
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Uruchamianie kodu**

1. Utwórz nowy projekt konsolowy .NET (`dotnet new console -n ReceiptExtractor`).
2. Dodaj pakiet Aspose.OCR (`dotnet add package Aspose.OCR`).
3. Zamień wygenerowany `Program.cs` na powyższy fragment.
4. Umieść obraz paragonu w podanej ścieżce.
5. Zbuduj i uruchom (`dotnet run`).

Powinieneś zobaczyć nazwę sklepu, datę i sumę wydrukowane dokładnie tak, jak pokazano wcześniej.

## Podsumowanie

W tym przewodniku omówiliśmy **jak używać Aspose** do **ładowania obrazu paragonu**, uruchamiania **ocr receipt image**, a na koniec **wyodrębnić dane paragonu** przy użyciu kilku linijek kodu. Najważniejsze wnioski: Aspose.OCR wykonuje najcięższą pracę — po skonfigurowaniu silnika OCR, `LayoutRecognizer` przekształca surowy tekst w ustrukturyzowany obiekt, któremu możesz zaufać.

Co dalej? Spróbuj zapisać wyodrębnione wartości w bazie danych, wygenerować podsumowanie PDF paragonu lub przekazać je do modelu uczenia maszynowego w celu klasyfikacji wydatków. Możesz także eksperymentować z innymi typami dokumentów strukturalnych, takimi jak faktury czy etykiety wysyłkowe — `ExtractInvoiceData` w Aspose działa w bardzo podobny sposób.

Masz pytania dotyczące przypadków brzegowych lub chcesz zobaczyć, jak obsługiwać wielostronicowe PDF‑y? zostaw komentarz lub sprawdź oficjalną dokumentację Aspose.OCR dla zaawansowanych scenariuszy. Szczęśliwego kodowania i ciesz się prostotą **jak używać Aspose** w automatyzacji paragonów!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}