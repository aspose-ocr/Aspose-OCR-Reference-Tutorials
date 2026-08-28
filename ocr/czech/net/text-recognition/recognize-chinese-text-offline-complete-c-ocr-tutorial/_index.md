---
category: general
date: 2026-01-02
description: Naučte se rozpoznávat čínský text a extrahovat text z PNG souborů pomocí
  offline rozpoznávání textu s Aspose.OCR. Není potřeba internet – proveďte OCR na
  obrázku během několika kroků.
draft: false
keywords:
- recognize chinese text
- extract text from png
- offline text recognition
- perform OCR on image
language: cs
og_description: Rozpoznávejte čínský text bez internetu. Tento tutoriál ukazuje, jak
  extrahovat text z PNG pomocí offline rozpoznávání textu a provést OCR na obrázku
  v C#.
og_title: Rozpoznávání čínského textu offline – krok za krokem C# průvodce
tags:
- OCR
- C#
- Aspose
title: Rozpoznání čínského textu offline – kompletní C# OCR tutoriál
url: /cs/net/text-recognition/recognize-chinese-text-offline-complete-c-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rozpoznávání čínského textu offline – kompletní tutoriál C# OCR

Už jste někdy potřebovali **rozpoznat čínský text** ze skenovaného PNG, ale vaše aplikace běží na stroji bez internetu? Nejste sami. V mnoha podnikových scénářích – například na serverech oddělených od sítě nebo v terénních zařízeních – spoléhat se na cloudové služby prostě není možnost.  

V tomto průvodci si projdeme samostatné řešení, které vám umožní **extrahovat text z png** souborů, spustit **offline rozpoznávání textu** a **provádět OCR na obrazových** aktivech pomocí Aspose.OCR. Na konci budete mít připravený C# konzolový program, který vytiskne čínské znaky přímo do konzole.

## Požadavky

- .NET 6 SDK (nebo jakákoli recentní verze .NET) nainstalováno lokálně.  
- Visual Studio 2022 nebo VS Code – podle toho, co preferujete.  
- Kopie NuGet balíčku Aspose.OCR pro .NET (`Aspose.OCR`).  
- Soubory jazykových zdrojů pro angličtinu a zjednodušenou čínštinu (v tutoriálu je ukázáno, jak je stáhnout automaticky).  
- Obrázek pojmenovaný `chinese_doc.png` umístěný ve složce, na kterou můžete odkazovat (`YOUR_DIRECTORY` placeholder).

Žádné další služby, žádné API klíče – jen lokální DLL a pár souborů zdrojů.

---

## Krok 1 – Stáhněte požadované jazykové zdroje (jednou)

Aspose.OCR ukládá jazykové balíčky na disk. Při prvním spuštění aplikace je musíte stáhnout. Volání `ResourceManager.DownloadResources` udělá přesně to a protože předáme jak angličtinu, tak zjednodušenou čínštinu, engine může později přepínat mezi nimi bez dalšího síťového provozu.

```csharp
using Aspose.OCR;

// Download English and Simplified Chinese language packs (run once)
ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);
```

> **Pro tip:** Uchovávejte staženou složku (`Aspose.OCR.Resources`) pod verzovacím systémem, pokud potřebujete reprodukovatelné sestavení na více strojích.

## Krok 2 – Inicializujte OCR engine v offline režimu

Nastavení `OfflineMode = true` říká knihovně, aby se vyhnula jakýmkoli HTTP voláním. To je klíč k pravému **offline rozpoznávání textu**.

```csharp
// Initialise the OCR engine for offline use
var ocrEngine = new OcrEngine()
{
    OfflineMode = true   // Guarantees no network traffic
};
```

> **Proč je to důležité:** Některé OCR knihovny přecházejí na cloudové služby, když chybí jazykový balíček. Vynucením offline režimu garantujeme deterministický výkon a soulad s politikami ochrany dat.

## Krok 3 – Načtěte PNG, který chcete zpracovat

Použijeme `System.Drawing.Bitmap` k načtení obrázku. Pokud váš projekt cílí na .NET 6+ na ne‑Windows platformách, zvažte `SkiaSharp` jako alternativu, ale pro většinu Windows‑centrických nasazení `Bitmap` funguje dobře.

```csharp
using System.Drawing;

// Load the PNG that contains Chinese characters
var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
var image = new Bitmap(imagePath);
```

> **Edge case:** Pokud je PNG velmi velký (více než 5 MP), můžete jej nejprve zmenšit, aby se urychlilo rozpoznávání a snížila spotřeba paměti:

