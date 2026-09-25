---
category: general
date: 2026-02-17
description: Jak provést hromadné OCR více PDF souborů a obrázků v C# pomocí Aspose
  OCR. Naučte se extrahovat text z PDF, převádět PDF na text a rozpoznávat text z
  obrázků.
draft: false
keywords:
- how to batch OCR
- extract text from pdf
- convert pdf to text
- recognize text from images
- extract text scanned pdf
language: cs
og_description: Jak dávkově provádět OCR více dokumentů v C# s Aspose OCR. Získejte
  krok za krokem kód pro extrakci textu z PDF, převod PDF na text a rozpoznání textu
  z obrázků.
og_title: Jak dávkově zpracovávat OCR soubory v C# – Kompletní průvodce
tags:
- OCR
- C#
- Aspose
- PDF
- Text Extraction
title: Jak dávkově provádět OCR soubory v C# – kompletní ukázkový kód
url: /cs/net/text-recognition/how-to-batch-ocr-files-in-c-full-code-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provádět dávkové OCR soubory v C# – Kompletní průvodce

Už jste se někdy zamysleli nad **jak provádět dávkové OCR** zásobník PDF a skenovaných obrázků, aniž byste museli psát samostatnou smyčku pro každý soubor? Nejste v tom sami. Většina vývojářů narazí na tento problém, když potřebují získat text z desítek stránek najednou. Dobrá zpráva? S Aspose OCR můžete předat kolekci souborů jedinému enginu a nechat ho udělat těžkou práci.  

V tomto tutoriálu projdeme praktické řešení, které vám umožní **extrahovat text z pdf**, **převést pdf na text** a **rozpoznat text z obrázků** v jednom dávkovém spuštění. Na konci budete mít připravenou konzolovou aplikaci, která vytiskne výsledek OCR pro každou stránku, a pochopíte, proč se každý krok provádí, abyste jej mohli přizpůsobit svým projektům.

## Požadavky – Co potřebujete před zahájením

- **.NET 6.0 nebo novější** (kód funguje i na .NET Framework, ale .NET 6+ se doporučuje)
- **Aspose.OCR NuGet balíček** – nainstalujte jej pomocí `dotnet add package Aspose.OCR`
- Několik ukázkových souborů: více‑stránkový PDF (`doc1.pdf`) a skenovaný TIFF (`doc2.tif`). Umístěte je do složky, na kterou můžete odkazovat, např. `C:\OCRSamples`.
- Základní znalost C# – měli byste být pohodlní s `using` příkazy a kolekcemi.

> Tip: Pokud nemáte licenci, Aspose nabízí zdarma dočasný klíč, který během vývoje odstraňuje limit 100 stránek.

## Krok 1: Nastavení projektu a import jmenných prostorů

Nejprve vytvořte nový konzolový projekt (nebo přidejte do existujícího) a přidejte požadované jmenné prostory.

```csharp
// Program.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;          // Aspose OCR core library
using Aspose.OCR.Image;   // ImageStream helper class
```

> **Proč je to důležité:** Importování `Aspose.OCR.Image` vám poskytuje pohodlnou metodu `ImageStream.FromFile`, která automaticky rozděluje stránky PDF do samostatných image streamů. To je tajná ingredience, která dělá dávkové zpracování bezbolestné.

## Krok 2: Inicializace OCR enginu

Engine je hlavní komponenta, která komunikuje s podkladovým OCR enginem. Pro celou dávku potřebujete pouze jednu instanci.

```csharp
// Step 2: Create a single OcrEngine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **Vysvětlení:** Opětovné použití stejného `OcrEngine` snižuje zatížení paměti a urychluje zpracování, protože nativní knihovny zůstávají načtené mezi stránkami.

## Krok 3: Vytvoření seznamu Image Streamů

Zde shromáždíme každý dokument, který chceme zpracovat. `ImageStream.FromFile` je dostatečně chytrý na to, aby rozdělil PDF na jednotlivé stránky, takže třístránkový PDF se za scénou stane třemi samostatnými streamy.

```csharp
// Step 3: Assemble the collection of image streams
List<ImageStream> imageStreams = new List<ImageStream>
{
    ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
    ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
};
```

> **Hraniční případ:** Pokud máte směs PDF, TIFF, JPEG nebo PNG, stačí je přidat do stejného seznamu – Aspose automaticky detekuje formát.

## Krok 4: Spuštění dávkové OCR operace

Nyní předáme seznam engine. `RecognizeBatch` vrací kolekci objektů `OcrResult`, jeden pro každou stránku.

```csharp
// Step 4: Perform batch OCR on the supplied streams
IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

> **Proč dávka?** Spouštění OCR stránku po stránce v ruční smyčce nutí engine se při každém volání znovu inicializovat, což může zdvojnásobit dobu zpracování. `RecognizeBatch` udržuje engine „teplý“ a streamuje výsledky zpět, jakmile jsou k dispozici.

## Krok 5: Výstup rozpoznaného textu

