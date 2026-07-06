---
category: general
date: 2026-05-06
description: Jak použít Aspose OCR k rozpoznání textu z obrázku, povolit automatické
  rozpoznávání jazyka a zlepšit rychlost OCR v Javě.
draft: false
keywords:
- how to use aspose
- recognize text from image
- improve ocr speed
- load image for ocr
- enable automatic language detection
language: cs
og_description: Jak použít Aspose OCR k rychlému rozpoznání textu z obrázku, povolit
  automatické rozpoznávání jazyka a zlepšit rychlost OCR v Javě.
og_title: Jak používat Aspose OCR pro obrázky s více jazyky
tags:
- Aspose
- OCR
- Java
- Image Processing
title: Jak použít Aspose OCR pro obrázky s více jazyky
url: /cs/java/advanced-ocr-techniques/how-to-use-aspose-ocr-for-mixed-language-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat Aspose OCR pro obrázky s více jazyky

Už jste se někdy zamýšleli **jak použít Aspose** k získání textu z obrázku, který obsahuje několik jazyků najednou? Nejste sami — vývojáři často narazí na problém, když obrázek kombinuje angličtinu, ruštinu, hindštinu nebo jakýkoli jiný skript. Dobrou zprávou je, že Aspose OCR to zvládá elegantně a můžete dokonce **rozpoznat text z obrázku** rychleji tím, že zúžíte sadu jazyků.

V tomto tutoriálu projdeme kompletním, připraveným příkladem v Javě, který **načte obrázek pro OCR**, zapne **automatické rozpoznávání jazyka** a ukáže jednoduchý trik k **zrychlení OCR**. Na konci budete mít samostatný program, který vytiskne extrahovaný text do konzole, a pochopíte, proč každé nastavení má význam.

> **Požadavky** – Java 17+ nainstalovaná, Maven nebo Gradle pro správu závislostí a licence Aspose OCR (bezplatná zkušební verze stačí pro hodnocení). Žádné další knihovny nejsou potřeba.

---

## Krok 1 – Přidání Aspose OCR do projektu

Než budete moci **používat Aspose**, potřebujete knihovnu na classpath. S Maven vypadá takto:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

Pokud dáváte přednost Gradle:

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Tip:** Používejte nejnovější stabilní verzi; novější verze často obsahují vylepšení výkonu, která přímo ovlivňují **zrychlení OCR**.

---

## Krok 2 – Vytvoření instance OCR Engine  

Srdcem každého pracovního postupu Aspose OCR je `OcrEngine`. Jeho vytvoření je jednoduché, ale stojí za zmínku, že engine uchovává interní cache. Opětovné použití jediné instance napříč mnoha obrázky může skutečně **zrychlit OCR**, protože knihovna se vyhne opakované nativní inicializaci.

```java
import com.aspose.ocr.*;

public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialise the OCR engine – one instance per application is ideal
        OcrEngine ocrEngine = new OcrEngine();
```

---

## Krok 3 – **Načíst obrázek pro OCR**  

Aspose podporuje mnoho formátů obrázků (PNG, JPEG, TIFF, BMP). Zde ukazujeme načtení PNG, který obsahuje text v angličtině, ruštině a hindštině. Pomocník `ImageStream.fromFile` abstrahuje detaily souborového I/O a zajistí, že obrázek je správně streamován do engine.

```java
        // Step 3: Load the picture that holds mixed languages
        // Replace the path with the actual location of your image file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));
```

> **Co když je obrázek v paměti?** Použijte `ImageStream.fromByteArray(byte[])` – ideální pro webové služby, které přijímají obrázky jako bytové proudy.

---

## Krok 4 – Povolení automatického rozpoznávání jazyka  

Ve výchozím nastavení předpokládá Aspose OCR jeden jazyk, což může vést k nečitelnému výstupu u vícejazykových obrázků. Zapnutí automatického rozpoznávání řekne engine, aby před rozpoznáním „vyčichl“ skript každého textového bloku.

