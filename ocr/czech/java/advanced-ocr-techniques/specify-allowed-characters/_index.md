---
date: 2026-02-20
description: Naučte se, jak extrahovat text z obrázků pomocí Aspose.OCR pro Javu,
  nastavit povolené znaky a použít dočasnou licenci – kompletní tutoriál Aspose OCR
  pro Javu.
linktitle: Specifying Allowed Characters in Aspose.OCR
second_title: Aspose.OCR Java API
title: Extrahování textu z obrázků pomocí Aspose.OCR – Povolené znaky
url: /cs/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

 final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z obrázků pomocí Aspose.OCR – Povolené znaky

## Úvod

Extrahování textu z obrázků je běžnou požadavkem v moderních aplikacích – ať už zpracováváte faktury, skenujete účtenky nebo digitalizujete tištěné dokumenty. V tomto tutoriálu projdeme kompletní **aspose ocr java tutorial**, který vám ukáže, jak **extrahovat text z obrázků** pomocí Aspose.OCR pro Java, nastavit povolené znaky a použít dočasnou licenci, když knihovnu jen testujete.

## Rychlé odpovědi
- **Co dělá Aspose.OCR?** Extrahuje text z obrázků s vysokou přesností a podporuje vlastní sady znaků.  
- **Potřebuji licenci?** Pro produkční použití je vyžadována dočasná nebo trvalá licence.  
- **Která verze JDK je podporována?** Nejnovější verze JDK jsou plně kompatibilní.  
- **Mohu omezit rozpoznávané znaky?** Ano – použijte API `setAllowedCharacters` k omezení výstupu.  
- **Jak dlouho trvá nastavení?** Přibližně 10‑15 minut pro základní implementaci.

## Co je „extrahování textu z obrázků“?
Extrahování textu z obrázků označuje proces převodu vizuálního textu (např. tištěného nebo ručně psaného) na strojově čitelné řetězce. To umožňuje následné úkoly, jako je vyhledávání, indexování nebo analýza dat.

## Proč použít Aspose.OCR pro Java?
- **Vysoká přesnost** napříč mnoha jazyky a fonty.  
- **Jednoduché API**, které se integruje do jakéhokoli Java projektu.  
- **Přizpůsobitelné** sady znaků, jazykové balíčky a předzpracování obrázků.  
- **Žádné externí závislosti** – knihovna je samostatná.

## Předpoklady

Předtím, než začnete, ujistěte se, že máte následující:

### Java Development Kit (JDK)

