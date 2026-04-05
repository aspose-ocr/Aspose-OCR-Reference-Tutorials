---
category: general
date: 2026-04-04
description: Jak rychle a bezpečně používat OCR. Naučte se extrahovat text z obrázku,
  převádět DJVU na text a načíst obrázek pro OCR pomocí Aspose.OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert djvu to text
- load image for OCR
- extract text from djvu
language: cs
og_description: Jak použít OCR v C# k extrakci textu z obrazových souborů a dokumentů
  DJVU. Krok za krokem tutoriál s kompletním kódem.
og_title: Jak používat OCR v C# – Kompletní průvodce
tags:
- OCR
- C#
- Aspose
title: Jak použít OCR v C# – Extrahovat text z obrázků a souborů DJVU
url: /cs/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-and-djvu-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat OCR v C# – Extrahování textu z obrázků a DJVU souborů

Už jste se někdy zamýšleli **jak používat OCR** k získání slov ze skenované stránky bez ručního psaní? Nejste jediní. V mnoha projektech – ať už digitalizujete staré knihy nebo získáváte data z účtenek – je získání textu z obrázku každodenní problém. Dobrá zpráva? S Aspose.OCR to můžete udělat během několika řádků kódu, i když je zdroj DJVU soubor.

V tomto průvodci projdeme vše, co potřebujete k **extrahování textu z obrázku**, **načtení obrázku pro OCR** a dokonce **převodu DJVU na text** pomocí C#. Na konci budete mít připravenou konzolovou aplikaci, která vypíše rozpoznaný text přímo do konzole. Žádná tajemství, žádné další závislosti, jen čistý C# a Aspose.

## Co se naučíte

- Jak nainstalovat a odkazovat na knihovnu Aspose.OCR.
- Přesný kód potřebný k **načtení obrázku pro OCR**, ať už jde o PNG, JPEG nebo DJVU stránku.
- Jak zavolat engine a získat výsledek.
- Tipy pro práci s velkými dokumenty a běžné úskalí.
- Kompletní, spustitelný příklad, který můžete zkopírovat a vložit do Visual Studia.

> **Předpoklad:** .NET 6.0 nebo novější a platná licence Aspose.OCR (nebo bezplatná zkušební verze). Pokud knihovnu ještě nemáte, stáhněte ji z NuGet pomocí `dotnet add package Aspose.OCR`.

---

## Jak používat OCR s Aspose v C#

Toto je jádro, kde skutečně odpovídáme na otázku **jak používat OCR** v C# projektu. Níže uvedený kód je kompletní program; můžete jej vložit do nové konzolové aplikace a stisknout F5.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create the OCR engine instance.
            var ocrEngine = new OcrEngine();

            // Step 2: Load the image (or DJVU page) you want to analyze.
            // Replace the path with your own file location.
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book-page.djvu");

            // Step 3: Run the recognition process.
            OcrResult ocrResult = ocrEngine.Recognize();

            // Step 4: Output the extracted text.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Proč to funguje:**  
- `OcrEngine` je vstupní bod; abstrahuje těžkou práci předzpracování obrázku, detekce jazyka a klasifikace znaků.  
- `ImageStream.FromFile` dokáže zpracovat mnoho formátů, včetně DJVU, což znamená, že můžete **převést DJVU na text** bez dalšího konverzního kroku.  
- `Recognize()` vrací objekt `OcrResult`, který obsahuje čistý text, skóre důvěry a dokonce i ohraničující rámečky, pokud je budete potřebovat později.

Spuštění programu vypíše něco jako:

```
=== OCR Result ===
In the beginning God created the heavens and the earth.
```

A to je vše – vaše první úspěšná operace **extrahování textu z DJVU**.

![how to use OCR example](/images/ocr-demo.png "Screenshot showing how to use OCR in a C# console app")

*Alt text: “how to use OCR” screenshot of console output.*

---

## Načtení obrázku pro OCR

Než engine dokáže něco přečíst, musíte **načíst obrázek pro OCR** správně. Aspose podporuje většinu rastrových formátů „out‑of‑the‑box“, ale několik tipů může rozpoznávání zjednodušit:

- **Změňte velikost velkých obrázků** na maximálně 2000 px na delší straně. Příliš velké soubory zvyšují využití paměti a mohou engine zpomalit.  
- **Převádějte barevné obrázky na odstíny šedi**, pokud zaznamenáte šumivé pozadí. Použijte `ocrEngine.Image = ImageStream.FromFile(path).ConvertToGrayscale();`.  
- **Nastavte DPI ručně** pro nízké rozlišení skenů (`ocrEngine.Image.DpiX = 300; ocrEngine.Image.DpiY = 300;`).

Tyto úpravy jsou volitelné, ale často zvyšují přesnost při **extrahování textu z obrázku** ze skenovaných účtenek.

---

## Extrahování textu z obrázku – osvědčené postupy

