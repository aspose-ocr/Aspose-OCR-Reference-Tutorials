---
category: general
date: 2026-03-05
description: Jak používat OCR v C# k extrakci textu z obrázku. Naučte se převádět
  obrázek na text, číst korejské znaky a rychle načíst obrázek pro OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert image to text
- read korean characters
- load image for OCR
language: cs
og_description: Jak používat OCR v C# a okamžitě extrahovat text z obrázku. Tento
  průvodce ukazuje, jak převést obrázek na text, číst korejské znaky a načíst obrázek
  pro OCR.
og_title: Jak používat OCR v C# – Extrahovat text z obrázku
tags:
- OCR
- C#
- Aspose
title: Jak použít OCR v C# – Extrahovat text z obrázku
url: /cs/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat OCR v C# – Extrahovat text z obrázku

Už jste se někdy zamysleli **jak používat OCR**, když máte snímek obrazovky plný korejského textu a potřebujete získat prostý řetězec? Nejste jediní, kdo se nad tím trápí. V tomto tutoriálu projdeme kompletním, připraveným k spuštění příkladem, který **extrahuje text z obrázku**, **převádí obrázek na text** a dokonce vám ukáže, jak **číst korejské znaky** pomocí Aspose.OCR.

Také se podíváme na často přehlížený krok **načtení obrázku pro OCR**, abyste později nečelili překvapení „soubor nebyl nalezen“. Na konci budete mít samostatný program, který můžete vložit do libovolného .NET projektu.

## Co budete potřebovat

- .NET 6+ (nebo .NET Framework 4.7.2 a novější) – kód funguje na obou.
- Aspose.OCR pro .NET – můžete si stáhnout bezplatnou zkušební verzi z webu Aspose.
- Vzorek obrázku (`korean_doc.png`), který obsahuje korejský text.
- Vaše oblíbené IDE (Visual Studio, Rider, VS Code – cokoliv, co máte rádi).

Žádné další knihovny třetích stran nejsou vyžadovány.

## Krok 1: Nastavení projektu a přidání Aspose.OCR

First, create a new console app:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Then add the Aspose.OCR NuGet package:

```bash
dotnet add package Aspose.OCR
```

> **Tip:** Pokud máte licenční soubor, umístěte jej do kořenového adresáře projektu; jinak bude fungovat bezplatná zkušební verze, ale přidá vodoznak do výstupu.

## Krok 2: Jak používat OCR – Inicializace enginu

Nyní napíšeme C# kód. První věc, kterou je třeba udělat, když **jak používat OCR**, je vytvořit instanci `OcrEngine`. Tento objekt je srdcem knihovny; obsahuje všechna nastavení, která budete později potřebovat.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: apply your license to remove trial limitations
            // Replace the path with the actual location of your .lic file
            ocrEngine.SetLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Proč je to důležité:** Bez správné instance enginu nemůžete nastavit jazyk, načíst obrázky ani získat výsledky. Engine také spravuje interní zdroje, takže jeho jednorázové vytvoření a opakované používání je efektivnější než opakované vytváření nových objektů.

## Krok 3: Výběr jazyka – Čtení korejských znaků

Další řádek říká enginu, jaký jazyk má hledat. Protože naším cílem je **číst korejské znaky**, nastavíme `OcrLanguage.Korean`. Můžete to vyměnit za arabštinu, thajštinu, gujarati atd., v závislosti na vašem použití.

```csharp
            // Step 3: Tell the engine which language to recognize
            ocrEngine.Language = OcrLanguage.Korean; // alternatives: Arabic, Thai, Gujarati, etc.
```

**Proč je to důležité:** Výběr jazyka výrazně zvyšuje přesnost. OCR engine používá jazykově specifické slovníky a modely znaků; pokud mu poskytnete špatný jazyk, může výstup být zkreslený.

## Krok 4: Načtení obrázku pro OCR – Převod obrázku na text

Než engine může něco udělat, musíte **načíst obrázek pro OCR**. Metoda `ImageStream.FromFile` načte soubor do formátu, který engine rozumí.

```csharp
            // Step 4: Load the image that contains the text
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/korean_doc.png");
```

Pokud se obrázek nachází v jiné složce, stačí upravit cestu. Nezapomeňte nastavit *Build Action* souboru na „Copy if newer“, aby spustitelný soubor mohl najít obrázek během běhu.

