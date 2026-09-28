---
category: general
date: 2025-12-29
description: Jak používat Aspose OCR k převodu textu z obrázku a extrahování korejského
  textu. Krok za krokem průvodce, jak extrahovat text z obrázku a rozpoznat korejský
  text v C#.
draft: false
keywords:
- how to use aspose
- convert image text
- extract text image
- extract korean text
- recognize korean text
language: cs
og_description: Naučte se, jak používat Aspose OCR k převodu textu z obrázku, extrahování
  korejského textu a rozpoznávání korejského textu z obrázků pomocí kompletního příkladu
  v C#.
og_title: Jak používat Aspose OCR – Rozpoznávejte korejský text v C#
tags:
- Aspose
- OCR
- C#
- Image Processing
title: Jak používat Aspose OCR v C# – Rozpoznávat korejský text z obrázků
url: /cs/net/text-recognition/how-to-use-aspose-ocr-in-c-recognize-korean-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat Aspose OCR v C# – Rozpoznat korejský text z obrázků

Už jste se někdy zamýšleli **jak používat Aspose** k získání korejských znaků z fotografie? Možná máte snímek obrazovky pouličního značení, naskenovaný účet nebo meme, které potřebujete převést na prohledávatelný text. Dobrou zprávou je, že Aspose OCR to dělá hračkou a nemusíte se zabývat nízkoúrovňovými triky pro zpracování obrazu.

V tomto tutoriálu projdeme **kompletní, spustitelný příklad**, který vám ukáže, jak **převést text z obrázku**, **extrahovat textový obrázek**, a konkrétně **extrahovat korejský text** pomocí knihovny Aspose OCR. Na konci budete mít konzolovou aplikaci, která vytiskne rozpoznaný korejský řetězec, a pochopíte, proč je každý řádek důležitý.

## Co budete potřebovat

- **.NET 6+** (jakékoli recentní .NET SDK funguje – Visual Studio, Rider nebo `dotnet` CLI)
- **Aspose.OCR for .NET** NuGet balíček  
  ```bash
  dotnet add package Aspose.OCR
  ```
- Soubor obrázku, který obsahuje korejské znaky (např. `korean_sign.jpg`).
- Trochu znalostí C# – pokud jste už napsali “Hello World”, jste připraveni.

> **Tip:** Aspose OCR podporuje více než 50 jazyků přímo z krabice. Zaměříme se na korejštinu, protože její skript Hangul často zaskočí obecné OCR enginy.

## Krok 1 – Instalace a odkaz na Aspose OCR

Nejprve přidejte knihovnu do svého projektu. NuGet příkaz výše udělá těžkou práci, ale pokud dáváte přednost UI, stačí vyhledat *Aspose.OCR* v NuGet Package Manageru.

```csharp
// No code needed here – the package reference is enough.
// The using directives below will bring the types into scope.
using Aspose.OCR;
using Aspose.OCR.Models;
```

> **Proč je to důležité:** `using` direktivy vám poskytují přístup k `OcrEngine`, `Language` a pomocné třídě `Image`. Bez nich by kompilátor stěžoval na neznámé typy.

## Krok 2 – Načtení obrázku, který chcete zpracovat

Aspose OCR pracuje s vlastním obalem `Image`, který dokáže číst JPEG, PNG, BMP a mnoho dalších formátů. Ukazujte ho na soubor, který obsahuje korejský text.

```csharp
// Step 2: Load the image containing Korean characters
var imagePath = Path.Combine(Environment.CurrentDirectory, "korean_sign.jpg");
var image = Image.Load(imagePath);
```

Pokud soubor není ve stejné složce jako váš spustitelný soubor, upravte cestu podle potřeby. Volání `Image.Load` provádí **převod textu z obrázku** do interní reprezentace, kterou OCR engine dokáže pochopit.

![příklad použití aspose OCR](/images/aspose-ocr-korean.png "jak použít aspose OCR k rozpoznání korejského textu")

*Alternativní text obrázku: “příklad použití aspose OCR ukazující korejské pouliční značení.”*

## Krok 3 – Nastavení OCR enginu pro korejštinu

Engine potřebuje vědět, který jazyk má hledat; jinak výchozí nastavení je angličtina a Hangul znaky budou chybět.

```csharp
// Step 3: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // Tell Aspose we want to recognize Korean (Hangul)
    Language = Language.Korean
};
```

> **Proč je to důležité:** Nastavení `Language = Language.Korean` říká engine načíst korejský jazykový balíček, což dramaticky zvyšuje přesnost pro Hangul glyfy. Přeskočení tohoto kroku často vede k nečitelnému výstupu.

## Krok 4 – Spuštění procesu rozpoznávání

Nyní skutečně požádáme Aspose o přečtení obrázku. Metoda `Recognize` vrací objekt `OcrResult`, který obsahuje extrahovaný řetězec a skóre důvěry.

