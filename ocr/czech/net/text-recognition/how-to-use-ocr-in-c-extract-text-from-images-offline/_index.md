---
category: general
date: 2026-03-07
description: Naučte se, jak používat OCR v C# k extrahování textu z obrazových souborů.
  Tento průvodce ukazuje offline OCR, převod obrazu na text a načtení obrazu pro OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- convert image to text
- load image for ocr
language: cs
og_description: Jak použít OCR v C# k extrahování textu z obrázků offline. Krok za
  krokem kód, tipy a úplné vysvětlení převodu obrázku na text.
og_title: Jak používat OCR v C# – Kompletní offline průvodce
tags:
- OCR
- C#
- Aspose
title: Jak použít OCR v C# – Extrahovat text z obrázků offline
url: /cs/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-offline/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat OCR v C# – Extrahovat text z obrázků offline

Už jste se někdy zamýšleli **jak používat OCR** v .NET projektu, aniž byste odesílali data do cloudu? Nejste v tom sami. Mnoho vývojářů potřebuje *extrahovat text z obrázku* souborů na zabezpečeném pracovním stanovišti a obávají se, že síťový provoz může odhalit citlivé informace.

Dobrá zpráva? S Aspose.OCR můžete rozpoznávat text z PNG, JPEG nebo PDF zcela offline. V tomto tutoriálu vás provedeme načtením obrázku pro OCR, nastavením enginu do offline režimu a nakonec **převodem obrázku na text** pomocí několika řádků C#.

Na konci tohoto průvodce budete schopni:

* Nainstalovat NuGet balíček Aspose.OCR.  
* Nastavit OCR engine pro offline zpracování.  
* Načíst obrázek pro OCR a extrahovat jeho textový obsah.  

Žádné externí služby, žádné API klíče – jen čistý C# kód, který běží na jakémkoli Windows nebo Linux stroji.

---

## Požadavky

Než se pustíme dál, ujistěte se, že máte:

* .NET 6.0 SDK nebo novější (kód funguje také s .NET Framework 4.7+).  
* Visual Studio 2022, VS Code nebo jakýkoli editor podporující C#.  
* Kopii knihovny **Aspose.OCR** – můžete ji získat z NuGet (`Aspose.OCR`).  
* Složku s OCR zdroji (`Resources`), která je součástí knihovny (obsahuje soubory s jazykovými daty).  
* Vzorový obrázek (např. `offline_test.png`) umístěný v známém adresáři.

> **Tip:** Uchovávejte složku resources vedle spustitelného souboru; zjednodušuje to konfiguraci `ResourcesPath`.

## Krok 1: Instalace NuGet balíčku Aspose.OCR

Nejprve přidejte knihovnu do svého projektu. Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package Aspose.OCR
```

Nebo, pokud dáváte přednost UI ve Visual Studiu, klikněte pravým tlačítkem na **Dependencies → Manage NuGet Packages**, vyhledejte *Aspose.OCR* a klikněte na **Install**.

> Instalace balíčku stáhne všechny potřebné binární soubory, takže nebudete potřebovat žádné další DLL.

## Krok 2: Vytvoření a konfigurace OCR enginu (Jak používat OCR – Offline režim)

Nyní vytvoříme instanci OCR enginu a řekneme mu, aby pracoval **offline**. Tím zajistíme, že během rozpoznávání nebude probíhat žádný síťový provoz.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Switch the engine to offline mode – crucial for privacy‑first apps
ocrEngine.Settings.EngineMode = EngineMode.Offline;
```

**Proč offline?**  
Když je `EngineMode` nastaven na `Online`, engine kontaktuje cloud Aspose a stáhne jazykové balíčky za běhu. V regulovaných prostředích (finance, zdravotnictví) je takový provoz často zakázán. Vynucením offline režimu zaručíte, že vše zůstane na místním počítači.

## Krok 3: Nastavení cesty enginu ke složce OCR zdrojů

OCR engine potřebuje jazyková data (trénované modely) pro rozpoznávání znaků. Řekněte mu, kde se tyto soubory nacházejí:

```csharp
// Replace with the absolute or relative path to your Resources folder
ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";
```

Pokud si nejste jisti, kde je složka, najděte ji v adresáři NuGet balíčku (`%USERPROFILE%\.nuget\packages\aspose.ocr\*\resources`). Zkopírujte celou složku do svého projektu pro snadnější nasazení.

## Krok 4: Načtení obrázku pro OCR (Load Image for OCR)

Můžete enginu předat jakýkoli podporovaný bitmap. Zde načteme PNG uložený na disku:

```csharp
// Load the image you want to recognize – this is the “load image for OCR” step
ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");
```

**Tip:** Pokud potřebujete zpracovávat obrázky ze streamu (např. nahrané přes API), použijte místo toho `ImageStream.FromStream(yourStream)`.

## Krok 5: Spuštění procesu rozpoznávání a převod obrázku na text

