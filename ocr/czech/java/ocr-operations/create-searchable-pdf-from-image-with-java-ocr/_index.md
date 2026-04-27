---
category: general
date: 2026-04-26
description: Vytvořte prohledávatelný PDF z obrázku pomocí Aspose OCR v Javě. Naučte
  se převést obrázek na PDF, provést OCR obrázku do PDF a rychle extrahovat text z
  obrázku.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- extract text from image
- how to set language
language: cs
og_description: Vytvořte prohledávatelný PDF z obrázku pomocí Aspose OCR. Tento průvodce
  ukazuje, jak převést obrázek na PDF, provést OCR obrázku do PDF a extrahovat text
  z obrázku.
og_title: Vytvořte prohledávatelný PDF z obrázku pomocí Java OCR
tags:
- Java
- OCR
- PDF
title: Vytvořit prohledávatelný PDF z obrázku pomocí Java OCR
url: /cs/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF z obrázku pomocí Java OCR

Už jste někdy potřebovali **vytvořit prohledávatelný PDF** ze skenované faktury, ale nevedeli jste, kde začít? Nejste v tom sami — mnoho vývojářů narazí na tento problém, když chtějí mít PDF, které lze skutečně prohledávat. Dobrá zpráva? S Aspose OCR pro Java můžete **převést obrázek na PDF**, spustit OCR za běhu a získat úhledný prohledávatelný soubor během několika řádků kódu.

V tomto tutoriálu projdeme celý proces: načtení obrázku, nastavení jazyka, provedení OCR a nakonec uložení **prohledávatelného PDF**. Na konci budete také vědět, jak **extrahovat text z obrázku** ručně, upravit nastavení jazyka a řešit několik běžných okrajových případů. Žádné externí služby, žádné neznámé nástroje z příkazové řádky — pouze čistá Java.

## Co budete potřebovat

- Java 17 nebo novější (API funguje i se staršími verzemi, ale 17 je optimální).  
- Knihovna Aspose OCR pro Java — nejnovější JAR můžete stáhnout z Maven Central (`com.aspose:aspose-ocr:23.10`).  
- Soubor s obrázkem, který obsahuje čitelný text (PNG, JPG nebo TIFF).  
- Trochu trpělivosti v IDE — IntelliJ IDEA nebo VS Code postačí.

Pokud už máte vše připravené, skvělé! Pokud ne, následující Maven snippet vás dostane do chodu:

```xml
<!-- Add to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Nyní, když je základ připraven, ponořme se do kódu.

## Krok 1: Inicializace OCR enginu — srdce **create searchable pdf**

Než začne jakákoli konverze, musíte vytvořit instanci `OcrEngine`. Představte si ji jako mozek, který přečte pixely a převádí je na znaky.

```java
import com.aspose.ocr.*;

public class PdfExportDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

*Proč je to důležité:* Engine uchovává všechna nastavení rozpoznávání (jazyk, režim přesnosti atd.). Vytvořit jej jednou a znovu použít pro více obrázků je efektivnější než vytvářet nový engine pro každý soubor.

## Krok 2: **How to set language** — zlepšete přesnost pro francouzštinu, němčinu nebo jakýkoli skript

Pokud znáte jazyk zdrojového dokumentu, nastavte jej v OCR enginu. Tím se zrychlí zpracování a sníží se chybovost.

```java
        // Step 2: (Optional) Specify the language to improve text extraction
        ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.FRENCH);
```

Můžete nahradit `OcrLanguage.FRENCH` za `ENGLISH`, `SPANISH`, `GERMAN` atd. Pokud si nejste jisti, řádek vynechte a nechte Aspose hádat — očekávejte mírný pokles přesnosti.

## Krok 3: Načtěte obrázek, který chcete **convert image to pdf**

```java
        // Step 3: Load the image that contains the text to be recognized
        ocrEngine.setImage("YOUR_DIRECTORY/french_invoice.png");
```

Metoda `setImage` přijímá cestu k souboru, `InputStream` nebo dokonce objekt `java.awt.Image`. Pokud máte pole bajtů (např. z webového uploadu), zabalte jej do `ByteArrayInputStream` a předávejte přímo.

## Krok 4: Proveďte OCR a **ocr image to pdf** v jednom volání

Aspose tento krok zjednodušuje: `recognizeToPdf` spustí rozpoznávací engine a zapíše prohledávatelný PDF najednou.

```java
        // Step 4: Recognize the text and save it as a searchable PDF
        ocrEngine.recognizeToPdf("YOUR_DIRECTORY/french_invoice_searchable.pdf");
```

Pod povrchem knihovna vytvoří neviditelnou textovou vrstvu, která se slaďuje s původním obrázkem. Když otevřete výsledný soubor v Adobe Readeru, budete moci zadat slovo do vyhledávacího pole a okamžitě skočit na odpovídající místo.

