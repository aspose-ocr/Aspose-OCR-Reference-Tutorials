---
date: 2026-02-12
description: Lär dig hur du OCR:ar bildtext med språkval med Aspose.OCR för Java.
  Denna steg‑för‑steg‑guide täcker extrahering av text i Java, OCR‑snedkorrigering
  och mer.
linktitle: How to OCR Image Text with Language Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Hur man OCR:ar bildtext med språk med Aspose.OCR
url: /sv/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man OCR:ar bildtext med språk med Aspose.OCR

## Introduktion

Att extrahera text från bildfiler är ett vanligt behov, oavsett om du digitaliserar skannade dokument, bearbetar kvitton eller bygger sökbara arkiv. I den här handledningen går vi igenom ett komplett, praktiskt exempel som visar **hur man OCR:ar bildtext** med en specifik språkinställning, så att du kan integrera pålitlig OCR i dina Java‑applikationer idag. Du får också se hur du hanterar OCR‑skevkorrektion och regionsbaserad igenkänning för optimal noggrannhet.

## Snabba svar
- **Vilket bibliotek hanterar OCR i Java?** Aspose.OCR for Java  
- **Vilken inställning väljer språket?** `settings.setLanguage(Language.Eng)` (or any supported language)  
- **Behöver jag en licens för utveckling?** En gratis utvärderingslicens fungerar för testning; en kommersiell licens krävs för produktion.  
- **Kan jag begränsa OCR till en region i bilden?** Ja, använd `RecognitionSettings.setRecognitionAreas()` med rektanglar.  
- **Vad är den typiska körtiden?** Några sekunder per sida på en standardlaptop, beroende på bildstorlek och språkkomplexitet.

## Hur man OCR:ar bildtext med språkval
I det här avsnittet svarar vi på huvudfrågan **hur man OCR:ar** en bild när du känner till textens språk. Att välja rätt språk förbättrar igenkänningsnoggrannheten dramatiskt eftersom OCR‑motorn kan använda språk‑specifika ordböcker och teckenmodeller.

### Varför detta är viktigt
- **Högre noggrannhet** – språk‑specifika modeller minskar felaktiga igenkänningar.  
- **Prestandaförbättring** – motorn hoppar över onödiga språkkontroller.  
- **Bättre hantering av diakritiska tecken** – franska, spanska, tyska osv. känns igen korrekt när motsvarande `Language`‑enum används.

## Vad är “extrahera text från bild”?
Att extrahera text från en bild (OCR) omvandlar den visuella representationen av tecken till maskinläsbara strängar. Detta möjliggör sökning, analys och dataextraktionsarbetsflöden som annars skulle kräva manuell transkription.

## Varför använda Aspose.OCR med språkval?
- **Flerspråkigt stöd** – Välj exakt språk(en) som finns i din bild för att öka noggrannheten.  
- **Finjusterad kontroll** – Justera skevhet, definiera igenkänningsområden och ställ in automatisk skevhetsbeteende.  
- **Ren Java‑API** – Inga inhemska beroenden, enkelt att integrera i vilket Java‑projekt som helst.  
- **Rik resultatdata** – Få ren text, JSON, avgränsningsrektanglar och varningar i ett anrop.

## Förutsättningar

Innan du börjar, se till att du har:

