---
category: general
date: 2026-02-13
description: Naučte se, jak používat OCR v C# k extrakci textu z obrazových souborů,
  povolit zpracování na GPU a rychle převádět skeny na text.
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: cs
og_description: Jak používat OCR v C#? Tento průvodce vám ukáže, jak extrahovat text
  z obrázkových souborů, povolit zpracování na GPU a převést skeny na text.
og_title: Jak používat OCR v C# – Extrahovat text z obrázků pomocí GPU
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: Jak používat OCR v C# – Extrahovat text z obrázků pomocí GPU
url: /cs/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat OCR v C# – Extrahovat text z obrázků s GPU

Už jste se někdy zamysleli **jak používat OCR** k získání textu ze skenovaného dokumentu bez námahy? Nejste jediní – vývojáři se neustále ptají: „Jak mohu efektivně extrahovat text ze souborů s obrázky?“ Dobrou zprávou je, že s Aspose.OCR můžete přesně to udělat a můžete dokonce **povolit zpracování na GPU** pro znatelně vyšší rychlost na podporovaném hardwaru.

V tomto tutoriálu projdeme kompletním příkladem od začátku do konce, který vám ukáže **jak používat OCR**, jak **extrahovat text z obrázku**, jak **převést sken na text** a co dělat, pokud GPU není k dispozici. Na konci budete mít připravenou C# konzolovou aplikaci, která vytiskne rozpoznaný text a řekne vám, zda byl GPU skutečně použit.

## Co budete potřebovat

- .NET 6 SDK nebo novější (kód funguje také s .NET Core)  
- Visual Studio 2022 nebo jakýkoli editor, který preferujete  
- Balíček Aspose.OCR pro .NET (k dispozici přes NuGet)  
- Soubor s vysokým rozlišením (např. `highres_scan.tif`) pro testování  

Není potřeba žádné složité nastavení – stačí pár příkazů NuGet a můžete začít.

## Krok 1: Nainstalujte Aspose.OCR a připravte projekt

Nejprve je třeba přidat knihovnu OCR do vašeho projektu. Otevřete terminál ve složce řešení a spusťte:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

Tím se vytvoří nový konzolový projekt s názvem **OcrDemo** a přidá se NuGet balíček `Aspose.OCR`. Knihovna obsahuje třídu `OcrEngine`, kterou budeme používat.

> **Tip:** Pokud používáte počítač s dedikovaným GPU, ujistěte se, že máte nainstalován nejnovější grafický ovladač; jinak knihovna automaticky přejde do režimu CPU.

## Krok 2: Napište kompletní OCR kód

Nyní otevřete `Program.cs` a nahraďte jeho obsah následujícím. Každý řádek je okomentován, abyste viděli *proč* děláme to, co děláme.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Proč to funguje

- **ProcessingMode = Gpu** říká enginu, aby nejprve zkusil GPU. Knihovna abstrahuje nízkoúrovňová volání CUDA/OpenCL, takže nemusíte sami spravovat kontexty zařízení.  
- **IsGpuEnabled** je boolean, který potvrzuje, zda cesta přes GPU uspěla. Pokud vidíte `false`, engine automaticky přešel na CPU – není se čeho bát.  
- **RecognizeImage** provádí veškerou těžkou práci: načte obrázek, spustí OCR model a vrátí výsledek jako prostý text. Není potřeba ručně předzpracovávat bitmapu, pokud nemáte speciální požadavky (např. vyrovnání sklonu).

## Krok 3: Spusťte aplikaci a ověřte výstup

Zkompilujte a spusťte:

```bash
dotnet run
```

Pokud je vše nastaveno správně, uvidíte něco jako:

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

Pokud GPU není k dispozici, první řádek bude obsahovat `GPU used: False`, ale extrahovaný text se stále zobrazí – díky elegantnímu přechodu na CPU.

> **Často kladená otázka:** *Co když je můj obrázek JPEG místo TIFF?*  
> Metoda `RecognizeImage` akceptuje jakýkoli formát podporovaný .NET `System.Drawing` (JPEG, PNG, BMP, atd.). Stačí změnit příponu souboru v `imagePath`.

## Krok 4: Volitelné – Vyladění nastavení pro vyšší přesnost

Aspose.OCR nabízí několik nastavení, která můžete upravit:

| Nastavení | Co dělá | Kdy použít |
|-----------|----------|------------|
| `ocrEngine.Language` | Vynutí konkrétní jazyk (např. `OcrLanguage.English`) | Pokud znáte jazyk dokumentu |
| `ocrEngine.PageSegMode` | Řídí, jak engine rozděluje stránky na bloky | Pro vícesloupcové rozvržení |
| `ocrEngine.DetectOrientation` | Automaticky otočí text, který není svislý | Skeny, které mohou být vzhůru nohama |

Tyto vlastnosti můžete nastavit před voláním `RecognizeImage`. Například:

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## Krok 5: Vizualizace toku (Obrázek s alternativním textem)

Níže je jednoduchý diagram, který ilustruje **jak používat OCR** s volitelným zrychlením pomocí GPU. Není nutný pro spuštění kódu, ale pomáhá pochopit celkový obrázek.

![Diagram ukazující, jak používat OCR se zpracováním na GPU](/images/ocr-gpu-flow.png)

*Alt text:* *Diagram ukazující, jak používat OCR se zpracováním na GPU, zvýrazňující přechod na CPU, pokud je potřeba.*

## Okrajové případy a řešení problémů

1. **Out‑of‑Memory na GPU** – Velmi velké obrázky mohou překročit paměť GPU. V takovém případě knihovna automaticky přejde na CPU. Můžete předem zmenšit velikost obrázku, aby byl paměťový nárok nízký.  
2. **Nesprávný formát obrázku** – Pokud `RecognizeImage` vyhodí *NotSupportedException*, ověřte příponu souboru a ujistěte se, že obrázek není poškozený. Převod na PNG často problém vyřeší.  
3. **Nízké skóre důvěry** – Když výsledek OCR obsahuje mnoho nečitelnych znaků, zvažte předzpracování (binarizaci, odstraňování šumu) nebo přechod na sken s vyšším rozlišením.  

## Shrnutí: Co jsme dosáhli

Právě jsme pokryli **jak používat OCR** v C# konzolové aplikaci, ukázali, jak **extrahovat text ze souborů s obrázky**, a ukázali, jak **povolit zpracování na GPU** pro rychlejší výsledky. Nyní víte, jak **převést sken na text**, ověřit, zda byl GPU skutečně použit, a vyladit několik nastavení pro okrajové scénáře.

### Další kroky

- Zkuste výstup vložit do **vyhledávacího indexu** (např. Elasticsearch), aby se vaše skenované PDF staly prohledávatelnými.  
- Experimentujte s **dávkovým zpracováním** – procházejte složku s obrázky a zapisujte každý výsledek do souboru `.txt`.  
- Kombinujte OCR s **překladovými API**, aby se automaticky překládaly skenované dokumenty v cizím jazyce.  

Máte další otázky? Zanechte komentář a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}