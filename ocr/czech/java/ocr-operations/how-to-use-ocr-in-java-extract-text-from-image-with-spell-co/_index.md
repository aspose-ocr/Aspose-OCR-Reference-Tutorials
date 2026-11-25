---
category: general
date: 2026-05-06
description: Jak použít OCR k extrakci textu z obrázku v Javě. Naučte se převod obrázku
  na text pomocí OCR, opravit chyby OCR a načíst obrázek pro OCR s Aspose OCR.
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: cs
og_description: Jak použít OCR v Javě k extrahování textu z obrázku, opravě chyb OCR
  a načtení obrázku pro OCR pomocí Aspose OCR.
og_title: Jak používat OCR v Javě – kompletní průvodce
tags:
- OCR
- Java
- Aspose
title: Jak použít OCR v Javě – Extrahovat text z obrázku s opravou pravopisu
url: /cs/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat OCR v Javě – Extrahovat text z obrázku s opravou pravopisu

Už jste se někdy zamysleli **jak používat OCR** k převodu rozmazané fotografie účtenky na čistý, prohledávatelný text? Nejste v tom sami. V mnoha projektech—aplikacích pro sledování výdajů, pipelinech pro digitalizaci faktur nebo dokonce rychlém skriptu pro zapisování poznámek—získání spolehlivého textu z obrázku je první překážkou.  

Tento tutoriál vám přesně ukáže, jak používat OCR v Javě, pokrývající vše od načtení obrázku pro OCR až po opravu OCR chyb, aby výsledek vypadal, jako by byl napsán člověkem. Na konci budete schopni **extrahovat text z obrázku**, provést konverzi **OCR image to text** a automaticky opravit běžné chyby rozpoznávání.

## Co vytvoříte

Vytvoříme malý Java konzolový program, který:

1. Načte PNG (nebo jakýkoli podporovaný formát) do Aspose OCR engine.  
2. Aktivuje vestavěnou funkci opravy pravopisu pro **opravu OCR chyb**.  
3. Spustí proces rozpoznávání a vypíše vyčištěný text.  

C​e žádné externí služby, žádné těžké frameworky—pouze jeden JAR a několik řádků kódu.

### Požadavky

- Java Development Kit (JDK) 8 nebo novější.  
- Maven (nebo jakýkoli nástroj pro sestavení) pro stažení knihovny Aspose OCR.  
- Soubor s obrázkem (např. `receipt.png`), který chcete analyzovat.  

Pokud vám chybí Aspose OCR JAR, přidejte tuto závislost do vašeho `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **Tip:** Bezplatná evaluační verze funguje pro testování, ale licence odstraní evaluační vodoznak.

## Krok 1 – Inicializace OCR Engine (Primární klíčové slovo v akci)

Prvním krokem je vytvořit instanci `OcrEngine`. Představte si ji jako mozek, který bude číst pixely a převádět je na znaky.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*Proč je to důležité:* Inicializace engine nastaví interní zdroje (jazykové modely, slovníky atd.). Vynechání tohoto kroku by později při načítání obrázku způsobilo `NullPointerException`.

## Krok 2 – Načtení obrázku pro OCR

Nyní skutečně **načteme obrázek pro OCR**. Aspose poskytuje pohodlný pomocník `ImageStream.fromFile`, ale můžete také předat `byte[]`, pokud chcete.

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*Častý úskalí:* Cesta k souboru musí být absolutní nebo relativní k pracovnímu adresáři. Pokud obrázek nelze najít, engine vyhodí `IOException`. Zkontrolujte cestu, zejména při spuštění z IDE oproti zabalenému JAR.

## Krok 3 – Aktivace opravy pravopisu pro **opravu OCR chyb**

Výchozí OCR může být hlučné—např. “l0ve” místo “love” nebo “0” místo “O”. Aktivace opravy pravopisu řekne engine, aby provedl post‑processing, který opraví typické chyby.

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*Proč to chcete:* Bez opravy pravopisu byste museli výstup ručně čistit, což ruší smysl automatizace. Vestavěný slovník funguje dobře pro angličtinu a několik dalších jazyků.

## Krok 4 – Provedení rozpoznání (**OCR Image to Text**)

S načteným obrázkem a aktivovanou opravou pravopisu můžeme nakonec požádat engine o rozpoznání textu.

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*Hraniční případ:* Pokud je obrázek nízkokontrastní nebo silně nakloněný, výsledek může stále obsahovat nesmysly. Zvažte předzpracování (např. binarizaci, deskew) před předáním engine.

## Krok 5 – Výstup vyčištěného textu

Poslední krok je jednoduše vytištění výsledku. Ve skutečné aplikaci jej můžete zapsat do databáze nebo souboru, ale pro tuto ukázku stačí `System.out`.

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Očekávaný výstup

Předpokládáme, že `receipt.png` obsahuje jasný seznam položek, můžete vidět něco jako:

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

Všimněte si, že „Qty“ a „Price“ jsou napsány správně, i když původní sken měl chybný „Qy“.

## Kompletní funkční příklad

Níže je kompletní program, který můžete zkopírovat a vložit do souboru pojmenovaného `SpellCorrectDemo.java`. Ujistěte se, že Aspose OCR JAR je ve vaší classpath.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

Spusťte jej pomocí:

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

Nyní byste měli vidět vyčištěný text vytištěný do konzole.

## Bonus: Ladění nastavení pro vyšší přesnost

Zatímco výchozí konfigurace funguje pro většinu tištěných dokumentů, možná budete muset upravit několik parametrů pro specializované scénáře:

| Nastavení | Co dělá | Kdy změnit |
|-----------|---------|------------|
| `setLanguage(OcrLanguage.English)` | Vynutí anglický slovník (snižuje falešně pozitivní výsledky) | Pokud obrázek obsahuje pouze anglický text. |
| `setResolution(300)` | Řekne engine DPI zdrojového obrázku | Pro skeny s vysokým rozlišením. |
| `setEnableAutoSkewCorrection(true)` | Automaticky otočí mírně nakloněné stránky | Když jsou obrázky pořízeny telefonem. |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## Často kladené otázky

**Q: Funguje to s PDF?**  
A: Ano. Převést každou stránku PDF na obrázek (např. pomocí Aspose PDF) a předat obrázek OCR engine.

**Q: Co když je můj obrázek ve formátu BMP?**  
A: `ImageStream.fromFile` podporuje PNG, JPEG, BMP, TIFF a GIF přímo. Stačí změnit příponu souboru.

**Q: Můžu vypnout opravu pravopisu?**  
A: Rozhodně—nastavte `setEnableSpellCorrection(false)`, pokud potřebujete surový OCR výstup pro další zpracování.

## Závěr

Nyní víte **jak používat OCR** v Javě k **extrahování textu z obrázku**, automaticky **opravovat OCR chyby** a správně **načíst obrázek pro OCR** pomocí Aspose OCR. Pěti‑krokový tok—initialise, load, enable spell correction, recognize, and output—pokrývá většinu běžných OCR úkolů.  

Odtud zvažte propojení této logiky s databázovým zápisem, REST endpointem nebo dávkovým procesorem pro zpracování desítek účtenek najednou. Experimentujte s tabulkou nastavení výše, abyste vytáhli poslední možnou přesnost.

Šťastné programování a ať jsou vaše OCR výsledky vždy čistší než vaše kávou znečištěné účtenky! 

![how to use ocr diagram showing image → OCR engine → corrected text flow]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}