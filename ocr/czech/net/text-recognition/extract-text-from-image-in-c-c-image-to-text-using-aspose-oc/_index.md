---
category: general
date: 2026-04-17
description: Extrahujte text z obrázku pomocí Aspose OCR v C#. Naučte se, jak číst
  text z PNG, převést obrázek na text a načíst obrázek pro OCR během několika minut.
draft: false
keywords:
- extract text from image
- read text from png
- convert image to text
- c# image to text
- load image for ocr
language: cs
og_description: Extrahujte text z obrázku pomocí Aspose OCR v C#. Tento tutoriál ukazuje,
  jak číst text z PNG, převést obrázek na text a efektivně načíst obrázek pro OCR.
og_title: Extrahování textu z obrázku v C# – Kompletní průvodce Aspose OCR
tags:
- Aspose OCR
- C#
- Image Processing
title: Extrahovat text z obrázku v C# – c# obrázek na text pomocí Aspose OCR
url: /cs/net/text-recognition/extract-text-from-image-in-c-c-image-to-text-using-aspose-oc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z obrázku v C# – Kompletní průvodce Aspose OCR

Už jste někdy potřebovali **extrahovat text z obrázku**, ale nebyli jste si jisti, kterou knihovnu zvolit? Nejste sami. Mnoho vývojářů narazí na tento problém, když mají PNG screenshot, naskenovanou fakturu nebo vícejazyčný cedule a chtějí převést pixely na prohledávatelný text.  

V tomto tutoriálu vás provedeme praktickým řešením, které vám umožní **číst text z PNG**, **převést obrázek na text** a **načíst obrázek pro OCR** pomocí Aspose OCR – vše v čistém, moderním C#. Na konci budete mít připravený program, který můžete vložit do libovolného .NET projektu.

## Co se naučíte

- Jak načíst soubor obrázku pro OCR (krok „načíst obrázek pro OCR“)  
- Jak nakonfigurovat Aspose OCR pro konkrétní jazykovou skupinu  
- Jak získat rozpoznaný řetězec a zobrazit jej v konzoli  
- Tipy pro práci s více jazyky, velkými soubory a správu paměti  

Externí dokumentace není potřeba; vše, co potřebujete, je v níže uvedených úryvcích kódu.

## Požadavky

- .NET 6+ SDK (nebo .NET Core 3.1+ – API je stejné)  
- Visual Studio 2022, VS Code nebo jakékoli jiné IDE, které preferujete  
- NuGet balíček **Aspose.OCR** (nainstalujte pomocí `dotnet add package Aspose.OCR`)  

Pokud máte vše připravené, pojďme na to.

