---
date: 2025-12-17
description: Naučte se, jak extrahovat obdélníky pro odstavce v OCR obrázcích pomocí
  Aspose.OCR pro .NET – průvodce, který vám ukáže, jak extrahovat obdélníky a získat
  souřadnice odstavců.
linktitle: Get Rectangles for Paragraphs in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Jak získat obdélníky pro odstavce při rozpoznávání obrazu OCR
url: /cs/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak extrahovat obdélníky pro odstavce v OCR rozpoznávání obrazu

## Úvod

Vítejte v našem komplexním průvodci, **jak extrahovat obdélníky** pro odstavce v OCR rozpoznávání obrazu pomocí Aspose.OCR pro .NET. Pokud chcete vylepšit svůj dokument‑zpracovatelský řetězec, získat hranice odstavců a automatizovat extrakci dat, jste na správném místě. Provedeme vás každým krokem — od nastavení prostředí po výpis souřadnic obdélníků — abyste mohli okamžitě začít používat výsledky OCR.

## Rychlé odpovědi
- **Co znamená „extrahovat obdélníky“?** Vrací ohraničující rámečky (x, y, šířka, výška) detekovaných oblastí textu.  
- **Která metoda API poskytuje obdélníky?** `AsposeOcr.GetRectangles` s `AreasType.PARAGRAPHS`.  
- **Potřebuji licenci pro vývoj?** Bezplatná zkušební verze funguje pro testování; pro produkci je vyžadována komerční licence.  
- **Mohu zpracovávat více obrázků najednou?** Ano — projděte seznam obrázků a zavolejte `GetRectangles` pro každý soubor.  
- **Jaké formáty jsou podporovány?** PNG, JPEG, TIFF, BMP a mnoho dalších.

## Co znamená „extrahovat obdélníky“ v OCR?

V terminologii OCR znamená extrahování obdélníků identifikaci geometrických hranic, které ohraničují každý odstavec nebo řádek textu v obrázku. Tyto souřadnice vám umožní zvýraznit, oříznout nebo dále analyzovat konkrétní části naskenovaného dokumentu.

## Proč extrahovat souřadnice odstavců?
- **Přesné post‑zpracování** – můžete každým obdélníkem napájet následné pracovní postupy (např. překlad, redakce).  
- **Vylepšené UI/UX** – překryjte ohraničující rámečky na původním obrázku, aby uživatelé viděli, kde byl text nalezen.  
- **Dávková automatizace** – rychle najděte a izolujte odstavce v rozsáhlých sadách dokumentů.

## Předpoklady

- Základní znalost C# a vývoje v .NET.  
- Vývojové prostředí s nainstalovaným Aspose.OCR pro .NET – můžete jej stáhnout [zde](https://releases.aspose.com/ocr/net/).  
- Znalost konceptů zpracování obrazu a proč je OCR nezbytné pro extrakci textu ze skenovaných souborů.

## Importujte jmenné prostory

Ve vašem souboru C# importujte požadované jmenné prostory, aby byly třídy OCR k dispozici:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Krok 1: Nastavte adresář dokumentů

Definujte složku, která obsahuje obrázky, jež chcete analyzovat:

```csharp
string dataDir = "Your Document Directory";
```

## Krok 2: Inicializujte instanci AsposeOcr

Vytvořte objekt `AsposeOcr` – poskytne vám přístup ke všem funkcím OCR:

```csharp
AsposeOcr api = new AsposeOcr();
```

## Krok 3: Zadejte cestu k obrázku

Ukazujte na konkrétní soubor obrázku, který chcete zpracovat:

```csharp
string fullPath = dataDir + "sample.png";
```

## Krok 4: Rozpoznání obrázku a získání obdélníků odstavců

Zavolejte metodu `GetRectangles`. Nastavením `detect_areas` na `true` řeknete enginu, aby vrátil **odstavcové** obdélníky:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## Krok 5: Vytiskněte výsledky

Vypište souřadnice, abyste viděli **extrahované souřadnice odstavců**, které byly detekovány:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## Časté problémy a řešení

| Problém | Důvod | Řešení |
|-------|--------|-----|
| Žádné obdélníky nebyly vráceny | Kvalita obrazu je příliš nízká nebo špatný `AreasType` | Ujistěte se, že je obrázek čistý a použijte `AreasType.PARAGRAPHS`. |
| Souřadnice jsou posunuty o jeden | Neshoda DPI škálování | Nastavte správné DPI při načítání obrázku nebo použijte `api.Config.Dpi`. |
| Výjimka licence | Spuštěno bez platné licence v produkci | Aplikujte dočasnou nebo trvalou licenci pomocí `api.SetLicense`. |

## Často kladené otázky

**Q: Je Aspose.OCR kompatibilní s různými formáty obrázků?**  
A: Ano, Aspose.OCR podporuje PNG, JPEG, TIFF, BMP a mnoho dalších běžných formátů.

**Q: Mohu použít Aspose.OCR pro dávkové zpracování více obrázků?**  
A: Rozhodně! Projděte kolekci cest k souborům a zavolejte `GetRectangles` pro každý obrázek.

**Q: Je k dispozici bezplatná zkušební verze Aspose.OCR pro .NET?**  
A: Ano, můžete si vyzkoušet bezplatnou verzi [zde](https://releases.aspose.com/).

**Q: Jak mohu získat dočasnou licenci pro Aspose.OCR?**  
A: Dočasnou licenci můžete získat [zde](https://purchase.aspose.com/temporary-license/).

**Q: Kde mohu najít další podporu a diskuse související s Aspose.OCR?**  
A: Navštivte [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) pro komunitní podporu a diskuse.

## Závěr

V tomto tutoriálu jsme ukázali **jak extrahovat obdélníky** pro odstavce pomocí Aspose.OCR pro .NET, prošli jsme každým úryvkem kódu a vysvětlili, jak interpretovat vrácené souřadnice. Integrací těchto kroků do vaší aplikace můžete spolehlivě získávat hranice odstavců, vylepšovat pracovní postupy dokumentů a vytvářet chytřejší OCR‑řízená řešení.

---

**Poslední aktualizace:** 2025-12-17  
**Testováno s:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}