Když pracujete s typickými formáty obrázků (PNG, JPEG, BMP), kroky zůstávají stejné, ale můžete engine doladit:

```csharp
ocrEngine.Image = ImageStream.FromFile("sample.png");

// Optional: enable language packs for better accuracy.
ocrEngine.Language = Language.English;

// Optional: set recognition mode to auto.
ocrEngine.RecognitionMode = RecognitionMode.Auto;
```

- **Výběr jazyka** má význam. Pokud zpracováváte vícejazyčné dokumenty, nastavte `ocrEngine.Language = Language.Multilingual;`.  
- **RecognitionMode** může být `Auto`, `Fast` nebo `Accurate`. `Accurate` poskytuje vyšší kvalitu za cenu rychlosti – použijte jej pro archivní úlohy.

---

## Převod DJVU na text – práce s více stránkami

DJVU soubory často obsahují několik stránek. Aspose zachází s každou stránkou jako s odděleným image streamem, takže je můžete procházet v cyklu:

```csharp
using Aspose.OCR;
using System.Collections.Generic;

var ocrEngine = new OcrEngine();
List<string> allPagesText = new List<string>();

int pageCount = ImageStream.GetPageCount("book.djvu");
for (int i = 1; i <= pageCount; i++)
{
    ocrEngine.Image = ImageStream.FromFile("book.djvu", i); // Load page i
    OcrResult result = ocrEngine.Recognize();
    allPagesText.Add(result.Text);
}

// Combine all pages into a single string.
string fullText = string.Join("\n--- Page Break ---\n", allPagesText);
Console.WriteLine(fullText);
```

**Proč cyklus?**  
DJVU soubory jsou v podstatě zásobník obrázků. Iterací přes každou stránku **extrahujete text z DJVU** v pořadí, čímž zachováte původní tok dokumentu.

---

## Běžné úskalí a profesionální tipy

| Problém | Proč se to děje | Řešení |
|------|----------------|-----|
| **Špatné znaky** | Nízké DPI nebo silná komprese | Zvětšit obrázek, nastavit `ocrEngine.Image.DpiX/Y = 300` |
| **Pomalé zpracování** | Použití režimu `Accurate` u velkých souborů | Přepnout na režim `Fast` pro hromadné úlohy |
| **Chybějící podpora jazyka** | Výchozí jazyk je pouze angličtina | Načíst další jazykové balíčky (`ocrEngine.Language = Language.Spanish;`) |
| **Chyby nedostatku paměti** | Načítání mnoha vysokorozlišovacích stránek najednou | Zpracovávat stránky po jedné a uvolňovat zdroje (`ocrEngine.Dispose();`) |

Rychlý **tip**: vždy po dokončení práce se stránkou zavolejte `ocrEngine.Dispose()`. Uvolní nativní zdroje a zabrání jemným únikům paměti, které mohou zhavarovat dlouho běžící služby.

---

## Testování vašeho OCR pipeline

Abyste ověřili, že vše funguje, vyzkoušejte následující jednoduché kontroly:

1. **Vytiskněte délku** rozpoznaného řetězce: `Console.WriteLine($"Characters recognized: {ocrResult.Text.Length}");`  
2. **Porovnejte s očekávaným textem** pomocí jednoduché diff knihovny, pokud máte referenční data.  
3. **Zaznamenejte skóre důvěry** (`ocrResult.Confidence`) pro automatické odhalování stránek s nízkou kvalitou.

Pokud je skóre důvěry konzistentně pod 0,7, vraťte se k předzpracování obrázku zmíněnému výše.

---

## Další kroky

Nyní, když už víte **jak používat OCR**, můžete rozšířit svůj workflow:

- **Dávkové zpracování**: Zabalte cyklus do `Parallel.ForEach` pro zrychlení velkých kolekcí.  
- **Export do PDF**: Použijte Aspose.PDF k vložení rozpoznaného textu jako skryté vrstvy pro prohledávatelné PDF.  
- **Integrace s AI**: Předejte extrahované řetězce jazykovému modelu pro shrnutí nebo extrakci entit.

Všechny tyto kroky staví na stejné základně, kterou jste právě vytvořili, a každý z nich těží ze stejných principů **extrahování textu z obrázku**, které jsme probírali.

---

## Závěr

Prozkoumali jsme podrobně **jak používat OCR** v C# s Aspose, od načtení obrázku, **extrahování textu z obrázku**, přes práci s **DJVU** soubory až po řešení běžných problémů. Kompletní, spustitelný příklad výše vám poskytuje pevný výchozí bod a tipy rozeseté po celém textu vám pomohou přizpůsobit řešení reálným projektům.  

Vyzkoušejte to, dolaďte nastavení pro své konkrétní dokumenty a během chvilky budete měnit skenované stránky na prohledávatelný text. Máte otázky nebo obtížný soubor, který odmítá spolupracovat? Zanechte komentář – hodně štěstí při programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}