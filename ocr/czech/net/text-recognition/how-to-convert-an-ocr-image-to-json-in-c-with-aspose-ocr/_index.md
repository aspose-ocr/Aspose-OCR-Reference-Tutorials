---
category: general
date: 2026-09-06
description: Převod OCR obrazu na JSON v C# pomocí Aspose.OCR – krok za krokem průvodce
  extrakcí textu z obrázku a získáním výstupu ve formátu JSON.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- ocr image to json
- extract text from image
- convert image to text
- recognize text from photo
- load image for ocr
language: cs
lastmod: 2026-09-06
og_description: OCR obrázek do JSON v C# s Aspose.OCR. Naučte se, jak načíst obrázek
  pro OCR, rozpoznat text z fotografie a převést výsledek do JSON.
og_image_alt: Screenshot of C# code that converts an OCR image to JSON using Aspose.OCR
og_title: Převod OCR obrázku do JSON v C# – kompletní průvodce Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-09-06'
  description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  headline: How to convert an OCR image to JSON in C# with Aspose.OCR
  type: TechArticle
- description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  name: How to convert an OCR image to JSON in C# with Aspose.OCR
  steps:
  - name: Place an image named `input.jpg` in the project root.
    text: Place an image named `input.jpg` in the project root.
  - name: Execute `dotnet run`.
    text: Execute `dotnet run`.
  - name: Observe the console output and open `output.json` to see the structured
      data.
    text: Observe the console output and open `output.json` to see the structured
      data.
  type: HowTo
- questions:
  - answer: Yes. Use `ocrEngine.SaveJson(Stream)` to write directly to a `MemoryStream`,
      then call `stream.ToArray()`.
    question: Can I get the OCR result as a byte array instead of a file?
  - answer: Aspose.OCR can accept PDF pages converted to images via Aspose.PDF, but
      the OCR engine itself works on raster images. Convert PDFs to images first,
      then **load image for ocr**.
    question: Does the engine support PDF input?
  - answer: 'Set `ocrEngine.Language = OcrLanguage.Arabic`. The JSON includes the
      correct text direction, which you can render in UI frameworks that support RTL.
      ## Conclusion You now have a complete solution for **ocr image to json** in
      C#. By loading an image, configuring the language, running the OCR engine, '
    question: How do I handle right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- JSON
- Image processing
title: Jak převést OCR obrázek na JSON v C# pomocí Aspose.OCR
url: /cs/net/text-recognition/how-to-convert-an-ocr-image-to-json-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak převést OCR obrázek na JSON v C# s Aspose.OCR

Pokud potřebujete **ocr image to json** v .NET aplikaci, tento návod vám ukáže, jak to provést pomocí Aspose.OCR. Provedeme vás načtením obrázku pro OCR, rozpoznáním textu z fotografie a konverzí výsledku do JSON, abyste mohli data využít v API nebo databázích.

Extrahování textu z obrazových souborů je běžná potřeba při zpracování faktur, skenování účtenek a archivních projektech. Na konci tohoto tutoriálu budete schopni **convert image to text**, získat výsledek jako prostý text a vygenerovat strukturovaný JSON payload, který zachovává informace o rozložení.

## Požadavky

Než začnete, ujistěte se, že máte:

- .NET 6.0 SDK nebo novější nainstalovaný  
- Visual Studio 2022 (nebo jakýkoli editor podporující .NET)  
- NuGet balíček Aspose.OCR (`Aspose.OCR`) přidaný do vašeho projektu  
- Ukázkový obrázek (`input.jpg`) umístěný ve složce, na kterou můžete odkazovat z kódu  

Nemusíte instalovat žádné další OCR enginy; Aspose.OCR zvládne těžkou práci interně.

## Krok 1: Nainstalujte NuGet balíček Aspose.OCR

Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package Aspose.OCR
```

Balíček obsahuje třídu `Aspose.OCR.OcrEngine`, která poskytuje metody pro **load image for ocr**, výběr jazyka a export výsledků.

## Krok 2: Vytvořte nový C# konzolový projekt

Pokud ještě nemáte projekt, vytvořte jej:

```bash
dotnet new console -n OcrToJsonDemo
cd OcrToJsonDemo
```

Přidejte `using` direktivy, které budete potřebovat:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;
```

## Krok 3: Načtěte obrázek a nakonfigurujte OCR engine

Následující kód ukazuje, jak **load image for ocr**, nastavit jazyk a připravit engine ke zpracování. V tomto příkladu používáme cyriliku, ale můžete přepnout na `OcrLanguage.English`, `OcrLanguage.French` atd., podle zdrojového jazyka.

