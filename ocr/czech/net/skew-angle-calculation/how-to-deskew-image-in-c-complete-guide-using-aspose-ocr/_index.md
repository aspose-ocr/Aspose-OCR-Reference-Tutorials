---
category: general
date: 2026-03-21
description: Naučte se, jak vyrovnat zkosené obrázky a rozpoznat text na obrázku pomocí
  Aspose OCR. Převádějte JPG na text a opravujte rotaci obrázku v několika řádcích
  kódu C#.
draft: false
keywords:
- how to deskew image
- recognize text image
- convert jpg to text
- correct image rotation
- recognize text jpg
language: cs
og_description: Jak vyrovnat zkosení obrazu a extrahovat text z JPEG pomocí Aspose
  OCR. Postupujte podle tohoto krok‑za‑krokem průvodce, abyste převáděli jpg na text
  a opravili rotaci obrazu.
og_title: Jak vyrovnat zkosení obrázku v C# – Rychlý tutoriál Aspose OCR
tags:
- OCR
- C#
- Aspose
title: Jak vyrovnat zkosení obrázku v C# – Kompletní průvodce s využitím Aspose OCR
url: /cs/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-guide-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak narovnat obrázek v C# – Kompletní průvodce s použitím Aspose OCR

Už jste se někdy zamýšleli **jak narovnat obrázek** soubory, které vyšli ze skeneru nakloněné pod podivným úhlem? Nejste v tom sami – mnoho vývojářů narazí na tento problém, když se snaží extrahovat text z účtenek, faktur nebo ručně psaných poznámek. Dobrou zprávou je, že s Aspose OCR můžete opravit otočení obrázku a získat čistý, prohledávatelný text během několika řádků.

V tomto tutoriálu projdeme celý proces: od instalace knihovny, povolení automatického narovnání, po rozpoznání textu na obrázku a nakonec konverzi JPG na text. Na konci budete mít připravenou konzolovou aplikaci, která **rozpozná text jpg** soubory bez nutnosti je nejprve ručně otáčet.

## Co budete potřebovat

- **.NET 6.0** nebo novější (kód funguje jak na .NET Core, tak na .NET Framework)  
- **Aspose.OCR for .NET** NuGet balíček – doporučena verze 23.12 nebo novější  
- Ukázkový **skewed JPEG** (např. `skewed_receipt.jpg`) umístěný na místě, kde ho aplikace může číst  
- Visual Studio, VS Code nebo jakýkoli C# editor, který preferujete  

Žádné další nástroje třetích stran nejsou potřeba. Knihovna interně provádí narovnání, OCR a dokonce i detekci jazyka.

![jak narovnat obrázek příklad](/images/deskew-example.png "jak narovnat obrázek pomocí Aspose OCR")

## Krok 1: Nastavení projektu a instalace Aspose.OCR

Aby vše bylo přehledné, vytvořte nový konzolový projekt:

```bash
dotnet new console -n DeskewDemo
cd DeskewDemo
dotnet add package Aspose.OCR --version 23.12.0
```

Řádek `dotnet add package` stáhne binárky **Aspose.OCR** a všechny nativní závislosti. Pokud používáte Windows, nativní DLL soubory se nainstalují automaticky; na Linuxu/macOS můžete potřebovat balíček `libgdiplus`, ale jde o jednorázovou instalaci.

## Krok 2: Povolení automatického narovnání (oprava otočení obrázku)

Nyní otevřete `Program.cs` a nahraďte jeho obsah kódem níže. Klíčový řádek je `ocrEngine.Settings.Deskew = true;` – to je příznak, který říká enginu, **jak narovnat obrázek** automaticky.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create an OCR engine (CPU mode is fine for most desktop apps)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------------
            // 2️⃣ Turn on deskewing – this corrects image rotation for us
            // ---------------------------------------------------------------
            ocrEngine.Settings.Deskew = true;   // <-- how to deskew image is handled here

            // ---------------------------------------------------------------
            // 3️⃣ Point the engine at the JPEG you want to process
            // ---------------------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/skewed_receipt.jpg";

            // ---------------------------------------------------------------
            // 4️⃣ Run OCR – the result already contains the corrected text
            // ---------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(imagePath);

            // ---------------------------------------------------------------
            // 5️⃣ Output the text – this is your “convert jpg to text” step
            // ---------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Proč povolit narovnání?

Když skener podává stránku pod úhlem, základní linie textu je nakloněná. Tradiční OCR enginy by četly každý znak jako nakloněnou verzi, což výrazně snižuje přesnost. Nastavením `Deskew = true` Aspose OCR pod pokličkou spustí rychlou Hough‑transformaci, otočí bitmapu zpět do vodorovné polohy a poté provede rozpoznání. Výsledek je stejný, jako kdybyste obrázek ručně otočili ve Photoshopu – jen rychlejší a plně automatizovaný.