Ujistěte se, že máte nainstalovaný nejnovější Java Development Kit ve vašem systému. Můžete si jej stáhnout [zde](https://www.oracle.com/java/technologies/javase-downloads.html).

### Aspose.OCR for Java Library

Stáhněte a nainstalujte knihovnu Aspose.OCR pro Java z [odkazu ke stažení](https://releases.aspose.com/ocr/java/).

### Aspose.OCR License

Pro plné využití Aspose.OCR si pořiďte platnou licenci. Můžete ji získat [zde](https://purchase.aspose.com/buy) nebo si prozkoumat [dočasnou licenci](https://purchase.aspose.com/temporary-license/) pro zkušební období.

## Jak použít dočasnou licenci

Když produkt hodnotíte, dočasná licence odstraní vodotisk pro hodnocení a odemkne plnou funkčnost na omezenou dobu. Vytvořte řetězec licence v portálu Aspose a předávejte jej konstruktoru `AsposeOCR`, jak je ukázáno v příkladu kódu níže. Pro produkční nasazení nahraďte dočasný klíč vaší trvalou licencí.

## Tipy pro předzpracování OCR obrázků

Kvalitní obrázek výrazně zlepšuje výsledky rozpoznávání. Před voláním OCR enginu zvažte:

- Převod obrázku na odstíny šedi.
- Zvýšení kontrastu, aby znaky vynikly.
- Odstranění šumu pozadí pomocí binarizačního filtru.
- Změnu velikosti nízkorozlišovacích obrázků na alespoň 300 dpi.

Tyto kroky jsou součástí **ocr image preprocessing** a lze je provést pomocí libovolné standardní Java knihovny pro zpracování obrazu před voláním Aspose.OCR.

## Import balíčků

Jakmile jsou předpoklady připraveny, importujte potřebné balíčky do vašeho Java projektu:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Průvodce krok za krokem

### Krok 1: Nastavte adresář dokumentů

Definujte složku, kde budete ukládat výsledky zpracované OCR. Tato cesta se později použije k nalezení souboru obrázku.

```java
String dataDir = "Your Document Directory";
```

### Krok 2: Zadejte cestu k obrázku

Nasmerujte API na obrázek, který chcete analyzovat.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### Krok 3: Vytvořte instanci Aspose.OCR

Vytvořte instanci OCR enginu s vaším licenčním klíčem. Klíč může být řetězec dočasné nebo trvalé licence.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### Krok 4: Proveďte OCR rozpoznání

Zavolejte metodu `RecognizeLine` k extrahování řádku textu z obrázku. Výsledek je prostý řetězec, který můžete dále zpracovat nebo uložit.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Tip:** Pokud potřebujete omezit výstup na konkrétní sadu znaků (např. pouze číslice), použijte metodu `setAllowedCharacters` na instanci `AsposeOCR` před voláním `RecognizeLine`. Tím zajistíte, že engine bude ignorovat všechny znaky mimo definovanou sadu.

## Časté problémy a řešení

| Problém | Důvod | Řešení |
|-------|--------|-----|
| **Žádný výstup nebo prázdný řetězec** | Nesprávná cesta k obrázku nebo nepodporovaný formát obrázku | Ověřte `imagePath` a použijte podporovaný formát (JPEG, PNG, BMP) |
| **Chyby rozpoznávání** | Nízké rozlišení obrázku nebo šumivé pozadí | Před OCR předzpracujte obrázek (zvyšte kontrast, binarizujte) |
| **Licence nebyla použita** | Chybějící nebo neplatný licenční klíč | Ujistěte se, že licenční řetězec je správný a umístěn v konstruktoru `AsposeOCR` |

## Často kladené otázky

**Q: Jak mohu získat dočasnou licenci pro Aspose.OCR?**  
A: Navštivte [stránku dočasné licence](https://purchase.aspose.com/temporary-license/) a požádejte o zkušební licenci.

**Q: Kde mohu najít podporu pro Aspose.OCR?**  
A: Připojte se ke komunitě na [Fóru Aspose.OCR](https://forum.aspose.com/c/ocr/16) pro pomoc a diskuze.

**Q: Mohu v Aspose.OCR specifikovat povolené znaky?**  
A: Ano, můžete přizpůsobit sadu znaků pomocí API `setAllowedCharacters`. Podívejte se do oficiální dokumentace pro podrobnosti.

**Q: Je Aspose.OCR kompatibilní s nejnovějšími verzemi JDK?**  
A: Rozhodně – Aspose.OCR je pravidelně aktualizován, aby byl kompatibilní s nejnovějšími verzemi Java.

**Q: Existují další OCR funkce kromě rozpoznávání řádků?**  
A: Ano, knihovna podporuje rozpoznávání bloků, odstavců a celých stránek, stejně jako jazykové balíčky a možnosti předzpracování obrázků.

## Závěr

Po absolvování tohoto **aspose ocr java tutorial** máte nyní funkční řešení pro **extrahování textu z obrázků** a kontrolu, které znaky jsou rozpoznány. Prozkoumejte kompletní [dokumentaci](https://reference.aspose.com/ocr/java/), abyste objevili pokročilé funkce jako podpora více jazyků, vlastní předzpracování a dávkové zpracování.

---

**Last Updated:** 2026-02-20  
**Tested With:** Aspose.OCR for Java 24.11  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}