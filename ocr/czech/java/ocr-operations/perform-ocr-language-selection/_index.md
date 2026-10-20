---
date: 2026-02-12
description: Naučte se, jak pomocí Aspose.OCR pro Javu provádět OCR textu z obrázku
  s výběrem jazyka. Tento krok‑za‑krokem průvodce zahrnuje extrakci textu v Javě,
  korekci zkosení OCR a další.
linktitle: How to OCR Image Text with Language Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Jak pomocí Aspose.OCR provést OCR textu na obrázku s jazykem
url: /cs/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést OCR textu z obrázku s jazykem pomocí Aspose.OCR

## Úvod

Extrahování textu z obrazových souborů je běžná potřeba, ať už digitalizujete naskenované dokumenty, zpracováváte účtenky nebo budujete prohledávatelné archivy. V tomto tutoriálu vás provedeme kompletním praktickým příkladem, který ukazuje **jak provést OCR textu z obrázku** s konkrétním nastavením jazyka, takže můžete ještě dnes integrovat spolehlivé OCR do svých Java aplikací. Také uvidíte, jak řešit korekci sklonu OCR a rozpoznávání založené na regionech pro optimální přesnost.

## Rychlé odpovědi
- **Jaká knihovna provádí OCR v Javě?** Aspose.OCR for Java  
- **Které nastavení vybírá jazyk?** `settings.setLanguage(Language.Eng)` (nebo jakýkoli podporovaný jazyk)  
- **Potřebuji licenci pro vývoj?** Bezplatná evaluační licence funguje pro testování; pro produkci je vyžadována komerční licence.  
- **Mohu omezit OCR na oblast obrázku?** Ano, použijte `RecognitionSettings.setRecognitionAreas()` s obdélníky.  
- **Jaký je typický čas běhu?** Několik sekund na stránku na standardním notebooku, v závislosti na velikosti obrázku a složitosti jazyka.

## Jak provést OCR textu z obrázku s výběrem jazyka
V této sekci odpovídáme na hlavní otázku **jak provést OCR** obrázku, když znáte jazyk textu. Výběr správného jazyka dramaticky zvyšuje přesnost rozpoznání, protože OCR engine může použít jazykově specifické slovníky a modely znaků.

### Proč je to důležité
- **Vyšší přesnost** – jazykově specifické modely snižují chybné rozpoznání.  
- **Zvýšení výkonu** – engine vynechává zbytečné kontroly jiných jazyků.  
- **Lepší zacházení s diakritikou** – francouzština, španělština, němčina atd. jsou rozpoznány správně, když je použeno odpovídající `Language` enum.

## Co je „extrahování textu z obrázku“?
Extrahování textu z obrázku (OCR) převádí vizuální reprezentaci znaků na strojově čitelné řetězce. To umožňuje vyhledávání, analytiku a workflow pro získávání dat, které by jinak vyžadovaly ruční přepis.

## Proč použít Aspose.OCR s výběrem jazyka?
- **Podpora více jazyků** – Vyberte přesně jazyk(y) přítomné v obrázku a zvýšte přesnost.  
- **Jemná kontrola** – Nastavte korekci sklonu, definujte oblasti rozpoznávání a nastavte chování auto‑sklonu.  
- **Čisté Java API** – Žádné nativní závislosti, snadná integrace do jakéhokoli Java projektu.  
- **Bohatá výstupní data** – Získáte prostý text, JSON, ohraničující obdélníky a varování v jednom volání.

## Předpoklady

Než začnete, ujistěte se, že máte:

