---
category: general
date: 2026-04-26
description: Wyodrębnij tekst z obrazu w C# przy użyciu Aspose.OCR i dowiedz się,
  jak w kilka minut przekształcić obraz do formatów JSON i XML.
draft: false
keywords:
- extract text from image
- convert image to json
- convert image to xml
- Aspose OCR C#
- image to JSON C#
- image to XML C#
language: pl
og_description: Wyodrębnij tekst z obrazu w C# przy użyciu Aspose.OCR. Dowiedz się
  krok po kroku, jak natychmiast przekształcić wynik do formatu JSON i XML.
og_title: Wyodrębnij tekst z obrazu w C# – konwertuj do JSON i XML
tags:
- OCR
- C#
- Aspose
- JSON
- XML
title: Wyodrębnij tekst z obrazu w C# – konwertuj do JSON i XML
url: /pl/net/text-recognition/extract-text-from-image-in-c-convert-to-json-xml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tekstu z obrazu w C# – konwersja do JSON i XML

Kiedykolwiek potrzebowałeś **wyodrębnić tekst z obrazu** w projekcie .NET, ale utknąłeś przy pytaniu „jak właściwie uzyskać te dane?” Nie jesteś sam. W wielu rzeczywistych aplikacjach — myśl o przetwarzaniu faktur, skanowaniu paragonów czy weryfikacji identyfikatorów — pobranie surowych znaków z obrazu jest pierwszym, kluczowym krokiem.  

Dobre wieści? Dzięki Aspose.OCR możesz zrobić to w kilku linijkach, a następnie natychmiast **konwertować obraz do JSON** lub **konwertować obraz do XML** dla systemów downstream. W tym przewodniku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia kod, wyjaśnimy, dlaczego każdy element ma znaczenie, i pokażemy kilka sztuczek, aby uniknąć typowych pułapek.

---

## Czego będziesz potrzebować

- **.NET 6+** (dowolny aktualny SDK działa; przykład celuje w .NET 6)
- **Aspose.OCR for .NET** pakiet NuGet  
  ```bash
  dotnet add package Aspose.OCR
  ```
- Plik obrazu (PNG, JPG itp.), który zawiera tekst do wydrukowania; użyjemy `invoice.png` jako przykładu.
- Edytor kodu — Visual Studio, VS Code lub Rider — cokolwiek wolisz.

To wszystko. Bez dodatkowych silników OCR, bez zewnętrznych usług, tylko jeden pakiet NuGet.

## Krok 1: Konfiguracja silnika OCR – Jak wyodrębnić tekst z obrazu

Najpierw tworzymy instancję `OcrEngine` i wskazujemy na plik obrazu. Ten krok jest fundamentem; bez prawidłowo załadowanego obrazu silnik nie może nic rozpoznać.

```csharp
using Aspose.OCR;
using System.IO;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process
// Replace YOUR_DIRECTORY with the actual folder path
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");

// Optional: verify the image was loaded
if (ocrEngine.Image == null)
{
    throw new FileNotFoundException("Image not found. Check the path and filename.");
}
```

**Dlaczego to ma znaczenie:**  
- `OcrEngine` enkapsuluje wszystkie niskopoziomowe przetwarzanie obrazu (binaryzacja, prostowanie).  
- Ładowanie obrazu za pomocą `ImageStream.FromFile` zapewnia, że silnik odczytuje dokładne bajty, zachowując DPI i głębię kolorów — oba mogą wpływać na dokładność rozpoznawania.  

> **Wskazówka:** Jeśli Twoje obrazy źródłowe znajdują się w strumieniu (np. przesłane przez web API), użyj `ImageStream.FromStream(yourStream)` zamiast `FromFile`.

## Krok 2: Określ język, którego silnik ma się spodziewać – dokładne wyodrębnianie tekstu z obrazu

Aspose.OCR obsługuje wiele alfabetów. Określenie właściwego języka zawęża zestaw znaków i zwiększa dokładność.

```csharp
// Set the language; Latin covers English, French, German, etc.
ocrEngine.Language = Language.Latin;
```

**Dlaczego:**  
Gdy ustawisz `Language.Latin`, silnik OCR ignoruje cyrylicę lub azjatyckie glify, zmniejszając liczbę fałszywych trafień. Jeśli później będziesz musiał obsługiwać dokumenty wielojęzyczne, możesz przełączyć się na `Language.Multilingual` lub połączyć języki.

## Krok 3: Uruchom proces rozpoznawania – wyodrębnij tekst z obrazu w jednym wywołaniu

Teraz faktycznie rozpoznajemy tekst. Metoda `Recognize` zwraca obiekt `RecognitionResult`, który zawiera surowy tekst, wyniki pewności oraz nawet dane układu.

```csharp
// Perform OCR
RecognitionResult recognitionResult = ocrEngine.Recognize();

// Quick sanity check
if (recognitionResult == null || string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text was detected. Verify the image quality.");
    return;
}

// Print the raw extracted text to the console
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(recognitionResult.Text);
```

**Dlaczego:**  
Wywołanie `Recognize` raz wystarczy, ponieważ silnik wewnętrznie wykonuje przetwarzanie wstępne, segmentację i klasyfikację znaków. Właściwość `Text` zwraca zwykły ciąg znaków, idealny do logowania lub szybkiej weryfikacji.

## Krok 4: Konwersja wyniku do JSON – łatwe konwertowanie obrazu do JSON

