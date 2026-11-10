---
category: general
date: 2026-09-23
description: Lär dig hur du utför OCR på bilder i Java med Aspose OCR, extraherar
  text från bild och aktiverar stavningskorrigering med en anpassad ordlista.
draft: false
keywords:
- how to perform ocr
- how to extract text from image
- java ocr maven dependency
- java image to text conversion
- aspose ocr java
lastmod: 2026-09-23
og_description: Hur man utför OCR på bilder i Java med Aspose OCR. Denna guide visar
  hur du laddar en bild, extraherar text från bilden och lägger till stavningskorrigering
  för korrekta resultat.
og_image_alt: 'Aspose OCR Java tutorial: extracting text from images with spell correction'
og_title: Hur man utför OCR på bilder med Aspose OCR i Java
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  headline: How to perform OCR on images with Aspose OCR in Java
  type: TechArticle
- description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  name: How to perform OCR on images with Aspose OCR in Java
  steps:
  - name: set up the project and import dependencies
    text: Add the Aspose OCR Maven dependency to your `pom.xml`. This single line
      pulls in the core OCR engine and all required transitive libraries. > **Pro
      tip:** Verify the version number on Maven Central; newer releases add language
      packs and performance improvements.
  - name: load the image for OCR
    text: '`OcrEngine` works with any `InputStream`. Use `ImageStream` to wrap a file
      path, byte array, or URL. **Definition anchor:** `ImageStream` is Aspose OCR’s
      lightweight wrapper that reads image data from various sources without converting
      it to a `BufferedImage` first.'
  - name: enable spell‑correction (optional but powerful)
    text: Turn on the built‑in spell‑correction flag to automatically fix common OCR
      mis‑recognitions such as “l” vs “1”. Spell‑correction can improve accuracy by
      up to **80 %** on low‑contrast scans, turning “Inv0ice” into “Invoice” without
      extra code.
  - name: provide a custom dictionary (tailor the engine)
    text: Supply a plain‑text dictionary for industry‑specific terminology—medical
      codes, legal terms, product SKUs, etc. **Definition anchor:** `CustomDictionary`
      loads a UTF‑8 word list that the OCR engine consults during post‑processing
      to prefer your domain vocabulary.
  - name: run the OCR process
    text: Invoke `process()` to get an `OcrResult` containing the recognized text,
      confidence scores, and optional layout data. If an error occurs, `ocrResult.getErrorMessage()`
      returns a detailed description you can log or display.
  - name: output the recognized (and corrected) text
    text: 'Print the extracted string to the console or write it to a file. For quick
      testing, a simple `System.out.println` is sufficient. Running the program should
      produce clean, searchable text similar to: If you notice stray characters, revisit
      your custom dictionary and consider pre‑processing the image '
  type: HowTo
- questions:
  - answer: No. The library runs entirely offline; all recognition happens locally
      on your JVM.
    question: Does Aspose OCR require an internet connection?
  - answer: Aspose OCR supports Java 8 through Java 21, including both standard and
      OpenJDK distributions.
    question: Which Java versions are supported?
  - answer: Yes. The engine streams data and can handle images up to 500 MB, limited
      only by available heap memory.
    question: Can I process images larger than 10 MB?
  - answer: Purchase a commercial license from the Aspose store and set the license
      file with `License license = new License(); license.setLicense("Aspose.OCR.lic");`.
    question: How do I license Aspose OCR for production?
  - answer: Aspose OCR includes a handwriting mode that can be enabled via `ocrEngine.getEngineOptions().setHandwriting(true);`,
      improving accuracy on cursive scripts.
    question: Is there built‑in support for handwritten text?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
- image to text
- OCR Maven dependency
title: Hur man utför OCR på bilder med Aspose OCR i Java
url: /sv/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utför OCR på bild – komplett Java‑handledning

Om du letar efter ett pålitligt sätt att **how to perform OCR** på bildfiler med Java, har du hamnat på rätt plats. Med Aspose OCR för Java kan du extrahera text från bildresurser på bara några rader kod, öka noggrannheten med en anpassad ordlista och aktivera stavningskorrigering för att rensa upp brusiga skanningar. Denna handledning guidar dig genom varje steg—från att ladda bilden för OCR till att skriva ut den korrigerade texten—så att du kan integrera bild‑till‑text‑konvertering i dina applikationer idag.

## Snabba svar
- **What is the main class to start OCR?** `OcrEngine` är Aspose OCR:s kärnklass som utför optisk teckenigenkänning.
- **Which Maven artifact adds OCR support?** Lägg till `com.aspose:aspose-ocr` i din `pom.xml`.
- **Do I need a license for development?** En gratis tillfällig licens fungerar för testning; en kommersiell licens krävs för produktion.
- **Can I improve accuracy on low‑quality scans?** Ja—aktivera stavningskorrigering och ange en anpassad ordlista.
- **Is multi‑page support built‑in?** Bearbeta varje sidobild i en loop; motorn är trådsäker för samtidig körning.

