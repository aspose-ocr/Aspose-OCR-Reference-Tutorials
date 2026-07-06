---
category: general
date: 2026-04-11
description: Naučte se, jak v Aspose OCR pro C# vypnout OCR, aby fungoval offline,
  extrahovat text z obrázku bez připojení k internetu a správně načíst obrázek pro
  OCR.
draft: false
keywords:
- how to disable OCR
- extract text from image
- load image for OCR
- offline OCR C#
- Aspose OCR resources
language: cs
og_description: Jak zakázat OCR v Aspose OCR pro C# a spustit offline, extrahovat
  text z obrázku bez potřeby internetu a snadno načíst obrázek pro OCR.
og_title: Jak zakázat OCR v C# – Offline průvodce Aspose OCR
tags:
- C#
- OCR
- Aspose
- Offline Processing
title: Jak zakázat OCR v C# – Offline průvodce Aspose OCR
url: /cs/net/ocr-configuration/how-to-disable-ocr-in-c-offline-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zakázat OCR v C# – Offline průvodce Aspose OCR

Už jste se někdy zamysleli **jak zakázat OCR**, když potřebujete skutečně offline řešení? Možná vytváříte zabezpečenou desktopovou aplikaci, která se nemůže spoléhat na síťové připojení, nebo prostě chcete předejít nečekaným stažení souborů. Ať už je to jakkoli, dobrá zpráva je, že Aspose OCR vám umožní vypnout automatické stahování zdrojů, nasměrovat jej na lokální složku a mít vše on‑premises. V tomto tutoriálu také uvidíte, jak **extrahovat text z obrázku** a správně **načíst obrázek pro OCR** bez jakýchkoli problémů.

Provedeme kompletní, připravený příklad, který ukazuje každý krok – od inicializace enginu až po výpis rozpoznaného japonského textu. Žádná externí dokumentace, žádná skrytá magie; jen čistý C# kód, který můžete dnes vložit do svého projektu. Na konci budete vědět, proč je důležité vypnout funkci automatického stahování, jak nastavit cestu ke zdrojům a na jaké úskalí si dát pozor.

## Požadavky

- .NET 6.0 (nebo jakákoli novější verze .NET) nainstalovaná ve vašem počítači.  
- NuGet balíček Aspose.OCR for .NET (`Install-Package Aspose.OCR`).  
- Složka, která již obsahuje jazykové zdroje, jež potřebujete (např. japonský model).  
- Soubor obrázku (`japan_doc.png`), na který chcete spustit OCR.  

Pokud vám chybí jazykové balíčky, stáhněte si je jednou z portálu Aspose, rozbalte do složky např. `AsposeOCRResources` a jste připraveni. Po vypnutí funkce automatického stahování se žádná další stažení nebudou provádět.

![Jak zakázat OCR offline](/images/how-to-disable-ocr.png "ilustrace jak zakázat OCR")

## Krok 1 – Vytvoření instance OCR enginu  

Prvním krokem je vytvořit instanci `OcrEngine`. Představte si tento objekt jako mozek, který bude číst váš obrázek.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Proč je to důležité:** Bez enginu nemůžete nic konfigurovat. Objekt drží všechna nastavení, včetně klíčového příznaku, který knihovně říká, zda může přistupovat k internetu.

## Krok 2 – Vypnutí automatického stahování zdrojů  

Ve výchozím nastavení se Aspose OCR pokusí načíst chybějící jazykové soubory za běhu. Pro zachování offline režimu přepněte přepínač `AutoDownloadResources` na `false`.

```csharp
        // Step 2: Disable automatic resource download to work offline
        ocrEngine.Settings.AutoDownloadResources = false;
```

> **Tip:** Vypnutí této funkce nejen zaručuje soukromí, ale také urychluje první rozpoznání, protože engine neplýtvá časem kontrolou aktualizací.

## Krok 3 – Nastavení cesty k lokální složce se zdroji  

Nyní řekněte enginu, kde se nachází předem stažené jazykové balíčky. Jedná se o cestu, kterou jste nastavili v předchozích požadavcích.

```csharp
        // Step 3: Point the engine to the folder containing pre‑downloaded resources
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";
```

> **Co může jít špatně?** Pokud je cesta špatná nebo chybí požadovaný jazykový soubor, engine vyhodí `ResourceNotFoundException`. Zkontrolujte pravopis složky a ujistěte se, že japonský model (`jpn.traineddata`) je přítomen.

