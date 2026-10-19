---
category: general
date: 2026-01-10
description: Naučte se rozpoznávat text z obrázku, extrahovat souřadnice textu a převádět
  účtenku do JSON pomocí Aspose OCR v C#. Krok za krokem tutoriál.
draft: false
keywords:
- recognize text from image
- how to extract text
- extract text coordinates
- convert receipt to json
language: cs
og_description: Rozpoznávejte text z obrázku v C# pomocí Aspose OCR. Tento průvodce
  ukazuje, jak extrahovat text, získat souřadnice a převést účtenku do JSON.
og_title: Rozpoznat text z obrázku – Kompletní C# OCR tutoriál
tags:
- OCR
- C#
- Aspose
title: Rozpoznání textu z obrázku v C# – Kompletní průvodce OCR a JSON
url: /cs/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznání textu z obrázku – Kompletní C# OCR tutoriál

Už jste někdy potřebovali rozpoznat text z obrázku, ale nebyli jste si jisti, kterou knihovnu zvolit? Nejste v tom sami. V mnoha reálných aplikacích—sledovačích výdajů, skenerů účtenek nebo archivátorech dokumentů—je spolehlivé získání textu první překážkou.

V tomto tutoriálu vás provedeme **jak extrahovat text**, získáme jeho ohraničující rámečky a nakonec **převod účtenky do JSON** pomocí Aspose.OCR pro .NET. Na konci budete mít samostatný C# projekt, který vezme fotografii účtenky a vytvoří úhledný JSON soubor s hodnotami důvěry a souřadnicemi.

## Co budete potřebovat

- **.NET 6.0 SDK** (nebo jakákoli novější verze). Starší frameworky také fungují, ale .NET 6 je ideální pro moderní knihovny.
- **Visual Studio 2022** nebo VS Code s rozšířením C#.
- **Aspose.OCR for .NET** NuGet balíček (`Aspose.OCR` a `Aspose.OCR.Output`). Můžete jej nainstalovat pomocí Package Manager Console:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Output
```

- Ukázkový obrázek účtenky (např. `receipt.jpg`) umístěný ve složce, na kterou budete později odkazovat.

To je vše—žádné další SDK, žádné nativní binární soubory, jen čistý spravovaný kód.

## Krok 1: Vytvořte nový konzolový projekt

Nejprve vytvořte konzolovou aplikaci. Je to nejrychlejší způsob, jak otestovat OCR bez UI režie.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later.
        }
    }
}
```

> **Tip:** Udržujte složku projektu přehlednou; vytvořte podsložku `Resources` a vložte tam `receipt.jpg`. Zjednoduší to práci s cestami.

## Krok 2: Načtěte obrázek účtenky

Nyní skutečně **rozpoznáváme text z obrázku**. Prvním krokem je nasměrovat OCR engine na soubor.

```csharp
// Inside Main()
string imagePath = @"Resources/receipt.jpg";
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Image = ImageStream.FromFile(imagePath)
};

Console.WriteLine("✅ Image loaded successfully.");
```

Proč obalujeme načítání jednoduchou kontrolou existence? Protože ve výrobě často pracujete s nahrávkami od uživatelů, které mohou chybět nebo být poškozené. Zachycení problému brzy vás ochrání před kryptickými výjimkami později.

## Krok 3: Proveďte OCR – **rozpoznání textu z obrázku**

S obrázkem v paměti požádáme Aspose, aby **rozpoznal text z obrázku**. Tato operace je synchronní a vrací bohatý výsledek.

```csharp
// Still inside Main()
try
{
    ocrEngine.Recognize();
    Console.WriteLine("🧠 OCR completed.");
}
catch (Exception ex)
{
    Console.WriteLine($"❗ OCR failed: {ex.Message}");
    return;
}
```

Za scénou Aspose spouští neuronovou síť trénovanou na milionech znaků. Engine naplní `ocrEngine.Text`, `ocrEngine.RecognitionResult` a kolekci objektů `OcrRegion`, které obsahují souřadnice. To je přesně to, co potřebujeme pro další krok.

## Krok 4: **Jak extrahovat text** – Získání surového řetězce

Pokud vás zajímá jen čistý text (např. pro rychlé vyhledávání), můžete jej získat přímo z engine:

```csharp
string plainText = ocrEngine.Text;
Console.WriteLine("\n--- Extracted Text ---");
Console.WriteLine(plainText);
```

Všimnete si zalomení řádků tam, kde OCR detekovalo hranice odstavců. V mnoha scénářích skenování účtenek je surový řetězec dostačující k získání částek, dat nebo názvů prodejců pomocí jednoduchých regexů.

## Krok 5: **extrahovat souřadnice textu** – Ohraničující rámečky pro každé slovo

Často potřebujete vědět, *kde* na obrázku se konkrétní text nachází—např. pro zvýraznění celkové částky v UI. Aspose nám to poskytuje pomocí objektů `OcrRegion`.

```csharp
Console.WriteLine("\n--- Text Coordinates (extract text coordinates) ---");
foreach (var region in ocrEngine.RecognitionResult.Regions)
{
    // Each region represents a word or a line depending on the engine settings.
    string word = region.Text;
    var bounds = region.BoundingBox; // X, Y, Width, Height
    Console.WriteLine($"Word: \"{word}\" | Box: X={bounds.X}, Y={bounds.Y}, W={bounds.Width}, H={bounds.Height}");
}
```

