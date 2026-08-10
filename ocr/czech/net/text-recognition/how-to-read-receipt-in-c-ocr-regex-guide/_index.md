---
category: general
date: 2026-02-13
description: Jak rychle načíst účtenku pomocí Aspose OCR a extrahovat částku pomocí
  regexu. Naučte se krok za krokem zpracování účtenky pomocí OCR.
draft: false
keywords:
- how to read receipt
- extract amount using regex
- regex find total
- process receipt with ocr
language: cs
og_description: Jak číst účtenku v C# pomocí Aspose OCR a regexu. Tento průvodce vám
  ukáže, jak zpracovat účtenku pomocí OCR a extrahovat celkovou částku.
og_title: Jak číst potvrzení v C# – Kompletní OCR a Regex tutoriál
tags:
- OCR
- C#
- Regex
- Aspose
title: Jak číst účtenku v C# – Průvodce OCR + Regex
url: /cs/net/text-recognition/how-to-read-receipt-in-c-ocr-regex-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak číst účtenku v C# – OCR + Regex průvodce

Už jste se někdy zamysleli nad tím, **jak číst receipt** na obrázcích, aniž byste ručně přepisovali každý řádek? V mnoha aplikacích pro malé podniky potřebujete získat celkovou částku z fotografie účtenky a ruční zadávání ruší smysl automatizace. Dobrá zpráva? S Aspose OCR můžete nechat motor udělat těžkou práci a jednoduchý regulární výraz najde celkovou částku. V tomto tutoriálu projdeme **process receipt with OCR**, extrahovat částku pomocí regexu a získáme připravenou hodnotu celku.

Uvidíte kompletní, spustitelný příklad, zjistíte, proč je model jazyka účtenky důležitý, a získáte tipy, jak zacházet s okrajovými případy, jako jsou různé měnové symboly nebo chybějící štítky „Total“. Žádná externí dokumentace není potřeba—vše, co potřebujete, je zde.

## Co se naučíte

- Jak nastavit Aspose OCR pro rozpoznávání specifické pro účtenky (model jazyka `Receipt` automaticky vyrovnává a odstraňuje šum z obrázku).  
- Jak použít regulární výraz, který **extract amount using regex** vzory fungující pro většinu US‑style receipts.  
- Jak zacházet s běžnými variantami, jako jsou „TOTAL“, „Total:“ nebo „Grand Total – $12.34“.  
- Jak bezpečně vypsat výsledek a co dělat, když není vzor nalezen.  

**Požadavky**: .NET 6+ (nebo .NET Framework 4.7+), platná licence Aspose OCR nebo zkušební verze a lokálně uložený obrázek účtenky. To je vše—žádné další NuGet balíčky kromě Aspose.OCR.

---

## Krok 1 – Instalace Aspose OCR a příprava projektu

### Proč je to důležité

Aspose OCR poskytuje speciálně vytvořený model **process receipt with OCR**, který umí narovnat zmačkaný papír a ignorovat šum na pozadí. Použití obecného textového modelu by vedlo k více chybám, zejména u nízkokvalitních skenů.

### Code

```csharp
// Install the package via NuGet first:
//   dotnet add package Aspose.OCR
using Aspose.OCR;
using Aspose.OCR.Enums;
using System.Text.RegularExpressions;

// If you have a license file, load it now (optional but removes trial watermark)
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

> **Tip:** Uchovávejte licenční soubor mimo složku se zdrojovým kódem, aby nedošlo k neúmyslnému commitu.

---

## Krok 2 – Konfigurace OCR enginu pro rozpoznávání účtenek

### Proč je to důležité

Model jazyka `Receipt` obsahuje vestavěné vyrovnání a odstranění šumu, což dramaticky zvyšuje přesnost u reálných účtenek, které jsou často složené nebo zmačkané.

### Code

```csharp
// Step 2: Create and configure the OCR engine for receipt processing
var ocrEngine = new OcrEngine
{
    // Receipt model is optimized for invoices, grocery receipts, etc.
    Language = OcrLanguage.Receipt
};
```

---

## Krok 3 – Rozpoznání textu z obrázku účtenky

### Proč je to důležité

Nejprve potřebujete surový text, než můžete použít jakýkoli regex. Metoda `RecognizeImage` vrací `OcrResult`, který obsahuje celý řetězec, skóre důvěry a další údaje, pokud je budete později potřebovat.

### Code

```csharp
// Step 3: Recognize text from the receipt image
// Replace the path with the actual location of your receipt file.
string receiptPath = @"C:\Receipts\sample-receipt.jpg";

OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

// Quick sanity check – print the whole OCR output (helps debugging)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(receiptResult.Text);
Console.WriteLine("===================\n");
```

**Očekávaný výstup OCR (příklad)**  
```
Walmart Supercenter
123 Main St.
Anytown, USA
Date: 02/12/2026
Item A   $3.45
Item B   $7.89
Subtotal $11.34
Tax      $0.91
Total:   $12.25
Thank you!
```

---

## Krok 4 – Vytvoření regexu pro **Extract Amount Using Regex**

### Proč je to důležité

Účtenky mají mnoho formátů, ale slovo „Total“ (nebo jeho blízká varianta) následované částkou v dolarech je spolehlivým ukotvením. Níže uvedený vzor toleruje volitelné mezery, dvojtečky, pomlčky a volitelný znak `$`.

### Code

```csharp
// Step 4: Use a regular expression to locate the total amount in the recognized text
string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
RegexOptions options = RegexOptions.IgnoreCase;

Match totalMatch = Regex.Match(receiptResult.Text, pattern, options);
```

**Vysvětlení vzoru**

| Část | Význam |
|------|---------|
| `Total` | Hledá slovo „Total“ (nerozlišuje velikost písmen). |
| `\s*[:\-]?` | Povolí libovolné bílé znaky, poté volitelnou dvojtečku nebo pomlčku. |
| `\s*\$?` | Volitelný bílý znak a volitelný dolarový znak. |
| `(\d+(\.\d{2})?)` | Zachytí jednu nebo více číslic, volitelně následované desetinnou tečkou a dvěma centy. |

---

## Krok 5 – Výstup extrahovaného celku nebo ošetření chybějících dat

### Proč je to důležité

I nejlepší OCR může některé slovo vynechat, zejména u rozmazaných účtenek. Poskytnutí elegantního náhradního řešení zabraňuje pádům a poskytuje vám možnost pro vlastní logiku (např. požádat uživatele o potvrzení).

### Code

```csharp
// Step 5: Output the extracted total, or indicate it wasn't found
if (totalMatch.Success)
{
    string amount = totalMatch.Groups[1].Value;
    Console.WriteLine($"Total: ${amount}");
}
else
{
    Console.WriteLine("Total amount not found. Consider reviewing the OCR output manually.");
}
```

**Ukázkový výstup v konzoli**

```
Total: $12.25
```

---

## Kompletní funkční příklad – Všechny kroky v jednom souboru

Níže je jeden samostatný program, který můžete zkopírovat a vložit do konzolového projektu. Obsahuje komentáře, ošetření chyb a volitelné načtení licence.

```csharp
// ---------------------------------------------------------------
// How to Read Receipt in C# – OCR + Regex (Complete Example)
// ---------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Enums;
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 0️⃣ Optional: Load your Aspose OCR license (remove trial watermark)
        try
        {
            var license = new Aspose.OCR.License();
            license.SetLicense("Aspose.OCR.lic"); // path to .lic file
        }
        catch (Exception ex)
        {
            Console.WriteLine("License not found – running in trial mode.");
        }

        // 1️⃣ Configure the OCR engine for receipt processing
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Receipt // receipt model = de‑skew + de‑noise
        };

        // 2️⃣ Path to the receipt image (change to your file)
        string receiptPath = @"YOUR_DIRECTORY/receipt.jpg";

        // 3️⃣ Perform OCR
        OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

        // 4️⃣ Debug: show full OCR text (helps when regex fails)
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(receiptResult.Text);
        Console.WriteLine("===================\n");

        // 5️⃣ Regex to **extract amount using regex** (find the total)
        string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
        Match totalMatch = Regex.Match(receiptResult.Text, pattern,
                                        RegexOptions.IgnoreCase);

        // 6️⃣ Output
        if (totalMatch.Success)
        {
            string amount = totalMatch.Groups[1].Value;
            Console.WriteLine($"Total: ${amount}");
        }
        else
        {
            Console.WriteLine("Total amount not found. You might need to adjust the regex or improve image quality.");
        }
    }
}
```

**Spuštění programu**

1. Vytvořte nový konzolový projekt (`dotnet new console -n ReceiptReader`).  
2. Přidejte NuGet balíček Aspose.OCR (`dotnet add package Aspose.OCR`).  
3. Nahraďte `YOUR_DIRECTORY/receipt.jpg` skutečnou cestou k obrázku účtenky.  
4. Sestavte a spusťte (`dotnet run`).  

Měli byste vidět výpis OCR následovaný `Total: $xx.xx`, pokud vše funguje.

---

## Řešení okrajových případů a běžných variant

### 1. Různé měnové symboly

If you deal with euros (€) or pounds (£), extend the pattern:

```csharp
string pattern = @"Total\s*[:\-]?\s*[$€£]?\s*(\d+(\.\d{2})?)";
```

### 2. Chybějící štítek „Total“

Some receipts only show “Grand Total”. Add an alternation:

```csharp
string pattern = @"(?:Total|Grand\s*Total)\s*[:\-]?\s*[$]?\s*(\d+(\.\d{2})?)";
```

### 3. Více celkových částek (např. „Subtotal“ a „Total“)

If the regex matches the first occurrence, you may want the **last** match:

```csharp
MatchCollection matches = Regex.Matches(receiptResult.Text, pattern,
                                         RegexOptions.IgnoreCase);
