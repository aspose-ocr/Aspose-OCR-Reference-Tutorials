---
category: general
date: 2026-03-28
description: Proveďte OCR na obrázku v Javě pomocí Aspose OCR, převádějte obrázek
  na text a rychle a spolehlivě extrahujte thajský text z PNG.
draft: false
keywords:
- run OCR on image
- convert image to text
- extract text from PNG
- extract Thai text
- recognize Thai text
language: cs
og_description: Spusťte OCR na obrázku pomocí Javy a Aspose OCR. Naučte se, jak převést
  obrázek na text, extrahovat thajský text z PNG a řešit běžné úskalí.
og_title: Spusťte OCR na obrázku pomocí Javy – Rychle extrahujte thajský text
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Spusťte OCR na obrázku v Javě – Extrahujte thajský text z PNG
url: /cs/java/ocr-operations/run-ocr-on-image-with-java-extract-thai-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spusťte OCR na obrázku v Javě – Kompletní tutoriál

Už jste se někdy zamýšleli, jak **run OCR on image** soubory spustit přímo z Java kódu? Možná máte sbírku thajských účtenek, naskenovaných dokumentů nebo screenshotů a potřebujete získat text, aniž byste ho museli ručně přepisovat. To je častý problém, zejména když je zdrojovým souborem PNG a jazyk není latinský.  

V tomto průvodci vám ukážeme, jak **run OCR on image** pomocí knihovny Aspose OCR, převést obrázek na prostý text a spolehlivě získat thajské znaky. Na konci budete umět **convert image to text**, **extract text from PNG** a dokonce **recognize Thai text** pomocí několika řádků kódu.

## Co tento tutoriál pokrývá

* Nastavení závislosti Aspose OCR v projektu Maven/Gradle.  
* Inicializaci `OcrEngine` a konfiguraci pro thajský jazyk.  
* Spuštění OCR na souboru PNG a ošetření možných chyb.  
* Vytištění výsledku do konzole a ověření výstupu.  

Předchozí zkušenost s Aspose není vyžadována – stačí základní Java IDE a obrázek, který chcete zpracovat.

## Požadavky

* Java 8 nebo novější (knihovna funguje i s Java 11+).  
* Nástroj pro sestavování – Maven nebo Gradle (ukážeme ukázku pro Maven).  
* Licence Aspose OCR (bezplatná zkušební verze stačí pro testování, ale licence odstraňuje omezení hodnocení).  
* PNG obsahující thajský text, např. `input.png` umístěný ve složce resources vašeho projektu.

---

## Krok 1: Přidejte Aspose OCR do svého projektu

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version -->
</dependency>
```

### Gradle (Kotlin DSL)

```kotlin
implementation("com.aspose:aspose-ocr:23.9")
```

> **Tip:** Udržujte verzi knihovny v souladu s oficiálními poznámkami k vydání Aspose; novější verze přidávají jazykové balíčky a vylepšení výkonu.

Po vyřešení závislosti by vám IDE mělo automaticky importovat požadované třídy.

## Krok 2: Inicializujte OCR Engine

Engine je srdcem procesu – představte si ho jako „mozek“, který analyzuje vzory pixelů. Také mu řekneme, že nás zajímají jen thajské znaky.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Tell the engine to look for Thai language patterns
        ocrEngine.getRecognitionSettings().setLanguage("th");
```

Proč nastavit jazyk explicitně? Protože zadání `"th"` zužuje množinu znaků, což urychluje rozpoznávání a snižuje chybné čtení podobně vypadajících glyfů.

## Krok 3: Spusťte OCR na souboru PNG

Nyní předáme engine obrázek, který chceme dekódovat. Metoda `recognizeImage` vrací objekt `OcrResult`, který obsahuje extrahovaný řetězec a skóre důvěry.