## Krok 4 – Výběr lokálního jazykového modelu  

Zvolte jazyk, který máte skutečně na disku. V našem příkladu používáme japonštinu, ale můžete nahradit `Language.Japanese` libovolným jiným jazykem, který jste si stáhli.

```csharp
        // Step 4: Select the language model that is available locally
        ocrEngine.Settings.Language = Language.Japanese;
```

> **Hraniční případ:** Některé jazyky vyžadují dodatečné slovníky (např. čínština). Ujistěte se, že i tyto pomocné soubory jsou ve stejné složce se zdroji.

## Krok 5 – Načtení obrázku pro OCR  

Zde **načteme obrázek pro OCR**. Metoda `ImageStream.FromFile` načte soubor do proudu, který Aspose může zpracovat.

```csharp
        // Step 5: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/japan_doc.png");
```

> **Tip:** Podporované formáty zahrnují PNG, JPEG, BMP a TIFF. Pokud potřebujete pracovat s PDF, nejprve každou stránku převedete na obrázek.

## Krok 6 – Spuštění rozpoznávacího procesu  

Nyní engine skutečně čte pixely a snaží se je převést na text.

```csharp
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Proč může být tento krok pomalý:** OCR je náročné na CPU, zejména u vysoce rozlišených obrázků. Pokud vás výkon trápí, zvažte předzmenšení obrázku před rozpoznáním.

## Krok 7 – Výpis extrahovaného textu  

Nakonec **extrahujeme text z obrázku** a vypíšeme jej do konzole.

```csharp
        // Step 7: Output the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Spuštění programu by mělo zobrazit japonské znaky, které byly v souboru `japan_doc.png`. Pokud je vše nastaveno správně, uvidíte čistý blok Unicode textu ve vaší konzoli.

### Očekávaný výstup

```
これはサンプルの日本語テキストです。
```

(Váš skutečný výstup bude záviset na obsahu obrázku.)

## Časté úskalí a jak se jim vyhnout  

| Problém | Proč se vyskytuje | Řešení |
|-------|----------------|-----|
| **Chybějící jazykový soubor** | `AutoDownloadResources` je nastaven na false, takže engine nemůže soubor stáhnout. | Ověřte, že `ResourcesPath` ukazuje na složku obsahující `jpn.traineddata`. |
| **Nesprávná cesta k obrázku** | `ImageStream.FromFile` vyhodí `FileNotFoundException`. | Použijte absolutní cesty nebo se ujistěte, že pracovní adresář je nastaven správně. |
| **Nepodporovaný formát obrázku** | Aspose čte jen určité formáty. | Před voláním `FromFile` převěďte obrázek na PNG nebo JPEG. |
| **Nedostatek paměti u velkých obrázků** | OCR načte celý obrázek do paměti. | Zmenšete nebo rozdělete obrázek, nebo zvýšte limit paměti procesu. |

## Rozšíření příkladu  

- **Dávkové zpracování:** Procházejte složku s obrázky, volajte stejný rozpoznávací kód a výsledek uložte do samostatného `.txt` souboru.  
- **Různé jazyky:** Nahraďte `Language.Japanese` za `Language.English` (nebo jiný) po umístění odpovídajících souborů zdrojů.  
- **Vlastní předzpracování:** Použijte Aspose.Imaging k deskewování nebo zlepšení kontrastu před OCR pro vyšší přesnost.

## Závěr  

Nyní víte **jak zakázat OCR** v Aspose OCR pro C# a spustit jej zcela offline. Nastavením `AutoDownloadResources` na `false`, nasměrováním enginu na lokální složku se zdroji a správným **načtením obrázku pro OCR** můžete spolehlivě **extrahovat text z obrázku** bez jakéhokoli přístupu k internetu. Tento přístup je ideální pro zabezpečená prostředí, CI pipeline nebo jakýkoli scénář, kde je síťový přístup omezený.

Jste připraveni na další krok? Zkuste zpracovat celou složku naskenovaných PDF, experimentujte s různými jazykovými balíčky nebo integrujte výsledek OCR do prohledávatelné databáze. Offline nastavení, které jste dnes vytvořili, je solidním základem pro jakýkoli on‑premises workflow zpracování dokumentů.

Šťastné programování a neváhejte zanechat komentář, pokud narazíte na potíže!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}