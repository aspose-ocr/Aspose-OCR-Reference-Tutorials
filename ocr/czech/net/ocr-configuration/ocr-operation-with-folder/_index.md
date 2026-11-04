---
date: 2026-02-25
description: Naučte se, jak pomocí Aspose.OCR pro .NET extrahovat text z obrázků a
  umožnit rozpoznávání OCR obrázků na úrovni složek.
linktitle: OCROperation with Folder in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Extrahovat text z obrázků pomocí OCR operace na složkách
url: /cs/net/ocr-configuration/ocr-operation-with-folder/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat text z obrázků pomocí OCR operace na složkách

## Úvod

Vítejte ve světě Optical Character Recognition (OCR) s **Aspose.OCR for .NET**! Pokud potřebujete **extrahovat text z obrázků** hromadně — například z celé složky naskenovaných dokumentů — tento tutoriál vás provede praktickým řešením. Pokryjeme vše od nastavení projektu až po výpis rozpoznaného textu, abyste mohli rychle integrovat OCR na úrovni složek do svých C# aplikací. Na konci také uvidíte, jak tento přístup umožňuje **převést obrázky na text**, **extrahovat text ze skenovaných dokumentů** a **číst text z obrázku v C#** pomocí několika řádků kódu.

## Rychlé odpovědi
- **Co tento tutoriál učí?** Jak extrahovat text z obrázků uložených ve složce pomocí Aspose.OCR.  
- **Jaký jazyk a platforma?** C# s .NET (Framework nebo .NET Core).  
- **Klíčový předpoklad?** Knihovna Aspose.OCR for .NET (odkaz ke stažení níže).  
- **Kolik řádků kódu?** Pouze sedm stručných bloků kódu.  
- **Mohu převést obrázky na text?** Ano — tento příklad přesně ukazuje, jak na to.

## Co znamená „extrahovat text z obrázků“?
Extrahování textu z obrázků znamená použití OCR technologie k přečtení znaků vložených do obrázků, PDF nebo naskenovaných dokumentů a jejich převod na editovatelné, prohledávatelné řetězce. Aspose.OCR poskytuje výkonný engine, který podporuje mnoho formátů obrázků a jazyků.

## Proč použít Aspose.OCR pro OCR na úrovni složek?
- **Vysoká přesnost** s vestavěnou detekcí jazyka.  
- **Dávkové zpracování** pomocí `RecognizeMultipleImages`, ideální pro složky.  
- **Jednoduché API**, které se přirozeně hodí do C# projektů.  
- **Škálovatelnost** – funguje jak na desktopu, tak na serverových prostředích.

## Běžné případy použití
- Digitalizace knihovny naskenovaných faktur nebo účtenek.  
- Převod archivovaných souborů PNG/JPEG na prohledávatelný text pro indexaci.  
- Automatizace zadávání dat čtením textu z obrázků štítků produktů.  
- Vytvoření funkce vyhledávání v dokumentech, která potřebuje **extrahovat text ze skenovaných dokumentů** za běhu.

## Požadavky

- Základní znalost C# a vývoje v .NET.  
- Visual Studio (libovolná recentní edice).  
- Knihovna **Aspose.OCR for .NET** – stáhněte ji [zde](https://releases.aspose.com/ocr/net/).  
- Pochopení konceptů OCR (volitelné, ale užitečné).

## Import Namespaces

Přidejte požadované `using` direktivy na začátek vašeho C# souboru, aby kompilátor věděl, kde najít OCR třídy.

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Průvodce krok za krokem

### Krok 1: Nastavení adresáře dokumentů
Definujte složku, která obsahuje obrázky, jež chcete zpracovat.

```csharp
// ExStart:1   
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

> **Tip:** Použijte absolutní cestu nebo `Path.Combine`, abyste se vyhnuli problémům s oddělovači cest na různých OS.

### Krok 2: Inicializace Aspose.OCR
Vytvořte instanci OCR enginu.

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Krok 3: Specifikace cesty k obrázkům
Ukazujte API na konkrétní podadresář, který obsahuje vaše soubory obrázků.

```csharp
// Image Path
string fullPath = dataDir + "OCR";
```

> **Proč je to důležité:** Metoda `RecognizeMultipleImages` očekává cestu ke složce, nikoli k jednotlivému souboru.

### Krok 4: Rozpoznání obrázků
Spusťte OCR na každém obrázku ve složce. Můžete přizpůsobit `RecognitionSettings`, pokud potřebujete jazykové nápovědy nebo specifické předzpracování.

```csharp
// Recognize image           
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
    //default or custom
});
```

### Krok 5: Výpis výsledků
Projděte vrácené pole `RecognitionResult` a vypište extrahovaný text.

```csharp
// Print result
for (int i = 0; i < result.Length; i++)
{
    Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
```

> **Častá chyba:** Zapomenutí zkontrolovat `result.Length` může způsobit `IndexOutOfRangeException`, když je složka prázdná. Vždy nejprve ověřte obsah složky.

### Krok 6: Zpráva o dokončení
Signalizujte úspěšné provedení.

```csharp
// ExEnd:1
Console.WriteLine("OCROperationWithFolder executed successfully");
```

## Tipy a osvědčené postupy

- **Velikost dávky:** Pokud zpracováváte tisíce souborů, zvažte rozdělení složky na menší dávky, aby byl paměťový výdej předvídatelný.  
- **Jazykové nápovědy:** Zadání správného jazykového kódu v `RecognitionSettings` výrazně zvyšuje přesnost, zejména u ne‑latinských skriptů.  
- **Asynchronní zpracování:** Zabalte volání OCR do `Task.Run` nebo použijte async/await, aby UI vlákna zůstala responzivní.  
- **Validace souborů:** Před voláním `RecognizeMultipleImages` filtrujte adresář na podporované přípony (`.png`, `.jpg`, `.jpeg`, `.tif`, `.tiff`).  

## Běžné problémy a řešení

| Problém | Příčina | Oprava |
|---------|----------|--------|
| Žádný výstup | Nesprávná nebo prázdná cesta ke složce | Ověřte, že `fullPath` ukazuje na správný adresář a obsahuje podporované formáty obrázků (PNG, JPEG, TIFF). |
| Zkreslené znaky | Nesprávné nastavení jazyka | Předávejte nakonfigurované `RecognitionSettings` s `Language` nastaveným na odpovídající ISO kód. |
| Výkonnostní zpoždění při mnoha obrázcích | Sekvenční zpracování na UI vlákně | Spusťte OCR na pozadí nebo použijte asynchronní vzory, aby UI zůstalo responzivní. |

## Často kladené otázky

**Q: Mohu použít Aspose.OCR for .NET v komerčních projektech?**  
A: Ano, Aspose.OCR for .NET je komerční produkt. Informace o licencování najdete [zde](https://purchase.aspose.com/buy).

**Q: Je k dispozici bezplatná zkušební verze?**  
A: Ano, bezplatnou zkušební verzi můžete vyzkoušet [zde](https://releases.aspose.com/).

**Q: Kde najdu dokumentaci?**  
A: Dokumentace je dostupná [zde](https://reference.aspose.com/ocr/net/).

**Q: Jak získat dočasnou licenci?**  
A: Dočasné licence lze získat [zde](https://purchase.aspose.com/temporary-license/).

**Q: Potřebuji podporu nebo mám otázky?**  
A: Navštivte [Aspose.OCR fórum](https://forum.aspose.com/c/ocr/16) pro komunitní podporu.

---

**Poslední aktualizace:** 2026-02-25  
**Testováno s:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}