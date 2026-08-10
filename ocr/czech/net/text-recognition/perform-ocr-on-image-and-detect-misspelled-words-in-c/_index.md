---
category: general
date: 2026-06-03
description: Proveďte OCR na obrázku a extrahujte text z obrázku pomocí Aspose.OCR.
  Naučte se, jak detekovat chybně napsaná slova a získat návrhy na opravu pravopisu
  v jednom C# demu.
draft: false
keywords:
- perform OCR on image
- extract text from image
- detect misspelled words
- get spelling suggestions
- how to extract text
language: cs
og_description: Proveďte OCR na obrázku, abyste extrahovali text, poté detekujte nesprávně
  napsaná slova a získejte návrhy pravopisu pomocí Aspose.OCR v C#.
og_title: Provést OCR na obrázku a detekovat pravopisně nesprávná slova v C#
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Perform OCR on image and extract text from image using Aspose.OCR.
    Learn how to detect misspelled words and get spelling suggestions in a single
    C# demo.
  headline: Perform OCR on Image and Detect Misspelled Words in C#
  type: TechArticle
tags:
- Aspose OCR
- C#
- Spell Checking
title: Proveďte OCR na obrázku a detekujte pravopisně chybné slova v C#
url: /cs/net/text-recognition/perform-ocr-on-image-and-detect-misspelled-words-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Proveďte OCR na obrázku a detekujte pravopisné chyby v C#

Už jste se někdy zamysleli, jak **perform OCR on image** soubory bez toho, aby vám to vytrhávalo vlasy? Nejste jediní. Ať už digitalizujete staré dopisy, skenujete účtenky nebo budujete inteligentní workflow dokumentů, získání čistého textu z obrázků je první překážkou. Dobrá zpráva? S Aspose.OCR můžete během několika minut vytvořit řešení a navíc můžete také **detect misspelled words** a **get spelling suggestions** během jednoho běhu.

V tomto tutoriálu vás provedeme kompletní, připravenou k spuštění C# konzolovou aplikací, která **extracts text from image**, spustí anglický spell‑checker a vytiskne každou chybu s užitečnými návrhy oprav. Na konci přesně budete vědět **how to extract text**, jak připojit spell‑check API a jak vypadá očekávaný výstup v konzoli.

## Co vytvoříte

- Načtěte bitmapu (nebo PNG), která obsahuje typografické chyby.  
- Spusťte Aspose.OCR k **perform OCR on image** a získejte surová data řetězce.  
- Inicializujte vestavěný anglický spell‑checker.  
- **Detect misspelled words** a **get spelling suggestions** pro každé.  
- Vytiskněte přehledný report do konzole.

Žádné externí služby, žádné komplikované HTTP volání – jen jediný NuGet balíček a několik řádků kódu.

## Požadavky

- .NET 6.0 SDK nebo novější (kód také funguje na .NET Framework 4.7+).  
- Visual Studio 2022 (nebo jakýkoli editor, který máte rádi).  
- Aspose.OCR pro .NET NuGet balíček (`Aspose.OCR`).  
- Obrázkový soubor (`letter_with_typos.png`) umístěný na místě, na které můžete odkazovat z projektu.

Pokud jste ještě nikdy nepoužili Aspose, nebojte se – instalace balíčku je tak jednoduchá jako spuštění:

```bash
dotnet add package Aspose.OCR
```

Nyní se ponořme do implementace.

## Krok 1: Nastavte projekt a nainstalujte Aspose.OCR

Vytvořte nový konzolový projekt a přidejte OCR knihovnu:

```bash
dotnet new console -n OcrSpellDemo
cd OcrSpellDemo
dotnet add package Aspose.OCR
```

Po dokončení obnovení otevřete `Program.cs`. Později nahradíme výchozí obsah plným demonstračním kódem, ale nejprve si povíme, proč je každý jmenný prostor důležitý.

- `Aspose.OCR` – jádro OCR enginu a zpracování obrázků.  
- `Aspose.OCR.SpellCheck` – nástroje pro pravopisnou kontrolu, které jsou součástí knihovny.  
- `System` – standardní .NET základní třídy (např. `Console`).

## Krok 2: Načtěte obrázek a proveďte OCR na obrázku

První skutečná práce je předat obrázek OCR enginu. Aspose.OCR čte mnoho formátů (PNG, JPEG, TIFF). Zde je úryvek, který dělá těžkou práci:

```csharp
// Step 2: Load the image that contains the text to be recognized
var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

// Step 3: Perform OCR to extract the raw text from the image
var ocrEngine = new OcrEngine();
var ocrResult = ocrEngine.Recognize(image);
```

> **Proč je to důležité:** `OcrImage.FromFile` abstrahuje podrobnosti na úrovni pixelů, zatímco `OcrEngine.Recognize` spouští natrénovaný neuronový model, který převádí vizuální glyfy na Unicode znaky. Vlastnost `ocrResult.Text` nyní obsahuje surový řetězec – přesně to, co potřebujete k **extract text from image**.  
> **Tip:** Pokud váš obrázek obsahuje více jazyků, můžete před voláním `Recognize` nastavit `ocrEngine.Language = OcrLanguage.Multilingual;`.

## Krok 3: Inicializujte anglický Spell‑Checker

Aspose.OCR obsahuje vestavěný engine pro pravopisnou kontrolu, který rozumí angličtině ihned po instalaci. Jeho inicializace je jednorázová:

```csharp
// Step 4: Initialise the English spell‑checker
var spellChecker = new SpellChecker(OcrLanguage.English);
```

