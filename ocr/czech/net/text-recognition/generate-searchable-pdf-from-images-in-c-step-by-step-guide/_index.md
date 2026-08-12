---
category: general
date: 2026-02-22
description: Vytvořte prohledávatelný PDF a extrahujte text z obrázku pomocí Aspose
  OCR. Naučte se, jak převést obrázek na PDF a získat prostý text v jednom tutoriálu.
draft: false
keywords:
- generate searchable pdf
- extract text from image
- convert image to pdf
- output plain text
- convert scanned image pdf
language: cs
og_description: Vytvořte prohledávatelný PDF ze skenovaných obrázků pomocí Aspose
  OCR. Tento průvodce ukazuje, jak extrahovat text z obrázku, získat prostý text a
  převést obrázek do PDF.
og_title: Generování prohledávatelného PDF z obrázků – kompletní C# tutoriál
tags:
- C#
- OCR
- PDF generation
- Aspose
title: Vytvořte prohledávatelný PDF z obrázků v C# – krok za krokem
url: /cs/net/text-recognition/generate-searchable-pdf-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF z obrázků v C# – Kompletní tutoriál

Už jste někdy potřebovali **vytvořit prohledávatelné PDF** ze skenovaného obrázku, ale nevedeli jste, kde začít? Nejste v tom sami – většina vývojářů narazí na tuto překážku, když poprvé potkají OCR. Dobrá zpráva? S Aspose OCR můžete **extrahovat text z obrázku**, **vytvořit prostý text** a **převést obrázek do PDF** během několika řádků C#.

V tomto průvodci projdeme celý proces, od načtení souboru PNG po uložení prohledávatelného PDF a souboru prostého textu. Na konci budete mít znovupoužitelný úryvek, který můžete vložit do libovolného .NET projektu. Žádné zbytečnosti, jen to, co opravdu funguje.

## Co se naučíte

- Jak nastavit **Aspose.OCR** v .NET konzolové aplikaci.  
- Rozdíl mezi režimy **output plain text** a **searchable PDF**.  
- Jak **extrahovat text z obrázku** a zapsat jej do souboru `.txt`.  
- Jak **převést obrázek do PDF**, který zachová původní bitmapu a přidá skrytou textovou vrstvu.  
- Tipy pro práci s velkými dávkami, běžné úskalí a kde vyladit nastavení pro vyšší přesnost.

> **Požadavky** – Potřebujete .NET 6+ (nebo .NET Framework 4.7+), Visual Studio 2022 (nebo libovolný editor) a licenci Aspose OCR (nebo bezplatnou zkušební verzi). Žádné další knihovny třetích stran nejsou vyžadovány.

![generate searchable pdf example](image-placeholder.png "Example of a generated searchable PDF")

## Krok 1: Instalace Aspose OCR a vytvoření enginu

Nejprve přidejte NuGet balíček do svého projektu:

```bash
dotnet add package Aspose.OCR
```

Nyní můžeme spustit OCR engine a nastavit jazyk, se kterým pracujeme. Angličtina je výchozí, ale můžete přepnout na francouzštinu, španělštinu atd. změnou enumu `Language`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine for English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };
```

**Proč je to důležité:** Engine obsahuje veškerou konfiguraci – jazyk, výstupní formát a volitelné předzpracování. Nastavením jednou a opakovaným použitím se vyhnete režii spouštění nové instance pro každý soubor.

## Krok 2: Extrahování textu a uložení jako prostý text

Pokud potřebujete jen surové znaky, přepněte engine na `OutputFormat.Text`. Tím řeknete Aspose OCR, aby přeskočil generování PDF a vrátil vám řetězec.

```csharp
        // Tell the engine to return plain text
        ocrEngine.OutputFormat = OutputFormat.Text;

        // Path to your source image (PNG, JPEG, BMP, etc.)
        string inputImagePath = @"YOUR_DIRECTORY/input.png";

        // Perform recognition – the result contains the extracted string
        OcrResult plainTextResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Write the text to a .txt file
        string textOutputPath = @"YOUR_DIRECTORY/output.txt";
        File.WriteAllText(textOutputPath, plainTextResult.Text);
