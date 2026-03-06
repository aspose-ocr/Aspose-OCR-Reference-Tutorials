---
category: general
date: 2026-03-05
description: jak používat OCR v C# k extrakci textu z obrázků účtenek. Naučte se,
  jak načíst obrázek pro OCR a rozpoznat obrázek účtenky během několika minut.
draft: false
keywords:
- how to use OCR
- extract text from receipt
- load image for OCR
- recognize receipt image
language: cs
og_description: jak používat OCR v C# pro extrakci textu z účtenek. Postupujte podle
  tohoto krok‑za‑krokem průvodce, jak načíst obrázek pro OCR a efektivně rozpoznat
  obrázek účtenky.
og_title: Jak používat OCR v C# – Rychlé extrahování textu z účtenky
tags:
- OCR
- C#
- Aspose
- Receipt Processing
title: Jak používat OCR v C# – Rychle extrahovat text z účtenek
url: /cs/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-receipts-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít OCR v C# – rychle extrahovat text z účtenek

Už jste se někdy zamýšleli, **jak použít OCR** k získání dat přímo z fotografie nákupní účtenky? Nejste v tom sami. V mnoha aplikacích pro malé firmy je úzkým místem převod rozmazaného PNG do strukturovaného textu, se kterým můžete skutečně pracovat.  

Dobrá zpráva? Několika řádky C# a Aspose.OCR můžete **load image for OCR**, spustit engine a **recognize receipt image** během méně než minuty. Níže uvidíte kompletní, připravený příklad, plus tipy na obtížné části, které většina tutoriálů přeskočí.

## Co tento průvodce pokrývá

* Instalace balíčku Aspose.OCR NuGet.  
* Nastavení OCR enginu – jádro **jak použít OCR** správně.  
* Načtení souboru účtenky (to je krok **load image for OCR**).  
* Spuštění procesu rozpoznávání a získání jak JSON, tak XML dat o rozložení.  
* Řešení běžných problémů, jako jsou chybějící licence nebo nepodporované formáty obrázků.  

Na konci budete mít samostatný program, který extrahuje text z jakékoli účtenky, kterou vložíte do složky. Žádné externí služby, žádná skrytá magie.

## Požadavky

* .NET 6 SDK nebo novější (kód se také kompiluje s .NET Core).  
* Platný licenční soubor Aspose.OCR (`Aspose.OCR.lic`). Můžete získat bezplatnou zkušební verzi od Aspose, pokud ji ještě nemáte.  
* Ukázkový obrázek účtenky – `receipt.png` funguje dobře, ale jakýkoli běžný rastrový formát bude stačit.  

Pokud už to máte, skvělé – pojďme na to.

