---
description: Naučte se, jak uložit výsledky OCR pomocí Aspose.OCR pro .NET – převést
  obrázek na PDF, extrahovat text z PNG a uložit rozpoznaný text do DOCX, TXT, PDF
  nebo XLSX.
linktitle: How to Save OCR Result as Document
second_title: Aspose.OCR .NET API
title: Jak uložit výsledek OCR jako dokument
url: /cs/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uložit výsledek OCR jako dokument

## Úvod

V tomto tutoriálu objevíte **jak uložit OCR** výstup pomocí Aspose.OCR pro .NET. Provedeme vás rozpoznáváním textu na obrázku a následným převodem tohoto textu do populárních formátů dokumentů, jako jsou DOCX, TXT, PDF a XLSX. Na konci budete schopni automatizovat extrakci dat z obrázků a uložit je jako prohledávatelné, editovatelné soubory—ideální pro archivaci, reportování nebo následné zpracování.

## Rychlé odpovědi
- **Co znamená „jak uložit ocr“?** Odkazuje na ukládání textu rozpoznaného z obrázku do formátu souboru, jako je DOCX, PDF atd.  
- **Do jakých formátů mohu exportovat?** DOCX, TXT, PDF a XLSX jsou podporovány přímo.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro hodnocení; pro produkční použití je vyžadována komerční licence.  
- **Mohu přímo převést obrázek na PDF?** Ano—uložte výsledek OCR jako PDF a získáte prohledávatelný PDF dokument.  
- **Je podporován PNG?** Rozhodně; můžete **extrahovat text z PNG** obrázků pomocí stejného API.

## Co je OCR a proč ukládat výsledky jako dokumenty?

Optické rozpoznávání znaků (OCR) převádí tištěný nebo ručně psaný text v obrázcích na strojově čitelné řetězce. Ukládání těchto řetězců jako dokumentů vám umožní:

* Vytvořit prohledávatelné PDF pro soulad s předpisy.  
* Naplnit tabulky (XLSX) pro analýzu dat.  
* Generovat editovatelné zprávy (DOCX).  
* Archivovat prosté textové záznamy (TXT) pro rychlé vyhledávání.

## Požadavky

Předtím, než začneme, ujistěte se, že máte:

- Aspose.OCR pro .NET nainstalovaný. Můžete jej stáhnout **[zde](https://releases.aspose.com/ocr/net/)**.  
- Složku ve vašem počítači, která bude obsahovat zdrojové obrázky a výstupní dokumenty. Aktualizujte proměnnou `dataDir` v kódu, aby ukazovala na tuto složku.

## Importovat jmenné prostory

Potřebujeme několik .NET jmenných prostorů pro přístup k souborovému I/O a třídám Aspose OCR.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### Krok 1: Inicializovat Aspose.OCR

Nastavte cestu k vašemu pracovnímu adresáři a vytvořte instanci OCR enginu.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Krok 2: Rozpoznat obrázek

Předávejte soubor obrázku (např. PNG) rozpoznávači. Zde **rozpoznáváme textové obrázky** a převádíme je na `RecognitionResult`.

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### Krok 3: Uložit výsledek v různých formátech

Nyní exportujeme rozpoznaný text. Vyberte formát, který vyhovuje vašemu workflow—ať už potřebujete **převést obrázek na PDF**, **extrahovat text z PNG**, nebo vytvořit tabulku.

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### Krok 4: Zobrazit zprávu o úspěchu

Jednoduchá zpráva v konzoli potvrzuje, že proces byl dokončen bez chyb.

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

## Časté úskalí a tipy

- **Cesty k souborům:** Vždy používejte absolutní cesty nebo zajistěte, aby `dataDir` končil oddělovačem cesty (`\` nebo `/`).  
- **Kvalita obrázku:** Vyšší rozlišení obrázků zvyšuje přesnost; zvažte předzpracování (odklon, odstranění šumu) pro lepší výsledky.  
- **Režim licence:** V evaluačním režimu může výstup obsahovat vodoznak; použijte platnou licenci k jeho odstranění.

## Často kladené otázky

**Q1. Je Aspose.OCR kompatibilní s různými formáty obrázků?**  
A1: Ano, Aspose.OCR podporuje širokou škálu formátů obrázků, což zajišťuje flexibilitu ve vašich OCR úlohách.

**Q2: Mohu přizpůsobit nastavení rozpoznávání pro vyšší přesnost?**  
A2: Rozhodně! Aspose.OCR poskytuje `RecognitionSettings` pro jemné doladění OCR procesu podle vašich specifických požadavků.

**Q3: Je k dispozici bezplatná zkušební verze?**  
A3: Ano, můžete začít s bezplatnou zkušební verzí **[zde](https://releases.aspose.com/)**.

**Q4: Jak mohu získat dočasnou licenci pro Aspose.OCR?**  
A4: Dočasné licence lze získat **[zde](https://purchase.aspose.com/temporary-license/)**.

**Q5: Kde mohu získat pomoc nebo se spojit s komunitou?**  
A5: Připojte se ke komunitě Aspose.OCR na **[Aspose Forum](https://forum.aspose.com/c/ocr/16)** pro podporu a diskuze.

**Poslední aktualizace:** 2026-02-12  
**Testováno s:** Aspose.OCR 24.11 pro .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}