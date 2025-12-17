---
date: 2025-12-17
description: Naučte se, jak získat OCR obdélníky řádků pomocí Aspose.OCR pro .NET,
  rozpoznávat textové řádky v obrázcích a snadno extrahovat souřadnice řádků.
linktitle: Get OCR Line Rectangles for Image Text Lines
second_title: Aspose.OCR .NET API
title: Získat OCR obdélníky řádků pro textové řádky obrázku
url: /cs/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Získání OCR obdélníků řádků pro textové řádky na obrázku

## Úvod

V tomto tutoriálu se dozvíte **jak získat OCR obdélníky řádků** pomocí Aspose.OCR pro .NET. Na konci průvodce budete schopni **rozpoznat textové řádky na obrázku** a **extrahovat souřadnice řádků** pro každý detekovaný řádek — ideální pro následné zpracování, jako je analýza rozvržení, extrakce dat nebo vlastní vykreslování.

## Rychlé odpovědi
- **Co znamená „získat OCR obdélníky řádků“?** Vrací ohraničující rámečky každého textového řádku detekovaného na obrázku.  
- **Která metoda API se používá?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro vývoj; pro produkci je vyžadována komerční licence.  
- **Podporované formáty obrázků?** PNG, JPEG, BMP, TIFF a další.  
- **Mohu to spustit na .NET Core?** Ano, Aspose.OCR plně podporuje .NET Core a .NET 5/6.

## Předpoklady

Před tím, než se ponoříte do tutoriálu, ujistěte se, že máte následující předpoklady:

- Základní znalosti C# a vývoje v .NET.  
- Integrované vývojové prostředí (IDE) jako Visual Studio.  
- Knihovna Aspose.OCR pro .NET nainstalována. Můžete si ji stáhnout [zde](https://releases.aspose.com/ocr/net/).  
- Ukázkový obrázek obsahující text pro OCR rozpoznání.

## Importování jmenných prostorů

Ujistěte se, že máte do projektu importovány potřebné jmenné prostory. Přidejte následující řádky na začátek vašeho C# souboru:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Nyní si rozdělíme proces získávání obdélníků řádků v OCR rozpoznávání obrázku na snadno sledovatelné kroky.

## Krok 1: Nastavte adresář dokumentu

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Nahraďte `"Your Document Directory"` skutečnou cestou ke složce, která obsahuje váš ukázkový obrázek.

## Krok 2: Inicializujte Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Vytvořte instanci třídy `AsposeOcr` pro přístup k OCR funkcionalitě.

## Krok 3: Zadejte cestu k obrázku

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Definujte úplnou cestu k obrázku, na kterém chcete provést OCR.

## Krok 4: Rozpoznat obrázek a získat obdélníky

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

Metoda `GetRectangles` vrací seznam objektů `Rectangle`, z nichž každý představuje souřadnice detekovaného textového řádku. Toto je jádro **získávání OCR obdélníků řádků**.

## Krok 5: Vytisknout výsledek

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Vytiskněte souřadnice detekovaných oblastí do konzole. Uvidíte hodnoty, které můžete později použít k **extrakci souřadnic řádků** pro vlastní zpracování.

## Proč použít Aspose.OCR pro obdélníky řádků?

- **Vysoká přesnost** – Pokročilé algoritmy detekují řádky i v šumových nebo nakloněných obrázcích.  
- **Cross‑platform** – Funguje na .NET Framework, .NET Core a .NET 5/6.  
- **Žádné externí závislosti** – Čistá .NET knihovna, nevyžaduje nativní DLL soubory.  
- **Bohatý výstup** – Kromě obdélníků řádků můžete také získat slova, znaky a skóre důvěry.

## Časté problémy a řešení

| Problém | Řešení |
|-------|----------|
| **Žádné obdélníky vráceny** | Ujistěte se, že obrázek obsahuje jasný, horizontální text a že je specifikováno `AreasType.LINES`. |
| **Nesprávné souřadnice** | Ověřte DPI obrázku; obrázky s nízkým rozlišením mohou způsobovat nepřesné ohraničení. |
| **Úzké hrdlo výkonu u velkých obrázků** | Změňte velikost obrázku na rozumné rozlišení před voláním `GetRectangles`. |
| **Výjimka licence** | Použijte zkušební licenci pro testování; aplikujte plnou licenci pro produkci, aby se předešlo omezením hodnocení. |

## Často kladené otázky

### Q1: Mohu použít Aspose.OCR pro .NET s jakýmkoli typem obrázku?

A1: Aspose.OCR podporuje širokou škálu formátů obrázků, což zajišťuje flexibilitu ve vašich OCR aplikacích.

### Q2: Jak přesné je rozpoznávání OCR?

A2: Aspose.OCR využívá pokročilé algoritmy pro vysokou přesnost, což jej činí vhodným pro různé scénáře rozpoznávání textu.

### Q3: Je k dispozici zkušební verze?

A3: Ano, můžete prozkoumat možnosti Aspose.OCR pro .NET pomocí [bezplatné zkušební verze](https://releases.aspose.com/).

### Q4: Kde najdu komplexní dokumentaci?

A4: Podívejte se na [dokumentaci](https://reference.aspose.com/ocr/net/) pro podrobné informace a pokyny k použití.

### Q5: Potřebujete pomoc nebo máte konkrétní otázky?

A5: Navštivte [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) pro podporu komunity a diskuze.

## Často kladené otázky

**Q: Mohu extrahovat jednotlivá slova místo celých řádků?**  
A: Ano, použijte `AreasType.WORDS` se stejnou metodou `GetRectangles` pro získání ohraničujících rámečků na úrovni slov.

**Q: Podporuje API více‑stránkové PDF?**  
A: Nejprve převěďte každou stránku PDF na obrázek a poté zavolejte `GetRectangles` na každém obrázku.

**Q: Jak zacházet s otočeným textem?**  
A: Aktivujte možnost automatického otočení v nastavení OCR nebo předzpracujte obrázek otočením před zpracováním.

**Q: Existuje způsob, jak získat skóre důvěry pro každý řádek?**  
A: Po získání obdélníků zavolejte `api.RecognizeImage(...).Lines` pro přístup k objektům řádků, které obsahují hodnoty důvěry.

**Q: Jaké verze .NET jsou kompatibilní?**  
A: Knihovna funguje s .NET Framework 4.5+, .NET Core 3.1+ a .NET 5/6.

## Závěr

Gratulujeme! Úspěšně jste **získali OCR obdélníky řádků** pro obrázek pomocí Aspose.OCR pro .NET. S ohraničujícími rámečky v ruce můžete nyní předávat souřadnice řádků do následných pracovních toků, jako je vlastní vykreslování, extrakce dat nebo analýza rozvržení.

---

**Poslední aktualizace:** 2025-12-17  
**Testováno s:** Aspose.OCR 24.11 pro .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}