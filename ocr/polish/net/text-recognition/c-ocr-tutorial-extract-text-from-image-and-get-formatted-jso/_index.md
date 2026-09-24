---
category: general
date: 2026-01-13
description: samouczek c# OCR, który pokazuje, jak wyodrębnić tekst z obrazu, załadować
  obraz do OCR i sformatować wyjście JSON przy użyciu Aspose OCR. Naucz się serializować
  obiekt do JSON.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- format json output
- serialize object to json
- load image for ocr
language: pl
og_description: samouczek c# OCR, który krok po kroku prowadzi przez wyodrębnianie
  tekstu z obrazu, ładowanie obrazu do OCR oraz formatowanie wyjścia JSON przy użyciu
  Aspose OCR.
og_title: c# OCR tutorial – wyodrębnianie tekstu i formatowanie JSON
tags:
- OCR
- C#
- JSON
title: c# tutorial OCR – wyodrębnij tekst z obrazu i uzyskaj sformatowany JSON
url: /pl/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-get-formatted-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Wyodrębnianie tekstu z obrazu i formatowanie wyjścia JSON

Zastanawiałeś się kiedyś, jak **wyodrębnić tekst z obrazu** pliki w projekcie C# bez walki z niskopoziomowym przetwarzaniem pikseli? To problem, który rozwiązuje ten *c# ocr tutorial*. W ciągu kilku minut zobaczysz, jak **wczytać obraz do OCR**, uruchomić Aspose OCR i **sformatować wyjście JSON**, aby móc bezpośrednio przekazać dane do swojego API lub bazy danych.

Przejdziemy przez każdy wiersz kodu, wyjaśnimy, dlaczego każdy element ma znaczenie, i pokażemy dokładny JSON, którego możesz się spodziewać. Po zakończeniu będziesz mieć gotową do uruchomienia aplikację konsolową, która zamieni plik PNG faktury w czysty, wcięty JSON. Bez zbędnych ozdobników, po prostu praktyczne rozwiązanie, które możesz wstawić do dowolnego projektu .NET 6+.

## Co obejmuje ten c# ocr tutorial

- Instalacja pakietu NuGet Aspose.OCR  
- Wczytywanie pliku obrazu do przetwarzania OCR  
- Rozpoznawanie tekstu w języku angielskim (lub dowolnym obsługiwanym języku)  
- **Serializing the OCR result to JSON** z ładnym formatowaniem  
- Wyświetlanie JSON w konsoli i zapisywanie go, jeśli chcesz  

Wystarczy podstawowa znajomość C# i aktualny .NET SDK. Nic więcej. Jeśli jesteś ciekawy, jak **wyodrębnić tekst z obrazu** z plików faktur, paragonów lub zeskanowanych formularzy, czytaj dalej.

---

## Krok 1: Przygotowanie środowiska c# ocr tutorial

Zanim napiszesz jakikolwiek kod, upewnij się, że masz odpowiednie narzędzia:

1. **.NET 6 SDK or later** – możesz go pobrać ze strony Microsoft.  
2. **Visual Studio 2022** (Community działa dobrze) lub dowolny edytor, który lubisz.  
3. **Aspose.OCR NuGet package** – uruchom `dotnet add package Aspose.OCR` w folderze projektu.

> **Pro tip:** Jeśli używasz potoku CI, dodaj odwołanie do pakietu w swoim pliku `.csproj`, aby kompilacja przywracała go automatycznie.

---

## Krok 2: Wczytaj obraz do OCR

Pierwszy prawdziwy krok w naszym tutorialu to pobranie obrazu, który chcesz przetworzyć. Aspose OCR działa z popularnymi formatami, takimi jak PNG, JPEG i TIFF.

```csharp
using Aspose.OCR;
using System.Text.Json;

// Replace this with the actual path to your invoice image
string imagePath = @"C:\Invoices\invoice.png";

// Create an OcrImage instance from the file system
OcrImage inputImage = OcrImage.FromFile(imagePath);
```

> **Why this matters:** Wczytanie obrazu jako `OcrImage` daje silnikowi dostęp do danych bitmapy i informacji o DPI, co poprawia dokładność rozpoznawania. Pominięcie tego kroku lub podanie uszkodzonego pliku spowoduje wyjątek w czasie wykonania.

---

## Krok 3: Wyodrębnij tekst z obrazu

Teraz uruchamiamy silnik OCR. Metoda `Recognize` zwraca bogaty obiekt `OcrResult` zawierający surowy tekst, wyniki pewności i szczegóły układu.

```csharp
// Initialize the OCR engine – no license needed for a trial run
OcrEngine ocrEngine = new OcrEngine();

// Recognize English text (you can change the language enum if needed)
OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);
```

> **Edge case:** Jeśli musisz przetworzyć dokument wielojęzyczny, wywołaj `Recognize` dwa razy z różnymi wartościami `OcrLanguage` i połącz wyniki. Silnik jest wątkowo‑bezpieczny, więc możesz nawet równolegle przetwarzać duże partie.

---

## Krok 4: Serializacja obiektu do JSON – Formatowanie wyjścia JSON

