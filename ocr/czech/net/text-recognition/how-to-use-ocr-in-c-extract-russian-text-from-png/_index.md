---
category: general
date: 2026-02-20
description: jak použít OCR v C# k načtení textu z PNG obrázků – naučte se převést
  obrázek na text a rychle extrahovat ruský text
draft: false
keywords:
- how to use ocr
- read text from png
- convert image to text
- recognize image text
- extract russian text
language: cs
og_description: Jak používat OCR v C# je vysvětleno v první větě – krok za krokem
  průvodce čtením textu z PNG, převodem obrázku na text a extrakcí ruského textu.
og_title: Jak používat OCR v C# – kompletní průvodce
tags:
- OCR
- C#
- Aspose
title: jak použít OCR v C# – Extrahovat ruský text z PNG
url: /cs/net/text-recognition/how-to-use-ocr-in-c-extract-russian-text-from-png/
---

" we keep.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak použít OCR v C# – Extrahovat ruský text z PNG

Už jste se někdy zamýšleli **jak použít OCR** v .NET projektu, aniž byste strávili týdny hledáním správné knihovny? Nejste v tom sami. V mnoha reálných aplikacích potřebujeme **číst text z PNG** souborů, převést tyto obrázky na prohledávatelné řetězce a někdy vytáhnout cyrilické znaky pro zpracování ruského jazyka.

V tomto tutoriálu vás provedeme praktickým příkladem, který vám přesně ukáže, jak **převést obrázek na text** pomocí Aspose.OCR, a poté **rozpoznat text na obrázku**, který je napsán v ruštině. Na konci budete mít připravený spustitelný konzolový program, který **extrahuje ruský text** z PNG souboru, a také několik tipů na okrajové případy, na které můžete později narazit.

---

## Co budete potřebovat

- .NET 6 SDK nebo novější (kód funguje také na .NET Core 3.1+)  
- Visual Studio 2022 nebo jakýkoli editor, který máte rádi (VS Code funguje dobře)  
- The **Aspose.OCR** NuGet package (`Install-Package Aspose.OCR`)  
- Ukázkový PNG obsahující ruské znaky (nazveme jej `sample_russian.png`)

To je vše—žádné extra nativní DLL, žádné externí služby a žádné šílené konfigurační soubory. Připravení? Ponořme se do toho.

---

## Krok 1 – Inicializace OCR enginu (jak použít OCR)

První věc, kterou musíte udělat, když chcete **použít OCR**, je vytvořit instanci enginu. Aspose za vás udělá těžkou práci, včetně stažení cyrilického jazykového balíčku při prvním požadavku.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Drawing;

// Create the OCR engine – this also triggers a one‑time download of language data
OcrEngine ocrEngine = new OcrEngine();
```

> **Proč je to důležité:** Engine uchovává veškerý vnitřní stav (např. jazykové modely) a poskytuje metodu `Recognize`, kterou později zavoláte. Vytvoření jedné instance a její opětovné použití napříč více obrázky je efektivnější než vytváření nového objektu pro každý soubor.

---

## Krok 2 – Načtení PNG obrázku (číst text z PNG)

Jakmile je engine připraven, potřebujete obrázek, který mu předáte. Krok **číst text z PNG** je jednoduchý, ale existuje několik úskalí:

1. **Cesta k souboru** – ujistěte se, že cesta je absolutní nebo relativní k pracovnímu adresáři spustitelného souboru.  
2. **Uvolnění** – `Image` implementuje `IDisposable`; zabalte ji do `using` bloku, aby nedocházelo k únikům paměti.

```csharp
string imagePath = @"YOUR_DIRECTORY\sample_russian.png";

