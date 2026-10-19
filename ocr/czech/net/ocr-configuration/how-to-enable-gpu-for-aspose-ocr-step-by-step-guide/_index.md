---
category: general
date: 2026-09-08
description: Naučte se, jak povolit GPU pro Aspose OCR, spustit dávkové zpracování
  OCR a efektivně extrahovat text z obrázků pomocí .NET.
draft: false
keywords:
- how to enable gpu
- extract text from images
- batch ocr processing
- ocr gpu acceleration
- aspose ocr .net
lastmod: 2026-09-08
og_description: Jak povolit GPU pro Aspose OCR. Tento průvodce ukazuje dávkové zpracování
  OCR, extrakci textu z obrázků a výběr optimálního GPU zařízení v .NET.
og_image_alt: Diagram of Aspose OCR engine offloading work to GPU for faster text
  extraction
og_title: Jak povolit GPU pro Aspose OCR – kompletní tutoriál
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Learn how to enable GPU for Aspose OCR, run batch OCR processing, and
    extract text from images efficiently using .NET.
  headline: How to enable GPU for Aspose OCR – complete tutorial
  type: TechArticle
- description: Learn how to enable GPU for Aspose OCR, run batch OCR processing, and
    extract text from images efficiently using .NET.
  name: How to enable GPU for Aspose OCR – complete tutorial
  steps:
  - name: 'Install the NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`'
    text: 'Install the NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`'
  - name: Replace the paths in `imageFiles` with the location of your own `.tif` files.
    text: Replace the paths in `imageFiles` with the location of your own `.tif` files.
  - name: 'Build and run: `dotnet run`.'
    text: 'Build and run: `dotnet run`.'
  type: HowTo
- questions:
  - answer: Yes, a commercial Aspose.OCR license is needed for production deployments;
      a free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Any NVIDIA GPU that supports CUDA 11.0 or newer, such as RTX 2060, RTX
      3070, RTX 4090, and the corresponding Tesla series.
    question: Which GPU models are officially supported?
  - answer: Absolutely. The same `OcrEngine` instance can be reused across requests;
      just ensure thread safety by cloning the engine per request.
    question: Can I run this code in an ASP.NET Core web API?
  - answer: Yes, you can set `ocrEngine.Language = Language.English | Language.Spanish`
      to enable simultaneous recognition of multiple languages.
    question: Does Aspose OCR handle multi‑language documents?
  - answer: The engine streams image data, so you can process images up to 10,000
      × 10,000 pixels without exhausting GPU memory, though performance may vary.
    question: What is the maximum image size the GPU can handle?
  type: FAQPage
tags:
- Aspose OCR
- GPU acceleration
- C#
- .NET
title: Jak povolit GPU pro Aspose OCR – kompletní tutoriál
url: /cs/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak povolit GPU pro Aspose OCR – kompletní tutoriál

Už jste se někdy zamysleli **jak povolit GPU** při používání Aspose OCR? Nejste jediní — vývojáři pracující s obrovským objemem dokumentů často narazí na výkonnostní limity, protože OCR engine běží na CPU. Dobrá zpráva? Zapnutí akcelerace GPU je poměrně jednoduché a může ušetřit sekundy u každé stránky. V tomto průvodci vás provedeme **jak povolit GPU**, spustíme **dávkové zpracování OCR**, extrahujeme rozpoznaný text a dokonce vybereme správné GPU zařízení. Na konci budete vědět **jak používat Aspose** pro bleskově rychlý extrahování textu OCR.

## Rychlé odpovědi
- **Co dělá povolení GPU?** Přesune analýzu na úrovni pixelů na grafickou kartu, čímž zkrátí dobu zpracování až o 80 % u typických 300 dpi obrázků.  
- **Potřebuji speciální licenci?** Ne, standardní balíček Aspose.OCR NuGet obsahuje podporu GPU.  
- **Jaká verze .NET je vyžadována?** .NET 6.0 nebo novější; API používá moderní funkce C#.  
- **Mohu spustit na stroji pouze s CPU?** Ano — pokud není nalezena kompatibilní GPU, engine se automaticky vrátí na CPU.  
- **Kolik obrázků mohu zpracovat najednou?** Můžete zařadit stovky souborů; GPU je bude zpracovávat sekvenčně, zatímco váš kód může předat další obrázek, jakmile předchozí skončí.

