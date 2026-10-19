---
category: general
date: 2026-04-01
description: Jak przekonwertować wynik OCR na JSON i XML w C# – dowiedz się, jak wyodrębnić
  tekst z obrazu i zapisać plik JSON w C# przy użyciu Aspose.OCR.
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: pl
og_description: Jak przekształcić wyniki OCR w ustrukturyzowane pliki JSON i XML przy
  użyciu C#. Przewodnik krok po kroku, jak wyodrębnić tekst z obrazu i zapisać plik
  JSON w C#.
og_title: Jak przekonwertować OCR na JSON i XML w C# – Zapisz plik JSON
tags:
- OCR
- C#
- Aspose
title: Jak przekonwertować OCR na JSON i XML w C# – Zapisz plik JSON
url: /pl/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak przekonwertować OCR na JSON i XML w C# – Zapisz plik JSON

**How to convert OCR** wyniki w coś, co naprawdę możesz wykorzystać, to pytanie, które zadaje wielu programistów. W tym przewodniku pokażemy, jak wyodrębnić tekst z obrazu, przekształcić wynik OCR w ładnie sformatowany JSON i XML, a następnie zapisać te pliki na dysku przy użyciu C#.

Jeśli kiedykolwiek patrzyłeś na surowy ciąg OCR i pomyślałeś: „Musi istnieć lepszy sposób na jego przechowywanie”, jesteś we właściwym miejscu. Po zakończeniu będziesz mieć kompletny, uruchamialny program, który nie tylko **extracts text from image** plików, ale także wie, jak **write JSON file C#** i **write XML file C#** bez większego wysiłku.

## Czego będziesz potrzebować

- **.NET 6.0** lub nowszy (kod działa również z .NET Framework 4.6+).  
- Pakiet NuGet **Aspose.OCR** – zainstaluj go poleceniem `dotnet add package Aspose.OCR`.  
- Obraz zawierający tekst (np. `invoice.png`).  
- Dowolne IDE – Visual Studio, Rider lub VS Code będą odpowiednie.

> **Pro tip:** Trzymaj pliki obrazów w dedykowanym folderze (np. `Resources/`), aby ścieżki były uporządkowane.

## Krok 1: Konfiguracja silnika OCR – How to Convert OCR

Najpierw tworzymy instancję `OcrEngine` i określamy, jakiego języka ma szukać. W większości przypadków wystarczy język angielski, ale możesz zamienić `Language.English` na dowolny obsługiwany język.

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine for English text
        var ocrEngine = new OcrEngine { Language = Language.English };
```

> **Why this matters:** Inicjalizacja silnika z właściwym językiem znacząco poprawia dokładność, szczególnie w przypadku skryptów nie‑łacińskich.

## Krok 2: Rozpoznawanie tekstu – Extract Text from Image

Teraz przekazujemy obraz do silnika. Metoda `Recognize` zwraca obiekt `OcrResult`, który zawiera surowy tekst oraz dane o położeniu.

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

Jeśli obraz nie zostanie znaleziony, `Recognize` zgłasza `FileNotFoundException`. Aby uprościć demo, zakładamy, że ścieżka jest poprawna, ale w produkcji warto otoczyć to blokiem try‑catch.

## Krok 3: Konwersja wyniku do JSON – Write JSON File C#

Aspose.OCR ułatwia serializację. Metoda `ToJson` przyjmuje flagę `indent`, aby uzyskać ładnie sformatowany wynik, co jest idealne, gdy planujesz otworzyć plik w edytorze tekstu.

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### Przykładowy JSON

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑31\nTotal: $250.00",
  "Regions": [
    {
      "Bounds": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Text": "Invoice #12345"
    }
    // … more regions …
  ]
}
```

> **How to extract text**: Właściwość `Text` zwraca czysty ciąg, który możesz przekazać do innych usług (indeksy wyszukiwania, bazy danych itp.).

## Krok 4: Zapis JSON – Write JSON File C# (Continued)

Gdy ciąg JSON jest gotowy, po prostu zapisujemy go do pliku przy użyciu `File.WriteAllText`. Domyślnie zapewnia kodowanie UTF‑8.

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

Teraz masz plik `invoice.json` obok obrazu, gotowy do dalszego przetwarzania.

## Krok 5: Konwersja wyniku do XML – Write XML File C#

Jeśli wolisz XML dla starszych systemów, metoda `ToXml` wykona ciężką pracę. Podobnie jak `ToJson`, obsługuje także ładne formatowanie.

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### Przykładowy XML

```xml
<OcrResult>
  <Text>Invoice #12345
Date: 2024-03-31
Total: $250.00</Text>
  <Regions>
    <Region>
      <Bounds X="10" Y="20" Width="200" Height="30" />
      <Text>Invoice #12345</Text>
    </Region>
    <!-- … more regions … -->
  </Regions>
</OcrResult>
```

## Krok 6: Zapis XML – Write XML File C# (Continued)

Zapisywanie XML jest identyczne jak w kroku JSON; wystarczy użyć rozszerzenia `.xml`.

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### Pełny działający przykład

Łącząc wszystkie elementy, oto kompletny program, który możesz skopiować i wkleić do aplikacji konsolowej:

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Initialise OCR engine for English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Recognise text from image
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");

        // Convert to JSON and save
        string jsonOutput = ocrResult.ToJson(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);

        // Convert to XML and save
        string xmlOutput = ocrResult.ToXml(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

Uruchom program, a znajdziesz dwa nowe pliki — `invoice.json` i `invoice.xml` — dokładnie tam, gdzie wskazałeś. Otwórz je, aby zweryfikować, że struktura odpowiada powyższym przykładom.

## Częste pytania i przypadki brzegowe

| Question | Answer |
|----------|--------|
| **What if the image contains multiple languages?** | Utwórz osobne instancje `OcrEngine` dla każdego języka lub użyj `Language.Multi`, jeśli jest obsługiwany. |
| **Can I control the output format (e.g., exclude region data)?** | Tak. Zarówno `ToJson`, jak i `ToXml` przyjmują opcjonalne parametry filtrujące pola; sprawdź dokumentację Aspose.OCR pod kątem `ExportOptions`. |
| **How do I handle large PDFs with many pages?** | Przetwarzaj każdą stronę osobno, agreguj wyniki, a następnie serializuj jednorazowo. |
| **Is the output UTF‑8 safe?** | Absolutnie — Aspose.OCR używa Unicode wewnętrznie, a `File.WriteAllText` zapisuje UTF‑8 domyślnie. |
| **What about performance?** | OCR jest intensywny pod względem CPU. W zadaniach wsadowych rozważ równoległe przetwarzanie na wielu rdzeniach lub użycie chmurowego API Aspose. |

## Zakończenie

Teraz wiesz, **how to convert OCR** wyniki zarówno do JSON, jak i XML przy użyciu C#. Postępując zgodnie z powyższymi krokami, możesz **extract text from image**, a następnie **write JSON file C#** i **write XML file C#** w kilku linijkach kodu. To podejście jest szybkie, niezawodne i działa z każdym typem obrazu obsługiwanym przez Aspose.OCR.

Gotowy na kolejne wyzwanie? Spróbuj podać

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}