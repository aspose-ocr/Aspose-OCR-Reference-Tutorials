---
category: general
date: 2026-02-22
description: Hur man använder OCR i Java för att extrahera text från en bild, förbättra
  OCR‑noggrannheten och ladda bild för OCR med praktiska kodexempel.
draft: false
keywords:
- how to use OCR
- extract text from image
- improve OCR accuracy
- load image for OCR
- OCR preprocessing
language: sv
og_description: Hur man använder OCR i Java för att extrahera text från en bild och
  förbättra OCR‑noggrannheten. Följ den här guiden för ett färdigt exempel som går
  att köra.
og_title: Hur man använder OCR i Java – Komplett steg‑för‑steg‑guide
tags:
- OCR
- Java
- Image Processing
title: Hur man använder OCR i Java – Komplett steg‑för‑steg‑guide
url: /sv/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så använder du OCR i Java – Komplett steg‑för‑steg‑guide

Har du någonsin behövt **how to use OCR** på en skev skärmbild och undrat varför resultatet ser ut som nonsens? Du är inte ensam. I många verkliga appar—skanna kvitton, digitalisera formulär eller hämta text från memes—beror pålitliga resultat på några enkla inställningar.

I den här handledningen går vi igenom **how to use OCR** för att *extract text from image* filer, visar dig hur du **improve OCR accuracy**, och demonstrerar det korrekta sättet att **load image for OCR** med ett populärt Java OCR‑bibliotek. I slutet har du ett självständigt program som du kan lägga in i vilket projekt som helst.

## Vad du kommer att lära dig

- Den exakta koden du behöver för att **load image for OCR** (utan dolda beroenden).
- Vilka förbehandlingsflaggor som förbättrar **improve OCR accuracy** och varför de är viktiga.
- Hur du läser OCR‑resultatet och skriver ut det i konsolen.
- Vanliga fallgropar—som att glömma att sätta ett intresseområde eller ignorera brusreducering—och hur du undviker dem.

### Förutsättningar

- Java 17 eller nyare (koden kompileras med vilken recent JDK som helst).
- Ett OCR‑bibliotek som tillhandahåller klasserna `OcrEngine`, `ImagePreprocessingOptions`, `OcrInput` och `OcrResult` (till exempel det fiktiva paketet `com.example.ocr` som används i kodsnutten). Byt ut det mot det riktiga biblioteket du använder.
- En exempelbild (`skewed_noisy.png`) placerad i en mapp du kan referera till.

> **Pro tip:** Om du använder ett kommersiellt SDK, se till att licensfilen finns på din classpath; annars kommer motorn att kasta ett initieringsfel.

---

## Steg 1: Skapa en OCR‑motorinstans – **how to use OCR** effektivt

Det första du behöver är ett `OcrEngine`‑objekt. Tänk på det som hjärnan som tolkar pixlarna.

```java
// Step 1: Initialize the OCR engine
import com.example.ocr.OcrEngine;

OcrEngine ocrEngine = new OcrEngine();
```

*Varför detta är viktigt:* Utan en motor har du ingen kontext för språkmodeller, teckensätt eller bildheuristik. Att instansiera den tidigt låter dig också fästa förbehandlingsalternativ senare.

---

## Steg 2: Konfigurera bildförbehandling – **improve OCR accuracy**

Förbehandling är den hemliga såsen som förvandlar en brusig skanning till ren, maskinläsbar text. Nedan aktiverar vi deskew, hög nivå av brusreducering, auto‑kontrast och ett intresseområde (ROI) för att fokusera på den relevanta delen av bilden.

```java
import com.example.ocr.ImagePreprocessingOptions;
import java.awt.Rectangle;

// Step 2: Set up preprocessing to improve OCR accuracy
ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
preprocessing.setDeskewEnabled(true); // Correct image rotation
preprocessing.setNoiseReductionLevel(
        ImagePreprocessingOptions.NoiseReduction.HIGH); // Reduce speckles
preprocessing.setAutoContrastEnabled(true); // Boost contrast
preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600)); // Process a sub‑region only

ocrEngine.setPreprocessingOptions(preprocessing);
```

*Varför detta är viktigt:*  
- **Deskew** justerar roterad text, vilket är avgörande när du skannar kvitton som inte är helt platta.  
- **Noise reduction** tar bort lösa pixlar som annars skulle tolkas som tecken.  
- **Auto‑contrast** utökar tonomfånget, så att svaga bokstäver framträder.  
- **ROI** får motorn att ignorera irrelevanta kanter, vilket sparar både tid och minne.

Om du hoppar över någon av dessa kommer du sannolikt att se en minskning i **improve OCR accuracy**‑resultat.

---

## Steg 3: Ladda bilden för OCR – **load image for OCR** korrekt

