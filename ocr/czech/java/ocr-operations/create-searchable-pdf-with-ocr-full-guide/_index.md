---
category: general
date: 2026-06-22
description: Vytvořte prohledávatelný PDF pomocí OCR v Javě. Naučte se, jak vypnout
  kompresi a rychle převést naskenovaný PDF obrázek na prohledávatelný PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- ocr to searchable pdf
- how to disable compression
- pdf without compression
language: cs
og_description: Vytvořte vyhledávatelný PDF pomocí OCR v Javě. Tento návod ukazuje,
  jak vypnout kompresi, převést naskenovaný PDF obrázek a vytvořit PDF bez komprese.
og_title: Vytvořte prohledávatelný PDF s OCR – kompletní Java tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  headline: Create Searchable PDF with OCR – Full Guide
  type: TechArticle
- description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  name: Create Searchable PDF with OCR – Full Guide
  steps:
  - name: Set the output format to `PDF_SEARCHABLE`.
    text: Set the output format to `PDF_SEARCHABLE`.
  - name: Turn off PDF compression with `PdfCompression.NONE`.
    text: Turn off PDF compression with `PdfCompression.NONE`.
  - name: Run OCR and capture the `PdfDocument`.
    text: Run OCR and capture the `PdfDocument`.
  - name: Save the file to disk.
    text: Save the file to disk.
  type: HowTo
tags:
- OCR
- PDF
- Java
- Document Processing
title: Vytvořte prohledávatelný PDF s OCR – kompletní průvodce
url: /cs/java/ocr-operations/create-searchable-pdf-with-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF s OCR – Kompletní průvodce

Už jste někdy potřebovali **vytvořit prohledávatelné PDF** z dávky naskenovaných obrázků, ale nebyli jste si jisti, jaká nastavení změnit? Nejste v tom sami – většina vývojářů narazí na stejný problém, když výstup skončí jako obrovská, nečitelné hromady.  

V tomto tutoriálu projdeme čistým, end‑to‑end příkladem, který vám přesně ukáže, jak **vytvořit prohledávatelné PDF** pomocí Java OCR engine, **převést naskenovaný obrázek PDF**, a co je nejdůležitější, **jak vypnout kompresi**, aby výsledný soubor zůstal věrný původním rozměrům. Na konci budete mít připravený útržek kódu a solidní pochopení, proč každá konfigurace má smysl.

## Co se naučíte

* Jak nakonfigurovat OCR engine na **ocr to searchable pdf**.  
* Důvod, proč vypnout PDF kompresi a jak získat **pdf without compression**.  
* Kompletní Java program, který vezme naskenovaný obrázek, spustí OCR a uloží **searchable PDF**.  
* Tipy pro řešení okrajových případů, jako jsou vícestránkové skeny nebo zdroje s nízkým rozlišením.  

**Požadavky** – Java 8+ nainstalovaná, kompatibilní OCR SDK (kód používá ABBYY FineReader Engine API, ale koncepty platí pro jakoukoli knihovnu nabízející `setOutputFormat` a `setPdfCompression`). IDE jako IntelliJ IDEA nebo Eclipse usnadní práci, ale stačí i jednoduchý textový editor.

---

![Create searchable PDF workflow](image-placeholder.png "Diagram ukazující proces vytvoření prohledávatelného pdf z naskenovaných obrázků až po finální PDF")

## Krok 1: Nastavte OCR engine na **Create Searchable PDF**

První věc, kterou musíte OCR engine sdělit, je, jaký typ výstupu očekáváte. Ve výchozím nastavení mnoho SDK vrací prostý text nebo rastrové PDF, které není prohledávatelné. Přepnutí formátu udělá těžkou práci za vás.

