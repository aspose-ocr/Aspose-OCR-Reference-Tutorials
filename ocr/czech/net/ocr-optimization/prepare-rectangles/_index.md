---
title: Připravte obdélníky v rozpoznávání obrazu OCR
linktitle: Připravte obdélníky v rozpoznávání obrazu OCR
second_title: Aspose.OCR .NET API
description: Odemkněte potenciál Aspose.OCR pro .NET pomocí našeho komplexního průvodce. Naučte se krok za krokem připravit obdélníky pro rozpoznávání obrázků. Vylepšete své aplikace .NET pomocí bezproblémové integrace OCR.
type: docs
weight: 11
url: /cs/net/ocr-optimization/prepare-rectangles/
---
## Úvod

V neustále se vyvíjejícím prostředí technologií hraje optické rozpoznávání znaků (OCR) klíčovou roli při transformaci obrázků na strojově čitelný text. Aspose.OCR for .NET vyniká jako robustní řešení pro vývojáře, kteří hledají bezproblémovou integraci funkcí OCR do svých aplikací .NET. V tomto komplexním průvodci prozkoumáme proces přípravy obdélníků v rozpoznávání obrázků OCR pomocí Aspose.OCR for .NET.

## Předpoklady

Než se ponoříte do výukového programu, ujistěte se, že máte splněny následující předpoklady:

- Pracovní znalost vývoje .NET.
-  Nainstalovaná knihovna Aspose.OCR for .NET. Můžete si jej stáhnout[tady](https://releases.aspose.com/ocr/net/).
- Základní porozumění konceptům rozpoznávání obrazu.

## Importovat jmenné prostory

Začněme importem potřebných jmenných prostorů k zahájení naší cesty OCR:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Krok 1: Nastavte adresář dokumentů

 Začněte zadáním adresáře, kde jsou uloženy vaše dokumenty. Nahradit`"Your Document Directory"` se skutečnou cestou k vašim dokumentům.

```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";

// Inicializujte instanci AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Krok 2: Rozpoznejte obrázek s více obdélníky

tomto kroku si ukážeme, jak rozpoznat text z obrázku pomocí více obdélníků. Postupujte podle těchto dílčích kroků:

### 2.1 Definujte obdélníky

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### 2.2 Proveďte rozpoznání OCR

```csharp
// první případ
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Zobrazte rozpoznaný text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## Krok 3: Rozpoznejte obrázek pomocí nastavení rozpoznávání

V tomto kroku předvedeme alternativní metodu pomocí RecognitionSettings pro rozpoznávání obrázků:

### 3.1 Definujte nastavení rozpoznávání

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### 3.2 Zobrazení rozpoznaného textu

```csharp
// Zobrazte rozpoznaný text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Závěr

Gratulujeme! Úspěšně jste prošli procesem přípravy obdélníků v rozpoznávání obrázků OCR pomocí Aspose.OCR for .NET. Tato příručka vám umožňuje bezproblémovou integraci OCR do vašich aplikací .NET a vylepšuje jejich schopnosti rozpoznávání textu.

### FAQ

### Q1: Mohu použít Aspose.OCR pro .NET s jinými frameworky .NET?

Odpověď 1: Ano, Aspose.OCR for .NET je kompatibilní s různými frameworky .NET.

### Q2: Je k dispozici bezplatná zkušební verze pro Aspose.OCR pro .NET?

 A2: Rozhodně! Máte přístup k bezplatné zkušební verzi[tady](https://releases.aspose.com/).

### Q3: Jak získám podporu pro Aspose.OCR pro .NET?

 A3: Navštivte[Fórum Aspose.OCR](https://forum.aspose.com/c/ocr/16) za specializovanou podporu.

### Q4: Mohu získat dočasnou licenci pro testovací účely?

 A4: Ano, můžete získat dočasnou licenci[tady](https://purchase.aspose.com/temporary-license/).

### Q5: Kde najdu dokumentaci pro Aspose.OCR pro .NET?

 A5: Dokumentace je k dispozici[tady](https://reference.aspose.com/ocr/net/).