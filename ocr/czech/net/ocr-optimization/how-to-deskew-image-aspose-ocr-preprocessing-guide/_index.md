---
category: general
date: 2026-04-29
description: jak vyrovnat sklon obrazu a zvýšit přesnost OCR pomocí Aspose OCR – naučte
  se odstraňovat šum, zvyšovat kontrast obrazu a extrahovat text z obrázků.
draft: false
keywords:
- how to deskew image
- remove noise from image
- boost image contrast
- extract text from image
- improve ocr accuracy
language: cs
og_description: jak vyrovnat obrázek a zlepšit přesnost OCR. Tento tutoriál ukazuje,
  jak odstranit šum z obrázku, zvýšit kontrast obrázku a extrahovat text z obrázku
  pomocí Aspose OCR.
og_title: Jak vyrovnat zkosení obrázku – Kompletní průvodce Aspose OCR
tags:
- Aspose OCR
- C#
- Image preprocessing
title: Jak vyrovnat obrázek – Průvodce předzpracováním OCR Aspose
url: /cs/net/ocr-optimization/how-to-deskew-image-aspose-ocr-preprocessing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak narovnat obrázek – Kompletní průvodce Aspose OCR

Už jste se někdy zamýšleli, **jak narovnat obrázek** před tím, než jej předáte OCR enginu? Nejste v tom sami. Šikmý sken nebo foto pořízené pod úhlem může narušit rozpoznávání textu a zanechat vás s nečitelným výstupem.  

V tomto tutoriálu projdeme kompletním řešením od začátku do konce, které nejen **jak narovnat obrázek**, ale také **odstranit šum z obrázku**, **zvýšit kontrast obrázku** a nakonec **extrahovat text z obrázku** pomocí Aspose OCR. Na konci uvidíte, jak **zlepšit přesnost OCR** bez zbytečného prohledávání dokumentace.

> **Co získáte:** připravenou C# konzolovou aplikaci, jasné vysvětlení každého kroku předzpracování a několik praktických tipů, které můžete zkopírovat a vložit do svých projektů.

## Požadavky

- .NET 6.0 nebo novější (kód funguje také s .NET Core a .NET Framework)  
- NuGet balíček Aspose.OCR (`Install-Package Aspose.OCR`)  
- Vzorek obrázku, který je šikmý, šumivý nebo s nízkým kontrastem (např. `skewed_noisy.jpg`)  
- Visual Studio, VS Code nebo jakýkoli C# editor, který preferujete  

Žádné další nativní knihovny nejsou potřeba – Aspose vše zpracovává v rámci procesu.

---

## Jak narovnat obrázek pomocí Aspose OCR

Prvním, co potřebujeme, je filtr pro narovnání, který koriguje úhel rotace. Aspose OCR obsahuje `FilterDeskew`, který analyzuje textové základny a podle toho otáčí bitmapu.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that will later recognize text.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Build an image‑processing pipeline.
        //    The order matters: deskew → denoise → contrast boost.
        ImageProcessingPipeline processingPipeline = new ImageProcessingPipeline();
        processingPipeline.Add(new FilterDeskew());          // ✅ how to deskew image
        processingPipeline.Add(new FilterDenoise());         // ✅ remove noise from image
        processingPipeline.Add(new FilterContrastBoost());   // ✅ boost image contrast

        // 3️⃣ Load your source picture.
        var sourceImage = OcrEngine.LoadImage(@"YOUR_DIRECTORY/skewed_noisy.jpg");

        // 4️⃣ Apply the pipeline – the image is now straight, cleaner, and sharper.
        var processedImage = processingPipeline.Apply(sourceImage);

        // 5️⃣ Run OCR on the cleaned‑up bitmap.
        var ocrResult = ocrEngine.Recognize(processedImage);

        // 6️⃣ Print the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Proč začínáme narovnáním:**  
Pokud textové řádky nejsou vodorovné, OCR engine se pokusí interpretovat šikmé znaky jako jiné glyfy, což dramaticky snižuje **zlepšit přesnost OCR**. Narovnání zarovná základny, poskytne rozpoznávači čisté plátno.

> *Tip:* Pokud znáte úhel rotace předem (např. všechny skeny jsou otočeny o 90°), můžete filtr přeskočit a otočit ručně – je to malé zrychlení výkonu.

---

## Odstranit šum z obrázku – Vyčistit sken

Šum se projevuje jako náhodné černé nebo bílé tečky (klasický vzor „sůl‑a‑pepř“) a může zmást segmentaci znaků. `FilterDenoise` použije mediánový filtr, který tyto šumy vyhladí a zároveň zachová hrany.

```csharp
// Inside the pipeline we already added FilterDenoise.
// If you need a custom strength, you can instantiate it like:
var denoise = new FilterDenoise { Strength = 2 }; // 1‑3 are typical values
processingPipeline.Add(denoise);
```

**Kdy upravit sílu:**  
- **Strength = 1** – Lehký zrnitost, rychlé zpracování.  
- **Strength = 3** – Velmi šumivé skeny (např. faxové dokumenty).  

