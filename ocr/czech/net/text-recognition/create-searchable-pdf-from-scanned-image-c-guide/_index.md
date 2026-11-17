---
category: general
date: 2026-04-26
description: Vytvořte prohledávatelný PDF ze skenovaného obrázku pomocí Aspose OCR
  v C#. Naučte se, jak převést skenovaný obrázek, extrahovat text a rychle vygenerovat
  prohledávatelný PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned image
- extract text from image
- how to ocr document
- convert tiff to pdf
language: cs
og_description: Vytvořte prohledávatelný PDF ze skenovaného obrázku pomocí Aspose
  OCR. Krok za krokem C# kód pro převod, extrakci textu a generování prohledávatelného
  PDF.
og_title: Vytvořte prohledávatelný PDF ze skenovaného obrázku – průvodce C#
tags:
- Aspose OCR
- C#
- PDF
- OCR
title: Vytvořte prohledávatelný PDF ze skenovaného obrázku – průvodce C#
url: /cs/net/text-recognition/create-searchable-pdf-from-scanned-image-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF ze skenovaného obrázku – C# průvodce

Už jste někdy potřebovali **vytvořit prohledávatelné PDF** soubory z papírových smluv, účtenek nebo starých archivů? Nejste v tom sami — většina vývojářů narazí na tento problém, když klient předá hromadu TIFF skenů a očekává prohledávatelné PDF jako finální výstup.  

V tomto tutoriálu vám ukážeme přesně **jak OCR dokument** a převést skenovaný obrázek na **prohledávatelné PDF** pomocí Aspose OCR pro .NET. Na konci budete schopni **převést skenovaný obrázek**, **extrahovat text z obrázku** a dokonce zpracovat více‑stránkové TIFF soubory bez potíží.

## Co budete potřebovat

* .NET 6.0 nebo novější (API funguje s .NET Core, .NET Framework a .NET 5+).  
* Platná licence Aspose OCR nebo jste spokojeni s evaluační vodotiskem.  
* Nainstalovaný NuGet balíček `Aspose.OCR` (`dotnet add package Aspose.OCR`).  
* Vzorkový TIFF soubor (např. `contract_scan.tif`), který chcete převést na prohledávatelné PDF.

To je vše — žádné extra knihovny, žádná složitá konfigurace. Připravení? Jdeme na to.

![Create searchable PDF example](create-searchable-pdf.png "create searchable pdf example")

## Krok 1 – Inicializace OCR enginu (Vytvoření prohledávatelného PDF)

Nejprve potřebujete instanci `OcrEngine`. Tento objekt je hlavní pracovník, který čte bitmapu, rozpoznává znaky a vrací vám text zpět.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine which language to look for – Latin works for most English documents
ocrEngine.Language = Language.Latin;
```

**Proč nastavit jazyk?**  
Pokud jej necháte na výchozím nastavení, Aspose bude zkoušet všechny jazykové balíčky, což zpomaluje. Nastavením `Language.Latin` řeknete enginu, aby se soustředil na latinskou abecedu, což zvyšuje rychlost a poskytuje přesnější výsledky pro anglické smlouvy.

## Krok 2 – Načtení vašeho skenovaného obrázku (Převod skenovaného obrázku)

Nyní předáme enginu obrázek, který chceme zpracovat. Aspose může číst cestu k souboru, stream nebo dokonce `byte[]`. Pro jednoduchost použijeme `ImageStream.FromFile`.  

```csharp
// Load the TIFF (or any supported image format)
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\contract_scan.tif");
```

Pokud budete někdy potřebovat **převést TIFF na PDF**, mějte na paměti, že více‑stránkové TIFFy jsou zpracovány automaticky — každý rámec se stane samostatnou PDF stránkou.

## Krok 3 – Spuštění OCR a získání textu (Extrahování textu z obrázku)

Spuštění OCR je tak jednoduché jako zavolat `Recognize`. Engine vrátí `RecognitionResult`, který obsahuje čistý text, skóre důvěry a informace o rozložení.  

```csharp
// Perform the OCR operation
RecognitionResult result = ocrEngine.Recognize();

// The raw text is available via the Text property
string extractedText = result.Text;

// Quick sanity check – print the first 200 characters
Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**Tip:** Pokud potřebujete jen text (žádné PDF), můžete zde zastavit a zapsat `extractedText` do souboru `.txt`. Většinou je však naším cílem prohledávatelné PDF, takže budeme pokračovat.

## Krok 4 – Uložení jako prohledávatelné PDF (Vytvoření prohledávatelného PDF)

Aspose dělá poslední krok triviálním: stačí zavolat `Save` s `SaveFormat.PdfSearchable`. Pod kapotou knihovna vloží extrahovaný text jako neviditelnou vrstvu a zachová původní vzhled obrázku.  

