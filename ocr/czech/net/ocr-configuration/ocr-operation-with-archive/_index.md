---
date: 2026-04-12
description: Naučte se, jak extrahovat text ze zip souborů prováděním OCR na obrázcích
  archivů s Aspose.OCR pro .NET, včetně nastavení, kódu a řešení problémů.
keywords:
- extract text from zip
- read images from zip
- Aspose OCR .NET
linktitle: Jak extrahovat text ze ZIP archivů pomocí Aspose.OCR pro .NET
second_title: Aspose.OCR .NET API
title: Jak extrahovat text ze ZIP archivů pomocí Aspose.OCR pro .NET
url: /cs/net/ocr-configuration/ocr-operation-with-archive/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak extrahovat text ze ZIP archivů pomocí Aspose.OCR pro .NET

## Úvod

V tomto komplexním tutoriálu se naučíte **jak extrahovat text ze zip** archivů aplikací OCR na každý obrázek uvnitř archivu. Ať už potřebujete **převést obrázky na text**, **číst obrázky ze zip**, nebo vytvořit prohledávatelný úložiště dokumentů, podrobný návod níže vás provede vším — od instalace Aspose.OCR pro .NET až po výpis rozpoznaného textu pro každý obrázek v ZIP souboru.

## Rychlé odpovědi
- **Co tento tutoriál pokrývá?** Extrahování textu ze ZIP archivů pomocí Aspose.OCR pro .NET.  
- **Jaké primární klíčové slovo je cílem?** *extract text from zip*.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro hodnocení; pro produkční nasazení je vyžadována komerční licence.  
- **Jaké verze .NET jsou podporovány?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Mohu přizpůsobit nastavení rozpoznávání?** Ano — použijte `RecognitionSettings` k vyladění přesnosti pro různé jazyky nebo kvalitu obrázků.

## Co je OCR a proč jej použít na ZIP archivy?

Optické rozpoznávání znaků (OCR) převádí naskenované obrázky nebo PDF do prohledávatelného, editovatelného textu. Když jsou tyto obrázky zabaleny uvnitř ZIP souboru, jejich extrahování a rozpoznání každého obrázku najednou šetří čas a snižuje složitost kódu. Metoda `RecognizeMultipleImages` z Aspose.OCR usnadňuje tento proces a umožňuje vám **číst obrázky ze zip** a okamžitě získat textový obsah.

## Požadavky

- Visual Studio 2019 nebo novější (nebo jakékoli IDE kompatibilní s .NET).  
- .NET Framework 4.5 + nebo .NET Core 3.1 + nainstalován.  
- Přístup k knihovně Aspose.OCR pro .NET (odkaz ke stažení níže).  
- Platná licence Aspose.OCR pro produkční použití (k dispozici zkušební verze).

## Importovat jmenné prostory

Ve svém .NET projektu importujte potřebné jmenné prostory pro přístup k funkcionalitě poskytované Aspose.OCR:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Stáhnout a nainstalovat Aspose.OCR pro .NET

