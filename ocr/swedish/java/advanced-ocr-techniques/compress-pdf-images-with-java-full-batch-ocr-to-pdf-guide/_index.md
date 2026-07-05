---
category: general
date: 2026-07-05
description: Komprimera PDF‑bilder när du konverterar PNG till PDF med Java. Lär dig
  bildförbehandling för OCR, känna igen text i JPG och batch‑OCR till PDF i en tutorial.
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: sv
og_description: Komprimera PDF‑bilder och konvertera PNG till PDF med Java. Den här
  guiden täcker bildförbehandling för OCR, känna igen text i JPG och batch‑OCR till
  PDF.
og_title: Komprimera PDF-bilder med Java – Komplett batch-OCR-handledning
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
title: Komprimera PDF‑bilder med Java – Fullständig batch‑OCR till PDF‑guide
url: /sv/java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Komprimera PDF‑bilder med Java – Fullständig batch‑OCR‑till‑PDF‑guide

Har du någonsin behövt **komprimera PDF‑bilder** samtidigt som du omvandlar en mapp med PNG‑filer till sökbara PDF‑filer? Du är inte ensam. I många automatiseringspipeline är den största smärtan att jonglera bildkvalitet, OCR‑noggrannhet och slutlig PDF‑storlek – allt på en gång.  

I den här handledningen går vi igenom en praktisk lösning som **konverterar PNG till PDF**, applicerar **bildförbehandling för OCR**, och slutligen **komprimerar PDF‑bilder** så att resultatet förblir lättviktigt. När du är klar vet du hur du **läser av text i JPG‑filer**, sätter upp ett **batch‑OCR‑till‑PDF**‑arbetsflöde, och håller dina PDF‑filer prydliga.

## Vad du kommer att lära dig

- Installera Aspose OCR för Java och applicera en licens.
- Konfigurera motorn för flertrådad körning, GPU‑acceleration och stavningskorrigering.
- Bygga en återanvändbar **bildförbehandling för OCR**‑pipeline (brusreducering, kontrast, binarisering).
- Använda **PdfSaveOptions** för att **komprimera PDF‑bilder** utan att offra läsbarhet.
- Loopa igenom en katalog för att **konvertera PNG till PDF** och **läsa av text i JPG** i bulk.
- Ett komplett, färdigt‑att‑köra Java‑program som du kan släppa in i vilket projekt som helst.

> **Förutsättningar**: Java 8+, Maven eller Gradle, en Aspose OCR för Java‑licens, och en mapp med PNG/JPG‑bilder som du vill bearbeta.

---

## Steg 1: Applicera Aspose OCR‑licensen (Viktigt för produktion)

Innan du kan anropa några OCR‑API:er måste du ladda en giltig licens; annars fastnar du med provbegränsningar.

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

*Varför detta är viktigt*: En licensierad motor låser upp GPU‑stöd, högre noggrannhet och tar bort vattenstämplar som annars skulle göra dina PDF‑filer onödigt stora.

---

## Steg 2: Konfigurera OCR‑motorn – Trådar, GPU och stavningskorrigering

En snabb OCR‑motor är ryggraden i varje **batch‑OCR‑till‑PDF**‑jobb. Vi startar så många trådar som värdens CPU klarar av, aktiverar GPU‑acceleration (om du har ett kompatibelt kort), och skärper stavningskorrigeringen för att rensa upp OCR‑fel.

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

*Proffstips*: Om du kör på en huvudlös server utan GPU, sätt bara `gpu.setEnabled(false)` – koden fungerar fortfarande, bara lite långsammare.

---

## Steg 3: Bygg en bildförbehandlings‑pipeline

Råa skanningar lider ofta av brus, låg kontrast eller ojämn belysning. **Bildförbehandling för OCR** förbättrar avsevärt igenkänningsgraden, särskilt i **läsa av text i JPG**‑scenarier.

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

