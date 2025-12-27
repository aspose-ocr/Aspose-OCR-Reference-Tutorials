---
date: 2025-12-27
description: Prozkoumejte pokročilou podporu jazyků OCR a funkce s Aspose.OCR pro
  .NET. Efektivní, přesné a přátelské k vývojářům.
linktitle: OCR Language Support – Ignored Characters in Image Recognition
second_title: Aspose.OCR .NET API
title: Podpora jazyků OCR – Ignorované znaky při rozpoznávání obrazu
url: /cs/net/ocr-settings/specify-ignored-characters/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Podpora jazyků OCR: Určete ignorované znaky při rozpoznávání obrazu

## Úvod

Podpora jazyků OCR je základním kamenem moderní automatizace dokumentů, umožňující aplikacím číst text z obrázků v mnoha abecedách a symbolech. V tomto tutoriálu se naučíte, jak říci **Aspose.OCR for .NET**, aby při rozpoznávání ignoroval konkrétní znaky – nezbytný trik, když potřebujete čistší výstup nebo chcete filtrovat šum, jako jsou čísla stránek nebo dekorativní symboly. Na konci průvodce budete mít připravený kód, který funkci ukazuje od začátku do konce.

## Rychlé odpovědi
- **Co znamená „ignorované znaky“?** Znaky, které OCR engine přeskočí při vytváření výsledného řetězce.  
- **Proč to používat?** Zlepšuje přesnost, když jsou určité symboly pro vaši obchodní logiku irelevantní.  
- **Která metoda API to řeší?** `RecognitionSettings.IgnoredCharacters`.  
- **Mohu to kombinovat s jazykovými balíčky?** Ano – ignorované znaky fungují vedle jakéhokoli načteného jazyka.  
- **Je vyžadována licence?** Pro produkční použití je potřeba dočasná nebo plná licence.

## Požadavky

Než se ponoříte do bohaté funkčnosti poskytované Aspose.OCR for .NET, ujistěte se, že máte následující požadavky připravené:

1. Instalace Aspose.OCR  

   Ujistěte se, že jste úspěšně nainstalovali Aspose.OCR for .NET. Potřebné soubory najdete na [stránce ke stažení](https://releases.aspose.com/ocr/net/).

2. Nastavení adresáře dokumentů  

   Vytvořte vyhrazený adresář pro své dokumenty. To bude klíčové pro bezproblémové spouštění příkladů. Aktualizujte proměnnou `dataDir` v příkladech na cestu k vašemu adresáři dokumentů.

3. Dočasná licence (volitelné)  

   Pokud zkoušíte Aspose.OCR for .NET s dočasnou licencí, získejte ji [zde](https://purchase.aspose.com/temporary-license/).

## Importujte jmenné prostory

Pro zahájení práce s Aspose.OCR for .NET budete potřebovat importovat potřebné jmenné prostory. Přidejte následující řádky do svého kódu:

```csharp
using System.IO;

using Aspose.OCR;
using System;
```

## Proč specifikovat ignorované znaky?

V mnoha reálných scénářích – například při zpracování faktur, účtenek nebo vícejazykových formulářů – můžete narazit na opakující se znaky, které nejsou součástí smysluplných dat (např. pomlčky používané jako oddělovače, čísla stránek nebo dekorativní symboly). Pokud OCR engine řeknete, aby tyto znaky přeskočil, snížíte úsilí při následném zpracování a zlepšíte celkovou spolehlivost následné analytiky.

## Postupný průvodce

### Krok 1: Nastavte svůj adresář dokumentů

Začněte určením adresáře, kde jsou vaše dokumenty uloženy. Nahraďte `"Your Document Directory"` skutečnou cestou k vašim dokumentům.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

### Krok 2: Inicializujte Aspose.OCR

Vytvořte instanci OCR engine. Tento objekt bude zpracovávat všechny následné volání rozpoznávání.

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Krok 3: Rozpoznávejte obrázek s ignorovanými znaky

Předávejte soubor obrázku spolu s objektem `RecognitionSettings`, který uvádí znaky, které chcete ignorovat. V tomto příkladu ignorujeme znaky `a`, `b` a `1`.

```csharp
// Recognize image with specified ignored characters
RecognitionResult result = api.RecognizeImage(dataDir + "SpanishOCR.bmp", new RecognitionSettings
{
    IgnoredCharacters = "ab1"
});
```

### Krok 4: Zobrazte rozpoznaný text

Nakonec vypište vyčištěný text do konzole nebo do jiného výstupu podle vašeho výběru.

```csharp
// Display the recognized text
Console.WriteLine(result.RecognitionText);
```

## Časté problémy a tipy

- **Nesprávná cesta:** Ujistěte se, že `dataDir` končí oddělovačem cesty (`\` nebo `/`) vhodným pro váš OS.  
- **Není podporován jazyk:** OCR engine musí mít jazykový balíček pro zdrojový obrázek; jinak nebudou ignorované znaky aplikovány správně.  
- **Chyby licence:** Pokud vidíte výjimku licence, ověřte, že soubor dočasné licence je ve vašem projektu správně odkazován.

## Závěr

Aspose.OCR for .NET poskytuje vývojářům pokročilé OCR schopnosti, zjednodušuje proces převodu obrázků na editovatelný a prohledávatelný text. Pomocí tohoto krok‑za‑krokem průvodce jste se naučili, jak vyloučit nežádoucí znaky, čímž učiníte své OCR pipeline čistší a spolehlivější. Prozkoumejte [dokumentaci](https://reference.aspose.com/ocr/net/) pro podrobnější informace a zjistěte, jak může Aspose.OCR pozvednout vaše OCR projekty.

## Často kladené otázky

### Q1: Mohu použít Aspose.OCR for .NET v nekomerčních projektech?

A1: Ano, Aspose.OCR for .NET může být používán jak v komerčních, tak v nekomerčních projektech. Pro více informací se podívejte na [detaily licencování](https://purchase.aspose.com/buy).

### Q2: Je k dispozici bezplatná zkušební verze?

A2: Samozřejmě! Bezplatnou zkušební verzi můžete získat [zde](https://releases.aspose.com/), abyste si před závazkem prozkoumali funkce a výhody Aspose.OCR for .NET.

### Q3: Jak mohu získat podporu pro Aspose.OCR?

A3: Pro jakékoli dotazy nebo pomoc navštivte [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16), kde můžete kontaktovat komunitu a získat odborné rady.

### Q4: Jaké jazyky Aspose.OCR podporuje?

A4: Aspose.OCR podporuje širokou škálu jazyků, což z něj činí univerzální volbu pro OCR úlohy. Kompletní seznam najdete v dokumentaci.

### Q5: Mohu zakoupit dočasnou licenci pro Aspose.OCR?

A5: Ano, pokud potřebujete dočasnou licenci, můžete ji získat [zde](https://purchase.aspose.com/temporary-license/) pro krátkodobé použití.

---

**Poslední aktualizace:** 2025-12-27  
**Testováno s:** Aspose.OCR 23.12 for .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}