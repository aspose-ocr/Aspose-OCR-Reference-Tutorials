---
category: general
date: 2026-04-06
description: Jak používat OCR v C# k extrakci prostého textu z JPG obrázků, včetně
  cyrilických znaků. Naučte se načíst obrázek pro OCR, rozpoznat text v JPG a získat
  spolehlivé výsledky.
draft: false
keywords:
- how to use OCR
- extract plain text
- extract cyrillic text
- recognize text jpg
- load image for OCR
language: cs
og_description: Jak používat OCR v C# k extrakci prostého textu z JPG souborů. Tento
  průvodce ukazuje, jak načíst obrázek pro OCR, rozpoznat text v JPG a pracovat s
  cyrilským textem.
og_title: Jak používat OCR v C# – Extrahovat prostý text z obrázků
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Jak použít OCR v C# – Extrahovat čistý text z obrázků
url: /cs/net/text-recognition/how-to-use-ocr-in-c-extract-plain-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat OCR v C# – Extrahovat prostý text z obrázků

Už jste se někdy zamýšleli **jak používat OCR** v .NET projektu, aniž byste se museli potýkat s nativními knihovnami? Možná máte složku naskenovaných účtenek, několik snímků obrazovky s cyrilskými popisky, nebo jen potřebujete vytáhnout text z JPEG pro rychlou analýzu. Dobrou zprávou je, že Aspose OCR dělá celý proces hračkou.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který ukazuje **jak používat OCR** k **extrahování prostého textu** z JPEG obrázku, jak **načíst obrázek pro OCR**, a dokonce jak **extrahovat cyrilský text**, když zdrojový jazyk není latinka. Na konci budete mít malou konzolovou aplikaci, která vytiskne rozpoznaný text přímo do konzole—žádné extra soubory, žádné tajemné vedlejší efekty.

> **Co získáte**  
> * Průvodce krok za krokem, který můžete zkopírovat a vložit do Visual Studia.  
> * Vysvětlení *proč* každá řádka má význam, ne jen *co* dělá.  
> * Tipy pro práci s velkými obrázky, více jazyky a běžné úskalí.

## Požadavky

* .NET 6 SDK nebo novější (kód funguje také s .NET Core a .NET Framework).  
* Visual Studio 2022 (nebo jakýkoli editor, který preferujete).  
* Přístup k internetu při prvním spuštění vzorku—Aspose OCR stahuje jazykové balíčky na vyžádání.  

Pokud vám chybí NuGet balíček Aspose OCR, pokryjeme to v prvním kroku.

## Krok 1 – Instalace Aspose OCR přes NuGet (a proč je to důležité)

Krok **načíst obrázek pro OCR** nemůže proběhnout, dokud není knihovna přítomna. Použití NuGet zajišťuje, že získáte nejnovější, bezpečnostně opravené binární soubory a automaticky stáhne všechny potřebné závislosti.

```bash
dotnet add package Aspose.OCR
```

*Proč je to důležité*: Aspose OCR je distribuován s malým jádrovým DLL a načítá jazyková data jen když o to požádáte. To udržuje vaši aplikaci lehkou a zabraňuje balení megabajtů nepoužívaných jazykových souborů.

## Krok 2 – Inicializace OCR Engine (srdce **jak používat OCR**)

Vytvoření instance `OcrEngine` je první skutečná řádka kódu, která má význam pro **jak používat OCR**. Engine ve výchozím nastavení používá režim „na vyžádání“, což znamená, že stáhne jazykový balíček při prvním požadavku na konkrétní jazyk.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Step 2: Create the engine – it will fetch language data when needed.
var ocrEngine = new OcrEngine();
```

> **Tip**: Pokud pracujete za firemním proxy, nastavte `OcrEngine.Proxy` před prvním voláním rozpoznání, aby stažení proběhlo úspěšně.

## Krok 3 – Vyberte jazyk – **Extrahovat cyrilský text** podle potřeby

Aspose OCR podporuje desítky skriptů. Pro **extrahování cyrilského textu** jednoduše nastavte vlastnost `Language` na `OcrLanguage.Cyrillic`. Při prvním spuštění této řádky se modul pro cyrilštinu (≈ 5 MB) stáhne z CDN Aspose.

```csharp
// Step 3: Tell the engine which language to look for.
// This will automatically download the Cyrillic language pack on first use.
ocrEngine.Language = OcrLanguage.Cyrillic;
```

Pokud váš obrázek obsahuje jen latinské znaky, můžete nahradit `Cyrillic` za `English`. Stejný vzor funguje pro jakýkoli podporovaný jazyk.

## Krok 4 – **Načíst obrázek pro OCR** – z disku nebo proudu

Nyní skutečně **načteme obrázek pro OCR**. Třída `System.Drawing.Image` zvládá většinu běžných formátů (JPG, PNG, BMP). Pokud jste na ne‑Windows platformě, zvažte místo toho `ImageSharp`, ale pro tento tutoriál je vestavěný typ dostačující.

```csharp
using System.Drawing;