## Vad är how to perform OCR?
Frasen **how to perform OCR** avser processen att konvertera tryckt eller handskriven text i en bild till redigerbara, sökbara digitala tecken med hjälp av optisk teckenigenkänningsteknologi. Aspose OCR implementerar denna process med en engångsmotor som stödjer över 20 rasterformat och mer än 50 språk.

## Varför använda Aspose OCR för Java?
Aspose OCR stödjer **20+ bildformat** (inklusive PNG, JPEG, TIFF, BMP och GIF) och kan bearbeta **batcher med hundratals sidor** utan att ladda hela dokumentet i minnet, vilket levererar upp till **300 sidor per minut** på en vanlig 4‑kärnig server. Dess inbyggda stavningskorrigering och anpassade ordlista‑funktioner minskar vanliga OCR‑felfrekvenser från 12 % till under 2 % på brusiga fakturor.

## Förutsättningar
- **Java Development Kit (JDK) 8+** – standard Java‑runtime.
- **Aspose OCR for Java**‑biblioteket – hämta den senaste JAR‑filen från Maven Central eller Aspose nedladdningsportal.
- En bildfil (t.ex. `invoice.png`) som du vill bearbeta.
- (Optional) `custom_dict.txt` – en UTF‑8‑textfil som innehåller domänspecifika ord, ett per rad.

Det är allt du behöver—inga externa tjänster eller tunga ramverk.

## Så utför du OCR på bild i Java?
Läs in din bild, aktivera stavningskorrigering, ange eventuellt en anpassad ordlista, kör motorn och läs resultatet. Detta tillvägagångssätt fungerar för enkelsidiga filer såväl som batch‑bearbetning, och motorn hanterar automatiskt bildavkodning, språkdetection och förtroendescore, vilket ger dig en pålitlig textutdata redo för vidare bearbetning. Följande avsnitt bryter ner varje steg med tydliga förklaringar och exakt kod som du kan kopiera.

### Steg 1: konfigurera projektet och importera beroenden

Lägg till Aspose OCR Maven‑beroendet i din `pom.xml`. Denna enda rad hämtar kärn‑OCR‑motorn och alla nödvändiga transitiva bibliotek.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

> **Pro tip:** Verifiera versionsnumret på Maven Central; nyare releaser lägger till språkpaket och prestandaförbättringar.

### Steg 2: läs in bilden för OCR

`OcrEngine` fungerar med vilken `InputStream` som helst. Använd `ImageStream` för att omsluta en filsökväg, byte‑array eller URL.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you wish to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Definition anchor:** `ImageStream` är Aspose OCR:s lätta omslag som läser bilddata från olika källor utan att först konvertera den till en `BufferedImage`.

### Steg 3: aktivera stavningskorrigering (valfritt men kraftfullt)

Aktivera den inbyggda stavningskorrigeringsflaggan för att automatiskt rätta vanliga OCR‑feligenkänningar såsom “l” vs “1”.

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

Stavningskorrigering kan förbättra noggrannheten med upp till **80 %** på lågkontrastskanningar, och omvandla “Inv0ice” till “Invoice” utan extra kod.

### Steg 4: tillhandahåll en anpassad ordlista (anpassa motorn)

Tillhandahåll en vanlig text‑ordlista för branschspecifik terminologi—medicinska koder, juridiska termer, produkt‑SKU‑er osv.

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

**Definition anchor:** `CustomDictionary` laddar en UTF‑8‑ordlista som OCR‑motorn konsulterar under efterbearbetning för att föredra ditt domänvokabular.

### Steg 5: kör OCR‑processen

Anropa `process()` för att få ett `OcrResult` som innehåller den igenkända texten, förtroendescore och valfri layoutdata.

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

Om ett fel uppstår returnerar `ocrResult.getErrorMessage()` en detaljerad beskrivning som du kan logga eller visa.

### Steg 6: skriv ut den igenkända (och korrigerade) texten

Skriv ut den extraherade strängen till konsolen eller skriv den till en fil. För snabb testning räcker en enkel `System.out.println`.

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

Att köra programmet bör producera ren, sökbar text liknande:

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

Om du märker stray‑tecken, gå tillbaka till din anpassade ordlista och överväg förbehandling av bilden (öka kontrast, brusreducering eller konvertera till gråskala).

## Hur extraherar du text från bild med en anpassad ordlista?
Läs in ordlistan innan bearbetning, och anropa sedan `ocrEngine.setCustomDictionary(customDict)`. Motorn kommer att prioritera ord från listan, vilket dramatiskt minskar falska positiva för specialiserade vokabulärer. Genom att tillhandahålla domänspecifika termer hjälper du OCR‑efterprocessorn att lösa tvetydiga tecken, såsom att skilja på bokstaven “O” och siffran “0”, vilket förbättrar den totala noggrannheten i tekniska dokument.

## Hur lägger du till java ocr maven‑beroendet korrekt?
Lägg till följande kodsnutt i din `pom.xml` inom `<dependencies>`‑sektionen. Detta beroende hämtar det centrala Aspose OCR‑biblioteket samt alla nödvändiga transitiva komponenter, vilket säkerställer att OCR‑motorn kan instansieras utan ytterligare konfiguration. Se till att köra `mvn clean install` efter att du uppdaterat filen så att Maven löser den senaste versionen från det centrala lagret.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

