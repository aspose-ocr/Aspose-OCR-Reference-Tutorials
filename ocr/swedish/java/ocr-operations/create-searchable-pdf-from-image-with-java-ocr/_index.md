---
category: general
date: 2026-04-26
description: Skapa sökbar PDF från en bild med Aspose OCR i Java. Lär dig att konvertera
  bild till PDF, OCR-bild till PDF och extrahera text från bilden snabbt.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- extract text from image
- how to set language
language: sv
og_description: Skapa sökbar PDF från en bild med Aspose OCR. Denna guide visar hur
  du konverterar en bild till PDF, OCR:ar en bild till PDF och extraherar text från
  bilden.
og_title: Skapa sökbar PDF från bild med Java OCR
tags:
- Java
- OCR
- PDF
title: Skapa sökbar PDF från bild med Java OCR
url: /sv/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa sökbar PDF från bild med Java OCR

Har du någonsin behövt **skapa sökbar PDF** från en skannad faktura men varit osäker på var du ska börja? Du är inte ensam—många utvecklare stöter på detta hinder när de vill ha en PDF som du faktiskt kan söka i. Den goda nyheten? Med Aspose OCR för Java kan du **konvertera bild till PDF**, köra OCR i realtid och få en prydlig sökbar fil med bara några rader kod.

I den här handledningen går vi igenom hela processen: ladda en bild, tala om för motorn vilket språk som förväntas, utföra OCR och slutligen spara en **sökbar PDF**. I slutet kommer du också att veta hur du **extraherar text från bild** manuellt, justerar språkinställningar och hanterar ett par vanliga kantfall. Inga externa tjänster, inga obskyra kommandoradsverktyg—bara ren Java.

## Vad du behöver

- Java 17 eller senare (API:et fungerar även med äldre versioner, men 17 är den optimala versionen).  
- Aspose OCR för Java‑biblioteket – du kan hämta den senaste JAR‑filen från Maven Central (`com.aspose:aspose-ocr:23.10`).  
- En bildfil som innehåller läsbar text (en PNG, JPG eller TIFF fungerar).  
- Lite tålamod med IDE:n—IntelliJ IDEA eller VS Code räcker.

Om du redan har detta, bra! Om inte, kommer Maven‑snutten nedan att få dig igång:

```xml
<!-- Add to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Nu när grunderna är lagda, låt oss dyka ner i koden.

## Steg 1: Initiera OCR‑motorn – hjärtat i **create searchable pdf**

Innan någon konvertering sker måste du skapa en `OcrEngine`‑instans. Tänk på den som hjärnan som läser pixlarna och omvandlar dem till tecken.

```java
import com.aspose.ocr.*;

public class PdfExportDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

*Varför detta är viktigt:* Motorn innehåller alla igenkänningsinställningar (språk, noggrannhetsläge osv.). Att instansiera den en gång och återanvända den för flera bilder är mer effektivt än att skapa en ny motor för varje fil.

## Steg 2: **How to set language** – förbättra noggrannheten för franska, tyska eller något skriftsystem

Om du känner till språket i källdokumentet, tala om det för OCR‑motorn. Detta snabbar upp bearbetningen och minskar felaktiga igenkänningar.

```java
        // Step 2: (Optional) Specify the language to improve text extraction
        ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.FRENCH);
```

Du kan ersätta `OcrLanguage.FRENCH` med `ENGLISH`, `SPANISH`, `GERMAN` osv. När du är osäker, utelämna raden och låt Aspose gissa—men förvänta dig en liten minskning i noggrannhet.

## Steg 3: Ladda bilden du vill **convert image to pdf**

```java
        // Step 3: Load the image that contains the text to be recognized
        ocrEngine.setImage("YOUR_DIRECTORY/french_invoice.png");
```

`setImage`‑metoden accepterar en filsökväg, `InputStream` eller till och med ett `java.awt.Image`‑objekt. Om du har en byte‑array (t.ex. från en webbladdning), paketera den i en `ByteArrayInputStream` och skicka den direkt.

## Steg 4: Utför OCR och **ocr image to pdf** i ett anrop

Aspose gör detta steg smärtfritt: `recognizeToPdf` kör igenkänningsmotorn och skriver en sökbar PDF i ett svep.