```java
// Step 1: Tell the engine we want a searchable PDF
engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

*Proč je to důležité*: Příznak `PDF_SEARCHABLE` instruuje engine, aby pod naskenovaným obrázkem vložil neviditelnou textovou vrstvu. Vyhledávací nástroje pak mohou dokument indexovat a chovat se jako jakékoli nativní PDF, které otevřete v Adobe Readeru.

## Krok 2: Vypněte kompresi – **How to Disable Compression** správně

Pokud tento krok přeskočíte, engine každou stránku komprimuje, aby ušetřil místo, ale komprese může rozmazat jemné detaily – což je obzvláště problematické, když později potřebujete extrahovat vysoce rozlišené obrázky.

```java
// Step 2: Turn off PDF compression to keep original image quality
engine.getConfig().setPdfCompression(PdfCompression.NONE);
```

**Tip**: Vypnutí komprese je nezbytné, když archivujete právní dokumenty nebo lékařské skeny, kde každý pixel hraje roli. Výsledný soubor může být větší, ale zachováte původní rozměry a ostrost.

## Krok 3: Proveďte OCR a získejte výsledný dokument

Nyní, když engine ví, co má výstup a jak má zacházet s obrázky, můžete spustit rozpoznávání. Volání vrátí objekt `PdfDocument`, který je připraven k uložení nebo dalším úpravám.

```java
// Step 3: Run OCR and capture the searchable PDF in memory
PdfDocument pdf = engine.recognizeToPdf();
```

*Co se děje pod kapotou?* Engine zpracuje každou vstupní stránku, provede rozpoznání znaků a připojí skrytou textovou vrstvu k obrázku. Pokud máte více stránek, jsou automaticky spojeny.

## Krok 4: Uložte **Searchable PDF** na disk

Nakonec zapište PDF z paměti do souboru. Vyberte umístění, kde máte právo zapisovat, a dejte souboru smysluplný název.

```java
// Step 4: Persist the searchable PDF on disk
pdf.save("YOUR_DIRECTORY/searchable.pdf");
```

Když otevřete `searchable.pdf` v prohlížeči, všimnete si, že můžete text vybírat a vyhledávat – i když viditelný obsah zůstává původní naskenovaný obrázek.

### Kompletní funkční příklad

Níže je samostatná Java třída, která spojuje všechny čtyři kroky. Klidně ji zkopírujte, upravte vstupní cestu a spusťte tak, jak je.

```java
import com.abbyy.ocrsdk.Engine;
import com.abbyy.ocrsdk.OcrOutputFormat;
import com.abbyy.ocrsdk.PdfCompression;
import com.abbyy.ocrsdk.PdfDocument;

/**
 * Demonstrates how to create searchable PDF from scanned images.
 * This example uses the ABBYY FineReader Engine Java API.
 */
public class SearchablePdfCreator {

    public static void main(String[] args) {
        // ---- 1. Initialize the OCR engine -------------------------------------------------
        Engine engine = new Engine();
        // (Assume license activation and engine initialization are handled elsewhere)

        // ---- 2. Configure output to be a searchable PDF ----------------------------------
        engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);

        // ---- 3. Disable compression for a PDF without compression -------------------------
        engine.getConfig().setPdfCompression(PdfCompression.NONE);

        // ---- 4. Load the scanned image(s) --------------------------------------------------
        // For simplicity, we let the engine auto‑detect images in the working folder.
        // You could also call engine.addImage("path/to/image.tif") for explicit control.
        engine.addImage("YOUR_DIRECTORY/scanned-page.tif");

        // ---- 5. Perform OCR and retrieve the PDF -----------------------------------------
        PdfDocument pdf = engine.recognizeToPdf();

        // ---- 6. Save the result -----------------------------------------------------------
        pdf.save("YOUR_DIRECTORY/searchable.pdf");