Match last = matches.Count > 0 ? matches[matches.Count - 1] : null;
```

### 4. Nízké rozlišení obrázků

- Zvyšte DPI při skenování (`300 DPI` je optimální).  
- Předzpracujte obrázek jednoduchým filtrem na snížení rozmazání před předáním Aspose (mimo rozsah tohoto průvodce, ale stojí za vyzkoušení).

---

## Pro tipy pro reálné projekty

- **Cache the OCR result** pokud potřebujete extrahovat několik polí (daň, položky atd.) – zaplatíte náklad na OCR jen jednou.  
- **Log the raw OCR text** do databáze; stane se cenným auditním záznamem pro sporné výdaje.  
- Při tvorbě webového API **run OCR in a background worker**; může to trvat několik stovek milisekund, což je v asynchronním režimu v pořádku, ale ne ideální pro synchronní požadavek.  
- **Validate the extracted amount** podle obchodních pravidel (např. částka musí být > 0) před uložením.  

---

## Závěr

Probrali jsme **how to read receipt** obrázky v C# pomocí Aspose OCR a poté **extract amount using regex**, abychom spolehlivě našli řádek s celkem. Využitím modelu jazyka `Receipt` získáte vyrovnaný a odšuměný text a stručný regulární výraz řeší většinu formátovacích zvláštností. Kompletní ukázkový kód výše lze vložit do jakéhokoli .NET konzolového nebo servisního projektu a další tipy pro okrajové případy vám poskytují pevný základ pro produkční nasazení.

Jste připraveni na další krok? Zkuste rozšířit řešení tak, aby získávalo jednotlivé položky, automaticky počítalo daň nebo se integrovalo s API pro sledování výdajů. A pokud narazíte na účtenku, která vzor rozbije, pamatujte, že přístup **regex find total** je jen výchozí – můžete vzor vždy upravit tak, aby odpovídal vašemu konkrétnímu prostředí.

Šťastné programování a ať je vaše zpracování účtenek rychlé, přesné a zcela automatizované!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}