using (Image russianImage = Image.FromFile(imagePath))
{
    // The image is now loaded and will be disposed automatically
}
```

> **Tip:** Pokud pracujete se streamy (např. nahranými soubory), použijte `Image.FromStream(stream)` místo `FromFile`.

---

## Krok 3 – Výběr cyrilického jazykového balíčku (extrahovat ruský text)

Aspose dodává mnoho jazykových balíčků, ale výchozí je angličtina. Protože naším cílem je **extrahovat ruský text**, musíme explicitně říct engine, aby použil cyrilický model.

```csharp
ocrEngine.Language = Language.Cyrillic;   // Switches the OCR engine to Cyrillic
```

> **Proč je to nezbytné:** Bez nastavení `Language.Cyrillic` se engine pokusí interpretovat glyfy jako latinské znaky, což vede k nečitelné výstupu. První volání může trvat několik sekund, než se stáhnou jazyková data—poté jsou uložena v místní cache.

---

## Krok 4 – Rozpoznání a převod obrázku na text (převést obrázek na text)

Zde je jádro tutoriálu: převod obrázku na prostý textový řetězec. Metoda `Recognize` dělá právě to.

```csharp
using (Image russianImage = Image.FromFile(imagePath))
{
    // Perform OCR – this returns the detected text as a string
    string recognizedText = ocrEngine.Recognize(russianImage);

    // Show the result in the console
    Console.WriteLine("=== Recognized Russian Text ===");
    Console.WriteLine(recognizedText);
}
```

**Očekávaný výstup v konzoli** (váš skutečný text se bude lišit podle obsahu PNG):

```
=== Recognized Russian Text ===
Привет, мир! Это пример текста на русском языке.
```

Pokud vidíte otazníky nebo náhodné symboly, zkontrolujte, že obrázek má vysoké rozlišení a že jste správně nastavili `Language.Cyrillic`.

---

## Krok 5 – Zobrazení a ověření rozpoznaného textu (rozpoznat text na obrázku)

V reálné aplikaci byste pravděpodobně výsledek uložili do databáze, vložili ho do vyhledávacího indexu nebo předali překladatelskému API. Pro tento tutoriál stačí jednoduchý `Console.WriteLine`, který dokáže, že můžeme **spolehlivě rozpoznat text na obrázku**.

```csharp
Console.WriteLine("\nDone! The OCR engine has extracted the Russian text.");
```

> **Okrajový případ:** Pokud PNG neobsahuje žádný text (nebo je text příliš rozmazaný), `Recognize` vrátí prázdný řetězec. Vždy to ošetřete:

```csharp
if (string.IsNullOrWhiteSpace(recognizedText))
{
    Console.WriteLine("No readable text found – try a clearer image or adjust DPI.");
}
```

---

## Kompletní funkční příklad

Níže je kompletní program, který můžete zkopírovat a vložit do nového konzolového projektu (`dotnet new console`). Obsahuje všechny using direktivy, správné uvolnění a malou část ošetření chyb.

```csharp
// ------------------------------------------------------------
// Full OCR example – extract Russian text from a PNG file
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine (downloads Cyrillic pack on first run)
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Path to the PNG that contains Russian text
        string imagePath = @"YOUR_DIRECTORY\sample_russian.png";

        // 3️⃣ Tell the engine to use Cyrillic (necessary for Russian)
        ocrEngine.Language = Language.Cyrillic;

        // 4️⃣ Load the image and run OCR
        using (Image russianImage = Image.FromFile(imagePath))
        {
            string recognizedText = ocrEngine.Recognize(russianImage);

            // 5️⃣ Output the result
            Console.WriteLine("=== Recognized Russian Text ===");
            Console.WriteLine(recognizedText);

            // Simple validation
            if (string.IsNullOrWhiteSpace(recognizedText))
            {
                Console.WriteLine("\n⚠️ No text detected – check image quality or language settings.");
            }
            else
            {
                Console.WriteLine("\n✅ OCR succeeded!");
            }
        }
    }
}
```

Uložte soubor, spusťte `dotnet run` a sledujte, jak konzole vypíše ruskou větu vloženou ve vašem PNG. 🎉

---

## Praktické tipy a běžné úskalí

| Situace | Co dělat |
|-----------|------------|
| **Obrázek má nízké rozlišení** | Zvyšte DPI před OCR (`new Bitmap(image, new Size(width*2, height*2))`). |
| **Text je otočen** | Použijte `ocrEngine.RotateImage` nebo předzpracujte pomocí `System.Drawing` k vyrovnání. |
| **Více jazyků na jednom obrázku** | Nastavte `ocrEngine.Language = Language.Cyrillic | Language.English;` pro povolení hybridního rozpoznání. |
| **Velká dávka souborů** | Znovu použijte jedinou instanci `OcrEngine`; pouze objekty `Image` je třeba uvolnit v každé iteraci. |
| **Běh na Linuxu** | Ujistěte se, že je nainstalován `libgdiplus` (`apt-get install -y libgdiplus`), protože `System.Drawing.Common` na něm závisí. |

---

## Vizualizace

![jak použít OCR v C# výstup konzole ukazující extrahovaný ruský text](ocr_console_output.png "jak použít OCR v C# – ukázkový výstup")

*Obrázek výše ilustruje okno konzole po dokončení programu, potvrzující, že jsme úspěšně **přečetli text z PNG** a **převáděli obrázek na text**.*

---

## Závěr

Probrali jsme **jak použít OCR** v C# od začátku do konce: inicializaci enginu, načtení PNG, přepnutí na cyrilický jazykový balíček, provedení rozpoznání a nakonec zobrazení extrahované ruské věty. Krátký program demonstruje celý workflow **převést obrázek na text** a ukazuje, jak **spolehlivě rozpoznat text na obrázku**.

Další kroky?  
- Zkuste extrahovat text z vícestránkových PDF (Aspose.OCR to také podporuje).  
- Experimentujte s dalšími jazykovými balíčky (`Language.Arabic`, `Language.ChineseSimplified`, atd.).  
- Připojte výstup k překladatelské službě nebo vyhledávacímu indexu, aby byla vaše aplikace skutečně vícejazyčná.

Máte otázky ohledně zpracování špatných skenů nebo integrace OCR do webového API? Zanechte komentář a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}