---
category: general
date: 2026-01-07
description: Extrahujte text z obrázku pomocí Aspose OCR v C#. Naučte se, jak rozpoznat
  text z fotografie, zlepšit přesnost OCR, načíst obrázek pro OCR a nastavit jazyk
  OCR.
draft: false
keywords:
- extract text from image
- recognize text from photo
- improve ocr accuracy
- load image for ocr
- set ocr language
language: cs
og_description: Extrahujte text z obrázku pomocí Aspose OCR. Tento průvodce ukazuje,
  jak rozpoznat text z fotografie, zlepšit přesnost OCR, načíst obrázek pro OCR a
  nastavit jazyk OCR.
og_title: Extrahovat text z obrázku pomocí Aspose OCR – C# tutoriál
tags:
- Aspose OCR
- C#
- Image Processing
title: Extrahování textu z obrázku pomocí Aspose OCR – Kompletní průvodce C#
url: /cs/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat text z obrázku – kompletní implementace v C# s Aspose OCR

Už jste někdy potřebovali **extrahovat text z obrázku**, ale nebyli jste si jisti, která knihovna vám poskytne spolehlivé výsledky? Nejste v tom sami. V mnoha reálných aplikacích—skenery účtenek, ověřovače ID nebo jen rychlý nástroj pro poznámky—je schopnost **rozpoznat text z fotografie** nezbytnou funkcí.

V tomto tutoriálu projdeme kompletním, připraveným příkladem, který vám ukáže, jak **načíst obrázek pro OCR**, nakonfigurovat engine pro **nastavení jazyka OCR**, a aplikovat několik předzpracovatelských triků pro **zlepšení přesnosti OCR**. Na konci budete mít jediný soubor C#, který vytiskne extrahovaný text do konzole, a pochopíte, proč každé nastavení má význam.

> **Tip:** Kód funguje s Aspose.OCR ≥ 23.5, .NET 6+ a v jakémkoli prostředí Windows, Linux nebo macOS, které může spouštět .NET Core.

## Požadavky

- .NET 6 SDK (nebo novější) nainstalován  
- Visual Studio 2022, VS Code nebo jakýkoli editor, který preferujete  
- NuGet balíček `Aspose.OCR` (nainstalujte pomocí `dotnet add package Aspose.OCR`)  
- Obrázkový soubor (JPEG/PNG), který obsahuje jasný tištěný nebo psaný text  

Pokud je máte, pojďme se ponořit.

![extract text from image example](/images/ocr-example.png "extract text from image – Aspose OCR output")

## Krok 1: Vytvoření a uvolnění OCR enginu – jádro „Extrahovat text z obrázku“

První věc, kterou potřebujete, je instance `OcrEngine`. Zabalit ji do bloku `using` zaručuje správné uvolnění nativních zdrojů.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

