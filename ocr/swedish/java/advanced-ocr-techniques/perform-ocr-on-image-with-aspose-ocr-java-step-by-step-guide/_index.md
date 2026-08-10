---
category: general
date: 2026-02-14
description: Lär dig hur du utför OCR på en bild och extraherar text från bilden med
  Aspose OCR i Java. Inkluderar inläsning av bild för OCR, anpassat lexikon och stavningskorrigering.
draft: false
keywords:
- perform OCR on image
- extract text from image
- load image for OCR
- Aspose OCR Java
- spell correction OCR
language: sv
og_description: Utför OCR på bild i Java med Aspose OCR. Den här guiden visar hur
  du laddar bild för OCR, extraherar text från bilden och aktiverar stavningskorrigering.
og_title: Utför OCR på bild – Komplett Java‑handledning
tags:
- OCR
- Java
- Aspose
title: Utför OCR på bild med Aspose OCR – Java steg‑för‑steg guide
url: /sv/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

Keep them.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utför OCR på bild – Komplett Java‑handledning

Har du någonsin behövt **utföra OCR på bild**‑filer men varit osäker på var du ska börja? Du är inte ensam; många utvecklare stöter på samma problem när de första gången försöker extrahera text från bilddata. Den goda nyheten är att med Aspose OCR för Java kan du få pålitliga resultat på bara några rader kod—plus att du kan öka noggrannheten med en anpassad ordlista och stavningskontroll.

I den här guiden går vi igenom allt du behöver veta: från att ladda bild för OCR, till att aktivera stavningskorrigering, och slutligen skriva ut den rensade texten. I slutet kommer du att kunna **utföra OCR på bild**‑tillgångar i dina egna Java‑projekt, och du kommer också att se hur du **extraherar text från bild**‑filer på ett sätt som fungerar även med brusiga skanningar.

## Vad du behöver

- **Java Development Kit (JDK) 8+** – koden använder standard‑Java‑API:er.
- **Aspose OCR for Java**‑biblioteket (du kan hämta den senaste JAR‑filen från Aspose‑webbplatsen eller Maven Central).
- En bildfil (t.ex. `invoice.png`) som du vill bearbeta.
- (Valfritt) En ren‑text‑fil `custom_dict.txt` som innehåller domänspecifika ord, ett per rad.

Det är allt—inga tunga ramverk, inga externa tjänster. Bara ren Java och Aspose OCR‑JAR‑filen.

## Steg 1: Ställ in projektet och importera beroenden

Först, skapa ett nytt Maven‑ (eller Gradle‑) projekt och lägg till Aspose OCR‑beroendet. Om du använder Maven bör din `pom.xml` innehålla:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

Om du föredrar att ladda ner JAR‑filen manuellt, lägg den i din `libs`‑mapp och lägg till den i klassökvägen.

> **Pro tip:** Verifiera alltid versionsnumret vid skrivandet; nyare versioner kan introducera ytterligare funktioner som språkpaket.

## Steg 2: Ladda bilden för OCR

Det första riktiga kodsteget är att rikta OCR‑motorn mot bilden du vill analysera. Aspose OCR använder en `ImageStream`‑wrapper som kan läsa från en fil, en byte‑array eller till och med en URL.

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

Observera hur vi **laddar bild för OCR** med ett enda metodanrop—ingen krånglig `BufferedImage`‑gymnastik behövs. Om din bild finns i resurser, ersätt bara sökvägen med `getClass().getResourceAsStream(...)`.

## Steg 3: Aktivera stavningskorrigering (valfritt men kraftfullt)

Aspose OCR kan automatiskt korrigera vanliga OCR‑fel (som “l” vs “1”). Att slå på den här funktionen är så enkelt som att växla en flagga:

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

Varför bry sig? Föreställ dig att skanna en utskriven faktura där teckensnittet är litet och skannern introducerar oönskade fläckar. Stavningskorrigering kommer ofta att omvandla “Inv0ice” tillbaka till “Invoice” utan extra arbete från dig.

## Steg 4: Tillhandahåll en anpassad ordlista (skräddarsy motorn)

