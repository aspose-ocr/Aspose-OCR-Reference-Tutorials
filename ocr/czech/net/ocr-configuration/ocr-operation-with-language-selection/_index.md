---
date: 2025-12-21
description: Naučte se provádět OCR a extrahovat text z obrázku pomocí Aspose.OCR
  pro .NET. Tento krok‑za‑krokem průvodce ukazuje rozpoznávání vícejazyčného textu
  a výběr jazyka.
linktitle: How to Perform OCR with Language Selection in Aspose.OCR
second_title: Aspose.OCR .NET API
title: Jak provést OCR s výběrem jazyka v Aspose.OCR
url: /cs/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést OCR s výběrem jazyka v Aspose.OCR

## Úvod

Pokud potřebujete **jak provést OCR** na obrázcích a extrahovat text z obrazových souborů v .NET aplikaci, Aspose.OCR pro .NET poskytuje rychlé, přesné a jazykově uvědomělé řešení. V tomto tutoriálu projdeme reálný příklad, který demonstruje rozpoznávání obrázků pomocí OCR s výběrem jazyka, takže můžete získat vícejazyčný text z obrázků pomocí několika řádků kódu.

## Rychlé odpovědi
- **Co dělá Aspose.OCR?** Rozpoznává tištěný a ručně psaný text na obrázcích a vrací extrahovaný text.  
- **Mohu si vybrat jazyk?** Ano – můžete specifikovat libovolný podporovaný jazyk, jako je angličtina, němčina, španělština, čínština atd.  
- **Potřebuji licenci pro vývoj?** Bezplatná zkušební verze funguje pro hodnocení; licence je vyžadována pro produkční použití.  
- **Které verze .NET jsou podporovány?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Je korekce sklonu automatická?** Můžete povolit `AutoSkew` a jemně doladit nastavení `SkewAngle`.

## Proč zvolit Aspose.OCR pro úlohy OCR?

- **Vysoká přesnost** napříč různými fonty a kvalitou obrázků.  
- **Vestavěný výběr jazyka** eliminuje potřebu externích jazykových balíčků.  
- **Jednoduché API**, které se čistě integruje s existujícími C# projekty.  
- **Žádné externí závislosti** – vše běží lokálně, což udržuje vaše data v bezpečí.

## Předpoklady

Než se ponoříme do kódu, ujistěte se, že máte následující předpoklady připravené:

- Aspose.OCR pro .NET: Ujistěte se, že máte nainstalovanou knihovnu Aspose.OCR. Můžete si ji stáhnout ze [stránky ke stažení Aspose.OCR pro .NET](https://releases.aspose.com/ocr/net/).

- Vývojové prostředí: Nastavte si pracovní prostředí s .NET aplikací. Pokud jste to ještě neudělali, podívejte se na [dokumentaci](https://reference.aspose.com/ocr/net/) pro podrobné instrukce.

## Importujte jmenné prostory

Ve vaší .NET aplikaci začněte importováním potřebných jmenných prostorů:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Krok 1: Inicializace Aspose.OCR

Začněte inicializací instance třídy Aspose.OCR. Tím připravíte prostředí pro využití OCR funkcí ve vaší aplikaci.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Krok 2: Zadejte cestu k obrázku

Dále definujte cestu k obrázku, na kterém chcete provést OCR. Ujistěte se, že je obrázek přístupný z vaší aplikace.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## Krok 3: Rozpoznání obrázku s výběrem jazyka

Nyní přichází hlavní operace OCR. Využijte knihovnu Aspose.OCR k rozpoznání textu ze zadaného obrázku. Upravte nastavení rozpoznávání, včetně výběru jazyka.

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## Krok 4: Vytisknutí a zobrazení výsledků

Po operaci OCR vytiskněte a zobrazte výsledky, včetně rozpoznaného textu, oblastí, varování a JSON reprezentace.

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## Časté problémy a tipy

- **Nesprávný výběr jazyka** – Pokud výstup vypadá poškozeně, zkontrolujte, že vlastnost `Language` odpovídá jazyku zdrojového obrázku.  
- **Šikmé obrázky** – Povolte `AutoSkew` nebo ručně upravte `SkewAngle` pro lepší přesnost u nakloněných skenů.  
- **Velké soubory** – Zpracovávejte velké obrázky po částech nebo snižte rozlišení před předáním do `RecognizeImage`, abyste šetřili paměť.

## Závěr

Gratulujeme! Naučili jste se **jak provést OCR** s výběrem jazyka pomocí Aspose.OCR pro .NET. Tento tutoriál vám ukázal, jak extrahovat text z obrazových souborů, přizpůsobit nastavení rozpoznávání a snadno pracovat s vícejazyčným obsahem.

## Často kladené otázky

### Q1: Je Aspose.OCR vhodný pro rozpoznávání vícejazyčného textu?

Ano, Aspose.OCR podporuje různé jazyky, což poskytuje flexibilitu pro vícejazyčné úlohy OCR.

### Q2: Mohu jemně doladit nastavení OCR pro konkrétní charakteristiky obrázku?

Rozhodně! Upravte parametry jako úhel sklonu, rozpoznávání řádků a detekci oblastí, abyste optimalizovali OCR pro různé scénáře.

### Q3: Kde mohu najít další podporu nebo diskuse v komunitě?

Navštivte [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) pro podporu a diskuse s komunitou.

### Q4: Je k dispozici bezplatná zkušební verze?

Ano, prozkoumejte [free trial](https://releases.aspose.com/) a vyzkoušejte možnosti Aspose.OCR.

### Q5: Jak mohu zakoupit Aspose.OCR pro .NET?

Pro nákup navštivte [purchase page](https://purchase.aspose.com/buy).

**Poslední aktualizace:** 2025-12-21  
**Testováno s:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}