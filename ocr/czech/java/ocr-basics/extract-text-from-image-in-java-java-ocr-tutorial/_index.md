---
category: general
date: 2026-03-07
description: Extrahujte text z obrázku pomocí Java OCR. Naučte se, jak načíst obrázek
  pro OCR, nastavit jazyk a spustit kompletní Java OCR tutoriál během několika minut.
draft: false
keywords:
- extract text from image
- load image for ocr
- use OCR in java
- java ocr tutorial
language: cs
og_description: Extrahujte text z obrázku pomocí Java OCR. Tento tutoriál ukazuje,
  jak načíst obrázek pro OCR, nastavit jazyk a provést Java OCR tutoriál krok za krokem.
og_title: Extrahování textu z obrázku v Javě – Kompletní průvodce OCR
tags:
- OCR
- Java
- Image Processing
title: Extrahování textu z obrázku v Javě – Java OCR tutoriál
url: /cs/java/ocr-basics/extract-text-from-image-in-java-java-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat text z obrázku v Javě – Kompletní průvodce OCR

Už jste někdy potřebovali **extrahovat text z obrázku**, ale nebyli jste si jisti, kde v Javě začít? Nejste v tom sami — vývojáři často narazí na tento problém při převodu naskenovaných značek, účtenek nebo ručně psaných poznámek na prohledávatelné řetězce.  

Dobrá zpráva? Za pár minut můžete mít funkční OCR pipeline, která čte kannadštinu, angličtinu nebo jakýkoli podporovaný jazyk. V tomto tutoriálu **načteme obrázek pro OCR**, nakonfigurujeme engine a projdeme **Java OCR tutoriál**, který můžete dnes zkopírovat a spustit.

## Co tento průvodce pokrývá

Začneme výpisem nástrojů, které budete potřebovat, a poté se ponoříme přímo do **krok‑za‑krokem** implementace. Na konci budete schopni:

* Načíst soubor obrázku do Java `ImageInputStream`.
* Nakonfigurovat OCR engine tak, aby rozpoznával konkrétní jazyk (Kannada v našem příkladu).
* Spustit proces rozpoznávání a vypsat extrahovaný text.
* Doladit nastavení pro vyšší přesnost a řešit běžné úskalí.

Žádná externí dokumentace není potřeba — vše, co potřebujete, je zde.  

**Požadavky**: Java 17 nebo novější, nástroj pro sestavení jako Maven nebo Gradle a OCR knihovna, která poskytuje třídu `OcrEngine` (například hypotetické *SimpleOCR* SDK). Pokud používáte Maven, přidejte závislost uvedenou níže.

---

## Krok 1 – Nastavte svůj projekt a přidejte OCR knihovnu

Než napíšeme jakýkoli kód, ujistěte se, že váš projekt vidí OCR třídy. S Mavenem vložte tento úryvek do vašeho `pom.xml`:

```xml
<!-- Maven dependency for SimpleOCR (replace with your actual OCR SDK) -->
<dependency>
    <groupId>com.example</groupId>
    <artifactId>simple-ocr</artifactId>
    <version>1.4.2</version>
</dependency>
```

Pokud dáváte přednost Gradlu, ekvivalent je:

```gradle
implementation 'com.example:simple-ocr:1.4.2'
```

> **Tip:** Udržujte verzi knihovny aktuální; novější verze často obsahují vylepšení jazykových modelů, která zvyšují přesnost.

Jakmile se závislost vyřeší, obnovte své IDE a můžete začít kódovat.

## Krok 2 – Importujte požadované třídy

Níže je úplný seznam importů, které budete v příkladu potřebovat. Jsou úmyslně minimalizovány, aby bylo jasné, co každá třída dělá.

```java
import com.example.ocr.OcrEngine;      // Main OCR engine
import com.example.ocr.OcrResult;      // Holds recognition result
import com.example.io.ImageInputStream; // Wrapper for image files
import java.nio.file.Paths;             // Convenient path handling
import java.io.IOException;             // For proper exception handling
```

> **Proč tyto importy?** `OcrEngine` a `OcrResult` jsou srdcem OCR procesu, zatímco `ImageInputStream` abstrahuje boilerplate pro čtení souborů. Použití `java.nio.file.Paths` dělá kód OS‑agnostickým.

## Krok 3 – Načtěte obrázek pro OCR

Nyní přichází část, která lidi často zaskočí: předání správného formátu obrázku engine. OCR SDK očekává `ImageInputStream`, který můžete získat z libovolného souboru na disku.

```java
// Step 3: Load the image that contains the text you want to extract
String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));
```

> **Hraniční případ:** Pokud je obrázek poškozený nebo v nepodporovaném formátu (např. GIF), konstruktor vyhodí `IOException`. Zabalte volání do try‑catch bloku nebo soubor předem ověřte.

## Krok 4 – Nakonfigurujte engine pro rozpoznání konkrétního jazyka

Většina OCR engineů nabízí podporu více jazyků. Pro zlepšení přesnosti byste měli engine přesně říct, který jazyk má hledat. V našem případě používáme kód jazyka `"kn"` pro kannadštinu.

```java
// Step 4: Create and configure the OCR engine for Kannada
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getConfig().setLanguage("kn"); // 'kn' = Kannada
```

