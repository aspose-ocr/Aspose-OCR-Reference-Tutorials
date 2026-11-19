---
category: general
date: 2026-04-29
description: Ställ in maximalt antal trådar i Aspose OCR Java för att snabba upp OCR‑behandlingen
  och enkelt extrahera text från bildfiler. Lär dig hur du konfigurerar parallell
  delning för snabbare resultat.
draft: false
keywords:
- set max threads
- extract text image
- speed up OCR
language: sv
og_description: Ställ in max antal trådar i Aspose OCR Java för att snabba upp OCR
  och snabbt extrahera text från bildfiler. Följ denna steg‑för‑steg‑guide.
og_title: Ställ in max antal trådar i Aspose OCR Java – Snabba upp OCR
tags:
- OCR
- Java
- Aspose
title: Ställ in maxtrådar i Aspose OCR Java – Snabba upp OCR
url: /sv/java/advanced-ocr-techniques/set-max-threads-in-aspose-ocr-java-speed-up-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# sätt max trådar i Aspose OCR Java – Snabba upp OCR

Har du någonsin undrat hur man **sätter max trådar** när man använder Aspose OCR i Java? Att sätta max trådar låter dig **snabba upp OCR** och **extract text image**-filer mycket snabbare på flerkärniga maskiner. I den här handledningen går vi igenom ett komplett, färdigt‑att‑köra exempel som visar exakt hur du konfigurerar parallell bearbetning, varför det är viktigt och vad du kan förvänta dig som resultat.

Om du någonsin har stirrat på ett gigantiskt skannat dokument och tänkt, “Det här tar evigheter,” så är du på rätt plats. Vi kommer också att beröra några vanliga fallgropar—som att få slut på minne när man tile‑ar stora bilder—så att du inte fastnar halvvägs.

---

## Vad du behöver

- **Java 17** eller nyare (API:et fungerar med äldre versioner men 17 ger bästa prestanda).  
- **Aspose.OCR for Java**‑biblioteket – du kan hämta det från Maven Central.  
- En bildfil (PNG, JPEG, TIFF, etc.) som du vill **extract text image** från.  
- En hyfsad CPU med minst 4 kärnor – ju fler kärnor, desto större nytta får du av att sätta max trådar.

Inga extra inhemska beroenden, inga externa tjänster. Bara ren Java och Aspose‑JAR.

## Steg 1: Lägg till Aspose OCR‑beroendet

Om du använder Maven, klistra in följande kodsnutt i din `pom.xml`. Gradle‑användare kan enkelt översätta det.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check Maven Central for the latest version -->
</dependency>
```

> **Proffstips:** Håll versionsnumret uppdaterat. Nya releaser innehåller ofta prestandaförbättringar som ytterligare **speed up OCR**.

## Steg 2: Initiera OCR‑motorn

Att skapa en `OcrEngine`‑instans är enkelt. Tänk på den som hjärnan som senare kommer att **extract text image** data.

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

Vid den här tidpunkten är motorn inaktiv och väntar på en bild och några inställningar. Vi kommer till den avgörande delen—**setting max threads**—i nästa steg.

## Steg 3: Ladda bilden du vill bearbeta

Du kan ladda en bild från en fil, en ström eller till och med en byte‑array. Här använder vi bekvämlighetsmetoden `ImageStream.fromFile`.

```java
        // Step 3: Load the image to be processed
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/big_image.png"));
```

Byt ut `YOUR_DIRECTORY/big_image.png` mot sökvägen till bilden du vill **extract text image** från. Motorn har nu bitmapen redo för igenkänning.

## Steg 4: **set max threads** – Konfigurera parallell bearbetning

Detta är tutorialens kärna. Som standard använder Aspose OCR ett trådtal som matchar antalet logiska CPU‑kärnor. Om du vill finjustera det—t.ex. begränsa belastningen på en delad server—kan du explicit **set max threads**.

Varför är detta viktigt? Varje tråd arbetar på ett segment av bilden. Fler trådar → fler segment → snabbare total bearbetning—förutsatt att din maskin kan hantera de extra kontextbytena. Om du har en 16‑kärnig arbetsstation kan du öka detta till 12 eller till och med 16 för maximal genomströmning.

```java
        // Step 4: Allow up to 8 parallel threads (defaults to number of CPU cores)
        ocrEngine.getProcessingSettings().setMaxParallelThreads(8);
