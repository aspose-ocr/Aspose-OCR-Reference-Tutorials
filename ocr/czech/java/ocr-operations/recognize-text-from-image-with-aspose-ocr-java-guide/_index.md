---
category: general
date: 2026-06-19
description: Rozpoznat text z obrázku pomocí Aspose OCR v Javě a naučit se převést
  obrázek do formátu DOCX, extrahovat text z PNG a převést naskenovaný obrázek do
  tabulky.
draft: false
keywords:
- recognize text from image
- convert image to docx
- extract text from png
- convert scanned image to spreadsheet
language: cs
og_description: Rozpoznávejte text z obrázku v Javě pomocí Aspose OCR. Postupujte
  podle tohoto krok‑za‑krokem tutoriálu, který převádí obrázek na docx, extrahuje
  text z png a převádí naskenovaný obrázek na tabulku.
og_title: Rozpoznání textu z obrázku pomocí Aspose OCR – průvodce pro Javu
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: recognize text from image using Aspose OCR in Java and learn to convert
    image to docx, extract text from png, and convert scanned image to spreadsheet.
  headline: recognize text from image with Aspose OCR – Java guide
  type: TechArticle
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Rozpoznat text z obrázku pomocí Aspose OCR – Java průvodce
url: /cs/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rozpoznání textu z obrázku pomocí Aspose OCR – průvodce pro Java

Už jste někdy potřebovali **rozpoznat text z obrázku**, ale nebyli jste si jisti, která knihovna zvládne německé PDF, PNG a dokonce vytvoří tabulku? Nejste v tom sami. V tomto tutoriálu projdeme kompletním příkladem v Javě, který nejen extrahuje znaky, ale také **převede obrázek na docx**, **extrahuje text z png** a dokonce **převede naskenovaný obrázek na tabulku**—vše pomocí několika řádků.

Použijeme Aspose.OCR, komerční knihovnu s jednoduchým API. Nebojte se, pokud nemáte licenci; demo funguje v evaluačním režimu, i když některé funkce (např. výstup ve vysokém rozlišení) jsou omezené. Na konci budete mít spustitelný program, který vezme PNG snímek zprávy a automaticky vytvoří soubory DOCX, XLSX a EPUB.

## Požadavky

* **Java Development Kit (JDK) 17** nebo novější nainstalovaný.
* **Aspose.OCR for Java** JAR (stáhněte z webu Aspose nebo přidejte přes Maven).
* Volitelný soubor **Aspose.OCR.lic**, pokud chcete plnou funkčnost bez evaluačních vodoznaků.
* Vzorek obrázku – nazveme ho `report.png` – umístěný ve složce, na kterou můžete odkazovat z kódu.

Pokud používáte Maven, přidejte tuto závislost do svého `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

Nyní, když je základ připraven, pojďme na to.

## Krok 1: rozpoznat text z obrázku – použít licenci (volitelné)

Nejprve musíme Aspose sdělit, že máme licenci. Přeskočení tohoto kroku demo nepoškodí, ale vygenerované soubory budou obsahovat malý banner „Evaluation“.

```java
import com.aspose.ocr.*;

public class ExportDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose.OCR license (optional for full functionality)
        License license = new License();
        try {
            license.setLicense("Aspose.OCR.lic");
            System.out.println("License loaded successfully.");
        } catch (Exception e) {
            System.out.println("License not found – running in evaluation mode.");
        }
```

> **Tip:** Umístěte soubor `.lic` vedle svého zkompilovaného JARu nebo použijte absolutní cestu; jinak volání `setLicense` vyhodí výjimku.

## Krok 2: rozpoznat text z obrázku – vytvořit a nakonfigurovat OCR engine

Nyní spustíme OCR engine a řekneme mu, jaký jazyk očekáváme. V tomto příkladu pracujeme s němčinou, ale Aspose podporuje desítky jazyků přímo z krabice.

```java
        // Create an OCR engine and set the recognition language to German
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setLanguage(Language.German); // change to Language.English for English text
```

Proč nastavit jazyk? Engine používá jazykově specifické slovníky ke zlepšení přesnosti, zejména pro znaky jako „ß“ nebo „ü“. Pokud to přeskočíte, stále získáte výsledek, ale bude hlučnější.

## Krok 3: rozpoznat text z obrázku – načíst PNG a získat surové výsledky

Zde je jádro dema: předáme engine cestu k PNG souboru a necháme ho udělat těžkou práci.

```java
        // Recognize text from the input image
        String inputImagePath = "YOUR_DIRECTORY/report.png"; // <-- replace with your actual path
        OcrResult ocrResult = ocrEngine.recognizeImage(inputImagePath);
        System.out.println("OCR completed. Extracted " + ocrResult.getText().length() + " characters.");
