---
category: general
date: 2026-06-03
description: Příklad Aspose OCR v C#, který ukazuje, jak nastavit limit paměti GPU,
  načíst obrázek pro OCR a rozpoznat text z TIF souborů, včetně kompletního kódu a
  tipů.
draft: false
keywords:
- aspose ocr c# example
- set gpu memory limit
- load image for ocr
- recognize text from tif
- gpu acceleration asp ocr
- high‑resolution OCR c#
- asp ocr cuda setup
language: cs
og_description: 'Naučte se kompletní příklad Aspose OCR v C#: povolte GPU, nastavte
  limit paměti GPU, načtěte obrázek pro OCR a rozpoznávejte text z TIF souborů. Kompletní
  kód je zahrnut.'
og_title: Příklad Aspose OCR v C# – Akcelerace GPU, limit paměti a zpracování TIF
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Aspose OCR C# example showing how to set GPU memory limit, load image
    for OCR and recognize text from TIF files with full code and tips.
  headline: Aspose OCR C# Example – Enable GPU, Set Memory Limit & Process TIF Images
  type: TechArticle
- description: Aspose OCR C# example showing how to set GPU memory limit, load image
    for OCR and recognize text from TIF files with full code and tips.
  name: Aspose OCR C# Example – Enable GPU, Set Memory Limit & Process TIF Images
  steps:
  - name: Why set a memory limit?
    text: '- **Stability:** Prevents out‑of‑memory crashes when processing gigantic
      images. - **Co‑existence:** Allows other GPU‑heavy apps (e.g., TensorFlow models)
      to run side‑by‑side. - **Predictability:** Makes performance testing repeatable
      because the GPU won’t start swapping.'
  - name: Handling multi‑page TIFFs
    text: If your TIFF contains several pages, Aspose OCR will only read the first
      one by default. To process all pages, you can loop over `image.Pages` (available
      in newer SDK versions) and feed each page to the engine separately.
  - name: Why this works well with TIF
    text: '- **Lossless compression:** TIFF often stores raw pixel data, giving the
      OCR engine the highest fidelity. - **Multiple color spaces:** Aspose can handle
      grayscale, RGB, or even CMYK TIFFs without extra conversion code.'
  - name: Expected output
    text: 'Running the program on a clear, 300 dpi scan of a printed page typically
      yields something like:'
  - name: Quick checklist
    text: '- ✅ **Aspose OCR C# example** compiled without errors. - ✅ **GPU enabled**
      (`Enable = true`). - ✅ **GPU memory limit** set to 2048 MB. - ✅ **Image loaded**
      from a TIF file. - ✅ **Text recognized** and printed.'
  type: HowTo
tags:
- Aspose
- OCR
- C#
- GPU
title: Aspose OCR C# příklad – povolit GPU, nastavit limit paměti a zpracovat TIF
  obrázky
url: /cs/net/ocr-optimization/aspose-ocr-c-example-enable-gpu-set-memory-limit-process-tif/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR C# příklad – povolení GPU, nastavení limitu paměti a zpracování TIF obrázků

Už jste se někdy zamýšleli, jak získat maximální výkon z **Aspose OCR C# příkladu** při práci s obrovskými TIFF skeny? Nejste sami. V mnoha reálných projektech — například digitalizace archivů nebo extrakce dat z vysoce rozlišených účtenek — úzkým místem není samotný OCR algoritmus, ale využití hardwaru.

Aspose OCR podporuje akceleraci pomocí GPU, ale musíte mu přesně říct, kolik paměti může použít, načíst správný typ obrázku a nakonec získat rozpoznaný text ze souboru .tif. Tento tutoriál vás provede každým krokem, od instalace SDK až po ladění nastavení GPU, takže můžete spustit OCR na šílenou rychlost, aniž byste přetížili RAM vaší grafické karty.

Navíc přidáme několik „co‑když“ scénářů — například zpracování více‑stránkových TIFFů nebo přepnutí na CPU, pokud GPU není k dispozici — aby výsledek byl robustní řešení, ne jen jednorázový útržek kódu.

## Co budete potřebovat

Než se pustíme dál, ujistěte se, že máte na svém počítači následující komponenty:

