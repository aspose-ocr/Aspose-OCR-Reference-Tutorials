---
category: general
date: 2026-05-06
description: Hur man använder OCR för att extrahera text från en bild i Java. Lär
  dig OCR bild‑till‑text‑konvertering, korrigera OCR‑fel och ladda bild för OCR med
  Aspose OCR.
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: sv
og_description: Hur man använder OCR i Java för att extrahera text från en bild, korrigera
  OCR‑fel och ladda bild för OCR med Aspose OCR.
og_title: Hur man använder OCR i Java – Komplett guide
tags:
- OCR
- Java
- Aspose
title: Hur du använder OCR i Java – Extrahera text från en bild med stavningskorrigering
url: /sv/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder OCR i Java – Extrahera text från bild med stavningskorrigering

Har du någonsin undrat **hur man använder OCR** för att förvandla ett suddigt kvittosfoto till ren, sökbar text? Du är inte ensam. I många projekt—utgiftsspårningsappar, fakturadigitaliseringspipelines eller till och med ett snabbt anteckningsskript—är det första hindret att få pålitlig text från en bild.  

Denna handledning visar exakt hur du använder OCR i Java, och täcker allt från att ladda bilden för OCR till att korrigera OCR‑fel så att resultatet läses som om det skrivits av en människa. I slutet kommer du att kunna **extrahera text från bild**, utföra **OCR bild till text**‑konvertering och automatiskt rätta vanliga igenkänningsfel.

## Vad du kommer att bygga

Vi kommer att skapa ett litet Java‑konsolprogram som:

1. Laddar en PNG (eller något annat stödd format) i Aspose OCR‑motorn.  
2. Aktiverar den inbyggda stavningskorrigeringsfunktionen för att **korrigera OCR‑fel**.  
3. Kör igenkänningsprocessen och skriver ut den rensade texten.  

Ingen extern tjänst, inga tunga ramverk—bara en enda JAR och några rader kod.

### Förutsättningar

- Java Development Kit (JDK) 8 eller nyare.  
- Maven (eller något annat byggverktyg) för att hämta Aspose OCR‑biblioteket.  
- En bildfil (t.ex. `receipt.png`) som du vill analysera.  

Om du saknar Aspose OCR‑JAR‑filen, lägg till detta beroende i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **Proffstips:** Den kostnadsfria utvärderingsversionen fungerar för testning, men en licens tar bort utvärderingsvattenstämpeln.

## Steg 1 – Initiera OCR‑motorn (Primärt nyckelord i handling)

Det första du måste göra är att skapa en instans av `OcrEngine`. Tänk på den som hjärnan som läser pixlarna och omvandlar dem till tecken.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*Varför detta är viktigt:* Att initiera motorn sätter upp interna resurser (språkmodeller, ordböcker osv.). Att hoppa över detta steg skulle leda till ett `NullPointerException` senare när du försöker ladda en bild.

## Steg 2 – Ladda bild för OCR

Nu **laddar vi faktiskt bilden för OCR**. Aspose tillhandahåller en bekväm `ImageStream.fromFile`‑hjälp, men du kan också mata in en `byte[]` om du föredrar det.

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*Vanligt fallgropp:* Filvägen måste vara absolut eller relativ till arbetskatalogen. Om bilden inte kan hittas kastar motorn ett `IOException`. Dubbelkolla sökvägen, särskilt när du kör från en IDE jämfört med en paketerad JAR.

## Steg 3 – Aktivera stavningskorrigering för att **korrigera OCR‑fel**

Standard‑OCR kan vara bullrigt—tänk “l0ve” istället för “love” eller “0” för “O”. Att aktivera stavningskorrigering får motorn att köra ett efterbearbetningssteg som rättar vanliga misstag.

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*Varför du vill ha detta:* Utan stavningskorrigering kan du behöva rensa utdata manuellt, vilket undergräver automatiseringens syfte. Den inbyggda ordboken fungerar bra för engelska och flera andra språk.

## Steg 4 – Utför igenkänning (**OCR bild till text**)

Med bilden laddad och stavningskorrigering aktiverad kan vi äntligen be motorn att känna igen texten.

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*Edge case:* Om bilden har låg kontrast eller är kraftigt snedvriden kan resultatet fortfarande innehålla nonsens. Överväg förbehandling (t.ex. binarisering, räta upp) innan du matar den till motorn.

## Steg 5 – Skriv ut den rensade texten

Det sista steget är helt enkelt att skriva ut resultatet. I en riktig applikation kan du skriva det till en databas eller en fil, men för den här demonstrationen räcker `System.out`.

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Förväntad utdata

Om vi antar att `receipt.png` innehåller en tydlig lista över varor, kan du se något liknande:

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

Observera hur “Qty” och “Price” är stavade korrekt även om den ursprungliga skanningen hade ett felaktigt “Qy”.

## Fullt fungerande exempel

Nedan är det kompletta programmet som du kan kopiera och klistra in i en fil med namnet `SpellCorrectDemo.java`. Se till att Aspose OCR‑JAR‑filen finns i din classpath.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

Kör det med:

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

Du bör nu se den rensade texten skriven till konsolen.

## Bonus: Justera inställningar för bättre noggrannhet

Även om standardkonfigurationen fungerar för de flesta tryckta dokument, kan du behöva justera några parametrar för specialiserade scenarier:

| Inställning | Vad den gör | När du bör ändra |
|-------------|--------------|------------------|
| `setLanguage(OcrLanguage.English)` | Tvingar engelsk ordbok (minskar falska positiva) | Om din bild bara innehåller engelsk text. |
| `setResolution(300)` | Anger motorns DPI för källbilden | För högupplösta skanningar. |
| `setEnableAutoSkewCorrection(true)` | Roterar automatiskt lätt snedvridna sidor | När bilder tas med en telefon. |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## Vanliga frågor

**Q: Fungerar detta med PDF‑filer?**  
A: Ja. Konvertera varje PDF‑sida till en bild (t.ex. med Aspose PDF) och mata in bilden i OCR‑motorn.

**Q: Vad händer om min bild är i BMP‑format?**  
A: `ImageStream.fromFile` stödjer PNG, JPEG, BMP, TIFF och GIF direkt. Ändra bara filändelsen.

**Q: Kan jag inaktivera stavningskorrigering?**  
A: Absolut—sätt `setEnableSpellCorrection(false)` om du behöver rå OCR‑utdata för vidare bearbetning.

## Slutsats

Du vet nu **hur man använder OCR** i Java för att **extrahera text från bild**, automatiskt **korrigera OCR‑fel**, och korrekt **ladda bild för OCR** med Aspose OCR. Det femstegsflödet—initiera, ladda, aktivera stavningskorrigering, känna igen och skriva ut—täcker majoriteten av vanliga OCR‑uppgifter.  

Från och med nu kan du överväga att kedja denna logik med en databasskrivning, ett REST‑slutpunkt eller en batch‑processor för att hantera dussintals kvitton samtidigt. Experimentera med tabellen med extra inställningar ovan för att pressa ut varje sista tecken av noggrannhet.

Lycka till med kodningen, och må dina OCR‑resultat alltid vara renare än dina kaffefläckade kvitton! 

![diagram som visar bild → OCR‑motor → korrigerad textflöde]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}