> **Častý úskalí:** Zadání cesty s obrácenými lomítky (`\`) v řetězcovém literálu bez jejich úniku způsobí chybu při kompilaci. Použijte buď dvojité obrácené lomítka (`\\`) nebo doslovný řetězec (`@"C:\\path\\file.png"`).

## Krok 5: Provedení OCR – Extrahování textu z obrázku

Nyní se provádí těžká práce. Volání `Recognize()` spustí OCR algoritmus a vlastnost `Text` vám poskytne surový řetězec.

```csharp
            // Step 5: Run OCR and get the recognized text
            string recognizedText = ocrEngine.Recognize().Text;
```

V tomto okamžiku jste **extrahovali text z obrázku** a efektivně **převáděli obrázek na text**. Výsledek může obsahovat znaky nového řádku, pokud původní rozložení mělo zalomení řádků.

## Krok 6: Zobrazení výsledku – Ověření výstupu

Nakonec vytiskneme výsledek do konzole, abyste mohli ověřit, že to funguje.

```csharp
            // Step 6: Output the result to the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

Run the program:

```bash
dotnet run
```

### Očekávaný výstup

```
=== Recognized Text ===
안녕하세요. 이것은 OCR 테스트 문서입니다.
```

Pokud vidíte korejské znaky podobné těm na obrázku, gratulujeme—ovládli jste **jak používat OCR** s Aspose.OCR!

![how to use OCR example diagram](image.png)

*Image alt text: diagram příkladu jak používat OCR ukazující tok od načtení obrázku po vytištění rozpoznaného textu.*

## Okrajové případy a varianty

### 1. Zpracování více stránek

Pokud potřebujete **extrahovat text z obrázku** souborů, které obsahují několik stránek (např. více‑stránkový TIFF), projděte smyčkou každou stránku a zavolejte `Recognize()` pro každou instanci `ImageStream`.

### 2. Práce s nízkou kvalitou skenů

Obrázky s nízkým rozlišením mohou snížit přesnost. Před voláním `Recognize()` můžete obrázek vylepšit pomocí předzpracovatelských nástrojů Aspose:

```csharp
ocrEngine.Image = ImageProcessing.Preprocess(ocrEngine.Image, ImageProcessingOptions.Deskew);
```

### 3. Přepínání jazyků za běhu

Předpokládejme, že máte dokument s více jazyky. Můžete změnit `ocrEngine.Language` mezi rozpoznáními:

```csharp
ocrEngine.Language = OcrLanguage.English;
string english = ocrEngine.Recognize().Text;

ocrEngine.Language = OcrLanguage.Korean;
string korean = ocrEngine.Recognize().Text;
```

### 4. Uložení výsledku do souboru

Pokud raději **převádíte obrázek na text** a chcete jej uložit, stačí zapsat řetězec do souboru `.txt`:

```csharp
System.IO.File.WriteAllText("output.txt", recognizedText);
```

## Často kladené otázky

- **Potřebuji licenci pro spuštění tohoto kódu?**  
  Ne. Bezplatná zkušební verze funguje dobře pro experimentování, ale přidává vodoznak do výstupu. Zakoupená licence odstraní vodoznak a odemkne plný výkon.

- **Mohu to použít na Linuxu?**  
  Rozhodně. Aspose.OCR je multiplatformní; stačí zajistit, že máte požadované nativní závislosti (libgdiplus pro .NET Core na Linuxu).

- **Co když je můj obrázek ve streamu místo souboru?**  
  Použijte `ImageStream.FromStream(yourStream)` – API přijímá libovolný `System.IO.Stream`.

## Závěr

Provedli jsme vás krok za krokem **jak používat OCR** v C# k **extrahování textu z obrázku**, **převodu obrázku na text** a **čtení korejských znaků**, přičemž jsme správně **načítali obrázek pro OCR**. Kompletní, spustitelný příklad výše by měl fungovat ihned, a další tipy vám poskytují plán pro pokročilejší scénáře.

Jste připraveni na další výzvu? Zkuste nahradit jazyk, zpracovávat PDF stránku po stránce nebo integrovat volání OCR do webového API, aby uživatelé mohli nahrávat obrázky a získat okamžité textové výsledky. Možnosti jsou neomezené a nyní máte pevný základ, na kterém můžete stavět.

Šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}