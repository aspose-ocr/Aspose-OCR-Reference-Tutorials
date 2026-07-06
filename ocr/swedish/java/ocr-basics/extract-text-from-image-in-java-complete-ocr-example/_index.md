---
category: general
date: 2026-02-19
description: Extrahera text från bild med Java OCR. Lär dig ett Java OCR‑exempel som
  laddar en bild för OCR och extraherar text från fakturafiler på bara några steg.
draft: false
keywords:
- extract text from image
- java ocr example
- load image for ocr
- extract text from invoice
language: sv
og_description: Extrahera text från bild med Java OCR. Denna guide visar hur du laddar
  en bild för OCR och hämtar text från fakturor med ett enkelt Java OCR‑exempel.
og_title: Extrahera text från bild i Java – Komplett OCR‑exempel
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Extrahera text från bild i Java – Komplett OCR‑exempel
url: /sv/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bild i Java – Komplett OCR-exempel

Har du någonsin behövt **extrahera text från bild** men varit osäker på vilket bibliotek du ska välja? Du är inte ensam—många utvecklare stöter på detta när de automatiserar fakturabehandling eller bygger sökbara arkiv. Den goda nyheten? Med några rader Java kan du ladda en bild för OCR, definiera ett intresseområde och hämta exakt den text du behöver.  

I den här handledningen går vi igenom ett **java ocr example** som visar exakt hur du **laddar bild för OCR**, sätter ett ROI och **extraherar text från faktura**‑filer med Aspose.OCR. I slutet har du ett körbart program som du kan lägga in i vilket Java‑projekt som helst.

## Vad du kommer att lära dig

- Hur du skapar en `OcrEngine`‑instans och varför det är viktigt.
- Det korrekta sättet att **ladda bild för OCR** med Asposes `ImageStream`.
- Att sätta ett **region of interest (ROI)** så att du bara bearbetar den del av bilden som innehåller fakturabeloppet.
- Att extrahera den igenkända texten och skriva ut den i konsolen.
- Vanliga fallgropar (t.ex. fel rektangelkoordinater) och snabba lösningar.

**Förutsättningar**

- Java 8 eller nyare installerat.
- Maven eller Gradle för att hämta Aspose.OCR‑biblioteket (`com.aspose:aspose-ocr`).
- En exempel‑fakturabild (`invoice.png`) placerad i en känd katalog.

Har du allt detta? Bra—låt oss dyka ner.

![Extrahera text från bild med Java OCR](/images/extract-text-from-image-java.png "exempel på extrahering av text från bild")

## Extrahera text från bild – Steg‑för‑steg Java OCR‑exempel

Nedan är hela källkoden. Kopiera‑klistra gärna den i `RoiOcrExample.java` och kör den direkt.

```java
import com.aspose.ocr.*;

public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance.
        // The engine holds all configuration and performs the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image.
        // You can point to any PNG, JPG, or TIFF file. Here we use a sample invoice.
        String imagePath = "YOUR_DIRECTORY/invoice.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Define the region of interest (ROI) you want to recognize.
        // x = 120, y = 340, width = 500, height = 120 – tweak these values for your own layout.
        Rectangle regionOfInterest = new Rectangle(120, 340, 500, 120);
        ocrEngine.setRegionOfInterest(regionOfInterest);

        // Step 4: Perform OCR on the specified ROI and retrieve the text.
        // recognize() returns an OcrResult object; getText() extracts the plain string.
        String extractedText = ocrEngine.recognize().getText();

        // Step 5: Output the recognized text.
        System.out.println("ROI text: " + extractedText);
    }
}
```

### Varför varje steg är viktigt

1. **Skapa OCR‑motorn** – utan en motor finns ingen kontext för bildbehandling. Objektet låter dig också justera språkpaket senare om du behöver flerspråkigt stöd.  
2. **Ladda bilden** – `ImageStream.fromFile` abstraherar filformatet och säkerställer att motorn läser bytes korrekt. Om du hoppar över detta får du ett `NullPointerException`.  
3. **Sätta ROI** – att bearbeta hela sidan kan vara slöseri. Genom att begränsa rektangeln till fakturans totalsumma‑område snabbar du upp igenkänningen och minskar brus.  
4. **Anropa `recognize()`** – här händer magin. Metoden kör OCR‑algoritmen över ROI och producerar ett resultatobjekt.  
5. **Skriva ut resultatet** – i riktiga projekt skulle du troligen lagra texten i en databas, men `System.out.println` är perfekt för en snabb demo.

## Ladda bild för OCR

Om du undrar om sökvägen måste vara absolut eller relativ, så fungerar båda—se bara till att Java‑processen kan läsa filen. På Windows måste bakåtsnedstreck escapetas (`C:\\images\\invoice.png`) eller så kan du använda snedstreck (`C:/images/invoice.png`).  

**Proffstips:** Om du bearbetar många fakturor i en loop, återanvänd samma `OcrEngine`‑instans; den cachar interna resurser och förbättrar genomströmning.

## Definiera Region of Interest (ROI)

Att välja rätt rektangel kan vara lite trial‑and‑error. Ett praktiskt sätt att hitta koordinater är att öppna bilden i någon grafikredigerare (som GIMP eller Paint.NET) och hålla musen över området—du ser X/Y‑värdena i statusfältet.  

Edge case: vissa fakturor har variabla layouter. I så fall kan du köra en snabb för‑scan av hela bilden, lokalisera nyckelord som “Total:” med ett regex, och sedan justera ROI dynamiskt.

## Utför OCR och hämta text

`recognize()`‑anropet är synkront—din tråd blockeras tills motorn är klar. För stora batcher kan du vilja starta en trådpool och bearbeta bilder parallellt. Kom bara ihåg att varje tråd behöver sin egen `OcrEngine`‑instans; de är inte trådsäkra.

## Kör och verifiera output

Compile and run:

```bash
javac -cp "path/to/aspose-ocr.jar" RoiOcrExample.java
java -cp ".:path/to/aspose-ocr.jar" RoiOcrExample
```

You should see something like:

```
ROI text: $1,254.00
```

Om output ser förvrängd ut, dubbelkolla ROI‑koordinaterna och säkerställ att bildkvaliteten är hög (300 dpi eller mer fungerar bäst).  

### Vanliga fallgropar & hur du åtgärdar dem

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Tom sträng | ROI utanför bildens gränser | Verifiera rektangelvärden mot bildens dimensioner |
| Felstavade ord | Låg upplösning | Använd en högupplöst källa eller applicera bildförbehandling (t.ex. binarisering) |
| `java.lang.NoClassDefFoundError` | Saknad Aspose‑JAR på classpath | Lägg till `aspose-ocr.jar` till `-cp` eller använd Maven/Gradle‑beroendehantering |

## Slutsats

Du vet nu hur du **extraherar text från bild** i Java med ett koncist **java ocr example**. Genom att ladda bilden korrekt, definiera ett fokuserat ROI och anropa `recognize()` kan du pålitligt **extrahera text från faktura**‑filer och föra den datan in i efterföljande system.

Vad blir nästa? Prova att byta ROI till olika fält (datum, leverantörsnamn), experimentera med språkpaket för flerspråkiga fakturor, eller integrera OCR‑steget i en Spring Boot‑mikrotjänst. Samma mönster fungerar för kvitton, pass eller vilket dokument som helst där du behöver exakt textutvinning.

Om du har frågor om att skala denna lösning eller hantera brusiga skanningar, lämna en kommentar nedan—lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}