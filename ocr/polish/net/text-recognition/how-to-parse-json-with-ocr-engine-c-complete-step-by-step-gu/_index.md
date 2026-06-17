---
category: general
date: 2026-03-17
description: Dowiedz się, jak parsować JSON z wyników OCR w C#. Ten samouczek opisuje,
  jak wyodrębnić tekst, wczytać obraz do OCR, uruchomić rozpoznawanie OCR oraz efektywnie
  korzystać z silnika OCR w C#.
draft: false
keywords:
- how to parse json
- how to extract text
- load image for OCR
- run OCR recognition
- use OCR engine C#
language: pl
og_description: Jak parsować JSON z wyniku OCR w C#. Postępuj zgodnie z naszym przewodnikiem,
  aby wyodrębnić tekst, załadować obraz do OCR, uruchomić rozpoznawanie OCR i używać
  silnika OCR w C#.
og_title: Jak parsować JSON przy użyciu silnika OCR w C# – pełny poradnik
tags:
- C#
- OCR
- JSON
- Image Processing
title: Jak parsować JSON przy użyciu silnika OCR w C# – Kompletny przewodnik krok
  po kroku
url: /pl/net/text-recognition/how-to-parse-json-with-ocr-engine-c-complete-step-by-step-gu/
---

/products-backtop-button >}}

All unchanged.

Make sure to keep markdown formatting.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak parsować JSON przy użyciu silnika OCR w C# – Kompletny przewodnik krok po kroku

Zastanawiałeś się kiedyś **jak parsować json**, który pochodzi bezpośrednio z silnika OCR? Nie jesteś sam. Większość programistów napotyka ten sam problem — otrzymują surowy JSON, a potem muszą znaleźć najlepszy sposób na wyodrębnienie przydatnych elementów, takich jak wyniki pewności (confidence scores) czy sam tekst. W tym przewodniku przeprowadzimy Cię przez ładowanie obrazu do OCR, uruchamianie rozpoznawania OCR i w końcu **jak parsować json** w czysty, łatwy do utrzymania sposób.

Na koniec tutorialu będziesz w stanie:

* Załadować obraz do OCR przy użyciu kilku linijek kodu.  
* Uruchomić rozpoznawanie OCR przy użyciu silnika OCR w C#.  
* **Jak wyodrębnić tekst** i inne metadane z ładunku JSON.  
* Obsłużyć typowe przypadki brzegowe (brakujące pola, nieoczekiwane formaty) bez awarii.

Nie potrzebujesz zewnętrznej dokumentacji — wszystko, czego potrzebujesz, znajduje się tutaj.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz:

* .NET 6.0 lub nowszy (kod kompiluje się również na .NET Framework 4.7+).  
* Odwołanie do biblioteki OCR, której używasz (przykład używa hipotetycznej klasy `OcrEngine`).  
* Pakiet NuGet `Newtonsoft.Json` do obsługi JSON (`Install-Package Newtonsoft.Json`).  
* Plik obrazu (np. `passport.png`) umieszczony w miejscu, które aplikacja może odczytać.

> **Pro tip:** Jeśli używasz komercyjnego SDK OCR, sprawdź, czy format wyjściowy JSON jest włączony — większość dostawców udostępnia go poprzez właściwość konfiguracyjną, taką jak `ocrEngine.Config.OutputFormat`.

## Krok 1 – Utwórz i skonfiguruj silnik OCR (Główne słowo kluczowe w akcji)

Pierwszą rzeczą, którą musisz zrobić, jest utworzenie instancji silnika OCR i ustawienie go tak, aby zwracał JSON. To właśnie tutaj fraza **jak parsować json** pojawia się po raz pierwszy w naszym kodzie, ponieważ silnik przekaże nam ciąg JSON, który później sparsujemy.

```csharp
using System;
using Newtonsoft.Json.Linq;   // For JSON parsing
// Assume OcrEngine, OutputFormat, and ImageStream live in the OCR SDK namespace
using OcrSdk;                  // <-- replace with the real namespace

// Step 1: Create an OCR engine instance and set JSON output
var ocrEngine = new OcrEngine();
ocrEngine.Config.OutputFormat = OutputFormat.Json;
```

