---
category: general
date: 2026-02-20
description: c# OCR tutoriál, který vám ukáže, jak extrahovat text z obrázku, rozpoznat
  text z PNG a převést obrázek na text pomocí několika řádků kódu.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- recognize text from png
- convert image to text
- how to extract text
language: cs
og_description: c# OCR tutoriál, který vás provede extrakcí textu z obrazových souborů,
  rozpoznáváním textu z PNG a převodem obrázků na text pomocí Aspose.OCR.
og_title: c# OCR tutoriál – Rychlý průvodce extrakcí textu z obrázků
tags:
- OCR
- C#
- Aspose
title: c# OCR tutoriál – Extrahování textu z obrázků pomocí Aspose.OCR
url: /cs/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutoriál – Extrahování textu z obrázků pomocí Aspose.OCR

Už jste někdy potřebovali **c# OCR tutoriál**, který skutečně funguje na reálném PNG souboru? Nejste v tom sami. V mnoha projektech—například skenování faktur, archivace účtenek nebo jednoduché parsování snímků obrazovky—vývojáři narazí na problém, když se snaží **extrahovat text z obrázku** bez spolehlivé knihovny.  

Dobrou zprávou je, že Aspose.OCR dělá celý proces hračkou. V tomto průvodci projdeme kompletním, spustitelným příkladem, který ukazuje **jak extrahovat text** z PNG, vysvětluje *proč* je každý řádek důležitý, a dokonce se dotýká okrajových případů, jako jsou licence a předzpracování obrazu. Na konci budete schopni **rozpoznat text z PNG** souborů a **převést obrázek na text** pomocí několika C# příkazů.

## Co tento tutoriál pokrývá

- Nastavení Aspose.OCR enginu v .NET konzolové aplikaci.  
- Načtení PNG (nebo jakéhokoli podporovaného bitmapu) z disku.  
- Spuštění OCR a vytištění výsledku do konzole.  
- Volitelná licence, ošetření chyb a tipy na výkon.  

Žádné externí služby, žádná skrytá magie—pouze čistý C# kód, který můžete zkopírovat‑vložit a spustit. Pokud jste se někdy ptali **jak extrahovat text** ze skenovaného dokumentu, zůstaňte s námi; odpovíme na to a několik otázek „co když“ během cesty.

## Požadavky

- .NET 6.0 SDK nebo novější (kód také funguje na .NET Framework 4.7+).  
- Visual Studio 2022 (nebo jakýkoli editor, který máte rádi).  
- Bezplatný nebo placený NuGet balíček Aspose.OCR pro .NET.  
- Obrázkový soubor pojmenovaný `sample.png` umístěný ve složce, na kterou můžete odkazovat.  

To je vše—nejsou potřeba žádné další nástroje třetích stran.

## c# OCR tutoriál: Nastavení Aspose.OCR

Nejprve: potřebujete knihovnu Aspose.OCR. Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package Aspose.OCR
```

Tím se stáhne nejnovější stabilní verze a přidají se potřebné DLL reference. Pokud máte licenční soubor (`Aspose.OCR.lic`), mějte ho po ruce; jinak bude fungovat bezplatná verze, ale s vodoznaky ve výsledku OCR.

### Proč je licence důležitá

Bez licence engine běží v evaluačním režimu, který vkládá řádek „Powered by Aspose“ do výstupu pro některé jazyky. Pro produkční kód budete chtít zavolat `SetLicense` co nejdříve, jak je ukázáno v kódu níže. Jedná se o jednorázové volání, ale odstraní vodoznak a odemkne plnohodnotné zpracování.

## Extrahování textu z obrázku pomocí Aspose.OCR

Nyní se ponořme do skutečného OCR kódu. Níže je **kompletní, samostatný** program, který můžete okamžitě zkompilovat a spustit.

```csharp
using System;
using System.Drawing;          // Needed for Image class
using Aspose.OCR;               // Core OCR namespace
using Aspose.OCR.Models;       // For OCR settings (optional)

class LicenseCheck
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // Step 2 (Optional): Apply your Aspose.OCR license
        // -------------------------------------------------
        // Uncomment and set the correct path if you have a license file.
        // ocrEngine.SetLicense(@"C:\MyLicenses\Aspose.OCR.lic");

        // -------------------------------------------------
        // Step 3: Load the image you want to process
        // -------------------------------------------------
        // You can use any supported format (png, jpg, bmp, tiff, etc.)
        string imagePath = @"C:\Images\sample.png";
        Image inputImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // Step 4: Recognize text from the loaded image
        // -------------------------------------------------
        // The Recognize method returns a plain string.
        string recognizedText = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 5: Display the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

**Co se zde děje?**  

1. **Vytvoření enginu** – `OcrEngine` je hlavní vstupní bod; interně načítá jazyková data.  
2. **Načtení licence** – volitelné, ale doporučené; jednoduše ukážete na svůj `.lic` soubor.  
3. **Načtení obrázku** – `Image.FromFile` funguje pro jakýkoli bitmapový formát; používáme PNG, protože zachovává bezztrátovou kvalitu, což je klíčové pro přesnost OCR.  
4. **Rozpoznání** – `ocrEngine.Recognize` provádí veškerou těžkou práci a vrací řetězec obsahující detekované znaky.  
5. **Výstup** – výsledek zapíšeme do konzole, ale můžete jej snadno poslat do souboru, databáze nebo UI ovládacího prvku.

### Očekávaný výstup

Pokud `sample.png` obsahuje text „Hello World“, konzole zobrazí:

```
=== OCR Result ===
Hello World
```

