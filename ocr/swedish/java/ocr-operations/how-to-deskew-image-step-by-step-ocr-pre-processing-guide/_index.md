---
category: general
date: 2026-02-19
description: Lär dig hur du räta upp en bild och tar bort brus för OCR. Denna handledning
  visar hur du känner igen text i en bild, korrigerar bildrotation och förbehandlar
  bild‑OCR med Aspose OCR.
draft: false
keywords:
- how to deskew image
- recognize text image
- how to remove noise
- correct image rotation
- preprocess image ocr
language: sv
og_description: Hur man räta upp en bild och tar bort brus så att du snabbt kan känna
  igen text i bilden. Följ den här guiden för att korrigera bildrotation och förbehandla
  bild‑OCR med Aspose.
og_title: Hur man räta upp en bild – Komplett OCR‑förbehandlingshandledning
tags:
- OCR
- Java
- Image Processing
title: Hur man räta upp bild — Steg‑för‑steg OCR‑förbehandlingsguide
url: /sv/java/ocr-operations/how-to-deskew-image-step-by-step-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man deskew‑ar bild — Fullständig OCR‑förbehandlingshandledning

Har du någonsin undrat **how to deskew image** filer innan du matar dem till en OCR‑motor? Kanske har du skannat en bunt kvitton och sidorna ser lite lutande ut, eller så är skanningen prickig med slumpmässiga punkter. Det är ett vanligt problem – sneda, brusiga bilder får textigenkänning att snubbla.  

Den goda nyheten? Du kan räta upp (correct image rotation) och ta bort brus (how to remove noise) på bara några rader Java med Aspose.OCR. I den här guiden går vi igenom hela flödet: från att ladda en brusig‑roterad PNG, applicera deskew + median denoise, hela vägen till **recognize text image** och skriva ut resultatet. I slutet har du ett återanvändbart kodstycke som du kan slänga in i vilket Java‑projekt som helst.

## Vad du behöver

- **Java 17** eller nyare (koden kompilerar med äldre versioner, men 17 är den optimala).  
- **Aspose.OCR for Java** – du kan hämta den senaste JAR‑filen från Maven Central (`com.aspose:aspose-ocr`).  
- En bildfil som både är roterad och brusig (t.ex. `noisy-rotated.png`).  
- En enkel IDE (IntelliJ, Eclipse eller till och med VS Code).  

Inga avancerade byggverktyg behövs; ett enkelt `javac` + `java`‑körning fungerar bra.

---

## Steg 1 – Skapa OCR‑motorinstans  

Det första du gör är att starta en `OcrEngine`. Tänk på den som hjärnan som senare kommer att läsa tecknen åt dig.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Pro tip:** Behåll motorn som en singleton om du bearbetar många bilder; den återanvänder interna buffertar och snabbar upp processen.

## Steg 2 – Aktivera Deskew och Median‑denoise (Hur man tar bort brus)

Nu instruerar vi motorn att **correct image rotation** och att **how to remove noise**. Båda filtren är valfria, men tillsammans förbättrar de noggrannheten avsevärt.

```java
        // Turn on preprocessing filters
        ocrEngine.getPreprocessing().setDeskew(true);          // fixes rotation
        ocrEngine.getPreprocessing().setMedianDenoise(true);   // smooths out speckles
```

Varför median‑denoise? Det bevarar kanter (linjerna som definierar tecken) samtidigt som det tar bort isolerade pixlar – precis vad du behöver för ren OCR.

## Steg 3 – Ladda bilden du vill bearbeta  

Här pekar vi motorn på filen som behöver rengöras. `ImageStream.fromFile` läser PNG‑filen till minnet.

```java
        // Load the noisy‑rotated image
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/noisy-rotated.png"));
```

Om din bild finns på en fjärrserver, mata bara in ett `InputStream` istället – Aspose hanterar det smidigt.

## Steg 4 – Kör OCR och fånga den igenkända texten  

Med förbehandling aktiverad läser motorn nu den korrigerade bilden. Anropet `recognize()` returnerar ett `RecognitionResult` som innehåller den extraherade strängen.

```java
        // Perform OCR – the engine automatically applies deskew & denoise first
        String recognizedText = ocrEngine.recognize().getText();

        // Show the output
        System.out.println("=== Recognized Text ===");
        System.out.println(recognizedText);
    }
}
```

Du bör se ren, läsbar text i konsolen, även om den ursprungliga bilden var sned och kornig.

## Steg 5 – Verifiera resultatet (Vad du kan förvänta dig)

När allt fungerar skriver konsolen ut något liknande:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑02‑15
Total: $1,234.56
```

Om utskriften fortfarande innehåller förvrängda tecken, dubbelkolla:

- Bildens upplösning (≥ 300 dpi är idealiskt).  
- Att filvägen är korrekt.  
- Om ytterligare filter (t.ex. `setContrastStretch`) kan hjälpa.

---

## Valfritt: Visuell bekräftelse med ett exempel på bild  

Nedan är en liten förhandsgranskning av ett roterat, brusigt kvitto. Lägg märke till lutningen – vår kod kommer att räta upp den åt dig.

![exempel på hur man deskew‑ar bild](deskew-demo.png "exempel på hur man deskew‑ar bild")

*Alt‑text: hur man deskew‑ar bild – före och efter bearbetning.*

---

## Vanliga frågor

### Fungerar detta med PDF‑filer eller bara PNG/JPEG?  
Aspose.OCR kan läsa PDF‑filer direkt; ersätt bara `ImageStream.fromFile` med `ImageStream.fromPdf`. Samma förbehandlingsflaggor gäller, så du får fortfarande **how to deskew image** och **how to remove noise**.

### Vad händer om jag behöver behålla den ursprungliga orienteringen för senare steg?  
Du kan klona bilden innan förbehandling:

```java
Image original = ocrEngine.getImage().clone();
ocrEngine.getPreprocessing().apply(); // modifies the internal copy
// Use original later if needed
```

### Kan jag ändra deskew‑vinkeln manuellt?  
Ja—`setDeskewAngle(double degrees)` låter dig åsidosätta den automatiska detekteringsalgoritmen. Användbart när auto‑detect misslyckas vid extrema rotationer.

### Hur skiljer sig median‑denoise från Gaussian blur?  
Medianfilter ersätter varje pixel med medianen av dess grannar, vilket bevarar kanter. Gaussian blur jämnar ut allt, vilket kan sudda ut teckenstreck – så median är det säkrare valet för OCR.

---

## Avslutning  

I den här handledningen gick vi igenom **how to deskew image** filer, demonstrerade **how to remove noise**, och visade hur du **recognize text image** med Aspose OCR:s inbyggda förbehandling. Genom att aktivera `setDeskew(true)` och `setMedianDenoise(true)` korrigerar du automatiskt **correct image rotation** och rensar bort prickar, vilket förvandlar en rörig skanning till en ren textsträng.  

Känn dig fri att experimentera: prova olika denoise‑strategier, mata in PDF‑filer, eller kedja flera bilder i en loop. Mönstret – motor → förbehandling → igenkänning – gäller för alla scenarier och ger en solid grund för vilken OCR‑pipeline som helst.

**Nästa steg** du kan utforska:

- **Batch‑behandling** – iterera över en mapp med bilder och skriv varje resultat till en `.txt`‑fil.  
- **Språkpaket** – ladda en specifik språkordbok för att öka noggrannheten för icke‑engelsk text.  
- **Avancerade filter** – som `setContrastStretch` eller `setBinarization` för lågkontrastskanningar.  

Har du fler frågor? lämna en kommentar, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}