```

Objekt `OcrResult` obsahuje surový Unicode řetězec plus informace o rozložení, které můžete později použít, pokud potřebujete zachovat formátování. Pokud je obrázek naskenovaná tabulka, engine stále vrátí prostý text – ideální pro další krok, kde **převádíme naskenovaný obrázek na tabulku**.

## Krok 4: převést obrázek na docx – uložení výsledku jako Word dokument

Aspose to dělá naprosto jednoduché exportovat výstup OCR do souboru DOCX. To je užitečné, když potřebujete editovatelný Word dokument pro další zpracování.

```java
        // Save the recognized text in DOCX format
        String outputDocxPath = "YOUR_DIRECTORY/report.docx";
        ocrResult.save(outputDocxPath, OutputFormat.Docx);
        System.out.println("Saved DOCX to " + outputDocxPath);
```

Za scénou knihovna vytvoří jednoduchý Word dokument s jedním odstavcem, který obsahuje extrahovaný text. Pokud potřebujete bohatší stylování (nadpisy, tabulky), můžete DOCX později post‑processovat pomocí Apache POI nebo Aspose.Words.

## Krok 5: převést naskenovaný obrázek na tabulku – export do XLSX

Někdy je naskenovaná faktura nebo finanční tabulka snazší zpracovat v Excelu. Ten samý `OcrResult` lze uložit jako soubor XLSX a Aspose se pokusí zachovat tabulkové struktury, pokud je detekuje.

```java
        // Save the same result in additional formats (XLSX, EPUB)
        String outputXlsxPath = "YOUR_DIRECTORY/report.xlsx";
        ocrResult.save(outputXlsxPath, OutputFormat.Xlsx);
        System.out.println("Saved XLSX to " + outputXlsxPath);
```

Pokud původní PNG obsahovalo čistou mřížku, výsledná tabulka bude mít samostatné buňky pro každý sloupec. Jinak získáte jediný sloupec s konci řádků – stále lepší než ruční kopírování.

## Krok 6: extrahovat text z png – také export do EPUB (volitelné)

Pro úplnost ukážeme, jak vygenerovat e‑book ve formátu EPUB. To demonstruje flexibilitu metody `save` v Aspose a poskytuje další způsob, jak **extrahovat text z png** pro publikaci.

```java
        // Optional: export to EPUB for e‑reading devices
        String outputEpubPath = "YOUR_DIRECTORY/report.epub";
        ocrResult.save(outputEpubPath, OutputFormat.Epub);
        System.out.println("Saved EPUB to " + outputEpubPath);
    }
}
```

To je celý program. Zkompilujte jej (`javac ExportDemo.java`) a spusťte (`java ExportDemo`). Pokud je vše správně nastaveno, uvidíte ve `YOUR_DIRECTORY` čtyři soubory: `report.docx`, `report.xlsx`, `report.epub`, a konzole vypíše počet extrahovaných znaků.

## Časté problémy a jak se jim vyhnout

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Licence nenalezena** | Cesta k `Aspose.OCR.lic` je špatná nebo chybí. | Umístěte soubor vedle JARu nebo použijte absolutní cestu v `setLicense`. |
| **Špatné znaky** | Nastaven špatný jazyk (např. angličtina pro německý text). | Zavolejte `ocrEngine.setLanguage(Language.German)` nebo správný jazykový enum. |
| **Prázdné výstupní soubory** | Chybná cesta k vstupnímu obrázku nebo nepodporovaný formát. | Ověřte cestu, ujistěte se, že soubor existuje a že je podporovaným rastrovým formátem (PNG, JPEG, BMP). |
| **Velká velikost souboru** | Používání obrázků s vysokým rozlišením bez zmenšení. | Změňte velikost obrázku na ~300 dpi před OCR; Aspose to může udělat automaticky pomocí `ocrEngine.setResolution(300)`. |

## Rozšíření řešení

Nyní, když můžete **rozpoznat text z obrázku** a **převést naskenovaný obrázek na tabulku**, můžete se ptát, co dalšího můžete udělat:

* **Dávkové zpracování** – projít složku s PNG soubory a vygenerovat ZIP soubor s DOCX/XLSX soubory.
* **Post‑zpracování** – použít regulární výrazy k vyčištění OCR šumu (např. nežádoucí konce řádků).
* **Integrace** – napojit kód na Spring Boot REST endpoint, který přijímá nahrané obrázky a vrací ke stažení DOCX.

Všechny tyto nápady staví na stejných základních krocích, které jsme právě prošli.

## Závěr

Právě jste se naučili, jak **rozpoznat text z obrázku** pomocí Aspose OCR pro Java, a nyní víte, jak **převést obrázek na docx**, **extrahovat text z png** a **převést naskenovaný obrázek na tabulku** pomocí několika volání metod. Kompletní, spustitelný příklad výše ukazuje každý import, každou konfiguraci a přesný výstup, který můžete očekávat.

Dále zkuste změnit jazyk na angličtinu, použít vícestránkový TIFF, nebo propojit výstup DOCX s Aspose.Words pro pokročilé formátování. Možnosti jsou neomezené, když kombinujete OCR s knihovnami pro generování dokumentů.

Máte otázky nebo narazili na problém? Zanechte komentář a šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným vysvětlením, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Převést obrázek na text v Javě pomocí Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Extrahovat text z obrázku v Javě s Aspose.OCR Detekcí oblastí](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Jak provést OCR textu z obrázku s jazykem pomocí Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}