- **Java Development Kit (JDK)** nainstalovaný (JDK 8 nebo novější).  
- **Aspose.OCR for Java** knihovnu – stáhněte ji z oficiální stránky [here](https://reference.aspose.com/ocr/java/).  
- Soubor obrázku, který obsahuje text, který chcete extrahovat, např. `p3.png`.

## Import balíčků

Ve vašem Java zdrojovém souboru zahrňte požadované Aspose.OCR třídy a standardní Java utility:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Průvodce krok za krokem

### Krok 1: Nastavte adresář dokumentů

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Nahraďte `"Your Document Directory"` absolutní cestou, kde se nachází `p3.png`.

### Krok 2: Definujte cestu k obrázku

```java
// The image path
String file = dataDir + "p3.png";
```

Ujistěte se, že proměnná `file` ukazuje na přesně ten obrázek, který chcete zpracovat.

### Krok 3: Vytvořte instanci Aspose.OCR API

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

Objekt `AsposeOCR` vám poskytuje přístup ke všem OCR operacím.

### Krok 4: Nastavte možnosti rozpoznávání (výběr jazyka)

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Zde:

1. Vypneme auto‑sklon, protože poskytujeme manuální hodnotu sklonu.  
2. Definujeme obdélníkovou oblast (`RecognitionAreas`), abychom omezili OCR na část obrázku, která skutečně obsahuje text.  
3. Nastavíme **jazyk** na angličtinu (`Language.Eng`). Změňte na `Language.Fra`, `Language.Spa` atd., podle vašeho zdrojového obrázku.

### Krok 5: Proveďte OCR a získejte výsledky

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Volání `RecognizePage` spustí OCR engine s obrázkem a nastavením, která jste definovali. Výsledek je uložen v objektu `RecognitionResult`.

### Krok 6: Vytiskněte a využijte výsledky

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

Výstup v konzoli ukazuje:

- Celý extrahovaný text (`recognitionText`).  
- Text pro každý definovaný obdélník (`recognitionAreasText`).  
- Souřadnice ohraničujících obdélníků.  
- JSON reprezentaci pro snadné další zpracování.  
- Detekovaný úhel sklonu a případná varování.

Nyní můžete `result.recognitionText` předat do své obchodní logiky – uložit, indexovat nebo předat dalšímu servisu.

## Časté problémy a řešení

| Problém | Příčina | Řešení |
|-------|-------|-----|
| **Garbage characters** | Špatně vybraný jazyk | Nastavte správný `Language` enum (např. `Language.Fra` pro francouzštinu). |
| **No text returned** | Oblast rozpoznávání nepokrývá text | Upravit souřadnice `Rectangle` nebo odstranit `RecognitionAreas` pro zpracování celého obrázku. |
| **Slow performance** | Velmi velký obrázek nebo vysoké rozlišení | Zmenšete obrázek před OCR nebo zvýšte alokaci paměti pro JVM. |
| **Warnings about unsupported format** | Formát obrázku není rozpoznán | Převeďte obrázek na PNG, JPEG nebo TIFF před zpracováním. |

## Často kladené otázky

**Q: Mohu rozpoznat více jazyků v jednom volání OCR?**  
A: Ano. Použijte `settings.setLanguage(Language.Eng | Language.Fra)` pro povolení vícejazykového rozpoznání.

**Q: Jaké formáty obrázků Aspose.OCR podporuje?**  
A: PNG, JPEG, BMP, TIFF, GIF a několik dalších. Stačí zadat správnou cestu k souboru.

**Q: Existuje limit velikosti obrázku?**  
A: Neexistuje pevný limit, ale velmi velké obrázky zvyšují spotřebu paměti a dobu zpracování. Zvažte změnu velikosti velkých souborů.

**Q: Jak získám produkční licenci?**  
A: Zakupte licenci na webu Aspose a aplikujte ji pomocí třídy `License`, jak je ukázáno v dokumentaci Aspose.

**Q: Mohu přímo extrahovat text z PDF stránky?**  
A: Ne přímo pomocí Aspose.OCR. Nejprve převěďte PDF stránku na obrázek (např. pomocí Aspose.PDF) a poté spusťte OCR.

## Závěr

Nyní jste viděli, jak **extrahovat text z obrázku** pomocí Aspose.OCR pro Java při výběru vhodného jazyka a omezení rozpoznávání na konkrétní oblasti. Tento přístup poskytuje přesné, výkonné OCR, které lze vložit do jakéhokoli Java‑based workflow – od systémů správy dokumentů po datové zachytávací pipeline. Připravení pokračovat? Vyzkoušejte změnu jazykového enumu, experimentujte s různými oblastmi rozpoznávání a integrujte výsledky do vlastní aplikační logiky.

---

**Last Updated:** 2026-02-12  
**Tested With:** Aspose.OCR 24.11 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}