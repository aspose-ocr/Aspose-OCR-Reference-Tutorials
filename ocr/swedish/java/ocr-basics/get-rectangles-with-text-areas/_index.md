---
date: 2025-12-10
description: Lär dig hur du känner igen text från en bild och extraherar stycken från
  en bild med Aspose.OCR för Java. Steg‑för‑steg‑guide med kodexempel.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: Identifiera text från bild och hämta rektanglar för textområden
url: /sv/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Känn igen text från bild och hämta rektanglar för textområden

## Introduktion

Om du behöver **känna igen text från bild**‑filer i en Java‑applikation, erbjuder Aspose.OCR för Java ett snabbt och exakt sätt att göra det. I den här handledningen går vi igenom de exakta stegen som krävs för att extrahera stycken från en bild, hämta de omgivande rektanglarna för varje textområde och skriva ut dessa koordinater i konsolen. När du är klar förstår du varför detta tillvägagångssätt fungerar, hur du integrerar biblioteket och var du kan utöka det för dina egna användningsfall.

## Snabba svar
- **Vad betyder “känna igen text från bild”?** Det innebär att konvertera visuella tecken i en bild till redigerbara strängdata.  
- **Vilket bibliotek hanterar detta i Java?** Aspose.OCR för Java.  
- **Behöver jag en licens för utveckling?** En tillfällig licens finns tillgänglig för testning; en fullständig licens krävs för produktion.  
- **Kan jag extrahera stycken istället för enskilda ord?** Ja – använd `AreasType.PARAGRAPHS` för att få rektanglar på styckennivå.  
- **Är koden kompatibel med Java 11+?** Absolut, API‑et fungerar med Java 11 och senare.

## Vad betyder “känna igen text från bild” i Aspose.OCR?
Aspose.OCR:s `RecognizePage`‑metod analyserar bitmapen, tillämpar OCR‑algoritmer och returnerar den igenkända strängen. När du begär textområden beräknar biblioteket också de exakta `Rectangle`‑koordinaterna för varje textblock, vilket gör det enkelt att markera eller bearbeta specifika sektioner senare.

## Varför använda Aspose.OCR för Java?
- **Hög precision** – stödjer flera språk och komplexa typsnitt.  
- **Enkel integration** – en enda JAR‑fil ger full OCR‑funktionalitet.  
- **Flexibel output** – du kan hämta råtext, formaterad HTML eller exakta rektanglar för textområden.  
- **Trådsäker** – lämplig för högkapacitets servermiljöer.

## Förutsättningar

- **Java Development Kit** (JDK 11 eller nyare) installerat på din maskin.  
- **Aspose.OCR för Java**‑bibliotek – ladda ner det från den officiella sidan [här](https://releases.aspose.com/ocr/java/).  
- En IDE eller byggverktyg (Maven/Gradle) för att hantera JAR‑beroendet.

## Importera paket

I ditt Java‑projekt importerar du de nödvändiga klasserna:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Steg‑för‑steg‑guide

### Steg 1: Ställ in ditt projekt
Skapa ett nytt Java‑projekt (eller lägg till i ett befintligt) och placera Aspose.OCR‑JAR‑filen på klassvägen. Om du använder Maven, lägg till beroendet enligt beskrivningen i nedladdningspaketet.

### Steg 2: Definiera dokumentkatalog och bildsökväg
Ange var din exempelbild finns:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Steg 3: Skapa Aspose.OCR‑instans
Instansiera OCR‑motorn:

```java
// Create Aspose.OCR instance
AsposeOCR api = new AsposeOCR();
```

### Steg 4: Känn igen text i bilden
Anropa `RecognizePage` för att konvertera bilden till vanlig text. Detta steg demonstrerar kärnfunktionen **känna igen text från bild**:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Steg 5: Hämta rektanglar med textområden
Nu hämtar du de omgivande rektanglarna för varje stycke (eller annan områdestyp). Här **extraherar du stycken från bild** och får deras koordinater:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Vanliga problem & felsökning

| Symptom | Trolig orsak | Åtgärd |
|---------|--------------|-----|
| `IOException` på `RecognizePage` | Felaktig filsökväg eller saknad läsbehörighet | Verifiera att `imagePath` pekar på en befintlig PNG/JPG och att appen har åtkomst till filsystemet. |
| Tom resultatsträng | Bild av låg kvalitet eller språk som inte stöds | Förbehandla bilden (öka kontrast, binarisera) eller ange rätt språk med `api.setLanguage("eng")`. |
| Inga rektanglar returneras | Fel `AreasType` används (t.ex. `WORDS` när du förväntar dig stycken) | Byt till `AreasType.PARAGRAPHS` eller `AreasType.LINES` efter behov. |

## Vanliga frågor

**Q: Är Aspose.OCR kompatibel med Java 11?**  
A: Ja, Aspose.OCR fungerar med Java 11 och senare versioner.

**Q: Kan jag använda Aspose.OCR för både personliga och kommersiella projekt?**  
A: Ja, du kan använda det i alla typer av projekt. För licensinformation, besök [här](https://purchase.aspose.com/buy).

**Q: Hur får jag en tillfällig licens för utvärdering?**  
A: Du kan skaffa en tillfällig licens [här](https://purchase.aspose.com/temporary-license/).

**Q: Var kan jag hitta community‑support eller officiell hjälp?**  
A: För support och diskussioner, besök [Aspose.OCR‑forumet](https://forum.aspose.com/c/ocr/16).

**Q: Stöder Aspose.OCR multitrådning?**  
A: Ja, biblioteket är trådsäkert och kan användas i samtidiga miljöer för bättre prestanda.

## Slutsats

I den här handledningen har du lärt dig hur du **känner igen text från bild**‑filer med Aspose.OCR för Java, extraherar stycken och hämtar de exakta rektanglar som omger varje textblock. Dessa funktioner låter dig bygga sökbara PDF‑filer, markera text i UI‑överlägg eller mata strukturerad data till efterföljande processer. Utforska API‑et vidare för att anpassa språkinställningar, hantera olika bildformat eller integrera med molnlagring.

---

**Senast uppdaterad:** 2025-12-10  
**Testad med:** Aspose.OCR 23.10 för Java  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}