## Vanliga frågor & edge cases

### Vad händer om bilden är i ett annat format (PDF, TIFF, etc.)?
Aspose OCR hanterar rasterformat direkt. För PDF‑filer, extrahera varje sida som en bild först—Aspose PDF för Java tillhandahåller `PdfExtractor` för att göra detta effektivt. När du har en `BufferedImage` eller byte‑ström fungerar samma `setImage`‑anrop. Detta tillvägagångssätt låter dig bearbeta flersidiga dokument utan att konvertera hela PDF‑filen till minnet, vilket håller arbetsflödet snabbt och skalbart.

### Hur hanterar jag flersidiga dokument?
Iterera över varje sidobild, skapa en ny `OcrEngine` (eller återställ den befintliga), och sammanfoga `OcrResult.getText()`‑värdena. Detta tillvägagångssätt håller stavningskontrollens kontexter oberoende per sida. Genom att bearbeta sidor sekventiellt eller i parallella trådar kan du upprätthålla hög genomströmning samtidigt som varje sida drar nytta av samma ordlista och stavningskorrigeringsinställningar.

### Kan jag begränsa språk eller teckenuppsättning?
Ja. Anropa `ocrEngine.getEngineOptions().setLanguage(Language.English)` (eller något annat stödjat språk) för att begränsa igenkänningsomfånget, vilket snabbar upp bearbetningen med upp till **30 %**. Att begränsa språket minskar teckenuppsättningen som motorn måste beakta, vilket minskar tvetydighet och förbättrar både hastighet och noggrannhet, särskilt för dokument som endast innehåller latinska tecken.

### Vad gäller prestanda för stora batcher?
Motorn är trådsäker för skriv‑skyddade operationer. Skapa en trådpool och tilldela varje bild till sin egen `OcrEngine`‑instans. På en 4‑kärnig maskin kan du uppnå **≈250 sidor/minut** med parallell körning. Säkerställ att tillräckligt heap‑minne är allokerat och övervaka CPU‑användning för att undvika flaskhalsar när du bearbetar tusentals högupplösta bilder.

## Tips för bättre noggrannhet

- **Pre‑process the image**: öka kontrast, applicera ett medianfilter eller konvertera till gråskala före OCR.
- **Use 300 dpi or higher** scans; lägre upplösningar ökar felfrekvensen dramatiskt.
- **Keep the custom dictionary focused**: för många irrelevanta ord kan förvirra stavningskontrollen.
- **Post‑process with regex**: validera datum, siffror eller ID:n efter extraktion för att fånga återstående avvikelser.

## Nästa steg

Nu när du vet **how to perform OCR** på bilder och **how to extract text from image**‑filer, kan du utforska:

- Spara OCR‑utdata som en sökbar PDF med ett dolt textlager.
- Lagra extraherad fakturadata direkt i en relationsdatabas.
- Använda maskininlärningsmodeller för att ytterligare rensa handskrivna anteckningar.
- Exponera OCR‑arbetsflödet som en REST‑ful webbtjänst för användaruppladdade bilder.

Var och en av dessa tillägg bygger på de grundläggande stegen som täckts ovan, så du kommer att finna övergången smidig.

---

**Last Updated:** 2026-09-23  
**Tested With:** Aspose OCR 24.12 for Java  
**Author:** Aspose  

## Vanliga frågor

**Q: Behöver Aspose OCR en internetanslutning?**  
A: No. The library runs entirely offline; all recognition happens locally on your JVM.

**Q: Vilka Java‑versioner stöds?**  
A: Aspose OCR stödjer Java 8 till Java 21, inklusive både standard‑ och OpenJDK‑distributioner.

**Q: Kan jag bearbeta bilder större än 10 MB?**  
A: Ja. Motorn strömmar data och kan hantera bilder upp till 500 MB, begränsat endast av tillgängligt heap‑minne.

**Q: Hur licensierar jag Aspose OCR för produktion?**  
A: Köp en kommersiell licens från Aspose‑butiken och ange licensfilen med `License license = new License(); license.setLicense("Aspose.OCR.lic");`.

**Q: Finns det inbyggt stöd för handskriven text?**  
A: Aspose OCR inkluderar ett handskriftsläge som kan aktiveras via `ocrEngine.getEngineOptions().setHandwriting(true);`, vilket förbättrar noggrannheten på kursiva skript.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you wish to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));

        // Step 3: Enable spell‑checking for the OCR result
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);

        // Step 4: Provide a custom dictionary (one word per line)
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));

        // Step 5: Run the OCR process
        OcrResult ocrResult = ocrEngine.process();

        // Step 6: Output the recognized (and corrected) text
        System.out.println(ocrResult.getText());
    }
}
```

## Relaterade handledningar

- [Utför OCR på bild med Aspose OCR Java steg‑för‑steg‑guide](/ocr/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/)
- [Förbehandla bild‑OCR i Java för att öka noggrannhet och extrahera text](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)
- [Hur du aktiverar GPU för OCR i Java för att känna igen text från bild](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}