## Krok 3: Rozpoznání textu na obrázku a konverze JPG na text

Volání `Recognize` provádí dvě věci najednou:

1. **Narovná** obrázek (protože jsme zapnuli příznak).  
2. **Extrahuje** textový obsah a vrací jej v objektu `OcrResult`.

Můžete zacházet s `ocrResult.Text` jako s obyčejným řetězcem, zapsat jej do souboru nebo předat do následných zpracovatelských pipeline. Pokud potřebujete surové skóre důvěry pro každé slovo, `ocrResult.Words` poskytuje kolekci s hodnotami `Confidence`.

### Příklad výstupu

Předpokládejme, že `skewed_receipt.jpg` obsahuje jednoduchou účtenku, můžete vidět něco jako:

```
=== Recognized Text ===
Store: Coffee Corner
Date: 2026-03-20
Item   Qty   Price
Latte   2    5.00
Bagel   1    2.50
Total          12.50
```

Všimněte si, jak se čísla pěkně zarovnají i přes to, že původní obrázek byl otočen přibližně o 7°. To je kouzlo **správné rotace obrázku**, které je v knihovně zabudováno.

## Krok 4: Spuštění příkladu a ověření výsledků

Zkompilujte a spusťte:

```bash
dotnet run
```

Pokud je vše správně nastaveno, uvidíte extrahovaný text vytištěný v konzoli. Pokud dostanete výjimku jako `FileNotFoundException`, zkontrolujte cestu k vašemu JPEG souboru a ujistěte se, že je čitelný.

### Časté úskalí a tipy pro profesionály

- **Velké obrázky** – Paměťová náročnost OCR roste s rozměry obrázku. Před předáním enginu změňte velikost příliš velkých souborů (např. > 3000 px šířka).  
- **Není‑latinské skripty** – Ve výchozím nastavení engine předpokládá angličtinu. Nastavte `ocrEngine.Settings.Language = OcrLanguage.French;` (nebo jakýkoli podporovaný jazyk), pokud potřebujete **rozpoznat text na obrázku** v jiných abecedách.  
- **Dávkové zpracování** – Pro mnoho souborů znovu použijte stejnou instanci `OcrEngine`; vytváření nového enginu pro každý soubor přináší zbytečnou režii.  
- **Kontrola kvality** – Po narovnání můžete exportovat opravenou bitmapu pomocí `ocrEngine.Settings.DeskewedImage.Save("corrected.jpg");` a vizuálně ověřit opravu rotace.

## Kompletní funkční příklad (vše dohromady)

Níže je kompletní, samostatný program, který můžete zkopírovat a vložit do `Program.cs`. Obsahuje komentáře, ošetření chyb a volitelný krok pro uložení narovnaného obrázku.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the input JPEG – change this to your actual file location
            string inputPath = @"YOUR_DIRECTORY\skewed_receipt.jpg";

            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: File not found – {inputPath}");
                return;
            }

            try
            {
                // 1️⃣ Create OCR engine (CPU mode is sufficient for most scenarios)
                var ocrEngine = new OcrEngine();

                // 2️⃣ Enable automatic deskewing – this is the core of how to deskew image
                ocrEngine.Settings.Deskew = true;

                // Optional: Save the corrected image to verify the rotation fix
                // ocrEngine.Settings.DeskewedImagePath = "corrected.jpg";

                // 3️⃣ Perform OCR – this simultaneously deskews and extracts text
                OcrResult result = ocrEngine.Recognize(inputPath);

                // 4️⃣ Output the recognized text – effectively convert jpg to text
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine("An unexpected error occurred:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

Spuštěním programu **rozpozná text jpg** soubory, automaticky opraví jakýkoli sklon a vytiskne čistý, prohledávatelný text do konzole.

## Závěr

Nyní máte solidní, připravený k nasazení úryvek, který ukazuje **jak narovnat obrázek** soubory a extrahovat jejich obsah pomocí Aspose OCR. Přístup funguje pro účtenky, faktury, naskenované smlouvy nebo jakýkoli JPEG, kde text není dokonale vodorovný.

Další kroky, které můžete prozkoumat:

- **Dávkové zpracování** složky s JPEGy a zápis každého výsledku do souboru `.txt` (navazuje na *konverzi jpg na text*).  
- Integrace OCR kroku do ASP.NET Core API, aby klienti mohli nahrávat obrázky a získávat text ve formátu JSON.  
- Experimentování s různými OCR nastaveními, jako `ocrEngine.Settings.Language` nebo `ocrEngine.Settings.RecognitionMode`, pro zlepšení přesnosti u dokumentů v jiných jazycích než angličtině.  

Vyzkoušejte to, upravte nastavení a nechte engine udělat těžkou práci. Jako vždy, pokud narazíte na problém nebo máte chytrou optimalizaci, podělte se o ni v komentáři níže. Šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}