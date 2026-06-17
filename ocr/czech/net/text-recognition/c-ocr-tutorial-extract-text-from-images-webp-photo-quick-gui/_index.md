---
category: general
date: 2026-03-17
description: c# OCR tutoriál – objevte, jak extrahovat text z obrázkových souborů,
  číst text z fotografií ve formátu WebP a převést obrázek na text pomocí jednoduchého
  OcrEngine.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: cs
og_description: c# OCR tutoriál vám ukáže, jak extrahovat text z obrazových souborů,
  číst text z fotografií ve formátu WebP a převést obrázek na text pomocí několika
  řádků kódu.
og_title: c# OCR tutoriál – Extrahujte text z obrázků během několika minut
tags:
- C#
- OCR
- Image Processing
title: 'c# OCR tutoriál: Extrahování textu z obrázků (WebP, fotografie) – Rychlý průvodce'
url: /cs/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

didn't miss any markdown formatting. Keep code block placeholders unchanged.

Check for any URLs: none.

Now produce final output with all translated content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutoriál – Extrahování textu z obrázků (WebP, Fotografie)

Už jste někdy potřebovali **extrahovat text z obrázku** souborů, ale nebyli jste si jisti, kde začít v C#? Možná máte screenshot ve formátu WebP, JPEG účtenky nebo naskenovanou stránku PDF a chcete jen slova uvnitř. V tomto **c# OCR tutoriálu** projdeme kompletním, připraveným k běhu příkladem, který čte text z fotografie, zpracovává WebP a další moderní formáty a převádí obrázek na prostý text – vše během několika řádků.

**Co z toho máte?** Budete schopni převést jakýkoli obrázek s textem na prohledávatelné řetězce, vložit je do databází nebo poslat do následných AI pipeline. Žádná magie, jen spolehlivý OCR engine, několik .NET API a jasná vysvětlení „proč“ za každým krokem.

## Co budete potřebovat

- **.NET 6 SDK** (nebo novější). Kód níže se kompiluje s .NET 6+ a běží na Windows, Linuxu nebo macOS.
- **Visual Studio 2022** nebo jakýkoli editor, který preferujete (VS Code funguje dobře).
- NuGet balíček **`Microsoft.Windows.SDK.Contracts`** (poskytuje `Windows.Media.Ocr`). Nainstalujte pomocí:

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- Obrázkový soubor, který chcete zpracovat – pro tento tutoriál použijeme **WebP** fotografii pojmenovanou `photo.webp` umístěnou ve složce `YOUR_DIRECTORY`.

> Pro tip: Pokud jste na ne‑Windows platformě, můžete nahradit `OcrEngine` knihovnou napříč platformami jako **Tesseract**. Ostatní kód zůstane prakticky stejný.

## Krok 1: Nastavení projektu C# OCR tutoriál

Nejprve vytvořte nový konzolový aplikaci. Otevřete terminál a spusťte:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Přidejte požadovaný balíček (jak je ukázáno výše) a otevřete projekt ve svém IDE. Toto základem poskytuje čistý start pro **c# OCR tutoriál**.

## Krok 2: Importujte jmenné prostory a připravte obrázek

Potřebujeme několik `using` direktiv, aby kompilátor věděl, kde najít `OcrEngine`, `SoftwareBitmap` a pomocníky pro načítání obrázků.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **Proč tyto jmenné prostory?**  
> `Windows.Media.Ocr` obsahuje třídu `OcrEngine`, která skutečně provádí rozpoznávání. `Windows.Graphics.Imaging` nám umožňuje dekódovat obrázek (včetně WebP) do `SoftwareBitmap`, který engine rozumí. Pomocníky `System.IO` a `Windows.Storage.Streams` usnadňují načítání souborů.

Nyní načtěte obrázek. Vestavěný dekodér zvládne WebP, HEIF, PNG, JPEG a další, takže můžete **číst text z WebP** bez extra pluginů.

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **Hraniční případ:** Pokud je váš obrázek již černobílý, můžete krok konverze přeskočit. Převod na odstíny šedi je malý výkonový zisk a často zlepšuje rozpoznávání na šumivých fotografiích.

