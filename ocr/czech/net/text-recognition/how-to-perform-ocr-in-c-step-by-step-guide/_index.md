---
category: general
date: 2026-02-14
description: Jak provést OCR v C# pomocí Aspose.OCR – naučte se extrahovat text z
  obrázku, načíst obrázek ze souboru a rychle spustit OCR na obrázku.
draft: false
keywords:
- how to perform OCR
- extract text from image
- load image from file
- recognize text from jpg
- run OCR on image
language: cs
og_description: Jak provádět OCR v C# s Aspose.OCR. Tento průvodce vám ukáže, jak
  extrahovat text z obrázku, načíst obrázek ze souboru a efektivně spustit OCR na
  obrázku.
og_title: Jak provést OCR v C# – Kompletní programovací tutoriál
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Jak provést OCR v C# – krok za krokem průvodce
url: /cs/net/text-recognition/how-to-perform-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provádět OCR v C# – Kompletní programovací tutoriál

Už jste se někdy zamysleli **jak provádět OCR** na obrázku, který jste právě pořízili telefonem? Možná potřebujete získat text pouličního značení z JPEG pro navigační aplikaci, nebo máte šarži naskenovaných smluv a chtěli byste je převést na prohledávatelný text. Stručně řečeno, chcete *extrahovat text z obrázku* bez odesílání čehokoliv do cloudu.

Dobrou zprávou je, že to vše můžete provádět lokálně s Aspose.OCR pro .NET. V tomto tutoriálu vás provedeme načtením obrázku ze souboru, rozpoznáním textu z JPG a nakonec **spuštěním OCR na obrázku** zcela offline. Na konci budete mít připravený úryvek kódu, který vytiskne rozpoznaný arabský text do konzole.

> **Co získáte:** samostatný spustitelný program v C#, vysvětlení, proč je každý řádek důležitý, a tipy na řešení běžných okrajových případů, jako chybějící zdroje nebo nepodporované jazyky.

## Požadavky

| Požadavek | Důvod |
|-------------|--------|
| .NET 6.0 nebo novější (nebo .NET Framework 4.7+) | Aspose.OCR cílí na .NET Standard 2.0, takže funguje jakékoli moderní runtime. |
| Visual Studio 2022 (nebo VS Code s rozšířením C#) | IDE usnadňuje správu NuGet balíčků a spuštění konzolové aplikace. |
| NuGet balíček Aspose.OCR (`Aspose.OCR`) | Jedná se o knihovnu, která skutečně provádí OCR. |
| Složka obsahující offline OCR zdroje (ke stažení z Aspose) | Offline zdroje zabraňují jakýmkoli HTTP voláním během rozpoznávání. |
| Obrázkový soubor (např. `arabic_sign.jpg`) | Použijeme JPEG, který obsahuje arabský text, ale funguje jakýkoli jazyk. |

Pokud vám něco chybí, pořiďte si to hned—nemá smysl začínat tutoriál a pak narazit na chybějící závislost v polovině.

## Krok 1: Nainstalujte Aspose.OCR a připravte zdroje

Nejprve přidejte balíček Aspose.OCR do svého projektu:

```bash
dotnet add package Aspose.OCR
```

Po instalaci balíčku stáhněte **offline OCR balíček zdrojů** z webu Aspose. Rozbalte jej do složky ve svém počítači, například:

```
C:\OCRResources\
```

> **Proč je to důležité:** Načtení zdrojů jednou při spuštění eliminuje síťovou latenci a udržuje vaše řešení v souladu s GDPR, protože nic neopouští stroj.

## Krok 2: Vytvořte OCR Engine a nasměrujte jej do složky se zdroji

Nyní vytvoříme instanci třídy `Engine` a řekneme jí, kde se zdroje nacházejí. Toto je jádro **jak provádět OCR** lokálně.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Step 2: Initialize the OCR engine with the offline resource folder
Engine ocrEngine = new Engine
{
    // Replace with the path you used in the previous step
    ResourceFolder = @"C:\OCRResources"
};

// Load the resources into memory – this prevents any hidden HTTP calls
ocrEngine.LoadResources();
```

**Tip:** Zabalte volání `LoadResources` do try‑catch bloku, pokud očekáváte, že cesta ke složce může být špatná. Výjimka vám řekne přesně, který soubor chybí.

## Krok 3: Načtěte obrázek ze souboru

Dále potřebujeme **načíst obrázek ze souboru**, aby jej engine mohl analyzovat. Aspose.OCR pracuje s vlastním obalem `ImageStream`.

```csharp
// Step 3: Load the JPEG you want to recognize
ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");
```

Pokud je váš obrázek jinde, stačí změnit cestu. Třída `ImageStream` abstrahuje podkladové zpracování bitmap, takže se nemusíte starat o kompatibilitu s GDI+.

## Krok 4: Rozpoznání textu z JPG pomocí nastavení jazyka

Nyní přichází jádro **jak provádět OCR** — skutečné rozpoznání znaků. Požádáme o arabské rozpoznání, ale můžete zaměnit `Language.Arabic` za jakýkoli jiný podporovaný jazyk.

```csharp
// Step 4: Run OCR specifying the desired language (Arabic in this example)
OcrResult ocrResult = ocrEngine.Recognize(
    image,
    new OcrOptions { Language = Language.Arabic }
);
```

**Proč specifikovat jazyk?** OCR engine používá jazykově specifické slovníky a modely znaků. Poskytnutí správného jazyka dramaticky zvyšuje přesnost, zejména u skriptů s komplexními tvary jako arabština.

## Krok 5: Zobrazte extrahovaný text

Nakonec **extrahujme text z obrázku** a vytiskněme jej. Toto je nejjednodušší způsob, jak ověřit, že OCR uspělo.

```csharp
// Step 5: Output the recognized text to the console
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrResult.Text);
```

Když spustíte program, měli byste v konzoli vidět arabskou frázi, která byla na značce. Pokud výstup vypadá poškozeně, zkontrolujte, že byl vybrán správný jazyk a že složka se zdroji obsahuje arabské datové soubory.

## Kompletní funkční příklad

Níže je kompletní, připravený ke kompilaci program, který spojuje všechny kroky. Zkopírujte jej do nového konzolového projektu (`dotnet new console`) a stiskněte **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Configure the OCR engine with offline resources
            // -------------------------------------------------
            Engine ocrEngine = new Engine
            {
                ResourceFolder = @"C:\OCRResources" // <-- change to your folder
            };
            ocrEngine.LoadResources(); // Loads language packs, fonts, etc.

            // -------------------------------------------------
            // Step 2: Load the image you want to process
            // -------------------------------------------------
            ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");

            // -------------------------------------------------
            // Step 3: Recognize text – specify language to improve accuracy
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(
                image,
                new OcrOptions { Language = Language.Arabic } // Change as needed
            );

            // -------------------------------------------------
            // Step 4: Output the result
            // -------------------------------------------------
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Očekávaný výstup (příklad):**

```
=== OCR Result ===
مطار القاهره الدولي
```

Pokud nahradíte obrázek anglickou značkou a nastavíte `Language.English`, stejný kód vypíše anglický text. To ukazuje, jak flexibilní může být **spuštění OCR na obrázku**.

## Extrahování textu z obrázku – Řešení běžných scénářů

### 1. Více stránek nebo více‑rámcových obrázků

Některé formáty obrázků (např. TIFF) mohou obsahovat několik stránek. Pro **extrahování textu z obrázku** v takových případech projděte každý rámec ve smyčce:

```csharp
for (int i = 0; i < image.FramesCount; i++)
{
    image.CurrentFrame = i;
    OcrResult pageResult = ocrEngine.Recognize(image, new OcrOptions { Language = Language.English });
    Console.WriteLine($"Page {i + 1}: {pageResult.Text}");
}
```

### 2. Nízké rozlišení obrázků

Přesnost OCR dramaticky klesá pod 70 dpi. Pokud narazíte na rozmazané výsledky, zvažte nejprve zvětšení obrázku:

```csharp
using System.Drawing;
using System.Drawing.Drawing2D;