**Dlaczego to ważne:** Ustawienie `OutputFormat` na `Json` zapewnia, że odpowiedź zawiera zarówno rozpoznany tekst **jak i** przydatne metadane, takie jak wyniki pewności. Jeśli pominiesz ten krok, otrzymasz zwykły tekst, a **jak parsować json** stanie się nieistotne.

## Krok 2 – Załaduj obraz do OCR

Teraz ładujemy obraz, który chcemy przeanalizować. To dokładnie miejsce, w którym drugorzędne słowo kluczowe **load image for OCR** błyszczy.

```csharp
// Step 2: Load the image you want to recognize
// Make sure the path points to a real file; otherwise an exception is thrown.
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY\passport.png");
```

> **Co jeśli plik nie istnieje?** Owiń wywołanie w `try/catch` i wyświetl przyjazny komunikat — Twoja aplikacja nie ulegnie awarii, a użytkownicy będą wiedzieć, co poszło nie tak.

## Krok 3 – Uruchom rozpoznawanie OCR

Po przygotowaniu silnika i załadowaniu obrazu, następnym logicznym krokiem jest faktyczne uruchomienie procesu rozpoznawania. To spełnia drugorzędne słowo kluczowe **run OCR recognition**.

```csharp
// Step 3: Execute OCR and get the raw result object
var ocrResult = ocrEngine.Recognize();
```

Właściwość `ocrResult.Text` zawiera teraz ciąg JSON. Jeśli wydrukujesz go w konsoli, zobaczysz coś podobnego do:

```json
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}
```

## Krok 4 – Jak wyodrębnić tekst (i inne pola) z JSON

Oto sedno tutorialu: **jak parsować json** i **jak wyodrębnić tekst** z ładunku OCR. Użyjemy `Newtonsoft.Json.Linq.JObject` ze względu na jego elastyczność.

```csharp
// Step 4: Output the raw JSON (optional, helps debugging)
Console.WriteLine("Raw OCR JSON:");
Console.WriteLine(ocrResult.Text);
Console.WriteLine();

// Step 5: Parse the JSON into a JObject
JObject jsonObject = JObject.Parse(ocrResult.Text);

// Extract the overall confidence score
var overallConfidence = jsonObject["OverallConfidence"]?.Value<double>() ?? 0.0;
Console.WriteLine($"Overall confidence: {overallConfidence:P0}");

// Extract the text from the first page (how to extract text)
string pageText = jsonObject["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
Console.WriteLine("Extracted text:");
Console.WriteLine(pageText);
```

**Dlaczego używać `JObject`?** Pozwala bezpiecznie poruszać się po drzewie JSON bez definiowania pełnej klasy modelu C#. Operatory warunkowe (`?.`) chronią przed `NullReferenceException`, jeśli silnik OCR pominie jakieś pole.

### Obsługa przypadków brzegowych

* **Brakujące pola:** Wzorzec `?.Value<T>() ?? default` zwraca rozsądny domyślny wynik.  
* **Wiele stron:** Iteruj po `jsonObject["Pages"]`, jeśli spodziewasz się więcej niż jednej strony.  
* **Niewartość numeryczna confidence:** Użyj `double.TryParse`, jeśli SDK czasami zwraca ciąg znaków.

## Krok 5 – Zadbaj o wszystko w wielokrotnego użytku metodzie

Aby uniknąć kopiowania tego samego kodu szablonowego, zamknij cały przepływ w metodzie pomocniczej. To także pokazuje **use OCR engine C#** w czysty, wielokrotnego użytku sposób.

```csharp
public static void RunOcrAndParseJson(string imagePath)
{
    // 1️⃣ Create engine & set JSON output
    var engine = new OcrEngine();
    engine.Config.OutputFormat = OutputFormat.Json;

    // 2️⃣ Load image (load image for OCR)
    engine.Image = ImageStream.FromFile(imagePath);

    // 3️⃣ Run OCR (run OCR recognition)
    var result = engine.Recognize();

    // 4️⃣ Show raw JSON (optional)
    Console.WriteLine("=== Raw JSON ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();

    // 5️⃣ Parse JSON (how to parse json)
    JObject obj = JObject.Parse(result.Text);

    // 6️⃣ Extract useful data (how to extract text)
    double confidence = obj["OverallConfidence"]?.Value<double>() ?? 0.0;
    string text = obj["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;

    Console.WriteLine($"Overall confidence: {confidence:P0}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(text);
}
```