Om du arbetar med branschspecifik terminologi—tänk medicinska koder, juridisk jargong eller produkt‑SKU:er—kan en anpassad ordlista förbättra noggrannheten avsevärt. Ordlistan är bara en textfil med ett ord per rad.

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

Se till att filen använder UTF‑8‑kodning; annars kan du få förvrängda tecken för icke‑ASCII‑ord.

## Steg 5: Kör OCR‑processen

Nu låter vi äntligen motorn göra sin magi. `process()`‑anropet returnerar ett `OcrResult`‑objekt som innehåller den igenkända texten, förtroendesiffror och till och med layouten om du behöver den senare.

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

Om du någonsin undrar om motorn kastade ett undantag, omslut detta anrop i ett try‑catch‑block och inspektera `ocrResult.getErrorMessage()` för detaljer.

## Steg 6: Skriv ut den igenkända (och korrigerade) texten

Det sista steget är att visa—eller lagra—den extraherade strängen. För en snabb demo skriver vi bara ut den i konsolen:

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

Att köra programmet bör skriva ut något liknande:

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

Om du ser oönskade tecken, dubbelkolla din anpassade ordlista och överväg att justera bildkvaliteten (t.ex. öka kontrasten innan du matar den till motorn).

### Fullt fungerande exempel

När vi sätter ihop allt, här är den kompletta, körklara klassen:

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

Spara den här filen som `SpellCorrectDemo.java`, justera sökvägarna, kompilera med `javac` och kör med `java SpellCorrectDemo`. Du bör nu **utföra OCR på bild**‑filer och se den extraherade texten skrivas ut.

## Vanliga frågor & kantfall

### Vad händer om bilden är i ett annat format (PDF, TIFF, etc.)?

Aspose OCR kan hantera många rasterformat direkt. För PDF‑filer måste du först extrahera varje sida som en bild—Aspose PDF för Java gör det smidigt. Samma `setImage`‑anrop fungerar när du har en `BufferedImage` eller en byte‑ström.

### Hur hanterar jag flersidiga dokument?

Loopa över varje sidobild, kör OCR‑stegen och sammanfoga resultaten. Kom ihåg att återställa eller skapa en ny `OcrEngine` för varje sida om du vill ha oberoende stavningskontrollkontexter.

### Kan jag begränsa språk eller teckenuppsättning?

Ja. Använd `ocrEngine.getEngineOptions().setLanguage(Language.English);` (eller något annat stödd språk) för att minska falska positiva och snabba upp bearbetningen.

### Vad gäller prestanda för stora batcher?

Aspose OCR är trådsäker för endast‑läs‑operationer. Du kan starta en trådpool och bearbeta bilder parallellt—undvik bara att dela samma `OcrEngine`‑instans mellan trådar.

## Tips för bättre noggrannhet

- **Förbehandla bilden**: öka kontrasten, ta bort bakgrundsbrus eller konvertera till gråskala.
- **Använd en högupplöst skanning** (300 dpi eller högre). Lägre upplösningar ger ofta förvrängda tecken.
- **Håll den anpassade ordlistan slank**: för många orelaterade ord kan förvirra stavningskontrollen.
- **Validera resultatet**: om du känner till det förväntade formatet (t.ex. datum, siffror), kör en regex‑efterbehandling för att fånga avvikelser.

## Nästa steg

Nu när du kan **utföra OCR på bild**‑filer och **extrahera text från bild** med Aspose OCR, kanske du vill utforska:

- **Spara OCR‑utdata till en PDF** med sökbara textlager.
- **Integrera med en databas** för att automatiskt lagra extraherad fakturadata.
- **Tillämpa maskininlärnings‑efterbehandling** för ännu högre noggrannhet på handskrivna anteckningar.
- **Använda `load image for OCR`‑flaggan** i en webbtjänst som accepterar användaruppladdade bilder.

Var och en av dessa ämnen bygger på de grundläggande stegen vi gick igenom, så du kommer att finna övergången smidig.

---

*Lycklig kodning! Om du stöter på problem, tveka inte att lämna en kommentar—inget slår att lära sig av verkliga exempel.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}