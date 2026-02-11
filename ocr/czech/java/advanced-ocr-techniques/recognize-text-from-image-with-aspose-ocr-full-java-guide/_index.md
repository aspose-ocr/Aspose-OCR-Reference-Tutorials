---
category: general
date: 2026-02-09
description: Naučte se rozpoznávat text z obrázku pomocí Aspose OCR v Javě. Tento
  krok‑za‑krokem tutoriál také pokrývá kontrolu pravopisu, vlastní slovníky a konfiguraci
  OCR enginu.
draft: false
keywords:
- recognize text from image
- Aspose OCR Java
- OCR spell checking
- custom OCR dictionary
- Java image processing
language: cs
og_description: Rozpoznávejte text z obrázku v Javě pomocí Aspose OCR. Postupujte
  podle tohoto návodu, abyste povolili kontrolu pravopisu, nastavili jazyk a okamžitě
  získali opravený výstup.
og_title: Rozpoznání textu z obrázku pomocí Aspose OCR – Kompletní Java tutoriál
tags:
- OCR
- Java
- Aspose
title: Rozpoznání textu z obrázku pomocí Aspose OCR – Kompletní Java průvodce
url: /cs/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/
---

ocr-workflow.png "recognize text from image workflow")

Translate alt: "Diagram ukazující OCR workflow pro rozpoznání textu z obrázku". Title: "workflow rozpoznání textu z obrázku". Keep URL same.

Now closing shortcodes.

We must ensure we keep all shortcodes exactly as original.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rozpoznání textu z obrázku – kompletní Java tutoriál

Už jste někdy potřebovali **rozpoznat text z obrázku**, ale nebyli jste si jisti, kterou API použít? Nejste v tom sami. V mnoha projektech—skenování faktur, digitalizace ručně psaných poznámek nebo tvorba prohledávatelného archivu—schopnost získat čistý, čitelný text z obrázku je revoluční.  

Dobrá zpráva? S Aspose OCR pro Java to můžete udělat během několika řádků a navíc získáte vestavěnou kontrolu pravopisu pro vyčištění výstupu OCR. V tomto tutoriálu projdeme celý proces, od vytvoření OCR enginu až po vytištění opraveného výsledku. Na konci budete mít připravenou Java třídu, která **spolehlivě rozpozná text z obrázku**.

---

## Co budete potřebovat

- **Java 8+** (kód funguje s jakýmkoli aktuálním JDK)
- **Aspose OCR for Java** knihovna – můžete získat nejnovější JAR z Aspose Maven repozitáře nebo jej stáhnout přímo z webu Aspose.
- Obrázkový soubor obsahující psaný nebo tištěný text (např. `typed_scanned_doc.png`).
- Rozumné množství RAM; OCR není náročné, ale 1 GB heap je více než dostatečné pro většinu skenů.

> *Tip:* Pokud používáte Maven, přidejte následující závislost do vašeho `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Nyní, když jsou předpoklady vyřešeny, pojďme se ponořit do kódu.

## Krok 1: Inicializace OCR enginu a získání jeho konfigurace

Prvním krokem je vytvořit instanci `OcrEngine`. Tento objekt je srdcem knihovny; obsahuje všechna nastavení, která budete později upravovat.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class SpellCheckExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and obtain its configuration object
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration ocrConfig = ocrEngine.getConfiguration();
```

Proč je to důležité: Objekt konfigurace vám poskytuje přímý přístup k výběru jazyka, příznakům kontroly pravopisu a cestám ke slovníkům. Bez něj byste byli omezeni na výchozí nastavení, která nemusí odpovídat vašemu zdrojovému materiálu.

## Krok 2: Výběr jazyka a zapnutí kontroly pravopisu

Dále řekněte enginu, jaký jazyk očekáváte na obrázku. Zde volíme angličtinu, ale Aspose podporuje desítky jazykových nastavení.

```java
        // Step 2: Choose the language for recognition and turn on spell‑checking
        ocrConfig.setLanguage(Language.ENGLISH);
        ocrConfig.setSpellCheckEnabled(true);
```

Zapnutí kontroly pravopisu je volitelné, ale výrazně zlepšuje čitelnost výstupu—zejména u skenovaných dokumentů, kde OCR engine může zaměnit „0“ za „O“.

## Krok 3: (Volitelné) Načtení vlastního slovníku pro kontrolu pravopisu

Pokud pracujete s oborovým žargonem—např. medicínskými termíny, právními zkratkami nebo vlastními kódy produktů—Aspose vám umožní připojit vlastní slovník.

```java
        // Step 3: (Optional) Provide a custom spell‑check dictionary
        ocrConfig.setSpellCheckDictionary("en_US"); // use a locale‑specific dictionary
```

Můžete také nastavit `setSpellCheckDictionary` na soubor `.dic` s úplnou cestou, pokud máte vlastní seznam. Engine sloučí vaše vlastní slova s vestavěným slovníkem, čímž zajistí, že oborová slovní zásoba zůstane zachována.

## Krok 4: Spuštění OCR na vašem obrázkovém souboru

Nyní začíná skutečná práce. Zadejte cestu k vašemu obrázku a nechte engine udělat své kouzlo.

```java
        // Step 4: Run OCR on the input image file
        RecognitionResult recognitionResult = ocrEngine.recognize("YOUR_DIRECTORY/typed_scanned_doc.png");
```

Za scénou Aspose provádí sérii předzpracovatelských kroků—odklonování, binarizaci a segmentaci znaků—před předáním pixelových dat svému neuronovému rozpoznávači. Výsledek je zabalen do objektu `RecognitionResult`, který obsahuje jak surový, tak opravený text.

## Krok 5: Zobrazení opraveného textu