## Krok 5: Ověřte výsledek — jak výstup vypadá?

```java
        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF generated.");
    }
}
```

Spusťte program, poté otevřete `french_invoice_searchable.pdf`. Zkuste vyhledat slovo, o kterém víte, že se na faktuře vyskytuje (např. „Total“). Pokud se zvýraznění objeví na správném místě, úspěšně jste **create searchable pdf**.  

![Vytvořit prohledávatelný PDF příklad](example.png)<!-- alt text includes primary keyword -->

### Očekávaný výstup

```
Searchable PDF generated.
```

A PDF soubor v `YOUR_DIRECTORY`, který můžete sdílet, indexovat nebo archivovat.

## Krok 6: Extrahujte surový text z obrázku (volitelné)

Někdy potřebujete prostý text pro další zpracování — třeba pro naplnění databáze nebo sentiment analýzu. Aspose vám umožní získat rozpoznaný text přímo:

```java
        // Optional: Get the extracted text as a String
        String extractedText = ocrEngine.getText();
        System.out.println("Extracted text:");
        System.out.println(extractedText);
```

Tento úryvek demonstruje **extract text from image** bez vytváření PDF. Je užitečný, když vás zajímá jen obsah, ne vizuální rozložení.

## Zpracování více stránek nebo obrázků

Co když je vaším zdrojem více‑stránkový TIFF nebo složka JPEGů? Můžete projít soubory ve smyčce a volat `recognizeToPdf` pro každý, poté sloučit PDF pomocí Aspose PDF nebo jiné knihovny. Zde je rychlý vzor:

```java
import java.io.File;
import com.aspose.pdf.*;

public class MultiPageDemo {
    public static void main(String[] args) throws Exception {
        OcrEngine engine = new OcrEngine();
        File folder = new File("YOUR_DIRECTORY/images");
        Document finalDoc = new Document();

        for (File img : folder.listFiles((d, n) -> n.matches(".*\\.(png|jpg|tif)"))) {
            engine.setImage(img.getAbsolutePath());
            // Save each page as a temporary PDF
            String tempPdf = img.getName() + ".pdf";
            engine.recognizeToPdf(tempPdf);
            // Append to final document
            Document pageDoc = new Document(tempPdf);
            finalDoc.getPages().add(pageDoc.getPages().get_Item(1));
        }
        finalDoc.save("YOUR_DIRECTORY/combined_searchable.pdf");
        System.out.println("All pages merged into searchable PDF.");
    }
}
```

**Pro tip:** Po sloučení odstraňte dočasné PDF, aby byl pracovní prostor uklizený.

## Časté úskalí a jak se jim vyhnout

- **Nízké rozlišení obrázků:** Přesnost OCR dramaticky klesá pod 150 dpi. Zvětšete rozlišení nebo požádejte o sken vyšší kvality, pokud je to možné.  
- **Nakloněné stránky:** Otočený obrázek může engine zmást. Použijte `ocrEngine.getImagePreprocessingSettings().setDeskew(true)` pro automatické opravení mírného sklonu.  
- **Není podporovaný jazyk:** Ujistěte se, že jazyk, který nastavujete, je zahrnut v licenci Aspose OCR; jinak se engine vrátí k angličtině.  
- **Velké soubory:** Zpracování 30 MB TIFF může být náročné na paměť. Zvažte rozdělení na menší části nebo zvýšení haldy JVM (`-Xmx2g`).

## Další kroky — kam dál

Nyní, když ovládáte základy **create searchable pdf**, můžete zkusit:

- **Dávkovou konverzi:** Spojte více‑stránkový vzor se schedulerem a zpracovávejte příchozí skeny každou noc.  
- **Vkládání metadat:** Použijte Aspose PDF k přidání názvu, autora nebo vlastních tagů do prohledávatelného PDF.  
- **Digitální podpisy:** Po OCR zabezpečte PDF certifikátem, čímž zajistíte soulad s právními požadavky.  

Všechny tyto rozšíření stále vycházejí ze základních konceptů, které jsme probírali: inicializace OCR enginu, volitelné nastavení jazyka, načtení obrázku a volání `recognizeToPdf`.

---

### TL;DR

Prošli jsme kompletním, spustitelným příkladem, který ukazuje, jak **create searchable PDF** z obrázku pomocí Aspose OCR pro Java. Kroky zahrnují inicializaci enginu, volitelné nastavení jazyka (odpověď na „how to set language“), načtení obrázku, provedení OCR, uložení prohledávatelného PDF a volitelně extrakci čistého textu. Také jsme pokryli zpracování více stránek, časté úskalí a nápady na další automatizaci.

Vyzkoušejte to na vlastních účtech, smlouvách nebo rukopisných poznámkách — přeměňte statické obrázky na plně prohledávatelné dokumenty během několika sekund. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}