---
category: general
date: 2026-07-05
description: Komprimujte PDF obrázky při převodu PNG na PDF pomocí Javy. Naučte se
  předzpracování obrázků pro OCR, rozpoznávejte text v JPG a provádějte dávkové OCR
  do PDF v jednom tutoriálu.
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: cs
og_description: Komprimujte PDF obrázky a převádějte PNG na PDF pomocí Javy. Tento
  průvodce zahrnuje předzpracování obrázků pro OCR, rozpoznávání textu v JPG a hromadné
  OCR do PDF.
og_title: Komprimujte obrázky PDF pomocí Javy – kompletní průvodce dávkovým OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  headline: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  type: TechArticle
- description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  name: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints a line for each image, e.g.:'
  - name: What if my server has no GPU?
    text: Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains
      unchanged, and you still get multithreaded CPU processing.
  - name: My PDFs are still too large—can I lower the quality further?
    text: Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink
      size more aggressively but may blur fine glyphs. Test with a representative
      sample.
  - name: How do I handle other image formats (TIFF, BMP)?
    text: 'Add the extensions to the filter lambda:'
  - name: Can I keep the original color images instead of binarizing?
    text: Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder
      if you need color retention for downstream analysis.
  type: HowTo
tags:
- ocr
- java
- pdf
- image-processing
title: Komprimujte PDF obrázky v Javě – Kompletní průvodce hromadným OCR do PDF
url: /cs/java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Komprimujte obrázky PDF pomocí Javy – Kompletní průvodce hromadným OCR do PDF

Už jste někdy potřebovali **komprimovat obrázky PDF** při převodu složky PNG souborů na prohledávatelné PDF? Nejste v tom sami. V mnoha automatizačních pipelinech je největší problém sladit kvalitu obrázku, přesnost OCR a konečnou velikost PDF – a to vše najednou.

V tomto tutoriálu projdeme praktické řešení, které **převádí PNG na PDF**, aplikuje **předzpracování obrázků pro OCR** a nakonec **komprimuje obrázky PDF**, aby výstup zůstal lehký. Na konci budete vědět, jak **rozpoznat text v JPG** souborech, nastavit workflow **hromadného OCR do PDF** a udržet své PDF přehledná.

## Co se naučíte

- Nastavení Aspose OCR pro Java a aplikace licence.
- Konfigurace enginu pro vícevláknové zpracování, akceleraci GPU a korekci pravopisu.
- Vytvoření znovupoužitelné **image preprocessing for OCR** pipeline (odšumění, kontrast, binarizace).
- Použití **PdfSaveOptions** k **compress PDF images** bez ztráty čitelnosti.
- Procházení adresáře a **convert PNG to PDF** a **recognize text JPG** ve velkém měřítku.
- Kompletní, připravený Java program, který můžete vložit do libovolného projektu.

> **Požadavky**: Java 8+, Maven nebo Gradle, licence Aspose OCR pro Java a složka PNG/JPG obrázků, které chcete zpracovat.

---

## Krok 1: Aplikujte licenci Aspose OCR (nezbytné pro produkci)

Než budete moci volat jakékoli OCR API, musíte načíst platnou licenci; jinak budete omezeni zkušební verzí.

```java
import com.aspose.ocr.*;

public class LicenseSetup {
    public static void loadLicense() throws Exception {
        License license = new License();
        // Point to your license file – keep it out of source control!
        license.setLicense("Aspose.OCR.Java.lic");
    }
}
```

*Proč je to důležité*: Licencovaný engine odemyká podporu GPU, vyšší přesnost a odstraňuje vodoznaky, které by jinak nafoukly vaše PDF soubory.

---

## Krok 2: Konfigurace OCR enginu – vlákna, GPU a korekce pravopisu

Rychlý OCR engine je páteří každé úlohy **batch OCR to PDF**. Spustíme tolik vláken, kolik hostitelský CPU zvládne, povolíme akceleraci GPU (pokud máte kompatibilní kartu) a zpřesníme korekci pravopisu, aby se odstranily chyby OCR.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.GPUSettings;
import com.aspose.ocr.spell.SpellCorrectionOptions;

