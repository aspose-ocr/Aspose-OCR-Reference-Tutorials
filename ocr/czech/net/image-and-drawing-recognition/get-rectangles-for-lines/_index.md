---
date: 2026-02-22
description: Naučte se provádět analýzu rozložení OCR rozpoznáváním textových řádků
  na obrázku a extrahováním obdélníků řádků pomocí Aspose.OCR pro .NET.
linktitle: Layout Analysis OCR – Get Line Rectangles from Images
second_title: Aspose.OCR .NET API
title: Analýza rozvržení OCR – Získat obdélníky řádků z obrázků
url: /cs/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analýza rozvržení OCR – Získání obdélníků řádků z obrázků

## Úvod

V tomto tutoriálu se dozvíte **jak získat OCR obdélníky řádků** pomocí Aspose.OCR pro .NET. Na konci průvodce budete schopni **rozpoznat textové řádky na obrázku** a **extrahovat souřadnice řádků** pro každý detekovaný řádek – ideální pro následné zpracování, jako je **analýza rozvržení OCR**, extrakce dat nebo vlastní vykreslování.

## Rychlé odpovědi
- **Co znamená „získat OCR obdélníky řádků“?** Vrací ohraničující rámečky každého textového řádku detekovaného na obrázku.  
- **Která metoda API se používá?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro vývoj; pro produkci je vyžadována komerční licence.  
- **Podporované formáty obrázků?** PNG, JPEG, BMP, TIFF a další.  
- **Mohu to spustit na .NET Core?** Ano, Aspose.OCR plně podporuje .NET Core a .NET 5/6.

## Předpoklady

Než se pustíte do tutoriálu, ujistěte se, že máte splněny následující předpoklady:

- Základní znalost C# a vývoje v .NET.  
- Integrované vývojové prostředí (IDE), například Visual Studio.  
- Knihovna Aspose.OCR pro .NET nainstalovaná. Můžete ji stáhnout [zde](https://releases.aspose.com/ocr/net/).  
- Vzorek obrázku obsahujícího text pro OCR rozpoznání.

## Import Namespaces

Ujistěte se, že do projektu máte importovány potřebné jmenné prostory. Přidejte následující řádky na začátek vašeho C# souboru:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Nyní si rozložíme proces získávání obdélníků řádků v OCR rozpoznávání obrázku na snadno sledovatelné kroky.

## layout analysis ocr – Krok‑za‑krokem průvodce

### Krok 1: Nastavte adresář dokumentu

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Nahraďte `"Your Document Directory"` skutečnou cestou ke složce, která obsahuje váš vzorový obrázek.

### Krok 2: Inicializujte Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Vytvořte instanci třídy `AsposeOcr`, abyste získali přístup k OCR funkcionalitě.

### Krok 3: Zadejte cestu k obrázku

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Definujte úplnou cestu k obrázku, na kterém chcete provést OCR.

### Krok 4: Rozpoznání obrázku a získání obdélníků

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

Metoda `GetRectangles` vrací seznam objektů `Rectangle`, z nichž každý představuje souřadnice detekovaného textového řádku. Toto je jádro **získání OCR obdélníků řádků** a umožňuje **analýzu rozvržení OCR**.

### Krok 5: Výpis výsledku

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Vytiskněte souřadnice detekovaných oblastí do konzole. Uvidíte hodnoty, které můžete později použít k **extrakci souřadnic řádků** pro vlastní zpracování.

## Proč použít Aspose.OCR pro obdélníky řádků?

- **Vysoká přesnost** – Pokročilé algoritmy detekují řádky i v šumových nebo nakloněných obrázcích.  
- **Cross‑platform** – Funguje na .NET Framework, .NET Core i .NET 5/6.  
- **Žádné externí závislosti** – Čistá .NET knihovna, nevyžaduje nativní DLL soubory.  
- **Bohatý výstup** – Kromě obdélníků řádků můžete také získat slova, znaky a skóre důvěry.

## Časté problémy a řešení

| Problém | Řešení |
|-------|----------|
| **Nejsou vráceny žádné obdélníky** | Ujistěte se, že obrázek obsahuje jasný, horizontální text a že je specifikováno `AreasType.LINES`. |
| **Nesprávné souřadnice** | Ověřte DPI obrázku; obrázky s nízkým rozlišením mohou způsobovat nepřesné ohraničení. |
| **Úzké hrdlo výkonu u velkých obrázků** | Před voláním `GetRectangles` změňte velikost obrázku na rozumné rozlišení. |
| **Výjimka licence** | Pro testování použijte zkušební licenci; pro produkci aplikujte plnou licenci, aby se předešlo omezením hodnocení. |

## Často kladené otázky

**Q: Mohu extrahovat jednotlivá slova místo celých řádků?**  
A: Ano, použijte `AreasType.WORDS` se stejnou metodou `GetRectangles` pro získání ohraničujících rámečků na úrovni slov.

**Q: Podporuje API více‑stránkové PDF?**  
A: Nejprve převěďte každou stránku PDF na obrázek a poté zavolejte `GetRectangles` na každý obrázek.

**Q: Jak zacházet s otočeným textem?**  
A: Aktivujte možnost automatického otočení v nastavení OCR nebo předzpracujte obrázek otočením.

**Q: Existuje způsob, jak získat skóre důvěry pro každý řádek?**  
A: Po získání obdélníků zavolejte `api.RecognizeImage(...).Lines` a získáte objekty řádků, které obsahují hodnoty důvěry.

**Q: Jaké verze .NET jsou kompatibilní?**  
A: Knihovna funguje s .NET Framework 4.5+, .NET Core 3.1+ a .NET 5/6.

## Reálné příklady použití

- **Analýza rozvržení dokumentu OCR** – Vložte obdélníky řádků do rozvrhového enginu pro rekonstrukci sloupcových struktur.  
- **Automatizovaná extrakce dat** – Použijte souřadnice k oříznutí jednotlivých řádků pro následné NLP pipeline.  
- **Vlastní vykreslování** – Překryjte ohraničující rámečky na původním obrázku pro vizuální ověření nebo UI overlaye.

## Závěr

Gratulujeme! Úspěšně jste **získali OCR obdélníky řádků** pro obrázek pomocí Aspose.OCR pro .NET. S těmito ohraničujícími rámečky můžete nyní předávat souřadnice řádků do následných pracovních toků, jako je vlastní vykreslování, extrakce dat nebo **analýza rozvržení OCR**.

---

**Poslední aktualizace:** 2026-02-22  
**Testováno s:** Aspose.OCR 24.11 pro .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}