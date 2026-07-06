---
category: general
date: 2026-04-26
description: Extrahujte text z obrázku v C# pomocí Aspose.OCR a naučte se, jak během
  několika minut převést obrázek do formátů JSON a XML.
draft: false
keywords:
- extract text from image
- convert image to json
- convert image to xml
- Aspose OCR C#
- image to JSON C#
- image to XML C#
language: cs
og_description: Extrahujte text z obrázku v C# pomocí Aspose.OCR. Naučte se krok za
  krokem, jak okamžitě převést výsledek do JSON a XML.
og_title: Extrahovat text z obrázku v C# – převést na JSON a XML
tags:
- OCR
- C#
- Aspose
- JSON
- XML
title: Extrahovat text z obrázku v C# – převést do JSON a XML
url: /cs/net/text-recognition/extract-text-from-image-in-c-convert-to-json-xml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat text z obrázku v C# – Převést na JSON a XML

Už jste někdy potřebovali **extrahovat text z obrázku** v .NET projektu, ale uvízli jste u otázky „jak vlastně získat data ven?“ Nejste v tom sami. V mnoha reálných aplikacích – například zpracování faktur, skenování účtenek nebo ověřování průkazů – je získání surových znaků z obrázku prvním, klíčovým krokem.  

Dobrá zpráva? S Aspose.OCR to můžete udělat během několika řádků a okamžitě **převést obrázek na JSON** nebo **převést obrázek na XML** pro následné systémy. V tomto průvodci projdeme kompletní, připravený k běhu kód, vysvětlíme, proč je každá část důležitá, a ukážeme vám několik tipů, jak se vyhnout běžným úskalím.

---

## Co budete potřebovat

- **.NET 6+** (jakýkoli recentní SDK funguje; ukázka cílí na .NET 6)
- **Aspose.OCR for .NET** NuGet balíček  
  ```bash
  dotnet add package Aspose.OCR
  ```
- Soubor s obrázkem (PNG, JPG atd.), který obsahuje tisknutelný text; jako příklad použijeme `invoice.png`.
- Editor kódu – Visual Studio, VS Code nebo Rider – jakýkoliv preferujete.

To je vše. Žádné další OCR enginy, žádné externí služby, jen jeden NuGet balíček.

---

## Krok 1: Nastavení OCR enginu – Jak extrahovat text z obrázku

Nejprve vytvoříme instanci `OcrEngine` a nasměrujeme ji na soubor s obrázkem. Tento krok je základem; bez správně načteného obrázku engine nemůže nic rozpoznat.

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

**Proč je to důležité:**  
- `OcrEngine` zapouzdřuje veškeré nízkoúrovňové předzpracování obrázku (binarizaci, vyrovnání).  
- Načtení obrázku pomocí `ImageStream.FromFile` zajišťuje, že engine přečte přesné bajty, zachovává DPI a barevnou hloubku – obojí může ovlivnit přesnost rozpoznání.  

> **Tip:** Pokud jsou vaše zdrojové obrázky ve streamu (např. nahrané přes webové API), použijte `ImageStream.FromStream(yourStream)` místo `FromFile`.

---

## Krok 2: Řekněte engine, jaký jazyk očekává – přesně extrahovat text z obrázku

Aspose.OCR podporuje mnoho abeced. Zadání správného jazyka omezuje množinu znaků a zvyšuje přesnost.

```csharp
// Set the language; Latin covers English, French, German, etc.
ocrEngine.Language = Language.Latin;
```

**Proč:**  
Když nastavíte `Language.Latin`, OCR engine ignoruje cyrilické nebo asijské glyfy, čímž snižuje falešně pozitivní výsledky. Pokud později potřebujete zpracovávat vícejazyčné dokumenty, můžete přepnout na `Language.Multilingual` nebo kombinovat jazyky.

---

## Krok 3: Spusťte proces rozpoznávání – extrahovat text z obrázku jedním voláním

Nyní skutečně rozpoznáváme text. Metoda `Recognize` vrací objekt `RecognitionResult`, který obsahuje surový text, skóre důvěry a dokonce i data o rozložení.

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

**Proč:**  
Jedno volání `Recognize` stačí, protože engine interně provádí předzpracování, segmentaci a klasifikaci znaků. Vlastnost `Text` vám poskytne prostý řetězec, ideální pro logování nebo rychlou validaci.

---

## Krok 4: Převod výsledku do JSON – jednoduše převést obrázek na JSON

Mnoho moderních služeb preferuje JSON payloady. Aspose.OCR poskytuje pohodlnou metodu `ToJson`, která serializuje celý `RecognitionResult`, včetně hodnot důvěry a ohraničujících rámečků.

```csharp
// Serialize the result to JSON
string jsonResult = recognitionResult.ToJson();

// Save the JSON to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonResult);

Console.WriteLine("JSON file saved at YOUR_DIRECTORY/invoice.json");
```

**Proč byste mohli chtít JSON:**  
- **Interoperabilita:** Front‑end aplikace (React, Angular) mohou JSON konzumovat přímo.  
- **Ladění:** JSON obsahuje důvěru pro každý znak, což vám umožní označit slova s nízkou důvěrou k ruční revizi.  

> **Okrajový případ:** Pokud váš následný systém potřebuje jen prostý text, můžete získat `recognitionResult.Text` a zabalit jej do vlastního JSON objektu místo celého Aspose payloadu.

---

## Krok 5: Převod výsledku do XML – převést obrázek na XML pro starší systémy

Některé podniky stále spoléhají na XML schémata pro výměnu dat. Metoda `ToXml` je obdobou `ToJson`, ale výstupem je XML.

```csharp
// Serialize the result to XML
string xmlResult = recognitionResult.ToXml();

// Save the XML to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlResult);

Console.WriteLine("XML file saved at YOUR_DIRECTORY/invoice.xml");
```

**Proč XML:**  
- **Validace schématu:** Můžete definovat XSD, který odpovídá struktuře generované Aspose, což zaručuje soulad s kontraktem.  
- **Integrace:** Starší ERP nebo systémy pro správu dokumentů často zpracovávají XML přímo.

---

## Kompletní funkční příklad – vše v jednom kódu

Níže je kompletní program, který spojuje vše dohromady. Zkopírujte a vložte jej do nového konzolového projektu (`dotnet new console`) a spusťte.

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

**Očekávaný výstup (konzole):**

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

JSON file saved at YOUR_DIRECTORY/invoice.json
XML file saved at YOUR_DIRECTORY/invoice.xml
```

Soubory JSON a XML budou obsahovat bohatší strukturu, například:

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

---

## Časté otázky a okrajové případy

### Co když je obrázek rozmazaný nebo otočený?

Aspose.OCR automaticky vyrovnává většinu obrázků, ale v extrémních případech můžete chtít předzpracovat pomocí `ocrEngine.Image = ImageProcessor.Deskew(ocrEngine.Image)`. Přidání mírného zvýšení kontrastu (`ImageProcessor.AdjustContrast`) může také zlepšit skóre důvěry.

### Můžu extrahovat text z PDF?

Ano – nejprve převěďte každou stránku PDF na obrázek (např. pomocí Aspose.PDF nebo volné knihovny jako PDFium) a poté tyto obrázky zadejte do stejného OCR toku.

### Jak zvládnout více jazyků v jednom dokumentu?

Set `ocrEngine.Language = Language.Multilingual;` or combine specific languages:

```csharp
ocrEngine.Language = Language.English | Language.French | Language.German;
```

Uvědomte si, že širší sady jazyků mohou

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}