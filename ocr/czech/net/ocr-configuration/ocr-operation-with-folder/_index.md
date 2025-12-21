---
date: 2025-12-21
description: Naučte se, jak extrahovat text z obrázků pomocí Aspose.OCR pro .NET,
  což umožňuje rozpoznávání OCR obrázků na základě složek.
linktitle: OCROperation with Folder in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Extrahovat text z obrázků pomocí OCR operace ve složkách
url: /cs/net/ocr-configuration/ocr-operation-with-folder/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat text z obrázků pomocí OCR operace na složkách

## Úvod

Vítejte ve světě optického rozpoznávání znaků (OCR) s **Aspose.OCR for .NET**! Pokud potřebujete **extrahovat text z obrázků** hromadně – například celou složku naskenovaných dokumentů – tento tutoriál vás provede praktickým řešením pro reálný svět. Pokryjeme vše od nastavení projektu až po výpis rozpoznaného textu, abyste mohli rychle integrovat OCR založené na složkách do svých C# aplikací.

## Rychlé odpovědi
- **Co tento tutoriál učí?** Jak extrahovat text z obrázků uložených ve složce pomocí Aspose.OCR.
- **Jaký jazyk a platforma?** C# s .NET (Framework nebo .NET Core).
- **Klíčová předpoklad?** Knihovna Aspose.OCR for .NET (odkaz ke stažení níže).
- **Kolik řádků kódu?** Pouze sedm stručných bloků kódu.
- **Mohu převést obrázky na text?** Ano – tento příklad to přesně ukazuje.

## Co je „extrahovat text z obrázků“?
Extrahování textu z obrázků znamená použití OCR technologie k přečtení znaků vložených do obrázků, PDF nebo naskenovaných dokumentů a jejich převod na editovatelné, prohledávatelné řetězce. Aspose.OCR poskytuje robustní engine, který podporuje mnoho formátů obrázků a jazyků.

## Proč použít Aspose.OCR pro OCR založené na složkách?
- **Vysoká přesnost** s vestavěnou detekcí jazyka.  
- **Dávkové zpracování** pomocí `RecognizeMultipleImages`, ideální pro složky.  
- **Jednoduché API**, které se přirozeně hodí do C# projektů.  
- **Škálovatelné** – funguje jak na desktopu, tak na serverových prostředích.

## Požadavky

- Základní znalost C# a vývoje v .NET.  
- Visual Studio (jakékoli recentní vydání).  
- Knihovna **Aspose.OCR for .NET** – stáhněte ji [zde](https://releases.aspose.com/ocr/net/).  
- Pochopení konceptů OCR (volitelné, ale užitečné).

## Importujte jmenné prostory

Přidejte požadované `using` direktivy na začátek vašeho C# souboru, aby kompilátor věděl, kde najít třídy OCR.

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Průvodce krok za krokem

### Krok 1: Nastavte adresář dokumentů
Definujte složku, která obsahuje obrázky, které chcete zpracovat.

```csharp
// ExStart:1   
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

> **Tip:** Použijte absolutní cestu nebo `Path.Combine`, abyste se vyhnuli problémům s oddělovači cest na různých OS.

### Krok 2: Inicializujte Aspose.OCR
Vytvořte instanci OCR enginu.

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Krok 3: Zadejte cestu k obrázkům
Nasmerujte API na konkrétní podadresář, který obsahuje vaše soubory obrázků.

```csharp
// Image Path
string fullPath = dataDir + "OCR";
```

> **Proč je to důležité:** Metoda `RecognizeMultipleImages` očekává cestu ke složce, nikoli k jednotlivému souboru.

### Krok 4: Rozpoznat obrázky
Spusťte OCR na každém obrázku ve složce. Můžete přizpůsobit `RecognitionSettings`, pokud potřebujete nápovědy pro jazyk nebo specifické předzpracování.

```csharp
// Recognize image           
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
    //default or custom
});
```

### Krok 5: Vytisknout výsledky
Projděte vrácené pole `RecognitionResult` a vypište extrahovaný text.

```csharp
// Print result
for (int i = 0; i < result.Length; i++)
{
    Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
```

> **Častý úskalí:** Zapomenutí zkontrolovat `result.Length` může způsobit `IndexOutOfRangeException`, když je složka prázdná. Vždy nejprve ověřte obsah složky.

### Krok 6: Zpráva o dokončení
Signalizujte úspěšné provedení.

```csharp
// ExEnd:1
Console.WriteLine("OCROperationWithFolder executed successfully");
```

## Časté problémy a řešení

| Problém | Příčina | Řešení |
|-------|-------|-----|
| Žádný výstup | Cesta ke složce nesprávná nebo prázdná | Ověřte, že `fullPath` ukazuje na správný adresář a obsahuje podporované formáty obrázků (PNG, JPEG, TIFF). |
| Zkreslené znaky | Nesprávné nastavení jazyka | Předávejte nakonfigurované `RecognitionSettings` s `Language` nastaveným na odpovídající ISO kód. |
| Zpomalení výkonu při mnoha obrázcích | Zpracování sekvenčně na UI vlákně | Spusťte OCR na pozadí nebo použijte async vzory, aby UI zůstalo responzivní. |

## Často kladené otázky

**Q: Mohu použít Aspose.OCR for .NET v komerčních projektech?**  
A: Ano, Aspose.OCR for .NET je komerční produkt. Informace o licencování najdete [zde](https://purchase.aspose.com/buy).

**Q: Je k dispozici bezplatná zkušební verze?**  
A: Ano, můžete vyzkoušet bezplatnou verzi [zde](https://releases.aspose.com/).

**Q: Kde najdu dokumentaci?**  
A: Dokumentace je dostupná [zde](https://reference.aspose.com/ocr/net/).

**Q: Jak získat dočasnou licenci?**  
A: Dočasné licence lze získat [zde](https://purchase.aspose.com/temporary-license/).

**Q: Potřebujete podporu nebo máte otázky?**  
A: Navštivte [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) pro komunitní podporu.

---

**Poslední aktualizace:** 2025-12-21  
**Testováno s:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}