---
category: general
date: 2026-01-09
description: c# OCR tutoriál pro čtení textu z PNG, převod obrázku na text a rozpoznání
  hindského textu na účtence pomocí Aspose OCR.
draft: false
keywords:
- c# ocr tutorial
- read text from png
- convert image to text
- recognize hindi text
- extract text from receipt
language: cs
og_description: c# OCR tutoriál, který vás naučí, jak číst text z PNG, převést obrázek
  na text a rozpoznat hindský text na účtence pomocí Aspose OCR.
og_title: c# OCR tutoriál – Extrahování hindského textu z PNG účtenek
tags:
- OCR
- C#
- Aspose
- Image Processing
title: c# OCR tutoriál – Extrahovat hindský text z PNG účtenek
url: /cs/net/text-recognition/c-ocr-tutorial-extract-hindi-text-from-png-receipts/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutoriál – Extrahování hindského textu z PNG účtenek

Už jste se někdy zamysleli, jak **číst text z PNG** souborů v C# aplikaci? Možná máte spoustu hindských účtenek a potřebujete automaticky získat částky. Právě tohle c# ocr tutoriál řeší—převod obrázku na prohledávatelný text pomocí několika řádků kódu.

V tomto průvodci vás provedeme instalací Aspose OCR, načtením PNG účtenky, rozpoznáním hindských znaků a nakonec vytištěním extrahovaného řetězce do konzole. Na konci budete schopni **převést obrázek na text**, **rozpoznat hindský text** a dokonce **extrahovat text z účtenky** obrázků, aniž byste opustili své IDE.

> **Poznámka k předpokladům:** Potřebujete platnou licenci Aspose OCR (nebo můžete použít bezplatnou zkušební verzi) a nainstalovaný .NET 6+. Pokud jste v NuGet noví, nebojte se—také to pokryjeme.

## Co budete potřebovat

- **Visual Studio 2022** (nebo jakýkoli editor kompatibilní s C#)
- **.NET 6 SDK** (nebo novější)
- **Aspose.OCR** NuGet balíček  
  ```bash
  dotnet add package Aspose.OCR
  ```
- Vzorek obrázku účtenky, např. `hindi-receipt.png`, uložený ve složce projektu.

Když máte tyto věci připravené, můžete okamžitě zkopírovat‑vložit finální kód a stisknout **F5**.

## Krok 1: Nastavení projektu a import jmenných prostorů

Nejprve vytvořte konzolový projekt, pokud ho ještě nemáte:

```bash
dotnet new console -n HindiReceiptOcr
cd HindiReceiptOcr
dotnet add package Aspose.OCR
```

Nyní otevřete `Program.cs`. Na začátku importujte jmenné prostory Aspose OCR, aby kompilátor věděl, kde najít třídy:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;
```

> **Proč je to důležité:** `OcrEngine` se nachází v `Aspose.OCR`, zatímco výčty související s jazykem jsou v `Aspose.OCR.Settings`. Zapomenutí jednoho z nich způsobí chybu při kompilaci.

## Krok 2: Inicializace OCR enginu a výběr jazykového modelu

OCR engine potřebuje vědět **který jazyk** má hledat. Aspose poskytuje mnoho jazykových balíčků; zadáním `OcrLanguage.Hindi` řeknete enginu, aby stáhl (pokud chybí) a použil hindský model.

```csharp
// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // The library will auto‑download the model the first time it runs.
    Language = OcrLanguage.Hindi
};
```

> **Tip:** Pokud plánujete zpracovávat účtenky v několika jazycích, můžete během běhu měnit `Language` nebo dokonce povolit režim `MultiLanguage`.

## Krok 3: Předání PNG účtenky enginu

Zde **čteme text z PNG**. Zadejte úplnou cestu (relativní k spustitelnému souboru funguje dobře). Metoda vrací prostý řetězec obsahující vše, co engine dokázal rozluštit.

```csharp
// Step 3: Perform OCR on the target image file
string imagePath = @"hindi-receipt.png";   // adjust if your file lives elsewhere
string recognizedText = ocrEngine.RecognizeImage(imagePath);
```

Pokud je obrázek vysokého rozlišení a text je čistý, získáte téměř dokonalé výsledky. Pro špinavé skeny zvažte předzpracování (např. binarizaci) – Aspose nabízí metody `PreprocessImage`, které můžete později prozkoumat.

## Krok 4: Zobrazení nebo uložení extrahovaného textu

Většina vývojářů jednoduše během testování výsledek vypíše do konzole. V produkčním scénáři můžete zapisovat do databáze nebo CSV souboru.

```csharp
// Step 4: Show the OCR result
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(recognizedText);
```

Spuštění programu se vzorovou účtenkou vytiskne něco jako:

```
=== OCR Output ===
दिनांक: 09/01/2026
बिल no: 12345
रक्कम: ₹ 1,250.00
धन्यवाद!
```

To je část **převést obrázek na text** v akci—žádná ruční přepisování není potřeba.

## Kompletní funkční příklad (připravený ke kopírování)

Níže je kompletní, samostatný program. Vložte jej do `Program.cs`, umístěte `hindi-receipt.png` vedle zkompilovaného `.exe` a stiskněte **Ctrl + F5**.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace HindiReceiptOcr
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine with Hindi language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.Hindi
            };

            // 2️⃣ Path to the PNG receipt (adjust if needed)
            string imagePath = @"hindi-receipt.png";

            // 3️⃣ Run OCR – this will download the Hindi model on first run
            string recognizedText = ocrEngine.RecognizeImage(imagePath);

            // 4️⃣ Output the result – you can also write to a file or DB
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### Očekávaný výstup

Když obrázek účtenky obsahuje jasné hindské znaky, konzole zobrazí extrahované řádky se zachováním zalomení řádků. Pokud OCR nedokáže rozpoznat slovo, uvidíte poškozený fragment—pouze podnět ke zlepšení kvality obrázku nebo úpravě předzpracování.

## Krok 5: Pokročilejší – Programové extrahování textu z účtenky

Pokud je vaším cílem **extrahovat text z účtenky** (datum, celková částka, číslo faktury), můžete po‑zpracovat OCR řetězec pomocí regulárních výrazů:

```csharp
using System.Text.RegularExpressions;

