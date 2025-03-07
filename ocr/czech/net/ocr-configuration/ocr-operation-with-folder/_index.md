---
title: OCROoperace se složkou v OCR rozpoznávání obrazu
linktitle: OCROoperace se složkou v OCR rozpoznávání obrazu
second_title: Aspose.OCR .NET API
description: Odemkněte sílu rozpoznávání obrázků OCR v .NET s Aspose.OCR. Extrahujte text z obrázků bez námahy.
weight: 11
url: /cs/net/ocr-configuration/ocr-operation-with-folder/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCROoperace se složkou v OCR rozpoznávání obrazu

## Úvod

Vítejte ve světě optického rozpoznávání znaků (OCR) pomocí Aspose.OCR pro .NET! Pokud hledáte bezproblémové extrahování textu z obrázků v rámci vašich aplikací .NET, jste na správném místě. Tento výukový program vás provede procesem rozpoznávání obrazu OCR pomocí složek a využije výkonné možnosti Aspose.OCR.

## Předpoklady

Než se ponoříte do výukového programu, ujistěte se, že máte následující předpoklady:

- Pracovní znalost vývoje C# a .NET.
- Visual Studio nainstalované na vašem počítači.
-  Aspose.OCR for .NET knihovna, kterou si můžete stáhnout[tady](https://releases.aspose.com/ocr/net/).
- Základní porozumění konceptům OCR.

## Importovat jmenné prostory

V kódu C# se ujistěte, že importujete potřebné jmenné prostory pro použití Aspose.OCR. Na začátek skriptu uveďte následující:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Krok 1: Nastavte adresář dokumentů

```csharp
// Start: 1
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
```

Ujistěte se, že jste nahradili "Your Document Directory" skutečnou cestou, kde jsou uloženy vaše obrázky.

## Krok 2: Inicializujte Aspose.OCR

```csharp
// Inicializujte instanci AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Vytvořte instanci třídy AsposeOcr, abyste mohli využívat její funkce.

## Krok 3: Zadejte cestu obrázku

```csharp
//Cesta obrázku
string fullPath = dataDir + "OCR";
```

Spojte cestu k adresáři dokumentu s konkrétní složkou obsahující vaše obrázky.

## Krok 4: Rozpoznejte obrázky

```csharp
// Rozpoznat obrázek
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
    //výchozí nebo vlastní
});
```

Použijte metodu RecognizeMultipleImages k provedení OCR na více obrazech v zadané složce.

## Krok 5: Tisk výsledků

```csharp
// Vytisknout výsledek
for (int i = 0; i < result.Length; i++)
{
    Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
```

Projděte si výsledky a vytiskněte rozpoznaný text pro každý obrázek.

## Krok 6: Závěr

```csharp
// Rozšíření: 1
Console.WriteLine("OCROperationWithFolder executed successfully");
```

Zajistěte, aby bylo dosaženo uzavření skriptu, což znamená úspěšné provedení operace OCR se složkami.

## Závěr

Gratulujeme! Úspěšně jste se naučili, jak implementovat rozpoznávání obrázků OCR se složkami pomocí Aspose.OCR for .NET. Tento výkonný nástroj otevírá nespočet možností pro extrahování textu z obrázků ve vašich aplikacích .NET.

## FAQ

### Q1: Mohu použít Aspose.OCR pro .NET v komerčních projektech?

 A1: Ano, Aspose.OCR for .NET je komerční produkt. Informace o licencích naleznete na adrese[tady](https://purchase.aspose.com/buy).

### Q2:. Je k dispozici bezplatná zkušební verze?

 A2: Ano, můžete prozkoumat bezplatnou zkušební verzi[tady](https://releases.aspose.com/).

### Q3: Kde najdu dokumentaci?

 A3: Dokumentace je k dispozici[tady](https://reference.aspose.com/ocr/net/).

### Q4: Jak mohu získat dočasné licence?

 A4: Lze získat dočasné licence[tady](https://purchase.aspose.com/temporary-license/).

### Q5: Potřebujete podporu nebo máte otázky?

 A5: Navštivte[Fórum Aspose.OCR](https://forum.aspose.com/c/ocr/16) za podporu komunity.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
