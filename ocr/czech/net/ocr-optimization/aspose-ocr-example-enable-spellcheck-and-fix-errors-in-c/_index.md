---
category: general
date: 2026-03-07
description: Příklad Aspose OCR ukazující, jak povolit kontrolu pravopisu, přidat
  vlastní slovník, načíst OCR z obrázku a rychle opravit chyby OCR.
draft: false
keywords:
- aspose ocr example
- how to enable spellcheck
- how to add dictionary
- load image ocr
- how to fix ocr errors
language: cs
og_description: Příklad Aspose OCR, který vás provede povolením kontroly pravopisu,
  přidáním vlastního slovníku, načtením obrázku pro OCR a opravou běžných chyb OCR.
og_title: Příklad Aspose OCR – Povolit kontrolu pravopisu a opravit chyby
tags:
- Aspose
- OCR
- C#
- SpellCheck
title: Příklad Aspose OCR – Povolit kontrolu pravopisu a opravit chyby v C#
url: /cs/net/ocr-optimization/aspose-ocr-example-enable-spellcheck-and-fix-errors-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Example – Enable Spellcheck and Fix Errors in C#

Už jste někdy potřebovali **Aspose OCR example**, který nejen načte text z obrázku, ale také odstraní ty otravné pravopisné chyby? Nejste v tom sami. V mnoha reálných projektech je surový výstup OCR posetý překlepy, zejména když zdrojový obrázek obsahuje nízkokontrastní písmo nebo ručně psané poznámky.  

Dobrá zpráva? S Aspose.OCR můžete **enable spellcheck**, připojit vlastní slovník a získat upravený řetězec během několika řádků kódu. Níže uvidíte přesně **how to enable spellcheck**, **how to add a dictionary** a **how to load image OCR**, takže konečně **fix OCR errors** bez toho, abyste si trhali vlasy.

V tomto tutoriálu pokryjeme vše, co potřebujete – od instalace NuGet až po kompletní spustitelný program, který vypíše opravený text. Na konci budete mít solidní **Aspose OCR example**, který můžete vložit přímo do jakéhokoli .NET projektu.

## Požadavky

- .NET 6.0 SDK nebo novější (kód funguje také s .NET Core a .NET Framework)
- Visual Studio 2022 nebo jakékoli C#‑kompatibilní IDE
- Soubor obrázku (`typed_text.png`) obsahující jasný, psaný anglický text
- Přístup k internetu pro stažení NuGet balíčku Aspose.OCR

Žádné další knihovny třetích stran nejsou vyžadovány.

---

## Step 1 – Install the Aspose.OCR NuGet Package (Load Image OCR)

Než budeme moci psát jakýkoli kód, potřebujeme knihovnu, která pohání OCR engine.

```bash
dotnet add package Aspose.OCR
```

> **Tip:** Pokud používáte Visual Studio, klikněte pravým tlačítkem na projekt → *Manage NuGet Packages* → vyhledejte **Aspose.OCR** a klikněte na *Install*.  

Instalace balíčku vám poskytne přístup k `OcrEngine`, `ImageStream` a vestavěným utilitám pro kontrolu pravopisu, které později použijeme. Jakmile je balíček na místě, jste připraveni na **load image OCR**.

## Step 2 – Create the OCR Engine Instance

Vytvoření engine je první konkrétní krok v jakémkoli **Aspose OCR example**. Představte si `OcrEngine` jako mozek, který analyzuje bitmapu a vydá text.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Step 2: Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

Konstruktor `OcrEngine` nevyžaduje žádné parametry, což jej činí přehledným pro rychlé prototypy.

## Step 3 – How to Enable Spellcheck (and Why It Matters)

Surový výstup OCR často obsahuje nesprávně rozpoznaná slova jako “teh” místo “the”. Povolení vestavěného spell‑checkeru umožní Aspose automaticky nahradit tyto chyby nejpravděpodobnějším správným pravopisem.

```csharp
// Step 3: Turn on spell checking and set the language to English
ocrEngine.Settings.SpellCheck.Enabled = true;
ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;
```

> **Proč povolit spellcheck?**  
> - **Přesnost:** Post‑processing spell check může zvýšit celkovou přesnost textu o 10‑15 % u tištěných dokumentů.  
> - **Uživatelská zkušenost:** Čistý text znamená méně následného čištění, když výsledek předáváte do vyhledávacích indexů nebo analytických pipeline.

## Step 4 – How to Add a Dictionary (Custom Words)

Někdy výchozí slovník nezná vaše značkové názvy, kódy produktů nebo oborový žargon. Právě zde vstupuje do hry **how to add dictionary**.

```csharp
// Step 4: Add custom words that the spell checker should accept
ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
{
    "AsposeOCR",   // our library name
    "OCRify",      // a fictional product
    "CSharpify"    // another custom term
});
```

