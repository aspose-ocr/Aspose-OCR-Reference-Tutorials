---
date: 2026-04-23
description: Zvyšte přesnost OCR pomocí Aspose OCR pro .NET, využitím kontroly pravopisu,
  podpory jazykových balíčků OCR a vlastních slovníků k zlepšení kvality OCR u skenovaných
  dokumentů.
keywords:
- improve ocr accuracy
- ocr language pack
- process scanned documents
- boost ocr quality
- ocr spell checking
linktitle: Zlepšete přesnost OCR pomocí kontroly pravopisu v obrázcích
second_title: Aspose.OCR .NET API
title: Zlepšete přesnost OCR pomocí kontroly pravopisu na obrázcích
url: /cs/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zlepšení přesnosti OCR pomocí pravopisné kontroly na obrázcích

Když pracujete s optickým rozpoznáváním znaků (OCR), konečným cílem je **zlepšit přesnost OCR**, aby extrahovaný text dokonale odpovídal původnímu obrázku. Špatně napsaná slova, šumivé pozadí a neobvyklá písma jsou běžnými viníky, které výsledek zhoršují. Spojením vestavěného pravopisného kontrolního enginu Aspose.OCR s jeho rozsáhlým jazykovým balíčkem OCR můžete dramaticky **zvýšit kvalitu OCR** pro jakýkoli naskenovaný dokument.

## Jak zlepšit přesnost OCR pomocí pravopisné kontroly

V této sekci projdeme kompletním pracovním postupem – od načtení obrázku po aplikaci pravopisné kontroly a nakonec vylepšení výstupu pomocí vlastního uživatelského slovníku. Uvidíte reálné ukázky před a po, dozvíte se, proč je to důležité při zpracování naskenovaných dokumentů, a objevíte tipy, jak co nejlépe využít funkci pravopisné kontroly v OCR.

## Rychlé odpovědi
- **Co dělá pravopisná kontrola pro OCR?** Automaticky detekuje špatně napsaná slova ve výstupu OCR a nahrazuje je nejpravděpodobnějšími správnými alternativami.  
- **Která knihovna tuto funkci poskytuje?** Aspose.OCR pro .NET obsahuje připravené API pro pravopisnou kontrolu.  
- **Potřebuji internetové připojení?** Ne, pravopisný kontrolní engine funguje zcela offline.  
- **Mohu přidat vlastní terminologii?** Ano, můžete poskytnout vlastní uživatelský slovník pro zpracování doménově specifických slov.  
- **Jaké jazyky jsou podporovány?** Podívejte se na sekci „aspose ocr language support“ pro podrobnosti.

## Co je pravopisná kontrola v OCR?

Pravopisná kontrola zkoumá surový text vrácený OCR enginem, identifikuje tokeny, které neodpovídají známým slovům ve vybraném jazykovém slovníku, a navrhuje nebo aplikuje opravy. Tento krok je nezbytný pro **zlepšení přesnosti OCR**, zejména při zpracování naskenovaných dokumentů, účtenek nebo formulářů, kde OCR může špatně interpretovat znaky.

## Proč použít jazykový balíček Aspose OCR?

Aspose.OCR je dodáván s rozsáhlými jazykovými balíčky a umožňuje vám připojit další slovníky. Využití **aspose ocr language support** znamená, že můžete zpracovávat vícejazyčné dokumenty bez psaní vlastních parserů a získáte přístup k jazykově specifickým pravidlům, která dále zlepšují kvalitu rozpoznávání.

## Předpoklady

Než se ponoříme do kouzla pravopisné kontroly, ujistěte se, že máte následující předpoklady připravené:

- Aspose.OCR for .NET Library: Stáhněte a nainstalujte knihovnu Aspose.OCR ze [stránky vydání](https://releases.aspose.com/ocr/net/).
- Document Directory: Ujistěte se, že máte určený adresář pro své dokumenty. Nahraďte `"Your Document Directory"` v ukázkách kódu skutečnou cestou.

## Importovat jmenné prostory

Začněme importováním potřebných jmenných prostorů ve vašem .NET projektu:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Krok 1: Inicializovat Aspose.OCR

Inicializujte instanci Aspose.OCR pro spuštění OCR procesu.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Krok 2: Rozpoznat obrázek

Dále rozpoznávejte text na obrázku pomocí Aspose.OCR. Zde je úryvek ukazující tento proces:

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Krok 3: Před korekcí

Získejte výsledek OCR před korekcí pro porovnání s opravenou verzí.

```csharp
// Get result
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Krok 4: Po korekci

Aplikujte pravopisnou kontrolu pro získání opraveného výsledku. Následující úryvek kódu ilustruje tento krok:

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Krok 5: Špatně napsaná slova a návrhy

Získejte seznam špatně napsaných slov spolu s navrhovanými opravami pomocí následujícího kódu:

```csharp
// Get list of misspelled words with suggestions
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
	Console.Write("Word:" + word.Word);
	Console.Write(" StartPosition:" + word.StartPosition);
	Console.WriteLine(" Length:" + word.Length);
	Console.WriteLine("SuggestedWords:");
	foreach (var suggest in word.SuggestedWords)
	{
		Console.Write(suggest.Word + " ");
	}
	Console.WriteLine();
}
```

## Krok 6: Opravit uživatelský text

Opravte konkrétní uživatelem poskytnutý text pomocí knihovny Aspose.OCR:

```csharp
// Correct user text
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Krok 7: Korekce s uživatelským slovníkem

Dále vylepšete korekci začleněním vlastního uživatelského slovníku:

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Tipy pro zvýšení kvality OCR

- **Vyberte správný OCR jazykový balíček**, který odpovídá zdrojovému dokumentu. Použití `Language.Eng` na francouzském dokumentu dramaticky sníží přesnost.  
- **Předzpracujte obrázky** (odklon, odstranění šumu, zvýšení kontrastu) před jejich předáním OCR enginu; čistší obrázky produkují méně chyb.  
- **Udržujte stručný uživatelský slovník** — jedno slovo na řádek — aby pravopisná kontrola mohla rychle najít vlastní termíny, aniž by zpomalovala velké dávky.  
- **Zpracovávejte stránky po dávkách** při práci s vícestránkovými PDF; to snižuje zatížení paměti a urychluje fázi pravopisné kontroly.

## Časté problémy a řešení

| Problém | Proč k tomu dochází | Jak opravit |
|-------|----------------|------------|
| Žádné návrhy nebyly vráceny | Jazykový balíček není načten nebo je text příliš krátký. | Ujistěte se, že `RecognitionSettings(Language.Eng)` odpovídá jazyku zdrojového obrázku a že výsledek OCR obsahuje dostatek znaků. |
| Vlastní slovník nebyl použit | Nesprávná cesta nebo formát souboru. | Ověřte, že `dictionary.txt` existuje na zadaném místě a používá jedno slovo na řádek. |
| Pravopisná kontrola zpomaluje velké dokumenty | Zpracování každého slova jednotlivě přidává režii. | Zpracovávejte stránky po dávkách nebo zvýšte alokaci paměti, pokud běžíte na .NET Core. |

## Často kladené otázky

### Q1: Mohu použít Aspose.OCR pro jazyky jiné než angličtinu?

A1: Ano, Aspose.OCR podporuje více jazyků. Podle toho upravte nastavení jazyka.

### Q2: Jak integrovat Aspose.OCR do mého .NET projektu?

A2: Podívejte se na [dokumentaci](https://reference.aspose.com/ocr/net/) pro podrobné kroky integrace.

### Q3: Je k dispozici zkušební verze Aspose.OCR?

A3: Ano, můžete si vyzkoušet funkce pomocí [bezplatné zkušební verze](https://releases.aspose.com/).

### Q4: Mohu nahrát vlastní slovník pro pravopisnou kontrolu?

A4: Rozhodně! Tutoriál ukazuje, jak vylepšit korekci pomocí uživatelem poskytnutého slovníku.

### Q5: Kde mohu získat podporu pro Aspose.OCR?

A5: Navštivte [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) pro komunitní podporu a rady.

---

**Poslední aktualizace:** 2026-04-23  
**Testováno s:** Aspose.OCR for .NET latest version  
**Autor:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}