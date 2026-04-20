---
category: general
date: 2026-02-11
description: Extrahujte text z obrázku v C# pomocí Aspose OCR. Naučte se, jak načíst
  obrázek pro OCR, zlepšit přesnost OCR a opravit chyby OCR pomocí pravopisné kontroly.
draft: false
keywords:
- extract text from image
- image to text c#
- improve ocr accuracy
- load image for ocr
- fix ocr errors
language: cs
og_description: Extrahujte text z obrázku v C# pomocí Aspose OCR. Tento průvodce ukazuje,
  jak načíst obrázek pro OCR, zlepšit přesnost OCR a opravit chyby OCR.
og_title: Extrahovat text z obrázku v C# – Kompletní průvodce OCR
tags:
- C#
- OCR
- Aspose
- Text Extraction
title: Extrahovat text z obrázku v C# – Kompletní průvodce OCR
url: /cs/net/ocr-optimization/extract-text-from-image-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z obrázku v C# – Kompletní průvodce OCR

Už jste někdy potřebovali **extrahovat text z obrázku**, ale výsledek vypadal jako nesmysl? Nejste v tom sami. V mnoha reálných aplikacích – například skenování účtenek, digitalizace poznámek nebo migrace starých dokumentů – získání čistého textu z obrázku je první a často nejnáročnější překážka.

Naštěstí s Aspose OCR můžete **načíst obrázek pro OCR**, spustit kontrolu pravopisu a získat úhledný, prohledávatelný text. V tomto tutoriálu projdeme celým procesem, od načtení JPEG až po vylepšení výstupu, a ukážeme vám přesně, jak **zlepšit přesnost OCR**.

> **Co získáte:** připravený C# konzolový program, který extrahuje text z obrázku, opravuje běžné chyby OCR a vypisuje jak surový, tak vyčištěný výsledek.

---

## Co budete potřebovat

- .NET 6 nebo novější (kód funguje také na .NET Framework 4.7+)
- Visual Studio 2022 (nebo jakékoli IDE dle vašeho výběru)
- Bezplatný zkušební klíč Aspose OCR nebo licencovaná verze
- Soubor obrázku obsahující psaný nebo tištěný text (např. `typed_note.jpg`)

Žádné další knihovny třetích stran nejsou potřeba – Aspose automaticky zajišťuje jazykové modely a kontrolu pravopisu.

## Krok 1 – Instalace NuGet balíčku Aspose OCR

Než budeme moci **extrahovat text z obrázku**, musí být OCR engine k dispozici na počítači.

```powershell
# From the Package Manager Console
Install-Package Aspose.OCR
```

Nebo, pokud dáváte přednost CLI:

```bash
dotnet add package Aspose.OCR
```

Balíček obsahuje jazyková data, ale nastavení `AutomaticResourceDownload = true` (jak uděláme později) zaručuje, že chybějící slovníky budou staženy za běhu.

## Krok 2 – Načtení obrázku pro OCR

Prvním, co engine potřebuje, je bitmapa. Můžete mu předat libovolný formát podporovaný `System.Drawing.Image`, například PNG, JPEG, BMP nebo TIFF.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Path to your source picture – change this to your own folder
string imagePath = @"C:\MyImages\typed_note.jpg";

// Load the image inside a using block so the file handle is released promptly
using (Image image = Image.FromFile(imagePath))
{
    // The rest of the OCR pipeline lives inside this block
}
```

> **Proč blok `using`?** Automaticky uvolní objekt `Image`, čímž zabrání problémům se zamčením souboru, které často potkají vývojáře zapomínající uvolnit prostředky.

## Krok 3 – Provedení OCR – „Obrázek na text C#“ v akci

Nyní skutečně **extrahujeme text z obrázku**. Třída `OcrEngine` provádí těžkou práci.

```csharp
// Step 3: Initialise the OCR engine
var ocrEngine = new OcrEngine
{
    AutomaticResourceDownload = true, // pulls language packs if missing
    Language = OcrLanguage.English    // set to your document's language
};

// Inside the using block from Step 2
var ocrResult = ocrEngine.Recognize(image);
string rawText = ocrResult.Text;
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

V tomto okamžiku máte řetězec, který odráží to, co engine vidí na obrázku. Ve skutečnosti může výstup obsahovat cizí znaky, špatně rozpoznaná slova nebo podivnosti v zalomení řádků – proto následuje další krok.

## Krok 4 – Zlepšení přesnosti OCR pomocí kontroly pravopisu

Aspose poskytuje dedikovaný `SpellChecker`, který zná jazyk, který zpracováváte. Provedení kontroly nad surovým řetězcem často opraví nejzjevnější chyby.

```csharp
// Step 4: Initialise spell‑check (resources are auto‑downloaded)
var spellChecker = new SpellChecker(OcrLanguage.English);

// Correct the OCR output
string correctedText = spellChecker.Correct(rawText);
Console.WriteLine("\nCorrected OCR output:");
Console.WriteLine(correctedText);
```

> **Tip:** Pokud pracujete s doménově specifickým slovníkem (např. lékařské termíny), můžete `SpellChecker` poskytnout vlastní slovník pomocí jeho přetížených metod.

## Krok 5 – Ruční oprava chyb OCR (volitelné)