```csharp
// Optional downscale for huge images
if (image.Width * image.Height > 5_000_000)
{
    var scaled = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
    image.Dispose();
    image = scaled;
}
```

## Krok 4 – Spusťte rozpoznávání se zjednodušenou čínštinou

Zde říkáme engine přesně, který jazyk použít. Objekt `RecognitionOptions` vám také umožní doladit věci jako `DetectOrientation` nebo `PreserveFormatting`, ale výchozí nastavení fungují dobře pro většinu tištěných dokumentů.

```csharp
using Aspose.OCR;

// Perform OCR using Simplified Chinese language pack
var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
{
    Language = Language.ChineseSimplified
});
```

## Krok 5 – Zobrazte (nebo dále zpracujte) extrahovaný text

Vlastnost `OcrResult.Text` obsahuje textovou reprezentaci. Můžete ji zapsat do konzole, souboru nebo předat do následného NLP pipeline.

```csharp
// Output the recognized Chinese text to the console
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

### Očekávaný výstup

Pokud `chinese_doc.png` obsahuje frázi “你好，世界！”, konzole zobrazí:

```
=== Recognized Chinese Text ===
你好，世界！
```

> **Poznámka:** Přesnost OCR závisí na kvalitě obrázku, čitelnosti písma a kontrastu. Pro nejlepší výsledky použijte skeny ve vysokém rozlišení (300 dpi nebo vyšší) a ujistěte se, že text není nakřivený.

---

## Kompletní funkční příklad

Níže je kompletní program připravený ke zkopírování a vložení. Uložte jej jako `Program.cs` v novém konzolovém projektu a spusťte `dotnet run`. Všechny kroky jsou spojeny dohromady, takže můžete vidět tok od stažení zdrojů až po finální výstup.

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;

class OfflineExample
{
    static void Main()
    {
        // 1️⃣ Download language resources (only needed once)
        ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);

        // 2️⃣ Initialise OCR engine in offline mode
        var ocrEngine = new OcrEngine()
        {
            OfflineMode = true
        };

        // 3️⃣ Load the PNG image
        var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
        using var image = new Bitmap(imagePath);

        // 4️⃣ Recognise Simplified Chinese text
        var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
        {
            Language = Language.ChineseSimplified
        });

        // 5️⃣ Print the result
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Tip:** Zabalte volání `ResourceManager.DownloadResources` do bloku `try/catch`, pokud chcete elegantní zacházení, když je internet skutečně nedostupný. Metoda jinak vyhodí `NetworkException`.

---

## Často kladené otázky (FAQ)

| Question | Answer |
|----------|--------|
| **Mohu rozpoznat tradiční čínštinu?** | Ano—nahraďte `Language.ChineseSimplified` za `Language.ChineseTraditional` a stáhněte odpovídající balíček. |
| **Co když potřebuji extrahovat text z JPEG místo PNG?** | Stejný kód funguje; stačí změnit příponu souboru. `Bitmap` podporuje většinu běžných rastrových formátů. |
| **Je možné získat ohraničující rámečky pro každý znak?** | Nastavte `RecognitionOptions.DetectRegions = true`. `OcrResult` pak bude obsahovat objekty `Region` s koordináty. |
| **Jak to spustím na Linuxu?** | Použijte balíček `System.Drawing.Common` (1.0+). Na headless Linuxu můžete potřebovat nativní závislost `libgdiplus`. |
| **Mohu hromadně zpracovávat složku obrázků?** | Určitě—zabalte logiku rozpoznávání do smyčky `foreach (var file in Directory.GetFiles(folder, "*.png"))` . |

## Další kroky a související témata

- **Zlepšit přesnost**: experimentujte s `RecognitionOptions.PreprocessImage = true`, aby engine automaticky vylepšil kontrast.  
- **Kombinovat jazyky**: můžete předat pole jazyků do `ResourceManager.DownloadResources` a nechat engine automaticky detekovat.  
- **Integrovat s UI**: vložte konzolový kód do WinForms nebo WPF aplikace a zobrazte výsledek OCR v textovém poli.  
- **Prozkoumat další Aspose knihovny**: `Aspose.PDF` pro generování PDF, `Aspose.Slides` pro automatizaci snímků atd.  

Pokud máte zájem o extrahování textu z jiných formátů obrázků, stejný vzor platí – stačí vyměnit cestu k souboru a případně upravit možnosti předzpracování. Šťastné kódování!

---

![recognize chinese text example](/images/recognize-chinese-text.png "Screenshot showing recognize chinese text output in console")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}