public class EngineConfig {
    public static OcrEngine createEngine() {
        OcrEngine ocrEngine = new OcrEngine();

        // Use all available logical processors
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Enable GPU – huge speedup for large batches
        GPUSettings gpu = new GPUSettings();
        gpu.setEnabled(true);
        ocrEngine.setGpuSettings(gpu);

        // Light spell correction: fix common typos without over‑correcting
        SpellCorrectionOptions spellOpts = new SpellCorrectionOptions();
        spellOpts.setMaxEditDistance(1);
        ocrEngine.getSpellCorrection().setOptions(spellOpts);

        return ocrEngine;
    }
}
```

*Tip*: Pokud běžíte na headless serveru bez GPU, stačí nastavit `gpu.setEnabled(false)` – kód bude stále fungovat, jen o něco pomaleji.

---

## Krok 3: Vytvoření pipeline pro předzpracování obrázků

Surové skeny často trpí šumem, nízkým kontrastem nebo nerovnoměrným osvětlením. **image preprocessing for OCR** dramaticky zvyšuje úspěšnost rozpoznání, zejména v scénářích **recognize text JPG**.

```java
import com.aspose.ocr.*;

public class PreprocessorSetup {
    public static ImagePreprocessor createPreprocessor() {
        return new ImagePreprocessor.Builder()
                .addDenoise(0.7)      // Reduce grain while preserving edges
                .addContrast(1.15)    // Boost contrast for clearer glyphs
                .addBinarize()        // Convert to black‑and‑white for OCR
                .build();
    }
}
```

*Proč je řadíme*: Nejprve odšumění zabraňuje binarizátoru v zesílení špiček; kontrast pak zajistí, že znaky vyniknou; nakonec binarizace poskytne OCR engine čistý binární obraz k práci.

---

## Krok 4: Připravte PDF Save Options – **Compress PDF Images** efektivně

Aspose vám umožňuje jemně doladit výstup PDF. Zapneme kompresi obrázků a nastavíme úroveň kvality, která vyvažuje velikost a čitelnost.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOptions {
    public static PdfSaveOptions createOptions() {
        PdfSaveOptions options = new PdfSaveOptions();
        options.setCompressImages(true);   // This is the key to compress PDF images
        options.setImageQuality(90);       // 90% retains sharp text while shrinking file size
        return options;
    }
}
```

*Výsledek*: Každé prohledávatelné PDF bude znatelně menší – ideální pro archivaci nebo odesílání e-mailem.

---

## Krok 5: Zpracování složky – **Convert PNG to PDF** a **Recognize Text JPG** v jednom cyklu