Obiekt `OcrResult` jest zwykłą klasą C#, co oznacza, że możemy przekazać go do `System.Text.Json`. Włączając `WriteIndented`, uzyskujemy wyjście czytelne dla człowieka.

```csharp
// Serialize the OCR result with pretty printing
string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
{
    WriteIndented = true
});
```

> **What you get:** Ładnie wcięty ciąg JSON, który zawiera rozpoznany tekst, pewność oraz układ strony. To idealne rozwiązanie do logowania, wysyłania do usługi webowej lub przechowywania w bazie NoSQL.

---

## Krok 5: Wyświetlanie i (opcjonalnie) zapisywanie sformatowanego JSON

Na koniec wypisujemy JSON w konsoli. Możesz także zapisać go do pliku przy użyciu `File.WriteAllText`, jeśli wolisz.

```csharp
// Show the JSON in the console
Console.WriteLine(json);

// Optional: Save to a .json file next to the image
string jsonPath = Path.ChangeExtension(imagePath, ".json");
File.WriteAllText(jsonPath, json);
Console.WriteLine($"\nJSON saved to: {jsonPath}");
```

**Oczekiwany wynik w konsoli (skrócony dla przejrzystości):**

```json
{
  "Text": "Invoice #12345\nDate: 2025‑12‑01\nTotal: $250.00",
  "Confidence": 0.97,
  "Pages": [
    {
      "PageNumber": 1,
      "Blocks": [
        {
          "Text": "Invoice #12345",
          "Confidence": 0.99,
          "Rectangle": { "X": 50, "Y": 30, "Width": 200, "Height": 30 }
        }
        // …more blocks…
      ]
    }
  ]
}
```

Jeśli silnik OCR nie znajdzie żadnego tekstu, pole `Text` będzie pustym ciągiem, a `Confidence` będzie równe `0`. To dobry sygnał, aby ponownie sprawdzić jakość obrazu.

---

## Krok 6: Kompletny działający przykład

Łącząc wszystko razem, oto pełny program, który możesz skopiować i wkleić do nowej aplikacji konsolowej:

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonResultDemo
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the source image (replace with your own path)
        string imagePath = @"C:\Invoices\invoice.png";
        OcrImage inputImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Recognize text – this is the core of our c# ocr tutorial
        OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);

        // 4️⃣ Serialize the result with pretty formatting
        string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
        {
            WriteIndented = true
        });

        // 5️⃣ Output to console and optionally write to a file
        Console.WriteLine(json);
        string jsonPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"\nJSON saved to: {jsonPath}");
    }
}
```

Uruchom program (`dotnet run` z folderu projektu) i obserwuj, jak konsola wypisuje ładnie sformatowaną reprezentację JSON Twojej zeskanowanej faktury.

---

## Typowe pułapki i wskazówki (c# ocr tutorial Extras)

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Blank `Text` field** | Obraz ma niski kontrast lub jest obrócony. | Wstępnie przetwórz obraz (zwiększ kontrast, prostuj) lub użyj `OcrEngine.ImagePreprocess`. |
| **`System.DllNotFoundException`** | Brak natywnych plików binarnych Aspose OCR. | Upewnij się, że pakiet NuGet został poprawnie przywrócony oraz że architektura środowiska uruchomieniowego (x64/x86) odpowiada Twojemu systemowi operacyjnemu. |
| **Performance lag on large PDFs** | OCR przetwarza każdą stronę kolejno. | Równolegle przetwarzaj, tworząc osobne instancje `OcrEngine` dla każdej strony (silnik jest wątkowo‑bezpieczny). |
| **JSON too large** | Serializujesz wszystkie szczegóły, w tym ramki ograniczające. | Użyj DTO, które zawiera tylko `Text` i `Confidence` przed serializacją. |

> **Remember:** Celem tego tutorialu jest pokazanie czystego, end‑to‑end przepływu. Zawsze możesz przyciąć JSON lub dodać więcej metadanych później.

---

## Zakończenie

Właśnie ukończyłeś **c# ocr tutorial**, który wczytuje obraz, **wyodrębnia tekst z obrazu** i generuje **format json output** poprzez **serializing object to json**. Kroki są proste, kod gotowy do uruchomienia, a JSON jest idealnie wcięty do dalszego wykorzystania.

Co dalej? Spróbuj zamienić `OcrLanguage.English` na `OcrLanguage.French` lub przetworzyć folder z paragonami w pętli. Możesz także zbadać zapisywanie JSON bezpośrednio do Azure Blob Storage lub wprowadzanie go do modelu uczenia maszynowego.

Jeśli napotkasz problemy, sprawdź ponownie, czy ścieżka do obrazu jest poprawna oraz czy licencja Aspose OCR (jeśli ją posiadasz) jest załadowana przed wywołaniem `Recognize`. Szczęśliwego kodowania i niech wyniki OCR zawsze będą wyraźne!

---

*Obraz ilustrujący przepływ OCR (alt text: "c# ocr tutorial diagram showing load image, recognize text, serialize to JSON")*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}