---
date: 2026-05-24
description: Objevte, jak používat OCR s Aspose.OCR pro Java, extrahovat text z obrázků,
  nastavit povolené znaky a během několika minut použít dočasnou licenci.
keywords:
- how to use OCR
- extract text from images
- how to apply license
- how to set characters
linktitle: Specifikace povolených znaků v Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-05-24'
  description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  headline: How to Use OCR – Extract Text from Images with Aspose.OCR
  type: TechArticle
- description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  name: How to Use OCR – Extract Text from Images with Aspose.OCR
  steps:
  - name: Set Your Document Directory
    text: Choose a folder where OCR results and temporary files will be stored. This
      path is later used to locate the image you want to process.
  - name: Specify the Image Path
    text: Provide the full file system path or a class‑path resource location that
      points to the image you wish to analyse.
  - name: Create an Aspose.OCR Instance
    text: '`AsposeOCR` is the core engine that performs optical character recognition.
      Instantiate it with either a temporary or permanent license string.'
  - name: Perform OCR Recognition
    text: '`RecognizeLine` extracts a single line of text from the supplied image
      and returns it as a plain Java `String`. You can call this method repeatedly
      for multi‑line documents. > **Pro tip:** If you need to restrict the output
      to digits only (e.g., for invoice numbers), call `setAllowedCharacters("0123'
  type: HowTo
- questions:
  - answer: Visit the [temporary license page](https://purchase.aspose.com/temporary-license/)
      to request a trial key that removes evaluation watermarks.
    question: How can I obtain a temporary license for Aspose.OCR?
  - answer: Join the community at the [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16)
      for help and discussions.
    question: Where can I find support for Aspose.OCR?
  - answer: Yes, use the `setAllowedCharacters` API to define a custom whitelist of
      characters. This is ideal for numeric‑only fields.
    question: Can I specify allowed characters in Aspose.OCR?
  - answer: Absolutely—Aspose.OCR is regularly updated to stay compatible with the
      newest Java releases.
    question: Is Aspose.OCR compatible with the latest JDK versions?
  - answer: The library also supports block, paragraph, and full‑page recognition,
      language packs, and advanced image preprocessing.
    question: Are there additional OCR features beyond line recognition?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Jak používat OCR – Extrahovat text z obrázků pomocí Aspose.OCR
url: /cs/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat OCR – Extrahovat text z obrázků pomocí Aspose.OCR

V moderních Java aplikacích je **jak používat OCR** častou otázkou, zejména když potřebujete převést naskenované faktury, účtenky nebo tištěné formuláře na prohledávatelný text. Tento tutoriál vás provede kompletním **Aspose.OCR pro Java** příkladem: extrahování textu z obrázků, omezení výstupu na vlastní sadu znaků a použití dočasné licence pro rychlé vyhodnocení.

## Rychlé odpovědi
- **Co dělá Aspose.OCR?** Extrahuje text z obrázků s vysokou přesností a umožňuje omezit rozpoznávané znaky.  
- **Potřebuji licenci?** Pro produkční použití je vyžadována dočasná nebo trvalá licence; dočasný klíč odstraňuje vodoznaky.  
- **Jaká verze JDK je podporována?** Knihovna funguje s nejnovějšími verzemi JDK (JDK 17, 19, 21).  
- **Mohu omezit rozpoznávané znaky?** Ano – použijte metodu `setAllowedCharacters` k omezení výstupu.  
- **Jak dlouho trvá nastavení?** Přibližně 10‑15 minut pro základní end‑to‑end implementaci.

## Co je “extrahovat text z obrázků”?
Extrahování textu z obrázků, také známé jako optické rozpoznávání znaků (OCR), převádí vizuální znaky – ať už tištěné, ručně psané nebo napsané na klávesnici – na strojově čitelné řetězce. Tato transformace umožňuje aplikacím vyhledávat, indexovat, upravovat a analyzovat obsah programově, podporuje workflow jako zpracování faktur, archivaci dokumentů a automatizaci zadávání dat.

## Proč použít Aspose.OCR pro Java?
Aspose.OCR podporuje **více než 60 jazyků**, dokáže zpracovat obrázky až do **10 MB** bez načítání celého souboru do paměti a dosahuje **>95 % přesnosti** u čistých skenů. Knihovna je samostatná, nevyžaduje externí OCR enginy, což zjednodušuje nasazení a snižuje licenční náklady.

## Předpoklady

### Java Development Kit (JDK)

Ujistěte se, že máte nainstalovaný nejnovější Java Development Kit. Stáhnout jej můžete [zde](https://www.oracle.com/java/technologies/javase-downloads.html).

### Aspose.OCR pro Java knihovna

Stáhněte a nainstalujte knihovnu Aspose.OCR pro Java z [odkazu ke stažení](https://releases.aspose.com/ocr/java/).

### Aspose.OCR licence

Pro odemknutí plné funkčnosti získejte licenci. Zakoupit ji můžete [zde](https://purchase.aspose.com/buy) nebo požádat o [dočasnou licenci](https://purchase.aspose.com/temporary-license/) pro zkušební účely.

## Jak používat OCR s Aspose.OCR pro Java?

Načtěte svůj obrázek, nakonfigurujte OCR engine a zavolejte metodu rozpoznání – vše během několika jednoduchých řádků. Tento přímý návod vám říká, co přesně udělat: vytvořit instanci `AsposeOCR` s vaším licenčním řetězcem, nastavit povolené znaky a zavolat `RecognizeLine` na cílovém obrázku, abyste získali extrahovaný text. API interně provádí předzpracování obrázku, takže získáte čisté výsledky bez dalšího kódu.

### Import balíčků

Třída `AsposeOCR` se nachází v balíčku `com.aspose.ocr`. Před zahájením kódování importujte požadované třídy.

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Průvodce krok za krokem

### Krok 1: Nastavte adresář dokumentů

Vyberte složku, kam budou uloženy výsledky OCR a dočasné soubory. Tato cesta bude později použita k nalezení obrázku, který chcete zpracovat.

```java
String dataDir = "Your Document Directory";
```

### Krok 2: Zadejte cestu k obrázku

Uveďte úplnou cestu v souborovém systému nebo umístění zdroje v class‑path, které ukazuje na obrázek, který chcete analyzovat.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### Krok 3: Vytvořte instanci Aspose.OCR

`AsposeOCR` je jádro, které provádí optické rozpoznávání znaků. Vytvořte ji buď s dočasným, nebo s trvalým licenčním řetězcem.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### Krok 4: Proveďte OCR rozpoznání

`RecognizeLine` extrahuje jediný řádek textu z předaného obrázku a vrátí jej jako obyčejný Java `String`. Tuto metodu můžete volat opakovaně pro víceřádkové dokumenty.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Tip:** Pokud potřebujete omezit výstup pouze na číslice (např. pro čísla faktur), zavolejte `setAllowedCharacters("0123456789")` na instanci `AsposeOCR` před voláním `RecognizeLine`. Tím přinutíte engine ignorovat jakékoli ne‑číselné symboly.  
> `setAllowedCharacters` je metoda třídy `AsposeOCR`, která omezuje OCR výstup na specifikovaný whitelist znaků.

## Časté problémy a řešení

| Problém | Důvod | Řešení |
|-------|--------|-----|
| **Žádný výstup nebo prázdný řetězec** | Nesprávná cesta k obrázku nebo nepodporovaný formát | Ověřte `imagePath` a použijte podporovaný formát (JPEG, PNG, BMP) |
| **Chyby rozpoznání** | Nízké rozlišení obrázku nebo šum v pozadí | Předzpracujte obrázek (zvyšte kontrast, binarizujte) před OCR |
| **Licence nebyla aplikována** | Chybějící nebo neplatný licenční klíč | Ujistěte se, že licenční řetězec je správný a předán konstruktoru `AsposeOCR` |

## Často kladené otázky

**Q: Jak získat dočasnou licenci pro Aspose.OCR?**  
A: Navštivte [stránku s dočasnou licencí](https://purchase.aspose.com/temporary-license/) a požádejte o zkušební klíč, který odstraňuje evaluační vodoznaky.

**Q: Kde mohu najít podporu pro Aspose.OCR?**  
A: Připojte se ke komunitě na [Aspose.OCR fóru](https://forum.aspose.com/c/ocr/16) pro pomoc a diskuze.

**Q: Mohu v Aspose.OCR specifikovat povolené znaky?**  
A: Ano, použijte API `setAllowedCharacters` k definování vlastního whitelistu znaků. To je ideální pro pole pouze s čísly.

**Q: Je Aspose.OCR kompatibilní s nejnovějšími verzemi JDK?**  
A: Rozhodně – Aspose.OCR je pravidelně aktualizován, aby zůstal kompatibilní s nejnovějšími verzemi Java.

**Q: Existují další OCR funkce nad rámec rozpoznání řádků?**  
A: Knihovna také podporuje rozpoznání bloků, odstavců a celých stránek, jazykové balíčky a pokročilé předzpracování obrázků.

## Závěr

Po absolvování tohoto **Aspose OCR Java tutoriálu** nyní víte, **jak používat OCR** k extrahování textu z obrázků, omezení sady znaků a použití dočasné licence pro rychlé testování. Prozkoumejte podrobnou [dokumentaci](https://reference.aspose.com/ocr/java/) a objevte podporu více jazyků, hromadné zpracování a vlastní předzpracovací pipeline.

---

**Poslední aktualizace:** 2026-05-24  
**Testováno s:** Aspose.OCR pro Java 24.11  
**Autor:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Související tutoriály

- [Jak nastavit licenci a ověřit Aspose.OCR licenci v Javě](/ocr/java/ocr-basics/set-license/)
- [Převod obrázku na text v Javě pomocí Aspose.OCR BufferedImage](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Aspose OCR Java příklad – Rozpoznávání řádků v obrázcích](/ocr/java/advanced-ocr-techniques/recognize-lines/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}