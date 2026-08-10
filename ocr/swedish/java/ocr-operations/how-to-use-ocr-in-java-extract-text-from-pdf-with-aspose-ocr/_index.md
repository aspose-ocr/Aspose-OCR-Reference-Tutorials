---
category: general
date: 2026-02-17
description: Hur man använder OCR i Java för att extrahera text från PDF, konvertera
  PDF till bilder och utföra OCR på skannade PDF-filer med Aspose.OCR.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- convert pdf to images
- perform OCR on pdf
- recognize scanned pdf
language: sv
og_description: Hur man använder OCR i Java för att extrahera text från PDF-filer.
  Lär dig att konvertera PDF till bilder och känna igen skannade PDF-filer med Aspose.OCR.
og_title: Hur du använder OCR i Java – Komplett guide
tags:
- OCR
- Java
- Aspose
title: Så använder du OCR i Java – Extrahera text från PDF med Aspose.OCR
url: /sv/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder OCR i Java – Extrahera text från PDF med Aspose.OCR

Har du någonsin undrat **hur man använder OCR** för att omvandla en skannad PDF till sökbar text? Du är inte ensam. De flesta utvecklare fastnar när en PDF kommer som en massa bilder, och de vanliga text‑extraheringsverktygen bara returnerar ingenting. Den goda nyheten? Med några rader Java‑kod och Aspose.OCR kan du **extrahera text från PDF**, **konvertera PDF till bilder** och **igenkänna skannad PDF** i ett enda, smärtfritt arbetsflöde.

I den här handledningen går vi igenom allt du behöver veta – från licensiering av biblioteket till utskrift av det slutliga resultatet. När du är klar har du ett färdigt program som drar ut ren text från vilken skannad rapport, faktura eller e‑bok som helst. Inga externa tjänster, ingen magi – bara ren Java‑kod som du kontrollerar.

## Vad du behöver

- **Java Development Kit (JDK) 8+** – vilken modern version som helst fungerar.  
- **Aspose.OCR for Java**‑JAR (ladda ner från Aspose‑webbplatsen).  
- En **giltig Aspose.OCR‑licensfil** (`Aspose.OCR.lic`). Gratis provversion fungerar, men en licens låser upp full noggrannhet.  
- En **exempel‑skannad PDF** (t.ex. `scanned-report.pdf`).  
- En IDE eller en enkel textredigerare plus en terminal.

Det är allt. Inga Maven, inga Gradle, inga extra beroenden – bara Aspose.OCR‑JAR‑filen på din classpath.

![exempel på hur man använder OCR](image-placeholder.png "exempel på hur man använder OCR")

## Steg 1 – Ladda din Aspose.OCR‑licens (Varför det är viktigt)

Innan motorn kan köras på full hastighet måste du berätta var licensen finns. Att hoppa över detta steg tvingar biblioteket in i utvärderingsläge, vilket lägger vattenstämplar på resultatet och kan begränsa noggrannheten.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – required for unrestricted OCR
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**Varför detta fungerar:** `License`‑klassen läser `.lic`‑filen och registrerar den globalt. När den är satt kommer varje `OcrEngine` du skapar automatiskt att använda de licensierade funktionerna.

## Steg 2 – Skapa OCR‑motorn (Motorn bakom magin)

En `OcrEngine`‑instans är arbetshästen som skannar bilder och spottar ut text. Tänk på den som hjärnan som tolkar pixelmönster.

```java
        // Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Proffstips:** Du kan justera språk, förtroendegränser eller till och med aktivera GPU‑acceleration via motorns egenskaper. För de flesta engelska PDF‑filer fungerar standardinställningarna bra.

## Steg 3 – Förbered indata: Lägg till din PDF (Konvertera PDF till bilder under huven)

Aspose.OCR behandlar varje sida i en PDF som en bild. När du anropar `addPdf` rasteriserar biblioteket tyst varje sida, vilket är exakt vad du behöver för att **konvertera PDF till bilder** innan igenkänning.

```java
        // Prepare OCR input – each PDF page becomes an image internally
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");
```

**Vad som händer:**  
- PDF‑filen öppnas.  
- Varje sida renderas med 300 dpi (standard) för att bevara teckendetaljer.  
- De renderade bitmap‑objekten lagras i `OcrInput`‑samlingen.

Om du någonsin behöver de råa bilderna (för felsökning eller anpassad förbehandling), anropa `ocrInput.getPages()` efter detta steg.

## Steg 4 – Kör OCR‑processen (Utför OCR på PDF)

Nu börjar det tunga arbetet. Metoden `recognize` loopar över varje bild, kör igenkänningsalgoritmen och samlar resultaten i ett `OcrResult`.

```java
        // Run OCR on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Varför du bör bry dig:** `OcrResult` innehåller inte bara ren text utan också förtroendescore, avgränsningsrutor och referensen till originalbilden. För de flesta användningsfall räcker `getText()`.