![Extract text from image using Aspose OCR in C#](https://example.com/aspsoe-ocr-demo.png "extract text from image using Aspose OCR")

## Krok 1 – Načtení obrázku pro OCR

Prvním krokem je poskytnout OCR enginu něco ke čtení. Aspose OCR pracuje s řadou formátů, ale PNG je běžná volba pro screenshoty a naskenovanou grafiku.

```csharp
using Aspose.OCR;

// Replace with the actual path to your PNG file
string imagePath = @"C:\Images\sample.png";

// OcrImage.FromFile handles PNG, JPEG, BMP, TIFF, etc.
OcrImage ocrImage = OcrImage.FromFile(imagePath);
```

> **Proč je to důležité:** Správné načtení obrázku zajišťuje, že engine vidí přesná pixelová data, která očekáváte. Pokud předáte poškozený stream, rozpoznání selže tiše.

## Krok 2 – Vytvoření a konfigurace OCR enginu

Dále vytvořte instanci `OcrEngine`. Volitelně můžete nastavit jazykovou skupinu; pro mnoho západních skriptů funguje výchozí nastavení, ale pokud pracujete s cyrilicí, arabštinou nebo asijskými znaky, budete chtít engine informovat předem.

```csharp
// The using statement guarantees proper disposal of native resources.
using var ocrEngine = new OcrEngine();

// Example: set language to Cyrillic if your PNG contains Russian or Ukrainian text.
// OcrLanguage.Cyrillic covers several Slavic languages.
ocrEngine.Language = OcrLanguage.Cyrillic;

// If you need to support multiple languages, you can combine flags:
 // ocrEngine.Language = OcrLanguage.English | OcrLanguage.Cyrillic;
```

> **Pro tip:** Nastavení jazyka zužuje množinu znaků, které engine hledá, což urychluje rozpoznání a zvyšuje přesnost.

## Krok 3 – Provedení OCR a extrakce textu

Nyní se děje těžká práce. Zavolejte `Recognize` s obrázkem, který jste načetli dříve, a poté přečtěte vlastnost `Text` z výsledku.

```csharp
// Run OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);

// The recognized string is available via the Text property
string extractedText = ocrResult.Text;

// Output the result to the console (or write to a file, DB, etc.)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(extractedText);
```

### Očekávaný výstup

Pokud `sample.png` obsahuje frázi „Hello, World!“, uvidíte:

```
=== OCR Output ===
Hello, World!
```

Pokud je obrázek složitější (např. víceřádková účtenka), engine zachová zalomení řádků a poskytne vám připravený blok textu ke zpracování.

## Krok 4 – Zabalte vše do kompletního programu

Níže je kompletní, samostatná konzolová aplikace, kterou můžete zkopírovat a vložit do nového C# projektu. Obsahuje ošetření chyb a komentáře vysvětlující jednotlivé části.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Load the image you want to recognize
                // Change the path to point at your own PNG file.
                var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.png");

                // 2️⃣ Create an OCR engine instance (disposed automatically)
                using var ocrEngine = new OcrEngine();

                // 3️⃣ Choose the language group.
                // Cyrillic works for Russian, Ukrainian, Bulgarian, etc.
                // For English only, you could use OcrLanguage.English.
                ocrEngine.Language = OcrLanguage.Cyrillic;

                // 4️⃣ Perform OCR
                var ocrResult = ocrEngine.Recognize(ocrImage);

                // 5️⃣ Output the recognized text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Simple error handling – in production you’d log this.
                Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

Spusťte program (`dotnet run` ze složky projektu) a sledujte, jak konzole vypíše extrahovaný řetězec. To je celý **workflow pro extrahování textu z obrázku** během méně než 30 řádků kódu.

## Krok 5 – Běžné varianty a okrajové případy

### Čtení textu z PNG vs. jiné formáty

I když příklad používá PNG, Aspose OCR také podporuje JPEG, BMP, TIFF a GIF. Stačí změnit příponu souboru; stejný volání `OcrImage.FromFile` funguje bez úprav.

### Převod obrázku na text ve Web API

Pokud potřebujete tuto funkci zpřístupnit přes HTTP endpoint, můžete přijmout nahrání `IFormFile`, převést stream na `OcrImage` pomocí `OcrImage.FromStream` a vrátit řetězec jako JSON. Hlavní OCR logika zůstává stejná.

```csharp
// Example snippet inside an ASP.NET Core controller action
[HttpPost("api/ocr")]
public async Task<IActionResult> OcrUpload(IFormFile file)
{
    using var stream = file.OpenReadStream();
    var ocrImage = OcrImage.FromStream(stream);
    using var engine = new OcrEngine { Language = OcrLanguage.English };
    var result = engine.Recognize(ocrImage);
    return Ok(new { text = result.Text });
}
```

### Práce s velkými obrázky

Velké, vysoce rozlišené obrázky mohou spotřebovat hodně paměti. Praktický přístup je zmenšit obrázek před jeho předáním engine:

```csharp
// Reduce resolution to 150 DPI (good trade‑off between speed and accuracy)
ocrEngine.ImagePreprocessing = ImagePreprocessingOptions.AutoResize;
ocrEngine.Dpi = 150;
```

### Dokumenty s více jazyky

Pokud dokument kombinuje angličtinu a cyrilici, spojte jazykové příznaky:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Cyrillic;
```

Engine se pokusí rozpoznat znaky z obou sad.

### Uvolňování prostředků

Příkaz `using` kolem `OcrEngine` zaručuje uvolnění nativních prostředků. Zapomenutí na to může vést k únikům paměti, zejména v dlouho běžících službách.

## Pro tipy pro spolehlivé OCR

- **Čisté obrázky vítězí:** Předzpracujte obrázky (odstranění šikmosti, šumu) pomocí knihoven jako **ImageSharp** před OCR.  
- **Velikost písma má význam:** Text menší než 10 px se často nečte; zvažte zvětšení obrázku.  
- **Kontrolujte `ocrResult.Confidence`:** Objekt `OcrResult` také poskytuje skóre důvěry pro každé slovo – použijte jej k označení částí s nízkou důvěrou k ruční kontrole.  
- **Dávkové zpracování:** Pro desítky souborů znovu použijte jednu instanci `OcrEngine`, abyste se vyhnuli opakovanému inicializačnímu zatížení.

## Závěr

Právě jste se naučili, jak **extrahovat text z obrázku** v C# pomocí Aspose OCR, od **načtení obrázku pro OCR** po **převod obrázku na text** a **čtení textu z PNG**. Kompletní, spustitelný příklad ukazuje přesný kód, který potřebujete, vysvětluje, proč každý krok existuje, a nabízí praktické varianty pro reálné scénáře.

Jste připraveni na další výzvu? Zkuste předat extrahovaný řetězec do vyhledávacího indexu, přeložit jej pomocí Azure Cognitive Services nebo vygenerovat prohledávatelný PDF se stejnou textovou vrstvou. Možnosti jsou neomezené a nyní máte pevný základ pro jakýkoli **c# image to text** projekt.

Klidně experimentujte, upravujte nastavení jazyků nebo integrujte tento úryvek do větší aplikace. Pokud narazíte na problémy, zanechte komentář níže – šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}