---
description: Naučte se, jak pomocí Aspose.OCR pro .NET specifikovat povolené znaky
  a efektivně rozpoznávat obrázky s číslicemi. Postupujte podle krok‑za‑krokem průvodce,
  který omezuje OCR pouze na číslice.
linktitle: Specify Allowed Characters OCR – Using Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: Specifikujte povolené znaky OCR – Použití Aspose.OCR pro .NET
url: /cs/net/ocr-settings/specify-allowed-characters/
weight: 13
---

 produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Specifikace povolených znaků OCR – Použití Aspose.OCR pro .NET

V tomto tutoriálu se naučíte, jak **specify allowed characters ocr** s Aspose.OCR pro .NET, což vám umožní omezit výstup OCR pouze na požadované znaky. To je obzvláště užitečné, když potřebujete **recognize digits image** soubory, jako jsou sériová čísla, ID faktur nebo řetězce podobné čárovým kódům. Provedeme vás nastavením, kódem a několika praktickými scénáři, abyste techniku mohli okamžitě použít.

## Rychlé odpovědi
- **Co dělá “specify allowed characters ocr”?** Omezuje OCR na předdefinovanou sadu znaků, čímž zvyšuje přesnost pro cílená data.  
- **Které znaky mohu povolit?** Jakákoli kombinace, kterou potřebujete – číslice, písmena nebo vlastní symboly (např. “0123456789”).  
- **Proč omezovat znaky?** Snižuje chybné rozpoznání a urychluje zpracování, pokud je znám očekávaný soubor znaků.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro vývoj; pro produkci je vyžadována komerční licence.  
- **Které verze .NET jsou podporovány?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Co je “specify allowed characters ocr”?
Když OCR skenuje obrázek, snaží se přiřadit každý vizuální vzor k úplné abecedě možných znaků. Pomocí **specify allowed characters ocr** řeknete enginu, aby ignoroval vše mimo váš whitelist, což dramaticky zvyšuje přesnost rozpoznání pro omezené datové sady.

## Proč použít Aspose.OCR pro rozpoznání obrázku s číslicemi?
Aspose.OCR poskytuje čisté, plynulé API pro vývojáře .NET. Jeho vestavěná možnost `AllowedCharacters` vám umožní zaměřit se na scénáře pouze s číslicemi, aniž byste museli psát vlastní logiku po‑zpracování. To je ideální pro:
- Čtení odečtů měřičů, čísel faktur nebo kódů produktů.  
- Ověřování uživatelem zadaných dat zachycených ze skenovaných formulářů.  
- Zrychlení dávkového zpracování, kde je sada znaků známa předem.

## Požadavky

Než se ponoříte do kódu, ujistěte se, že máte:

- Praktické znalosti vývoje v .NET.  
- Knihovnu **Aspose.OCR for .NET**. Můžete si ji stáhnout [zde](https://releases.aspose.com/ocr/net/).  
- Visual Studio (nebo jakékoli jiné preferované .NET IDE).

## Importování jmenných prostorů

Ve svém .NET projektu importujte potřebné jmenné prostory pro využití funkcí Aspose.OCR:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Nyní rozdělíme tutoriál do série podrobných kroků:

## Jak specifikovat povolené znaky OCR – Průvodce krok za krokem

### Krok 1: Nastavte cestu ke složce s obrázky

Nejprve definujte, kde jsou uloženy vaše ukázkové obrázky.

```csharp
string dataDir = "Your Document Directory";
```

### Krok 2: Inicializujte Aspose.OCR s whitelistem pouze pro číslice

Vytvořte instanci `AsposeOcr` a předáte znaky, které chcete povolit – v tomto případě všechny číslice.

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

### Krok 3: Rozpoznat jediný řádek obsahující číslice

Použijte metodu `RecognizeLine` k extrakci textu z obrázku, který obsahuje pouze čísla.

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

### Krok 4: Výstup rozpoznaných číslic

Vytiskněte výsledek do konzole, abyste mohli ověřit výstup.

```csharp
Console.WriteLine(result);
```

### Krok 5: Použijte RecognitionSettings pro větší kontrolu

Pokud potřebujete jemnější kontrolu – například vynutit rozpoznání jedné řádky – můžete použít přetížení, které přijímá `RecognitionSettings`.

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

### Krok 6: Zobrazte výsledek druhého případu

```csharp
Console.WriteLine(result2.RecognitionText);
```

### Krok 7: Potvrďte úspěšné provedení

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Po provedení těchto kroků jste se naučili, jak **specify allowed characters ocr** a efektivně **recognize digits image** obsah pomocí Aspose.OCR pro .NET.

## Časté problémy a řešení
- **Prázdný výsledek:** Ujistěte se, že kvalita obrázku je dostatečná (jasný kontrast, minimální šum).  
- **Vráceny špatné znaky:** Zkontrolujte, že řetězec whitelistu přesně odpovídá očekávaným znakům.  
- **Soubor nenalezen:** Ověřte, že `dataDir` ukazuje na správnou složku a že název souboru odpovídá velikosti písmen.

## Často kladené otázky

### Q1: Je Aspose.OCR pro .NET vhodný jak pro začátečníky, tak pro zkušené vývojáře?  
**A:** Rozhodně! API je navrženo tak, aby bylo intuitivní pro nováčky, a zároveň nabízí pokročilé možnosti pro zkušené uživatele.

### Q2: Mohu použít Aspose.OCR pro .NET k rozpoznání znaků v několika jazycích?  
**A:** Ano, Aspose.OCR podporuje širokou škálu jazyků. Můžete kombinovat jazykové balíčky s funkcí allowed‑characters pro vícejazyčné scénáře.

### Q3: Jak často je Aspose.OCR pro .NET aktualizován?  
**A:** Aktualizace jsou vydávány pravidelně, aby přidaly nové funkce, zlepšily přesnost a zajistily kompatibilitu. Podívejte se na [dokumentaci](https://reference.aspose.com/ocr/net/) pro podrobnosti o nejnovější verzi.

### Q4: Je k dispozici bezplatná zkušební verze Aspose.OCR pro .NET?  
**A:** Ano, můžete prozkoumat funkce stažením [bezplatné zkušební verze](https://releases.aspose.com/).

### Q5: Kde mohu získat pomoc nebo se spojit s komunitou pro podporu?  
**A:** Navštivte [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16), kde můžete klást otázky, sdílet zkušenosti a získat pomoc od inženýrů Aspose i ostatních vývojářů.

**Poslední aktualizace:** 2026-02-15  
**Testováno s:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}