![příklad použití OCR](https://example.com/ocr-receipt.png "příklad použití OCR")

## Krok 1: Instalace Aspose.OCR a vytvoření nového projektu

Nejprve potřebujete knihovnu, která skutečně odlehčí těžkou práci. Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Tento příkaz vytvoří konzolovou aplikaci a stáhne nejnovější balíček Aspose.OCR. Z mé zkušenosti je lepší mít krátký název projektu, aby generované cesty byly přehlednější, zejména když začnete pracovat s více demo aplikacemi.

## Krok 2: Inicializace OCR enginu – jádro **jak použít OCR**

Nyní napíšeme kód, který odpovídá na otázku “**jak použít OCR** v C#”. Otevřete `Program.cs` a nahraďte jeho obsah úryvkem níže. Všimněte si komentářů – vysvětlují *proč* za každým řádkem, ne jen *co*.

```csharp
using System;
using System.IO;
using Aspose.OCR;          // Aspose OCR namespace
using Aspose.OCR.Image;   // For loading images

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create and configure the OCR engine.
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // Why set a license? Without it the engine runs in evaluation mode,
        // which adds a watermark to the output and limits batch size.
        ocrEngine.SetLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Load the receipt image – this is the **load image for OCR** step.
        // -------------------------------------------------
        // Change the path to point at your own receipt file.
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");

        // The ImageStream class abstracts file I/O and supports many formats.
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣ Run the recognition process – this is where we **recognize receipt image**.
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Export the layout information as JSON.
        // -------------------------------------------------
        string jsonResult = ocrResult.ToJson();
        File.WriteAllText("receipt.json", jsonResult);
        Console.WriteLine("✅ JSON saved to receipt.json");

        // -------------------------------------------------
        // 5️⃣ Export the same layout information as XML.
        // -------------------------------------------------
        string xmlResult = ocrResult.ToXml();
        File.WriteAllText("receipt.xml", xmlResult);
        Console.WriteLine("✅ XML saved to receipt.xml");

        // -------------------------------------------------
        // 6️⃣ Quick preview – print the plain text to console.
        // -------------------------------------------------
        Console.WriteLine("\n--- Extracted Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Proč to funguje

* **`OcrEngine`** je vstupní bod; obsahuje veškerou konfiguraci, kterou můžete později upravit (jazyk, DPI, atd.).  
* **`SetLicense`** odstraňuje vodotisk z hodnocení – klíčový krok, pokud plánujete distribuovat kód.  
* **`ImageStream.FromFile`** provádí **load image for OCR**, podporuje PNG, JPEG, BMP, TIFF a další.  
* **`Recognize()`** je metoda, která skutečně **recognize receipt image**. V pozadí provádí binarizaci, segmentaci a klasifikaci znaků.  
* Export do JSON a XML vám poskytne jak čitelný výstup pro člověka, tak strukturu vhodnou pro strojové zpracování, kterou můžete předat dalším parserům.

## Krok 3: Spusťte demo a ověřte výstup

Zkompilujte a spusťte:

```bash
dotnet run
```

Pokud je vše správně nastaveno, uvidíte něco jako:

```
✅ JSON saved to receipt.json
✅ XML saved to receipt.xml

--- Extracted Text ---
Walmart Supercenter
Date: 03/04/2026
Item    Qty   Price
Milk    2     2.58
Bread   1     1.99
Total   4.57
```

Konzole vypíše čistý text, zatímco `receipt.json` a `receipt.xml` obsahují podrobné informace o rozložení (souřadnice, skóre důvěryhodnosti atd.). Tyto soubory jsou užitečné, pokud později potřebujete mapovat jednotlivé řádky na databázová pole.

## Okrajové případy a profesionální tipy

### 1️⃣ Chybějící nebo neplatná licence
Pokud `SetLicense` selže, engine přejde do zkušebního režimu a ve výstupu se objeví vodotisk. Zabalte volání do try/catch a zalogujte přátelskou zprávu:

```csharp
try { ocrEngine.SetLicense("Aspose.OCR.lic"); }
catch (Exception ex)
{
    Console.WriteLine("⚠️ License not found – running in trial mode.");
    Console.WriteLine(ex.Message);
}
```

### 2️⃣ Nepodporované formáty obrázků
Aspose.OCR podporuje většinu rastrových formátů, ale pokud mu předáte PDF nebo více‑stránkový TIFF, musíte nejprve převést požadovanou stránku na obrázek. K tomu můžete použít knihovnu `Aspose.PDF`.

### 3️⃣ Velké účtenky a výkon
Zpracování 10 MB obrázku může být pomalé. Před předáním enginu snižte rozlišení:

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath).Resize(1024, 0);
```

Metoda `Resize` zachovává poměr stran (`0` pro výšku) a výrazně snižuje velikost souboru, aniž by to ovlivnilo přesnost OCR pro typické účtenky.

### 4️⃣ Problémy s jazykem a fonty
Účtenky mohou obsahovat speciální znaky (€, ¥, atd.). Nastavte jazyk explicitně, pokud znáte locale:

```csharp
ocrEngine.Language = Language.English; // or Language.Spanish, etc.
```

Pro smíšené jazykové účtenky můžete zapnout vícejazyčný režim:

```csharp
ocrEngine.Language = Language.English | Language.French;
```

### 5️⃣ Extrahování strukturovaných dat
Surový text je užitečný, ale většina aplikací potřebuje strukturovaná pole (datum, celkem, položky). JSON rozložení obsahuje souřadnice `BoundingBox` pro každé slovo. Můžete jej následně zpracovat takto:

```csharp
var layout = Newtonsoft.Json.Linq.JObject.Parse(jsonResult);
foreach (var word in layout["Words"])
{
    string text = (string)word["Text"];
    // Simple heuristics: look for "$" or "Total"
}
```

Tento úryvek ukazuje myšlenku; v produkci byste pravděpodobně použili regulární výraz nebo malý pravidlový engine.

## Často kladené otázky

**Q: Můžu to spustit na Linuxu?**  
A: Rozhodně. Aspose.OCR je multiplatformní; stačí nainstalovat .NET runtime na vašem Linuxovém serveru a stejný kód bude fungovat.

**Q: Co když potřebuji zpracovat desítky účtenek za minutu?**  
A: Spusťte smyčku `Parallel.ForEach` a znovu použijte jedinou instanci `OcrEngine` – je thread‑safe pro operace jen ke čtení. Nezapomeňte řešit limity licence pro souběžné použití.

**Q: Funguje to s mobilními fotografiemi pořízenými pod úhlem?**  
A: Engine obsahuje základní deskewing, ale u výrazně nakloněných obrázků můžete předzpracovat pomocí knihovny pro zpracování obrazu (např. OpenCV), abyste nejprve narovnali účtenku.

## Kompletní funkční příklad (kopíruj‑vložit)

Níže je *celý* program, který můžete vložit do `Program.cs`. Žádné další soubory nejsou potřeba kromě licence a obrázku účtenky.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        try
        {
            ocrEngine.SetLicense("Aspose.OCR.lic");
        }
        catch (Exception)
        {
            Console.WriteLine("⚠️ Running in trial mode – license not found.");
        }

        // Load the image to be processed (load image for OCR)
        string imagePath = Path.Combine(Environment.CurrentDirectory, "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}