---
category: general
date: 2026-02-14
description: Naučte se, jak provádět OCR na obrázku a extrahovat text z obrázku pomocí
  Aspose OCR v Javě. Zahrnuje načítání obrázku pro OCR, vlastní slovník a opravu pravopisu.
draft: false
keywords:
- perform OCR on image
- extract text from image
- load image for OCR
- Aspose OCR Java
- spell correction OCR
language: cs
og_description: Proveďte OCR na obrázku v Javě s Aspose OCR. Tento průvodce ukazuje,
  jak načíst obrázek pro OCR, extrahovat text z obrázku a povolit opravu pravopisu.
og_title: Proveďte OCR na obrázku – Kompletní Java tutoriál
tags:
- OCR
- Java
- Aspose
title: Proveďte OCR na obrázku pomocí Aspose OCR – Java krok za krokem průvodce
url: /cs/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Provádění OCR na obrázku – Kompletní Java tutoriál

Už jste někdy potřebovali **provádět OCR na obrázku** soubory, ale nebyli jste si jisti, kde začít? Nejste v tom sami; mnoho vývojářů narazí na stejnou překážku, když poprvé zkusí extrahovat text z obrazových dat. Dobrou zprávou je, že s Aspose OCR pro Java můžete získat spolehlivé výsledky během několika řádků kódu – a navíc můžete zvýšit přesnost pomocí vlastního slovníku a kontroly pravopisu.

V tomto průvodci vás provedeme vším, co potřebujete vědět: od načtení obrázku pro OCR, přes povolení opravy pravopisu, až po vytištění vyčištěného textu. Na konci budete schopni **provádět OCR na obrázku** v rámci svých Java projektů a také uvidíte, jak **extrahovat text z obrázku** souborů způsobem, který funguje i u špinavých skenů.

## Co budete potřebovat

- **Java Development Kit (JDK) 8+** – kód používá standardní Java API.
- **Aspose OCR for Java** knihovna (můžete stáhnout nejnovější JAR z webu Aspose nebo Maven Central).
- Soubor s obrázkem (např. `invoice.png`), který chcete zpracovat.
- (Volitelně) Textový soubor `custom_dict.txt` obsahující doménově specifická slova, jedno na řádek.

To je vše—žádné těžkopádné frameworky, žádné externí služby. Pouze čistá Java a Aspose OCR JAR.

## Krok 1: Nastavení projektu a import závislostí

Nejprve vytvořte nový Maven (nebo Gradle) projekt a přidejte závislost Aspose OCR. Pokud používáte Maven, váš `pom.xml` by měl obsahovat:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

Pokud raději stáhnete JAR ručně, vložte jej do složky `libs` a přidejte jej do classpath.

> **Tip:** Vždy ověřte číslo verze v době psaní; novější vydání mohou přinést další funkce, jako jsou jazykové balíčky.

## Krok 2: Načtení obrázku pro OCR

Prvním skutečným krokem kódu je nasměrovat OCR engine na obrázek, který chcete analyzovat. Aspose OCR používá obal `ImageStream`, který může číst ze souboru, pole bajtů nebo dokonce z URL.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you wish to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

Všimněte si, jak **načítáme obrázek pro OCR** jedním voláním metody—žádné složité cvičení s `BufferedImage` nejsou potřeba. Pokud je váš obrázek v resources, stačí nahradit cestu za `getClass().getResourceAsStream(...)`.

## Krok 3: Povolení opravy pravopisu (volitelné, ale výkonné)

Aspose OCR může automaticky opravit běžné OCR chyby (např. „l“ vs „1“). Zapnutí této funkce je tak jednoduché jako přepnutí příznaku:

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

Proč to dělat? Představte si skenování tištěné faktury, kde je písmo malé a skener přidává drobné šmouhy. Oprava pravopisu často změní „Inv0ice“ zpět na „Invoice“ bez dalšího úsilí z vaší strany.

## Krok 4: Poskytnutí vlastního slovníku (přizpůsobení engine)

Pokud pracujete s oborově specifickou terminologií—např. medicínské kódy, právnický žargon nebo produktové SKU—vlastní slovník může dramaticky zlepšit přesnost. Slovník je jen textový soubor s jedním slovem na řádku.

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

Ujistěte se, že soubor používá kódování UTF‑8; jinak můžete vidět poškozené znaky u ne‑ASCII slov.

