---
category: general
date: 2026-05-21
description: Proveďte OCR na obrázku pomocí C#. Naučte se, jak načíst obrázek pro
  OCR, extrahovat text z PNG a rozpoznat text z obrázku pomocí malého ukázkového kódu.
draft: false
keywords:
- perform OCR on image
- extract text from PNG
- recognize text from image
- load image for OCR
language: cs
og_description: Rychle provádějte OCR na obrázku v C#. Tento průvodce ukazuje, jak
  načíst obrázek pro OCR, extrahovat text z PNG a rozpoznat text z obrázku s výstupem
  HTML, který zachovává rozložení.
og_title: Proveďte OCR na obrázku pomocí C# – Kompletní programovací tutoriál
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  headline: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  name: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  steps:
  - name: Load Image for OCR
    text: The line `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");`
      is where we **load image for OCR**. The `ImageStream` helper abstracts away
      file‑format details, so you can feed JPEG, BMP, or TIFF without changing code.
  - name: Extract Text from PNG
    text: 'Once `engine.Recognize()` finishes, the OCR engine holds the recognized
      text internally. You can pull it out as a string if you only need raw text:'
  - name: Recognize Text from Image
    text: 'The `Recognize()` call does the heavy lifting. Under the hood the engine:'
  - name: Handling Layout‑Aware HTML Output
    text: 'Most developers stop at plain text, but the `HtmlSaveOptions` we used let
      you **perform OCR on image** and keep the visual structure intact. Two flags
      matter:'
  - name: Scaling to Multiple Files
    text: 'If you need to **perform OCR on image** files in a folder, wrap the core
      logic in a simple loop:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Aspose.OCR
title: Proveďte OCR na obrázku pomocí C# – Kompletní průvodce krok za krokem
url: /cs/net/text-recognition/perform-ocr-on-image-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Proveďte OCR na obrázku pomocí C# – Kompletní krok‑za‑krokem průvodce

Už jste se někdy zamysleli, jak **provést OCR na obrázku** souborech bez zdlouhavých těžkopádných GUI? Nejste v tom sami. Ať už digitalizujete účtenky, získáváte data ze skenovaných formulářů, nebo jen potřebujete převést PNG na prohledávatelný text, několik řádků C# to zvládne.

V tomto tutoriálu projdeme načtením obrázku pro OCR, rozpoznáním textu z obrázku a nakonec extrahováním textu z PNG jako čistého HTML. Na konci budete mít připravenou konzolovou aplikaci, která **provádí OCR na obrázku** a zachovává původní rozvržení.

## Co vytvoříte

- Minimální konzolový program, který načte PNG (nebo jakýkoli podporovaný obrázek)  
- Použije OCR engine k **rozpoznání textu z obrázku**  
- Uloží výsledek jako HTML s ohledem na rozvržení, vkládající původní obrázek  
- Ukáže, jak **načíst obrázek pro OCR**, **extrahovat text z PNG** a řešit běžné okrajové případy  

> **Předpoklady**  
> - .NET 6.0 SDK nebo novější (můžete také cílit na .NET Framework 4.7+)  
> - NuGet‑kompatibilní OCR knihovna – příklad používá *Aspose.OCR*, ale funguje i jakákoli knihovna s podobným API  
> - Základní znalost C# (nic složitého)  

Máte to? Skvělé—ponořme se.

## Proveďte OCR na obrázku – Kompletní prohlídka kódu

Níže je **úplný, spustitelný** program. Zkopírujte jej do nového konzolového projektu (`dotnet new console`) a stiskněte **F5**.

```csharp
using System;
using Aspose.OCR;               // OCR engine namespace
using Aspose.OCR.Models;        // Save options namespace
using Aspose.OCR.ImageProcessing; // Image loading helpers

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine and set the language
            // -------------------------------------------------
            var engine = new OcrEngine
            {
                Language = OcrLanguage.English   // You can change to French, German, etc.
            };

            // -------------------------------------------------
            // Step 2: Load the image for OCR
            // -------------------------------------------------
            // Replace the path with your actual PNG/JPEG/TIFF file.
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");

            // -------------------------------------------------
            // Step 3: Perform OCR recognition
            // -------------------------------------------------
            engine.Recognize();

            // -------------------------------------------------
            // Step 4: Configure HTML save options – keep layout
            // -------------------------------------------------
            var htmlOptions = new HtmlSaveOptions
            {
                PreserveLayout = true,   // Keep columns, tables, and spacing
                EmbedImages = true       // Embed the original PNG inside the HTML
            };

            // -------------------------------------------------
            // Step 5: Save the recognized content as layout‑aware HTML
            // -------------------------------------------------
            engine.Save("YOUR_DIRECTORY/form.html", htmlOptions);

            Console.WriteLine("HTML with layout saved.");
        }
    }
}
```

> **Očekávaný výstup**  
> ```
> HTML with layout saved.
> ```  
> Po spuštění najdete `form.html` vedle vašeho PNG. Otevřete jej v prohlížeči a uvidíte přesně stejné rozvržení, ale nyní je text vybratelný a prohledávatelný.

### Načíst obrázek pro OCR

Řádek `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");` je místem, kde **načítáme obrázek pro OCR**. Pomocník `ImageStream` abstrahuje detaily formátu souboru, takže můžete zadat JPEG, BMP nebo TIFF bez změny kódu.  

**Proč nepředat jen `Bitmap`?**  
Protože mnoho OCR SDK očekává stream, který také nese metadata DPI. Použití vestavěného načítače knihovny zaručuje, že engine vidí obrázek přesně tak, jak se zobrazuje na obrazovce, což zvyšuje přesnost.