```java
        // Step 4: Turn on auto‑detect – this is the key to handling mixed‑language images
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

---

## Krok 5 – **Zrychlit OCR** omezením sady jazyků  

Úplná automatická detekce prohledává všechny jazyky, které Aspose podporuje (více než 70). Pokud znáte možné jazyky dopředu, můžete engine poskytnout nápovědu. Menší pole jazyků zmenšuje vyhledávací prostor a tím **zrychluje OCR**.

```java
        // Step 5 (optional but recommended): Limit detection to known languages
        // "en" = English, "ru" = Russian, "hi" = Hindi
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });
```

> **Proč to pomáhá?** Engine přeskočí jazykové modely, které nepotřebuje, čímž šetří CPU cykly a paměť. Pokud později přidáte další jazyky, stačí pole aktualizovat — žádná úprava kódu není nutná.

---

## Krok 6 – Proveďte rozpoznání a **rozpoznat text z obrázku**

Nyní se děje těžká práce. `recognize()` vrací objekt `OcrResult`, který obsahuje čistý text, skóre důvěry a dokonce i informace o rozložení, pokud je budete potřebovat později.

```java
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 7: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Očekávaný výstup v konzoli

```
=== Extracted Text ===
Hello world!
Привет мир!
नमस्ते दुनिया!
```

Pokud obrázek obsahuje další šum nebo nakřivený text, můžete u těchto řádků vidět nižší důvěru. V takovém případě zvažte předzpracování obrázku (odklon, binarizaci) před předáním Aspose.

---

## Časté otázky a okrajové případy

### Co když je obrázek obrovský (např. >10 MP)?

Velké obrázky spotřebují více paměti a mohou zpomalit zpracování. Rychlý způsob, jak **zrychlit OCR**, je zmenšit rozlišení obrázku při zachování čitelnosti:

```java
// Example using java.awt for simple resizing (optional)
BufferedImage original = ImageIO.read(new File("large.png"));
int targetWidth = 2000; // adjust based on your needs
BufferedImage resized = new BufferedImage(targetWidth,
        (original.getHeight() * targetWidth) / original.getWidth(),
        BufferedImage.TYPE_INT_RGB);
Graphics2D g = resized.createGraphics();
g.drawImage(original, 0, 0, targetWidth, resized.getHeight(), null);
g.dispose();
ocrEngine.setImage(ImageStream.fromImage(resized));
```

### Jak zacházet se skripty zprava doleva, jako je arabština?

Aspose OCR automaticky respektuje směr skriptu, ale můžete chtít nastavit příznak `RightToLeft` pro následné zpracování:

```java
ocrEngine.getSettings().setRightToLeft(true);
```

### Můžu extrahovat text z PDF místo obrázků?

Ano — převod každé stránky PDF na obrázek (pomocí Aspose PDF nebo libovolného rasterizéru) a předání výsledku do stejného OCR pipeline. Stejná logika **rozpoznat text z obrázku** se použije.

---

## Kompletní funkční příklad (připravený ke zkopírování)

```java
import com.aspose.ocr.*;
import java.io.File;

/**
 * Demonstrates how to use Aspose OCR to recognize text from an image
 * that contains multiple languages, with automatic language detection
 * and a speed‑optimising language whitelist.
 */
public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine – reuse this instance for many images
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that holds mixed languages (replace with your path)
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));

        // Enable automatic detection of language per text block
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // OPTIONAL: Restrict detection to English, Russian, and Hindi to boost speed
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });

        // Run OCR and capture the result
        OcrResult ocrResult = ocrEngine.recognize();

        // Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Uložte soubor jako `MixedLanguageDemo.java`, zkompilujte pomocí `javac` a spusťte pomocí `java MixedLanguageDemo`. Pokud je vše nastaveno správně, uvidíte v konzoli vytištěný vícejazykový text.

---

## Závěr

Nyní víte **jak používat Aspose** k **rozpoznání textu z obrázku** souborů, které obsahují několik jazyků, jak **povolit automatické rozpoznávání jazyka** a praktický tip, jak **zrychlit OCR** omezením sady jazyků. Výše uvedený kód je připravený ke zkopírování a vysvětlení by vám měla dodat jistotu při úpravě řešení — ať už potřebujete **načíst obrázek pro OCR** ze streamu, bytového pole nebo dokonce ze snímku webkamery.

Další kroky? Vyzkoušejte:

* Přidání předzpracování obrázku (odšumění, binarizace) pro skeny nízké kvality.  
* Export `OcrResult` jako JSON pro downstream služby.  
* Integraci engine do REST endpointu Spring Boot, aby klienti mohli nahrávat obrázky a okamžitě získávat extrahovaný text.

Šťastné programování a ať jsou vaše OCR pipeline rychlé, přesné a vícejazykové!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}