Přílišné zvýšení síly může rozmazat tenké tahy, což může *poškodit* **zlepšit přesnost OCR**. Otestujte několik hodnot na reprezentativním vzorku.

---

## Zvýšit kontrast obrázku – Zvýraznit slabé znaky

Obrázky s nízkým kontrastem (např. vybledlé účtenky) často způsobují, že OCR engine přehlédne lehké glyfy. `FilterContrastBoost` roztáhne histogram tak, že tmavé pixely se stanou tmavšími a světlé pixely světlejšími.

```csharp
var contrast = new FilterContrastBoost { ContrastLevel = 1.5f }; // 1.0 = no change
processingPipeline.Add(contrast);
```

**Proč je kontrast důležitý:**  
Vyšší kontrast zlepšuje poměr signál‑k‑šumu, což usnadňuje neuronovému rozpoznávači Aspose rozlišovat „I“ od „l“. Přesto může nadměrné zvýšení kontrastu saturaci obrázku, proměnit hladké přechody v tvrdé hrany, které vypadají jako artefakty. Cílem je rovnováha; 1,5‑2,0 je dobrý výchozí bod.

---

## Extrahovat text z obrázku – Poslední krok OCR

Nyní, když je obrázek rovný, čistý a živý, OCR engine může vykonat svou práci. Metoda `Recognize` vrací objekt `OcrResult`, který obsahuje surový text, skóre důvěry a dokonce i ohraničující rámečky, pokud je potřebujete.

```csharp
var ocrResult = ocrEngine.Recognize(processedImage);
Console.WriteLine(ocrResult.Text);
```

**Ukázkový výstup** (předpokládejme, že zdrojový obrázek obsahuje „Invoice #12345“):

```
=== OCR Output ===
Invoice #12345
Date: 04/28/2026
Total: $1,234.56
```

Pokud vidíte chybějící znaky, zkontrolujte znovu pipeline předzpracování – možná obrázek stále potřebuje silnější odšumění nebo jinou úroveň kontrastu.  

> *Často kladená otázka:* „Co když potřebuji rozpoznat jazyk jiný než angličtinu?“  
> Stačí nastavit `ocrEngine.Language = Language.English;` na jiný podporovaný jazyk (např. `Language.French`). Kroky předzpracování zůstávají stejné.

---

## Zlepšit přesnost OCR – Další úpravy

I když máte dokonalou pipeline, několik dalších nastavení může posunout **zlepšit přesnost OCR** dál:

| Tip | Kdy použít | Jak |
|-----|--------------|-----|
| **Binary Thresholding** | Velmi tmavé nebo velmi světlé skeny | `processingPipeline.Add(new FilterBinarize());` |
| **Resize Image** | Malé písmo (<10 pt) | `processedImage = OcrEngine.Resize(processedImage, 2.0);` |
| **Specify Character Set** | Známá abeceda (pouze číslice, atd.) | `ocrEngine.Characters = "0123456789";` |
| **Multi‑page PDFs** | Dávkové zpracování | Loop over each page and reuse the same pipeline. |

Pamatujte: každý další filtr přidává čas zpracování, takže povolujte jen to, co skutečně potřebujete.

---

## Kompletní funkční příklad (připravený ke kopírování a vložení)

Níže je celý program, připravený ke kompilaci. Nahraďte `YOUR_DIRECTORY` složkou, která obsahuje `skewed_noisy.jpg`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Build preprocessing pipeline
        ImageProcessingPipeline pipeline = new ImageProcessingPipeline();
        pipeline.Add(new FilterDeskew());                     // how to deskew image
        pipeline.Add(new FilterDenoise { Strength = 2 });    // remove noise from image
        pipeline.Add(new FilterContrastBoost { ContrastLevel = 1.8f }); // boost image contrast

        // Load source image
        var sourcePath = @"YOUR_DIRECTORY/skewed_noisy.jpg";
        var sourceImage = OcrEngine.LoadImage(sourcePath);

        // Apply pipeline
        var cleanImage = pipeline.Apply(sourceImage);

        // Perform OCR
        var result = ocrEngine.Recognize(cleanImage);

        // Output
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(result.Text);
    }
}
```

**Očekávaný výsledek:** Čistý, narovnaný text vytištěný do konzole, s mnohem méně chybami rozpoznání než při předání surového souboru přímo do `ocrEngine.Recognize`.

---

## Závěr

Probrali jsme **jak narovnat obrázek**, jak **odstranit šum z obrázku**, jak **zvýšit kontrast obrázku** a nakonec jak **extrahovat text z obrázku** pomocí Aspose OCR. Řetězením těchto filtrů uvidíte výrazné zlepšení **zlepšit přesnost OCR**, zejména u skenů nízké kvality.

Jste připraveni na další výzvu? Zkuste předat multi‑page PDF do stejné pipeline, nebo experimentujte s vlastními prahy pro binarizaci. Stejné principy platí – narovnejte, vyčistěte, zesvětlete, pak rozpoznávejte.

Máte otázky nebo podivný okrajový případ? Zanechte komentář a pojďme to společně vyřešit. Šťastné kódování!  

![příklad jak narovnat obrázek](deskew-example.png "příklad jak narovnat obrázek")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}