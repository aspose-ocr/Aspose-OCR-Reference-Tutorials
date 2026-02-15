---
category: general
date: 2026-02-14
description: Naučte se provádět OCR na souboru TIFF nebo obrázku a převést PDF pomocí
  OCR na prohledávatelný PDF — krok za krokem průvodce v C#.
draft: false
keywords:
- how to perform OCR
- convert pdf using OCR
- make searchable pdf
- tiff to searchable pdf
- searchable pdf from image
language: cs
og_description: Objevte, jak provádět OCR na obrázcích, převádět PDF pomocí OCR a
  vytvořit prohledávatelný PDF s Aspose OCR v stručném tutoriálu v C#.
og_title: Jak provést OCR a vytvořit prohledávatelný PDF v C#
tags:
- OCR
- C#
- Aspose
- PDF conversion
title: Jak provést OCR a vytvořit prohledávatelný PDF v C#
url: /cs/net/text-recognition/how-to-perform-ocr-and-create-a-searchable-pdf-in-c/
---

.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést OCR a vytvořit prohledávatelný PDF v C#

Už jste někdy potřebovali **provést OCR** na naskenovaném dokumentu, ale nebyli jste si jisti, jak výsledek převést na prohledávatelný PDF? Nejste v tom sami — mnoho vývojářů narazí na tuto překážku při práci se starými archivy TIFF nebo PDF obsahujícími jen obrázky. Dobrá zpráva? S několika řádky C# a knihovnou Aspose.OCR můžete převést TIFF nebo jakýkoli obrázek na plně prohledávatelný PDF během několika sekund.

V tomto tutoriálu vás provedeme vším, co potřebujete vědět: od instalace knihovny, načtení vícestránkového TIFF, až po volání `RecognizeToPdf`, abyste mohli **convert PDF using OCR** a **make searchable PDF** soubory, které vaši uživatelé skutečně mohou prohledávat. Na konci budete mít připravenou konzolovou aplikaci, která z obrázkového zdroje vytvoří prohledávatelný PDF.

## Požadavky

- **.NET 6.0** nebo novější (kód také funguje na .NET Framework 4.7+).
- Platná licence **Aspose.OCR** nebo dočasný evaluační klíč (bezplatná zkušební verze stačí pro testování).
- Visual Studio 2022 (nebo jakýkoli editor, který preferujete) s **NuGet** správcem balíčků.
- Vstupní soubor pojmenovaný `input.tif` umístěný ve složce, kterou ovládáte — více­stránkové TIFF fungují ihned.

> **Tip:** Pokud používáte Windows, zkopírujte TIFF do stejné složky jako zkompilovaný `.exe`, abyste se vyhnuli problémům s cestami.

## Krok 1: Instalace NuGet balíčku Aspose.OCR

Otevřete složku projektu v terminálu a spusťte:

```bash
dotnet add package Aspose.OCR
```

Tím se stáhne nejnovější stabilní verze (k únoru 2026 je to 23.10) a přidají se všechny potřebné závislosti. Po dokončení obnovení uvidíte `Aspose.OCR` uvedený pod **Dependencies** v Solution Exploreru.

## Krok 2: Vytvoření minimální konzolové aplikace

Vytvořte nový konzolový projekt, pokud ještě žádný nemáte:

```bash
dotnet new console -n OcrSearchablePdfDemo
cd OcrSearchablePdfDemo
```

Nahraďte automaticky vygenerovaný `Program.cs` kompletním kódem uvedeným v **Krok 3**. Program:

1. Vytvoří instanci OCR enginu.
2. Načte zdrojový obrázek (nebo více­stránkový TIFF).
3. Spustí OCR a zapíše výstup přímo do prohledávatelného PDF.
4. Upozorní uživatele, že proces byl úspěšný.

## Krok 3: Kompletní funkční kód — od obrázku k prohledávatelnému PDF

Níže je **celý** zdrojový soubor. Zkopírujte jej do `Program.cs`. Komentáře jsou zahrnuty pro vysvětlení méně zřejmých částí.

```csharp
using System;
using Aspose.OCR;          // Core OCR namespace
using Aspose.OCR.Image;   // Provides ImageStream helpers

namespace OcrSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialise the OCR engine.
            // -------------------------------------------------
            // The Engine class is the entry point for all OCR operations.
            // You can optionally pass a license object here if you have one.
            var ocrEngine = new Engine();

            // -------------------------------------------------
            // 2️⃣ Load the source image.
            // -------------------------------------------------
            // ImageStream.FromFile supports TIFF, PDF, JPEG, PNG, etc.
            // For multi‑page TIFFs the stream automatically contains all pages.
            string inputPath = "YOUR_DIRECTORY/input.tif";
            var imageStream = ImageStream.FromFile(inputPath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR and write a searchable PDF.
            // -------------------------------------------------
            // RecognizeToPdf does the heavy lifting:
            // • It runs the OCR engine on every page.
            // • It embeds the extracted text as an invisible layer.
            // • The visual appearance of the original image is preserved.
            string outputPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.RecognizeToPdf(imageStream, outputPath);

            // -------------------------------------------------
            // 4️⃣ Inform the user.
            // -------------------------------------------------
            Console.WriteLine("Searchable PDF created at: " + outputPath);
        }
    }
}
```

