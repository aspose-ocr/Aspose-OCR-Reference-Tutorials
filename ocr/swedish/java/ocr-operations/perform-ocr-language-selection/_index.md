---
date: 2025-12-13
description: Lär dig hur du extraherar text från en bild med Aspose.OCR för Java med
  språkval. Denna steg‑för‑steg Aspose OCR Java‑handledning visar exakt OCR‑konfiguration.
linktitle: How to Extract Text from Image with Language Selection Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Hur man extraherar text från en bild med språkval med Aspose.OCR
url: /sv/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man extraherar text från bild med språkval med Aspose.OCR

## Introduktion

Att extrahera text från bildfiler är ett vanligt behov, oavsett om du digitaliserar skannade dokument, bearbetar kvitton eller bygger sökbara arkiv. Aspose.OCR för Java gör denna uppgift enkel och ger dig fin‑granulär kontroll över språkval, skevningskorrigering och igenkänningsområden. I den här handledningen går vi igenom ett komplett, praktiskt exempel som visar **hur man extraherar text från bild** med en specifik språkinställning, så att du kan integrera pålitlig OCR i dina Java‑applikationer redan idag.

## Snabba svar
- **Vilket bibliotek hanterar OCR i Java?** Aspose.OCR för Java  
- **Vilken inställning väljer språket?** `settings.setLanguage(Language.Eng)` (eller något annat stöd­järt språk)  
- **Behöver jag en licens för utveckling?** En gratis utvärderingslicens fungerar för testning; en kommersiell licens krävs för produktion.  
- **Kan jag begränsa OCR till ett område i bilden?** Ja, använd `RecognitionSettings.setRecognitionAreas()` med rektanglar.  
- **Vad är den typiska körtiden?** Några sekunder per sida på en vanlig laptop, beroende på bildstorlek och språkets komplexitet.

## Vad betyder “extrahera text från bild”?
Att extrahera text från bild (OCR) omvandlar den visuella representationen av tecken till maskinläsbara strängar. Detta möjliggör sökning, analys och datautvinningsarbetsflöden som annars skulle kräva manuell transkription.

## Varför använda Aspose.OCR med språkval?
- **Flerspråkigt stöd** – Välj exakt de språk som finns i din bild för att öka noggrannheten.  
- **Finjusterad kontroll** – Justera skevning, definiera igenkänningsområden och ställ in auto‑skevningsbeteende.  
- **Rent Java‑API** – Inga inhemska beroenden, enkelt att integrera i vilket Java‑projekt som helst.  
- **Rik resultatdata** – Få vanlig text, JSON, avgränsande rektanglar och varningar i ett enda anrop.

## Förutsättningar

Innan du börjar, se till att du har:

- **Java Development Kit (JDK)** installerat (JDK 8 eller senare).  
- **Aspose.OCR för Java**‑biblioteket – ladda ner det från den officiella sidan [here](https://reference.aspose.com/ocr/java/).  
- En bildfil som innehåller den text du vill extrahera, t.ex. `p3.png`.

## Importera paket

I din Java‑källfil, inkludera de nödvändiga Aspose.OCR‑klasserna och vanliga Java‑verktyg:

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

Här gör vi:

1. Inaktiverar auto‑skevning eftersom vi anger ett manuellt skevningsvärde.  
2. Definierar ett rektangulärt område (`RecognitionAreas`) för att begränsa OCR till den del av bilden som faktiskt innehåller text.  
3. Sätter **språket** till engelska (`Language.Eng`). Ändra detta till `Language.Fra`, `Language.Spa` osv., beroende på din källbild.

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

Anropet `RecognizePage` kör OCR‑motorn med bilden och de inställningar du definierat. Resultatet lagras i ett `RecognitionResult`‑objekt.

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

Konsolutskriften visar:

- Den fullständiga extraherade texten (`recognitionText`).  
- Text för varje definierat rektangel (`recognitionAreasText`).  
- Koordinater för avgränsande rektanglar.  
- En JSON‑representation för enkel vidarebehandling.  
- Upptäckt skevningsvinkel och eventuella varningar.

Du kan nu föra `result.recognitionText` in i din affärslogik – lagra den, indexera den eller skicka den till en annan tjänst.

## Vanliga problem och lösningar

| Problem | Orsak | Lösning |
|-------|-------|-----|
| **Skräptecken** | Fel språk valt | Ange rätt `Language`‑enum (t.ex. `Language.Fra` för franska). |
| **Ingen text returneras** | Igenkänningsområdet täcker inte texten | Justera `Rectangle`‑koordinaterna eller ta bort `RecognitionAreas` för att bearbeta hela bilden. |
| **Långsam prestanda** | Mycket stor bild eller hög upplösning | Skala ner bilden innan OCR eller öka minnesallokeringen för JVM. |
| **Varningar om ej stödformat** | Bildformatet känns inte igen | Konvertera bilden till PNG, JPEG eller TIFF innan bearbetning. |

## Vanliga frågor

**Q: Kan jag känna igen flera språk i ett enda OCR‑anrop?**  
A: Ja. Använd `settings.setLanguage(Language.Eng \| Language.Fra)` för att aktivera flerspråkig igenkänning.

**Q: Vilka bildformat stöder Aspose.OCR?**  
A: PNG, JPEG, BMP, TIFF, GIF och flera andra. Ange bara rätt filsökväg.

**Q: Finns det någon storleksgräns för bilden?**  
A: Det finns ingen hård gräns, men mycket stora bilder ökar minnesanvändning och bearbetningstid. Överväg att ändra storlek på stora filer.

**Q: Hur får jag en produktionslicens?**  
A: Köp en licens från Aspose‑webbplatsen och applicera den via `License`‑klassen enligt Aspose‑dokumentationen.

**Q: Kan jag extrahera text direkt från en PDF‑sida?**  
A: Inte direkt med Aspose.OCR. Konvertera PDF‑sidan till en bild först (t.ex. med Aspose.PDF) och kör sedan OCR.

## Slutsats

Du har nu sett hur du **extraherar text från bild** med Aspose.OCR för Java samtidigt som du väljer rätt språk och begränsar igenkänning till specifika områden. Detta tillvägagångssätt levererar exakt, högpresterande OCR som kan inbäddas i vilket Java‑baserat arbetsflöde som helst – från dokumenthanteringssystem till datainsamlingspipelines.

---

**Senast uppdaterad:** 2025-12-13  
**Testad med:** Aspose.OCR 24.11 för Java  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}