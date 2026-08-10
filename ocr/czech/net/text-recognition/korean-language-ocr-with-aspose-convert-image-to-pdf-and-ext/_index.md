---
category: general
date: 2026-05-28
description: Návod na OCR korejského jazyka pomocí Aspose v C#. Naučte se, jak načíst
  obrázek ze streamu, extrahovat prostý text, převést obrázek do PDF a exportovat
  prohledávatelné PDF.
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: cs
og_description: OCR korejského jazyka v C# pomocí Aspose. Krok za krokem průvodce
  načtením obrázku ze streamu, extrakcí prostého textu, převodem obrázku do PDF a
  exportem prohledávatelného PDF.
og_title: OCR pro korejský jazyk – převod obrázku na PDF a extrakce textu (průvodce
  C#)
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: 'OCR korejského jazyka s Aspose: převod obrázku na PDF a extrakce textu v C#'
url: /cs/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Korejské OCR s Aspose: Převod obrázku na PDF a extrakce textu v C#

Už jste se někdy zamýšleli, jak spustit **Korean Language OCR** na obrázku, aniž byste něco posílali do cloudu? Nejste v tom sami. Ať už digitalizujete dopravní značky, zpracováváte účtenky nebo budujete vícejazyčný vyhledávací index, schopnost rozpoznat korejské znaky lokálně vám může ušetřit čas, peníze i starosti s ochranou soukromí.

V tomto tutoriálu vás provedeme kompletním, spustitelným příkladem, který ukazuje, jak **načíst obrázek ze streamu**, **extrahovat čistý text**, **převést obrázek na PDF** a nakonec **exportovat prohledávatelné PDF** — vše pomocí Aspose.OCR a několika řádků C#. Žádné externí služby, žádná skrytá magie — jen čistý .NET kód, který můžete vložit do libovolné konzolové aplikace.

## Co získáte

- Fungující konzolový program, který načítá JPEG soubor pomocí souborového streamu.  
- Korejský text extrahovaný jako čisté Unicode řetězce.  
- Podrobnou JSON zprávu o průběhu OCR pro ladění nebo analytiku.  
- Prohledávatelné PDF, které můžete otevřít v libovolném PDF prohlížeči a skutečně vybrat korejská slova.  

**Požadavky**  
- .NET 6.0 nebo novější (kód funguje také na .NET Framework 4.7+).  
- NuGet balíček Aspose.OCR pro .NET nainstalovaný (`Install-Package Aspose.OCR`).  
- Složka obsahující `korean_sign.jpg` a zapisovatelnou destinaci pro výstupní soubory.  

Pokud už máte všechny potřebné součásti, skvěle — přijďme na to.

## Krok 1: Inicializace OCR enginu pro korejské OCR

Prvním krokem je vytvořit instanci `OcrEngine`. Povolení GPU (pokud ho máte) dramaticky zrychlí rozpoznávání a vypnutí automatického stahování zdrojů nutí knihovnu používat offline jazykové balíčky, které poskytnete.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **Proč je to důležité:**  
> *GPU akcelerace* může zkrátit dobu zpracování z sekund na milisekundy u velkých dávkách. Nastavení `AutomaticResourceDownload` na `false` zajišťuje, že ukázka funguje offline — klíčová podmínka pro mnoho podnikovních prostředí.

## Krok 2: Načtení obrázku ze streamu

Čtení obrázku přes stream vám dává flexibilitu: můžete načítat soubory z disku, síťových sdílení nebo dokonce z paměťových blobů. Zde otevíráme lokální JPEG soubor, ale stejný vzor funguje pro jakýkoli `Stream`.

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **Tip:** Pokud budete potřebovat zpracovávat obrázky nahrané přes webové API, stačí nahradit `File.OpenRead` metodou `IFormFile.OpenReadStream()` — zbytek zůstane beze změny.

## Krok 3: Výběr korejského jazyka a aplikace předzpracovatelských filtrů

Aspose.OCR podporuje několik předzpracovatelských kroků, které obrázek před rozpoznáním vyčistí. Pro korejské značky jsou obvykle dostačující korekce sklonu a odšumění.

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **Co se děje pod kapotou?**  
> Filtr `Deskew` narovná natočený text, zatímco `Denoise` odstraní šum, který může zmást klasifikátor znaků. Vynechání těchto kroků často vede k nečitelnému výstupu, zejména u nízkokvalitních fotografií.

## Krok 4: Asynchronní extrakce čistého textu

Nyní nastává okamžik pravdy — požádáme engine, aby rozpoznal znaky a vrátil nám čistý řetězec. Použití `RecognizeAsync` udržuje UI responzivní, pokud tento kód začleníte do desktopové nebo webové aplikace.

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

Po spuštění programu byste měli vidět něco podobného:

```
OCR complete. Extracted text:
서울시청
```

> **Proč asynchronně?**  
> OCR může být náročné na CPU. Asynchronní provedení zabraňuje blokování vlákna, což je zvláště užitečné v ASP.NET Core, kde je nedostatek vláken reálným problémem.

## Krok 5: Získání podrobného výsledku rozpoznání a uložení jako JSON

Někdy potřebujete víc než jen surový řetězec — například skóre důvěry, ohraničující rámečky nebo původní data obrázku. Metoda `RecognizeDetailed` vrací objekt `RecognitionResult`, který lze serializovat do JSON pro pozdější analýzu.

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

Otevřením `korean_ocr.json` uvidíte strukturu podobnou této:

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **Kdy to použít?**  
> Pokud budujete vyhledávací index, hodnoty důvěry vám umožní odfiltrovat nízkokvalitní výsledky. Pokud potřebujete zvýraznit text v UI, ohraničující rámečky jsou vaším mapovým podkladem.

## Krok 6: Převod obrázku na PDF a export prohledávatelného PDF

Aspose usnadňuje přechod z rastru na vektor. Nastavením `OutputFormat` na `SearchablePdf` knihovna vloží původní obrázek a překryje jej neviditelnou textovou vrstvou obsahující výstup OCR. Výsledné PDF lze vyhledávat, kopírovat a indexovat stejně jako jakékoli nativní PDF.

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

Otevřete `korean_searchable.pdf` v Adobe Readeru nebo jiném PDF prohlížeči, stiskněte **Ctrl+F**, zadejte korejské slovo a sledujte, jak vás prohlížeč přenese na přesné místo na stránce. To je síla prohledávatelného PDF.

> **Další tip:** Pokud potřebujete jen vizuální PDF bez skryté textové vrstvy, změňte `OutputFormat` na `Pdf`.

## Kompletní funkční příklad

Níže je celý program — zkopírujte, vložte, nahraďte `YOUR_DIRECTORY` skutečnou cestou a stiskněte **F5**.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### Očekávaný výstup v konzoli

```
OCR complete. Extracted text:
서울시청
```

A vedle vašeho zdrojového obrázku najdete tři nové soubory:

- `korean_ocr.json` — úplná data rozpoznání.  
- `korean_searchable.pdf` — PDF, které můžete prohledávat.  
- (volitelně) jakékoli mezilehlé logy, které si přidáte.

## Často kladené otázky a okrajové případy

**Co když nemám GPU?**  
Nastavte `EnableGpu = false`; fallback na CPU je naprosto dostačující pro malé dávky.

**Mohu zpracovávat více obrázků v jednom běhu?**  
Určitě. Zabalte hlavní logiku do smyčky `foreach (var file in Directory.GetFiles(...))` a při každé iteraci přiřaďte `ocrEngine.Image` novému souboru.

**Jak zacházet s dalšími jazyky společně s korejštinou?**  
Aspose.OCR umožňuje nastavit `Language = Language.AutoDetect` nebo kombinovat jazyky pomocí bitového OR operátoru (např. `Language.Korean | Language.English`).

**Co když je důvěra OCR nízká?**  
Prozkoumejte `detailedResult.Pages[0].Words` a odfiltrujte položky s `Confidence < 0.7`. Můžete také vyladit předzpracovatelské filtry — zkuste přidat `PreprocessFilter.ContrastEnhancement`.

## Závěr

Právě jste viděli, jak provést **Korean Language OCR** od začátku do konce, od **načtení obrázku ze streamu** po **extrakci čistého textu**, následně **převod obrázku na PDF** a nakonec **export prohledávatelného PDF**. Přístup je modulární, takže můžete snadno vyměnit zdroj obrázku, změnit výstupní formát nebo zapojit JSON do jakéhokoli downstream pipeline.

Co dál

## Související tutoriály

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}