*Varför vi kedjar dessa*: Brusreducering först förhindrar att binariseringen förstärker fläckar; kontrast säkerställer att tecken framträder; slutligen ger binariseringen OCR‑motorn en ren binär bild att arbeta med.

---

## Steg 4: Förbered PDF‑spara‑alternativ – **Komprimera PDF‑bilder** effektivt

Aspose låter dig finjustera PDF‑utdata. Vi slår på bildkomprimering och ställer in en kvalitetsnivå som balanserar storlek och läsbarhet.

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

*Resultat*: Varje sökbar PDF blir märkbart mindre – idealiskt för arkivering eller utskick via e‑post.

---

## Steg 5: Bearbeta mappen – **Konvertera PNG till PDF** och **läsa av text i JPG** i en loop

Nu sätter vi ihop allt. Loopen går igenom en inmatningskatalog, kör OCR på varje PNG eller JPG, och skriver en sökbar PDF till en utmatningsmapp. PDF‑namnet speglar källbildens namn.

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

### Förväntad utdata

När programmet körs skrivs en rad för varje bild, t.ex.:

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

Öppna någon av de resulterande PDF‑filerna i en visare så ser du markerbar, sökbar text medan filstorleken vanligtvis är **30‑50 % mindre** än en icke‑komprimerad motsvarighet.

---

## Vanliga frågor & kantfall

### Vad händer om min server saknar GPU?
Sätt bara `gpuSettings.setEnabled(false)`. Resten av pipelinen förblir oförändrad, och du får fortfarande flertrådad CPU‑bearbetning.

### Mina PDF‑filer är fortfarande för stora – kan jag sänka kvaliteten ytterligare?
Ja. Justera `options.setImageQuality(70)` eller till och med `50`. Lägre värden minskar storleken mer aggressivt men kan göra fina tecken suddiga. Testa med ett representativt urval.

### Hur hanterar jag andra bildformat (TIFF, BMP)?
Lägg till filändelserna i filter‑lambda‑uttrycket:

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

Samma förbehandlingspipeline fungerar för de flesta rasterformat.

### Kan jag behålla originalfärgbilderna istället för att binarisera?
Byt ut `.addBinarize()` mot `.addGrayscale()` i preprocessor‑buildern om du behöver färgbevarande för vidare analys.

---

## Proffstips för produktionsklar batch‑OCR

- **Minneshantering**: Återanvänd en enda `OcrEngine`‑instans (som visat) för att undvika overhead av att skapa/förstöra objekt per bild.
- **Felhantering**: Wrappa per‑fil‑blocket i ett `try/catch` för att logga misslyckanden utan att avbryta hela batchen.
- **Loggning**: Använd ett riktigt loggningsramverk (SLF4J, Log4j) istället för `System.out.println` för skalbara lösningar.
- **Parallellism**: För enorma mappar, överväg att bearbeta underkataloger i parallella streams, men håll ett öga på GPU‑konkurrens.
- **Säkerhet**: Förvara licensfilen utanför kodförrådet och skydda den med filsystembehörigheter.

---

## Slutsats

Vi har just demonstrerat hur man **komprimerar PDF‑bilder** samtidigt som man utför en **batch‑OCR‑till‑PDF**‑konvertering som **konverterar PNG till PDF**, **läser av text i JPG**, och använder en robust **bildförbehandling för OCR**‑pipeline. Det kompletta Java‑programmet är självständigt, körs på vilken modern JDK som helst, och producerar lätta sökbara PDF‑filer redo för arkivering eller vidare analys.

Nästa steg? Experimentera med olika förbehandlingsparametrar, prova OCR‑språk annat än engelska, eller integrera arbetsflödet i en Spring Boot‑mikrotjänst som övervakar en katalog och bearbetar filer i realtid. De grundläggande koncepten – licensladdning, motorinställning, förbehandling och PDF‑komprimering – förblir desamma, vilket ger dig en solid grund för alla OCR‑drivna projekt.

Har du frågor eller vill dela dina egna justeringar? lämna en kommentar nedan, och lycka till med kodandet!

![Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output](alt="Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output")

## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}