Nakonec vytiskněte vyčištěný řetězec do konzole. Uvidíte výstup OCR **s aplikovanou kontrolou pravopisu**, který je často připraven k přímému uložení do databáze nebo vložení do vyhledávacího indexu.

```java
        // Step 5: Display the corrected text returned by the engine
        System.out.println("Corrected text:");
        System.out.println(recognitionResult.getText());
    }
}
```

### Očekávaný výstup

Předpokládejme, že `typed_scanned_doc.png` obsahuje větu *„The quick brown fox jumps over the lazy dog.“*, konzole zobrazí:

```
Corrected text:
The quick brown fox jumps over the lazy dog.
```

Pokud by původní sken měl skvrnu, která změnila „quick“ na „qu1ck“, kontrola pravopisu by ji automaticky opravila zpět na „quick“.

## Řešení běžných okrajových případů

### 1. Nízké rozlišení obrázků

Přesnost OCR výrazně klesá pod 150 dpi. Pokud jsou vaše zdrojové obrázky nízkého rozlišení, zvažte jejich nejprve zvětšení (např. pomocí OpenCV) nebo požádejte o sken vyšší kvality.  

### 2. Vícejazyčné dokumenty

Aspose OCR může měnit jazyky za běhu, ale musíte nastavit odpovídající `Language` enum před každým voláním `recognize`. Pro stránky s více jazyky může být nutné spustit obrázek přes engine dvakrát—jednou pro každý jazyk—a poté sloučit výsledky.

### 3. Velké PDF nebo vícestránkové TIFFy

Pokud potřebujete **rozpoznat text z obrázku** souborů vložených v PDF, extrahujte každou stránku jako obrázek (pomocí Aspose PDF nebo jiné knihovny) a předávejte je jednotlivě OCR engine. Engine je bezstavový, takže můžete znovu použít stejnou instanci `OcrEngine` napříč stránkami.

### 4. Přizpůsobení citlivosti kontroly pravopisu

Výchozí práh kontroly pravopisu funguje pro většinu anglických textů. Pro vysoce technické dokumenty můžete snížit citlivost úpravou interního `SpellCheckOptions`—i když to vyžaduje ponoření se do pokročilého API Aspose, což přesahuje rámec tohoto úvodního průvodce.

## Kompletní funkční příklad (připravený ke kopírování a vložení)

Níže je kompletní Java třída, připravená ke kompilaci a spuštění. Nahraďte `YOUR_DIRECTORY/typed_scanned_doc.png` skutečnou cestou k vašemu obrázku.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class SpellCheckExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and obtain its configuration object
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration ocrConfig = ocrEngine.getConfiguration();

        // Step 2: Choose the language for recognition and turn on spell‑checking
        ocrConfig.setLanguage(Language.ENGLISH);
        ocrConfig.setSpellCheckEnabled(true);

        // Step 3: (Optional) Provide a custom spell‑check dictionary
        ocrConfig.setSpellCheckDictionary("en_US"); // or a full path to your .dic file

        // Step 4: Run OCR on the input image file
        RecognitionResult recognitionResult = ocrEngine.recognize("YOUR_DIRECTORY/typed_scanned_doc.png");

        // Step 5: Display the corrected text returned by the engine
        System.out.println("Corrected text:");
        System.out.println(recognitionResult.getText());
    }
}
```

Zkompilujte pomocí:

```bash
javac -cp "path/to/aspose-ocr.jar" SpellCheckExample.java
java -cp ".;path/to/aspose-ocr.jar" SpellCheckExample
```

Měli byste vidět opravený text vytištěný do konzole, což potvrzuje, že jste úspěšně **rozpoznali text z obrázku** a aplikovali kontrolu pravopisu.

## Často kladené otázky

**Q: Podporuje Aspose OCR ruční psaní?**  
A: Knihovna je optimalizována pro tištěný text. Rozpoznávání ručně psaného textu je k dispozici v samostatném modulu (`aspose-ocr-handwriting`), který můžete integrovat podobně.

**Q: Mohu zpracovávat obrázky z URL místo lokálního souboru?**  
A: Ano. Stáhněte obrázek do dočasného bufferu (např. pomocí `java.net.URL`) a předávejte pole bajtů do `ocrEngine.recognize(InputStream)`.

**Q: Co když potřebuji extrahovat jen konkrétní oblasti obrázku?**  
A: Použijte `ocrEngine.setRegion(Rectangle)` před voláním `recognize`. Tím omezíte OCR na definovaný obdélník, ušetříte čas a snížíte počet falešných pozitiv.

## Závěr

Právě jsme prošli kompletním, end‑to‑end příkladem, jak **rozpoznat text z obrázku** pomocí Aspose OCR pro Java. Konfigurací OCR enginu, zapnutím kontroly pravopisu a volitelným načtením vlastního slovníku můžete převést špinavé skeny na čistý, prohledávatelný text s minimálním množstvím kódu.

Od tady můžete zkoumat:

- **Dávkové zpracování** – procházet složku s obrázky a ukládat každý výsledek do databáze.  
- **Integraci s Aspose PDF** – extrahovat obrázky z PDF a předávat je OCR engine.  
- **Pokročilou podporu jazyků** – přepnout `ocrConfig.setLanguage` na `Language.FRENCH` nebo `Language.SPANISH` pro vícejazyčné projekty.  

Vyzkoušejte to, dolaďte nastavení a uvidíte, jak se kvalita zlepší pro váš konkrétní případ použití. Šťastné programování a ať jsou vaše skeny vždy ostré!  

![Diagram ukazující OCR workflow pro rozpoznání textu z obrázku](/images/ocr-workflow.png "workflow rozpoznání textu z obrázku")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}