/// <summary>
/// Demonstrates how to extract text from image using Aspose OCR.
/// </summary>
class Program
{
    static void Main()
    {
        // Step 1 – Initialize the OCR engine (the heart of the process)
        using (var ocrEngine = new OcrEngine())
        {
            // The rest of the workflow lives inside this block.
```

**Proč je to důležité:** `OcrEngine` drží neřízenou paměť pro nativní OCR DLL. Okamžité uvolnění zabraňuje únikům paměti, zejména když zpracováváte mnoho obrázků najednou.

## Krok 2: Definování nastavení rozpoznávání – zlepšení přesnosti OCR

Dále vytvoříme objekt `RecognitionSettings`. Zde **nastavíme jazyk OCR** a přidáme předzpracovatelské filtry, které často rozhodují o rozdílu mezi poškozeným řetězcem a čistým výstupem.

```csharp
            // Step 2 – Configure recognition settings
            var recognitionSettings = new RecognitionSettings
            {
                // Set the language to English; other languages are available via Language enum.
                Language = Language.English,

                // PreprocessFilters help the engine deal with real‑world photo issues.
                PreprocessFilters = new[]
                {
                    PreprocessFilter.Deskew,          // Corrects slight rotation
                    PreprocessFilter.Denoise,         // Reduces grainy noise
                    PreprocessFilter.ContrastEnhance // Boosts text visibility
                }
            };
```

**Proč tyto filtry?**  
- **Deskew** opravuje běžný problém, kdy je foto pořízené telefonem o několik stupňů mimo osu.  
- **Denoise** odstraňuje šmouhy, které mohou být interpretovány jako znaky.  
- **ContrastEnhance** zvýrazňuje slabý inkoust, což je nezbytné pro **zlepšení přesnosti OCR**.

## Krok 3: Načtení obrázku – efektivní načtení obrázku pro OCR

Aspose poskytuje `ImageStream.FromFile` pro rychlé načtení. Můžete také použít `MemoryStream`, pokud obrázek pochází z webového požadavku nebo databáze.

```csharp
            // Step 3 – Load the image you want to analyze
            var imagePath = @"YOUR_DIRECTORY/phone_photo.jpg";
            var imageStream = ImageStream.FromFile(imagePath);
```

**Častý úskalí:** Zadání cesty s lomítky (/) na Windows funguje, ale použití `Path.Combine` je bezpečnější pro multiplatformní projekty.

## Krok 4: Provedení rozpoznání – rozpoznat text z fotografie

Nyní zavoláme `Recognize`, předáme jak stream obrázku, tak naše nastavení. Metoda vrátí prostý řetězec s extrahovaným textem.

```csharp
            // Step 4 – Run OCR and capture the result
            string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);
```

Pokud obrázek obsahuje více bloků textu, Aspose je spojí pomocí koncových znaků řádku, zachovávajíc původní rozvržení, jak jen to jde.

## Krok 5: Výstup výsledku – ověření extrakce

Nakonec výsledek zapíšete do konzole. Ve skutečné aplikaci jej můžete uložit do databáze, odeslat do jiné služby nebo zobrazit v uživatelském rozhraní.

```csharp
            // Step 5 – Show the extracted text
            Console.WriteLine("=== Extracted Text Start ===");
            Console.WriteLine(recognizedText);
            Console.WriteLine("=== Extracted Text End ===");
        } // End of using block – OcrEngine disposed
    }
}
```

### Očekávaný výstup v konzoli

```
=== Extracted Text Start ===
This is a sample receipt.
Total: $23.45
Thank you for shopping!
=== Extracted Text End ===
```

Pokud vidíte poškozené znaky, zkontrolujte, že je obrázek jasný, jazyk odpovídá textu a předzpracovatelské filtry jsou vhodné.

## Krok 6: Volitelné úpravy – doladění pro okrajové případy

### a. Přepínání jazyků

```csharp
recognitionSettings.Language = Language.Spanish; // For Spanish receipts
```

### b. Přidání vlastních filtrů

Aspose také nabízí `PreprocessFilter.Sharpen` nebo `PreprocessFilter.Binarize`. Experimentujte s nimi, když výchozí trojice nepostačuje.

### c. Práce s velkými obrázky

Pro velmi vysoké rozlišení fotografií nejprve zmenšete velikost, aby se snížila spotřeba paměti:

```csharp
var resizedStream = ImageProcessor.Resize(imageStream, 1024, 768);
string text = ocrEngine.Recognize(resizedStream, recognitionSettings);
```

## Často kladené otázky

**Q: Funguje to s ručně psanými poznámkami?**  
**A:** Aspose OCR je optimalizováno pro tištěný text. Rozpoznávání ručně psaného vyžaduje jiný engine (např. Aspose.OCR for Handwriting nebo model strojového učení).

**Q: Mohu zpracovávat více obrázků ve smyčce?**  
**A:** Rozhodně. Stačí přesunout blok `using (var ocrEngine = new OcrEngine())` mimo smyčku a znovu použít engine pro lepší výkon.

**Q: Co když je obrázek stránkou PDF?**  
**A:** Nejprve převěďte stránku PDF na obrázek (Aspose.PDF může vykreslit stránky jako PNG/JPEG), poté ji předáte OCR engine.

## Shrnutí – co jsme dosáhli

- **Extrahovali jsme text z obrázku** pomocí jediného, samostatného C# programu.  
- Ukázali jsme, jak **rozpoznat text z fotografie** s předzpracováním, které **zlepšuje přesnost OCR**.  
- Ukázali jsme správný způsob **načtení obrázku pro OCR** a **nastavení jazyka OCR** pro vícejazyčné scénáře.  

## Další kroky a související témata

- **Dávkové zpracování:** Kombinujte tento úryvek s `Directory.GetFiles` pro OCR celé složky.  
- **Post‑zpracování:** Použijte regulární výrazy k vyčištění dat, částek nebo ID po extrakci.  
- **Integrace:** Přeneste extrahovaný text do Azure Cognitive Search nebo Elastic pro prohledávatelné dokumenty.  

Neváhejte experimentovat s různými kombinacemi filtrů, jazyky a zdroji obrázků. Základní vzorec zůstává stejný: vytvořte engine, nakonfigurujte nastavení, načtěte obrázek, rozpoznávejte a výstupujte. Šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}