I ten nejlepší kontrolor pravopisu může přehlédnout chyby závislé na kontextu. Rychlý post‑processing může zachytit například „l“ vs „1“ nebo „O“ vs „0“.

```csharp
// Simple regex to replace common OCR confusions
string finalText = System.Text.RegularExpressions.Regex.Replace(
    correctedText,
    @"\b([lI])\b", // isolated l or I
    "1");

// Additional custom rules can be added here
Console.WriteLine("\nFinal cleaned text:");
Console.WriteLine(finalText);
```

Neváhejte tuto část rozšířit o vlastní heuristiky – například vyhledávací tabulku pro kódy produktů nebo seznam známých zkratek.

## Kompletní funkční příklad

Níže je celý program, který můžete zkopírovat a vložit do nového projektu Console App. Obsahuje všechny diskutované kroky a užitečné komentáře.

```csharp
// ------------------------------------------------------------
// Extract Text from Image in C# – Full Example
// ------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure OCR engine – automatic download ensures language data is present
        var ocrEngine = new OcrEngine
        {
            AutomaticResourceDownload = true,
            Language = OcrLanguage.English
        };

        // 2️⃣ Load the image you want to analyse
        string imagePath = @"C:\MyImages\typed_note.jpg";
        using (Image image = Image.FromFile(imagePath))
        {
            // 3️⃣ Run OCR – this is where we *extract text from image*
            var ocrResult = ocrEngine.Recognize(image);
            string rawText = ocrResult.Text;
            Console.WriteLine("Before (raw OCR):");
            Console.WriteLine(rawText);
            Console.WriteLine(new string('-', 40));

            // 4️⃣ Spell‑check to *improve OCR accuracy*
            var spellChecker = new SpellChecker(OcrLanguage.English);
            string correctedText = spellChecker.Correct(rawText);
            Console.WriteLine("After (spell‑checked):");
            Console.WriteLine(correctedText);
            Console.WriteLine(new string('-', 40));

            // 5️⃣ Optional custom clean‑up – *fix OCR errors* that the spell‑checker missed
            string finalText = Regex.Replace(correctedText,
                @"\b([lI])\b", // replace isolated 'l' or 'I' with '1'
                "1");

            Console.WriteLine("Final (post‑processed):");
            Console.WriteLine(finalText);
        }
    }
}
```

### Očekávaný výstup

Předpokládejme, že `typed_note.jpg` obsahuje větu „Hello world, this is a test 123“, konzole zobrazí něco jako:

```
Before (raw OCR):
H3llo w0rld, th1s is a test 123

After (spell‑checked):
Hello world, this is a test 123

Final (post‑processed):
Hello world, this is a test 123
```

Všimněte si, že kontrola pravopisu změnila „H3llo“ na „Hello“ a regulární výraz odstranil cizí „1“, která se objevila ve slově „th1s“.

## Časté otázky a okrajové případy

| Question | Answer |
|----------|--------|
| **Mohu použít jiný jazyk?** | Ano. Nastavte `ocrEngine.Language = OcrLanguage.Spanish` (nebo jakýkoli podporovaný enum) a předávejte stejný jazyk do `SpellChecker`. |
| **Co když je můj obrázek velmi velký?** | Zmenšete jej před předáním OCR; `Image` má metodu `GetThumbnailImage` pro rychlé změny velikosti. |
| **Potřebuji internetové připojení?** | Pouze při první chybějící jazykové sadě; poté jsou zdroje uloženy lokálně. |
| **Jak zacházet s více‑stránkovými PDF?** | Převést každou stránku na obrázek (např. pomocí `PdfRenderer`) a spustit stejný proces pro každou stránku. |
| **Je kontrola pravopisu jazykově uvědomělá?** | Ano. Používá stejný jazykový model, který jste poskytli OCR engine, což zajišťuje konzistenci. |

## Další kroky a související témata

- **Dávkové zpracování:** Zabalte kód do smyčky `foreach` pro zpracování složky s obrázky.
- **Ručně psaný text:** Přepněte na `OcrLanguage.EnglishHandwritten` pro lepší výsledky u kurzívních poznámek.
- **Paralelismus:** Použijte `Parallel.ForEach` pro zrychlení velkých úloh na vícejádrových strojích.
- **Export do JSON/CSV:** Serializujte `finalText` spolu s metadaty (název souboru, skóre důvěry) pro následnou analytiku.

Pokud vás zajímá, jak převést extrahované řetězce na prohledávatné PDF, podívejte se na náš návod **„Vytvoření prohledávatelného PDF z obrázku v C#“**. Staví přímo na stejném OCR pipeline, který jsme právě probírali.

## Závěr

Právě jsme ukázali pragmatický způsob, jak **extrahovat text z obrázku** v C# pomocí Aspose OCR, a zároveň jsme ukázali, jak **načíst obrázek pro OCR**, **zlepšit přesnost OCR** a **opravit chyby OCR** pomocí vestavěného kontroloru pravopisu a malého regexu pro čištění. Kompletní příklad funguje hned po instalaci, vyžaduje pouze jeden NuGet balíček a lze jej rozšířit tak, aby vyhovoval prakticky jakémukoli scénáři digitalizace dokumentů.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}