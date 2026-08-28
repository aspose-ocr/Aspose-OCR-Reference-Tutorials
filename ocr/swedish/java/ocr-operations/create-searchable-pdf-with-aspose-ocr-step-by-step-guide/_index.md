---
category: general
date: 2026-01-02
description: Skapa sökbar PDF från en skannad bild‑PDF med Aspose OCR. Lär dig att
  ställa in OCR‑språk, bädda in ett textlager i PDF och använda högkomprimeringsalternativ
  för PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- high compression pdf
- embed text layer pdf
- set OCR language
language: sv
og_description: Skapa sökbara PDF-filer snabbt. Den här guiden visar hur du konverterar
  skannade bild‑PDF:er, bäddar in ett textlager, ställer in OCR-språk och möjliggör
  högkomprimerade PDF-filer.
og_title: Skapa sökbar PDF med Aspose OCR – Komplett guide
tags:
- Aspose OCR
- Java PDF
- Document Automation
title: Skapa sökbar PDF med Aspose OCR – Steg‑för‑steg‑guide
url: /sv/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa sökbar PDF – Komplett programmeringshandledning

Har du någonsin behövt **create searchable PDF**‑filer från skannade bilder men inte vetat var du ska börja? Du är inte ensam. I många dokumenttunga arbetsflöden är en ren bild‑endast PDF en återvändsgränd för sökning och indexering.  

Den goda nyheten är att du med Aspose OCR kan **convert scanned image PDF** till ett fullt sökbart dokument med bara några rader Java. Den här handledningen guidar dig genom varje steg — initiering av OCR‑motorn, konfiguration av high compression PDF‑inställningar, inbäddning av ett dolt textlager och även val av rätt OCR‑språk.  

När du är klar med den här guiden har du ett körbart program som producerar en searchable PDF, en fil du kan släppa in i vilken sökmotor eller dokumenthanteringssystem som helst utan problem.

---

## Skapa sökbar PDF – Översikt

Innan vi dyker ner i koden, låt oss klargöra vad “create searchable PDF” faktiskt betyder. En searchable PDF innehåller två parallella lager:

1. **Visual layer** – den ursprungliga skannade bilden (eller renderade sidan).  
2. **Text layer** – osynliga men maskinläsbara tecken som extraheras av OCR.  

När du öppnar en sådan PDF i Adobe Reader och markerar text, interagerar du faktiskt med det dolda textlagret, inte bilden. Denna dubbellager‑metod är vad som möjliggör **embed text layer PDF**‑funktionaliteten.

---

## Konvertera skannad bild‑PDF med Aspose OCR

Det första du behöver är en skannad bild (PNG, JPEG, TIFF) som du vill omvandla till en PDF. Aspose OCR kan läsa den bilden, köra OCR och överlämna resultatet till en PDF‑skrivare.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Step 2: Configure PDF save options to embed a searchable text layer
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // enable searchable PDF
        pdfSaveOptions.setCompressionLevel(9);        // optional: high compression

        // Step 3: Perform OCR on the scanned image and save the result as a searchable PDF
        ocrEngine.recognizeImageAndSave(
                "YOUR_DIRECTORY/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,                // set OCR language
                "YOUR_DIRECTORY/output.pdf",                // output PDF file
                pdfSaveOptions);                            // options defined above

        // Step 4: Indicate that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

**Varför detta fungerar:**  
- `setCreateSearchablePdf(true)` talar om för Aspose att generera det dolda textlagret, vilket uppfyller kravet **embed text layer pdf**.  
- `setCompressionLevel(9)` skjuter filen in i **high compression pdf**‑intervallet, vilket minskar den slutliga storleken utan att kompromissa med OCR‑noggrannheten.  
- `RecognitionLanguage.ENGLISH`‑argumentet visar hur man **set OCR language**; du kan byta ut det mot franska, tyska osv., beroende på ditt källmaterial.

---

## Inställningar för hög komprimering av PDF

Stora skannade PDF‑filer kan snabbt växa till hundratals megabyte. Aspose erbjuder ett enkelt komprimerings‑API som fungerar på PDF‑nivå. Metoden `setCompressionLevel` accepterar värden från 0 (ingen komprimering) till 9 (maximal komprimering).  