S vše připravené spusťte OCR. Metoda `Recognize()` provede těžkou práci a extrahovaný text je dostupný přes vlastnost `Text`.

```csharp
// Perform OCR – this is where the engine reads the pixels and produces text
ocrEngine.Recognize();

// Grab the result – now you have “convert image to text” completed
string extractedText = ocrEngine.Text;
```

## Krok 6: Výstup extrahovaného textu

Nakonec zobrazte výsledek. V konzolové aplikaci můžete jednoduše zapisovat do konzole, ale ve webovém API byste řetězec vrátili jako JSON.

```csharp
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(extractedText);
```

Spuštěním programu by se měl vytisknout textový obsah souboru `offline_test.png`. Například pokud obrázek obsahuje frázi *„Hello, World!“*, uvidíte:

```
=== OCR Result ===
Hello, World!
```

## Kompletní funkční příklad

Níže je kompletní, připravený k spuštění program. Zkopírujte a vložte jej do nového konzolového projektu (`dotnet new console`) a upravte cesty tak, aby odpovídaly vašemu prostředí.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // Step 2: Set offline mode – no network traffic
        // -------------------------------------------------
        ocrEngine.Settings.EngineMode = EngineMode.Offline;

        // -------------------------------------------------
        // Step 3: Provide path to OCR resource files
        // -------------------------------------------------
        ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";

        // -------------------------------------------------
        // Step 4: Load the image you want to recognize
        // -------------------------------------------------
        ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");

        // -------------------------------------------------
        // Step 5: Run recognition and extract text
        // -------------------------------------------------
        ocrEngine.Recognize();
        string extractedText = ocrEngine.Text;

        // -------------------------------------------------
        // Step 6: Show the result
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);
    }
}
```

> **Očekávaný výstup:** Konzole vypíše přesný text obsažený v PNG souboru. Pokud je obrázek rozmazaný, výsledek může obsahovat nesprávně rozpoznané znaky – viz sekce s řešením problémů níže.

## Časté problémy a tipy (Efektivní rozpoznávání textu z PNG)

| Problém | Proč k tomu dochází | Jak opravit |
|-------|----------------|------------|
| **Prázdný výstup** | ResourcesPath ukazuje na špatnou složku nebo chybí jazykové soubory. | Ověřte, že složka obsahuje `eng.traineddata` (nebo jiné jazykové soubory) a dvojitě zkontrolujte řetězec cesty. |
| **Špatné znaky** | Rozlišení obrázku je příliš nízké nebo obrázek není binarizován. | Předzpracujte obrázek (zvyšte DPI, použijte `ImageProcessor` k zaostření). |
| **Zpomalení výkonu** | Velké obrázky jsou zpracovávány v plném rozlišení. | Změňte velikost obrázku na maximální šířku 2000 px před předáním OCR. |
| **Nesprávný formát** | Použití BMP s neobvyklým formátem pixelu. | Převeďte obrázek nejprve na PNG nebo JPEG (`System.Drawing.Image.Save`). |

**Tip:** Pokud potřebujete rozpoznávat více jazyků, nastavte `ocrEngine.Settings.Language = Language.English | Language.French;` před voláním `Recognize()`.

## Často kladené otázky

**Q: Můžu tento kód použít na Linuxu?**  
Ano. Aspose.OCR je multiplatformní; stačí zajistit, že jsou přítomny nativní knihovny (jsou součástí NuGet balíčku).

**Q: Co když nemám složku Resources?**  
Můžete si stáhnout zdarma jazykové balíčky z webu Aspose nebo je extrahovat z NuGet balíčku (`.../aspose.ocr/<version>/resources`).

**Q: Existuje způsob, jak získat skóre důvěry?**  
Ano. Po volání `Recognize()` prohlédněte `ocrEngine.RecognizedWords` – každé slovo obsahuje vlastnost `Confidence`.

## Závěr

Probrali jsme **jak používat OCR** v C# k *extrahování textu z obrázku* souborů zcela offline. Instalací Aspose.OCR, nastavením `EngineMode.Offline`, určením cesty ke zdrojům, načtením obrázku a voláním `Recognize()` můžete spolehlivě **převést obrázek na text** aniž byste se kdykoli připojili k internetu.

Vezměte výše uvedený kód, nahraďte vlastní cesty k obrázkům a začněte vytvářet funkce jako prohledávatelné PDF, automatizaci zadávání dat nebo nástroje pro přístupnost. Dále můžete zkoumat **rozpoznávání textu z PNG** hromadně, nebo integrovat engine do ASP.NET Core API pro poskytování OCR výsledků front‑end aplikacím.

Šťastné programování a nebojte se experimentovat – OCR je překvapivě shovívavé, jakmile je engine správně nastaven!

--- 

![Diagram ukazující offline OCR workflow – jak používat OCR v zabezpečeném prostředí](https://example.com/ocr-workflow.png "jak používat OCR diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}