- **Java Development Kit (JDK)** installed (JDK 8 or later).  
- **Aspose.OCR for Java** library – download it from the official site [here](https://reference.aspose.com/ocr/java/).  
- En bildfil som innehåller den text du vill extrahera, t.ex. `p3.png`.

## Importera paket

I din Java‑källfil, inkludera de nödvändiga Aspose.OCR‑klasserna och standard‑Java‑verktygen:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Steg‑för‑steg‑guide

### Steg 1: Ställ in din dokumentkatalog

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Byt ut `"Your Document Directory"` mot den absoluta sökvägen där `p3.png` finns.

### Steg 2: Definiera bildens sökväg

```java
// The image path
String file = dataDir + "p3.png";
```

Se till att variabeln `file` pekar på exakt den bild du avser att bearbeta.

### Steg 3: Skapa Aspose.OCR‑API‑instans

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR`‑objektet ger dig åtkomst till alla OCR‑operationer.

### Steg 4: Ställ in igenkänningsalternativ (språkval)

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Här:

1. Inaktivera automatisk skevhet eftersom vi tillhandahåller ett manuellt skevhetsvärde.  
2. Definiera en rektangulär region (`RecognitionAreas`) för att begränsa OCR till den del av bilden som faktiskt innehåller text.  
3. Ställ in **språket** till engelska (`Language.Eng`). Ändra detta till `Language.Fra`, `Language.Spa` osv., beroende på din källbild.

### Steg 5: Utför OCR och hämta resultat

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

`RecognizePage`‑anropet kör OCR‑motorn med bilden och de inställningar du definierat. Resultatet lagras i ett `RecognitionResult`‑objekt.

### Steg 6: Skriv ut och använd resultat

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

Konsolutdata visar:

- Den fullständiga extraherade texten (`recognitionText`).  
- Text för varje definierad rektangel (`recognitionAreasText`).  
- Koordinater för avgränsningsrektangeln.  
- En JSON‑representation för enkel efterföljande bearbetning.  
- Detekterad skevhetsvinkel och eventuella varningar.

Du kan nu mata `result.recognitionText` in i din affärslogik – lagra den, indexera den eller skicka den till en annan tjänst.

## Vanliga problem och lösningar

| Problem | Orsak | Lösning |
|-------|-------|-----|
| **Skräptecken** | Fel språk valt | Ställ in rätt `Language`‑enum (t.ex. `Language.Fra` för franska). |
| **Ingen text returnerad** | Igenkänningsområdet täcker inte texten | Justera `Rectangle`‑koordinaterna eller ta bort `RecognitionAreas` för att bearbeta hela bilden. |
| **Långsam prestanda** | Mycket stor bild eller hög upplösning | Skala ner bilden innan OCR eller öka minnesallokeringen för JVM. |
| **Varningar om ej stödd format** | Bildformatet känns inte igen | Konvertera bilden till PNG, JPEG eller TIFF innan bearbetning. |

## Vanliga frågor

**Q: Kan jag känna igen flera språk i ett enda OCR‑anrop?**  
A: Ja. Använd `settings.setLanguage(Language.Eng | Language.Fra)` för att aktivera flerspråkig igenkänning.

**Q: Vilka bildformat stöder Aspose.OCR?**  
A: PNG, JPEG, BMP, TIFF, GIF och flera andra. Ange bara rätt filsökväg.

**Q: Finns det någon storleksgräns för bilden?**  
A: Det finns ingen strikt gräns, men mycket stora bilder ökar minnesanvändning och bearbetningstid. Överväg att ändra storlek på stora filer.

**Q: Hur får jag en produktionslicens?**  
A: Köp en licens från Aspose‑webbplatsen och tillämpa den via `License`‑klassen som visas i Aspose‑dokumentationen.

**Q: Kan jag extrahera text från en PDF‑sida direkt?**  
A: Inte direkt med Aspose.OCR. Konvertera PDF‑sidan till en bild först (t.ex. med Aspose.PDF) och kör sedan OCR.

## Slutsats

Du har nu sett hur man **extraherar text från bild** med Aspose.OCR för Java samtidigt som du väljer rätt språk och begränsar igenkänningen till specifika regioner. Detta tillvägagångssätt levererar exakt, högpresterande OCR som kan integreras i vilket Java‑baserat arbetsflöde som helst – från dokumenthanteringssystem till datainsamlingspipelines. Redo att gå vidare? Prova att byta språk‑enum, experimentera med olika igenkänningsområden och integrera resultaten i din egen applikationslogik.

---

**Senast uppdaterad:** 2026-02-12  
**Testad med:** Aspose.OCR 24.11 for Java  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}