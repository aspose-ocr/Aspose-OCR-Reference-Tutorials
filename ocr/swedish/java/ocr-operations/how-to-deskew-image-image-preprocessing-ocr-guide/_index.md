---
category: general
date: 2026-06-22
description: 'Hur man räta upp bild för OCR: lär dig bildförbehandlingens OCR‑steg,
  ta bort salt‑och‑peppar‑brus och öka noggrannheten.'
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: sv
og_description: Hur man korrigerar bildens lutning för OCR, tar bort salt‑och‑peppar‑brus
  och använder förbehandlingstekniker för OCR i ett komplett Java‑exempel.
og_title: Hur man räta upp bild – Bildförbehandling OCR-guide
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: 'How to deskew image for OCR: learn image preprocessing OCR steps,
    remove salt pepper noise, and boost accuracy.'
  headline: How to Deskew Image – Image Preprocessing OCR Guide
  type: TechArticle
tags:
- OCR
- image-processing
- Java
title: Hur man räta upp en bild – Bildförbehandling för OCR-guide
url: /sv/java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man räta upp bild – Bildförbehandling OCR‑guide

Har du någonsin funderat **hur man räta upp bild** så att din OCR‑motor faktiskt läser texten? Du är inte ensam. En sned skanning kan förvandla ett perfekt dokument till ett rörigt kaos, och de flesta utvecklare stöter på det åtminstone en gång.

I den här handledningen går vi igenom en komplett **image preprocessing OCR**‑pipeline som inte bara korrigerar rotation utan också **remove[s] salt pepper**‑artefakter och ökar kontrasten – i princip allt du behöver för att **preprocess images OCR**‑stil innan du matar in dem i motorn. I slutet har du ett färdigt Java‑exempel och en klar mental modell för varför varje steg är viktigt.

## Hur man räta upp bild – Bygga förbehandlings‑pipeline

Kärnan i alla OCR‑vänliga arbetsflöden är ett **preprocess options**‑objekt som kedjar ihop en serie filter. Tänk på det som ett löpande band: varje filter utför en uppgift och skickar sedan bilden vidare till nästa. Nedan är ett minimalt men komplett exempel med ett hypotetiskt OCR‑bibliotek som levereras med `DeskewFilter`, `DenoiseFilter` och `ContrastBoostFilter`.

```java
import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.DeskewFilter;
import com.example.ocr.filters.DenoiseFilter;
import com.example.ocr.filters.ContrastBoostFilter;

/**
 * Demonstrates how to deskew image and apply common OCR preprocessing steps.
 */
public class OcrPreprocessDemo {

    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine (replace with your actual implementation)
        Engine engine = new Engine();

        // 2️⃣ Build the preprocessing pipeline
        ImagePreprocessOptions preprocessOptions = new ImagePreprocessOptions();

        // 2a️⃣ Deskew – correct rotation up to ±15°
        preprocessOptions.addFilter(new DeskewFilter(15));

        // 2b️⃣ Denoise – remove salt‑and‑pepper noise
        preprocessOptions.addFilter(new DenoiseFilter());

        // 2c️⃣ Contrast boost – make low‑contrast scans more readable
        preprocessOptions.addFilter(new ContrastBoostFilter(1.5f));

        // 3️⃣ Attach the pipeline to the engine
        engine.setPreprocessOptions(preprocessOptions);

        // 4️⃣ Run OCR on a sample image
        String result = engine.recognizeText("sample-scanned-page.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== OCR RESULT ===");
        System.out.println(result);
    }
}
```

### Varför detta fungerar

* **DeskewFilter** analyserar bildens dominerande textrader, uppskattar vinkeln och roterar bitmapen tillbaka till horisontell. De flesta bibliotek begränsar korrigeringen till ±15° eftersom större vinklar oftast indikerar en dåligt skannad sida som kräver manuell åtgärd.
* **DenoiseFilter** riktar in sig på det klassiska *salt‑and‑pepper*‑mönstret – de isolerade svarta eller vita pixlarna som ser ut som brus på en TV. Att ta bort dem förhindrar att OCR‑motorn misstar brus för tecken.
* **ContrastBoostFilter** sträcker histogrammet, så att svaga streck framträder tydligare. En multiplikator på `1.5f` är ett säkert standardvärde; du kan öka den om dina skanningar är särskilt urtvättade.

> **Proffstips:** Om du vet att dina dokument aldrig överstiger en 10° lutning, skicka den mindre gränsen till `DeskewFilter` – algoritmen kör snabbare och tenderar mindre att överkorrigera.

## Image Preprocessing OCR: Lägga till filter i rätt ordning

Ordningen är viktig. Föreställ dig att du avlägsnar brus *innan* du räter upp bilden; bruset kan störa vinkeldetektionen och leda till ett feljusterat resultat. Omvänt, att applicera kontrastökning *efter* räta upp säkerställer att rotationen inte introducerar nya artefakter.

Nedan är en snabb checklista som du kan kopiera‑klistra in i vilket projekt som helst:

