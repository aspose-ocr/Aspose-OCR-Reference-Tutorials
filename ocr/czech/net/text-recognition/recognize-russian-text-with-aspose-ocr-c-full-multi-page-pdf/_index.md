---
category: general
date: 2026-01-01
description: Okamžitě rozpoznávejte ruský text pomocí Aspose OCR C#. Naučte se rozpoznávat
  čínský text, číst počet stránek PDF a převádět text stránek PDF v jednom tutoriálu.
draft: false
keywords:
- recognize russian text
- aspose ocr c#
- recognize chinese text
- read pdf page count
- convert pdf page text
language: cs
og_description: Rychle rozpoznávejte ruský text pomocí Aspose OCR C#. Tento tutoriál
  také pokrývá, jak rozpoznat čínský text, zjistit počet stránek PDF a převést text
  stránek PDF.
og_title: Rozpoznání ruského textu pomocí Aspose OCR C# – Kompletní průvodce
tags:
- Aspose OCR
- C#
- PDF processing
title: Rozpoznat ruský text pomocí Aspose OCR C# – Kompletní průvodce vícestránkovým
  PDF
url: /cs/net/text-recognition/recognize-russian-text-with-aspose-ocr-c-full-multi-page-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznání ruského textu pomocí Aspose OCR C# – kompletní návod pro více‑stránkové PDF

Už jste někdy potřebovali **rozpoznat ruský text** v PDF, které míchá jazyky, a přemýšleli, jak to udělat, aniž byste museli tahat samostatný nástroj pro každou stránku? Nejste v tom sami. V mnoha reálných projektech narazíte na jediný PDF, který obsahuje angličtinu, ruštinu a dokonce čínštinu na různých stránkách, a přesto chcete mít jeden čistý textový výstup.

V tomto průvodci vám ukážeme, jak **rozpoznat ruský text** (a další jazyky) pomocí **Aspose OCR C#**, a zároveň demonstrujeme, jak **číst počet stránek PDF**, **rozpoznat čínský text** a **převést text stránky PDF** do praktického výpisu v konzoli. Žádné externí služby, žádné skryté kroky — jen čistý C# kód, který můžete zkopírovat a spustit.

> **Co si z toho odnesete**  
> * Spustitelná C# konzolová aplikace, která zpracuje více‑stránkové PDF.  
> * Výběr jazyka po stránce (ruština, čínština, angličtina).  
> * Techniky pro získání počtu stránek PDF a extrakci textu z každé stránky.  
> * Tipy, úskalí a rozšíření, která můžete použít ve svých projektech.

---

## Požadavky

- .NET 6.0 nebo novější (kód funguje také na .NET Framework 4.7+).  
- **Aspose.OCR for .NET** NuGet balíček nainstalovaný (`dotnet add package Aspose.OCR`).  
- PDF soubor, který obsahuje smíšené jazyky; pro ukázku budeme odkazovat na `mixed_lang.pdf`.  
- Základní znalost C# konzolových aplikací.

Pokud vám něco chybí, stáhněte si nejnovější Aspose OCR z NuGet a umístěte PDF do složky, která je přístupná z kořenového adresáře projektu.

---

## Krok 1 – Inicializace Aspose OCR Engine

První věc, kterou potřebujete, je instance `OcrEngine`. Tento objekt obsahuje všechna nastavení (např. jazyk) a provádí těžkou práci.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class MultiPageDemo
{
    static void Main()
    {
        // Create the OCR engine – this is where we’ll set language per page
        OcrEngine ocrEngine = new OcrEngine();
```

> **Proč je to důležité:**  
> Engine je znovu použitelný, takže neplýtváme pamětí vytvářením nové instance pro každou stránku. Opětovné použití také umožňuje měnit jazyk za běhu, což je nezbytné pro **rozpoznání ruského textu** na jedné stránce a **rozpoznání čínského textu** na jiné.

---

## Krok 2 – Načtení PDF a zjištění počtu stránek

Než začneme rozpoznávat, potřebujeme PDF objekt a jeho počet stránek. Aspose OCR zachází s každou stránkou jako s `OcrImage`.

```csharp
        // Load the multi‑page PDF
        OcrImage multiPageImage = OcrImage.FromFile(@"YOUR_DIRECTORY/mixed_lang.pdf");

        // Print the total number of pages – this answers the “read pdf page count” question
        Console.WriteLine($"PDF contains {multiPageImage.PageCount} pages.");
```

> **Tip:** Pokud je PDF obrovské, můžete si nejprve přečíst počet stránek a rozhodnout, zda zpracujete všechny stránky nebo jen podmnožinu.

---

## Krok 3 – Přiřazení každé stránky požadovanému jazyku

Aspose OCR podporuje mnoho jazyků, ale musíte mu říct, který použít pro kterou stránku. Níže vytvoříme `Dictionary<int, OcrLanguage>`, kde klíč je index stránky od nuly.

```csharp
        // Define which language each page should be read with
        var languageMap = new Dictionary<int, OcrLanguage>
        {
            { 0, OcrLanguage.English },   // Page 1 – English
            { 1, OcrLanguage.Russian },   // Page 2 – Russian (our primary focus)
            { 2, OcrLanguage.Chinese }    // Page 3 – Chinese
        };
```

> **Proč je to klíčové:**  
> Bez tohoto mapování by OCR engine zkoušel jeden výchozí jazyk pro všechny stránky, což by vedlo k nečitelné výstupní podobě ruského nebo čínského textu. Tento krok přímo umožňuje **rozpoznat ruský text** a **rozpoznat čínský text** správně.

---

## Krok 4 – Procházení všech stránek, nastavení jazyka a rozpoznání textu

Nyní iterujeme přes každou stránku, přepínáme jazyk podle našeho mapování a voláme `Recognize`. Výsledek je uložen v `OcrResult`, ze kterého získáme čistý text.

```csharp
        // Process each page one by one
        for (int pageIndex = 0; pageIndex < multiPageImage.PageCount; pageIndex++)
        {
            // Choose language – default to English if we haven’t specified one
            ocrEngine.Settings.Language = languageMap.ContainsKey(pageIndex)
                                          ? languageMap[pageIndex]
                                          : OcrLanguage.English;

            // Perform OCR on the current page
            var pageResult = ocrEngine.Recognize(multiPageImage.GetPage(pageIndex));

            // Output the recognized text – this is the “convert pdf page text” step
            Console.WriteLine($"--- Page {pageIndex + 1} ({ocrEngine.Settings.Language}) ---");
            Console.WriteLine(pageResult.Text);
            Console.WriteLine(); // Blank line for readability
        }
    }
}
```

### Očekávaný výstup v konzoli

```
PDF contains 3 pages.
--- Page 1 (English) ---
This is an English paragraph on the first page.

