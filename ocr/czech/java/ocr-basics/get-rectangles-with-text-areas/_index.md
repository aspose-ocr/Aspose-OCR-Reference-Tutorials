---
date: 2026-02-09
description: Naučte se, jak převést obrázek na text a extrahovat obdélníky oblastí
  textu pomocí knihovny Aspose OCR pro Javu. Podrobný návod krok za krokem s ukázkami
  kódu.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: Převod obrázku na text – Rozpoznání textu z obrázku a získání obdélníků textových
  oblastí
url: /cs/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převést obrázek na text – Rozpoznat text z obrázku a získat obdélníky oblastí textu

## Úvod

Pokud potřebujete **převést obrázek na text** a **rozpoznat text z obrázku** v Java aplikaci, Aspose.OCR pro Java poskytuje rychlý a přesný způsob, jak to provést. V tomto tutoriálu projdeme přesné kroky potřebné k extrahování odstavců z obrázku, získání ohraničujících obdélníků pro každou oblast textu a vytištění těchto souřadnic do konzole. Na konci pochopíte, proč tento přístup funguje, jak knihovnu integrovat a kde ji můžete rozšířit pro své vlastní případy použití.

## Rychlé odpovědi
- **Co znamená „rozpoznat text z obrázku“?** Znamená to převod vizuálních znaků na obrázku do editovatelných řetězcových dat.  
- **Která knihovna to v Javě řeší?** Aspose.OCR pro Java.  
- **Potřebuji licenci pro vývoj?** Do testování je k dispozici dočasná licence; pro produkci je vyžadována plná licence.  
- **Mohu extrahovat odstavce místo jednotlivých slov?** Ano – použijte `AreasType.PARAGRAPHS` k získání obdélníků na úrovni odstavců.  
- **Je kód kompatibilní s Java 11+?** Rozhodně, API funguje s Java 11 a novějšími.

## Co je „převést obrázek na text“ v Aspose.OCR?
`RecognizePage` metoda Aspose.OCR analyzuje bitmapu, aplikuje OCR algoritmy a vrací rozpoznaný řetězec. Když požadujete oblasti textu, knihovna také vypočítá přesné souřadnice `Rectangle` pro každý blok textu, což usnadňuje pozdější zvýraznění nebo zpracování konkrétních částí.

## Proč použít tuto **java ocr knihovnu**?
- **Vysoká přesnost** – podporuje více jazyků a složité fonty.  
- **Jednoduchá integrace** – jeden JAR přidá plnou OCR funkčnost.  
- **Flexibilní výstup** – můžete získat surový text, formátované HTML nebo přesné obdélníky oblastí textu.  
- **Bezpečné pro vlákna** – vhodné pro prostředí s vysokým průtokem na serveru.

## Předpoklady

- **Java Development Kit** (JDK 11 nebo novější) nainstalovaný na vašem počítači.  
- **Aspose.OCR pro Java** knihovna – stáhněte ji z oficiální stránky [zde](https://releases.aspose.com/ocr/java/).  
- IDE nebo nástroj pro sestavení (Maven/Gradle) pro správu JAR závislosti.

## Import balíčků

Ve vašem Java projektu importujte potřebné třídy:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Průvodce krok za krokem

### Krok 1: Nastavte svůj projekt
Vytvořte nový Java projekt (nebo přidejte do existujícího) a umístěte Aspose.OCR JAR na classpath. Pokud používáte Maven, přidejte závislost podle popisu v balíčku ke stažení.

### Krok 2: Definujte adresář dokumentu a cestu k obrázku
Uveďte, kde se nachází váš ukázkový obrázek:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Krok 3: Vytvořte instanci Aspose.OCR
Vytvořte instanci OCR enginu:

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### Krok 4: Rozpoznat text na obrázku
Zavolejte `RecognizePage` pro převod obrázku na prostý text. Tento krok demonstruje hlavní schopnost **recognize text image java**:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Krok 5: Získat obdélníky s oblastmi textu
Nyní získejte ohraničující obdélníky pro každý odstavec (nebo jiné typy oblastí). Zde **extrahujete odstavce z obrázku** a získáte jejich souřadnice:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Časté problémy a řešení

| Příznak | Pravděpodobná příčina | Řešení |
|---------|-----------------------|--------|
| `IOException` on `RecognizePage` | Nesprávná cesta k souboru nebo chybějící oprávnění ke čtení | Ověřte, že `imagePath` ukazuje na existující PNG/JPG a že aplikace má přístup k souborovému systému. |
| Empty result string | Nízká kvalita obrázku nebo nepodporovaný jazyk | Předzpracujte obrázek (zvyšte kontrast, binarizujte) nebo specifikujte správný jazyk pomocí `api.setLanguage("eng")`. |
| No rectangles returned | Použití nesprávného `AreasType` (např. `WORDS` místo očekávaných odstavců) | Přepněte na `AreasType.PARAGRAPHS` nebo `AreasType.LINES` podle potřeby. |

## Často kladené otázky

**Q: Je Aspose.OCR kompatibilní s Java 11?**  
A: Ano, Aspose.OCR funguje s Java 11 a novějšími verzemi.

**Q: Mohu používat Aspose.OCR jak pro osobní, tak komerční projekty?**  
A: Ano, můžete jej použít v jakémkoli typu projektu. Pro podrobnosti o licencování navštivte [zde](https://purchase.aspose.com/buy).

**Q: Jak získám dočasnou licenci pro hodnocení?**  
A: Dočasnou licenci můžete získat [zde](https://purchase.aspose.com/temporary-license/).

**Q: Kde mohu najít komunitní podporu nebo oficiální asistenci?**  
A: Pro podporu a diskuse navštivte [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16).

**Q: Podporuje Aspose.OCR multithreading?**  
A: Ano, knihovna je bezpečná pro vlákna a může být použita v souběžných prostředích pro lepší výkon.

## Závěr

V tomto **aspose ocr java tutoriálu** jste se naučili, jak **převést obrázek na text** pomocí Aspose.OCR pro Java, extrahovat odstavce a získat přesné obdélníky obklopující každý blok textu. Tyto možnosti vám umožní vytvářet prohledávatelné PDF, zvýrazňovat text v UI překryvech nebo předávat strukturovaná data do následných procesů. Prozkoumejte API dále pro přizpůsobení nastavení jazyka, zpracování různých formátů obrázků nebo integraci s cloudovým úložištěm.

---

**Last Updated:** 2026-02-09  
**Tested With:** Aspose.OCR 23.10 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}