| Steg | Filter | Orsak |
|------|--------|-------|
| 1 | `DeskewFilter` | Justerar textbaslinjen |
| 2 | `DenoiseFilter` | Tar bort isolerat pixelbrus |
| 3 | `ContrastBoostFilter` | Förbättrar läsbarheten för OCR |

Om du behöver infoga ytterligare steg – exempelvis ett **binariserings**‑filter för binär OCR – placerar du det **efter** kontrastökningen, eftersom en ren, hög‑kontrast bild binariseras mer exakt.

## Ta bort salt‑pepper‑brus med DenoiseFilter

Salt‑och‑pepper‑brus är notoriskt i lågkvalitativa skanningar, särskilt de som kommer från billiga telefonkameror. `DenoiseFilter` i vårt bibliotek implementerar en median‑filter‑kärna som ersätter varje pixel med medianen av dess omgivande grannskap. Effekten? De där fläckarna försvinner utan att sudda ut själva tecknen.

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*När ska kernel‑storleken ökas?* Om dina källbilder är fyllda med stora fläckar, kommer en större kärna att rensa dem, men var försiktig: för stor kan börja radera fina streck i små teckensnitt.

## Preprocess Images OCR – Applicera pipelinen

När du har byggt filterkedjan är det en en‑radersats (`engine.setPreprocessOptions`) för att fästa den på motorn. Från och med då kör varje anrop till `recognizeText` automatiskt genom pipelinen. Du behöver inte manuellt anropa varje filter – din kod förblir prydlig, och framtida förändringar (lägga till ett nytt filter, justera parametrar) är centraliserade.

Här är hur ett lyckat körning ser ut med ett exempel‑scan som ursprungligen hade en 12° lutning och märkbart pepper‑brus:

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Lägg märke till hur texten är ren, korrekt orienterad och fri från stray‑tecken som annars skulle ha dykt upp som “I n v o i c e” eller “$‑‑‑”.

## Edge Cases & Vanliga fallgropar

| Situation | Vad att hålla utkik efter | Föreslagen åtgärd |
|-----------|---------------------------|-------------------|
| Rotation > 15° | DeskewFilter kan ge upp | Förrotera manuellt eller använd ett filter med större intervall |
| Extremt låg upplösning (< 100 dpi) | Kontrastökning kan inte återställa detaljer | Resampla bilden först (t.ex. `ResampleFilter`) |
| Blandat brus (Gaussian + salt‑pepper) | DenoiseFilter ensam räcker inte | Kedja ett `GaussianBlurFilter` före `DenoiseFilter` |
| Färgsökningar med färgad text | Gråskalakonvertering behövs | Infoga `GrayscaleFilter` före kontrastökning |

Genom att förutse dessa scenarier sparar du timmar av felsökning senare.

## Fullt fungerande exempel (All‑in‑One)

Nedan är en självständig Java‑klass som du kan släppa in i vilket Maven‑ eller Gradle‑projekt som helst som inkluderar `com.example.ocr`‑beroendet. Den demonstrerar **hur man räta upp bild**, **remove salt pepper**‑brus och **preprocess images OCR**‑stil.

```java
package com.myapp.demo;

import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.*;

public class CompleteOcrPipeline {

    public static void main(String[] args) {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine (replace with your own)
        // -------------------------------------------------
        Engine engine = new Engine();

        // -------------------------------------------------
        // 2️⃣ Configure preprocessing pipeline
        // -------------------------------------------------
        ImagePreprocessOptions options = new ImagePreprocessOptions();

        // Deskew up to ±15° – the core of "how to deskew image"
        options.addFilter(new DeskewFilter(15));

        // Remove salt‑and‑pepper artifacts
        options.addFilter(new DenoiseFilter());

        // Boost contrast by 1.5× to aid OCR recognition
        options.addFilter(new ContrastBoostFilter(1.5f));

        // (Optional) Convert to grayscale – often improves OCR accuracy
        options.addFilter(new GrayscaleFilter());

        // Attach the pipeline
        engine.setPreprocessOptions(options);

        // -------------------------------------------------
        // 3️⃣ Perform OCR on a test file
        // -------------------------------------------------
        String imagePath = "src/main/resources/scanned-document.png";
        String text = engine.recognizeText(imagePath);

        // -------------------------------------------------
        // 4️⃣ Show the result
        // -------------------------------------------------
        System.out.println("=== OCR RESULT ===");
        System.out.println(text);
    }
}
```

**Förväntad output** (förutsatt att `scanned-document.png` innehåller en tydlig faktura):

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

Om du byter ut bilden mot en som redan är perfekt inriktad, kommer du märka att pipelinen fortfarande körs – inget kraschar, och OCR‑noggrannheten förblir hög.

## Slutsats

Du har nu en solid förståelse för **hur man räta upp bild** och varför varje förbehandlingssteg – **image preprocessing OCR**, **remove salt pepper** och **preprocess images OCR** – spelar en avgörande roll för att leverera ren, sökbar text. Exemplet ovan är komplett,

## Vad bör du lära dig härnäst?

De följande handledningarna täcker nära besläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Calculate Skew Angle for OCR Image Preprocessing](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}