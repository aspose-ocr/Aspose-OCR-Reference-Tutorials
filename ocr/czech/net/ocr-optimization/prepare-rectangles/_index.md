---
date: 2026-07-23
description: Naučte se, jak extrahovat text z obrázku pomocí Aspose.OCR pro .NET,
  připravit obdélníky pro zlepšení přesnosti OCR a efektivně převést obrázek na text.
keywords:
- extract text from image
- convert image to text
- improve ocr accuracy
lastmod: 2026-07-23
linktitle: Připravte obdélníky v rozpoznávání obrázků OCR
og_description: Extrahujte text z obrázku pomocí Aspose.OCR pro .NET. Naučte se připravovat
  obdélníky, zvýšit přesnost OCR a efektivně převést obrázek na text.
og_image_alt: Guide to extract text from image using rectangles with Aspose.OCR for
  .NET
og_title: Extrahování textu z obrázku pomocí obdélníků – Průvodce OCR
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how to extract text from image using Aspose.OCR for .NET, preparing
    rectangles to improve OCR accuracy and convert image to text efficiently.
  headline: Extract Text from Image with Rectangles – OCR Guide
  type: TechArticle
- questions:
  - answer: It converts visual characters in a picture into machine‑readable strings.
    question: What does “extract text from image” mean?
  - answer: Aspose.OCR for .NET provides a full‑featured OCR engine.
    question: Which library handles this in .NET?
  - answer: A free trial works for development; a commercial license is required for
      deployment.
    question: Do I need a license for production?
  - answer: Yes—define rectangles to target only the areas that contain useful text.
    question: Can I limit OCR to specific zones?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: What .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr
- Aspire.OCR
- .NET image processing
- extract text from image
title: Extrahování textu z obrázku pomocí obdélníků – Průvodce OCR
url: /cs/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z obrázku pomocí obdélníků – Průvodce OCR

## Úvod

Optické rozpoznávání znaků (OCR) vám umožňuje **extrahovat text z obrázku** souborů, aby se staly prohledávatelné a editovatelné. V tomto tutoriálu vám ukážeme, jak zvýšit přesnost OCR přípravou vlastních obdélníků, které zaměří engine na přesně požadované zóny. Pomocí Aspose.OCR pro .NET uvidíte celý pracovní postup – od nastavení projektu po získání rozpoznaných řetězců – takže můžete vložit spolehlivou konverzi obrázku na text do jakékoli .NET aplikace.

## Rychlé odpovědi
- **Co znamená „extrahovat text z obrázku“?** Převádí vizuální znaky na obrázku do strojově čitelných řetězců.  
- **Která knihovna to v .NET řeší?** Aspose.OCR pro .NET poskytuje plnohodnotný OCR engine.  
- **Potřebuji licenci pro produkci?** Bezplatná zkušební verze funguje pro vývoj; pro nasazení je vyžadována komerční licence.  
- **Mohu omezit OCR na konkrétní zóny?** Ano – definujte obdélníky, které cílí jen na oblasti obsahující užitečný text.  
- **Jaké verze .NET jsou podporovány?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Co je „extrahování textu z obrázku“ s obdélníky?

Proces `extract text from image` čte znaky uvnitř definovaných obdélníkových zón a ignoruje vše ostatní. Omezením OCR na tyto zóny získáte vyšší přesnost, rychlejší zpracování a menší úsilí při následném zpracování. Tento přístup izoluje text, který vás zajímá, a odstraňuje pozadí, dekorativní prvky a další vizuální šum, který může OCR engine zmást.

## Proč připravit obdélníky před OCR?

Příprava obdélníků vám umožní soustředit OCR engine na nejrelevantnější části obrázku, což zlepšuje jak rychlost, tak přesnost. Zúžením oblasti analýzy snižujete množství dat, která engine musí prozkoumat, což vede k rychlejším výsledkům a méně chybám způsobeným nadbytečným vizuálním nepořádkem.

- **Zaměřte se na relevantní obsah:** Přeskočte záhlaví, patičky nebo dekorativní grafiku, která by engine zmátla.  
- **Zvýšení výkonu:** Menší oblasti vyžadují méně výpočtů, což zkracuje dobu běhu až o 40 % u velkých skenů.  
- **Zlepšení přesnosti:** Snížení vizuálního šumu zvyšuje míru rozpoznání znaků z ~85 % na >95 % u špinavých dokumentů.

## Proč je to důležité pro reálné projekty

Mnoho obchodních dokumentů – účtenky, faktury, ID karty – kombinuje text s logy nebo čárovými kódy. Nakreslením obdélníků kolem polí, která skutečně potřebujete, extrahujete jen cenná data, čímž snížíte následnou čistící práci a zvýšíte spolehlivost automatizovaných pracovních postupů. Toto cílené extrahování snižuje úsilí při následném zpracování a pomáhá udržovat soulad se standardy pro zacházení s daty.

## Běžné případy použití

- **Automatizace zadávání dat:** Vytažení konkrétních polí ze skenovaných formulářů nebo výdajových účtenek.  
- **Kontroly souladu:** Izolovat právní klauzule nebo regulatorní prohlášení pro ověření.  
- **Indexování obsahu:** Indexovat jen nadpis nebo popisek obrázku pro viditelnost ve vyhledávačích.

