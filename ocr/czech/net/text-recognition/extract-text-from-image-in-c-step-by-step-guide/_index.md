---
category: general
date: 2026-05-06
description: Extrahujte text z obrázku pomocí Aspose OCR v C#. Naučte se převést JPG
  na text, nastavit jazyk OCR a efektivně číst text z JPG.
draft: false
keywords:
- extract text from image
- convert jpg to text
- image to text c#
- read text from jpg
- set OCR language
language: cs
og_description: Extrahujte text z obrázku v C# pomocí Aspose OCR. Tento průvodce ukazuje,
  jak převést JPG na text, nastavit jazyk OCR a číst text z JPG.
og_title: Extrahování textu z obrázku v C# – Kompletní tutoriál
tags:
- OCR
- C#
- Aspose
title: Extrahovat text z obrázku v C# – krok za krokem
url: /cs/net/text-recognition/extract-text-from-image-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z obrázku v C# – Kompletní programový průvodce

Už jste někdy potřebovali **extrahovat text z obrázku**, ale nevěděli, kterou knihovnu zvolit? Nejste sami – vývojáři se často ptají: „Jak převést JPG na text, aniž bych posílal data do cloudu?“ Dobrou zprávou je, že Aspose OCR vám poskytuje plně offline řešení, které funguje přímo ve vaší .NET aplikaci.

V tomto tutoriálu projdeme vše, co potřebujete vědět: od instalace NuGet balíčku Aspose OCR, přes **nastavení jazyka OCR** pro ruštinu, až po **čtení textu z JPG** souborů. Na konci budete mít znovupoužitelný úryvek, který můžete vložit do libovolného C# projektu a okamžitě začít extrahovat text z obrázků.

> **Co si odnesete**  
> • Přehledný, spustitelný příklad, který **extrahuje text z obrázku**.  
> • Znalost, jak **převést JPG na text** pomocí motoru Aspose OCR.  
> • Tipy na konfiguraci **nastavení jazyka OCR** pro vícejazyčné scénáře.  
> • Řešení okrajových případů pro nečitelné obrázky a chybějící jazykové balíčky.

## Požadavky

Než se pustíme do práce, ujistěte se, že máte:

| Požadavek | Proč je důležitý |
|-------------|----------------|
| .NET 6.0 nebo novější (jakýkoli aktuální .NET runtime) | Aspose OCR cílí na .NET Standard 2.0+, takže novější runtime poskytuje nejlepší výkon. |
| Visual Studio 2022 (nebo VS Code s C# rozšířeními) | Přátelské IDE vám pomůže rychle ladit OCR tok. |
| Přístup k internetu **jednou** pro stažení NuGet balíčku Aspose OCR | Po první instalaci můžete povolit **offline zdroje**, aby se již žádná další stahování neprováděla. |
| Vzorek JPG obrázku (`input.jpg`) obsahujícího ruský text (nebo jakýkoli jazyk, který chcete použít) | Tutoriál používá ruský příklad, ale můžete zaměnit libovolný jazykový balíček, který máte nainstalovaný. |

Pokud některý z těchto bodů není vám známý, nepanikařte. Instalace NuGet balíčku je tak jednoduchá jako zadání jediného příkazu a zbytek kroků funguje stejně pro každý formát obrázku podporovaný Aspose.

## Přehled řešení

Z vysoké úrovně proces vypadá takto:

1. **Vytvořit** `OcrEngine` s offline zdroji, aby knihovna nezkoušela během běhu stahovat jazyková data.  
2. **Nastavit** požadovaný jazyk (např. ruštinu) pomocí výčtu `OcrLanguage`.  
3. **Zavolat** `RecognizeImage` na lokálním JPG souboru.  
4. **Vytisknout** extrahovaný řetězec do konzole nebo jej předat do vlastního workflow.

Níže je rychlý diagram, který ilustruje tok dat:

![Extract text from image using Aspose OCR in C#](https://example.com/placeholder-image.png){.align-center alt="extrahovat text z obrázku pomocí Aspose OCR v C#"}

*Diagram je pouze ilustrativní; kód provádí těžkou práci.*

## Extrahování textu z obrázku – základní pojmy

Než začneme psát kód, rozbalme si pár pojmů, které často vývojáře zaskočí:

- **OfflineResources** – Když je `true`, Aspose OCR hledá jazykové balíčky, které jste předem stáhli. Tím se eliminuje krok „auto‑download“, který může zpomalit start v produkčním prostředí.  
- **OcrLanguage** – Výčet obsahuje desítky identifikátorů jazyků (`English`, `Russian`, `Japanese`, …). Výběr správného výrazně zvyšuje přesnost, protože engine může použít jazykově specifické heuristiky.  
- **Kvalita obrázku** – OCR funguje nejlépe na vysoce kontrastních, šuměných obrázcích. Pokud dostáváte nečitelné výsledky, zvažte předzpracování (např. binarizaci) před předáním obrázku do engine.

Pochopení těchto bodů vám pomůže rozhodnout, kdy **nastavit jazyk OCR** ručně a kdy spoléhat na automatické rozpoznání, a proč **převod JPG na text** není jen jednorázová jednorázová operace.

## Krok 1: Instalace NuGet balíčku Aspose OCR

Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package Aspose.OCR
```

*Tip:* Po první instalaci přidejte `-v latest`, aby se vždy získala nejnovější stabilní verze. Velikost balíčku je přibližně 15 MB, což je rozumné pro většinu desktopových nebo serverových nasazení.

## Krok 2: Převod JPG na text – inicializace engine

Nyní, když je knihovna na vašem počítači, vytvoříme `OcrEngine`, který pracuje offline.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 2.1: Create an OCR engine with offline resources.
        // This prevents the SDK from trying to download language data at runtime.
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            OfflineResources = true   // <-- crucial for production stability
        });

        // Step 2.2: Choose the language pack you need.
        // Here we use Russian; replace with OcrLanguage.English for English text.
        ocrEngine.Language = OcrLanguage.Russian;

        // Step 2.3: Perform OCR on a local JPG file.
        // The file path can be absolute or relative to the executable.
        var result = ocrEngine.RecognizeImage("YOUR_DIRECTORY/input.jpg");

        // Step 2.4: Output the extracted text.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(result.Text);
    }
}
```

### Proč je to důležité

- **Offline režim** zaručuje deterministické časy startu – žádné nečekané síťové volání při nasazení na uzavřený server.  
- **Nastavení jazyka** (`OcrLanguage.Russian`) říká engine použít ruskou znakovou sadu, což zvyšuje přesnost rozpoznání z ~70 % na >95 % u čistých obrázků.  
- Metoda `RecognizeImage` přijímá jakýkoli formát obrázku, který Aspose podporuje (`.jpg`, `.png`, `.tiff`, …). Proto můžeme **číst text z JPG** bez dalších konverzních kroků.

## Krok 3: Nastavení jazyka OCR – práce s více jazyky

Někdy potřebujete zpracovat dokumenty, které obsahují smíšené jazyky (např. ruštinu a angličtinu). Aspose OCR vám umožní zadat *náhradní* pole jazyků:

```csharp
// Example: Russian primary, English secondary
ocrEngine.Language = OcrLanguage.Russian;
ocrEngine.AdditionalLanguages = new[] { OcrLanguage.English };
```

Když primární jazyk nedokáže rozpoznat znak, engine automaticky zkontroluje další seznam. Tato technika je obzvláště užitečná pro faktury, kde se mísí cyrilické názvy firem s anglickými kódy produktů.

> **Poznámka:** Jazykové balíčky musí být přítomny ve složce `Resources` vašeho projektu. Pokud obdržíte `FileNotFoundException`, stáhněte chybějící balíček z portálu Aspose a umístěte jej vedle spustitelného souboru.

## Krok 4: Čtení textu z JPG – běžné úskalí a opravy

I s správným jazykovým balíčkem můžete narazit na:

| Problém | Typický symptom | Rychlá oprava |
|-------|-----------------|-----------|
| Nízký kontrast | Zkreslený nebo prázdný výstup | Použijte jednoduchý filtr pro zvýšení kontrastu pomocí `System.Drawing` před OCR. |
| Otočený obrázek | Text je vodorovně | Nastavte `ocrEngine.ImageRotation = OcrRotation.Rotate90;` (nebo 180/270) před voláním `RecognizeImage`. |
| Velký soubor | Pomalu rozpoznávání, vysoká spotřeba paměti | Zmenšete obrázek na maximálně 2000 px na delší straně; kvalita OCR zůstane vysoká. |

Zde je kompaktní pomocná metoda, která předzpracuje a vylepší obrázek před předáním engine:

```csharp
using System.Drawing;
using System.Drawing.Imaging;

static string PreprocessAndRead(string jpgPath)
{
    // Load the original image
    using var original = new Bitmap(jpgPath);

    // Resize while preserving aspect ratio (max 2000px)
    int maxDim = 2000;
    int newWidth, newHeight;
    if (original.Width > original.Height)
    {
        newWidth = maxDim;
        newHeight = original.Height * maxDim / original.Width;
    }
    else
    {
        newHeight = maxDim;
        newWidth = original.Width * maxDim / original.Height;
    }

    using var resized = new Bitmap(original, new Size(newWidth, newHeight));

    // Optional: increase contrast (simple linear stretch)
    var contrast = new ImageAttributes();
    float[][] matrix = {
        new float[] {1.2f, 0, 0, 0, 0},
        new float[] {0, 1.2f, 0, 0, 0},
        new float[] {0, 0, 1.2f, 0, 0},
        new float[] {0, 0, 0, 1, 0},
        new float[] {0, 0, 0, 0, 1}
    };
    contrast.SetColorMatrix(new ColorMatrix(matrix));

    using var graphics = Graphics.FromImage(resized);
    graphics.DrawImage(resized, new Rectangle(0, 0, newWidth, newHeight), 0, 0, newWidth, newHeight, GraphicsUnit.Pixel, contrast);

    // Save to a temporary file (Aspose OCR works with file paths)
    string tempPath = Path.GetTempFileName() + ".jpg";
    resized.Save(tempPath, ImageFormat.Jpeg);

    // Run OCR
    var engine = new OcrEngine(new OcrEngineSettings { OfflineResources = true });
    engine.Language = OcrLanguage.Russian;
    var res = engine.RecognizeImage(tempPath);
    File.Delete(tempPath); // clean up
    return res.Text;
}
```

Nyní můžete zavolat `Console.WriteLine(PreprocessAndRead("YOUR_DIRECTORY/input.jpg"));` a získat čistší výsledek.

## Kompletní funkční příklad – všechny kroky v jednom souboru

Níže je *úplný* program, který můžete zkopírovat do `Program.cs`. Obsahuje poznámky k instalaci, konfiguraci jazyka, předzpracování a ošetření chyb.

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        string imagePath = "YOUR_DIRECTORY/input.jpg";

        try
        {

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}