**Co uvidíte:** Po spuštění programu se ve výstupní složce objeví soubor `searchable.pdf`. Otevřete jej v Adobe Readeru nebo jakémkoli PDF prohlížeči a zkuste vyhledat slovo, které je v původním TIFF. Text by měl být nalezen okamžitě, což dokazuje, že jste úspěšně **made searchable PDF** z obrázku.

### Spuštění aplikace

```bash
dotnet run
```

Pokud je vše nastaveno správně, získáte:

```
Searchable PDF created at: YOUR_DIRECTORY/searchable.pdf
```

Otevřete PDF, stiskněte `Ctrl+F`, zadejte slovo ze zdroje a sledujte, jak zvýraznění skočí na správné místo.

## Krok 4: Běžné varianty a okrajové případy

### Převod běžného PDF (pouze obrázky) na prohledávatelný PDF

Pokud je vaším zdrojem PDF, který obsahuje naskenované obrázky místo textu, můžete stále použít stejnou metodu — stačí změnit zdroj `ImageStream`:

```csharp
var pdfStream = ImageStream.FromFile("YOUR_DIRECTORY/input.pdf");
ocrEngine.RecognizeToPdf(pdfStream, "YOUR_DIRECTORY/searchable_from_pdf.pdf");
```

Tím se vyřeší scénář **convert pdf using OCR** bez jakéhokoli dalšího kódu.

### Zpracování velkých více­stránkových dokumentů

Pro dokumenty přesahující několik stovek stránek zvažte:

- **Zvýšení limitu paměti** (`Engine.MemoryLimit = 2_000; // MB`).
- **Zpracování po částech**: načtěte podmnožinu stránek, zapište mezilehlé PDF a poté je sloučte pomocí PDF knihovny (např. Aspose.PDF).

### Práce s jazyky jinými než angličtina

Aspose.OCR podporuje mnoho jazyků ihned po instalaci. Nastavte jazyk před rozpoznáním:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Pokud potřebujete **tiff to searchable pdf** v ne‑latinské abecedě, ujistěte se, že je nainstalován odpovídající jazykový balíček.

### Co když je výstupní PDF prázdný?

- Ověřte, že vstupní soubor není poškozený.
- Zajistěte, aby OCR engine měl platnou licenci — režim hodnocení může ukládat omezení počtu stránek.
- Zkontrolujte, že rozlišení obrázku je alespoň 300 dpi; nižší rozlišení může způsobit špatné rozpoznání.

## Krok 5: Programové ověření výsledku (volitelné)

Někdy chcete potvrdit, že PDF skutečně obsahuje textovou vrstvu. Můžete použít Aspose.PDF k extrakci textu:

```csharp
using Aspose.Pdf;

var pdfDoc = new Document("YOUR_DIRECTORY/searchable.pdf");
string extracted = pdfDoc.Pages[1].ExtractText();
Console.WriteLine("First page text snippet: " + extracted.Substring(0, 100));
```

Pokud `extracted` není prázdný, úspěšně jste **made searchable pdf**.

## Závěr

Přehledně jsme pokryli **how to perform OCR** na TIFF (nebo jakýkoli obrázek) a bezproblémově **convert PDF using OCR** k vytvoření **searchable PDF**, který se chová jako nativní dokument. Klíčové kroky jsou:

1. Instalace Aspose.OCR.  
2. Inicializace `Engine`.  
3. Načtení obrázku pomocí `ImageStream`.  
4. Volání `RecognizeToPdf`.  

Odtud můžete experimentovat s nastavením jazyků, zpracováním velkých dávkách nebo kombinovat výstup s dalšími úkoly manipulace s PDF. Stejný vzor funguje pro **tiff to searchable pdf**, **searchable pdf from image**, a dokonce i skenovaná PDF.

Jste připraveni na další výzvu? Zkuste vložit OCR do webového API, aby uživatelé mohli nahrávat skeny a okamžitě dostávat prohledávatelné PDF, nebo prozkoumejte OCR na ručně psaných poznámkách pomocí pokročilých nastavení `OcrEngine`. Možnosti jsou neomezené — šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}