Nu pekar vi faktiskt motorn på filen vi vill läsa. Klassen `OcrInput` kan acceptera flera bilder, men för detta exempel håller vi det enkelt.

```java
import com.example.ocr.OcrInput;

// Step 3: Load the image you want to extract text from
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png"); // replace with your real path
```

*Varför detta är viktigt:* Sökvägen måste vara absolut eller relativ till arbetskatalogen; annars kastar motorn ett `FileNotFoundException`. Observera också att metodnamnet `add` antyder att du kan köa flera bilder—praktiskt för batch‑behandling.

---

## Steg 4: Utför OCR och skriv ut den igenkända texten – **how to use OCR** end‑to‑end

Till sist ber vi motorn att känna igen texten och skriva ut den. Objektet `OcrResult` innehåller den råa strängen, förtroendesiffror och rad‑för‑rad‑metadata (om du behöver det senare).

```java
import com.example.ocr.OcrResult;

// Step 4: Run OCR and print the extracted text
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Förväntad utskrift** (förutsatt att exempelbilden innehåller “Hello, OCR World!”):

```
=== OCR Output ===
Hello, OCR World!
```

Om resultatet ser förvrängt ut, gå tillbaka till Steg 2 och justera förbehandlingsalternativen—kanske sänka brusreduceringsnivån eller justera ROI‑rektangeln.

---

## Fullt, körbart exempel

Nedan är ett komplett Java‑program som du kan kopiera‑och‑klistra in i en fil som heter `OcrDemo.java`. Det binder ihop alla steg vi diskuterade.

```java
// OcrDemo.java – A complete, runnable example showing how to use OCR in Java
import com.example.ocr.OcrEngine;
import com.example.ocr.ImagePreprocessingOptions;
import com.example.ocr.OcrInput;
import com.example.ocr.OcrResult;
import java.awt.Rectangle;

public class OcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing (this is the key to improve OCR accuracy)
        ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
        preprocessing.setDeskewEnabled(true);
        preprocessing.setNoiseReductionLevel(
                ImagePreprocessingOptions.NoiseReduction.HIGH);
        preprocessing.setAutoContrastEnabled(true);
        preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600));
        ocrEngine.setPreprocessingOptions(preprocessing);

        // 3️⃣ Load the image you want to extract text from
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace the path with your own image location
        ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run the OCR engine and print the result
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Spara filen, kompilera med `javac OcrDemo.java` och kör `java OcrDemo`. Om allt är korrekt konfigurerat kommer du att se den extraherade texten skriven i konsolen.

---

## Vanliga frågor & edge‑cases

| Question | Answer |
|----------|--------|
| **Vad händer om min bild är i JPEG‑format?** | `OcrInput.add()`‑metoden accepterar alla stödjade rasterformat—PNG, JPEG, BMP, TIFF. Ändra bara filändelsen i sökvägen. |
| **Kan jag bearbeta flera sidor samtidigt?** | Absolut. Anropa `ocrInput.add()` för varje fil, och skicka sedan samma `ocrInput` till `recognize()`. Motorn returnerar ett sammanslaget `OcrResult`. |
| **Vad händer om OCR‑resultatet är tomt?** | Dubbelkolla att ROI faktiskt innehåller text. Se också till att `setDeskewEnabled(true)` är på; en 90° rotation får motorn att tro att bilden är tom. |
| **Hur ändrar jag språkmodellen?** | De flesta bibliotek exponerar en `setLanguage(String)`‑metod på `OcrEngine`. Anropa den före `recognize()`, t.ex. `ocrEngine.setLanguage("eng")`. |
| **Finns det ett sätt att få förtroendesiffror?** | Ja, `OcrResult` ger ofta `getConfidence()` per rad eller per tecken. Använd den för att filtrera resultat med låg förtroendegrad. |

---

## Slutsats

Vi har gått igenom **how to use OCR** i Java från början till slut: skapa motorn, konfigurera förbehandling för att **improve OCR accuracy**, korrekt **load image for OCR**, och slutligen skriva ut den extraherade texten. Den kompletta kodsnutten är klar att köra, och förklaringarna svarar på “varför” bakom varje rad.

Redo för nästa steg? Prova att byta ut ROI‑rektangeln för att fokusera på olika delar av bilden, experimentera med `NoiseReduction.MEDIUM`, eller integrera resultatet i en sökbar PDF. Du kan också utforska relaterade ämnen som **extract text from image** med molntjänster, eller batch‑processa tusentals filer med en flertrådad kö.

Har du fler frågor om OCR, bildförbehandling eller Java‑integration? Lämna en kommentar, och lycka till med kodandet! 

![How to use OCR example](/images/ocr-demo.png "how to use OCR – Java example showing preprocessing and result")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}