## Steg 5 – Hämta och visa den extraherade texten

Till sist drar du ut ren‑text‑strängen från resultatet och skriver ut den. Du kan också skriva den till en fil, skicka den till ett sökindex eller föra in den i en efterföljande NLP‑pipeline.

```java
        // Output the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

### Förväntad utskrift

Om `scanned-report.pdf` innehåller ett enkelt stycke kommer du att se något i stil med:

```
Extracted text:
Quarterly Sales Report
Region: North America
Total Revenue: $4,527,000
...
```

Den exakta formateringen speglar den ursprungliga layouten och bevarar radbrytningar där det är möjligt.

## Hantera vanliga kantfall

### 1. Flerspråkiga PDF‑filer

Om ditt dokument innehåller fransk eller spansk text, sätt språket innan du anropar `recognize`:

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);
```

Du kan ange en array av språk så att motorn kan autodetektera.

### 2. Låga upplösningar

När du arbetar med 150 dpi‑skanningar, öka den interna renderings‑DPI:n:

```java
ocrInput.addPdf("low-res.pdf", 600); // render at 600 dpi for better accuracy
```

Högre DPI förbättrar teckenklarheten men kräver mer minne.

### 3. Stora PDF‑filer (Minneshantering)

För PDF‑filer med dussintals sidor, behandla dem i batcher:

```java
int batchSize = 10;
for (int i = 0; i < ocrInput.getPages().size(); i += batchSize) {
    List<OcrPage> batch = ocrInput.getPages().subList(i, Math.min(i + batchSize, ocrInput.getPages().size()));
    OcrInput batchInput = new OcrInput();
    batchInput.getPages().addAll(batch);
    OcrResult batchResult = ocrEngine.recognize(batchInput);
    // Append batchResult.getText() to your final output
}
```

Detta förhindrar att JVM‑heapen växer okontrollerat.

## Fullt, kör‑klart exempel

Nedan är det kompletta programmet – inklusive imports och licenshantering – så att du kan kopiera och köra direkt.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (required for full functionality)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Step 2: Create an OCR engine instance that will perform the recognition
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Prepare the OCR input by adding the PDF file.
        // Each page of the PDF is internally converted to an image.
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");

        // Step 4: Run the OCR process on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

Kör det med:

```bash
javac -cp "path/to/aspose-ocr.jar" PdfOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" PdfOcrDemo
```

Du bör se den extraherade texten skriven till konsolen.

## Sammanfattning – Vad vi gick igenom

- **Hur man använder OCR** i Java med Aspose.OCR.  
- Arbetsflödet för att **extrahera text från PDF**‑filer.  
- Internt konverterar biblioteket **PDF till bilder** innan teckenigenkänning.  
- Tips för **att utföra OCR på PDF** med flera språk, låga upplösningar och stora dokument.  
- Ett komplett, körbart kodexempel som du kan klistra in i vilket Java‑projekt som helst.

## Nästa steg & relaterade ämnen

Nu när du kan **igenkänna skannad PDF**, fundera på dessa uppföljningsidéer:

- **Skapande av sökbar PDF** – lägg OCR‑texten över den ursprungliga PDF‑filen för att skapa ett sökbart dokument.  
- **Batch‑behandlingstjänst** – paketera koden i en Spring Boot‑mikrotjänst som tar emot PDF‑filer via REST.  
- **Integration med Elasticsearch** – indexera den extraherade texten för snabb fulltextsökning i ditt dokumentarkiv.  
- **Bild‑förbehandling** – använd OpenCV för att räta upp eller avbrusa sidor innan OCR för ännu högre precision.

Varje ämne bygger på de grundläggande koncept vi gått igenom, så experimentera gärna och låt OCR‑motorn göra det tunga arbetet.

---

*Lycka till med kodandet! Om du stöter på problem – som licensfel eller oväntade null‑resultat – lämna en kommentar nedan. Jag hjälper gärna till med felsökning.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}