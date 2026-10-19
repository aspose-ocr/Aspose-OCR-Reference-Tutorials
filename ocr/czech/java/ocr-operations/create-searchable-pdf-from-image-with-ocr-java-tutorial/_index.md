---
category: general
date: 2026-01-07
description: Vytvořte prohledávatelný PDF z obrázku pomocí Aspose OCR v Javě. Naučte
  se, jak převést obrázek na PDF, rozpoznat text z obrázku a vytvořit PDF z JPG.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- how to use ocr
- generate pdf from jpg
language: cs
og_description: Vytvořte prohledávatelný PDF z obrázku pomocí Aspose OCR v Javě. Podrobný
  návod krok za krokem, jak převést obrázek na PDF, rozpoznat text z obrázku a vygenerovat
  PDF z JPG.
og_title: Vytvořte prohledávatelný PDF z obrázku – Průvodce Java OCR
tags:
- OCR
- Java
- PDF
- Aspose
title: Vytvořte prohledávatelný PDF z obrázku s OCR – Java tutoriál
url: /cs/java/ocr-operations/create-searchable-pdf-from-image-with-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF z obrázku pomocí OCR – Java tutoriál

Už jste někdy potřebovali **vytvořit prohledávatelné PDF** ze skenovaného obrázku, ale nevedeli ste, kde začať? Nie ste sami – mnoho vývojárov narazí na tento problém, keď sa prvýkrát snažia premeniť JPEG na PDF, ktorý je možné skutočne prehľadávať.  

V tomto návode prejdeme kompletným, spustiteľným príkladom, ktorý vám ukáže, ako **previesť obrázok na PDF**, **rozpoznať text z obrázku** a nakoniec **vytvoriť PDF z JPG** pomocou Aspose OCR pre Java. Žiadne nejasné odkazy, len kód, ktorý môžete skopírovať‑vložiť a spustiť ešte dnes.

## Čo budete potrebovať

Predtým, než sa pustíme do práce, uistite sa, že máte na svojom počítači nasledujúce:

* **Java 17** alebo novšiu (API funguje s akoukoľvek aktuálnou verziou JDK).  
* **Aspose.OCR for Java** knižnicu – najnovší JAR si môžete stiahnuť z Maven Central alebo z webu Aspose.  
* Vzorový obrázok, napríklad `sample.jpg`, umiestnený v priečinku, na ktorý môžete odkazovať.  
* IDE alebo jednoduchý textový editor plus terminál – čokoľvek, čo vám vyhovuje.

To je všetko. Žiadne ťažké frameworky, žiadne ďalšie natívne závislosti. Poďme na to.

## Krok 1 – Vytvorenie prohľadávatelného PDF: Inicializácia OCR enginu

Prvou vecou, ktorú urobíme, je spustiť inštanciu `OcrEngine` a nasmerovať ju na zdrojový obrázok. Tento objekt je srdcom Aspose OCR; spracováva všetko od načítania bitmapy po poskytovanie rozpoznaného textu.

```java
import com.aspose.ocr.*;

public class HelloOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the image you want to turn into a searchable PDF
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

> **Prečo je to dôležité:** Správna inicializácia enginu zabezpečuje, že knižnica dokáže načítať formát obrázka, ktorý jej poskytujete. Ak je cesta nesprávna, dostanete `FileNotFoundException` a celý reťazec sa zastaví.

## Krok 2 – Zvýšenie výkonu: Povolenie GPU, viacjadrového CPU a opravy pravopisu

OCR môže byť náročný na CPU, najmä pri veľkých dokumentoch. Aspose vám poskytuje niekoľko nastavení, ktoré môžete upraviť, aby bol proces rýchlejší a presnejší.

```java
        // 2️⃣ Turn on performance helpers – GPU, multi‑core CPU, and spell correction
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)                 // uses GPU if one is available
                 .setUseMultiCore(true)           // spreads work across CPU cores
                 .setEnableSpellCorrection(true); // cleans up common OCR mistakes
```

> **Tip:** Ak bežíte na serveri bez GPU, `setUseGpu(false)` vám neublíži – jednoducho sa vráti na viacjadrové spracovanie CPU.

## Krok 3 – Zlepšenie kvality obrázka: Vyrovnanie a odstránenie šumu (voliteľné, ale odporúčané)

Skeny zriedka sú dokonalé. Mierny náklon alebo šum môžu rozpoznávač zmiasť. Trieda `ImageProcessingOptions` vám umožní obrázok predtým vyčistiť, než ho engine začne čítať.

```java
        // 3️⃣ Pre‑process the image – straighten it and remove noise
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)   // automatically rotates tilted text
                 .setDespeckle(true); // reduces background speckles
