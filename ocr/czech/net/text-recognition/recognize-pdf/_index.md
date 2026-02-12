---
date: 2026-01-02
description: Naučte se, jak provádět OCR PDF v .NET, extrahovat text z PDF, převádět
  PDF na text a číst text z PDF v C# pomocí Aspose.OCR. Podrobný návod krok za krokem
  s ukázkami kódu.
linktitle: How to OCR PDF in .NET with Aspose.OCR
second_title: Aspose.OCR .NET API
title: Jak provést OCR PDF v .NET pomocí Aspose.OCR
url: /cs/net/text-recognition/recognize-pdf/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést OCR PDF v .NET s Aspose.OCR

## Úvod

Pokud hledáte spolehlivý způsob **jak provést OCR PDF** soubory v prostředí .NET, jste na správném místě. V tomto tutoriálu projdeme celý proces extrakce textu z PDF, převodu PDF na text a čtení textu z PDF ve stylu C# pomocí knihovny Aspose.OCR. Ať už potřebujete zpracovat jednu stránku nebo **OCR více stránek PDF**, níže uvedené kroky vám poskytují solidní, připravené řešení pro produkci.

## Rychlé odpovědi
- **Jakou knihovnu mám použít?** Aspose.OCR pro .NET
- **Mohu extrahovat text z PDF s více stránkami?** Ano – nastavte `StartPage` a `PagesNumber` v `DocumentRecognitionSettings`.
- **Potřebuji licenci pro produkci?** Je vyžadována komerční licence; je k dispozici zkušební verze.
- **Které verze .NET jsou podporovány?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.
- **Je OCR nejlepší způsob, jak extrahovat text?** Pro naskenované PDF nebo obrázky v PDF je OCR nezbytné; pro nativní PDF může být rychlejší PDF parser.

## Co je OCR a proč jej používat pro PDF?

Optické rozpoznávání znaků (OCR) převádí obrázky textu — například naskenované stránky—na prohledávatelné, editovatelné znaky. Když PDF obsahuje naskenované stránky, tradiční extrakce textu selže, což z OCR techniku, která spolehlivě dělá **extrahuje text PDF** a **převádí PDF na text**.

## Proč zvolit Aspose.OCR pro .NET?

- **Vysoká přesnost** pro více jazyků a fontů.
- **Vestavěná podpora** pro PDF s více stránkami, umožňující specifikovat rozsah stránek ke zpracování.
- **Jednoduché API**, které se hladce integruje do C# projektů, poskytuje**čtení textu PDF v C#** nebo **extrakci textu PDF v C#**.

## Předpoklady

Než se ponoříme do kódu, vyberte se, že máte následující:

- Aspose.OCR pro .NET nainstalováno. Pokud ho ještě nemáte, stáhněte si jej z [Aspose.OCR for .NET dokumentace](https://reference.aspose.com/ocr/net/).
- PDF soubor, na kterém chcete spustit OCR. Poznamenejte si úplnou cestu k souboru ve vašem počítači.

Nyní, když máte vše připravené, pojďme začít kódovat.

## Import jmenných prostorů

Ve vaší aplikaci .NET importujte jmenný prostor Aspose.OCR, získáte přístup k funkcím OCR:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Krok 1: Inicializace Aspose.OCR

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Zde definujeme složku, která obsahuje naše PDF, a vytvoříme objekt `AsposeOcr`, který provede rozpoznání.

## Krok 2: Zadání cesty k PDF

```csharp
// Image Path
string fullPath = dataDir + "multi_page_1.pdf";
```

Nahraďte `multi_page_1.pdf` názvem PDF, které chcete zpracovat. Tato cesta je používána OCR enginem.

## Krok 3: Rozpoznání PDF (OCR vícestránkový PDF)

```csharp
// Recognize image
List<RecognitionResult> results = api.RecognizePdf(fullPath, new DocumentRecognitionSettings { StartPage = 2, PagesNumber = 2 });
```

Metoda `RecognizePdf` spouští OCR na zadaných stránkách. Upravte `StartPage` a `PagesNumber` pro cílení na libovolný rozsah, což je zvláště užitečné pro scénáře **OCR více stránek PDF**.

## Krok 4: Vytisknutí výsledků

```csharp
// Print result
int pageCounter = 0;
foreach (var result in results)
{
    PrintRecognitionResult(result, pageCounter++);
}
```

Smyčka iteruje přes `RecognitionResult` každé stránky a vypisuje extrahovaný text. Můžete nahradit `PrintRecognitionResult` vlastní logikou pro uložení textu do databáze nebo jeho zápis do souboru.

## Běžné případy použití

- **Automatizace zpracování faktur** – extrahujte položky z naskenovaných faktur.
- **Digitální archivace** – převádějte staré naskenované dokumenty na prohledávatelné PDF.
- **Data mining** – získejte text ze zpráv, které jsou dostupné jen jako naskenované PDF.

## Odstraňování problémů a tipy

- **Nízká přesnost?** hledá se, že PDF má vysoké rozlišení (300dpi nebo vyšší).
- **Problémy s pamětí u velkých PDF?** Zpracovávejte dokumenty v menších dávných stránkách.
- **Potřebujete zpracovat PDF chráněné heslem?** Načtěte soubor do streamu a předávejte heslo OCR API (viz dokumentace Aspose.OCR).

## Závěr

Gratulujeme! Naučili jste se **jak provést OCR PDF** soubory v .NET, extrahovali text a viděli, jak **převést PDF na text** pro jednostránkové i vícestránkové dokumenty. Tento přístup vám poskytuje flexibilitu integrovat OCR do jakékoli C# aplikace, ať už jde o webovou službu, desktopový nástroj nebo úlohu na pozadí.

## Často kladené otázky

**Q: Mohu extrahovat text z PDF chráněného heslem?**
A: Ano. Použijte přetížení `RecognizePdf`, které přijímá parametry hesla.

**O: Funguje OCR na ručně psaných PDF?**
A: Aspose.OCR dokáže spolehlivě rozpoznat tištěný text; ručně psaný text může vyžadovat další předzpracování nebo specializovaný engine.

**O: Jaký je dopad na výkon u velkých dokumentů?**
A: Doba zpracování roste s počtem stránek a rozlišením obrázku. Rozdělení dokumentu na menší dávky může zlepšit odezvu.

**Q: Jak uložit výsledky OCR do textového souboru?**
A: Uvnitř smyčky `foreach` zapište `result.Text` do `StreamWriter` pro každou stránku.

**Q: Existuje způsob, jak zachovat původní rozvržení PDF po OCR?**
A: Můžete si vytvořit nové prohledávatelné PDF překrytím OCR textu na původní stránky pomocí Aspose.PDF po extrakci.

**Poslední aktualizace:** 2026-01-02
**Testováno s:** Aspose.OCR 24.11 pro .NET
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}