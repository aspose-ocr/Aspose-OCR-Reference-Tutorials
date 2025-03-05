---
title: Získejte obdélníky pro odstavce v rozpoznávání obrazu OCR
linktitle: Získejte obdélníky pro odstavce v rozpoznávání obrazu OCR
second_title: Aspose.OCR .NET API
description: Odemkněte pokročilé možnosti OCR s Aspose.OCR pro .NET. Extrahujte obdélníky odstavců bez námahy.
type: docs
weight: 11
url: /cs/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
---
## Úvod

Vítejte v našem komplexním průvodci o využití Aspose.OCR pro .NET k extrahování obdélníků odstavců při rozpoznávání obrázků OCR. Pokud chcete zlepšit své možnosti zpracování dokumentů a využít sílu optického rozpoznávání znaků (OCR) ve svých aplikacích .NET, jste na správném místě.

## Předpoklady

Než se pustíme do výukového programu, ujistěte se, že máte splněny následující předpoklady:

- Základní znalost vývoje v C# a .NET.
-  Vývojové prostředí nastavené pomocí Aspose.OCR pro .NET. Pokud jste to ještě neudělali, můžete si ji stáhnout[tady](https://releases.aspose.com/ocr/net/).
- Pochopení konceptů zpracování obrazu a důležitosti OCR při extrahování textu z obrázků.

## Importovat jmenné prostory

V kódu C# se ujistěte, že máte naimportovány potřebné jmenné prostory pro efektivní použití Aspose.OCR. V horní části souboru uveďte následující:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Krok 1: Nastavte adresář dokumentů

Začněte inicializací cesty k adresáři vašeho dokumentu, kde jsou uloženy obrázky pro zpracování OCR:

```csharp
string dataDir = "Your Document Directory";
```

## Krok 2: Inicializujte instanci AsposeOcr

Vytvořte instanci třídy AsposeOcr, abyste získali přístup k funkcím OCR:

```csharp
AsposeOcr api = new AsposeOcr();
```

## Krok 3: Zadejte cestu obrázku

Definujte úplnou cestu k obrázku, který chcete zpracovat:

```csharp
string fullPath = dataDir + "sample.png";
```

## Krok 4: Rozpoznejte obrázek a získejte obdélníky odstavce

 Vyvolat`GetRectangles` metoda k získání obdélníků pro odstavce v obrazu OCR. Soubor`detect_areas` na`true` pokud chcete extrahovat odstavce:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## Krok 5: Tisk výsledků

Vytiskněte souřadnice identifikovaných oblastí:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## Krok 6: Závěr

Gratulujeme! Úspěšně jste provedli proces rozpoznávání obrazu OCR k získání obdélníků pro odstavce pomocí Aspose.OCR for .NET.

## Závěr

V tomto tutoriálu jsme prozkoumali základní kroky k integraci Aspose.OCR for .NET do vašich aplikací, což vám umožní extrahovat obdélníky odstavců z obrázků zpracovaných OCR. Aspose.OCR zjednodušuje implementaci OCR, což z něj činí cenný nástroj pro zpracování dokumentů a extrakci textu.

## FAQ

### Q1: Je Aspose.OCR kompatibilní s různými formáty obrázků?

Odpověď 1: Ano, Aspose.OCR podporuje různé formáty obrázků, včetně PNG, JPEG a TIFF.

### Q2: Mohu použít Aspose.OCR pro dávkové zpracování více obrázků?

A2: Rozhodně! Aspose.OCR usnadňuje dávkové zpracování pro bezproblémové zpracování více obrázků.

### Q3: Je k dispozici bezplatná zkušební verze pro Aspose.OCR pro .NET?

 A3: Ano, můžete prozkoumat bezplatnou zkušební verzi[tady](https://releases.aspose.com/).

### Q4: Jak mohu získat dočasnou licenci pro Aspose.OCR?

 A4: Můžete získat dočasnou licenci[tady](https://purchase.aspose.com/temporary-license/).

### Q5: Kde najdu další podporu a diskuse týkající se Aspose.OCR?

 A5: Přejděte na[Fórum Aspose.OCR](https://forum.aspose.com/c/ocr/16) za podporu komunity a diskuze.