```csharp
// Save the result as a searchable PDF
ocrEngine.Save(@"C:\Docs\contract_searchable.pdf", SaveFormat.PdfSearchable);
```

Když otevřete `contract_searchable.pdf` v libovolném PDF prohlížeči, budete moci text vybrat, kopírovat a vyhledávat — přesně to, co klient očekává od „prohledávatelného PDF“.

## Zpracování více‑stránkových TIFFů (Převod TIFF na PDF)

Pokud váš zdrojový soubor obsahuje několik stránek, Aspose automaticky zachází s každým rámcem jako s oddělenou stránkou. Žádné extra smyčky nejsou potřeba. Nicméně můžete chtít nastavit DPI nebo kvalitu obrázku pro každou stránku:

```csharp
// Optional: tweak image processing settings before OCR
ocrEngine.ImageProcessingOptions.Dpi = 300; // higher DPI improves accuracy
ocrEngine.ImageProcessingOptions.Compression = ImageCompression.Jpeg;
```

Po nastavení těchto možností opakujte **Krok 2** pro každý rámec, nebo jednoduše nasměrujte `ImageStream.FromFile` na více‑stránkový TIFF a nechte Aspose udělat těžkou práci.

## Časté problémy a jak je vyřešit

| Příznak | Pravděpodobná příčina | Oprava |
|---------|-----------------------|--------|
| Text je zkreslený nebo chybí | Nesprávně nastavený jazyk | Nastavte `ocrEngine.Language` na správný jazykový balíček (např. `Language.German`). |
| PDF je obrovské (10 MB pro jednostránkový sken) | Výchozí komprese obrázku je nízká | Upravte `ocrEngine.ImageProcessingOptions.Compression` na `Jpeg` a nastavte rozumnou hodnotu `Quality` (0‑100). |
| OCR běží velmi pomalu | Používá se výchozí detekce jazyka `Auto` | Výslovně nastavte očekávaný jazyk. |
| Nezobrazí se prohledávatelná vrstva | Uloženo pomocí `SaveFormat.Pdf` místo `PdfSearchable` | Použijte `PdfSearchable`. |

## Kompletní příklad od začátku do konce

Spojením všech částí získáte připravenou konzolovou aplikaci, kterou můžete zkopírovat a vložit do Visual Studia:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.Latin,
                // Optional: improve accuracy for low‑resolution scans
                ImageProcessingOptions = { Dpi = 300, Compression = ImageCompression.Jpeg }
            };

            // 2️⃣ Load the scanned image (convert scanned image)
            string inputPath = @"C:\Docs\contract_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Run OCR and extract text (extract text from image)
            RecognitionResult result = ocrEngine.Recognize();
            Console.WriteLine("First 200 characters of extracted text:");
            Console.WriteLine(result.Text.Substring(0, Math.Min(200, result.Text.Length)));

            // 4️⃣ Save as searchable PDF (create searchable pdf)
            string outputPath = @"C:\Docs\contract_searchable.pdf";
            ocrEngine.Save(outputPath, SaveFormat.PdfSearchable);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Co uvidíte:**  
* Konzolové okno, které vypíše úryvek OCR‑ovaného textu.  
* Soubor `contract_searchable.pdf` ležící vedle vašeho původního TIFF. Otevřete jej, stiskněte **Ctrl + F** a vyhledejte libovolné slovo, které se vyskytovalo v původním skenu — voilà, funguje.

## Další kroky a související témata

* **How to OCR document** batchy – zabalte výše uvedený kód do smyčky `foreach` a zpracujte celý adresář.  
* **Convert scanned image** formáty jiných než TIFF (PNG, JPEG) – stejná API funguje; stačí změnit příponu souboru.  
* **Extract text from image** pro další analýzu – předávejte `result.Text` do pipeline zpracování přirozeného jazyka.  
* **Optimize PDF size** – prozkoumejte `PdfSaveOptions` pro další kompresi obrázků nebo vkládání fontů jen když je to potřeba.  

Experimentujte s těmito nápady a rychle se stanete osobou, na kterou se obrací každý s požadavkem „převést tento sken na prohledávatelné PDF“.

---

### TL;DR

Nyní víte, jak **vytvořit prohledávatelné PDF** soubory ze skenovaných obrázků pomocí Aspose OCR v C#. Proces je: inicializovat engine, načíst obrázek, spustit OCR a uložit s `PdfSearchable`. Nastavte jazykové parametry, DPI a kompresi pro zvládnutí okrajových případů a jste připraveni **převést skenovaný obrázek**, **extrahovat text z obrázku** a dokonce **převést TIFF na PDF** ve velkém měřítku. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}