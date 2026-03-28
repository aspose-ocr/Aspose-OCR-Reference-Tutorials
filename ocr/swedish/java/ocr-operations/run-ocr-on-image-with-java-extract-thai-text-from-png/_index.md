---
category: general
date: 2026-03-28
description: Kör OCR på en bild i Java med Aspose OCR för att konvertera bilden till
  text, extrahera thailändsk text från PNG snabbt och pålitligt.
draft: false
keywords:
- run OCR on image
- convert image to text
- extract text from PNG
- extract Thai text
- recognize Thai text
language: sv
og_description: Kör OCR på bild med Java och Aspose OCR. Lär dig hur du konverterar
  bild till text, extraherar thailändsk text från PNG och hanterar vanliga fallgropar.
og_title: Kör OCR på bild med Java – Extrahera thaitext snabbt
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Kör OCR på bild med Java – Extrahera thailändsk text från PNG
url: /sv/java/ocr-operations/run-ocr-on-image-with-java-extract-thai-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kör OCR på bild med Java – Fullständig handledning

Har du någonsin undrat hur man **run OCR on image** filer direkt från Java‑kod? Kanske har du en samling thailändska kvitton, skannade dokument eller skärmdumpar och du behöver texten utan att skriva in den manuellt. Det är ett vanligt problem, särskilt när källan är en PNG och språket är icke‑latinskt.  

I den här guiden visar vi exakt hur du **run OCR on image** med Aspose OCR‑biblioteket, konverterar bilden till vanlig text och på ett pålitligt sätt extraherar thailändska tecken. I slutet kommer du att kunna **convert image to text**, **extract text from PNG**, och till och med **recognize Thai text** med bara några rader kod.

## Vad den här handledningen täcker

* Ställa in Aspose OCR‑beroendet i ett Maven/Gradle‑projekt.  
* Initiera `OcrEngine` och konfigurera den för thailändska.  
* Köra OCR på en PNG‑fil och hantera möjliga fel.  
* Skriva ut resultatet till konsolen och verifiera utskriften.  

Ingen tidigare erfarenhet av Aspose krävs—bara en grundläggande Java‑IDE och en bildfil du vill bearbeta.

## Förutsättningar

* Java 8 eller nyare installerat (biblioteket fungerar även med Java 11+).  
* Ett byggverktyg – Maven eller Gradle (vi visar Maven‑exemplet).  
* En Aspose OCR‑licens (gratis provversion fungerar för testning, men en licens tar bort utvärderingsgränserna).  
* En PNG som innehåller thailändsk text, t.ex. `input.png` placerad i ditt projekts resurser‑mapp.

---

## Steg 1: Lägg till Aspose OCR i ditt projekt

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version -->
</dependency>
```

### Gradle (Kotlin DSL)

```kotlin
implementation("com.aspose:aspose-ocr:23.9")
```

> **Pro tip:** Håll biblioteksversionen i synk med de officiella Aspose‑versionsnotiserna; nyare versioner lägger till språkpaket och prestandaförbättringar.

När beroendet är löst bör din IDE automatiskt importera de nödvändiga klasserna.

## Steg 2: Initiera OCR‑motorn

Motorn är hjärtat i processen – tänk på den som “hjärnan” som analyserar pixelmönster. Vi kommer också att tala om för den att vi bara bryr oss om thailändska tecken.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Tell the engine to look for Thai language patterns
        ocrEngine.getRecognitionSettings().setLanguage("th");
```

Varför ange språket explicit? Eftersom att specificera `"th"` begränsar teckenuppsättningen, vilket snabbar upp igenkänning och minskar felaktiga läsningar av liknande tecken.

## Steg 3: Kör OCR på PNG‑filen

Nu matar vi motorn med bilden vi vill avkoda. Metoden `recognizeImage` returnerar ett `OcrResult`‑objekt som innehåller den extraherade strängen och förtroendesiffror.