```java
        // Step 3: Perform OCR on the target image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

Pokud soubor nelze najít, Aspose vyhodí `FileNotFoundException`. Je dobré obalit volání do bloku `try‑catch` v produkčním kódu, ale pro tento tutoriál to ponecháme jednoduché.

## Krok 4: Výstup rozpoznaného textu

Nakonec výsledek vytiskneme. Metoda `getText()` vrací prostý Java `String`, který můžete uložit, poslat po síti nebo zapsat do souboru.

```java
        // Step 4: Display the extracted Thai text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Po spuštění programu byste měli vidět něco podobného:

```
=== Recognized Thai Text ===
สวัสดีครับ นี่คือข้อความจากรูปภาพ
```

Pokud výstup vypadá poškozeně, zkontrolujte, že zdrojové PNG má vysoké rozlišení (alespoň 300 dpi) a že kód jazyka `"th"` odpovídá vašemu cílovému jazyku.

### Kompletní výpis

Níže je kompletní, připravený ke spuštění Java soubor. Zkopírujte jej do svého IDE, případně upravte cestu k obrázku, a stiskněte **Run**.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Select Thai language for recognition
        ocrEngine.getRecognitionSettings().setLanguage("th");

        // Run OCR on the PNG image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // Output the recognized text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

![run OCR on image example](image.png "run OCR on image example – Java code extracting Thai text from PNG")

## Krok 5: Běžné varianty a okrajové případy

### Převod obrázku na text v jiných formátech

Pokud potřebujete **convert image to text** pro JPEG nebo BMP, stačí změnit příponu souboru v `imagePath`. Aspose OCR podporuje PNG, JPEG, BMP, TIFF a dokonce i PDF stránky.

### Extrakce textu z PNG s více jazyky

Můžete nechat engine detekovat několik jazyků najednou:

```java
ocrEngine.getRecognitionSettings().setLanguage("th,en");
```

Výsledek bude obsahovat směs thajských a anglických znaků, což je užitečné pro bilingvní účtenky.

### Zpracování obrázků nízké kvality

U rozmazaných skenů zvažte zapnutí předzpracování:

```java
ocrEngine.getRecognitionSettings().setPreprocessMode(PreprocessMode.Auto);
```

Tím se spustí vestavěné algoritmy pro odstranění šumu a zvýšení kontrastu, což zlepšuje krok **extract text from PNG**.

### Aktivace licence

Bez licence Aspose vloží vodotiskovou řádku do výstupu po 100 stránkách. Aktivujte licenci co nejdříve:

```java
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

Umístěte soubor `.lic` vedle svého JAR souboru nebo na něj odkažte pomocí absolutní cesty.

## Často kladené otázky

**Q: Funguje to na Linuxu?**  
A: Naprosto. Aspose OCR je čistě Java, takže jakýkoli OS kompatibilní s JVM je v pořádku.

**Q: Co když PNG obsahuje ručně psanou thajštinu?**  
A: Rozpoznávání rukopisu je omezené; možná budete potřebovat specializovaný model neuronové sítě. Aspose OCR exceluje u tištěného textu.

**Q: Můžu zpracovat složku obrázků najednou?**  
A: Zabalte volání `recognizeImage` do smyčky přes `Files.list(Paths.get("folder"))`. Pro výkon pamatujte na opakované použití stejné instance `OcrEngine`.

## Závěr

Prošli jsme kompletním příkladem, jak **run OCR on image** soubory v Javě, konkrétně jak **extract Thai text** z PNG. Inicializací `OcrEngine`, nastavením jazyka, voláním `recognizeImage` a vytištěním výsledku máte nyní spolehlivý způsob, jak **convert image to text** bez použití třetích stran.

Odtud můžete:

* **extract text from PNG** soubory hromadně pro projekty data‑miningu.  
* Kombinovat výstup OCR s překladovým API a získat anglické ekvivalenty.  
* Prozkoumat další jazyky podporované Aspose, jako čínštinu nebo arabštinu, změnou kódu jazyka.

Vyzkoušejte to na vlastních obrázcích – upravte nastavení předzpracování, experimentujte s různými formáty souborů a zjistěte, jak robustní je řešení ve vašem reálném workflow.

Šťastné programování a ať jsou vaše OCR pipeline vždy přesné!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}