Wiele nowoczesnych usług preferuje ładunki JSON. Aspose.OCR udostępnia wygodną metodę `ToJson`, która serializuje cały `RecognitionResult`, włącznie z wartościami pewności i ramkami ograniczającymi.

```csharp
// Serialize the result to JSON
string jsonResult = recognitionResult.ToJson();

// Save the JSON to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonResult);

Console.WriteLine("JSON file saved at YOUR_DIRECTORY/invoice.json");
```

**Dlaczego możesz chcieć JSON:**  
- **Interoperacyjność:** Aplikacje front‑end (React, Angular) mogą bezpośrednio konsumować JSON.  
- **Debugowanie:** JSON zawiera pewność dla każdego znaku, co pozwala oznaczyć słowa o niskiej pewności do ręcznej weryfikacji.  

> **Przypadek brzegowy:** Jeśli Twój system downstream potrzebuje tylko zwykłego tekstu, możesz wyodrębnić `recognitionResult.Text` i opakować go w własny obiekt JSON zamiast pełnego ładunku Aspose.

## Krok 5: Konwersja wyniku do XML – konwertowanie obrazu do XML dla starszych systemów

Niektóre przedsiębiorstwa wciąż polegają na schematach XML do wymiany danych. Metoda `ToXml` odzwierciedla `ToJson`, ale zwraca XML.

```csharp
// Serialize the result to XML
string xmlResult = recognitionResult.ToXml();

// Save the XML to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlResult);

Console.WriteLine("XML file saved at YOUR_DIRECTORY/invoice.xml");
```

**Dlaczego XML:**  
- **Walidacja schematu:** Możesz zdefiniować XSD, który odpowiada strukturze generowanej przez Aspose, zapewniając zgodność kontraktu.  
- **Integracja:** Starsze systemy ERP lub zarządzania dokumentami często parsują XML od razu po instalacji.

## Pełny działający przykład – kod wszystko‑w‑jednym

Poniżej znajduje się kompletny program, który łączy wszystko razem. Skopiuj i wklej go do nowego projektu konsolowego (`dotnet new console`) i uruchom.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Initialize OCR engine and load the image
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();
            // Adjust the path to point at your PNG/JPG file
            string imagePath = "YOUR_DIRECTORY/invoice.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image at {imagePath}");
                return;
            }

            // -------------------------------------------------
            // Step 2: Specify language (Latin for most European scripts)
            // -------------------------------------------------
            ocrEngine.Language = Language.Latin;

            // -------------------------------------------------
            // Step 3: Run OCR and get the result
            // -------------------------------------------------
            RecognitionResult result = ocrEngine.Recognize();

            if (result == null || string.IsNullOrWhiteSpace(result.Text))
            {
                Console.WriteLine("No text detected – check image quality or language setting.");
                return;
            }

            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();

            // -------------------------------------------------
            // Step 4: Convert to JSON (convert image to json)
            // -------------------------------------------------
            string json = result.ToJson();
            string jsonPath = "YOUR_DIRECTORY/invoice.json";
            File.WriteAllText(jsonPath, json);
            Console.WriteLine($"JSON output written to {jsonPath}");

            // -------------------------------------------------
            // Step 5: Convert to XML (convert image to xml)
            // -------------------------------------------------
            string xml = result.ToXml();
            string xmlPath = "YOUR_DIRECTORY/invoice.xml";
            File.WriteAllText(xmlPath, xml);
            Console.WriteLine($"XML output written to {xmlPath}");
        }
    }
}
```

**Oczekiwany wynik (konsola):**

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

JSON file saved at YOUR_DIRECTORY/invoice.json
XML file saved at YOUR_DIRECTORY/invoice.xml
```

Pliki JSON i XML będą zawierały bogatszą strukturę, na przykład:

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
  "Confidence": 0.96,
  "Blocks": [
    { "Text": "Invoice #12345", "Confidence": 0.98, "Rectangle": { "X": 12, "Y": 30, "Width": 200, "Height": 20 } },
    ...
  ]
}
```

```xml
<RecognitionResult>
  <Text>Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00</Text>
  <Confidence>0.96</Confidence>
  <Blocks>
    <Block>
      <Text>Invoice #12345</Text>
      <Confidence>0.98</Confidence>
      <Rectangle X="12" Y="30" Width="200" Height="20"/>
    </Block>
    ...
  </Blocks>
</RecognitionResult>
```

## Częste pytania i przypadki brzegowe

### Co zrobić, gdy obraz jest rozmyty lub obrócony?

Aspose.OCR automatycznie prostuje większość obrazów, ale w ekstremalnych przypadkach możesz chcieć wstępnie przetworzyć je za pomocą `ocrEngine.Image = ImageProcessor.Deskew(ocrEngine.Image)`. Dodanie niewielkiego zwiększenia kontrastu (`ImageProcessor.AdjustContrast`) może również poprawić wynik pewności.

### Czy mogę wyodrębnić tekst z plików PDF?

Tak — najpierw przekonwertuj każdą stronę PDF na obraz (np. używając Aspose.PDF lub darmowej biblioteki takiej jak PDFium), a następnie podaj te obrazy do tego samego przepływu OCR.

### Jak obsłużyć wiele języków w jednym dokumencie?

Ustaw `ocrEngine.Language = Language.Multilingual;` lub połącz konkretne języki:

```csharp
ocrEngine.Language = Language.English | Language.French | Language.German;
```

Pamiętaj, że szersze zestawy językowe mogą

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}