```

**Tip:** `plainTextResult.Text` už odstraňuje zalomení řádků, která patří do OCR rozvržení. Pokud potřebujete zachovat původní rozestupy, podívejte se místo toho na `plainTextResult.TextBlocks`.

### Očekávaný výsledek

Otevřete `output.txt` a měli byste vidět něco jako:

```
Hello, world!
This is a sample scanned document.
```

To je část **output plain text** tutoriálu – rychlá, nenáročná a ideální pro další zpracování (např. indexování).

## Krok 3: Přepnutí do režimu prohledávatelného PDF

Nyní vytvoříme **prohledávatelné PDF**. Engine vloží původní bitmapu a pod ní umístí text vygenerovaný OCR, což umožní vyhledávat v dokumentu v libovolném PDF prohlížeči.

```csharp
        // Change the output format to searchable PDF
        ocrEngine.OutputFormat = OutputFormat.SearchablePdf;

        // Recognize the same image again – this time we get PDF bytes
        OcrResult pdfResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Save the PDF bytes to a file
        string pdfOutputPath = @"YOUR_DIRECTORY/output.pdf";
        File.WriteAllBytes(pdfOutputPath, pdfResult.RawData);
    }
}
```

**Proč znovu rozpoznáváme:** OCR engine kešuje poslední obrázek, ale výstupní formát určuje, jaká data vrátí. Přepnutím formátu vynutíme nový průchod, který zahrne skrytou textovou vrstvu.

### Jak PDF vypadá

Otevřete `output.pdf` v Adobe Readeru nebo jiném prohlížeči a zkuste vybrat text. Uvidíte, že můžete kopírovat, vyhledávat a zvýrazňovat obsah – i když vizuálně zůstává původní bitmapa. To je charakteristické pro **convert scanned image pdf**.

## Krok 4: Zpracování více souborů (volitelné)

V reálných projektech se zřídka pracuje s jediným obrázkem. Níže je rychlá smyčka, která zpracuje každý PNG ve složce a vytvoří odpovídající soubory `.txt` a `.pdf`.

```csharp
        string folder = @"YOUR_DIRECTORY";
        foreach (var file in Directory.GetFiles(folder, "*.png"))
        {
            // Plain‑text extraction
            ocrEngine.OutputFormat = OutputFormat.Text;
            var txtResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllText(Path.ChangeExtension(file, ".txt"), txtResult.Text);

            // Searchable PDF generation
            ocrEngine.OutputFormat = OutputFormat.SearchablePdf;
            var pdfResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllBytes(Path.ChangeExtension(file, ".pdf"), pdfResult.RawData);
        }