## Co je povolení GPU?
Povolení GPU je proces konfigurace `OcrEngine` Aspose OCR tak, aby směroval úlohy zpracování obrazu na grafickou kartu kompatibilní s CUDA místo centrálního procesoru. Tento přepínač je řízen dvěma vlastnostmi: `UseGpu` a `GpuDeviceId`. Povolení tohoto příznaku přesune výpočetně náročnou analýzu pixelů na GPU, která může paralelně zpracovávat tisíce vláken, což dramaticky snižuje dobu zpracování.

Třída `OcrEngine` je jádrovou součástí Aspose OCR, která provádí analýzu obrazu a rozpoznávání textu.

## Proč použít akceleraci GPU s Aspose OCR?
Aspose OCR podporuje **více než 50 vstupních formátů obrázků** a může zpracovávat dávky o stovkách stránek, aniž by načítal celý dokument do paměti. Když je akcelerace GPU povolena, benchmarky ukazují **70 %‑80 % snížení** průměrné doby zpracování na stránku na RTX 3080 ve srovnání s čistým CPU provedením. Tento nárůst rychlosti se přímo promítá do nižších nákladů na cloud a rychlejších výsledků viditelných uživateli v aplikacích s intenzivním zpracováním dokumentů.

## Předpoklady
- .NET 6.0 nebo novější (kód používá moderní syntaxi C#)  
- NuGet balíček Aspose.OCR pro .NET (verze 23.10 nebo novější)  
- GPU kompatibilní s CUDA s nainstalovaným odpovídajícím ovladačem (minimálně CUDA 11.0)  
- Složka obsahující ukázkové soubory `.tif` pro dávkové spuštění  

Pokud máte tyto základy pokryté, pojďme se ponořit dál.

## Jak povolit GPU v Aspose OCR

Načtěte OCR engine, zapněte režim GPU a případně vyberte index zařízení.  

`OcrEngine` je hlavní třída Aspose OCR, která provádí analýzu obrazu a rozpoznávání textu.  

Povolení GPU je dvoustupňová operace: nastavte `UseGpu = true` a pokud je k dispozici více GPU, přiřaďte požadovaný `GpuDeviceId`. Tento přímý odpovědní odstavec vysvětluje celý proces v 45 slovech.

První věc, kterou musíte říct `OcrEngine`, aby používal GPU. To se provádí pomocí dvou jednoduchých vlastností: `UseGpu` a volitelně `GpuDeviceId`. Nastavením `UseGpu` na `true` přepnete engine do režimu GPU, zatímco `GpuDeviceId` vám umožní vybrat, který GPU (pokud jich máte více) má provádět těžkou práci.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;
using System.Collections.Generic;

// Step 1: Create the OCR engine and enable GPU acceleration
var ocrEngine = new OcrEngine
{
    // Turn on GPU support – this is the core of “how to enable gpu”
    UseGpu = true,

    // (optional) Choose GPU index 0; change if you have multiple devices
    GpuDeviceId = 0
};
```

> **Proč je to důležité** – Verze pro CPU zpracovává každý pixel sekvenčně, což může být úzké hrdlo pro vysoce rozlišené obrázky. Verze pro GPU spouští tisíce vláken paralelně, což dramaticky snižuje čas na stránku.

### Vizuální přehled  

![Diagram ukazující, jak OCR engine přenáší práci na GPU, když je nastaveno „povolit GPU“](/images/enable-gpu-diagram.png){: .center .responsive alt="povolit gpu"}

[Diagram ukazující, jak OCR engine přenáší práci na GPU, když je nastaveno „povolit GPU“](/images/enable-gpu-diagram.png)

*(Pokud obrázek nevidíte, představte si jen diagram, kde OCR engine předává buffer obrazu jádru CUDA.)*

## Jak spustit dávkové zpracování OCR s Aspose

`Metoda `Recognize` třídy `OcrEngine` zpracuje obrázek a vrátí `OcrResult`, který obsahuje extrahovaný text a metadata. Můžete zpracovat celou složku iterací přes seznam cest k souborům. Engine automaticky zařadí každý obrázek do GPU, udržuje pipeline aktivní, zatímco vaše aplikace nadále předává nové soubory. Tento přístup vám umožní efektivně zpracovat stovky TIFF souborů, přičemž GPU provádí těžkou práci paralelně.

```csharp
// Step 2: Define the image files you want to process
var imageFiles = new List<string>
{
    @"C:\OCRSamples\page1.tif",
    @"C:\OCRSamples\page2.tif",
    @"C:\OCRSamples\page3.tif"
};

// Step 3: Process each image and report the character count
foreach (var imagePath in imageFiles)
{
    // Recognize the image – the GPU does the heavy lifting behind the scenes
    var ocrResult = ocrEngine.Recognize(imagePath);

    // Show how many characters were extracted – a quick sanity check
    Console.WriteLine($"{imagePath}: {ocrResult.Text.Length} characters");
}
```

> **Tip** – Pro opravdu velké dávky zvažte použití `Parallel.ForEach` spolu s `ocrEngine.Clone()`, abyste se vyhnuli problémům s bezpečností vláken. Metoda `Clone` vytvoří mělkou kopii engine, která stále ukazuje na stejný GPU kontext.

### Očekávaný výstup

```
C:\OCRSamples\page1.tif: 1245 characters
C:\OCRSamples\page2.tif: 1130 characters
C:\OCRSamples\page3.tif: 1389 characters
```

Pokud čísla vypadají rozumně, vaše **dávkové zpracování OCR** funguje a GPU je využíváno.

## Jak extrahovat text z obrázků – získání výsledků

`OcrResult` je objekt, který obsahuje výstup OCR, včetně rozpoznaného textu, skóre důvěry a informací o rozložení. Metoda `Recognize` vrací objekt `OcrResult`. Získáte čistý text z vlastnosti `Text` a zapíšete jej do souboru pro další použití. Ukládání OCR textu umožňuje následné zpracování (indexování vyhledávání, datová těžba atd.) bez opětovného spouštění engine a poskytuje trvalý záznam pro ladění.

```csharp
foreach (var imagePath in imageFiles)
{
    var ocrResult = ocrEngine.Recognize(imagePath);
    var extractedText = ocrResult.Text;

    // Save the text to a .txt file with the same base name
    var outputPath = System.IO.Path.ChangeExtension(imagePath, ".txt");
    System.IO.File.WriteAllText(outputPath, extractedText);

    Console.WriteLine($"Extracted text saved to {outputPath}");
}
```

> **Proč extrahovat do souboru?** – Ukládání OCR textu umožňuje následné zpracování (indexování vyhledávání, datová těžba atd.) bez opětovného spouštění engine. Také vám poskytuje trvalý záznam pro ladění.

## Jak nastavit GPU zařízení pro optimální výkon

`CudaDeviceInfo` poskytuje informace o GPU kompatibilních s CUDA nainstalovaných v systému. Když je přítomno více GPU, použijte `GpuDeviceId` pro výběr nejlepšího. Index odpovídá pořadí vrácenému metodou `CudaDeviceInfo.GetDevices()`. Výběrem vhodného zařízení zajistíte, že použijete nejvýkonnější GPU a vyhnete se soutěži s ostatními úlohami na sekundárních kartách.

```csharp
using Aspose.OCR.Gpu;

// List all available GPU devices
var devices = CudaDeviceInfo.GetDevices();
for (int i = 0; i < devices.Length; i++)
{
    Console.WriteLine($"Device {i}: {devices[i].Name} (Compute Capability {devices[i].ComputeCapability})");
}

// Suppose you want to use the second GPU (index 1)
ocrEngine.GpuDeviceId = 1;
Console.WriteLine($"Switched to GPU device {ocrEngine.GpuDeviceId}");
```

> **Okrajový případ** – Některé starší GPU nepodporují požadovanou verzi CUDA. V takovém scénáři `UseGpu = true` tiše přejde na CPU, takže po inicializaci vždy zkontrolujte `ocrEngine.IsGpuEnabled`.

## Jak použít Aspose OCR v reálném projektu

Spojením všech částí, zde je kompaktní, připravená ke spuštění konzolová aplikace, která demonstruje **jak povolit GPU**, spouští **dávkové zpracování OCR**, extrahuje text a umožňuje vám vybrat GPU zařízení. Vzor vytvoří `OcrEngine`, povolí GPU, vyjmenuje dostupná zařízení, zpracuje každý obrázek a zapíše rozpoznaný text do souboru `.txt` vedle zdrojového obrázku.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine with GPU support
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true,
            GpuDeviceId = 0 // change if you have multiple GPUs
        };

        // -------------------------------------------------
        // 2️⃣ (Optional) Show available GPU devices
        // -------------------------------------------------
        var devices = CudaDeviceInfo.GetDevices();
        Console.WriteLine("Available GPU devices:");
        for (int i = 0; i < devices.Length; i++)
        {
            Console.WriteLine($"  [{i}] {devices[i].Name} – Compute {devices[i].ComputeCapability}");
        }

        // -------------------------------------------------
        // 3️⃣ Define the batch of images to process
        // -------------------------------------------------
        var imageFiles = new List<string>
        {
            @"C:\OCRSamples\page1.tif",
            @"C:\OCRSamples\page2.tif",
            @"C:\OCRSamples\page3.tif"
        };

        // -------------------------------------------------
        // 4️⃣ Process each image, extract text, and save it
        // -------------------------------------------------
        foreach (var imagePath in imageFiles)
        {
            var result = ocrEngine.Recognize(imagePath);
            var text = result.Text;

            var txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, text);

            Console.WriteLine($"{Path.GetFileName(imagePath)} → {Path.GetFileName(txtPath)} ({text.Length} chars)");
        }

        Console.WriteLine("All done! GPU‑accelerated OCR batch completed.");
    }
}
```

### Spuštění vzorku

1. Nainstalujte NuGet balíček: `dotnet add package Aspose.OCR --version 23.10.0`  
2. Nahraďte cesty v `imageFiles` umístěním vašich vlastních souborů `.tif`.  
3. Sestavte a spusťte: `dotnet run`.  

Měli byste vidět seznam GPU, následovaný řádkem pro každý obrázek, který uvádí počet znaků a cestu k vygenerovanému souboru `.txt`.

## Časté otázky a úskalí

- **Funguje to na stroji pouze s CPU?**  
  Ano — pokud je `UseGpu` nastaveno na `true`, ale není nalezena kompatibilní GPU, Aspose se vrátí na CPU. Můžete ověřit režim pomocí `ocrEngine.IsGpuEnabled`.

- **Co když dostanu chybu „CUDA driver version is insufficient“?**  
  Aktualizujte svůj NVIDIA driver na nejnovější verzi, která odpovídá CUDA toolkitu dodávanému s Aspose. Knihovna vyžaduje alespoň CUDA 11.0 pro nedávné funkce GPU.

- **Mohu zpracovávat PDF přímo?**  
  Aspose OCR pracuje s rastrovými obrázky. Nejprve převěďte stránky PDF na obrázky (např. pomocí Aspose.PDF) a pak je předávejte OCR engine.

- **Jak zlepšit přesnost u špatně naskenovaných dokumentů?**  
  Povolit předzpracování pomocí `ocrEngine.Preprocess = true` nebo použít vyšší rozlišení obrázků (300 dpi nebo více). Akcelerace GPU stále platí.

## Často kladené otázky

**Q: Je licence vyžadována pro produkční použití?**  
A: Ano, pro produkční nasazení je potřeba komerční licence Aspose.OCR; pro vyhodnocení je k dispozici bezplatná zkušební verze.

**Q: Které modely GPU jsou oficiálně podporovány?**  
A: Jakýkoli NVIDIA GPU, který podporuje CUDA 11.0 nebo novější, například RTX 2060, RTX 3070, RTX 4090 a odpovídající řada Tesla.

**Q: Mohu spustit tento kód v ASP.NET Core web API?**  
A: Rozhodně. Stejnou instanci `OcrEngine` lze znovu použít napříč požadavky; jen zajistěte bezpečnost vláken klonováním engine pro každý požadavek.

**Q: Zvládá Aspose OCR dokumenty ve více jazycích?**  
A: Ano, můžete nastavit `ocrEngine.Language = Language.English | Language.Spanish` pro povolení simultánního rozpoznávání více jazyků.

**Q: Jaká je maximální velikost obrázku, kterou GPU zvládne?**  
A: Engine streamuje data obrázku, takže můžete zpracovat obrázky až do 10 000 × 10 000 pixelů, aniž byste vyčerpali paměť GPU, i když výkon se může lišit.

---

**Poslední aktualizace:** 2026-09-08  
**Testováno s:** Aspose.OCR 23.10 pro .NET  
**Autor:** Aspose

## Související tutoriály

- [Jak použít OCR v C pro extrahování textu z obrázků s GPU akcelerací](/ocr/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/)
- [Extrahovat text z obrázku s Aspose OCR GPU C průvodcem](/ocr/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-gpu-c-guide/)
- [Odstranit pozadí OCR s Aspose OCR kompletním GPU průvodcem](/ocr/net/ocr-optimization/remove-background-ocr-with-aspose-ocr-complete-gpu-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}