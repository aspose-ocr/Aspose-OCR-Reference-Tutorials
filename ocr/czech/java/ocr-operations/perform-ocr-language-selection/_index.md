---
title: Provádění OCR s výběrem jazyka v Aspose.OCR
linktitle: Provádění OCR s výběrem jazyka v Aspose.OCR
second_title: Aspose.OCR Java API
description: Odemkněte přesnou extrakci textu z obrázků pomocí Aspose.OCR pro Java. Postupujte podle našeho podrobného průvodce pro přesné OCR s výběrem jazyka.
type: docs
weight: 11
url: /cs/java/ocr-operations/perform-ocr-language-selection/
---
## Úvod

V neustále se vyvíjejícím prostředí technologií hraje optické rozpoznávání znaků (OCR) klíčovou roli při získávání smysluplných informací z obrázků. Aspose.OCR for Java vyniká jako výkonný nástroj, který umožňuje vývojářům bezproblémově integrovat funkce OCR do jejich aplikací Java. V tomto podrobném průvodci prozkoumáme, jak provádět OCR s výběrem jazyka pomocí Aspose.OCR, čímž se uvolní potenciál pro přesné zpracování různorodého obsahu.

## Předpoklady

Než se pustíte do výukového programu, ujistěte se, že máte splněny následující předpoklady:

- Vývojové prostředí Java: Ujistěte se, že máte v systému nainstalovanou Javu a že je vaše vývojové prostředí nastaveno.

-  Knihovna Aspose.OCR: Stáhněte a nainstalujte knihovnu Aspose.OCR pro Javu. Najdete zde knihovnu a související dokumentaci[tady](https://reference.aspose.com/ocr/java/).

- Soubor obrázku: Připravte soubor obrázku obsahující text, který chcete extrahovat. Použijme například soubor s názvem "p3.png."

## Importujte balíčky

Ve svém projektu Java naimportujte potřebné balíčky, abyste mohli využít funkce Aspose.OCR. Na začátek souboru Java přidejte následující řádky:

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

## Krok 1: Nastavte adresář dokumentů

```java
// Cesta k adresáři dokumentů.
String dataDir = "Your Document Directory";
```

Nahraďte "Your Document Directory" skutečnou cestou k adresáři, kde je umístěn váš soubor obrázku.

## Krok 2: Definujte cestu obrázku

```java
// Cesta obrazu
String file = dataDir + "p3.png";
```

Upravte proměnnou souboru tak, aby ukazovala na váš konkrétní soubor obrázku.

## Krok 3: Vytvořte instanci Aspose.OCR API

```java
// Vytvořte instanci API
AsposeOCR api = new AsposeOCR();
```

Inicializací objektu AsposeOCR získáte přístup k jeho funkcím.

## Krok 4: Nastavte možnosti rozpoznávání

```java
// Nastavte možnosti rozpoznávání
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Přizpůsobte nastavení rozpoznávání podle svých požadavků. Upravte parametry, jako je zkosení, jazyk a oblasti rozpoznávání.

## Krok 5: Proveďte OCR a načtěte výsledky

```java
// Získejte výsledný objekt
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Proveďte operaci OCR pomocí zadaného souboru obrázku a nastavení. Zachyťte výsledek do objektu RecognitionResult.

## Krok 6: Vytiskněte a využijte výsledky

```java
// Vytisknout výsledek
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

Vytiskněte extrahovaný text, rozpoznávací oblasti, reprezentaci JSON, úhel zkosení a veškerá varování. Použijte výsledky podle potřeby ve své aplikaci.

## Závěr

V tomto tutoriálu jsme se ponořili do bezproblémové integrace Aspose.OCR pro Java pro provádění OCR s výběrem jazyka. Tato výkonná knihovna otevírá svět možností pro vývojáře, kteří chtějí přesně extrahovat text z obrázků.

## FAQ

### Q1: Mohu použít Aspose.OCR pro více jazyků v jednom procesu rozpoznávání?

Odpověď 1: Ano, v RecognitionSettings můžete nastavit více jazyků, abyste zvýšili přesnost rozpoznávání vícejazyčného obsahu.

### Q2: Jak mohu zpracovat různé formáty obrázků pomocí Aspose.OCR?

Odpověď 2: Aspose.OCR podporuje různé formáty obrázků, včetně PNG, JPEG a TIFF. Jednoduše zadejte správnou cestu k souboru v proměnné cesta k obrázku.

### Otázka 3: Existuje omezení velikosti obrázku, který může Aspose.OCR zpracovat?

Odpověď 3: Aspose.OCR dokáže zpracovat obrázky různých velikostí, ale větší obrázky mohou vyžadovat více času a prostředků na zpracování.

### Q4: Mohu doladit nastavení rozpoznávání pro konkrétní oblasti v rámci obrázku?

A4: Rozhodně. Použijte funkci RecognitionAreas k definování konkrétních obdélníků v rámci obrazu pro cílené rozpoznání.

### Q5: Je Aspose.OCR vhodný pro osobní i komerční projekty?

A5: Ano, Aspose.OCR nabízí flexibilní možnosti licencování, takže je vhodný pro osobní i komerční použití.