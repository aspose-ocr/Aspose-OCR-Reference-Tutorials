---
category: general
date: 2026-04-01
description: Jak převést výstup OCR do JSON a XML v C# – naučte se extrahovat text
  z obrázku a zapisovat JSON soubor v C# pomocí Aspose.OCR.
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: cs
og_description: Jak převést výsledky OCR do strukturovaných souborů JSON a XML pomocí
  C#. Krok za krokem průvodce extrakcí textu z obrázku a zápisem souboru JSON v C#.
og_title: Jak převést OCR na JSON a XML v C# – Zapsat JSON soubor
tags:
- OCR
- C#
- Aspose
title: Jak převést OCR na JSON a XML v C# – Zapsat JSON soubor
url: /cs/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak převést OCR na JSON a XML v C# – Zapsat JSON soubor

**How to convert OCR** výsledky do něčeho, co můžete skutečně použít, je otázka, kterou si klade mnoho vývojářů. V tomto průvodci vám ukážeme, jak extrahovat text z obrázku, převést výstup OCR na hezky formátovaný JSON a XML a poté tyto soubory zapsat na disk pomocí C#.

Pokud jste někdy zírali na surový řetězec OCR a pomysleli si: „Musí existovat lepší způsob, jak to uložit,“ jste na správném místě. Na konci budete mít kompletní, spustitelný program, který nejen **extracts text from image** soubory, ale také umí **write JSON file C#** a **write XML file C#** bez potíží.

## Co budete potřebovat

- **.NET 6.0** nebo novější (kód funguje také s .NET Framework 4.6+).  
- **Aspose.OCR** NuGet balíček – nainstalujte jej pomocí `dotnet add package Aspose.OCR`.  
- Obrázek obsahující text (např. `invoice.png`).  
- Jakékoliv IDE, které chcete – Visual Studio, Rider nebo VS Code bude stačit.

> **Tip:** Uchovávejte své soubory obrázků v samostatné složce (např. `Resources/`), aby cesty zůstaly přehledné.

## Krok 1: Nastavení OCR enginu – How to Convert OCR

Nejprve vytvoříme instanci `OcrEngine` a řekneme jí, jaký jazyk má hledat. Ve většině případů stačí angličtina, ale můžete nahradit `Language.English` libovolným podporovaným jazykem.

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

> **Proč je to důležité:** Inicializace enginu se správným jazykem dramaticky zvyšuje přesnost, zejména u ne‑latinských skriptů.

## Krok 2: Rozpoznání textu – Extract Text from Image

Nyní předáme obrázek engine. Metoda `Recognize` vrací objekt `OcrResult`, který obsahuje surový text i data o umístění.

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

Pokud obrázek nelze najít, `Recognize` vyhodí `FileNotFoundException`. Pro jednoduchost demo předpokládáme, že cesta je správná, ale v produkci byste to měli obalit do try‑catch bloku.

## Krok 3: Převod výsledku na JSON – Write JSON File C#

Aspose.OCR usnadňuje serializaci. Metoda `ToJson` přijímá parametr `indent`, který vytváří hezky formátovaný výstup, což je ideální, když chcete soubor otevřít v textovém editoru.

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### Očekávaný JSON příklad

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

> **Jak extrahovat text**: Vlastnost `Text` vám poskytne čistý řetězec, který můžete předat dalším službám (vyhledávací indexy, databáze atd.).

## Krok 4: Uložení JSON – Write JSON File C# (Pokračování)

Jakmile je řetězec JSON připraven, jednoduše jej zapíšeme do souboru pomocí `File.WriteAllText`. Tím se zajistí výchozí kódování UTF‑8.

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

Nyní máte `invoice.json` vedle vašeho obrázku, připravený pro další zpracování.

## Krok 5: Převod výsledku na XML – Write XML File C#

Pokud dáváte přednost XML pro starší systémy, metoda `ToXml` udělá těžkou práci. Stejně jako `ToJson` také podporuje hezké formátování.

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### Očekávaný XML příklad

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

## Krok 6: Uložení XML – Write XML File C# (Pokračování)

Ukládání XML je stejné jako krok s JSON; stačí použít příponu `.xml`.

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### Kompletní funkční příklad

Spojením všech částí získáte kompletní program, který můžete zkopírovat a vložit do konzolové aplikace:

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

Spusťte program a najdete dva nové soubory — `invoice.json` a `invoice.xml` — tam, kde jste je určili. Otevřete je a ověřte, že struktura odpovídá výše uvedeným ukázkám.

## Časté otázky a okrajové případy

| Otázka | Odpověď |
|----------|--------|
| **Co když obrázek obsahuje více jazyků?** | Vytvořte samostatné instance `OcrEngine` pro každý jazyk nebo použijte `Language.Multi`, pokud je podporováno. |
| **Mohu řídit formát výstupu (např. vyloučit data o regionech)?** | Ano. Jak `ToJson`, tak `ToXml` přijímají volitelné parametry pro filtrování polí; podívejte se do dokumentace Aspose.OCR na `ExportOptions`. |
| **Jak zvládnout velké PDF s mnoha stránkami?** | Zpracovávejte každou stránku samostatně, agregujte výsledky a poté je jednou serializujte. |
| **Je výstup bezpečný v UTF‑8?** | Naprostá jistota — Aspose.OCR používá interně Unicode a `File.WriteAllText` zapisuje ve výchozím nastavení UTF‑8. |
| **Jaký je výkon?** | OCR je náročné na CPU. Pro dávkové úlohy zvažte paralelizaci napříč jádry nebo použití cloudového API od Aspose. |

## Závěr

Nyní víte, **how to convert OCR** výsledky do JSON i XML pomocí C#. Dodržením výše uvedených kroků můžete **extract text from image**, poté **write JSON file C#** a **write XML file C#** pomocí několika řádků. Tento přístup je rychlý, spolehlivý a funguje s jakýmkoli typem obrázku, který Aspose.OCR podporuje.

Ready for the next challenge? Try feeding the

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}