```csharp
// Step 3: Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Choose the language that matches the text in the image.
// Replace OcrLanguage.Cyrillic with the language you need.
ocrEngine.Language = OcrLanguage.Cyrillic;

// Load the image file. The ImageStream class abstracts file, stream, or byte[] sources.
string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **Proč je to důležité:** Nastavení správného jazyka dramaticky zvyšuje přesnost, když **recognize text from photo**. Engine používá jazykově specifické slovníky a znakové sady.

## Krok 4: Spusťte OCR proces a získejte výsledky

Nyní spusťte OCR engine. Pokud proces uspěje, můžete **extract text from image** jako prostý text, HTML nebo JSON. Aspose.OCR poskytuje metodu `SaveJson`, která zapíše strukturovaný výsledek do souboru.

```csharp
// Step 4: Execute the OCR process
if (ocrEngine.Process())
{
    // Plain‑text output
    string plainText = ocrEngine.Text;
    Console.WriteLine("=== Plain Text ===");
    Console.WriteLine(plainText);

    // JSON output – includes bounding boxes, confidence scores, and line information
    string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
    ocrEngine.SaveJson(jsonPath);
    Console.WriteLine($"\nJSON result saved to: {jsonPath}");
}
else
{
    Console.WriteLine("OCR processing failed. Check the image path and format.");
}
```

### Očekávaná struktura JSON

Typický soubor `output.json` vypadá takto (formátováno pro čitelnost):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Пример текста",
          "Confidence": 0.96,
          "Rect": { "X": 45, "Y": 120, "Width": 210, "Height": 30 }
        },
        {
          "Text": "Еще одна строка",
          "Confidence": 0.93,
          "Rect": { "X": 45, "Y": 160, "Width": 230, "Height": 28 }
        }
      ]
    }
  ]
}
```

JSON payload obsahuje text každého řádku, skóre důvěry a obdélník, který řádek v původní fotografii ohraničuje. To usnadňuje mapování OCR výsledku zpět na UI prvky nebo databázová pole.

## Krok 5: Kompletní zdrojový kód pro demo

Níže je kompletní, připravený k spuštění program, který provádí workflow **ocr image to json**. Zkopírujte jej do `Program.cs` a spusťte `dotnet run`.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrToJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Select the language (Cyrillic in this example)
            ocrEngine.Language = OcrLanguage.Cyrillic;

            // 3️⃣ Load the image you want to process
            string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found: {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Run the OCR process
            if (ocrEngine.Process())
            {
                // 5️⃣ Retrieve plain text (optional)
                string plainText = ocrEngine.Text;
                Console.WriteLine("=== Plain Text ===");
                Console.WriteLine(plainText);

                // 6️⃣ Save the result as JSON
                string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
                ocrEngine.SaveJson(jsonPath);
                Console.WriteLine($"\nJSON result saved to: {jsonPath}");
            }
            else
            {
                Console.WriteLine("OCR processing failed. Verify the image format and language settings.");
            }
        }
    }
}
```

### Spuštění příkladu

1. Umístěte obrázek pojmenovaný `input.jpg` do kořenové složky projektu.  
2. Proveďte `dotnet run`.  
3. Sledujte výstup v konzoli a otevřete `output.json`, abyste viděli strukturovaná data.

## Profesionální tipy a běžné úskalí

| Situace | Doporučení |
|-----------|----------------|
| **Nízké rozlišení fotografií** | Zvyšte DPI před zpracováním nebo použijte `ocrEngine.Image = ImageStream.FromFile(path, 300)` k vynucení 300 DPI. |
| **Smíšené jazyky** | Nastavte `ocrEngine.Language = OcrLanguage.Multilingual` a případně poskytněte seznam jazyků pomocí `ocrEngine.Language = new[] { OcrLanguage.English, OcrLanguage.Cyrillic }`. |
| **Velké dokumenty** | Zpracovávejte jednu stránku najednou, aby se snížila spotřeba paměti; engine podporuje více-stránkové TIFFy. |
| **Nesprávné znaky** | Ověřte, že je vybrán správný `OcrLanguage`; použití špatného jazyka snižuje přesnost, když **convert image to text**. |
| **JSON postrádá pole** | Ujistěte se, že používáte Aspose.OCR verze 23.6 nebo novější; starší verze neobsahovaly metodu `SaveJson`. |

## Často kladené otázky

**Q: Můžu získat OCR výsledek jako pole bajtů místo souboru?**  
A: Ano. Použijte `ocrEngine.SaveJson(Stream)`, který zapíše přímo do `MemoryStream`, a poté zavolejte `stream.ToArray()`.

**Q: Podporuje engine vstupní PDF?**  
A: Aspose.OCR může přijímat PDF stránky převedené na obrázky pomocí Aspose.PDF, ale samotný OCR engine pracuje jen s rastrovými obrázky. Nejprve převěďte PDF na obrázky a pak **load image for ocr**.

**Q: Jak zacházet se skripty psanými zprava doleva, jako je arabština?**  
A: Nastavte `ocrEngine.Language = OcrLanguage.Arabic`. JSON zahrnuje správný směr textu, který můžete vykreslit v UI frameworkech podporujících RTL.

## Závěr

Nyní máte kompletní řešení pro **ocr image to json** v C#. Načtením obrázku, nastavením jazyka, spuštěním OCR engine a exportem výsledku jako JSON můžete **extract text from image**, **convert image to text** a **recognize text from photo** v jednom plynulém workflow.  

Odtud můžete dál:

- Integrovat JSON výstup s Web API (`ASP.NET Core`)  
- Uložit výsledek do NoSQL databáze jako MongoDB  
- Přidat post‑processing pro opravu běžných OCR chyb  

Neváhejte experimentovat s různými jazyky, formáty obrázků a možnostmi výstupu, aby vyhovovaly potřebám vašeho projektu. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [recognize text from image in C# – Complete Guide to OCR and JSON](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/)
- [Convert Image to Text in C# with Aspose OCR – Step‑by‑Step Guide](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}