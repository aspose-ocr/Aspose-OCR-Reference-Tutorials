---
category: general
date: 2025-12-29
description: Vytvořte prohledávatelný PDF z vícestránkového TIFF a naučte se, jak
  převést TIFF na PDF, extrahovat text z TIFF a programově generovat PDF.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- convert image to pdf
- how to generate pdf
- extract text from tiff
language: cs
og_description: Vytvořte prohledávatelný PDF z vícestránkového TIFF pomocí Aspose
  OCR. Naučte se, jak převést TIFF na PDF, extrahovat text z TIFF a generovat PDF
  v C#.
og_title: Vytvořte prohledávatelný PDF z TIFF – krok za krokem C# tutoriál
tags:
- Aspose OCR
- C#
- PDF/A
- Document Automation
title: Vytvořte prohledávatelný PDF z TIFF – Kompletní C# průvodce
url: /cs/net/text-recognition/create-searchable-pdf-from-tiff-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF z TIFF – Kompletní průvodce v C#

Už jste někdy potřebovali **vytvořit prohledávatelné PDF** ze skenovaného TIFF, ale nebyli jste si jisti, kde začít? Nejste v tom sami – mnoho vývojářů narazí na tento problém, když potřebují dokument PDF/A‑2b, který může být indexován vyhledávači. V tomto tutoriálu projdeme přesně kód, který potřebujete, vysvětlíme, proč je každý řádek důležitý, a ukážeme vám, jak **převést tiff na pdf** bez ztráty textu.

Také se dotkneme souvisejících úkolů, jako je **převést obrázek na pdf**, odpovíme na **jak generovat pdf** v C# a ukážeme, jak **extrahovat text z tiff** pomocí Aspose.OCR. Na konci budete mít připravený ukázkový kód, který můžete vložit do libovolného .NET projektu.

---

## Co naučíte

- Nastavit OCR engine pomocí Aspose.OCR.
- Načíst více‑stránkový TIFF soubor a spustit rozpoznávání textu.
- Uložit výsledek OCR jako prohledávatelný dokument PDF/A‑2b.
- Zvládnout běžné úskalí (velké soubory, využití paměti, nastavení DPI).
- Rozšířit řešení na jiné formáty obrázků nebo dávkové zpracování.

**Požadavky**  
- .NET 6.0 nebo novější (kód také funguje na .NET Framework 4.8).  
- Platná licence Aspose.OCR (nebo dočasný evaluační klíč).  
- Visual Studio 2022 nebo jakékoli C# IDE, které preferujete.

---

## Krok 1 – Instalace NuGet balíčku Aspose.OCR

Než budeme moci **vytvořit prohledávatelné pdf**, potřebujeme OCR knihovnu, která provádí těžkou práci.

```bash
dotnet add package Aspose.OCR
```

> **Tip:** Pokud používáte CI pipeline, připněte konkrétní verzi (např. `Aspose.OCR --version 23.10`), abyste se vyhnuli neočekávaným breaking changes.

---

## Krok 2 – Inicializace OCR Engine

Vytvoření engine je první věc, kterou uděláte, když chcete **převést tiff na pdf**. Engine uchovává konfiguraci jako jazyk, rozlišení a výkonnostní příznaky.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create an OCR engine instance – this object will be reused for every image.
var ocrEngine = new OcrEngine
{
    // Optional: set language to English (default is English + Latin).
    Language = Language.English,
    // Optional: improve speed for large files by limiting the max memory usage.
    // MaxMemoryUsage = 1024 * 1024 * 200 // 200 MB
};
```

*Proč je to důležité:* Inicializace engine jednou a její opětovné použití snižuje režii, zejména když později **převádíte obrázek na pdf** v dávkovém úkolu.

---

## Krok 3 – Načtení více‑stránkového TIFF

Aspose.OCR pracuje s třídou `Image` ze stejné knihovny. Načtení více‑stránkového TIFF je tak jednoduché, jako ukázat na cestu k souboru.

```csharp
// Load the TIFF file from disk. Replace the path with your actual location.
var inputImage = Image.Load(@"C:\Docs\input.tif");

// If you need to work with a different format (PNG, JPEG), the same method works.
```

*Hraniční případ:* Některé TIFF soubory obsahují kompresi, kterou Aspose.OCR nedokáže přečíst. Pokud narazíte na výjimku, zkuste nejprve převést TIFF do nekomprimovaného formátu (např. pomocí ImageMagick).

---

## Krok 4 Spuštění OCR a získání výsledku

Nyní skutečně **extrahujeme text z tiff**. Metoda `Recognize` vrací `OcrResult`, který obsahuje jak prostý text, tak PDF reprezentaci.

```csharp
// Perform OCR on the loaded image.
OcrResult ocrResult = ocrEngine.Recognize(inputImage);