Nakonec projdeme výsledky a zapíšeme text každé stránky do konzole. Zde můžete nahradit `Console.WriteLine` zápisem do souboru, vkládáním do databáze nebo jakoukoli další akcí.

```csharp
// Step 5: Display the OCR output for each page
for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResults[pageIndex].Text);
}
```

### Očekávaný výstup v konzoli

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Pokud spustíte program s ukázkovými soubory, měli byste vidět blok textu pro každou stránku, což dokazuje, že jste úspěšně **extrahovali text ze skenovaného pdf** v jednom průchodu.

## Řešení běžných problémů

| Problém | Proč k tomu dochází | Rychlé řešení |
|---------|----------------------|---------------|
| **Out‑of‑memory errors** | Velké PDF generují mnoho vysoce rozlišených obrázků. | Omezte DPI při načítání PDF: `ocrEngine.Settings.ImageDpi = 200;` |
| **Garbage characters** | Zdrojový sken je nízké kvality nebo používá nepodporovaný jazyk. | Nastavte jazyk explicitně: `ocrEngine.Language = Language.English;` |
| **Partial results** | Dávkový seznam obsahuje poškozený soubor. | Zabalte `RecognizeBatch` do try/catch a zaznamenejte `e.Message` pro problematický soubor. |
| **Performance bottleneck** | Běží na jednom vlákně na vícejádrovém stroji. | Použijte `Parallel.ForEach` s oddělenými instancemi `OcrEngine` pro každé vlákno (pokročilé). |

## Bonus: Ukládání OCR výsledků do textových souborů

Pokud dáváte přednost mít samostatný `.txt` soubor pro každou stránku, stačí přidat malý zápisový blok uvnitř smyčky:

```csharp
string outputPath = @"C:\OCRResults";
System.IO.Directory.CreateDirectory(outputPath);

for (int i = 0; i < ocrResults.Count; i++)
{
    string fileName = System.IO.Path.Combine(outputPath, $"Page_{i + 1}.txt");
    System.IO.File.WriteAllText(fileName, ocrResults[i].Text);
}
```

Nyní jste **převod pdf na text** proměnili v úhlednou složku s čistými textovými soubory – ideální pro následné indexování nebo vyhledávání.

## Kompletní funkční příklad

Níže je kompletní program připravený ke zkopírování a vložení. Žádné skryté závislosti, žádné externí skripty.

```csharp
// FullProgram.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Initialise OCR engine (reuse for the whole batch)
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: tweak settings for speed or accuracy
        ocrEngine.Settings.ImageDpi = 200;          // lower memory usage
        ocrEngine.Language = Language.English;     // set language explicitly

        // Build the list of image streams (PDF pages auto‑split)
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
            ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
        };

        // Perform batch OCR
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Output each page's text to console
        for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
        {
            Console.WriteLine($"--- Page {pageIndex + 1} ---");
            Console.WriteLine(ocrResults[pageIndex].Text);
        }

        // (Optional) Save each page to a .txt file
        string outputFolder = @"C:\OCRResults";
        System.IO.Directory.CreateDirectory(outputFolder);
        for (int i = 0; i < ocrResults.Count; i++)
        {
            string txtPath = System.IO.Path.Combine(outputFolder, $"Page_{i + 1}.txt");
            System.IO.File.WriteAllText(txtPath, ocrResults[i].Text);
        }
    }
}
```

Spusťte `dotnet run` ze složky projektu a sledujte, jak se konzole zaplní extrahovaným textem. To je **jak provádět dávkové OCR** kolekci dokumentů během několika řádků C#.

## Co jsme pokryli – Rychlý přehled

- Nastavili .NET konzolovou aplikaci a nainstalovali Aspose.OCR.  
- Vytvořili jedinou instanci `OcrEngine` pro efektivní proces.  
- Sestavili seznam objektů `ImageStream`, které automaticky rozdělují PDF na stránky.  
- Spustili `RecognizeBatch` pro **extrahování textu z pdf** a dalších formátů obrázků najednou.  
- Vytiskli výsledky a případně je uložili jako jednotlivé `.txt` soubory, čímž dokončili workflow **převod pdf na text**.

## Další kroky a související témata

- **Scale up**: Použijte `Parallel.ForEach` s poolem objektů `OcrEngine` pro souběžné zpracování stovek souborů.  
- **Language packs**: Vyměňte `Language.English` za `Language.French` nebo načtěte vlastní slovník, když potřebujete **rozpoznat text z obrázků** v jiných jazycích.  
- **Post‑processing**: Proveďte výstup OCR přes kontrolu pravopisu nebo parser přirozeného jazyka pro zvýšení přesnosti skenovaných smluv.  
- **Alternative libraries**: Porovnejte Aspose OCR s Tesseract.NET, pokud hledáte open‑source řešení – oba mohou **extrahovat text ze skenovaného pdf**, ale liší se licencí a přesností „out‑of‑the‑box“.

---

![how to batch OCR example](alt="how to batch OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}