| Předpoklad | Proč je důležitý |
|------------|-------------------|
| **.NET 6 SDK** (nebo novější) | Aspose OCR cílí na .NET Standard 2.0+, takže funguje s jakoukoliv aktuální verzí .NET. |
| **Aspose.OCR NuGet balíček** (`Install-Package Aspose.OCR`) | Hlavní knihovna, která poskytuje `OcrEngine`, `GpuSettings` atd. |
| **CUDA 11+** (NVIDIA) **nebo ROCm 5+** (AMD) | Požadováno pro akceleraci GPU; SDK během běhu zkontroluje kompatibilní driver. |
| GPU s alespoň **2 GB VRAM** (nastavíme limit na 2048 MB) | Bez dostatečné paměti může engine tiše přejít na CPU. |
| **Vysoké rozlišení TIFF** obrázek, který chcete zpracovat | Aspose OCR dokáže číst prakticky jakýkoliv rastrový formát, ale TIF je běžný pro skeny. |
| Visual Studio 2022 (nebo jakýkoliv oblíbený editor) | Pro sestavení a ladění C# projektu. |

Pokud některý z těchto komponent chybí, kód se stále zkompiluje, ale nebudete vidět požadované zrychlení.

## Krok 1: Vytvoření Aspose OCR C# příkladového enginu

Prvním krokem v každém **Aspose OCR C# příkladu** je vytvořit instanci OCR enginu. `OcrEngine` je jako režisér filmu — koordinuje vše od načtení obrázku po extrakci textu.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();
```

> **Tip:** Pokud plánujete zpracovávat mnoho obrázků po sobě, nechte jeden `OcrEngine` běžet po celou dobu. Opakované vytváření nového enginu pro každý obrázek přidává režii, která může převýšit samotný čas OCR.

## Krok 2: Nastavení limitu paměti GPU (a povolení akcelerace)

Nyní přichází část, která často lidi zaskočí: **nastavení limitu paměti GPU**. Ve výchozím nastavení se Aspose OCR pokusí využít co nejvíce VRAM, což na sdílené pracovní stanici může odepřit jiné aplikace. Objekt `GpuSettings` vám umožní omezit alokaci.

```csharp
        // Step 2: Enable GPU acceleration (requires CUDA 11+ or ROCm 5+)
        ocrEngine.Settings.Gpu = new GpuSettings
        {
            Enable = true,          // Turn on the GPU path
            DeviceId = 0,           // First GPU in the system (change if you have multiple)
            MemoryLimitMb = 2048    // Optional cap – 2 GB in this example
        };
```

### Proč nastavit limit paměti?

- **Stabilita:** Zabrání pádům kvůli nedostatku paměti při zpracování obrovských obrázků.  
- **Spolupráce:** Umožní ostatním aplikacím náročným na GPU (např. TensorFlow modely) běžet současně.  
- **Předvídatelnost:** Zajistí opakovatelnost testování výkonu, protože GPU nebude začínat swapovat.

Pokud `MemoryLimitMb` vynecháte, Aspose alokuje tolik, kolik považuje za nutné – což může být v pořádku na dedikovaném inference serveru, ale riskantní na vývojářském notebooku.

## Krok 3: Načtení obrázku pro OCR

Načtení správného formátu souboru je další klíčový krok. Metoda `OcrImage.FromFile` automaticky detekuje typ obrázku, ale stále byste měli ověřit, že soubor existuje a že jde o podporovanou variantu TIFF (např. LZW‑komprimovaný nebo CCITT‑G4).

```csharp
        // Step 3: Load the high‑resolution image to be processed
        var imagePath = "YOUR_DIRECTORY/large_photo.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            System.Console.WriteLine($"Error: File not found -> {imagePath}");
            return;
        }

        var image = OcrImage.FromFile(imagePath);
```

### Zpracování více‑stránkových TIFFů

Pokud váš TIFF obsahuje několik stránek, Aspose OCR ve výchozím nastavení načte jen první. Pro zpracování všech stránek můžete iterovat přes `image.Pages` (k dispozici v novějších verzích SDK) a každou stránku předat enginu zvlášť.

```csharp
        foreach (var page in image.Pages)
        {
            var result = ocrEngine.Recognize(page);
            System.Console.WriteLine($"--- Page {page.Index + 1} ---");
            System.Console.WriteLine(result.Text);
        }
        return; // Skip the single‑image path below
```

Ukázkový úryvek výše představuje **načtení obrázku pro OCR** vzor, který funguje jak pro jednostránkové, tak pro více‑stránkové soubory.

## Krok 4: Rozpoznání textu z TIF (nebo libovolného rastrového formátu)

Jakmile je obrázek v paměti, požádáme Aspose, aby udělal své kouzlo. Metoda `Recognize` vrací `OcrResult`, který obsahuje čistý text, skóre důvěry a dokonce i informace o ohraničujících rámečcích, pokud je potřebujete.

```csharp
        // Step 4: Perform OCR recognition on the image
        var ocrResult = ocrEngine.Recognize(image);