// Step 4: Load the picture that holds the text.
using var image = Image.FromFile(@"C:\Images\cyrillic_sample.jpg");
```

> **Proč je to důležité**: Načtení obrázku uvnitř bloku `using` zaručuje, že neřízené GDI+ zdroje jsou rychle uvolněny, což zabraňuje únikům paměti v dlouho běžících službách.

## Krok 5 – **Rozpoznat text JPG** – Spustit OCR proces

S engine nastaveným a obrázkem načteným, konečně **rozpoznáme text jpg**. Metoda `Recognize` vrací `OcrResult`, který obsahuje prostý řetězec, skóre důvěry a dokonce i ohraničující rámečky, pokud je později potřebujete.

```csharp
// Step 5: Perform the recognition.
var ocrResult = ocrEngine.Recognize(image);
```

Pokud chcete doladit přesnost, můžete upravit `ocrEngine.Config` (např. povolit `AutoRotate` nebo nastavit `TextOrientation`). Pro většinu jednoduchých scénářů výchozí nastavení funguje překvapivě dobře.

## Krok 6 – **Extrahovat prostý text** – Zobrazit výsledek

Posledním krokem **jak používat OCR** je získat rozpoznaný řetězec z `ocrResult` a něco s ním udělat. Zde jej jednoduše vypíšeme do konzole, což také ukazuje, jak **extrahovat prostý text** z objektu výsledku.

```csharp
// Step 6: Output the plain text to the console.
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrResult.Text);
```

### Očekávaný výstup

Pokud `cyrillic_sample.jpg` obsahuje frázi “Привет мир” (Hello world), měli byste vidět:

```
=== Recognized Text ===
Привет мир
```

Pokud je obrázek rozmazaný nebo je text příliš malý, výstup může obsahovat chyby; můžete zkontrolovat `ocrResult.Confidence`, abyste se rozhodli, zda zopakovat s vyšším rozlišením zdroje.

## Kompletní, připravený k spuštění příklad

Níže je kompletní program. Zkopírujte jej do nového projektu Console App (`dotnet new console`) a spusťte. Kromě obrázku, na který odkazujete, nejsou potřeba žádné další soubory.

```csharp
// ---------------------------------------------------------------
// How to Use OCR in C# – Complete Example
// ---------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Install Aspose.OCR via NuGet first (dotnet add package Aspose.OCR)

        // 2️⃣ Initialize the OCR engine – on‑demand language download.
        var ocrEngine = new OcrEngine();

        // 3️⃣ Select Cyrillic to **extract Cyrillic text**.
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // 4️⃣ **Load image for OCR** – change the path to your own file.
        using var image = Image.FromFile(@"YOUR_DIRECTORY\cyrillic_sample.jpg");

        // 5️⃣ **Recognize text jpg** – run the engine.
        var ocrResult = ocrEngine.Recognize(image);

        // 6️⃣ **Extract plain text** – display it.
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Poznámka**: Nahraďte `YOUR_DIRECTORY\cyrillic_sample.jpg` skutečnou cestou k vašemu JPEG souboru.

## Časté otázky a okrajové případy

### Co když potřebuji **rozpoznat text jpg** ze streamu místo souboru?

Můžete přímo předat `MemoryStream`:

```csharp
using var ms = new MemoryStream(File.ReadAllBytes("myImage.jpg"));
using var img = Image.FromStream(ms);
var result = ocrEngine.Recognize(img);
```

### Jak zvládnout více jazyků na jednom obrázku?

Nastavte `ocrEngine.Language` na `OcrLanguage.Multilingual`. Engine se pokusí automaticky detekovat každý skript, což je užitečné, když účtenka kombinuje angličtinu a cyrilštinu.

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

### Můj obrázek je obrovský (více než 5 MP). Zkolabuje engine?

Velké obrázky zvyšují využití paměti a mohou zpomalit rozpoznání. Rychlé předběžné zmenšení pomůže:

```csharp
var resized = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
var result = ocrEngine.Recognize(resized);
```

### Můžu získat skóre důvěry pro každou řádku?

Ano—`ocrResult.Lines` obsahuje `Confidence` pro každou řádku. Procházením můžete filtrovat výsledky s nízkou důvěrou.

```csharp
foreach (var line in ocrResult.Lines)
{
    if (line.Confidence > 0.8)
        Console.WriteLine(line.Text);
}
```

## Pro tipy pro produkčně připravené OCR

* **Ukládejte jazykové balíčky do cache** – první stažení může trvat několik sekund; uložte soubory do známé složky a nastavte `ocrEngine.LanguageDataPath`, aby se znovu použily.  
* **Dávkové zpracování** – znovu použijte jedinou instanci `OcrEngine` pro mnoho obrázků; vytváření nového engine pro každý soubor přidává zbytečnou zátěž.  
* **Zpracování chyb** – obalte volání `Recognize` do try/catch bloku. Aspose vyhazuje `OcrException` pro poškozené obrázky nebo nepodporované formáty.  
* **Logování** – zaznamenávejte `ocrResult.Confidence`, abyste později mohli auditovat, které stránky potřebovaly manuální revizi.

## Závěr

Právě jsme prošli **jak používat OCR** v C# k **extrahování prostého textu** z JPEG, ukázali kroky **načíst obrázek pro OCR**, ukázali, jak **rozpoznat text jpg**, a dokonce vytáhli **cyrilský text** z obrázku. Ukázka je plně funkční, vyžaduje jen jeden NuGet balíček a může být rozšířena pro zpracování vícejazykových dokumentů, dávkových úloh nebo scénářů skenování v reálném čase.

Připraveni na další výzvu? Zkuste vyměnit cyrilský jazyk za arabštinu, experimentujte s příznakem `AutoRotate`, nebo integrujte výstup do vyhledávacího indexu. Možnosti jsou neomezené.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}