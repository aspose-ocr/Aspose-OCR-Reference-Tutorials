---
category: general
date: 2026-02-22
description: Rozpoznat text z obrázku pomocí Aspose OCR v C#. Krok za krokem průvodce
  extrakcí textu z PNG, převodem obrázku na text a čtením vloženého zdroje v C# pro
  licencování.
draft: false
keywords:
- recognize text from image
- extract text from png
- convert image to text
- read embedded resource c#
- perform ocr on image
language: cs
og_description: Rozpoznávejte text z obrázku okamžitě pomocí Aspose OCR. Naučte se
  extrahovat text z PNG, převést obrázek na text a číst vložený zdroj v C# pro bezproblémové
  licencování.
og_title: Rozpoznat text z obrázku v C# – kompletní tutoriál Aspose OCR
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Rozpoznat text z obrázku v C# s Aspose OCR
url: /cs/net/text-recognition/recognize-text-from-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rozpoznání textu z obrázku v C# s Aspose OCR

Už jste někdy potřebovali **rozpoznat text z obrázku**, ale nebyli jste si jisti, kde začít v C#? Nejste sami — většina vývojářů narazí na stejnou překážku, když poprvé potkají OCR. V tomto tutoriálu se ponoříme přímo do funkčního řešení, které vám umožní **extrahovat text z png**, **převést obrázek na text** a dokonce **číst vložený zdroj c#** pro licencování bez potíží.  

Probereme vše od načtení vložené licence Aspose OCR až po vytištění výsledného řetězce na konzoli. Na konci budete mít samostatný program, který můžete vložit do libovolného .NET projektu a spustit ještě dnes.

## Co budete potřebovat

- **.NET 6+** (kód se také kompiluje na .NET Framework, ale .NET 6 je aktuální LTS)
- **Aspose.OCR for .NET** NuGet balíček (verze 23.9 nebo novější)
- **sample PNG** obrázek obsahující čistý, tištěný anglický text
- **Aspose OCR license file** (`Aspose.OCR.lic`) přidaný do vašeho projektu jako *Embedded Resource*  

Pokud vám některý z nich není znám, nebojte se — každý krok níže vysvětluje, jak jej nastavit.

## Krok 1: Načtení vložené licence C# (Embedded Resource)

Než OCR engine může pracovat, Aspose potřebuje platnou licenci. Uložení souboru `.lic` jako vloženého zdroje ho drží mimo zdrojový strom a usnadňuje nasazení.

```csharp
using System;
using System.Reflection;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Load the embedded Aspose OCR license
        // ------------------------------------------------------------
        var assembly = Assembly.GetExecutingAssembly();

        // The resource name follows the folder hierarchy in the project.
        // Adjust "MyApp.Resources.Aspose.OCR.lic" if yours differs.
        using (var licenseStream = assembly.GetManifestResourceStream(
               "MyApp.Resources.Aspose.OCR.lic"))
        {
            if (licenseStream == null)
            {
                Console.Error.WriteLine(
                    "License file not found. Make sure it's marked as Embedded Resource.");
                return;
            }

            var license = new License();
            license.SetLicenseFromStream(licenseStream);
        }

        // Continue with OCR steps...
```

**Proč je to důležité:**  
Vložení licence zabraňuje náhodnému odhalení ve verzovacím systému a zaručuje, že soubor cestuje s kompilovanou DLL. Pokud je stream `null`, program se ukončí brzy — toto je naše první obranná kontrola.

## Krok 2: Inicializace OCR engine (provedení OCR na obrázku)

Jakmile je licence načtena, můžeme vytvořit instanci `OcrEngine`. Nastavíme jazyk na angličtinu, protože takový jazyk používá náš ukázkový PNG.

```csharp
        // ------------------------------------------------------------
        // 2️⃣ Initialise the OCR engine – this is where we perform OCR on image
        // ------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = Language.English   // change to Language.French etc. if needed
        };
```

**Tip:** Enum `Language` podporuje více než 30 jazyků. Přepnutí je tak jednoduché jako `Language.Spanish`. Pokud někdy potřebujete detekci více jazyků, vytvořte samostatné enginy nebo použijte `ocrEngine.AutoDetectLanguage = true` (k dispozici v novějších verzích Aspose).

## Krok 3: Načtení PNG obrázku (extrahování textu z PNG)

Aspose OCR pracuje s vlastní třídou `Image`, nikoli s `System.Drawing.Image`. Ukážete mu cestu k souboru, nebo mu předáte `Stream`, pokud dáváte přednost.

```csharp
        // ------------------------------------------------------------
        // 3️⃣ Load the image – this is the step where we extract text from png
        // ------------------------------------------------------------
        const string imagePath = "YOUR_DIRECTORY/sample.png";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Image not found at {imagePath}");
            return;
        }

        var image = Image.Load(imagePath);
```