> **Proč nastavit jazyk?** Omezení sady znaků snižuje falešně pozitivní výsledky, zejména u skriptů s mnoha podobnými glyfy.

Pokud budete potřebovat změnit jazyk, stačí změnit řetězec kódu — žádné další úpravy nejsou potřeba.

## Krok 5 – Spusťte OCR proces a extrahujte text

S načteným obrázkem a nakonfigurovaným engine je samotné rozpoznání jedním voláním metody. Objekt výsledku vám poskytne čistý text a volitelně skóre důvěry.

```java
// Step 5: Run OCR and retrieve the recognized text
OcrResult ocrResult = ocrEngine.recognize(imageStream);
String extractedText = ocrResult.getText();
```

> **Často kladená otázka:** *Co když OCR vrátí prázdný řetězec?*  
> Obvykle to znamená, že kvalita obrázku je příliš nízká (rozmazání, nízký kontrast) nebo jazyk nebyl nastaven správně. Zkuste předzpracovat obrázek (zvýšit kontrast, binarizovat) nebo dvojitě zkontrolovat kód jazyka.

## Krok 6 – Zobrazte výsledek

Nakonec vytiskněte výstup do konzole. Ve skutečné aplikaci jej můžete uložit do databáze nebo předat do vyhledávacího indexu.

```java
// Step 6: Output the recognized Kannada text
System.out.println("Extracted text:");
System.out.println(extractedText);
```

### Očekávaný výstup

Pokud zdrojový obrázek obsahuje kannadskou frázi “ಕರ್ನಾಟಕ” (Karnataka), konzole by měla zobrazit:

```
Extracted text:
ಕರ್ನಾಟಕ
```

A to je vše — kompletní workflow **použití OCR v Javě**, který můžete přizpůsobit libovolnému jazyku nebo zdroji obrázku.

---

## Kompletní funkční příklad

Níže je celý program připravený ke kompilaci. Nahraďte `YOUR_DIRECTORY` skutečnou cestou k vašemu souboru obrázku.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrResult;
import com.example.io.ImageInputStream;
import java.nio.file.Paths;
import java.io.IOException;

public class KannadaOcrExample {
    public static void main(String[] args) {
        try {
            // Create OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Configure for Kannada (language code "kn")
            ocrEngine.getConfig().setLanguage("kn");

            // Load the image you want to extract text from
            String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
            ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));

            // Run the OCR process
            OcrResult ocrResult = ocrEngine.recognize(imageStream);

            // Print the extracted text
            System.out.println("Extracted text:");
            System.out.println(ocrResult.getText());
        } catch (IOException e) {
            System.err.println("Failed to load image or run OCR: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Unexpected error during OCR: " + e.getMessage());
        }
    }
}
```

> **Tip:** Pro produkční kód zvažte opětovné použití jediné instance `OcrEngine` napříč více obrázky; opakované vytváření může být nákladné.

---

## Často kladené otázky a hraniční případy

### Jak zlepšit přesnost u špinavých fotografií?

- **Předzpracujte** obrázek: převést na odstíny šedi, aplikovat mediánové filtrování nebo zvýšit kontrast.
- **Změňte velikost** obrázku na alespoň 300 DPI; většina OCR engineů očekává toto rozlišení.
- **Nastavte whitelist** znaků, pokud znáte očekávaný výstup (např. jen číslice).

### Můžu tento přístup použít pro PDF?

Ano. Extrahujte každou stránku jako obrázek (pomocí PDFBox nebo iText) a pak tyto obrázky předáte do stejné pipeline. Kód zůstává stejný; mění se jen zdroj obrázku.

### Co když potřebuji rozpoznat více jazyků na jednom obrázku?

Většina SDK umožňuje předat seznam oddělený čárkou, např. `"en,kn"`. Engine se pokusí odpovídat kterémukoli ze zadaných skriptů.

### Existuje způsob, jak získat skóre důvěry?

`OcrResult` často obsahuje metodu `getConfidence()`, která vrací float mezi 0 a 1 pro každou řádku. Použijte ji k filtrování výsledků s nízkou důvěrou.

---

## Další kroky

Nyní, když můžete **extrahovat text z obrázku** pomocí Javy, můžete zkoumat:

- **Dávkové zpracování** – procházet složku s obrázky a zapisovat výsledky do CSV.
- **Integrace s Apache Tika** – kombinovat OCR s parsováním dokumentů pro jednotný vyhledávací index.
- **Server‑side API** – vystavit OCR logiku přes REST endpoint (Spring Boot to umožňuje snadno).
- **Alternativní knihovny** – vyzkoušejte Tesseract přes `tess4j`, pokud potřebujete open‑source řešení.

Každé z těchto témat staví na základních konceptech pokrytých v tomto **java ocr tutoriálu**, takže klidně experimentujte a rozšiřujte kód.

---

## Závěr

Prošli jsme kompletním Java příkladem, který **extrahuje text z obrázku**, a ukázali přesně, jak **načíst obrázek pro OCR**, nakonfigurovat nastavení jazyka a **použít OCR v Javě** k získání čitelných řetězců. Útržek je samostatný, elegantně ošetřuje chyby a lze jej vložit do libovolného Java projektu s minimálním úsilím.  

Vyzkoušejte jej, upravte kód jazyka a brzy budete převádět naskenované dokumenty na prohledávatelná data bez námahy. Šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}