Nyní vše spojíme. Smyčka prochází vstupní adresář, spouští OCR na každém PNG nebo JPG a zapisuje prohledávatelné PDF do výstupní složky. Název PDF odráží název zdrojového obrázku.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.PdfSaveOptions;
import java.io.File;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license
        LicenseSetup.loadLicense();

        // 2️⃣ Engine & preprocessing
        OcrEngine ocrEngine = EngineConfig.createEngine();
        ocrEngine.setPreprocessor(PreprocessorSetup.createPreprocessor());

        // 3️⃣ PDF options (compress PDF images)
        PdfSaveOptions pdfOptions = PdfOptions.createOptions();

        // 4️⃣ Define input / output folders
        File inputFolder = new File("YOUR_DIRECTORY/input");
        File outputFolder = new File("YOUR_DIRECTORY/output");
        if (!outputFolder.exists()) outputFolder.mkdirs();

        // 5️⃣ Filter PNG & JPG files
        File[] imageFiles = inputFolder.listFiles((dir, name) ->
                name.toLowerCase().endsWith(".png") || name.toLowerCase().endsWith(".jpg"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG or JPG files found in the input folder.");
            return;
        }

        // 6️⃣ Process each file
        for (File image : imageFiles) {
            // Recognize text – works for both PNG and JPG
            ocrEngine.recognizeImage(image.getAbsolutePath());

            // Build output PDF path (same base name)
            String pdfPath = outputFolder.getAbsolutePath() + File.separator +
                    image.getName().replaceAll("\\.(png|jpg)$", ".pdf");

            // Save as searchable PDF – this step also compresses images
            ocrEngine.saveAsSearchablePdf(pdfPath, pdfOptions);

            System.out.println("✅ Processed: " + image.getName() + " → " + pdfPath);
        }

        System.out.println("🎉 All files have been converted and compressed!");
    }
}
```

### Očekávaný výstup

Spuštění programu vypíše řádek pro každý obrázek, např.:

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

Otevřete libovolné výsledné PDF v prohlížeči a uvidíte vybratelný, prohledávatelný text, zatímco velikost souboru je typicky **o 30‑50 % menší** než u nekomprimovaného protějšku.

---

## Časté otázky a okrajové případy

### Co když můj server nemá GPU?

Stačí nastavit `gpuSettings.setEnabled(false)`. Zbytek pipeline zůstane beze změny a stále získáte vícevláknové zpracování CPU.

### Moje PDF jsou stále příliš velká – mohu dále snížit kvalitu?

Ano. Upravte `options.setImageQuality(70)` nebo i `50`. Nižší hodnoty velikost zmenší agresivněji, ale mohou rozmazat jemné glyfy. Otestujte na reprezentativním vzorku.

### Jak zacházet s dalšími formáty obrázků (TIFF, BMP)?

Přidejte přípony do lambda filtru:

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

### Mohu zachovat originální barevné obrázky místo binarizace?

Nahraďte `.addBinarize()` za `.addGrayscale()` v builderu preprocessoru, pokud potřebujete zachovat barvu pro následnou analýzu.

---

## Profesionální tipy pro produkčně připravené hromadné OCR

- **Memory management**: Znovupoužijte jedinou instanci `OcrEngine` (jak je ukázáno), abyste se vyhnuli režii vytváření/ničení objektů pro každý obrázek.
- **Error handling**: Zabalte blok pro každý soubor do `try/catch`, abyste zaznamenali selhání bez přerušení celého batch procesu.
- **Logging**: Používejte správný logging framework (SLF4J, Log4j) místo `System.out.println` pro škálovatelná řešení.
- **Parallelism**: Pro obrovské složky zvažte zpracování podadresářů v paralelních streamech, ale sledujte soutěž o GPU.
- **Security**: Uložte licenční soubor mimo repozitář a chraňte jej pomocí oprávnění souborového systému.

---

## Závěr

Právě jsme ukázali, jak **komprimovat obrázky PDF** při provádění **batch OCR to PDF** konverze, která **convert PNG to PDF**, **recognize text JPG**, a používá robustní pipeline **image preprocessing for OCR**. Kompletní Java program je samostatný, běží na jakémkoli moderním JDK a vytváří lehká prohledávatelná PDF připravená k archivaci nebo následné analýze.

Další kroky? Experimentujte s různými parametry předzpracování, vyzkoušejte OCR jazyky jiné než angličtinu, nebo integrujte workflow do Spring Boot microservice, který sleduje složku a zpracovává soubory za běhu. Základní koncepty – načítání licence, konfigurace enginu, předzpracování a komprese PDF – zůstávají stejné a poskytují pevný základ pro jakýkoli OCR‑řízený projekt.

Máte otázky nebo chcete sdílet své úpravy? Zanechte komentář níže a šťastné programování!

![Diagram hromadného OCR workflow zobrazující vstupní obrázky, předzpracování, OCR engine a komprimovaný výstup PDF](alt="Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output")

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Rozpoznat text PDF – OCR operace s Aspose.OCR pro Java](/ocr/english/java/ocr-operations/)
- [rozpoznat textový obrázek s Aspose OCR – Kompletní Java OCR tutoriál](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Převést obrázek na text v Javě pomocí Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}