```java
        // Step 4: Recognize the text and save it as a searchable PDF
        ocrEngine.recognizeToPdf("YOUR_DIRECTORY/french_invoice_searchable.pdf");
```

Bakom kulisserna skapar biblioteket ett osynligt textlager som matchar den ursprungliga bilden. När du öppnar den resulterande filen i Adobe Reader kan du skriva ett ord i sökfältet och omedelbart hoppa till den matchande platsen.

## Steg 5: Verifiera resultatet – hur ser utdata ut?

```java
        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF generated.");
    }
}
```

Kör programmet, öppna sedan `french_invoice_searchable.pdf`. Försök söka efter ett ord du vet finns i fakturan (t.ex. “Total”). Om markeringen hamnar på rätt ställe har du lyckats **create searchable pdf**.  
![Exempel på sökbar PDF](example.png)<!-- alt text includes primary keyword -->

### Förväntad utdata

```
Searchable PDF generated.
```

Och en PDF‑fil i `YOUR_DIRECTORY` som du kan dela, indexera eller arkivera.

## Steg 6: Extrahera råtext från bilden (valfritt)

Ibland behöver du ren text för vidare bearbetning—kanske för att mata in i en databas eller köra en sentimentanalys. Aspose låter dig hämta den igenkända texten direkt:

```java
        // Optional: Get the extracted text as a String
        String extractedText = ocrEngine.getText();
        System.out.println("Extracted text:");
        System.out.println(extractedText);
```

Detta kodsnutt demonstrerar **extract text from image** utan att skapa en PDF. Det är praktiskt när du bara bryr dig om innehållet, inte den visuella layouten.

## Hantera flera sidor eller bilder

Vad händer om din källa är en flersidig TIFF eller en mapp med JPEG‑filer? Du kan loopa över filerna och anropa `recognizeToPdf` för varje, sedan slå ihop PDF‑erna med Aspose PDF eller något annat bibliotek. Här är ett snabbt mönster:

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

**Pro tip:** Ta bort de temporära PDF‑erna efter sammanslagning för att hålla arbetsytan prydlig.

## Vanliga fallgropar och hur du undviker dem

- **Lågrelösningsbilder:** OCR‑noggrannheten sjunker dramatiskt under 150 dpi. Skala upp eller begär en högre upplösning om möjligt.  
- **Snedvridna sidor:** En roterad bild kan förvirra motorn. Använd `ocrEngine.getImagePreprocessingSettings().setDeskew(true)` för att automatiskt korrigera mild snedvridning.  
- **Ej stödd språk:** Se till att språket du anger är inkluderat i din Aspose OCR‑licens; annars faller motorn tillbaka till engelska.  
- **Stora filer:** Att bearbeta en 30 MB TIFF kan vara minneskrävande. Överväg att dela upp den i mindre delar eller öka JVM‑heapen (`-Xmx2g`).

## Nästa steg – vart du går härifrån

Nu när du behärskar grunderna i **create searchable pdf**, kanske du vill utforska:

- **Batchkonvertering:** Kombinera flersidiga mönstret med en schemaläggare för att bearbeta inkommande skanningar varje natt.  
- **Metadata‑injektion:** Använd Aspose PDF för att lägga till titel, författare eller anpassade taggar till den sökbara PDF‑en.  
- **Digitala signaturer:** Säkra PDF‑en med ett certifikat efter OCR, vilket säkerställer efterlevnad för juridiska dokument.  

Alla dessa tillägg bygger fortfarande på de grundläggande koncept vi gick igenom: initiera OCR‑motorn, eventuellt ange språk, ladda bilden och anropa `recognizeToPdf`.

---

### TL;DR

Vi gick igenom ett komplett, körbart exempel som visar hur man **create searchable PDF** från en bild med Aspose OCR för Java. Stegen inkluderar att initiera motorn, eventuellt ange språk (svar på “how to set language”), ladda bilden, utföra OCR, spara en sökbar PDF och eventuellt extrahera ren text. Vi täckte också hantering av flera sidor, vanliga fallgropar och idéer för vidare automatisering.

Prova det med dina egna kvitton, kontrakt eller handskrivna anteckningar—förvandla dessa statiska bilder till fullt sökbara dokument på sekunder. Lycka till med kodningen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}