```csharp
// Step 4: Run OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(image);
```

Pokud potřebujete **extrahovat textový obrázek** z větší fotografie (např. snímek obrazovky s více UI prvky), můžete nejprve oříznout oblast zájmu pomocí `image.Crop(...)` před voláním `Recognize`. To je užitečný trik, když vás zajímá jen konkrétní část obrázku.

## Krok 5 – Výstup rozpoznaného korejského textu

Nakonec zobrazte výsledek. V reálné aplikaci jej můžete uložit do databáze nebo předat překladovému API, ale pro tento tutoriál je výpis do konzole dostatečně jednoduchý.

```csharp
// Step 5: Print the recognized Korean text
Console.WriteLine("Recognized Korean text:");
Console.WriteLine(ocrResult.Text);
```

### Očekávaný výstup

```
Recognized Korean text:
서울특별시 강남구 테헤란로 123
```

Váš skutečný výstup bude samozřejmě odrážet jakékoli korejské znaky, které byly v souboru `korean_sign.jpg`.

## Kompletní funkční příklad

Níže je **kompletní program**, který můžete zkopírovat a vložit do nového konzolového projektu (`dotnet new console`). Ujistěte se, že soubor obrázku leží vedle zkompilovaného `.exe`, nebo upravte cestu.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Install Aspose.OCR via NuGet before running this code.

        // 2️⃣ Load the image that contains Korean text.
        var imagePath = Path.Combine(Environment.CurrentDirectory, "korean_sign.jpg");
        var image = Image.Load(imagePath);

        // 3️⃣ Create the OCR engine and set it to recognize Korean.
        var ocrEngine = new OcrEngine
        {
            Language = Language.Korean   // 👈 This enables Hangul support.
        };

        // 4️⃣ Run the OCR process.
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted Korean string.
        Console.WriteLine("Recognized Korean text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Spusťte program pomocí `dotnet run` a sledujte, jak se korejské znaky objeví ve vaší konzoli.

## Časté otázky a okrajové případy

### Co když OCR vrátí nečitelný text?

- **Zkontrolujte nastavení jazyka.** Zapomenutí `Language.Korean` je nejčastější chyba.
- **Zlepšete kvalitu obrazu.** Ostřejší obrázky, vyšší DPI a správné osvětlení zvyšují přesnost.
- **Předzpracujte obrázek.** Aspose OCR nabízí vestavěné filtry (`image.Binarize()`, `image.Deskew()`), které mohou vyčistit šumové skeny.

### Můžu **převést text z obrázku** hromadně?

Určitě. Zabalte výše uvedené kroky do smyčky `foreach`, která prochází složku s obrázky. Zde je rychlý úryvek:

```csharp
foreach (var file in Directory.GetFiles(@"C:\KoreanImages", "*.jpg"))
{
    var img = Image.Load(file);
    var result = ocrEngine.Recognize(img);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), result.Text);
}
```

Tento skript **extrahuje textový obrázek** z každého souboru a zapíše soubor `.txt` vedle něj.

### Jak zacházet s více jazyky na stejném obrázku?

Aspose OCR může automaticky detekovat jazyk, pokud nastavíte `Language = Language.Auto`. Nicméně automatická detekce může být pomalejší a mírně méně přesná než specifikování konkrétního jazyka. Pokud víte, že obrázek obsahuje jak korejštinu, tak angličtinu, můžete provést dva průchody – nejprve s `Language.Korean`, poté s `Language.English` – a výsledky spojit.

## Tipy pro produkčně připravené OCR

- **Ukládejte OcrEngine do cache.** Vytváření nového engine pro každý požadavek přidává režii. Používejte singleton, pokud zpracováváte mnoho obrázků.
- **Omezte velikost obrázku.** Velké obrázky spotřebovávají paměť; před předáním engine je zmenšete na ~1500 px šířky.
- **Zacházejte s výjimkami.** Zabalte volání `Recognize` do try/catch, aby se elegantně řešily poškozené soubory.

## Závěr

Právě jsme prošli **jak používat Aspose** k **převodu textu z obrázku**, **extrahování textového obrázku**, a konkrétně **extrahování korejského textu** pomocí několika řádků C# kódu. Kroky jsou jednoduché:

1. Nainstalujte Aspose OCR.  
2. Načtěte svůj obrázek.  
3. Nastavte engine pro korejštinu.  
4. Spusťte `Recognize`.  
5. Vypište výsledek.

Nyní můžete tento úryvek zapojit do větších pracovních toků – hromadné zpracování, archivaci dokumentů nebo dokonce aplikace pro překlad v reálném čase. Chcete jít dál? Zkuste přidat metody `Image.Preprocess()` od Aspose, experimentujte s různými jazyky nebo integrujte výstup s Azure Cognitive Services pro překlad.

Máte další otázky ohledně **rozpoznání korejského textu** nebo jiných funkcí Aspose? Zanechte komentář a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}