## Krok 3: Spusťte OCR engine – Rozpoznání textu z fotografie

Zde je jádro **c# OCR tutoriálu**. Vytvoříme instanci `OcrEngine`, předáme jí bitmapu a získáme rozpoznaný text.

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Co se děje?**  
- `TryCreateFromUserProfileLanguages()` vybere jazyk(y), které jsou nastaveny ve vašem Windows uživatelském profilu, což obvykle zahrnuje angličtinu, španělštinu atd. Pokud potřebujete konkrétní jazyk, použijte `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))`.  
- `RecognizeAsync` provádí těžkou práci na pozadí a vrací `OcrResult`, který obsahuje surový řetězec, ohraničující rámečky slov a skóre důvěry.  
- Nakonec vytiskneme `ocrResult.Text`, což vám poskytne výsledek **převodu obrázku na text**, který můžete dále použít.

## Krok 4: Kompletní, spustitelný příklad

Spojením všeho dohromady, zde je samostatný program, který můžete zkopírovat do `Program.cs`. Kompiluje se, běží a vypíše text extrahovaný z `photo.webp`.

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### Očekávaný výstup

Pokud `photo.webp` obsahuje větu „Hello, world! This is a test.“ uvidíte něco jako:

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

Přesné zalomení řádků závisí na rozložení zdrojového obrázku, ale výsledek **extrahování textu z obrázku** bude vždy prostý řetězec, který můžete dále manipulovat.

## Časté otázky a hraniční případy

### Funguje to s jinými formáty obrázků?

Ano. Použitý dekodér (`BitmapDecoder`) automaticky rozpozná JPEG, PNG, BMP, GIF, **WebP**, HEIF a další. Takže můžete **číst text z WebP**, JPEG nebo dokonce TIFF bez změny kódu.

### Co když OCR engine vrátí nízkou důvěru?

Můžete zkontrolovat `ocrResult.Lines` a každé `OcrWord` pro `ConfidenceScore`. Pokud je skóre pod prahem (např. 0.6), zvažte:

- Předzpracování obrázku (zvýšení kontrastu, zaostření, vyrovnání).  
- Použití zdrojového obrázku s vyšším rozlišením.  
- Přechod na specializovanou knihovnu jako **Tesseract** pro vícejazyčnou podporu.

### Jak zacházet s více jazyky na jednom obrázku?

Vytvořte samostatné instance `OcrEngine` pro každý jazyk a spusťte je sekvenčně, nebo použijte knihovnu, která podporuje detekci smíšených jazyků. Pro vestavěný engine můžete předat objekt `Language`:

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### Můžu to spustit na Linuxu/macOS?

`Windows.Media.Ocr` API je pouze pro Windows. Na ne‑Windows platformách nahraďte část OCR knihovnou **Tesseract** (přes `Tesseract.Net.SDK`). Kód pro načítání a předzpracování zůstává stejný, takže zbytek tohoto **c# OCR tutoriálu** stále platí.

## Pro tipy pro lepší přesnost

- **Změňte velikost** velkých obrázků na maximálně 2000 px na delší straně – OCR enginy pracují rychleji při středních velikostech.  
- **Odstraňte šum** pomocí jednoduchého Gaussova rozostření, pokud je foto zrnitý.  
- **Vyrovnejte** bitmapu, pokud text není dokonale horizontální; `SoftwareBitmap` lze před předáním `OcrEngine` otočit.  
- **Ukládejte do cache** instanci `OcrEngine`, pokud zpracováváte mnoho obrázků najednou; opakované vytváření přidává režii.

## Související témata k prozkoumání

- **Převod obrázku na text** pomocí **Tesseract** pro multiplatformní projekty.  
- **Extrahování textu z PDF** renderováním každé stránky na obrázek.  
- **Dávkový OCR**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}