Můžete předat pole, seznam nebo dokonce načíst ze souboru, pokud máte velké vlastní slovní zásoby. Spell‑checker nyní bude tyto položky považovat za platné, čímž zabrání chybným opravám.

## Step 5 – Load the Image for OCR (Load Image OCR)

Nyní, když je engine nakonfigurován, musíme ho nasměrovat na obrázek, který chceme přečíst. Pomocník `ImageStream.FromFile` abstrahuje podrobnosti čtení souboru.

```csharp
// Step 5: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");
```

> **Tip:** Pokud se váš obrázek nachází v podadresáři projektu, nastavte jeho vlastnost *Copy to Output Directory* na *Copy always*, aby cesta byla vyřešena za běhu.

## Step 6 – Perform Recognition and Fix OCR Errors

S vším nastaveným, jediným voláním `Recognize()` spustíte OCR pipeline, použijete spell‑checking a uložíte vyčištěný výsledek do `ocrEngine.Text`.

```csharp
// Step 6: Run OCR and let the spell checker clean the output
ocrEngine.Recognize();

// Step 7: Output the corrected text to the console
Console.WriteLine("Corrected text:");
Console.WriteLine(ocrEngine.Text);
```

### Očekávaný výstup

Předpokládejme, že `typed_text.png` obsahuje větu `The quick brown fox jumps over teh lazy dog`, konzole zobrazí:

```
Corrected text:
The quick brown fox jumps over the lazy dog
```

Všimněte si, že “teh” bylo automaticky opraveno na “the”. Kdybyste přidali “OCRify” do vlastního slovníku a obrázek by obsahoval toto slovo, engine by ho ponechal beze změny.

---

## Kompletní funkční příklad (připravený ke kopírování a vložení)

Níže je kompletní program, který můžete vložit do nového konzolového projektu. Obsahuje všechny výše uvedené kroky a několik komentářů pro přehlednost.

```csharp
// ---------------------------------------------------------------
// Aspose OCR Example – Enable Spellcheck and Fix Errors
// ---------------------------------------------------------------

using System;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable spell checking (how to enable spellcheck)
            ocrEngine.Settings.SpellCheck.Enabled = true;
            ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;

            // 3️⃣ Add custom words (how to add dictionary)
            ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
            {
                "AsposeOCR",
                "OCRify",
                "CSharpify"
            });

            // 4️⃣ Load the image (load image OCR)
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");

            // 5️⃣ Run OCR – this also fixes common OCR errors (how to fix ocr errors)
            ocrEngine.Recognize();

            // 6️⃣ Show the corrected result
            Console.WriteLine("Corrected text:");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

Uložte to jako `Program.cs`, spusťte `dotnet run` a měli byste vidět opravenou větu vytištěnou v konzoli.

---

## Často kladené otázky a okrajové případy

| Question | Answer |
|----------|--------|
| **Co když je obrázek vícestránkový PDF?** | Aspose.OCR dokáže zpracovat stránky PDF jako obrázky. Použijte `ocrEngine.Image = ImageStream.FromPdf("file.pdf", pageNumber: 1);` a projděte stránky ve smyčce. |
| **Mohu změnit jazyk na jiný než angličtinu?** | Rozhodně. Nastavte `ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.French;` (nebo jakýkoli podporovaný jazyk). |
| **Můj vlastní slovník je obrovský—ovlivní to výkon?** | Přidání tisíců slov vyžaduje malou počáteční náročnost, ale vyhledávání je O(1) díky hash‑setu pod kapotou. Pro obrovské slovníky zvažte načtení jednorázově při startu aplikace. |
| **Co když OCR engine vyhodí výjimku u poškozeného obrázku?** | Zabalte `Recognize()` do try‑catch bloku a prozkoumejte `ocrEngine.LastError`. Můžete také předem ověřit rozměry obrázku pomocí `ocrEngine.Image.Width` a `Height`. |
| **Potřebuji licenci pro produkční použití?** | Bezplatná evaluační verze funguje pro testování, ale komerční licence odstraňuje vodoznak evaluace a odemyká plný výkon. |

---

## Závěr

Nyní máte **complete Aspose OCR example**, který ukazuje **how to enable spellcheck**, **how to add a dictionary**, **load image OCR** a **how to fix OCR errors** čistým, připraveným pro produkci způsobem. Konfigurací spell‑checkeru a zadáním vlastního seznamu slov výrazně zlepšíte kvalitu extrahovaného textu, aniž byste museli psát jakoukoli post‑processing logiku.

Jste připraveni na další krok? Zkuste změnit jazyk na španělštinu, načíst vícestránkový PDF nebo integrovat výstup do vyhledávatelného indexu Azure Cognitive Search. Stejný vzor platí – jen upravte jazykový příznak a možná rozšiřte vlastní slovník.

Pokud vám tento průvodce přišel užitečný, dejte mu hvězdičku na GitHubu, sdílejte ho s kolegy nebo zanechte komentář níže. Šťastné programování a ať jsou vaše OCR výsledky vždy bez chyb!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}