```

> **Okrajový prípad:** Ak je váš zdrojový obrázok už čistý, môžete tento krok preskočiť. Neškodí, ale pridá niekoľko milisekúnd režijných nákladov.

## Krok 4 – Rozpoznanie textu z obrázka a generovanie PDF

Teraz sa deje mágia. Zavoláme `recognize()` a engine vráti `OcrResult`. Odtiaľ môžete uložiť výstup v rôznych formátoch – PDF je najčastejší pre prohľadávané dokumenty.

```java
        // 4️⃣ Perform OCR and get the result object
        OcrResult ocrResult = ocrEngine.recognize();

        // 5️⃣ Save the result as a searchable PDF (you could also choose TXT, DOCX, etc.)
        ocrResult.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);
    }
}
```

> **Čo uvidíte:** `sample-output.pdf` obsahuje pôvodný obrázok ako pozadie, zatiaľ čo rozpoznaný text je navrchu ako neviditeľná vrstva. Otvorte ho v Adobe Reader a skúste vybrať text – budete prekvapení.

## Krok 5 – Overenie výstupu prohľadávaného PDF

Po zapísaní súboru je dobré skontrolovať, či je PDF skutočne prohľadávaný.

```java
import java.awt.Desktop;
import java.io.File;

public class VerifyPdf {
    public static void main(String[] args) throws Exception {
        File pdf = new File("YOUR_DIRECTORY/sample-output.pdf");
        if (pdf.exists() && Desktop.isDesktopSupported()) {
            Desktop.getDesktop().open(pdf); // opens the PDF in the default viewer
        } else {
            System.out.println("PDF not found or cannot be opened on this platform.");
        }
    }
}
```

Otvorte PDF, stlačte **Ctrl F**, napíšte slovo, o ktorom viete, že sa nachádza na obrázku – ak ho vyhľadávanie nájde, úspešne ste **vytvorili prohľadávané pdf**!

## Ako použiť OCR v reálnych scenároch (bonus)

* **Dávkové spracovanie:** Zabaľte kód do slučky, ktorá prechádza priečinok s JPG súbormi. Nezabudnite opakovane používať jednu inštanciu `OcrEngine`, aby ste udržali nízku spotrebu pamäte.  
* **Podpora jazykov:** Aspose OCR podporuje viac ako 60 jazykov. Stačí zavolať `ocrEngine.getEngineOptions().setLanguage(Language.English);` (alebo akúkoľvek inú hodnotu enumu).  
* **Spracovanie chýb:** Zachyťte `OcrException`, aby ste elegantne riešili poškodené súbory.  

Tieto vylepšenia robia riešenie dostatočne robustné pre produkčné pipeline.

## Kompletný Java príklad – Vytvorenie prohľadávatelného PDF z JPG

Nižšie je celý, samostatný program, ktorý môžete skompilovať a spustiť tak, ako je. Nahraďte `YOUR_DIRECTORY` skutočnou cestou na vašom počítači.

```java
import com.aspose.ocr.*;

public class CreateSearchablePdf {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // -------------------------------------------------
        // 2️⃣ Performance helpers
        // -------------------------------------------------
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)
                 .setUseMultiCore(true)
                 .setEnableSpellCorrection(true);

        // -------------------------------------------------
        // 3️⃣ Image pre‑processing (optional but helpful)
        // -------------------------------------------------
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)
                 .setDespeckle(true);

        // -------------------------------------------------
        // 4️⃣ Run OCR and save as searchable PDF
        // -------------------------------------------------
        OcrResult result = ocrEngine.recognize();
        result.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);

        System.out.println("✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf");
    }
}
```

**Očakávaný výstup:**  

```
✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf
```

Otvorte vygenerované PDF a mali by ste byť schopní vyhľadávať akékoľvek slovo, ktoré sa objavilo v `sample.jpg`. Ak nevidíte textovú vrstvu, skontrolujte cestu k obrázku a uistite sa, že OCR engine nevyhadzuje skryté výnimky.

## Záver

Ukázali sme vám, ako **vytvoriť prohľadávatelné PDF** z JPEG pomocou Aspose OCR pre Java. Od načítania obrázka, nastavenia výkonu, čistenia obrázka až po rozpoznanie textu a uloženie prohľadávaného PDF – každý krok bol vysvetlený s *prečo* a *ako*.  

Teraz môžete **previesť obrázok na PDF**, **rozpoznať text z obrázku** a **vytvoriť PDF z JPG** vo svojich aplikáciách. Ďalej skúste spracovať celý priečinok skenov, experimentovať s rôznymi jazykmi alebo pridať ochranu heslom k výstupnému PDF. Možnosti sú neobmedzené.

Máte otázky ohľadom okrajových prípadov, licencovania alebo ladenia výkonu? Napíšte komentár nižšie a šťastné kódovanie! 

![Diagram illustrating OCR pipeline – create searchable pdf](/images/ocr-pipeline.png "Diagram vytvářející prohledávatelné PDF")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}