```java
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.setCompressionLevel(9); // 9 = strongest compression
```

Tips:

- **Använd förlustfria bildformat** (PNG) för texttunga skanningar; JPEG är bättre för foton.  
- **Aktivera font‑subsetting** om du bäddar in egna typsnitt — Aspose gör detta automatiskt när du skapar en searchable PDF.  
- **Testa utdata‑storleken** efter varje förändring; ibland ger en nivå‑8 komprimering dig en 10 % minskning med försumbar kvalitetsförlust jämfört med nivå 9.

---

## Inbädda textlager‑PDF för sökbarhet

Om du hoppar över anropet `setCreateSearchablePdf(true)`, kommer den resulterande filen att se bra ut men du kommer inte kunna söka i dess innehåll. Det dolda textlagret skapas genom att mappa varje igenkänd tecken till dess position på sidan.  

```java
pdfSaveOptions.setCreateSearchablePdf(true);
```

**Vad du bör vara uppmärksam på:**  

- **Dokument med blandade språk** – du kan behöva köra OCR två gånger, en gång per språk, och sedan slå ihop textlagren.  
- **Komplexa layouter** (tabeller, flerkolumn) – Aspose gör ett bra jobb, men dubbelkolla resultatet med en PDF‑visare som visar dolt text (t.ex. Adobe Acrobats “Edit PDF”-läge).

---

## Ställ in OCR‑språk för exakt igenkänning

OCR‑motorns noggrannhet beror på vilket språk du förväntar den på. Aspose levereras med ett antal inbyggda språk, och du kan även lägga till egna språkpaket.

```java
ocrEngine.recognizeImageAndSave(
        "input.png",
        RecognitionLanguage.ENGLISH, // change to RecognitionLanguage.FRENCH, etc.
        "output.pdf",
        pdfSaveOptions);
```

**När du bör byta språk:**  

- Dokument innehåller **icke‑latinska skript** (kyrilliska, arabiska) – byt till lämplig `RecognitionLanguage`.  
- Sidor med blandade språk – du kan anropa `recognizeImageAndSave` två gånger, varje gång med ett annat språk, och sedan slå ihop PDF‑filerna.

---

## Köra det kompletta exemplet

Nedan är det fullständiga, färdiga programmet. Ersätt platshållar‑sökvägarna med faktiska filplatser, se till att Aspose OCR‑JAR‑filen finns i din classpath, och kör.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Configure PDF save options
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // embed text layer PDF
        pdfSaveOptions.setCompressionLevel(9);        // high compression PDF

        // Perform OCR and save searchable PDF
        ocrEngine.recognizeImageAndSave(
                "C:/scans/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,          // set OCR language
                "C:/output/searchable.pdf",           // output PDF
                pdfSaveOptions);                      // options defined above

        System.out.println("Searchable PDF created.");
    }
}
```

**Förväntad utskrift:** När du kör programmet skriver konsolen ut:

```
Searchable PDF created.
```

Öppna `searchable.pdf` i någon PDF‑visare, försök markera text, och du kommer att se det osynliga lagret i aktion. Du har framgångsrikt **create searchable pdf** från en skannad bild.

![exempel på skapa sökbar pdf](image-placeholder.png "exempel på skapa sökbar pdf")

*Skärmdumpen ovan (platshållare) skulle vanligtvis visa PDF‑visaren med markerbar text över en skannad sida.*

---

## Slutsats

Vi har gått igenom allt du behöver för att **create searchable PDF**‑filer med Aspose OCR:

- Initiera OCR‑motorn.  
- **Convert scanned image PDF** genom att mata in en PNG/JPEG i `recognizeImageAndSave`.  
- Använd `setCreateSearchablePdf(true)` för att **embed text layer PDF**.  
- Applicera `setCompressionLevel(9)` för en **high compression PDF** som förblir lätt.  
- Välj rätt `RecognitionLanguage` för att **set OCR language** för maximal noggrannhet.

Härifrån kan du experimentera med batch‑behandling, olika språk, eller till och med kombinera flera skannade sidor till en enda searchable PDF. Samma mönster fungerar för andra språk som spanska eller japanska — byt bara `RecognitionLanguage`‑enum.

Känn dig fri att lämna en kommentar om du stöter på problem, och lycka till med kodningen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}