## Krok 5: Spuštění OCR procesu

Nyní konečně necháme engine udělat své kouzlo. Volání `process()` vrací objekt `OcrResult`, který obsahuje rozpoznaný text, skóre důvěry a dokonce i rozložení, pokud jej později potřebujete.

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

Pokud se někdy zamyslíte, zda engine vyhodil výjimku, zabalte toto volání do try‑catch bloku a podívejte se na `ocrResult.getErrorMessage()` pro podrobnosti.

## Krok 6: Výstup rozpoznaného (a opraveného) textu

Posledním krokem je zobrazit—nebo uložit—extrahovaný řetězec. Pro rychlou ukázku jej jednoduše vypíšeme do konzole:

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

Spuštění programu by mělo vypsat něco jako:

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

Pokud vidíte cizí znaky, zkontrolujte svůj vlastní slovník a zvažte úpravu kvality obrázku (např. zvýšení kontrastu před předáním engine).

### Kompletní funkční příklad

Spojením všeho dohromady, zde je kompletní, připravená ke spuštění třída:

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you wish to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));

        // Step 3: Enable spell‑checking for the OCR result
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);

        // Step 4: Provide a custom dictionary (one word per line)
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));

        // Step 5: Run the OCR process
        OcrResult ocrResult = ocrEngine.process();

        // Step 6: Output the recognized (and corrected) text
        System.out.println(ocrResult.getText());
    }
}
```

Uložte tento soubor jako `SpellCorrectDemo.java`, upravte cesty, zkompilujte pomocí `javac` a spusťte pomocí `java SpellCorrectDemo`. Nyní byste měli **provádět OCR na obrázku** soubory a vidět vytištěný extrahovaný text.

## Často kladené otázky a okrajové případy

### Co když je obrázek v jiném formátu (PDF, TIFF, atd.)?

Aspose OCR dokáže zpracovat mnoho rastrových formátů přímo. Pro PDF budete muset nejprve extrahovat každou stránku jako obrázek—Aspose PDF pro Java to provádí dobře. Stejné volání `setImage` funguje, jakmile máte `BufferedImage` nebo bajtový stream.

### Jak zvládnout vícestránkové dokumenty?

Procházejte každým obrázkem stránky, spusťte OCR kroky a spojte výsledky. Nezapomeňte resetovat nebo vytvořit nový `OcrEngine` pro každou stránku, pokud chcete nezávislé kontexty kontroly pravopisu.

### Můžu omezit jazyk nebo znakovou sadu?

Ano. Použijte `ocrEngine.getEngineOptions().setLanguage(Language.English);` (nebo jakýkoli jiný podporovaný jazyk) ke snížení falešných pozitiv a zrychlení zpracování.

### Co výkon při velkých dávkách?

Aspose OCR je thread‑safe pro operace jen pro čtení. Můžete vytvořit thread pool a zpracovávat obrázky souběžně—jen se vyhněte sdílení stejné instance `OcrEngine` mezi vlákny.

## Tipy pro vyšší přesnost

- **Předzpracování obrázku**: zvýšení kontrastu, odstranění šumu na pozadí nebo převod na odstíny šedi.
- **Použijte sken s vysokým rozlišením** (300 dpi nebo vyšší). Nižší rozlišení často vede k poškozeným znakům.
- **Udržujte vlastní slovník úsporný**: příliš mnoho nesouvisejících slov může zmást kontrolu pravopisu.
- **Ověřte výstup**: pokud znáte očekávaný formát (např. data, čísla), spusťte regex post‑processing pro zachycení anomálií.

## Další kroky

Nyní, když můžete **provádět OCR na obrázku** soubory a **extrahovat text z obrázku** pomocí Aspose OCR, můžete chtít prozkoumat:

- **Ukládání výstupu OCR do PDF** s vyhledávatelnými textovými vrstvami.
- **Integrace s databází** pro automatické ukládání extrahovaných fakturačních dat.
- **Použití strojového učení v post‑processingu** pro ještě vyšší přesnost u ručně psaných poznámek.
- **Použití příznaku `load image for OCR`** ve webové službě, která přijímá obrázky nahrané uživateli.

Každé z těchto témat staví na základních krocích, které jsme pokryli, takže přechod bude plynulý.

*Šťastné programování! Pokud narazíte na problémy, neváhejte zanechat komentář—nic nepřekoná učení se z reálných příkladů.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}