// Example: pull the amount (₹) from the OCR result
var amountMatch = Regex.Match(recognizedText, @"रक्कम:\s*₹\s*([\d,]+\.\d{2})");
if (amountMatch.Success)
{
    Console.WriteLine($"Detected amount: {amountMatch.Groups[1].Value}");
}
```

Tento malý úryvek ukazuje, jak převést surový výstup OCR na strukturovaná data—ideální pro import do účetního softwaru.

## Časté problémy a jak se jim vyhnout

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Prázdný výstup** | Špatná cesta k obrázku nebo soubor nebyl zkopírován do výstupní složky. | Použijte `Path.GetFullPath` a ověřte, že soubor existuje (`File.Exists`). |
| **Špatné znaky** | PNG s nízkým rozlišením nebo komprimovanými barvami. | Zvětšete obrázek, nastavte DPI na 300+, nebo použijte `ocrEngine.ImagePreprocessor`. |
| **Jazykový model nebyl stažen** | Žádné připojení k internetu při prvním spuštění. | Předem stáhněte hindský model přes Aspose portál nebo jej hostujte lokálně. |
| **Zpoždění výkonu** | Zpracování mnoha stránek ve smyčce bez uvolnění prostředků. | Zabalte `OcrEngine` do bloku `using` nebo znovu použijte jedinou instanci. |

## Ilustrace obrázku

![c# OCR tutoriál čtení hindského textu z PNG účtenky](https://example.com/placeholder-image.png "c# OCR tutoriál – čtení textu z PNG účtenky")

*Snímek obrazovky ukazuje hindskou účtenku před a po konverzi OCR.*

## Shrnutí: Co jsme probrali

- Nastavili jsme C# konzolovou aplikaci a přidali NuGet balíček Aspose OCR.  
- Inicializovali jsme `OcrEngine` s jazykovým modelem **recognize hindi text**.  
- **Četli jsme text z PNG** pomocí `RecognizeImage`.  
- **Převod obrázku na text** a výsledek vypsali.  
- Ukázali jsme jednoduchý vzor pro **extrahování textu z účtenky** polí.  

Vše bylo dodáno v jediném spustitelném souboru—přesně to, co by **c# OCR tutoriál** měl poskytnout.

## Další kroky a související témata

1. **Dávkové zpracování** – procházet složku s obrázky účtenek a ukládat výsledky do CSV.  
2. **Předzpracování** – prozkoumat `ocrEngine.ImagePreprocessor` pro odstranění šumu, korekci sklonu nebo zvýšení kontrastu.  
3. **Vícejazykové OCR** – povolit `OcrLanguage.Multilingual` pro zpracování účtenek, které kombinují hindštinu a angličtinu.  
4. **Integrace** – odeslat extrahovaná data do modelu Entity Framework Core pro trvalé uložení.  

Pokud vás některé z nich zajímají, podívejte se na naše tutoriály o **convert image to text in C#** a **extract structured data from OCR results**.

### Šťastné programování!

Neváhejte zanechat komentář, pokud narazíte na problémy, nebo se podělit, jak jste rozšířili tento **c# OCR tutoriál** ve svých projektech. Pamatujte, OCR je jen první krok—čistá data jsou místem, kde se děje pravá magie. 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}