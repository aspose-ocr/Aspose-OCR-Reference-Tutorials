---
category: general
date: 2026-06-06
description: Rozpoznávejte text na obrázku pomocí C# OCR – krok za krokem příklad
  C# OCR, který extrahuje text ze skenů a během několika minut převádí sken na text.
draft: false
keywords:
- recognize text image
- c# ocr example
- extract text scan
- convert scan to text
- image to text c#
language: cs
og_description: Rozpoznávejte text z obrázku pomocí C# OCR. Naučte se praktický příklad
  C# OCR, který extrahuje text ze skenů, převádí sken na text a zpracovává reálné
  obrázky.
og_title: Rozpoznání textu na obrázku v C# – Kompletní OCR tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: recognize text image using C# OCR – a step‑by‑step c# ocr example that
    extracts text from scans and convert scan to text in minutes.
  headline: recognize text image in C# – Full OCR Guide
  type: TechArticle
- questions:
  - answer: The `Windows.Media.Ocr` namespace is Windows‑only. On Linux or macOS you’d
      swap it for TesseractSharp or IronOcr—both expose a similar `Engine.Recognize`
      method, so the surrounding code stays virtually unchanged.
    question: Does this work on .NET Core on Linux?
  - answer: Handwriting recognition is still experimental. For best results, stick
      to printed fonts or consider a cloud service like Azure Cognitive Services if
      you need high accuracy.
    question: How accurate is the built‑in OCR for handwritten notes?
  - answer: 'Not out of the box. Convert each PDF page to an image first (using `PdfSharp`
      or `Ghostscript`) and then feed the bitmap to the OCR engine. --- ## Conclusion
      You now have a complete, production‑ready **c# ocr example** that can **recognize
      text image** files, **extract text scan** contents, and **co'
    question: Can I process PDFs directly?
  type: FAQPage
tags:
- OCR
- C#
- Image Processing
title: Rozpoznání textu na obrázku v C# – Kompletní průvodce OCR
url: /cs/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznat textový obrázek v C# – Kompletní OCR tutoriál

Už jste se někdy zamýšleli, jak **recognize text image** přímo ze skenované fotografie pomocí C#? Nejste v tom sami. Ať už digitalizujete staré účtenky, získáváte data z vizitky, nebo jen převádíte nízkokvalitní sken na editovatelný text, schopnost extrahovat text z obrázku je užitečný trik, který by měl mít každý vývojář ve svém arzenálu.

V tomto průvodci projdeme **c# ocr example**, který načte obrázek, spustí optické rozpoznávání znaků a vypíše výsledek do konzole. Na konci budete schopni **extract text scan** soubory, **convert scan to text** a dokonce vyladit proces pro šumivé obrázky. Žádné složité služby třetích stran – jen vestavěné Windows.Media.Ocr API (nebo jakýkoli kompatibilní OcrEngine) a pár řádků kódu.

## Co se naučíte

* Jak nastavit C# projekt pro OCR.
* Přesný kód potřebný k **recognize text image** souborům.
* Tipy pro práci s nízkým rozlišením skenů a vícestránkovými dokumenty.
* Způsoby, jak rozšířit příklad na znovupoužitelnou knihovnu pro vaše aplikace.

### Požadavky

* .NET 6.0 nebo novější (API funguje i na .NET 5+).
* Visual Studio 2022 (Community edice je v pořádku) nebo libovolné IDE, které preferujete.
* Ukázkový obrázek, např. `lowres_scan.jpg`, umístěný ve složce, na kterou můžete odkazovat.
* Základní znalost async/await – volání OCR jsou asynchronní v Windows API.

> **Pro tip:** Pokud pracujete na ne‑Windows platformě, zaměňte jmenný prostor `Windows.Media.Ocr` za multiplatformní knihovnu jako TesseractSharp; zbytek logiky zůstane stejný.

---

## Krok 1: Nastavení pro **recognize text image** s OCR enginem

Nejprve potřebujeme instanci OCR enginu. Třída `OcrEngine` je vstupním bodem pro jakoukoli operaci **image to text c#**.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Create the OCR engine – default language is English.
        OcrEngine engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));
        if (engine == null)
        {
            Console.WriteLine("Failed to create OcrEngine. Make sure you are on Windows 10 version 1809 or later.");
            return;
        }

        // Continue with the rest of the pipeline...
```

**Proč je to důležité:** Engine abstrahuje těžkou práci rozpoznávání vzorů. Explicitním vytvořením získáte kontrolu nad nastavením jazyka, což je nezbytné, když později chcete **extract text scan** dokumenty v jiných jazycích.

## Krok 2: Načtení souboru obrázku – jádro **convert scan to text**

Dále načteme obrázek z disku a převedeme jej na `SoftwareBitmap`, formát, který OCR engine očekává.

```csharp
        // Load the image file into a SoftwareBitmap.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "lowres_scan.jpg");
        using (FileStream fs = new FileStream(imagePath, FileMode.Open, FileAccess.Read))
        {
            // Decode the image (supports JPEG, PNG, BMP, etc.).
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Optional: upscale low‑resolution images for better accuracy.
            SoftwareBitmap upscaled = SoftwareBitmap.Convert(bitmap, bitmap.BitmapPixelFormat, bitmap.BitmapAlphaMode);
            // Pass the bitmap to OCR.
            await RecognizeAsync(engine, upscaled);
        }
    }
