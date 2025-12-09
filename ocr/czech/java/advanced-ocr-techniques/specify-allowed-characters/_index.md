---
date: 2025-12-09
description: Naučte se, jak pomocí Aspose.OCR pro Javu extrahovat text z obrázků a
  specifikovat povolené znaky – kompletní tutoriál Aspose OCR Java.
linktitle: Specifying Allowed Characters in Aspose.OCR
second_title: Aspose.OCR Java API
title: Extrahovat text z obrázků pomocí Aspose.OCR – Povolené znaky
url: /cs/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z obrázků pomocí Aspose.OCR – Povolené znaky

## Úvod

Extrahování textu z obrázků je běžnou potřebou v moderních aplikacích — ať už zpracováváte faktury, skenujete účtenky nebo digitalizujete tištěné dokumenty. **Aspose.OCR for Java** tuto úlohu usnadňuje, nabízí vysoce přesné rozpoznání a flexibilní konfigurační možnosti, jako je specifikace povolených znaků. V tomto tutoriálu vás provedeme kompletním **aspose ocr java tutorial**, který ukazuje, jak nastavit knihovnu, spustit OCR a omezit sadu znaků podle vašich potřeb.

## Rychlé odpovědi
- **Co Aspose.OCR dělá?** Extrahuje text z obrázků s vysokou přesností a podporuje vlastní sady znaků.  
- **Potřebuji licenci?** Pro produkční použití je vyžadována dočasná nebo trvalá licence.  
- **Jaká verze JDK je podporována?** Nejnovější verze JDK jsou plně kompatibilní.  
- **Mohu omezit rozpoznávané znaky?** Ano — použijte API pro povolené znaky k omezení výstupu.  
- **Jak dlouho trvá nastavení?** Přibližně 10‑15 minut pro základní implementaci.

## Co je „extrahování textu z obrázků“?
Extrahování textu z obrázků označuje proces převodu vizuálního textu (např. tištěného nebo ručně psaného) na strojově čitelné řetězce. To umožňuje následné úkoly, jako je vyhledávání, indexování nebo analýza dat.

## Proč používat Aspose.OCR pro Java?
- **Vysoká přesnost** napříč více jazyky a fonty.  
- **Jednoduché API**, které se integruje do libovolného Java projektu.  
- **Přizpůsobitelné** sady znaků, jazykové balíčky a předzpracování obrázků.  
- **Žádné externí závislosti** — knihovna je samostatná.

## Předpoklady

Než začnete, ujistěte se, že máte následující:

### Java Development Kit (JDK)

Ujistěte se, že máte nainstalovaný nejnovější Java Development Kit. Můžete jej stáhnout [zde](https://www.oracle.com/java/technologies/javase-downloads.html).

### Knihovna Aspose.OCR pro Java

Stáhněte a nainstalujte knihovnu Aspose.OCR pro Java z [odkaz ke stažení](https://releases.aspose.com/ocr/java/).

### Licence Aspose.OCR

Pro plný potenciál Aspose.OCR si pořiďte platnou licenci. Můžete ji získat [zde](https://purchase.aspose.com/buy) nebo vyzkoušet [dočasnou licenci](https://purchase.aspose.com/temporary-license/) pro zkušební období.

## Import balíčků

Jakmile jsou předpoklady připraveny, importujte potřebné balíčky do svého Java projektu:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Průvodce krok za krokem

### Krok 1: Nastavte adresář dokumentů

Definujte složku, kde budete ukládat výsledky zpracované OCR. Tato cesta se později použije k nalezení souboru s obrázkem.

```java
String dataDir = "Your Document Directory";
```

### Krok 2: Zadejte cestu k obrázku

Nasmerujte API na obrázek, který chcete analyzovat.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### Krok 3: Vytvořte instanci Aspose.OCR

Vytvořte OCR engine s vaším licenčním klíčem. Klíč může být dočasný nebo trvalý řetězec.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### Krok 4: Proveďte rozpoznání OCR

Zavolejte metodu `RecognizeLine` k extrahování řádku textu z obrázku. Výsledek je prostý řetězec, který můžete dále zpracovávat nebo ukládat.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Pro tip:** Pokud potřebujete omezit výstup na konkrétní sadu znaků (např. pouze číslice), použijte metodu `setAllowedCharacters` na instanci `AsposeOCR` před voláním `RecognizeLine`. Tím zajistíte, že engine ignoruje všechny znaky mimo definovanou sadu.

## Časté problémy a řešení

| Problém | Důvod | Oprava |
|-------|--------|-----|
| **Žádný výstup nebo prázdný řetězec** | Nesprávná cesta k obrázku nebo nepodporovaný formát obrázku | Ověřte `imagePath` a použijte podporovaný formát (JPEG, PNG, BMP) |
| **Chyby rozpoznání** | Nízké rozlišení obrázku nebo šum v pozadí | Předzpracujte obrázek (zvyšte kontrast, binarizujte) před OCR |
| **Licence nebyla použita** | Chybějící nebo neplatný licenční klíč | Ujistěte se, že licenční řetězec je správný a umístěn v konstruktoru `AsposeOCR` |

## Často kladené otázky

**Q: Jak mohu získat dočasnou licenci pro Aspose.OCR?**  
A: Navštivte [stránku s dočasnou licencí](https://purchase.aspose.com/temporary-license/) a požádejte o zkušební licenci.

**Q: Kde mohu najít podporu pro Aspose.OCR?**  
A: Připojte se ke komunitě na [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16) pro pomoc a diskuze.

**Q: Mohu v Aspose.OCR specifikovat povolené znaky?**  
A: Ano, můžete přizpůsobit sadu znaků pomocí API `setAllowedCharacters`. Podívejte se do oficiální dokumentace pro podrobnosti.

**Q: Je Aspose.OCR kompatibilní s nejnovějšími verzemi JDK?**  
A: Rozhodně — Aspose.OCR je pravidelně aktualizován, aby byl kompatibilní s nejnovějšími verzemi Java.

**Q: Existují další funkce OCR nad rámec rozpoznávání řádků?**  
A: Ano, knihovna podporuje rozpoznávání bloků, odstavců i celých stránek, stejně jako jazykové balíčky a možnosti předzpracování obrázků.

## Závěr

Po absolvování tohoto **aspose ocr java tutorial** máte nyní funkční řešení pro **extrahování textu z obrázků** a kontrolu, které znaky jsou rozpoznány. Prozkoumejte kompletní [documentation](https://reference.aspose.com/ocr/java/) a objevte pokročilé funkce, jako je podpora více jazyků, vlastní předzpracování a dávkové zpracování.

---

**Last Updated:** 2025-12-09  
**Tested With:** Aspose.OCR for Java 24.11  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}