**Hraniční případ:** Pokud váš PNG obsahuje alfa kanál (průhledné pozadí), Aspose může špatně interpretovat prázdný prostor. Rychlé řešení je předzpracovat obrázek pomocí `ImageProcessor` a zploštit jej, ale pro většinu skenovaných dokumentů výchozí načítač funguje dobře.

## Krok 4: Spuštění rozpoznání (převod obrázku na text)

S připraveným enginem a obrázkem je samotné volání OCR jednou řádkou. Objekt výsledku vám poskytne surový řetězec a skóre důvěry.

```csharp
        // ------------------------------------------------------------
        // 4️⃣ Recognise the image – this is where we convert image to text
        // ------------------------------------------------------------
        var ocrResult = ocrEngine.Recognize(image);

        // Optional: check confidence (0‑100)
        Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
```

**Proč by vás mohla zajímat důvěra:**  
Nízká důvěra (např. < 70 %) obvykle signalizuje rozmazaný sken nebo nepodporované písmo. V produkci můžete přejít na jiný OCR engine nebo požádat uživatele o opětovné skenování.

## Krok 5: Výstup rozpoznaného textu

Nakonec vytiskněte extrahovaný řetězec. Ve skutečné aplikaci jej můžete zapsat do databáze, JSON souboru nebo poslat do vyhledávacího indexu.

```csharp
        // ------------------------------------------------------------
        // 5️⃣ Output the recognised text – the final result of recognize text from image
        // ------------------------------------------------------------
        Console.WriteLine("\n--- Recognised Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Očekávaný výstup v konzoli

```
Confidence: 96%
--- Recognised Text ---
Hello, world!
This is a sample PNG used for OCR testing.
```

Pokud vidíte výše uvedený text (nebo něco podobného), gratulujeme — úspěšně jste **rozpoznali text z obrázku** pomocí Aspose OCR!

## Časté úskalí a jak se jim vyhnout

| Příznak | Pravděpodobná příčina | Oprava |
|---------|-----------------------|--------|
| `License not set` výjimka | Licenční soubor není vložený nebo je špatný název zdroje | Ověřte `Build Action = Embedded Resource` a dvakrát zkontrolujte plně kvalifikovaný název |
| Prázdný výstup | DPI obrázku je příliš nízké (méně než 150) | Převzorkujte PNG na alespoň 150 DPI před předáním Aspose |
| Poškozené znaky | Vybrán špatný jazyk | Nastavte `ocrEngine.Language` na správnou hodnotu enumu `Language` |
| `OutOfMemoryException` při velkých obrázcích | Přímé načtení obrovského PNG (10 MB+) | Použijte `Image.Load(stream, maxWidth: 2000, maxHeight: 2000)` pro okamžité zmenšení |

## Pro tip: Dávkové zpracování

Pokud potřebujete **rozpoznat text z obrázku** ve velkém množství souborů, zabalte hlavní logiku do smyčky `foreach` a znovu použijte stejnou instanci `OcrEngine`. Opakované používání engine ušetří několik milisekund na soubor, protože podkladové nativní knihovny zůstávají načtené.

```csharp
var images = System.IO.Directory.GetFiles("YOUR_DIRECTORY", "*.png");
foreach (var path in images)
{
    var img = Image.Load(path);
    var result = ocrEngine.Recognize(img);
    Console.WriteLine($"{path} → {result.Text.Trim()}");
}
```

## Další kroky

- **Doladit předzpracování** – vyzkoušejte `ImageProcessor` pro zlepšení kontrastu nebo odstranění šumu.  
- **Prozkoumat další výstupní formáty** – `ocrResult.GetWords()` poskytuje ohraničující rámečky, užitečné pro zvýraznění textu v UI.  
- **Kombinovat s Azure Cognitive Services**, pokud potřebujete cloudovou podporu pro ručně psaný text.  

Všechny tyto rozšíření stále používají stejný základní vzor: načíst licenci, vytvořit engine, předat obrázek a přečíst text.

![Screenshot of console showing recognized text from image](/images/ocr-result.png "recognize text from image result screenshot")

## Závěr

Prošli jsme kompletním, připraveným pro produkci příkladem, který ukazuje, jak **rozpoznat text z obrázku** v C# pomocí Aspose OCR. Od načtení vloženého zdroje pro licencování po načtení PNG, provedení OCR a vytištění výsledku, je pokryta každá část.  

Nyní můžete **extrahovat text z png**, **převést obrázek na text** a dokonce **číst vložený zdroj c#** pro licencování — vše během několika desítek řádků kódu. Klidně experimentujte s různými jazyky, většími dávkami obrázků nebo integrujte výstup do vlastní pipeline pro zpracování dokumentů. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}