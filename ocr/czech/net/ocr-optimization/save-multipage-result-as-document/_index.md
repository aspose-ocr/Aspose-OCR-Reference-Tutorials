---
date: 2026-04-23
description: Naučte se, jak převádět obrázky na PDF v C# pomocí Aspose.OCR, ukládat
  vícestránkové výsledky OCR jako dokumenty a extrahovat text z obrázků.
keywords:
- extract text from images
- batch image to pdf
- convert scanned images pdf
linktitle: Převod obrázků do PDF C# – Uložení vícestránkového výsledku OCR
second_title: Aspose.OCR .NET API
title: Extrahovat text z obrázků – převést obrázky do PDF v C#
url: /cs/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat text z obrázků – Převést obrázky na PDF C#

## Úvod

V tomto tutoriálu se dozvíte, jak **extrahovat text z obrázků** při **převodu obrázků na PDF C#** pomocí Aspose.OCR pro .NET a poté uložit více‑stránkový výsledek OCR jako dokument. Ať už potřebujete **dávkový převod obrázků do PDF** pro archivaci, **převod naskenovaných obrázků do PDF** pro soulad, nebo jen získat prohledávatelný text z fotografií, provedeme vás každým krokem s jasnými vysvětleními, praktickými tipy a doporučeními osvědčených postupů.

## Rychlé odpovědi
- **Co tento tutoriál pokrývá?** Převod více obrázků do PDF/Docx/Txt/Xlsx a extrahování textu z obrázků pomocí Aspose.OCR v C#.
- **Jaké výstupní formáty jsou podporovány?** Docx, Text, Pdf a Xlsx (můžete také přímo výstupovat PDF).
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro hodnocení; pro produkci je vyžadována trvalá licence.
- **Jaké verze .NET jsou kompatibilní?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
- **Mohu extrahovat text během převodu?** Ano—použijte výsledky OCR k získání textu před uložením.

## Co je „extrahování textu z obrázků“ a proč to kombinovat s převodem do PDF?

Extrahování textu z obrázků znamená použití OCR (Optical Character Recognition) k převodu vizuálních znaků na prohledávatelné, editovatelné řetězce. Když **převádíte obrázky na PDF C#**, vložíte tyto řetězce do PDF, takže se dokument stane prohledávatelný a indexovatelný—ideální pro digitální archivaci a těžbu dat.

## Proč použít Aspose.OCR pro tento úkol?

- **Vysoká přesnost** napříč desítkami jazyků.  
- **Podpora více stránek** – zpracování dávky obrázků v jednom volání (ideální pro scénáře **dávkového převodu obrázků do PDF**).  
- **Přímé ukládání** do populárních kancelářských formátů bez dalších konverzních kroků.  
- **Plná integrace s .NET** – bez nativních závislostí, funguje na Windows, Linuxu i v cloudových runtimech.

## Požadavky

1. Nainstalovaný Aspose.OCR pro .NET. Můžete jej stáhnout [zde](https://releases.aspose.com/ocr/net/).  
2. Získaná bezplatná zkušební verze nebo zakoupená licence – zkušební verzi získáte [zde](https://releases.aspose.com/) nebo ji zakupte [zde](https://purchase.aspose.com/buy).  
3. Prostudovali jste oficiální [dokumentaci](https://reference.aspose.com/ocr/net/), abyste se seznámili s rozhraním API.  
4. Připojili jste se ke komunitě na [fóru podpory](https://forum.aspose.com/c/ocr/16) pro pomoc s případnými překážkami.  

Nyní, když je vše připraveno, pojďme začít kódovat.

## Importovat jmenné prostory

Začněte přidáním požadovaných jmenných prostorů do vašeho C# souboru:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

Tyto importy vám poskytují přístup ke kolekcím, práci se soubory, LINQ a třídám Aspose OCR.

## Krok 1: Nastavte adresář dokumentů

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

Nahraďte `"Your Document Directory"` absolutní nebo relativní cestou, kde jsou vaše zdrojové obrázky a kam chcete uložit výstupní soubory.

## Krok 2: Inicializovat Aspose.OCR

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Vytvoření objektu `AsposeOcr` vám poskytuje přístup ke všem operacím OCR, včetně pracovního postupu **převodu obrázků na PDF C#**.

## Krok 3: Rozpoznat obrázky

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

Metoda `RecognizeMultipleImages` zpracuje každý soubor v seznamu a vrátí kolekci `RecognitionResult`. Můžete zadat libovolný počet obrázků, což je ideální pro scénáře **převodu naskenovaných obrázků do PDF**.

## Krok 4: Uložit výsledky v preferovaných formátech

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

Vyberte formát, který nejlépe vyhovuje vašemu následnému workflow:

- **Docx** – editovatelný dokument Word s prohledávatelným textem.  
- **Text** – extrakce prostého textu pro rychlou těžbu dat (**extrahovat text z obrázků**).  
- **Pdf** – klasický výstup PDF, ideální pro archivaci.  
- **Xlsx** – tabulková reprezentace pro tabulková data.

## Běžné případy použití

- **Digitální archivace:** Převést naskenované papírové smlouvy na prohledávatelné PDF.  
- **Automatizace zadávání dat:** Extrahovat text z účtenek nebo faktur a vložit jej do databáze.  
- **Dávkové zpracování:** Zpracovat tisíce obrázků v jedné úloze s minimálním kódem—ideální pro potřeby **dávkového převodu obrázků do PDF**.

## Řešení problémů a tipy

- **Velké sady obrázků:** Zpracovávejte obrázky v menších dávkách, abyste předešli špičkám paměti.  
- **Kvalita obrázku:** Zajistěte, aby obrázky měly alespoň 300 dpi pro optimální přesnost OCR.  
- **Chyby licence:** Ověřte, že je soubor licence správně načten před voláním metod OCR.  
- **Prázdné výsledky:** OCR engine vrátí prázdný `RecognitionResult` pro nečitelné stránky; zkontrolujte `result[i].Text` na null nebo prázdné řetězce a podle toho je ošetřete.

## Často kladené otázky

**Q: Mohu převést obrázky na PDF C# bez použití OCR?**  
A: Ano, můžete použít Aspose.PDF nebo jiné knihovny pro čistý převod obrázku na PDF, ale OCR přidává prohledávatelný text.

**Q: Jak mohu extrahovat text z obrázků v C# po převodu?**  
A: Seznam `result` vrácený metodou `RecognizeMultipleImages` obsahuje vlastnosti `Text`, které můžete zapsat do souboru `.txt` nebo zpracovat přímo.

**Q: Je možné nastavit vlastní okraje stránky nebo orientaci?**  
A: Při ukládání do PDF nebo Docx můžete upravit rozvržení dokumentu pomocí API Aspose.Words nebo Aspose.PDF před voláním `SaveMultipageDocument`.

**Q: Co se stane, pokud obrázek nelze přečíst?**  
A: OCR engine vrátí prázdný `RecognitionResult` pro tuto stránku; můžete zkontrolovat `result[i].Text` na null nebo prázdné řetězce a podle toho je ošetřit.

**Q: Podporuje API nasazení do cloudu?**  
A: Ano, knihovna funguje na jakémkoli .NET runtime, včetně Azure Functions a AWS Lambda, pokud runtime splňuje požadavky na verzi.

---

**Poslední aktualizace:** 2026-04-23  
**Testováno s:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}