```

**Proč to děláme:** Přímé předání surového souborového proudu do OCR často vede k špatným výsledkům, zejména u nízkokvalitních skenů. Konverze na `SoftwareBitmap` nám umožní upravit DPI, barevnou hloubku a dokonce aplikovat filtry před rozpoznáním.

## Krok 3: Provedení operace **recognize text image**

Nyní konečně zavoláme metodu `RecognizeAsync` enginu. Tady se děje kouzlo.

```csharp
    private static async Task RecognizeAsync(OcrEngine engine, SoftwareBitmap bitmap)
    {
        // Run OCR – this returns an OcrResult object.
        OcrResult result = await engine.RecognizeAsync(bitmap);

        // The Result contains a collection of lines and words.
        Console.WriteLine("=== OCR Output ===");
        foreach (var line in result.Lines)
        {
            Console.WriteLine(line.Text);
        }

        // For a quick **image to text c#** check, also output the raw string.
        Console.WriteLine("\nFull Text:\n" + result.Text);
    }
}
```

**Co uvidíte:** Pokud `lowres_scan.jpg` obsahuje frázi „Hello World“, konzole vypíše:

```
=== OCR Output ===
Hello World

Full Text:
Hello World
```

To je celý **c# ocr example** v akci – jen čtyři logické kroky, přesto pokrývá vše od načtení souboru po finální výstup.

## Krok 4: Řešení okrajových případů – když sken není dokonalý

Reálné obrázky nejsou vždy ostré. Zde je několik úprav, které můžete provést bez přepisování celého programu:

| Problém | Rychlé řešení |
|-------|-----------|
| **Velmi nízké DPI (≤ 72)** | Zvětšete bitmapu pomocí `BitmapTransform` před rozpoznáním. |
| **Šikmý text** | Použijte transformační rotaci (`SoftwareBitmap.Rotate`) k narovnání stránky. |
| **Více jazyků** | Vytvořte `OcrEngine.TryCreateFromLanguage(new OcrLanguage("en-fr"))` a nastavte `engine.Language` podle potřeby. |
| **Velké soubory** | Zpracovávejte obrázek po částech (`engine.RecognizeAsync(tileBitmap)`) a výsledky spojte. |

Tyto úpravy zajistí, že vaše rutina **extract text scan** zůstane spolehlivá i při práci s šumivými účtenkami nebo fotografiemi pořízenými pod úhlem.

## Krok 5: Přeměna příkladu na znovupoužitelný pomocník (volitelné)

Pokud plánujete **convert scan to text** na několika místech aplikace, zabalte logiku do malé utility třídy:

```csharp
public static class OcrHelper
{
    private static readonly OcrEngine _engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));

    public static async Task<string> ImageToTextAsync(string filePath)
    {
        using var fs = new FileStream(filePath, FileMode.Open, FileAccess.Read);
        var decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
        var bitmap = await decoder.GetSoftwareBitmapAsync();

        var result = await _engine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

Nyní stačí zavolat:

```csharp
string text = await OcrHelper.ImageToTextAsync("YOUR_DIRECTORY/lowres_scan.jpg");
Console.WriteLine(text);
```

**Proč to budete milovat:** Pomocník izoluje OCR logiku, takže se můžete soustředit na obchodní logiku – ideální pro **c# ocr example**, který bude znovu použit napříč projekty.

---

![recognize text image example](https://example.com/ocr-demo.png "Screenshot of OCR console output showing recognize text image result")

*Alt text:* **příklad rozpoznání textového obrázku** z C# OCR konzolové aplikace.

---

## Často kladené otázky

**Q: Funguje to na .NET Core na Linuxu?**  
A: Jmenný prostor `Windows.Media.Ocr` je pouze pro Windows. Na Linuxu nebo macOS jej nahradíte TesseractSharp nebo IronOcr – oba poskytují podobnou metodu `Engine.Recognize`, takže okolní kód zůstane prakticky beze změny.

**Q: Jak přesná je vestavěná OCR pro ručně psané poznámky?**  
A: Rozpoznávání rukopisu je stále experimentální. Pro nejlepší výsledky používejte tištěné fonty nebo zvažte cloudovou službu jako Azure Cognitive Services, pokud potřebujete vysokou přesnost.

**Q: Můžu zpracovávat PDF přímo?**  
A: Ne přímo. Nejprve převěďte každou stránku PDF na obrázek (pomocí `PdfSharp` nebo `Ghostscript`) a pak bitmapu předáte OCR engine.

---

## Závěr

Nyní máte kompletní, produkčně připravený **c# ocr example**, který dokáže **recognize text image** soubory, **extract text scan** obsah a **convert scan to text** během několika řádků kódu. Porozuměním toku – vytvoření enginu, načtení obrázku, asynchronní rozpoznání a zpracování výsledku – můžete tento vzor přizpůsobit libovolnému C# projektu, který potřebuje převádět obrázky na prohledávatelné řetězce.

Jste připraveni na další krok? Zkuste přidat jednoduché UI pomocí WinForms nebo WPF, experimentujte s různými jazyky nebo propojte výstup s databází pro prohledávatelné archivy. Možnosti jsou neomezené, když ovládnete techniky **image to text c#**.

Šťastné kódování a ať jsou vaše skeny vždy ostré!


## Co byste se měli naučit dál?


Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}