Všimněte si, že procházíme **extrahování souřadnic textu** pro každý rozpoznaný segment. Souřadnice jsou relativní k původnímu obrázku, takže je můžete překrýt v grafickém plátně nebo v HTML elementu `<canvas>`.

## Krok 6: **převod účtenky do JSON** – Ukládání podrobných výsledků

Nyní přichází část, která spojuje vše dohromady: chceme strojově čitelnou strukturu, která zahrnuje text, skóre důvěry a ohraničující rámečky. Aspose poskytuje `JsonSaveOptions`, které to usnadňují.

```csharp
// Define where the JSON will be saved
string jsonPath = @"Resources/receipt.json";

// Configure JSON options to keep confidence and bounding boxes
JsonSaveOptions jsonOptions = new JsonSaveOptions
{
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};

// Save the OCR result
ocrEngine.Save(jsonPath, jsonOptions);
Console.WriteLine($"\n💾 Detailed OCR results saved to {jsonPath}");
```

Výsledný soubor vypadá zhruba takto (zkráceně):

```json
{
  "Regions": [
    {
      "Text": "Store",
      "Confidence": 0.99,
      "BoundingBox": { "X": 45, "Y": 120, "Width": 80, "Height": 20 }
    },
    {
      "Text": "Total",
      "Confidence": 0.97,
      "BoundingBox": { "X": 300, "Y": 560, "Width": 70, "Height": 22 }
    }
    // ... more regions ...
  ]
}
```

Nyní máte artefakt **převodu účtenky do JSON**, který můžete předat downstream službám—např. API pro výdajové zprávy, analytické pipeline nebo i jednoduché UI, které kreslí obdélníky kolem každého slova.

## Kompletní funkční příklad

Spojením všech částí dohromady získáte kompletní `Program.cs`, který můžete zkopírovat do svého projektu:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image
            // -------------------------------------------------
            string imagePath = @"Resources/receipt.jpg";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            OcrEngine ocrEngine = new OcrEngine
            {
                Image = ImageStream.FromFile(imagePath)
            };
            Console.WriteLine("✅ Image loaded.");

            // -------------------------------------------------
            // 2️⃣ Run OCR – recognize text from image
            // -------------------------------------------------
            try
            {
                ocrEngine.Recognize();
                Console.WriteLine("🧠 OCR completed.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❗ OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 3️⃣ Extract plain text (how to extract text)
            // -------------------------------------------------
            Console.WriteLine("\n--- Extracted Text ---");
            Console.WriteLine(ocrEngine.Text);

            // -------------------------------------------------
            // 4️⃣ Get coordinates (extract text coordinates)
            // -------------------------------------------------
            Console.WriteLine("\n--- Text Coordinates ---");
            foreach (var region in ocrEngine.RecognitionResult.Regions)
            {
                var box = region.BoundingBox;
                Console.WriteLine($"Word: \"{region.Text}\" | Box: X={box.X}, Y={box.Y}, W={box.Width}, H={box.Height}");
            }

            // -------------------------------------------------
            // 5️⃣ Save detailed JSON (convert receipt to json)
            // -------------------------------------------------
            string jsonPath = @"Resources/receipt.json";
            JsonSaveOptions jsonOptions = new JsonSaveOptions
            {
                IncludeConfidence = true,
                IncludeBoundingBoxes = true
            };
            ocrEngine.Save(jsonPath, jsonOptions);
            Console.WriteLine($"\n💾 JSON saved at {jsonPath}");
        }
    }
}
```

Spusťte program (`dotnet run`) a sledujte výstup v konzoli. Otevřete `Resources/receipt.json` a ověřte strukturu.

## Časté otázky a okrajové případy

- **Co když je obrázek rozmazaný?**  
  Aspose OCR funguje nejlépe při 300 dpi nebo vyšším. Pokud získáte nízké skóre důvěry, zvažte aplikaci ostření před předáním obrázku engine.

- **Mohu rozpoznávat více jazyků?**  
  Ano. Nastavte `ocrEngine.Language = Language.English | Language.Spanish;` před voláním `Recognize()`.

- **Jak omezím výstup jen na čísla (např. částky)?**  
  Po získání čistého textu spusťte regex jako `\d+\.\d{2}` na `ocrEngine.Text`. Protože již máme souřadnice, můžete mapovat nalezený řetězec zpět na jeho oblast pro vizuální zvýraznění.

- **Je formát JSON přizpůsobitelný?**  
  Třída `JsonSaveOptions` poskytuje několik příznaků. Pokud potřebujete zcela vlastní schéma, můžete iterovat přes `ocrEngine.RecognitionResult.Regions` a serializovat objekty sami pomocí `System.Text.Json`.

## Závěr

Právě jsme ukázali, jak **rozpoznat text z obrázku** v C# pomocí Aspose.OCR, **jak extrahovat text**, získat **souřadnice extrahovaného textu** a nakonec **převést účtenku do JSON**. Celý proces běží v jediné, snadno spustitelné konzolové aplikaci, což je ideální pro prototypy nebo jako stavební blok ve větších systémech.

Další kroky? Zkuste předat JSON do front‑endu, který kreslí ohraničující rámečky, nebo zapojte výstup do služby pro výdajové zprávy. Můžete také experimentovat s různými formáty obrázků (PNG, TIFF) nebo hromadně zpracovat složku s účtenkami.

Máte další otázky ohledně OCR, Aspose nebo práce s JSON? Zanechte komentář níže a šťastné kódování! 

![Příklad obrázku účtenky pro rozpoznání textu z obrázku](receipt.jpg "Příklad obrázku účtenky")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}