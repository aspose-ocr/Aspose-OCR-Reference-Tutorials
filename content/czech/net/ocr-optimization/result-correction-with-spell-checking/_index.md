---
title: Oprava výsledku s kontrolou pravopisu v rozpoznávání obrazu OCR
linktitle: Oprava výsledku s kontrolou pravopisu v rozpoznávání obrazu OCR
second_title: Aspose.OCR .NET API
description: Vylepšete přesnost OCR pomocí Aspose.OCR pro .NET. Opravte pravopis, přizpůsobte slovníky a dosáhněte bezproblémového rozpoznávání textu bez námahy.
type: docs
weight: 13
url: /cs/net/ocr-optimization/result-correction-with-spell-checking/
---
## Úvod

oblasti optického rozpoznávání znaků (OCR) je dosažení přesných výsledků zásadní pro extrakci smysluplných informací z obrázků. Jedním z běžných problémů je řešení chybně napsaných slov v procesu rozpoznávání. Naštěstí Aspose.OCR for .NET poskytuje výkonné řešení pro vylepšení výsledků OCR pomocí kontroly pravopisu.

Tento tutoriál vás provede procesem opravy výsledků s kontrolou pravopisu pomocí Aspose.OCR pro .NET. Nakonec budete vybaveni ke zlepšení přesnosti textu odvozeného z OCR a zajistíte tak jemnější a bezchybnější výstup.

## Předpoklady

Než se ponoříme do kouzla kontroly pravopisu, ujistěte se, že máte splněny následující předpoklady:

-  Aspose.OCR for .NET Library: Stáhněte si a nainstalujte knihovnu Aspose.OCR z[stránka vydání](https://releases.aspose.com/ocr/net/).

- Adresář dokumentů: Ujistěte se, že máte určený adresář pro vaše dokumenty. Nahraďte "Your Document Directory" ve fragmentech kódu skutečnou cestou.

## Importovat jmenné prostory

Začněme importem potřebných jmenných prostorů do vašeho projektu .NET:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Krok 1: Inicializujte Aspose.OCR

Inicializací instance Aspose.OCR nastartujete proces OCR.

```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";

// Inicializujte instanci AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Krok 2: Rozpoznejte obrázek

Dále rozpoznávejte text v obrázku pomocí Aspose.OCR. Zde je úryvek demonstrující tento proces:

```csharp
// Rozpoznat obrázek
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Krok 3: Před opravou

Před opravou načtěte výsledek OCR, abyste jej mohli porovnat s opravenou verzí.

```csharp
// Získejte výsledek
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Krok 4: Po opravě

Chcete-li získat opravený výsledek, použijte kontrolu pravopisu. Tento krok ilustruje následující fragment kódu:

```csharp
// Získejte opravený výsledek
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Krok 5: Nesprávně napsaná slova a návrhy

Získejte seznam chybně napsaných slov spolu s navrhovanými opravami pomocí následujícího kódu:

```csharp
// Získejte seznam chybně napsaných slov s návrhy
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

## Krok 6: Opravte uživatelský text

Opravte konkrétní text zadaný uživatelem pomocí knihovny Aspose.OCR:

```csharp
// Správný uživatelský text
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Krok 7: Oprava pomocí uživatelského slovníku

Dále vylepšete opravu začleněním vlastního uživatelského slovníku:

```csharp
// Získejte opravený výsledek pomocí uživatelského slovníku
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Závěr

Gratulujeme! Úspěšně jste prošli možnostmi kontroly pravopisu Aspose.OCR pro .NET. Tato funkce vám umožňuje zpřesnit výsledky OCR, zajistit přesnost a eliminovat chyby.

## FAQ

### Q1: Mohu použít Aspose.OCR pro jiné jazyky než angličtinu?

A1: Ano, Aspose.OCR podporuje více jazyků. Upravte odpovídajícím způsobem nastavení jazyka.

### Q2: Jak integruji Aspose.OCR do mého projektu .NET?

 A2: Viz[dokumentace](https://reference.aspose.com/ocr/net/) pro podrobné integrační kroky.

### Q3: Je k dispozici zkušební verze pro Aspose.OCR?

 A3: Ano, můžete prozkoumat funkce pomocí[zkušební verze zdarma](https://releases.aspose.com/).

### Q4: Mohu nahrát vlastní slovník pro kontrolu pravopisu?

A4: Rozhodně! Výukový program ukazuje, jak zlepšit opravu pomocí slovníku poskytnutého uživatelem.

### Q5: Kde mohu hledat podporu pro Aspose.OCR?

 A5: Navštivte[Fórum Aspose.OCR](https://forum.aspose.com/c/ocr/16) za podporu a vedení komunity.