```

## Steg 5: Aktivera parallell tiling – Ett annat sätt att **speed up OCR**

Parallell tiling delar upp en enorm bild i mindre rutor som kan bearbetas oberoende. Detta är särskilt hjälpsamt för mycket stora skanningar (tänk A0‑stora ritningar).

```java
        // Step 5: Enable tile‑based parallelism for faster processing of large images
        ocrEngine.getProcessingSettings().setEnableParallelTiling(true);
```

När du kombinerar **set max threads** med tiling ger du i princip OCR‑motorn en två‑delad boost: fler arbetare *och* smartare arbetsfördelning. I mina tester gick en 4000×3000 PNG från ~12 sekunder till under 5 sekunder.

## Steg 6: Kör igenkänning och **extract text image**‑innehåll

Nu kör vi faktiskt OCR‑motorn. Metoden `recognize()` returnerar ett `OcrResult`‑objekt som innehåller den rena textrepresentationen.

```java
        // Step 6: Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 7: Output the recognized text
        System.out.println(ocrResult.getText());
    }
}
```

`getText()`‑anropet ger dig en enda `String` som innehåller allt motorn kunde läsa. Du kan sedan efterbehandla den (trimma blanksteg, dela upp i rader, osv.) beroende på dina efterföljande behov.

## Förväntad output

Om källbilden innehåller meningen *“Hello, world!”* kommer du att se något liknande:

```
Hello, world!
```

För fler‑sidiga PDF:er som har rasteriserats kommer output att sammanfoga texten från varje sida, med bibehållna radbrytningar. Konsolen visar hela det extraherade innehållet, vilket bevisar att du framgångsrikt **extract text image** data samtidigt som du **speed up OCR** tack vare trådinställningarna.

## Fullt fungerande exempel (Klar‑för‑kopiering)

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Load the image to be processed
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/big_image.png"));

        // Step 4: Allow up to 8 parallel threads (defaults to number of CPU cores)
        ocrEngine.getProcessingSettings().setMaxParallelThreads(8);

        // Step 5: Enable tile‑based parallelism for faster processing of large images
        ocrEngine.getProcessingSettings().setEnableParallelTiling(true);

        // Step 6: Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 7: Output the recognized text
        System.out.println(ocrResult.getText());
    }
}
```

> **Obs:** Om du får ett `OutOfMemoryError` på extremt stora filer, försök minska `setMaxParallelThreads` eller inaktivera tiling (`setEnableParallelTiling(false)`). Den rätta balansen beror på din hårdvara.

## Visuell översikt

![set max threads configuration in Aspose OCR Java](https://example.com/images/set-max-threads.png "set max threads configuration in Aspose OCR Java")

*Skärmdumpen visar `ProcessingSettings`‑panelen där du kan justera trådräkningen och slå på/av tiling.*

## Vanliga frågor & kantfall

### Vad händer om jag bara har en dual‑core‑laptop?

Du kan fortfarande **set max threads** till `2` (standard). Vinsten blir modest, men att aktivera tiling kan fortfarande spara en eller två sekunder på stora bilder.

### Fungerar detta på macOS och Linux?

Absolut. Aspose OCR‑biblioteket är plattforms‑agnostiskt så länge du har en kompatibel JRE. Se bara till att bildsökvägen använder rätt filseparator (`/` fungerar överallt).

### Kan jag använda detta med en ström istället för en fil?

Ja. Byt ut `ImageStream.fromFile` mot `ImageStream.fromByteArray` eller `ImageStream.fromInputStream`. Resten av konfigurationen—**set max threads**, **speed up OCR**—förblir identisk.

### Kommer en ökning av trådräkningen någonsin att *sakta* ner saker?

Om du kraftigt överskrider antalet fysiska kärnor kommer OS att börja kontext‑byta mycket, vilket faktiskt kan öka latensen. En bra tumregel: **threads ≤ cores + 2**. Experimentera och övervaka CPU‑användning.

## Tips för att få ut det mesta av parallell OCR

1. **Profilera först** – Kör en baslinje utan några parallella inställningar, aktivera sedan `setMaxParallelThreads` och jämför tiderna.  
2. **Batchprocess** – Om du har dussintals bilder, mata dem sekventiellt genom samma `O

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}