## Požadavky

- Základní znalost C# a vývoje v .NET.  
- Knihovna Aspose.OCR pro .NET nainstalována – stáhněte ji **[zde](https://releases.aspose.com/ocr/net/)** nebo prohlédněte všechny verze **[zde](https://releases.aspose.com/)**.  
- Ukázkový obrázek (např. `sample.png`), který obsahuje text, který chcete extrahovat.

## Importovat jmenné prostory

`using` příkazy přinášejí OCR engine a třídy geometrie do rozsahu.

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Krok 1: Nastavte adresář dokumentů

Zadejte složku, která obsahuje vaše obrázky, a vytvořte instanci OCR engine.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Jak extrahovat text z obrázku pomocí více obdélníků

Načtěte obrázek jednou a poté předávejte seznam obdélníků OCR engine. Každý obdélník definuje oblast zájmu a engine vrátí samostatný řetězec pro každou oblast, což vám umožní zpracovávat pole jednotlivě a podle potřeby kombinovat výsledky.

### Definujte obdélníky

Objekty `Rectangle` popisují souřadnice X‑Y a velikost každé zóny, kterou chcete skenovat.  

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### Proveďte OCR rozpoznání

Metoda `RecognizeImage` zpracuje obrázek pomocí poskytnutého seznamu obdélníků a vrátí rozpoznaný text pro každou oblast.  

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## Jak extrahovat text z obrázku pomocí RecognitionSettings (alternativní přístup)

Pokud dáváte přednost volání založenému na nastaveních, můžete dosáhnout stejného výsledku pomocí `RecognitionSettings`. Tento objekt vám umožní seskupit definice obdélníků spolu s jazykem, DPI a dalšími OCR možnostmi, což poskytuje čisté volání API s jedním parametrem.

### Definujte nastavení rozpoznávání

`RecognitionSettings` vám umožní seskupit seznam obdélníků a další možnosti (např. jazyk, DPI) do jednoho objektu.  

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### Zobrazte rozpoznaný text

Iterujte přes vrácené řetězce a vypište text každé oblasti.  

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Běžné problémy a tipy

- **Nesprávné souřadnice obdélníku:** Ověřte, že `X`, `Y`, `Width` a `Height` odpovídají zamýšlené oblasti.  
- **Kvalita obrázku:** Nízké rozlišení nebo silně komprimované obrázky zhoršují výsledky OCR; zvažte předzpracování, např. binarizaci.  
- **Prázdné výsledky:** Ujistěte se, že obdélníky skutečně obsahují čitelný text; jinak engine vrátí prázdné řetězce.

## Řešení problémů a osvědčené postupy

| Příznak | Pravděpodobná příčina | Řešení |
|---------|-----------------------|--------|
| Žádný výstup nebo prázdné řetězce | Obdélníky mimo hranice obrázku | Zkontrolujte rozměry obrázku a souřadnice obdélníků |
| Zkreslené znaky | Špatný kontrast nebo šum | Použijte převod na odstíny šedi a prahování před OCR |
| Pomalý výkon u velkých souborů | Příliš mnoho obdélníků nebo velmi velký obrázek | Rozdělte obrázek nebo kde je to možné snižte počet obdélníků |

## Závěr

Nyní víte, jak **extrahovat text z obrázku** přípravou vlastních obdélníků s Aspose.OCR pro .NET. Tento přístup vám poskytuje přesnou kontrolu nad OCR zpracováním, což přináší rychlejší a přesnější funkce extrakce textu pro jakékoli .NET řešení.

## Často kladené otázky

**Q:** Mohu použít Aspose.OCR pro .NET s jinými .NET frameworky?  
**A:** Ano, Aspose.OCR pro .NET funguje s .NET Framework 4.5+, .NET Core 3.1+ a .NET 5/6/7.

**Q:** Je k dispozici bezplatná zkušební verze?  
**A:** Rozhodně! Stáhněte si zkušební verzi **[zde](https://releases.aspose.com/)**.

**Q:** Kde mohu získat podporu pro Aspose.OCR pro .NET?  
**A:** Navštivte **[forum Aspose.OCR](https://forum.aspose.com/c/ocr/16)** pro specializovanou pomoc.

**Q:** Mohu získat dočasnou licenci pro testování?  
**A:** Ano, dočasná licence je k dispozici **[zde](https://purchase.aspose.com/temporary-license/)**.

**Q:** Kde je oficiální dokumentace?  
**A:** Kompletní reference API je umístěna **[zde](https://reference.aspose.com/ocr/net/)**.

---

**Poslední aktualizace:** 2026-07-23  
**Testováno s:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Související tutoriály

- [Jak extrahovat obdélníky pro odstavce v OCR rozpoznávání obrázků](/ocr/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/)
- [Jak OCR obrázek – provést OCR na obrázku v OCR rozpoznávání obrázků](/ocr/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Jak extrahovat text z obrázku pomocí Aspose.OCR pro .NET](/ocr/net/text-recognition/get-recognition-result/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}