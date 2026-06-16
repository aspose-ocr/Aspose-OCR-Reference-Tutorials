---
category: general
date: 2026-02-24
description: Jak povolit GPU v příkladu Aspose OCR C# – rychle převést obrázek na
  prostý text. Obsahuje nastavení ID GPU zařízení a návod na čtení textu z obrázku
  v C#.
draft: false
keywords:
- how to enable gpu
- image to plain text
- aspose ocr example
- set gpu device id
- read image text c#
language: cs
og_description: Jak povolit GPU v příkladu Aspose OCR pro C#. Naučte se nastavit ID
  GPU zařízení a efektivně číst text z obrázku v C#.
og_title: Jak povolit GPU pro Aspose OCR v C# – Rychlý převod obrázku na prostý text
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Jak povolit GPU pro Aspose OCR v C# – Rychlý převod obrázku na prostý text
url: /cs/net/ocr-optimization/how-to-enable-gpu-for-aspose-ocr-in-c-fast-image-to-plain-te/
---

content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak povolit GPU pro Aspose OCR v C# – Rychlé převádění obrázku na prostý text

Už jste se někdy zamýšleli **jak povolit GPU** při používání Aspose OCR k převodu obrázku na editovatelný text? Nejste sami – mnoho vývojářů narazí na výkonovou bariéru při zpracování velkých faktur nebo naskenovaných smluv. Dobrá zpráva? Převod obrázku na prostý text může být bleskově rychlý, jakmile využijete svou grafickou kartu.

V tomto průvodci projdeme kompletním **příkladem Aspose OCR**, který vám přesně ukáže, jak povolit GPU, nastavit ID GPU zařízení a **číst text z obrázku v C#** stylu. Na konci budete mít spustitelný program, který extrahuje text z libovolného podporovaného obrázku během zlomku času, který by byl potřeba při přístupu pouze s CPU.

## Co budete potřebovat