// The result includes recognized text (ocrResult.Text) and a PDF stream.
Console.WriteLine("Recognized characters: " + ocrResult.Text.Length);
```

*Co se děje pod kapotou?* Engine prohledá každou stránku, spustí model neuronové sítě pro detekci znaků a vytvoří prohledávatelnou textovou vrstvu, která bude později vložena do PDF.

---

## Krok 5 – Uložení jako prohledávatelné PDF/A‑2b

Nakonec **vytvoříme prohledávatelné pdf** uložením výsledku OCR ve formátu PDF/A‑2b. PDF/A‑2b je archivní standard, který zaručuje dlouhodobou čitelnost.

```csharp
// Save the OCR result as a searchable PDF/A‑2b file.
string outputPath = @"C:\Docs\output.pdf";
ocrResult.Save(outputPath, SaveFormat.PdfA2b);

Console.WriteLine($"Searchable PDF saved to: {outputPath}");
```

*Proč PDF/A‑2b?* Na rozdíl od běžného PDF, PDF/A‑2b vkládá všechny fonty a barevné profily, což zajišťuje, že dokument bude vypadat stejně i po letech – ideální pro odvětví s přísnými požadavky na shodu.

---

## Kompletní funkční příklad

Níže je kompletní program, který můžete zkopírovat a vložit do konzolové aplikace. Obsuje všechny výše uvedené kroky a také malou část ošetření chyb.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Initialize OCR engine
                var ocrEngine = new OcrEngine
                {
                    Language = Language.English
                };

                // 2️⃣ Load the multi‑page TIFF
                string inputPath = @"C:\Docs\input.tif";
                var inputImage = Image.Load(inputPath);

                // 3️⃣ Recognize text
                OcrResult ocrResult = ocrEngine.Recognize(inputImage);
                Console.WriteLine($"Extracted {ocrResult.Text.Length} characters.");

                // 4️⃣ Save as searchable PDF/A‑2b
                string outputPath = @"C:\Docs\output.pdf";
                ocrResult.Save(outputPath, SaveFormat.PdfA2b);
                Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
            }
        }
    }
}
```

*Očekávaný výstup:* Po spuštění uvidíte řádek v konzoli potvrzující počet znaků a další řádek potvrzující umístění PDF. Otevření `output.pdf` v Adobe Acrobat vám umožní vyhledávat jakékoli slovo, které se objevilo v původním TIFF.

---

## Vizualizace

![Příklad vytvoření prohledávatelného PDF z TIFF](https://example.com/images/create-searchable-pdf.png "Příklad vytvoření prohledávatelného PDF z TIFF")

*Snímek obrazovky ukazuje PDF otevřené v Acrobat s vyhledávacím panelem zvýrazňujícím nalezený text.*

---

## Časté otázky a tipy

### 1. Co když má TIFF mnoho stránek (např. 500)?

Zpracování obrovského souboru najednou může vyčerpat paměť. Rozdělte soubor na menší dávky pomocí `Image.Split()` nebo knihovny třetí strany a poté procházejte každou dávku se stejnou instancí `ocrEngine`.

### 2. Můžu změnit výstup PDF na běžné PDF místo PDF/A?

Jistě—stačí nahradit `SaveFormat.PdfA2b` za `SaveFormat.Pdf`. Mějte na paměti, že ztratíte dlouhodobé archivní záruky.

### 3. Jak **převést obrázek na pdf** bez OCR (např. pro netextové obrázky)?

Použijte přímo `Image.Save(outputPath, SaveFormat.Pdf)`. Nebude přidána OCR vrstva, ale obrázek bude vložen jako stránka.

### 4. Podporuje OCR jazyky jiné než angličtinu?

Ano. Nastavte `ocrEngine.Language = Language.Spanish` (nebo libovolný podporovaný enum). Také můžete načíst vlastní jazykový balíček, pokud je potřeba.

### 5. Co DPI a kvalita obrazu?

Vyšší DPI zvyšuje přesnost, ale prodlužuje dobu zpracování. Dobré pravidlo je 300 dpi pro skenované dokumenty. Můžete to nastavit pomocí `ocrEngine.Dpi = 300`.

---

## Rozšíření řešení

- **Dávková konverze:** Zabalte hlavní logiku do `foreach`, který prochází adresář s TIFF soubory.
- **Integrace do cloudu:** Nahrajte vygenerované PDF na Azure Blob Storage nebo Amazon S3 hned po uložení.
- **Vkládání metadat:** Použijte Aspose.PDF k přidání názvu, autora a vlastních metadat do prohledávatelného PDF.

---

## Závěr

Právě jsme **vytvořili prohledávatelné PDF** z více‑stránkového TIFF pomocí Aspose.OCR, probírali, jak **převést tiff na pdf**, prozkoumali způsoby **převést obrázek na pdf**, odpověděli na **jak generovat pdf** programově a ukázali vám, jak **extrahovat text z tiff** efektivně. S kompletním ukázkovým kódem jej můžete vložit do libovolného C# projektu a začít vytvářet soubory PDF/A‑2b, které jsou okamžitě prohledávatelné.

Další kroky? Zkuste zpracovat dávku faktur, experimentovat s různými jazykovými nastaveními nebo zkombinovat tento workflow s dokumentovým systémem. Možnosti jsou neomezené, jakmile budete vědět, jak **vytvořit prohledávatelné pdf** ve velkém měřítku.

Pokudazíte na nějaké potíže nebo máte nápady na vylepšení, neváhejte zanechat komentář. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}