```java
        // Step 3: Perform OCR on the target image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

Om filen inte kan hittas kastar Aspose ett `FileNotFoundException`. Det är en bra idé att omsluta anropet i ett `try‑catch`‑block för produktionskod, men för den här handledningen håller vi det enkelt.

## Steg 4: Skriv ut den igenkända texten

Till sist skriver vi ut resultatet. Metoden `getText()` returnerar en vanlig Java `String` som du kan lagra, skicka över ett nätverk eller skriva till en fil.

```java
        // Step 4: Display the extracted Thai text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

När du kör programmet bör du se något liknande:

```
=== Recognized Thai Text ===
สวัสดีครับ นี่คือข้อความจากรูปภาพ
```

Om utskriften ser förvrängd ut, dubbelkolla att käll‑PNG‑filen har hög upplösning (minst 300 dpi) och att språkkoden `"th"` matchar ditt mål‑språk.

### Fullständig kodlista

Nedan är den kompletta, färdiga Java‑filen. Kopiera och klistra in den i din IDE, ersätt bildsökvägen om behövs, och tryck på **Run**.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Select Thai language for recognition
        ocrEngine.getRecognitionSettings().setLanguage("th");

        // Run OCR on the PNG image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // Output the recognized text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

![run OCR on image example](image.png "run OCR on image example – Java code extracting Thai text from PNG")

## Steg 5: Vanliga variationer & kantfall

### Konvertera bild till text i andra format

Om du behöver **convert image to text** för en JPEG eller BMP, ändra helt enkelt filändelsen i `imagePath`. Aspose OCR stödjer PNG, JPEG, BMP, TIFF och även PDF‑sidor.

### Extrahera text från PNG med flera språk

Du kan be motorn att upptäcka flera språk samtidigt:

```java
ocrEngine.getRecognitionSettings().setLanguage("th,en");
```

Resultatet kommer att innehålla en blandning av thailändska och engelska tecken, vilket är praktiskt för tvåspråkiga kvitton.

### Hantera lågkvalitativa bilder

För suddiga skanningar, överväg att aktivera förbehandling:

```java
ocrEngine.getRecognitionSettings().setPreprocessMode(PreprocessMode.Auto);
```

Detta aktiverar inbyggda brusreducerings‑ och kontrastförbättringsalgoritmer, vilket förbättrar steget **extract text from PNG**.

### Licensaktivering

Utan licens lägger Aspose in en vattenstämpelrad i utskriften efter 100 sidor. Aktivera din licens tidigt:

```java
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

Placera `.lic`‑filen bredvid din JAR eller referera till den via en absolut sökväg.

## Vanliga frågor

**Q: Fungerar detta på Linux?**  
**A: Absolut. Aspose OCR är ren Java, så alla JVM‑kompatibla OS fungerar.**

**Q: Vad händer om PNG‑filen innehåller handskriven thailändska?**  
**A: Handstiftsigenkänning är begränsad; du kan behöva en dedikerad neuronnätsmodell. Aspose OCR utmärker sig med tryckt text.**

**Q: Kan jag batch‑processa en mapp med bilder?**  
**A: Omslut anropet `recognizeImage` i en loop över `Files.list(Paths.get("folder"))`. Kom ihåg att återanvända samma `OcrEngine`‑instans för prestanda.**

## Slutsats

Vi har gått igenom ett komplett, end‑to‑end‑exempel på hur man **run OCR on image** filer i Java, specifikt för att **extract Thai text** från en PNG. Genom att initiera `OcrEngine`, ange språket, anropa `recognizeImage` och skriva ut resultatet har du nu ett pålitligt sätt att **convert image to text** utan tredjepartstjänster.

Från här kan du:

* **extract text from PNG**‑filer i bulk för data‑mining‑projekt.  
* Kombinera OCR‑utdata med ett översättnings‑API för att få engelska motsvarigheter.  
* Utforska andra språk som stöds av Aspose, såsom kinesiska eller arabiska, genom att byta språkkod.

Prova det med dina egna bilder—justera förbehandlingsinställningarna, experimentera med olika filformat och se hur robust lösningen känns i ditt verkliga arbetsflöde.

Lycka till med kodandet, och må dina OCR‑pipelines alltid vara korrekta!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}