Pokud je obrázek rozmazaný nebo obsahuje ne‑latinské znaky, výstup může obsahovat poškozené symboly. Zde přichází do hry předzpracování (úprava kontrastu, binarizace) — podrobněji v další sekci.

## Rozpoznávání textu z PNG souborů – Tipy a triky

PNG je populární formát, protože ukládá pixely bez kompresních artefaktů. Přesto ne všechny PNG jsou stejné. Zde je několik praktických tipů, které vám mohou přijít vhod:

- **Rozlišení má význam** – Cílem je alespoň 300 dpi. Nižší rozlišení může způsobit chybějící znaky.  
- **Barva vs. odstíny šedi** – Převedení barevného PNG na odstíny šedi před OCR může zlepšit rychlost bez ztráty přesnosti.  
- **Odstranění šumu** – Malé skvrny často engine zmást; jednoduchý mediánový filtr může pomoci.

Níže je rychlý úryvek, který ukazuje, jak předzpracovat obrázek před předáním do Aspose.OCR:

```csharp
using System.Drawing.Imaging;

// Convert to grayscale
Bitmap grayBitmap = new Bitmap(inputImage.Width, inputImage.Height);
using (Graphics g = Graphics.FromImage(grayBitmap))
{
    var colorMatrix = new ColorMatrix(
        new float[][]{
            new float[]{0.3f,0.3f,0.3f,0,0},
            new float[]{0.59f,0.59f,0.59f,0,0},
            new float[]{0.11f,0.11f,0.11f,0,0},
            new float[]{0,0,0,1,0},
            new float[]{0,0,0,0,1}});
    var attributes = new ImageAttributes();
    attributes.SetColorMatrix(colorMatrix);
    g.DrawImage(inputImage, new Rectangle(0,0,grayBitmap.Width,grayBitmap.Height),
                0,0,inputImage.Width,inputImage.Height, GraphicsUnit.Pixel, attributes);
}

// Optional: Apply a simple binary threshold
Bitmap binBitmap = new Bitmap(grayBitmap.Width, grayBitmap.Height);
for (int y = 0; y < grayBitmap.Height; y++)
{
    for (int x = 0; x < grayBitmap.Width; x++)
    {
        Color pixel = grayBitmap.GetPixel(x, y);
        int bw = pixel.R < 128 ? 0 : 255; // threshold at 128
        binBitmap.SetPixel(x, y, Color.FromArgb(bw, bw, bw));
    }
}

// Now run OCR on the cleaned bitmap
string cleanedText = ocrEngine.Recognize(binBitmap);
Console.WriteLine(cleanedText);
```

**Pro tip:** Pokud zpracováváte desítky obrázků, vytvořte jediný `OcrEngine` a znovu jej použijte. Vytváření nového enginu pro každý obrázek přidává zbytečnou zátěž.

## Převod obrázku na text – Pokročilé možnosti

Aspose.OCR není omezen na pouhé extrahování textu. Můžete ho požádat, aby vrátil **strukturovaná data** (např. ohraničující rámečky slov) nebo nastavil **jazykové nápovědy** pro zlepšení přesnosti u vícejazykových dokumentů.

```csharp
// Set language to English + Spanish (ISO codes)
ocrEngine.Language = Language.English | Language.Spanish;

// Request detailed OCR result
OcrResult result = ocrEngine.RecognizeImage(inputImage, OcrOptions.DetectTextBlocks);

// Iterate over detected words
foreach (var word in result.Words)
{
    Console.WriteLine($"{word.Text} (x:{word.Bounds.X}, y:{word.Bounds.Y})");
}
```

Objekt `OcrResult` poskytuje souřadnice každého slova, což je užitečné pro zvýraznění textu v UI nebo pro následné zpracování (např. redakci citlivých informací).

## Jak extrahovat text v reálných scénářích

Pojďme se podívat na několik otázek „co když“, které se často objevují v produkčních prostředích.

### Co když je obrázek stránkou PDF?

Aspose.OCR může číst PDF přímo, ale budete potřebovat knihovnu Aspose.PDF k rasterizaci každé stránky do obrázku. Pracovní postup je:

1. Načtěte PDF pomocí `Aspose.Pdf.Document`.  
2. Převeďte stránku na bitmapu (`PdfConverter`).  
3. Předávejte bitmapu do `OcrEngine.Recognize`.

### Co když výsledek OCR obsahuje nesmyslné znaky?

Typické příčiny jsou nízké rozlišení, nadměrný šum nebo nepodporovaná písma. Zkuste:

- Zvětšení obrázku (`Bitmap` změna velikosti).  
- Aplikaci ostření filtru.  
- Určení správného jazyka (jak je ukázáno výše).

### Co když potřebuji zpracovávat obrázky paralelně?

Protože `OcrEngine` není thread‑safe, vytvořte **samostatnou instanci pro každý vlákno** nebo použijte thread‑local pool. Příklad s `Parallel.ForEach`:

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine(); // each thread gets its own engine
    var img = Image.FromFile(path);
    string text = engine.Recognize(img);
    // Store or log 'text' as needed
});
```

## Kompletní funkční příklad

Sestavením všeho dohromady, zde je kompaktní verze, kterou můžete vložit do nového konzolového projektu:

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialize OCR engine (single instance for this demo)
        OcrEngine engine = new OcrEngine();

        // Uncomment if you have a license file
        // engine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // Path to the PNG you want to read
        string file = @"C:\Images\sample.png";

        // Load, optionally preprocess, then recognize
        using (Image img = Image.FromFile(file))
        {
            string text = engine.Recognize(img);
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(text);
        }
    }
}
```

Zkompilujte pomocí `dotnet run` a sledujte, jak konzole vytiskne extrahovaný text. Jednoduché, že? To je krása dobře‑des

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}