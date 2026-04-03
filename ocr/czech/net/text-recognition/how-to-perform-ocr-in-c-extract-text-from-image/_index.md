---
category: general
date: 2026-04-03
description: Naučte se provádět OCR v C# a extrahovat text z obrázku pomocí Aspose
  OCR, s kontrolou pravopisu pro ruštinu.
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- how to spell check
- ocr russian language
language: cs
og_description: Naučte se provádět OCR v C# a extrahovat text z obrázku pomocí Aspose
  OCR, s kontrolou pravopisu pro ruštinu.
og_title: Jak provést OCR v C# – Extrahovat text z obrázku
tags:
- OCR
- C#
- Aspose
- SpellCheck
title: Jak provést OCR v C# – Extrahovat text z obrázku
url: /cs/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provádět OCR v C# – Extrahovat text z obrázku

Už jste se někdy zamýšleli **jak provádět OCR** na fotografii ručně psané poznámky? Možná máte naskenovaný účtenku, ceduli v cizím jazyce nebo stránku PDF, která se nechce kopírovat‑vkládat. Dobrá zpráva? Několika řádky C# a knihovnou Aspose OCR můžete tu fotografii během chvilky proměnit v editovatelný text.

V tomto průvodci vám nejen ukážeme **jak provádět OCR**, ale také projdeme **extrahování textu z obrázku**, **převod obrázku na text** a dokonce **jak provést kontrolu pravopisu** výsledku, když pracujete s dokumenty v ruštině. Zní to jako hodně? Zůstaňte s námi – rozložíme vše krok po kroku.

## Co se naučíte

* Nastavit Aspose OCR pro podporu ruského jazyka.  
* Načíst soubor obrázku a spustit optické rozpoznávání znaků pro **extrahování textu z obrázku**.  
* Použít vestavěný kontroler pravopisu k automatické opravě překlepů – dokonalá odpověď na otázku “**jak provést kontrolu pravopisu**” výstupu OCR.  
* Vytisknout vyčištěný řetězec do konzole, připravený pro další zpracování nebo uložení.

**Požadavky** – budete potřebovat:

* .NET 6.0 nebo novější (kód funguje také s .NET Framework 4.8).  
* Platnou licenci Aspose OCR nebo dočasný evaluační klíč.  
* Soubor obrázku, který obsahuje ruský text (pro ukázku budeme používat `russian_note.jpg`).  

Pokud jsou některé z nich neznámé, žádný problém. Níže uvedené kroky obsahují přesný příkaz NuGet pro stažení Aspose OCR a kód je zcela samostatný.

![how to perform OCR example](/images/ocr-demo.png "how to perform OCR in C# example")

## Krok 1 – Instalace Aspose OCR a přidání jmenných prostorů

Nejprve potřebujete knihovnu. Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package Aspose.OCR
```

Tento příkaz stáhne nejnovější stabilní verzi (k dubnu 2026 je to 22.9). Po obnovení balíčku přidejte požadované `using` direktivy na začátek vašeho C# souboru:

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;
```

*Tip:* Pokud používáte Visual Studio, IDE vám tyto direktivy navrhne automaticky, jakmile napíšete první název třídy.

## Krok 2 – Inicializace OCR enginu pro ruský jazyk

Část **jak provádět OCR** začíná vytvořením instance `OcrEngine`. Zadáním `OcrLanguage.Russian` říkáme enginu, aby načetl cyrilický znakový soubor a jazykově specifické heuristiky.

```csharp
// Step 2: Initialise OCR engine for Russian
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Russian   // Enables Russian language support
};
```

Proč je to důležité? Bez nastavení jazyka engine výchozí nastavení používá angličtinu a bude špatně interpretovat mnoho cyrilických znaků, což vede k nečitelné výstupu. Explicitní nastavení jazyka výrazně zvyšuje přesnost.

## Krok 3 – Načtení obrázku a **převod obrázku na text**

Nyní načteme obrázek do paměti. Metoda `Image.FromFile` funguje s většinou běžných formátů (JPG, PNG, BMP). Po načtení zavoláme `Recognize` pro **převod obrázku na text**.

```csharp
// Step 3: Load the image that contains Russian text
Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

// Step 4: Perform OCR – this is the core “how to perform OCR” call
string rawText = ocrEngine.Recognize(sourceImage);
```

Proměnná `rawText` nyní obsahuje surový výstup OCR, který může stále obsahovat překlepy nebo špatně rozpoznané znaky. Můžete jej vytisknout, abyste viděli, co engine zachytil:

```csharp
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

## Krok 4 – **Jak provést kontrolu pravopisu** výsledku OCR

Ruské OCR může být hlučné, zejména u skenů s nízkým rozlišením. Aspose poskytuje třídu `SpellChecker`, která rozumí ruským slovníkům ihned po instalaci. Zde je, jak ji použít:

```csharp
// Step 5: Initialise the spell checker
SpellChecker spellChecker = new SpellChecker();