// Load as Bitmap, resize, then wrap back into ImageStream
Bitmap bmp = new Bitmap(@"C:\OCRResources\lowres.jpg");
Bitmap highRes = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
ImageStream highResStream = ImageStream.FromBitmap(highRes);
```

### 3. Chybějící jazykový balíček

Pokud dostanete výjimku jako *„Language data not found“*, zkontrolujte, že odpovídající soubory `.dat` existují ve vaší `ResourceFolder`. Aspose poskytuje samostatný zip pro každý jazyk.

## Spuštění OCR na obrázku – Tipy pro výkon

- **Ukládejte Engine do cache:** Vytvoření nového `Engine` pro každý obrázek přidává režii. Uchovávejte jednu instanci pro dávkové zpracování.
- **Paralelizujte bezpečně:** `Engine` je po `LoadResources` vlákny‑bezpečný pro operace jen pro čtení. Můžete spustit více úkolů, z nichž každý zavolá `Recognize` na jiném obrázku.
- **Uvolněte po dokončení:** I když `Engine` implementuje `IDisposable`, .NET GC ho nakonec uvolní. Explicitní volání `ocrEngine.Dispose()` v bloku `using` je dobrý zvyk.

```csharp
using (Engine ocrEngine = new Engine { ResourceFolder = @"C:\OCRResources" })
{
    ocrEngine.LoadResources();
    // run recognitions here
}
```

## Rozpoznání textu z JPG – Okrajové případy, na které si dát pozor

| Situace | Co zkontrolovat | Oprava |
|-----------|----------------|-----|
| **Poškozený JPEG** | `ImageStream.FromFile` vyhodí `FileNotFoundException` nebo `ArgumentException`. | Ověřte integritu souboru, případně obrázek znovu uložte v grafickém editoru. |
| **Nepodporovaný jazyk** | `Language` enum neobsahuje požadovaný jazyk. | Aktualizujte Aspose.OCR na nejnovější verzi; nové jazyky jsou přidávány pravidelně. |
| **Obrázky s kombinovaným skriptem** (např. angličtina + arabština) | Jedna volba jazyka může přehlédnout sekundární skript. | Spusťte OCR dvakrát s různými jazykovými možnostmi a výsledky spojte. |

## Shrnutí – Nyní víte, jak provádět OCR v C#

V tomto průvodci jsme pokryli **jak provádět OCR** pomocí Aspose.OCR, od instalace NuGet balíčku po vytištění rozpoznaného textu. Naučili jste se **načíst obrázek ze souboru**, **extrahovat text z obrázku**, **rozpoznat text z jpg** a bezpečně **spustit OCR na obrázku** v produkčně připraveném způsobu.

### Co dál?

- **Experimentujte s jinými formáty souborů** jako PNG nebo BMP — stačí změnit příponu souboru.
- **Integrujte s databází** pro uložení OCR výsledků do prohledávatelných archivů.
- **Kombinujte s počítačovým viděním** (např. detekce oblastí textu před OCR) pro zvýšení rychlosti.

Neváhejte upravit nastavení jazyka, dávkově zpracovávat složky nebo připojit výstup k webovému API. OCR je stavební blok; skutečná síla přichází, když jej zapojíte do větších pracovních toků.

Šťastné programování a ať jsou vaše obrázky vždy krystalicky čisté!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}