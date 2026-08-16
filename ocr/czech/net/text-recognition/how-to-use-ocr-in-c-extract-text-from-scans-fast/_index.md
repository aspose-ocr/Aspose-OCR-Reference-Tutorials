---
category: general
date: 2026-03-13
description: Jak používat OCR v C# k extrakci textu ze skenů. Naučte se převádět TIFF
  na text pomocí Aspose OCR, akcelerace GPU a krok za krokem kódu.
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: cs
og_description: Jak použít OCR v C# k extrakci textu ze skenů. Tento průvodce vám
  ukáže, jak převést TIFF na text pomocí Aspose OCR a akcelerace GPU.
og_title: Jak použít OCR v C# – Rychle extrahovat text ze skenů
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Jak používat OCR v C# – Rychle extrahovat text ze skenů
url: /cs/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat OCR v C# – Rychle extrahovat text ze skenů

Už jste se někdy zamysleli **jak používat OCR** k získání čitelného textu ze zásobníku naskenovaných TIFF souborů? Nejste v tom sami. V mnoha reálných projektech—například digitalizace faktur, archivace historických dokumentů nebo jednoduše zpřístupnění PDF pro vyhledávání—potřebují vývojáři spolehlivý způsob, jak **extrahovat text ze skenů** bez zbytečného úsilí.

Dobrá zpráva? S Aspose OCR a několika řádky C# můžete převést TIFF na text během několika sekund, i na skromném pracovním stanovišti. Níže najdete kompletní, připravený příklad, plus vysvětlení každého rozhodnutí, abyste jej mohli přizpůsobit svému workflow.

## Co budete potřebovat

| Předpoklad | Proč je to důležité |
|--------------|----------------|
| .NET 6+ (or .NET Framework 4.7+) | Balíček Aspose OCR NuGet cílí na moderní .NET runtime. |
| Visual Studio 2022 (or any IDE you like) | Poskytuje vám IntelliSense a snadné ladění. |
| A CUDA‑compatible GPU & driver (optional) | Umožňuje `ocrEngine.UseGpu = true` pro znatelný nárůst rychlosti u velkých dávek. |
| A folder of TIFF images you want to process | Tento tutoriál používá soubory `*.tif`, ale můžete upravit vzor. |
| Aspose.OCR NuGet package (`Install-Package Aspose.OCR`) | Jádrová knihovna, která provádí těžkou práci. |

Pokud vám něco chybí, pořiďte si to hned—nemá smysl číst dál a pak narazit na chybějící závislost.

## Přehled řešení

Na vysoké úrovni program dělá tři věci:

1. **Vytvořit OCR engine** a volitelně zapnout akceleraci GPU.  
2. **Procházet každý TIFF soubor** v adresáři, spustit rozpoznání a zachytit vzniklý prostý text.  
3. **Zapsat text** do souboru `.txt` umístěného vedle původního obrázku.

A to je vše. Kód je úmyslně malý, přesto ukazuje osvědčené postupy jako explicitní výběr jazyka, správné uvolňování prostředků a ošetření chyb pro nejčastější okrajové případy.

![Příklad použití OCR v C#](/images/how-to-use-ocr-csharp.png "Ilustrace použití OCR v C# k extrahování textu ze skenů")

## Krok 1: Inicializace OCR Engine (Jak používat OCR)

Prvním, co potřebujete, je instance `OcrEngine`. Tento objekt je vstupní bránou ke všem funkcím Aspose OCR. Ve výchozím nastavení pracuje na CPU, ale nastavení `UseGpu = true` říká knihovně, aby těžké maticové výpočty přenesla na vaši grafickou kartu—za předpokladu, že máte nainstalovaný ovladač kompatibilní s CUDA.

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**Proč je to důležité:**  
- **GPU akcelerace** může zkrátit dobu zpracování až o 70 % u vysoce rozlišených skenů.  
- **Explicitní výběr jazyka** zabraňuje hádání enginu a zvyšuje přesnost, zejména u ne‑latinských skriptů.

## Krok 2: Nasměrujte engine na své skeny (Převod TIFF na text)

Dále řekneme programu, kde hledat obrázky. Použití `Directory.GetFiles` s filtrem `*.tif` udržuje logiku jednoduchou a zabraňuje načítání nesouvisejících souborů jako `.jpg` nebo `.png`.

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**Poznámka k okrajovému případu:** Pokud je adresář prázdný, smyčka níže se jednoduše nikdy neprovede, což je naprosto v pořádku. Později uvidíte přátelskou zprávu „No files found“.

## Krok 3: Zpracovat každý TIFF soubor (Extrahovat text ze skenů)

Nyní srdce programu: načítání každého obrázku, spuštění OCR a uložení výstupu. Pomocná metoda `ImageStream.FromFile` streamuje soubor přímo do paměti, což je efektivnější než nejprve načíst `Bitmap`.

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**Proč obalujeme každou iteraci do `try/catch`:**  
Skenování dávky dokumentů je nepořádné; poškozený TIFF nebo výpadek paměti by neměly přerušit celý běh. Blok catch zaznamená problém a pokračuje dál, čímž udržuje pipeline robustní.

### Očekávaný výstup

Pro každý `example.tif` najdete soubor `example.txt` vedle, který obsahuje něco jako:

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

Pokud OCR engine nedokáže přečíst řádek, jednoduše ponechá prázdnou řádku nebo zkreslený znak—nic nezhavaruje.

## Krok 4: Vyčištění a uvolnění (Nejlepší praxe)

`OcrEngine` implementuje `IDisposable`, takže je zdvořilé uvolnit nativní zdroje, když skončíte. V krátké konzolové aplikaci můžete spoléhat na GC, ale explicitní uvolnění je návyk, který stojí za to si osvojit.

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## Kompletní funkční příklad (připravený ke kopírování)

Níže je kompletní program, který můžete vložit do nového projektu Console App. Kompiluje se tak, jak je, za předpokladu, že jste přidali balíček Aspose.OCR NuGet.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### Rychlý kontrolní seznam

- **GPU příznak** – odstraňte nebo nastavte na `false`, pokud nemáte CUDA ovladač.  
- **Jazyk** – vyměňte `Language.English` za jakýkoli jiný podporovaný jazyk.  
- **Vzor souboru** – změňte `"*.tif"` na `"*.png"` nebo `"*.*"` pokud jsou vaše skeny v jiném formátu.  

## Časté úskalí a tipy (c# OCR tutoriál)

| Úskalí | Jak se mu vyhnout |
|---------|-----------------|
| **Chyby nedostatku paměti** při velkých dávkách | Zpracovávejte soubory v menších blocích nebo po každých 50 souborech zavolejte `GC.Collect()` (zřídka potřeba). |
| **GPU nebylo detekováno**, ale `UseGpu = true` | Engine tiše přepne na CPU, ale můžete po konstrukci zkontrolovat `ocrEngine.IsGpuAvailable`. |
| **Špatný jazykový balíček** vede k poškozenému výstupu | Vždy explicitně nastavte `ocrEngine.Language`; výchozí může být `Language.Unknown`. |
| **Cesta k souboru obsahuje Unicode znaky** | Použijte `Path.GetFullPath` pro normalizaci, nebo předřaďte `@"\\?\"` na Windows, pokud cesty překračují |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}