Stáhněte si nejnovější balíček ze stránky vydání **[zde](https://releases.aspose.com/ocr/net/)** a postupujte podle standardních kroků instalace pomocí NuGet nebo ručně.

## Získat licenci

Získejte licenci na **[stránce nákupu](https://purchase.aspose.com/buy)** nebo vyzkoušejte **[bezplatnou zkušební verzi](https://releases.aspose.com/)**. Umístěte soubor licence do kořenového adresáře projektu a načtěte jej za běhu podle popisu v dokumentaci Aspose.

## Krok 1: Nastavit adresář dokumentů

Začněte inicializací cesty k vašemu adresáři dokumentů. Tento složka bude obsahovat ZIP archiv, který chcete zpracovat:

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";
// ExEnd:1
```

> **Tip:** Použijte `Path.Combine` pro zpracování cest napříč platformami.

## Krok 2: Inicializovat Aspose.OCR

Vytvořte instanci třídy Aspose.OCR pro zahájení OCR operací:

```csharp
// ExStart:3
AsposeOcr api = new AsposeOcr();
// ExEnd:3
```

## Krok 3: Specifikovat cestu k ZIP archivu

Definujte úplnou cestu k vašemu archivnímu souboru (ZIP soubor obsahující obrázky, které chcete číst):

```csharp
// ExStart:4
string fullPath = dataDir + "OCR.zip";
// ExEnd:4
```

## Krok 4: Rozpoznat obrázky uvnitř ZIP

Spusťte OCR rozpoznávání na zadaném archivu pomocí výchozích nebo vlastních nastavení. Tento volání automaticky extrahuje každý obrázek ze ZIP a provede na něm OCR:

```csharp
// ExStart:5
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
   //default or custom settings
});
// ExEnd:5
```

> Můžete upravit `RecognitionSettings` pro zlepšení přesnosti pro konkrétní jazyky, DPI nebo pro povolení rozpoznávání rukopisu.

## Krok 5: Vytisknout extrahovaný text

Projděte výsledky a vytiskněte rozpoznaný text pro každý obrázek uvnitř archivu. Zde skutečně **extrahujete text ze zip**:

```csharp
// ExStart:6
for (int i = 0; i < result.Length; i++)
{
	 Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
// ExEnd:6
```

Výstup zobrazuje index každého obrázku následovaný extrahovaným řetězcem, což efektivně **převádí obrázky na text** a **extrahuje text ze souborů archivu** v jedné operaci.

## Proč je tento přístup důležitý

- **Dávkové zpracování:** Zpracovává libovolný počet obrázků uvnitř ZIP bez ruční extrakce.  
- **Výkon:** Snižuje I/O režii čtením přímo z archivu.  
- **Škálovatelnost:** Funguje s velkými ZIP soubory a může být kombinováno s asynchronními vzory pro scénáře s vysokou propustností.  

## Časté problémy a řešení

| Problém | Příčina | Řešení |
|-------|-------|----------|
| Žádný text nevrácen | Kvalita obrázku je příliš nízká | Předzpracujte obrázky (např. binarizací) nebo upravte `RecognitionSettings.Dpi` |
| Výjimka při čtení ZIP | Neplatná cesta k archivu | Ověřte, že `fullPath` ukazuje na platný soubor `.zip` a že aplikace má oprávnění ke čtení |
| Licence nebyla použita | Soubor licence chybí nebo nebyl načten | Zavolejte `License license = new License(); license.SetLicense("Aspose.OCR.lic");` před vytvořením instance `AsposeOcr` |

## Často kladené otázky

**Q: Mohu používat Aspose.OCR pro .NET bez licence?**  
A: Ano, je k dispozici bezplatná zkušební verze pro hodnocení, ale pro produkční nasazení je vyžadována licencovaná verze.

**Q: Podporuje knihovna ZIP archivy chráněné heslem?**  
A: V současné době `RecognizeMultipleImages` funguje se standardními ZIP soubory. Pro šifrované archivy nejprve extrahujte obrázky pomocí knihovny třetí strany a poté předávejte pole obrázků OCR enginu.

**Q: Jak mohu zlepšit přesnost pro ručně psaný text?**  
A: Povolit příznak `RecognitionSettings.EnableHandwritingRecognition` a nastavit vyšší DPI (např. 300).

**Q: Existuje způsob, jak získat skóre důvěry pro každý rozpoznaný řádek?**  
A: Každý `RecognitionResult` obsahuje vlastnost `Confidence`, kterou můžete zaznamenat nebo použít k filtrování výsledků s nízkou důvěrou.

## Další zdroje

- **Aspose.OCR Forum:** Pro podporu komunity a pokročilé scénáře navštivte [Aspose.OCR fórum](https://forum.aspose.com/c/ocr/16).  
- **Dočasná licence:** Pokud potřebujete krátkodobé hodnocení, požádejte o [dočasnou licenci](https://purchase.aspose.com/temporary-license/).  
- **Oficiální dokumentace:** Zůstaňte v obraze o nejnovějších změnách API prohlížením [dokumentace](https://reference.aspose.com/ocr/net/).

---

**Poslední aktualizace:** 2026-04-12  
**Testováno s:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}