#### Pro tip
Pokud zpracováváte dávku souborů, zabalte krok načítání do `try/catch` a logujte jakékoli `FileNotFoundException`. Tím zabráníte zhroucení celé dávky kvůli chybějícímu souboru.

### Extrahovat text z PNG

Jakmile `engine.Recognize()` skončí, OCR engine interně drží rozpoznaný text. Můžete jej získat jako řetězec, pokud potřebujete jen surový text:

```csharp
string plainText = engine.Text;   // Returns the whole document as plain text
Console.WriteLine(plainText);
```

Toto je nejrychlejší způsob, jak **extrahovat text z PNG**, když vám nevadí rozvržení. Pro většinu úloh zadávání dat stačí prostý text — jen nezapomeňte oříznout koncové znaky řádků, pokud plánujete import do CSV.

### Rozpoznat text z obrázku

Volání `Recognize()` vykonává těžkou práci. Pod kapotou engine:

1. Normalizuje obrázek (odstraňuje šikmost, šum)  
2. Segmentuje jej na řádky a slova  
3. Spustí klasifikátor neuronové sítě trénovaný na milionech glyfů  

Protože jsme nastavili `Language = OcrLanguage.English`, engine používá anglické slovníky, což výrazně snižuje falešně pozitivní výsledky. Pokud potřebujete vícejazyčnou podporu, stačí předat pole jazyků:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

### Zpracování výstupu HTML s ohledem na rozvržení

Většina vývojářů končí u prostého textu, ale `HtmlSaveOptions`, které jsme použili, vám umožní **provést OCR na obrázku** a zachovat vizuální strukturu. Důležité jsou dva příznaky:

- `PreserveLayout = true` – zachovává sloupce, tabulky a mezery.  
- `EmbedImages = true` – vloží původní PNG jako Base64‑kódovaný `<img>` prvek, takže HTML je samostatné.

Pokud dáváte přednost lehčímu souboru, nastavte `EmbedImages = false` a HTML bude odkazovat na původní PNG na disku.

#### Okrajový případ: Velké soubory

U obrázků větších než 5 MB může vkládání výrazně navýšit velikost HTML. V takových případech přepněte na externí odkazy na obrázky a zvažte předchozí kompresi PNG pomocí `ImageProcessor.Compress`.

## Běžné problémy a pro tipy

| Příznak | Pravděpodobná příčina | Řešení |
|--------|-----------------------|--------|
| Zkreslené znaky | Nesprávně nastavený jazyk nebo chybějící jazykový balíček | Nainstalujte odpovídající jazyková data a nastavte `engine.Language` správně |
| Žádný text ve výstupu | Obrázek je příliš tmavý nebo má nízké rozlišení | Předzpracujte pomocí `engine.Image = ImageProcessor.AdjustContrast(engine.Image, 1.2)` |
| Rozvržení v HTML poškozené | `PreserveLayout` zůstalo na výchozím `false` | Nastavte `PreserveLayout = true` v `HtmlSaveOptions` |
| Pomalé zpracování mnoha stránek | Engine se znovu inicializuje pro každý soubor | Znovu použijte stejnou instanci `OcrEngine` a měňte jen `engine.Image` v každé iteraci |

### Škálování na více souborů

Pokud potřebujete **provést OCR na obrázku** souborech ve složce, zabalte hlavní logiku do jednoduché smyčky:

```csharp
foreach (var file in Directory.GetFiles("YOUR_DIRECTORY", "*.png"))
{
    engine.Image = ImageStream.FromFile(file);
    engine.Recognize();
    var htmlPath = Path.ChangeExtension(file, ".html");
    engine.Save(htmlPath, htmlOptions);
    Console.WriteLine($"Processed {Path.GetFileName(file)}");
}
```

Všimněte si, že **načítáme obrázek pro OCR** uvnitř smyčky, ale zachováváme stejné objekty `engine` a `htmlOptions`. Tím se snižuje zatížení paměti a urychlují dávkové úlohy.

## Dál: Export do PDF nebo DOCX

Stejný `engine` může ukládat i do jiných formátů:

```csharp
engine.Save("output.pdf", new PdfSaveOptions { PreserveLayout = true });
engine.Save("output.docx", new WordSaveOptions { PreserveLayout = true });
```

Pokud váš downstream systém očekává prohledávatelné PDF, jde o jednorázovou změnu — není potřeba psát samostatný konverzní pipeline.

## Závěr

Ukázali jsme vám, jak **provést OCR na obrázku** souborech pomocí C#, od načtení obrázku po **extrahování textu z PNG** a nakonec **rozpoznání textu z obrázku** do HTML s ohledem na rozvržení. Kompletní příklad je připravený ke spuštění a nyní rozumíte, proč je každý krok důležitý, jak jej přizpůsobit pro různé jazyky a na co si dát pozor.

Další krok: vyzkoušejte výměnu anglického jazyka za jiný locale, experimentujte s `PreserveLayout = false` pro úspornější HTML, nebo přesměrujte výstup prostého textu do databáze pro prohledávatelné archivy. Možnosti jsou neomezené, když spojíte výkonný OCR engine s několika řádky C#.

Máte otázky ohledně zpracování více‑stránkových TIFF, nebo chcete vědět, jak to integrovat do ASP.NET Core API? Zanechte komentář níže a šťastné kódování!

## Související tutoriály

- [Extrahovat text z obrázku v C# s výběrem jazyka pomocí Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Jak extrahovat text z obrázku přípravou obdélníků v OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extrahovat text z obrázku – rozpoznat řádek pomocí Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}