// Step 6: Correct spelling mistakes in the recognized text
string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);
```

Metoda `CheckAndCorrect` vrací nový řetězec, kde jsou špatně napsaná slova nahrazena nejpravděpodobnějšími správnými alternativami. Respektuje také interpunkci, takže nedostanete zeď textu.

*Hraniční případ:* Pokud je výstup OCR prázdný (např. obrázek je úplně bílý), `CheckAndCorrect` jednoduše vrátí prázdný řetězec. Je dobré se proti tomu chránit, pokud plánujete výsledek zapisovat do souboru.

## Krok 5 – Zobrazení vyčištěného výsledku

Nakonec vypíšeme opravený řetězec. V reálné aplikaci jej můžete zapisovat do databáze, JSON API nebo Word dokumentu. Pro tuto ukázku stačí výpis do konzole:

```csharp
// Step 7: Show the corrected result
Console.WriteLine("\nCorrected text:");
Console.WriteLine(correctedText);
```

Když spustíte program, měli byste vidět něco jako:

```
Raw OCR output:
Привeт мир! Этo тeкcт c русcкoй оcнoвнoй.

Corrected text:
Привет мир! Это текст с русской основой.
```

Všimněte si, jak kontrola pravopisu změnila “Привeт” (smíšené latinské ‘e’) na správné cyrilické “Привет”. To je kouzlo **jak provést kontrolu pravopisu** výstupu OCR.

## Kompletní funkční příklad

Níže je kompletní spustitelný program, který spojuje všechny kroky. Zkopírujte jej do nového konzolového projektu a stiskněte **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine configured for Russian language
        OcrEngine ocrEngine = new OcrEngine { Language = OcrLanguage.Russian };

        // Step 2: Load the image that contains the text to be recognized
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

        // Step 3: Perform OCR to extract raw text from the image
        string rawText = ocrEngine.Recognize(sourceImage);

        // Optional: Show raw OCR output
        System.Console.WriteLine("Raw OCR output:");
        System.Console.WriteLine(rawText);

        // Step 4: Initialise the spell checker
        SpellChecker spellChecker = new SpellChecker();

        // Step 5: Correct spelling mistakes in the recognized text
        string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);

        // Step 6: Display the corrected result
        System.Console.WriteLine("\nCorrected text:");
        System.Console.WriteLine(correctedText);
    }
}
```

### Očekávaný výstup

Spuštění programu s čistou, vysoké rozlišení fotografií ruského rukopisu obvykle poskytne čistou, čitelnou větu. Pokud je obrázek rozmazaný, můžete stále získat částečně správná slova, ale kontrola pravopisu vyhladí většinu zjevných chyb.

## Časté problémy a tipy

| Problém | Proč se to děje | Jak opravit / vyhnout se |
|-------|----------------|--------------------|
| **Špatné znaky** | Nízké DPI nebo špatné pozadí | Předzpracujte obrázek (zvyšte kontrast, změňte velikost na ≥300 dpi) před předáním do `Recognize`. |
| **Prázdný výstup** | Špatná cesta k souboru nebo nepodporovaný formát | Ověřte cestu a použijte `Image.FromFile` uvnitř `try/catch` bloku pro zobrazení chyb. |
| **Kontrola pravopisu neodhalí chyby** | Vzácná slova nejsou ve slovníku | Rozšiřte slovník načtením vlastního seznamu slov pomocí `spellChecker.AddUserDictionary("mywords.txt")`. |
| **Zpoždění výkonu při velkých dávkách** | OCR je náročné na CPU | Spusťte OCR na pozadí nebo použijte `Parallel.ForEach` pro více obrázků. |
| **Výjimka licence** | Použití evaluační verze po uplynutí zkušební doby | Zakupte licenci a zavolejte `License license = new License(); license.SetLicense("Aspose.Total.lic");` před vytvořením `OcrEngine`. |

## Další kroky – Pokročilejší OCR

Nyní, když jste zvládli **jak provádět OCR**, zvažte tyto rozšíření:

* **Dávkové zpracování** – Procházet složku s obrázky a zapisovat každý opravený text do souboru `.txt`.  
* **Konverze PDF** – Použít Aspose PDF k vložení extrahovaného textu zpět do prohledávatelného PDF.  
* **Detekce jazyka** – Pokud potřebujete zpracovávat více jazyků, nejprve prozkoumejte výstup OCR a podle toho přepněte `OcrLanguage`.  
* **Integrace s Azure Cognitive Services** – Porovnat výsledky Aspose s OCR API od Microsoftu pro hybridní přístup.

Všechny tyto témata přirozeně zahrnují sekundární klíčová slova **extract text from image**, **convert image to text**, a **how to spell check**, takže

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}