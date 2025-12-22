---
date: 2025-12-22
description: Naučte se, jak extrahovat text z obrázku pomocí Aspose.OCR pro .NET.
  Tento průvodce vás provede přípravou obdélníků pro OCR rozpoznávání obrazu a zvyšováním
  přesnosti.
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Jak extrahovat text z obrázku vytvořením obdélníků v OCR
url: /cs/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Připravte obdélníky v OCR rozpoznávání obrazu

## Úvod

Optical Character Recognition (OCR) je nezbytný pro převod vizuálního obsahu na prohledávatelný, editovatelný text. V tomto tutoriálu **extrahujete text z obrázku** tím, že připravíte vlastní obdélníky, které zaměří OCR engine na konkrétní oblasti. Pomocí Aspose.OCR pro .NET projdeme každý krok – od nastavení projektu až po získání rozpoznaného textu – abyste mohli integrovat výkonnou funkci převodu obrazu na text do svých .NET aplikací.

## Rychlé odpovědi
- **Co znamená “extrahovat text z obrázku”?** Znamená to převod vizuálních znaků na obrázku do strojově čitelných řetězců.  
- **Která knihovna pomáhá s tím v .NET?** Aspose.OCR for .NET.  
- **Potřebuji licenci pro vývoj?** Bezplatná zkušební verze funguje pro testování; licence je vyžadována pro produkci.  
- **Mohu cílit na konkrétní oblasti?** Ano, definováním obdélníků, které omezují rozsah OCR.  
- **Jaké verze .NET jsou podporovány?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Co je “extrahovat text z obrázku” s obdélníky?
Když na obrázku definujete obdélníkové zóny, OCR engine zpracuje pouze tyto zóny. To zvyšuje přesnost, snižuje dobu zpracování a umožňuje ignorovat šum v pozadí nebo irelevantní části.

## Proč připravit obdélníky před OCR?
- **Zaměřte se na relevantní obsah:** Přeskočte záhlaví, zápatí nebo dekorativní grafiku.  
- **Zvýšení výkonu:** Menší oblasti znamenají rychlejší rozpoznávání.  
- **Zlepšení přesnosti:** Méně vizuálního šumu vede k čistějším výsledkům.

## Požadavky

- Znalost C# a vývoje v .NET.  
- Knihovna Aspose.OCR pro .NET nainstalována – můžete ji stáhnout **[zde](https://releases.aspose.com/ocr/net/)**.  
- Ukázkový obrázek (např. `sample.png`), který obsahuje text, který chcete extrahovat.

## Importujte jmenné prostory

Nejprve načtěte požadované jmenné prostory do rozsahu:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Krok 1: Nastavte adresář dokumentů

Určete, kde se nacházejí vaše soubory obrázků, a vytvořte instanci OCR engine.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Jak extrahovat text z obrázku pomocí více obdélníků

### Krok 2: Rozpoznat obrázek s více obdélníky

#### 2.1 Definujte obdélníky

Vytvořte seznam objektů `Rectangle`, které vymezují oblasti, které chcete, aby OCR engine skenoval.

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 Proveďte OCR rozpoznání

Předávejte cestu k obrázku a seznam obdélníků metodě `RecognizeImage`. Metoda vrací kolekci řetězců – každý záznam odpovídá jednomu obdélníku.

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### Krok 3: Rozpoznat obrázek s nastavením rozpoznávání (alternativní přístup)

Pokud dáváte přednost použití `RecognitionSettings`, můžete dosáhnout stejného výsledku s mírně odlišným voláním API.

#### 3.1 Definujte nastavení rozpoznávání

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 Zobrazte rozpoznaný text

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Časté problémy a tipy

- **Nesprávné souřadnice obdélníku:** Ujistěte se, že hodnoty `X`, `Y`, `Width` a `Height` správně odpovídají požadované oblasti.  
- **Kvalita obrázku:** Obrázky s nízkým rozlišením mohou dávat špatné výsledky OCR; zvažte předzpracování (např. binarizaci).  
- **Prázdné výsledky:** Ověřte, že obdélníky skutečně obsahují text; jinak engine vrátí prázdné řetězce.

## Závěr

Nyní jste se naučili, jak **extrahovat text z obrázku** přípravou vlastních obdélníků pomocí Aspose.OCR pro .NET. Tato technika vám poskytuje detailní kontrolu nad OCR zpracováním, což vám pomůže vytvářet rychlejší a přesnější funkce pro extrakci textu ve vašich aplikacích.

## Často kladené otázky

**Q:** Mohu použít Aspose.OCR pro .NET s jinými .NET frameworky?  
**A:** Ano, Aspose.OCR pro .NET je kompatibilní s různými .NET frameworky.

**Q:** Je k dispozici bezplatná zkušební verze pro Aspose.OCR pro .NET?  
**A:** Rozhodně! K bezplatné zkušební verzi můžete přistupovat **[zde](https://releases.aspose.com/)**.

**Q:** Jak získám podporu pro Aspose.OCR pro .NET?  
**A:** Navštivte **[Aspose.OCR fórum](https://forum.aspose.com/c/ocr/16)** pro specializovanou podporu.

**Q:** Mohu získat dočasnou licenci pro testovací účely?  
**A:** Ano, dočasnou licenci můžete získat **[zde](https://purchase.aspose.com/temporary-license/)**.

**Q:** Kde najdu dokumentaci pro Aspose.OCR pro .NET?  
**A:** Dokumentace je k dispozici **[zde](https://reference.aspose.com/ocr/net/)**.

---

**Poslední aktualizace:** 2025-12-22  
**Testováno s:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}