> **Proč je tento krok zásadní:** Výstup OCR může obsahovat nesprávně rozpoznané znaky (např. „l“ vs „1“) nebo skutečné překlepy ze zdrojového dokumentu. Spell‑checker prohledá řetězec, najde podezřelé tokeny a navrhne alternativy.

## Krok 4: Detekujte pravopisné chyby a získejte návrhy oprav

Nyní předáme OCR text kontroleru:

```csharp
// Step 5: Check the recognized text for misspelled words and obtain suggestions
var misspellings = spellChecker.Check(ocrResult.Text);
```

`misspellings` je kolekce, kde každý záznam obsahuje chybné slovo a pole možných oprav.

## Krok 5: Výstup výsledků

Nakonec projdeme kolekci a vytiskneme čitelný report:

```csharp
// Step 6: Output each misspelled word together with its suggested corrections
foreach (var entry in misspellings)
{
    Console.WriteLine($"Misspelled: {entry.Word}");
    Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
}
```

### Očekávaný výstup v konzoli

Předpokládejme, že `letter_with_typos.png` obsahuje větu:

```
Ths is an exampel of a lettter with som misspelled wrds.
```

Spuštěním dema získáte něco jako:

```
Misspelled: Ths
  Suggestions: This, Thus, The
Misspelled: exampel
  Suggestions: example, exemplar, exampell
Misspelled: lettter
  Suggestions: letter, litter, lett
Misspelled: som
  Suggestions: some, sum, son
Misspelled: wrds
  Suggestions: words, wards, wryds
```

## Kompletní funkční příklad

Níže je **kompletní, připravený ke zkopírování** program. Nahraďte `YOUR_DIRECTORY` skutečnou cestou k vašemu obrázku.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Load the image that contains the text to be recognized
        var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

        // Step 2: Perform OCR to extract the raw text from the image
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(image);

        // Step 3: Initialise the English spell‑checker
        var spellChecker = new SpellChecker(OcrLanguage.English);

        // Step 4: Check the recognized text for misspelled words and obtain suggestions
        var misspellings = spellChecker.Check(ocrResult.Text);

        // Step 5: Output each misspelled word together with its suggested corrections
        foreach (var entry in misspellings)
        {
            Console.WriteLine($"Misspelled: {entry.Word}");
            Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
        }

        // Optional: Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

> **Okrajové případy k úvaze**  
> - **Prázdný obrázek:** Pokud OCR engine vrátí prázdný řetězec, `spellChecker.Check` jednoduše vrátí prázdnou kolekci – žádná havárie.  
> - **Neanglický text:** Vyměňte `OcrLanguage.English` za `OcrLanguage.French` (nebo jakýkoli podporovaný jazyk), abyste **detect misspelled words** v jiných locale.  
> - **Velké dokumenty:** Pro více‑stránkové PDF byste prošli každou stránku, provedli OCR a poté agregovali výsledky před pravopisnou kontrolou.

## Vizualizace (Alt text obrázku)

![Diagram zobrazující tok provedení OCR na obrázku, extrakci textu z obrázku a následnou detekci pravopisných chyb s návrhy oprav](perform-ocr-on-image-flow.png)

*Diagram výše ilustruje kompletní pipeline: obrázek → OCR engine → surový text → spell‑checker → návrhy.*

## Časté otázky a tipy

| Question | Answer |
|----------|--------|
| **Potřebuji internetové připojení?** | Ne. Aspose.OCR běží zcela lokálně; ideální pro offline nebo zabezpečená prostředí. |
| **Jak přesný je spell‑checker?** | Používá slovník přibližně 150 000 anglických slov a fuzzy porovnávání, takže většina běžných překlepů je zachycena. |
| **Mohu si přizpůsobit slovník?** | Ano. `SpellChecker.AddUserDictionary("custom.txt")` vám umožní načíst termíny specifické pro doménu (např. názvy produktů). |
| **Co když je obrázek nakřivený?** | OCR engine automaticky detekuje orientaci, ale v obtížných případech můžete ručně zavolat `ocrEngine.ImagePreprocessing.Rotate(angle)`. |
| **Existuje způsob, jak zvýraznit návrhy v UI?** | Po získání kolekce `misspellings` můžete mapovat každé `entry.Word` zpět na jeho pozici v `ocrResult.Text` a podtrhnout jej v RichTextBoxu nebo webovém zobrazení. |

## Závěr

Právě jsme vám ukázali **how to perform OCR on image**, **extract text from image**, a pak **detect misspelled words** při **getting spelling suggestions** – vše pomocí stručné C# konzolové aplikace. Základní myšlenka je jednoduchá: nechte Aspose.OCR udělat těžkou práci rozpoznávání znaků a nechte jeho vestavěný spell‑checker vyčistit výstup. Odtud můžete rozšířit demo na plnohodnotnou službu zpracování dokumentů, integrovat ji s webovým API nebo zapojit do desktopového editoru.

Jste připraveni na další krok? Zkuste změnit jazyk na španělštinu, načíst více‑stránkový PDF, nebo vytvořit malý WPF front‑end, který uživatelům umožní kliknout na slovo a přijmout návrh. Stavební bloky už jsou na místě – jen dál experimentujte.

Pokud narazíte na problémy nebo máte nápady na rozšíření, zanechte komentář níže. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Extrahovat text z obrázku v C# s výběrem jazyka pomocí Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extrahovat text z obrázku pomocí Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extrahovat text z obrázku – optimalizace OCR s Aspose.OCR pro .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}