- .NET 6.0 nebo novější (API funguje s .NET Core a .NET Framework)
- GPU kompatibilní s CUDA s nainstalovaným nejnovějším ovladačem
- Licence Aspose.OCR pro .NET (nebo bezplatná zkušební verze, která funguje pro vývoj)
- Visual Studio 2022 (nebo jakýkoli editor C#, který preferujete)

Žádné další NuGet balíčky kromě `Aspose.OCR` nejsou potřeba – stačí samotná knihovna.

---

## Krok 1 – Instalace NuGet balíčku Aspose OCR

Nejprve přidejte oficiální knihovnu Aspose OCR do svého projektu. Otevřete Package Manager Console a spusťte:

```powershell
Install-Package Aspose.OCR
```

Tím se stáhne `Aspose.OCR.dll` a všechny jeho závislosti. Pokud dáváte přednost GUI, klikněte pravým tlačítkem na projekt → **Manage NuGet Packages** → vyhledejte *Aspose.OCR* a klikněte na **Install**.  

*Pro tip:* Po instalaci ověřte, že se složka `Aspose.OCR` zobrazí pod **Dependencies** v Solution Exploreru.

---

## Krok 2 – Vytvoření jednoduché kostry konzolové aplikace

Vytvoříme malou konzolovou aplikaci, která demonstruje celý proces. Vytvořte nový projekt:

```bash
dotnet new console -n GpuOcrDemo
cd GpuOcrDemo
```

Nahraďte vygenerovaný soubor `Program.cs` kompletním kódem uvedeným níže. Tato kostra nám poskytuje čistý vstupní bod a umožňuje soustředit se na OCR logiku.

---

## Krok 3 – Jak povolit GPU a nastavit ID GPU zařízení

Nyní hvězda představení: **jak povolit GPU** v Aspose OCR. Knihovna poskytuje objekt `OcrSettings`, kde můžete přepnout `UseGpu` a volitelně vybrat konkrétní CUDA zařízení pomocí `GpuDeviceId`. Níže je přesný úryvek, který vložíte do svého programu:

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration – this is the crucial “how to enable gpu” step
        ocrEngine.Settings = new OcrSettings()
        {
            UseGpu = true,          // Turn on GPU processing
            GpuDeviceId = 0         // Optional: select the first CUDA‑compatible device
        };

        // 3️⃣ Recognise text from an image (any supported format)
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/large_invoice.png");

        // 4️⃣ Output the plain‑text result to the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Proč povolit GPU?

Povolení GPU přenáší těžkou práci – předzpracování pixelů, segmentaci znaků a inferenci neuronových sítí – na grafickou kartu. Na skromné GTX 1650 můžete zaznamenat **2‑3× zrychlení** oproti režimu pouze s CPU, zejména u dokumentů s vysokým rozlišením.

### Výběr ID zařízení

Pokud má váš počítač více GPU, `GpuDeviceId` vám umožní cílit na konkrétní. `0` vybere první zařízení; `1` by vybral druhé, atd. Dostupná ID můžete zjistit pomocí nástroje NVIDIA `nvidia-smi` nebo dotazováním třídy `GpuInfo` z Aspose (zde zkráceně nezobrazena).

---

## Krok 4 – Kompletní funkční příklad (připravený ke kopírování a vložení)

Níže je kompletní, připravený ke spuštění program. Vložte jej do `Program.cs`, nahraďte cestu k obrázku skutečným souborem na disku a stiskněte **F5**.

```csharp
// Program.cs – Complete Aspose OCR GPU example
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Validate the input argument (optional but handy)
            if (args.Length == 0)
            {
                Console.WriteLine("Usage: dotnet run <image_path>");
                return;
            }

            string imagePath = args[0];

            // Initialise the OCR engine
            var ocrEngine = new OcrEngine();

            // -------------------- How to Enable GPU --------------------
            // Turn on GPU acceleration and optionally pick a device
            ocrEngine.Settings = new OcrSettings()
            {
                UseGpu = true,          // Enables GPU processing
                GpuDeviceId = 0         // Selects the first CUDA‑compatible GPU
            };
            // ---------------------------------------------------------

            try
            {
                // Recognise the image – this is the “image to plain text” core
                var ocrResult = ocrEngine.RecognizeImage(imagePath);

                // Display the extracted text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Graceful error handling – helpful when the GPU is unavailable
                Console.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

### Očekávaný výstup

Pokud dodaný obrázek obsahuje řádek *„Invoice #12345 – Total $1,250.00“*, konzole vypíše:

```
=== Extracted Text ===
Invoice #12345 – Total $1,250.00
```

Výsledek je prostý text, připravený pro další zpracování (např. vložení do databáze nebo parseru přirozeného jazyka).

---

## Krok 5 – Ověření využití GPU (volitelné)

Aby bylo jisté, že GPU je skutečně používáno, otevřete nástroj pro sledování GPU (např. **NVIDIA‑Smi** nebo **GPU-Z**) během běhu programu. Měli byste vidět špičku ve využití výpočtů pro vybrané zařízení. Pokud vidíte jen aktivitu CPU, zkontrolujte:

- Ovladač GPU je aktuální.
- Příznak `UseGpu` je nastaven na `true`.
- Formát vašeho obrázku je podporován (PNG, JPEG, TIFF, atd.).

---

## Časté problémy a jak se jim vyhnout

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **GPU nebylo detekováno** | Zastaralý ovladač nebo chybějící CUDA runtime | Nainstalujte nejnovější NVIDIA driver a CUDA toolkit |
| **`Aspose.OCR` throws “GPU not supported”** | Běží na GPU bez CUDA (např. starší AMD) | Nastavte `UseGpu = false` nebo přepněte na kompatibilní GPU |
| **Nesprávná cesta k obrázku** | Relativní cesta ukazuje na špatnou složku | Použijte absolutní cestu nebo předávejte cestu jako argument příkazové řádky |
| **Licence nebyla použita** | Režim zkušební verze může omezovat využití GPU | Register a license with `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Rozšíření příkladu: Dávkové zpracování s GPU

Pokud potřebujete zpracovat desítky faktur, zabalte volání rozpoznání do smyčky. Protože GPU zůstává zahřáté, následné obrázky těží z **warm‑up cache**, což šetří další milisekundy u každého běhu.

```csharp
string[] files = Directory.GetFiles(@"C:\Invoices\", "*.png");
foreach (var file in files)
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Trim()}");
}
```

Pamatujte, že je třeba používat stejnou instanci `OcrEngine` – vytvoření nového enginu pro každý soubor by znovu inicializovalo GPU kontext a zničilo výkon.

---

## Závěr

Nyní máte solidní, end‑to‑end **příklad Aspose OCR**, který ukazuje **jak povolit GPU**, jak **nastavit ID GPU zařízení** a jak **číst text z obrázku v C#** stylu. Přepnutím `UseGpu` a nasměrováním na správné zařízení proměníte pomalý OCR úkol vázaný na CPU na vysoce výkonný pipeline, který zvládne velké faktury, účtenky nebo jakýkoli naskenovaný dokument.

Neváhejte experimentovat: vyzkoušejte různé formáty obrázků, upravte `GpuDeviceId` na systémech s více GPU, nebo kombinujte toto s dalšími knihovnami Aspose pro generování PDF. Jakmile je GPU v akci, možnosti jsou neomezené.

---

<img src="gpu-ocr.png" alt="jak povolit gpu s Aspose OCR v C# – rychle převést obrázek na prostý text">

*Šťastné programování! Pokud narazíte na problémy, zanechte komentář níže nebo navštivte oficiální fóra Aspose pro podrobnější informace.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}