Teraz możesz wywołać `RunOcrAndParseJson(@"C:\Images\passport.png");` z `Main` lub dowolnego innego miejsca w aplikacji.

## Pełny działający przykład

Poniżej znajduje się kompletny, samodzielny program konsolowy, który możesz skopiować i wkleić do nowego projektu `.csproj`. Zawiera wszystkie elementy, o których rozmawialiśmy, oraz odrobinę obsługi błędów.

```csharp
// File: Program.cs
using System;
using Newtonsoft.Json.Linq;
using OcrSdk;               // Replace with the actual namespace of your OCR library

class Program
{
    static void Main()
    {
        try
        {
            // Adjust the path to point at a real image on your machine
            string imagePath = @"YOUR_DIRECTORY\passport.png";

            RunOcrAndParseJson(imagePath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Unexpected error: {ex.Message}");
        }
    }

    /// <summary>
    /// Demonstrates how to parse JSON returned by an OCR engine,
    /// and how to extract text, confidence, and other metadata.
    /// </summary>
    /// <param name="imagePath">Full path to the image file.</param>
    public static void RunOcrAndParseJson(string imagePath)
    {
        // 1️⃣ Initialize OCR engine (use OCR engine C#)
        var engine = new OcrEngine();
        engine.Config.OutputFormat = OutputFormat.Json;

        // 2️⃣ Load image for OCR
        engine.Image = ImageStream.FromFile(imagePath);

        // 3️⃣ Run OCR recognition
        var result = engine.Recognize();

        // 4️⃣ Print raw JSON (helps debugging)
        Console.WriteLine("=== Raw OCR JSON ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // 5️⃣ Parse JSON (how to parse json)
        JObject json = JObject.Parse(result.Text);

        // 6️⃣ Extract overall confidence
        double overallConf = json["OverallConfidence"]?.Value<double>() ?? 0.0;
        Console.WriteLine($"Overall confidence: {overallConf:P0}");

        // 7️⃣ Extract text from first page (how to extract text)
        string firstPageText = json["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(firstPageText);
    }
}
```

**Oczekiwany wynik** (zakładając, że OCR zakończył się sukcesem):

```
=== Raw OCR JSON ===
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}

Overall confidence: 92%
=== Extracted Text ===
John Doe
Passport No: 123456789
```

Jeśli obraz nie może zostać odczytany, SDK wyrzuci wyjątek, który przechwytujemy w `Main`, wypisując przyjazny komunikat zamiast awarii.

## Najczęściej zadawane pytania (FAQ)

**P:** Co jeśli silnik OCR zwróci tablicę stron?  
**O:** Iteruj po `json["Pages"]` i konkatenuj każdą wartość `["Text"]`, lub przetwarzaj je indywidualnie w zależności od potrzeb.

**P:** Czy mogę zdeserializować JSON do typowanej klasy C#?  
**O:** Oczywiście. Zdefiniuj strukturę klasy odpowiadającą schematowi JSON i użyj `JsonConvert.DeserializeObject<YourRootClass>(result.Text)`. Daje to bezpieczeństwo w czasie kompilacji, ale wymaga utrzymania modelu w synchronizacji z wyjściem SDK.

**P:** Czy to działa z asynchronicznymi API OCR?  
**O:** Tak. Zamień `engine.Recognize()` na `await engine.RecognizeAsync()` i zmień `RunOcrAndParseJson` na `async Task`. Część parsowania JSON pozostaje taka sama.

**P:** Jak zapisać JSON do pliku w celu późniejszej analizy?  
**O:** Po pobraniu `result.Text` wywołaj `File.WriteAllText(@"output.json", result.Text);`. Następnie możesz go wczytać ponownie za pomocą `JObject.Parse(File.ReadAllText(...))`.

## Co dalej

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}