```

### Proč to funguje dobře s TIF

- **Bezeztrátová komprese:** TIFF často ukládá surová pixelová data, což dává OCR enginu nejvyšší věrnost.  
- **Různé barevné prostory:** Aspose zvládne grayscale, RGB i CMYK TIFFy bez nutnosti další konverze.

Pokud potřebujete nastavit jazykové balíčky (např. francouzštinu nebo japonštinu), nastavte `ocrEngine.Settings.Language = "fr"` před voláním `Recognize`.

## Krok 5: Zobrazení rozpoznaného textu

Nakonec vypíšeme text do konzole. Ve skutečné aplikaci byste ho možná uložili do databáze, JSON souboru nebo předali dál do NLP pipeline.

```csharp
        // Step 5: Display the recognized text
        System.Console.WriteLine("=== OCR Output ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Očekávaný výstup

Spuštění programu na čistém, 300 dpi skenu tištěné stránky obvykle vrátí něco jako:

```
=== OCR Output ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
...
```

Pokud je obrázek rozmazaný nebo je limit paměti GPU nastaven příliš nízko, můžete vidět poškozené znaky nebo zkrácený výsledek. Snížení `MemoryLimitMb` pod velikost obrázku (často ~1 GB pro 6000×8000 pixelový TIFF) může způsobit automatické přepnutí na CPU.

## Kompletní funkční příklad

Níže je kompletní, připravený k spuštění program. Zkopírujte jej do nového Console App projektu, nahraďte `YOUR_DIRECTORY/large_photo.tif` cestou k vašemu TIFF souboru a stiskněte **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration and set a memory cap
        ocrEngine.Settings.Gpu = new GpuSettings
        {
            Enable = true,
            DeviceId = 0,
            MemoryLimitMb = 2048 // 2 GB limit – adjust to your GPU size
        };

        // Step 3: Load the image (ensure the file exists)
        var imagePath = "YOUR_DIRECTORY/large_photo.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            System.Console.WriteLine($"Error: File not found -> {imagePath}");
            return;
        }

        var image = OcrImage.FromFile(imagePath);

        // Step 4: Perform OCR on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 5: Output the recognized text
        System.Console.WriteLine("=== OCR Output ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Rychlý kontrolní seznam

- ✅ **Aspose OCR C# příklad** zkompilován bez chyb.  
- ✅ **GPU povoleno** (`Enable = true`).  
- ✅ **Limit paměti GPU** nastaven na 2048 MB.  
- ✅ **Obrázek načten** z TIF souboru.  
- ✅ **Text rozpoznán** a vytištěn.

## Časté problémy a jak se jim vyhnout

| Příznak | Pravděpodobná příčina | Oprava |
|---------|-----------------------|--------|
| `System.DllNotFoundException: cudart64_110.dll` | CUDA runtime není nainstalován nebo verze nesedí. | Nainstalujte CUDA 11.x (nebo 12.x) odpovídající vašemu driveru. |
| OCR vrací prázdný řetězec | Obrázek je příliš tmavý nebo DPI < 150. | Předzpracujte pomocí `image.AdjustContrast()` nebo převeďte na 300 dpi. |
| Pád kvůli nedostatku paměti na GPU | `MemoryLimitMb` je příliš nízký pro daný obrázek. | Zvyšte limit nebo rozdělte obrázek na dlaždice pomocí `image.Crop`. |
| Chyba `Unsupported image format` | TIFF používá exotickou kompresi (např. JPEG‑2000). | Před OCR konvertujte TIFF do podporovaného formátu pomocí ImageMagick. |

## Rozšíření demo

Nyní, když máte solidní **aspose ocr c# příklad**, můžete zkusit:

- **Dávkové zpracování:** Procházet složku s TIFy a výsledek ukládat do `.txt` souboru.  
- **Jazykové balíčky:** `ocrEngine.Settings.Language = "es"` pro španělštinu nebo načíst vlastní slovníky.  
- **Ohraničující rámečky:** Použít `ocrResult.Regions` k získání souřadnic pro každé slovo — užitečné např. pro nástroje na redakci.  
- **Přepnutí na CPU:** Obalit GPU blok do `try/catch`; při selhání nastavit `ocrEngine.Settings.Gpu.Enable = false` a zopakovat.

Tyto rozšíření zachovávají základní vzor, ale přidávají hodnotu pro specifické použití.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční kódové příklady s podrobným krok‑za‑krokem vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Extrahovat text z obrázku pomocí Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extrahovat text z obrázku – optimalizace OCR s Aspose.OCR pro .NET](/ocr/english/net/ocr-optimization/)
- [Extrahovat text z obrázku v C# s výběrem jazyka pomocí Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}