```

**Poznámka k okrajovým případům:** Velké obrázky mohou vyčerpat paměť. Pokud narazíte na `OutOfMemoryException`, zvažte zmenšení pomocí `Image.Resize` před rozpoznáním nebo zpracovávejte soubory po menších dávkách.

## Krok 5: Jemné ladění přesnosti OCR

Aspose OCR nabízí několik „knoflíčků“, které můžete nastavit:

| Nastavení | Co dělá | Kdy použít |
|-----------|----------|------------|
| `ocrEngine.PageSegmentationMode` | Řídí, jak engine rozděluje obrázek na textové bloky. | Uvícení více‑sloupcových rozvržení. |
| `ocrEngine.Deskew` | Automaticky otáčí mírně nakloněné stránky. | Skenované dokumenty, které nejsou dokonale zarovnané. |
| `ocrEngine.RemoveNoise` | Pokouší se vyčistit šmouhy a artefakty pozadí. | Nízkokvalitní skeny nebo faxované stránky. |

Příklad:

```csharp
ocrEngine.Deskew = true;
ocrEngine.RemoveNoise = true;
```

Povolení těchto možností může prodloužit dobu zpracování, ale zisk v kvalitě **extract text from image** je často stojí za to.

## Krok 6: Programové ověření výstupu

Někdy potřebujete ověřit, že PDF skutečně obsahuje prohledávatelný text (např. v automatizovaných testech). Nejjednodušší kontrola je ověřit, že pole bajtů PDF není prázdné a že délka `RawData` převyšuje velikost obrázku.

```csharp
if (pdfResult.RawData.Length > Image.Load(inputImagePath).Data.Length)
{
    Console.WriteLine("Searchable PDF generated successfully!");
}
else
{
    Console.WriteLine("Warning: PDF may not contain hidden text.");
}
```

Pro hlubší validaci můžete použít PDF knihovnu (např. iTextSharp) k extrakci textového proudu a porovnání s `plainTextResult.Text`.

## Běžné úskalí a jak se jim vyhnout

- **Chybějící licence** – Bez platné licence Aspose knihovna běží v evaluačním režimu a do PDF přidává vodoznak. Zaregistrujte licenci co nejdříve (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`).  
- **Nesprávná cesta** – Hard‑codování absolutních cest funguje na vašem počítači, ale selže jinde. Používejte `Path.Combine` s `AppDomain.CurrentDomain.BaseDirectory` pro přenositelnost.  
- **Nesupported Image Formats** – GIFy a TIFFy s více snímky vyžadují speciální zpracování (`Image.LoadMultiPage`). Převeďte je na PNG/JPEG, pokud potřebujete jen první stránku.  
- **Úzká místa výkonu** – Vytváření nového `OcrEngine` uvnitř smyčky je nákladné. Uchovávejte jednu instanci a měňte jen `OutputFormat`, jak je ukázáno.

## Shrnutí

Probrali jsme celý workflow pro **vytvoření prohledávatelného PDF** ze skenovaného obrázku pomocí Aspose OCR:

1. Nainstalujte NuGet balíček a vytvořte `OcrEngine`.  
2. Nastavte `OutputFormat.Text` pro **output plain text** a zapište jej do souboru `.txt`.  
3. Přepněte na `OutputFormat.SearchablePdf` pro **convert image to PDF** s neviditelnou textovou vrstvou.  
4. Uložte bajty PDF a případně smyčkou projděte adresář pro dávkové zpracování.  
5. Jemně dolaďte přesnost pomocí deskew, odstraňování šumu a nastavení segmentace stránek.  

Vše to lze zabalit do kompaktního, samostatného programu, který můžete zkopírovat a vložit do Visual Studia.

## Co vyzkoušet dál?

- **Dávkové zpracování** s UI front‑endem (WinForms nebo WPF), aby uživatelé mohli soubory přetahovat a upouštět.  
- **Detekce jazyka** – Aspose OCR dokáže automaticky detekovat jazyk; vyzkoušejte `ocrEngine.Language = Language.AutoDetect`.  
- **Post‑processing** – Předejte extrahovaný text do vyhledávacího indexu (ElasticSearch, Azure Cognitive Search) pro okamžité vyhledávání dokumentů.  
- **Alternativní výstupy** – Použijte `OutputFormat.Hocr` pro HTML‑založené OCR výsledky, užitečné pro webové náhledy.

Klidně experimentujte s různými rozlišeními obrázků, barevnými režimy a nastavením OCR. Čím více si s tím pohráváte, tím lépe pochopíte kompromisy mezi rychlostí a přesností.

---

**Šťastné kódování!** Pokud narazíte na nějaké nejasnosti, zanechte komentář níže nebo se podívejte do dokumentace Aspose OCR pro podrobnější informace. Váš další projekt – ať už jde o fakturaci, archivaci nebo tvorbu prohledávatelné znalostní báze – bude od teď o mnoho jednodušší.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}