--- Page 2 (Russian) ---
Это русский текст на второй странице.

--- Page 3 (Chinese) ---
这是第三页的中文文本。
```

> **Vysvětlení postupu:**  
> * Smyčka respektuje **čtení počtu stránek PDF**, který jsme vypsali dříve.  
> * Přepínáním `ocrEngine.Settings.Language` v každé iteraci zajišťujeme přesné **rozpoznání ruského textu** na stránce 2 a **rozpoznání čínského textu** na stránce 3.  
> * Příkazy `Console.WriteLine` efektivně **převádějí text stránky PDF** na lidsky čitelný řetězec.

---

## Krok 5 – Spuštění, ověření a ladění

1. Sestavte projekt (`dotnet build`).  
2. Spusťte jej (`dotnet run`).  
3. Porovnejte výstup v konzoli s originálním PDF.  

Pokud zaznamenáte chybějící znaky, zvažte:

- **Zvýšení přesnosti OCR** nastavením `ocrEngine.Settings.DetectTextOrientation = true;`.  
- **Poskytnutí vlastního jazykového balíčku**, pokud jsou vestavěné slovníky pro ruštinu nebo čínštinu zastaralé.  
- **Úpravu DPI** při načítání PDF (`OcrImage.FromFile(path, 300)`), což může zlepšit rozpoznání u nízkokvalitních skenů.

---

## Bonus: Řešení okrajových případů

### Co když jazyk stránky není v mapě?

Kód již přepne na angličtinu, ale můžete také přidat záložní řešení, které zaznamená varování:

```csharp
if (!languageMap.TryGetValue(pageIndex, out var lang))
{
    Console.WriteLine($"Warning: No language defined for page {pageIndex + 1}. Using English.");
    lang = OcrLanguage.English;
}
ocrEngine.Settings.Language = lang;
```

### Můžeme zpracovávat PDF s více než třemi jazyky?

Ano. Rozšiřte `languageMap` o další indexy a podporované hodnoty `OcrLanguage` (např. `OcrLanguage.French`). Smyčka zvládne libovolný počet stránek.

### Jak exportovat výsledky do souboru místo konzole?

Nahraďte volání `Console.WriteLine` příkazem `File.AppendAllText("output.txt", …)` nebo použijte `StringBuilder`, který zapíšete jednorázově po skončení smyčky.

---

## Ilustrační obrázek

![příklad rozpoznání ruského textu](/images/recognize-russian-text.png "Snímek obrazovky ukazující výstup OCR pro ruský text")

*Obrázek výše demonstruje výstup v konzoli, když je provedeno **rozpoznání ruského textu** na PDF s více jazyky.*

---

## Závěr

Prošli jsme kompletním příkladem, který ukazuje, jak **rozpoznat ruský text** (a také **rozpoznat čínský text**) z více‑stránkového PDF pomocí **Aspose OCR C#**. Čtením počtu stránek PDF, mapováním každé stránky na správný jazyk a iterací přes dokument můžete **převést text stránky PDF** na čisté řetězce připravené k uložení, indexaci nebo dalšímu zpracování.

Stručně:

- **Inicializujte** jediný `OcrEngine`.  
- **Načtěte** PDF a **přečtěte počet stránek PDF**.  
- **Namapujte** stránky na jazyky (ruština, čínština, atd.).  
- **Iterujte**, nastavte `ocrEngine.Settings.Language` a **rozpoznávejte** každou stránku.  
- **Vypište** nebo uložte extrahovaný text.

Neváhejte tento vzor přizpůsobit větším dokumentům, přidat ošetření chyb nebo propojit výsledky s vyhledávacím indexem. Hlavní myšlenka — výběr jazyka po stránce — zůstává stejná a umožňuje spolehlivé **rozpoznání ruského textu** v PDF s více jazyky.

Máte jiný scénář, například skenování obrázků místo PDF? Ten samý engine funguje; stačí nahradit `OcrImage.FromFile` za `OcrImage.FromStream` nebo `FromBitmap`. Šťastné programování a ať je vaše OCR vždy přesná!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}