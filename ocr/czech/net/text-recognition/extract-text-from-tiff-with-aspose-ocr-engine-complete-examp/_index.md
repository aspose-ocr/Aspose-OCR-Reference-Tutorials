---
category: general
date: 2026-04-04
description: Naučte se, jak extrahovat text z TIFF souborů pomocí OCR enginu – příklad
  v C#. Krok za krokem průvodce s výstupem ve formátu JSON a XML.
draft: false
keywords:
- extract text from tiff
- ocr engine example
- Aspose OCR C#
- multi‑page TIFF OCR
- JSON OCR result
language: cs
og_description: Extrahujte text z TIFF souborů pomocí OCR enginu – příklad v C#. Podrobné
  kroky, kompletní kód a tipy pro výstup ve formátu JSON/XML.
og_title: Extrahování textu z TIFF pomocí Aspose OCR Engine – kompletní průvodce
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Extrahovat text z TIFF pomocí Aspose OCR Engine – kompletní příklad
url: /cs/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-engine-complete-examp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat text z TIFF – Kompletní příklad OCR enginu v C#

Už jste někdy potřebovali **extrahovat text z TIFF** obrázků, ale nebyli jste si jisti, která knihovna dokáže zpracovat více‑stránkové soubory bez spousty obcházek? Nejste v tom sami. V mnoha starších systémech přicházejí dokumenty jako více‑stránkové TIFF skeny a získání surového textu je nezbytná funkce pro vyhledávání, soulad nebo automatizaci zadávání dat.

Dobrá zpráva? S Aspose OCR to můžete udělat během několika řádků—žádné manipulace s nízkoúrovňovými pixlovými buffery. Tento tutoriál vás provede **kompletním příkladem OCR enginu**, který načte více‑stránkový TIFF, rozpozná každou stránku a vypíše jak hezky formátovaný JSON, tak volitelný XML. Na konci budete mít připravenou C# konzolovou aplikaci, která během sekund extrahuje text z TIFF souborů.

## Co se naučíte

- Jak nastavit Aspose OCR engine v .NET projektu.  
- Přesný kód potřebný k **extrahování textu z TIFF** souborů, včetně zpracování více stránek.  
- Proč můžete chtít výstup v JSON místo XML a jak vygenerovat oba.  
- Tipy pro odstraňování běžných problémů (např. DPI obrázku, využití paměti).  

### Předpoklady

- .NET 6.0 SDK nebo novější (kód funguje s .NET Core a .NET Framework).  
- Platná licence Aspose OCR (nebo klíč pro bezplatnou zkušební verzi).  
- Visual Studio 2022 nebo jakýkoli C# editor, který preferujete.  
- Ukázkový více‑stránkový TIFF soubor (nazvaný `multi-page.tiff` v příkladu).  

> **Tip:** Pokud máte omezený rozpočet, bezplatná zkušební verze vám stále umožní extrahovat text až z 100 stránek za měsíc—ideální pro testování.

---

## Krok 1 – Inicializace OCR enginu (ocr engine example)

Než budeme moci **extrahovat text z TIFF**, potřebujeme instanci OCR enginu. Tento objekt obsahuje veškeré nastavení, které můžete později upravit (jazyk, rozlišení, atd.).

```csharp
using Aspose.OCR;
using System.IO;

// Create a new OCR engine – this is the core of our ocr engine example
var ocrEngine = new OcrEngine();

// Optional: set language if you know the document’s language
// ocrEngine.Language = Language.English;
```

*Proč je to důležité:* Třída `OcrEngine` abstrahuje těžkou práci. Vytvoření jedné instance a její opakované použití pro více obrázků je paměťově úspornější než vytváření nového enginu pro každou stránku.

---

## Krok 2 – Načtení více‑stránkového TIFF (extract text from TIFF)

Nyní nasměrujeme engine na náš zdrojový soubor. `ImageStream.FromFile` podporuje TIFF, JPEG, PNG a mnoho dalších, ale v tomto tutoriálu se zaměříme na TIFF.

```csharp
// Load the multi‑page TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi-page.tiff");
```

> **Poznámka:** Nahraďte `YOUR_DIRECTORY` skutečnou cestou ke složce na vašem počítači.  
> **Tip:** Pokud má váš TIFF nízké DPI (méně než 150), zvažte předzpracování pro zlepšení přesnosti OCR.

---

## Krok 3 – Rozpoznání všech stránek

Volání `Recognize()` spustí OCR algoritmus napříč **každou stránkou** v TIFF. Výsledný objekt obsahuje surový text, skóre důvěry a segmentaci po stránkách.

```csharp
// Run OCR on the loaded image – this extracts text from all pages
var ocrResult = ocrEngine.Recognize();
```

*Co získáte zpět:* `ocrResult` obsahuje kolekci objektů `PageResult`. Text každé stránky lze získat pomocí `ocrResult.Pages[i].Text`. Engine také poskytuje úrovně důvěry, které mohou být užitečné pro kontrolu kvality.

---

## Krok 4 – Uložení výsledků jako JSON (a volitelně XML)

Většina moderních pipeline preferuje JSON, ale starší systémy stále pracují s XML. Zde je návod, jak vygenerovat oba, pěkně formátované.

```csharp
// Convert the recognition result to pretty‑printed JSON
string jsonResult = ocrResult.ToJson(prettyPrint: true);
File.WriteAllText(@"YOUR_DIRECTORY/result.json", jsonResult);

// Optional: also output XML for older workflows
string xmlResult = ocrResult.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY/result.xml", xmlResult);
```