        System.out.println("✅ Searchable PDF created successfully at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**Očekávaný výstup** – Po spuštění programu uvidíte zprávu v konzoli výše a soubor `searchable.pdf` se objeví v `YOUR_DIRECTORY`. Otevřením v libovolném PDF čtečce byste měli být schopni:

* Zvýraznit text.  
* Použít vestavěné vyhledávání (Ctrl + F) k nalezení slov.  
* Exportovat skrytou textovou vrstvu, pokud bude potřeba.

---

## Proč vypínat kompresi? Pochopení **PDF Without Compression**

Možná se ptáte: „Není komprese vždy dobrá?“ Odpověď je nuancovaná:

| Situace | Zachovat kompresi (`NORMAL`) | Vypnout kompresi (`NONE`) |
|-----------|-----------------------------|------------------------------|
| Archivace právních smluv | ❌ Může změnit pixelovou věrnost | ✅ Zaručuje původní vzhled |
| Velká dávka nízkokvalitních skenů | ✅ Šetří úložiště | ❌ Zvětšuje velikost bez přínosu |
| Potřeba OCR přesnosti u drobných fontů | ❌ Rozmazává jemné detaily | ✅ Zachovává každý tah |

Stručně řečeno, **how to disable compression** je kompromis mezi úložištěm a věrností. Pro většinu workflow s prohledávatelným PDF, kde chcete vyhledávat text spíše než tisknout obrázky, je vypnutí komprese nejbezpečnější volba.

## Převod **Scanned Image PDF** přímo

Někdy už máte PDF, které obsahuje naskenované obrázky (tzv. „image‑only PDF“). Pro **convert scanned image pdf** do prohledávatelné verze můžete celý PDF předat engine místo jednotlivých obrázků:

```java
engine.addPdf("YOUR_DIRECTORY/scanned-image-only.pdf");
PdfDocument searchable = engine.recognizeToPdf();
searchable.save("YOUR_DIRECTORY/searchable-from-pdf.pdf");
```

Stejné konfigurační příznaky (`PDF_SEARCHABLE` a `PdfCompression.NONE`) se použijí, takže získáte **pdf without compression** i při startu z PDF kontejneru.

## Časté úskalí & Jak se jim vyhnout

* **Zapomněli nastavit výstupní formát** – Engine ve výchozím nastavení vytváří rastrové PDF, které není prohledávatelné. Vždy zavolejte `setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE)` před `recognizeToPdf()`.  
* **Nedostatek paměti při velkých dávkách** – Načítejte a zpracovávejte stránky po částech, nebo použijte streaming API, pokud ho vaše SDK nabízí.  
* **Nesprávné cesty k souborům** – Používejte absolutní cesty nebo se ujistěte, že pracovní adresář je nastaven správně; jinak `pdf.save()` vyhodí `IOException`.  
* **Licence není aktivována** – Většina komerčních OCR SDK vyžaduje platnou licenci; engine vyhodí výjimku za běhu, pokud licence chybí.

---

## Závěr

Nyní máte kompletní, připravené řešení, které ukazuje **how to create searchable PDF** soubory z naskenovaných obrázků, jak **convert scanned image PDF**, a přesně **how to disable compression** pro vytvoření **pdf without compression**. Klíčové kroky jsou:

1. Nastavit výstupní formát na `PDF_SEARCHABLE`.  
2. Vypnout PDF kompresi pomocí `PdfCompression.NONE`.  
3. Spustit OCR a získat `PdfDocument`.  
4. Uložit soubor na disk.

Odtud můžete experimentovat s fonty, přidávat vodoznaky nebo hromadně zpracovávat celé složky. Pokud vás zajímá přidání jazykových balíčků OCR, práce s vícestránkovými TIFF nebo integrace tohoto workflow do webové služby, podívejte se na naše nadcházející tutoriály „Výběr OCR jazyků v Javě“ a „Streaming OCR pro velké sady dokumentů“.

Máte otázky nebo jste narazili na problém? Zanechte komentář níže – šťastné kódování a užívejte si nově prohledávatelná PDF!

## Co se naučíte dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Rozpoznání textu v PDF – OCR operace s Aspose.OCR pro Java](/ocr/english/java/ocr-operations/)
- [OCR rozpoznávání PDF dokumentů v Aspose.OCR pro Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Převod obrázků do PDF C# – Uložení vícestránkového OCR výsledku](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}