### Ukázkový výstup JSON (zkrácený)

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
      "Confidence": 0.97
    },
    {
      "PageNumber": 2,
      "Text": "Itemized List\n1. Widget A – $500.00\n2. Widget B – $750.00",
      "Confidence": 0.95
    }
  ]
}
```

JSON je čitelný pro člověka, což usnadňuje ladění. XML odráží stejnou strukturu, pokud ji potřebujete.

---

## Krok 5 – Ověření extrakce (extract text from TIFF)

Po zápisu souborů rychlá kontrola pomůže zajistit, že se nic nepokazilo.

```csharp
// Load the JSON back just to confirm it was saved correctly
string loadedJson = File.ReadAllText(@"YOUR_DIRECTORY/result.json");
Console.WriteLine("First 200 characters of JSON output:");
Console.WriteLine(loadedJson.Substring(0, Math.Min(200, loadedJson.Length)));
```

Pokud se vám vytiskne úryvek, úspěšně jste **extrahovali text z TIFF** a uložili jej. Odtud můžete JSON poslat do vyhledávacího indexu, databáze nebo jakékoli další služby.

---

## Proč použít Aspose OCR k extrahování textu z TIFF?

- **Podpora více stránek přímo z krabice** – není potřeba TIFF ručně rozdělovat.  
- **Vysoká přesnost** díky proprietárním modelům neuronových sítí.  
- **Cross‑platform** – funguje na Windows, Linux a macOS .NET runtime.  
- **Bohaté výstupní formáty** (JSON, XML, prostý text), které vyhovují jak moderním, tak starším stackům.  

Pokud stále váháte, vyzkoušejte bezplatnou zkušební verzi na ukázkovém dokumentu. Všimnete si rychlosti a jednoduchosti ve srovnání s open‑source alternativami, které často vyžadují další předzpracování obrázku.

---

## Časté problémy a jak se jim vyhnout

| Problém | Příznak | Řešení |
|-------|---------|-----|
| Nízké rozlišení TIFF | Chybějící znaky, nízká důvěra | Zvětšete obrázek na ≥150 DPI před OCR (`ocrEngine.Image = ImageStream.FromFile(...).Resize(150)` ) |
| Špatný jazyk | Rozmazaná slova, zejména pro neanglický text | Nastavte `ocrEngine.Language = Language.Spanish` (nebo vhodný) před `Recognize()` |
| Nedostatek paměti u velkých souborů | `OutOfMemoryException` | Zpracovávejte stránky po dávkách: projděte `ocrEngine.Image.Pages` a zavolejte `RecognizePage(i)` |
| Licence nebyla použita | Vodoznak „Evaluation“ ve výstupu | Zaregistrujte licenci: `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Kompletní funkční příklad (připravený ke zkopírování)

Níže je kompletní program, který můžete vložit do nového konzolového projektu. Obsahuje všechny části, o kterých jsme mluvili—initializaci, načtení, rozpoznání a ukládání.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine (ocr engine example)
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // Optional: set license if you have one
            // var license = new License();
            // license.SetLicense("Aspose.OCR.lic");

            // -------------------------------------------------
            // 2️⃣  Load the multi‑page TIFF (extract text from TIFF)
            // -------------------------------------------------
            string tiffPath = @"YOUR_DIRECTORY/multi-page.tiff";
            if (!File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -------------------------------------------------
            // 3️⃣  Recognize every page
            // -------------------------------------------------
            var ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // 4️⃣  Save JSON (pretty) and optional XML
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/result.json";
            string jsonResult = ocrResult.ToJson(prettyPrint: true);
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"JSON saved to {jsonPath}");

            // Optional XML output
            string xmlPath = @"YOUR_DIRECTORY/result.xml";
            string xmlResult = ocrResult.ToXml();
            File.WriteAllText(xmlPath, xmlResult);
            Console.WriteLine($"XML saved to {xmlPath}");

            // -------------------------------------------------
            // 5️⃣  Quick verification (extract text from TIFF)
            // -------------------------------------------------
            string preview = jsonResult.Length > 200 ? jsonResult.Substring(0, 200) + "..." : jsonResult;
            Console.WriteLine("\nPreview of JSON output:");
            Console.WriteLine(preview);
        }
    }
}
```

Uložte soubor jako `Program.cs`, spusťte `dotnet run` a sledujte, jak konzole zobrazí, kam byly uloženy JSON a XML. To je vše—právě jste dokončili **příklad OCR enginu**, který extrahuje text z TIFF.

---

## Další kroky a související témata

- **Dávkové zpracování:** Zabalte výše uvedenou logiku do smyčky `foreach`, abyste automaticky zpracovali desítky TIFF souborů.  
- **Integrace vyhledávání:** Přesuňte JSON do Elasticsearch nebo Azure Cognitive Search pro plnotextové vyhledávání ve skenovaných dokumentech.  
- **Předzpracování obrázků:** Prozkoumejte Aspose `ImageProcessing` API pro korekci sklonu, odstranění šumu nebo úpravu kontrastu před OCR.  
- **Alternativní výstup:** Použijte `ocrResult.ToPlainText()`, pokud potřebujete jen surové řetězce bez metadat.  

Pokud vás zajímají jiné formáty obrázků, stejný postup funguje pro PDF (stačí změnit zdrojový soubor) nebo PNG. Hlavní myšlenkou je, že jakmile je engine nastaven, zbytek je opakovatelný pipeline.

---

## Závěr

Prošli jsme **kompletním příkladem OCR enginu**, který vám umožní **extrahovat text z TIFF** souborů pomocí Aspose OCR, a výstupem jsou čisté JSON a volitelný XML pro jakýkoli následný workflow. Kód je samostatný, vysvětlení pokrývají „proč“ každého kroku

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}