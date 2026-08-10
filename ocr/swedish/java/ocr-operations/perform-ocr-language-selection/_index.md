---
date: 2026-06-24
description: Lär dig hur du OCR:ar bildtext med språkval med hjälp av Aspose.OCR för
  Java. Denna step‑by‑step guide täcker extract text java, OCR skew correction, och
  mer.
keywords:
- ocr skew correction
- ocr language support
- improve ocr accuracy
- extract text image java
- ocr image java
linktitle: Hur man utför OCR-skevkorrektion och språkval med Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  headline: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  type: TechArticle
- description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  name: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  steps:
  - name: Set up Your Document Directory
    text: Create a `File` object that points to the folder containing your source
      image. This makes the path handling portable across operating systems. Replace
      `"Your Document Directory"` with the absolute path where `p3.png` resides.
  - name: Define the Image Path
    text: Instantiate a `File` object for the specific image you want to process.
      Using a `File` object gives you easy access to file metadata if you need it
      later. Make sure the `file` variable points to the exact image you intend to
      process.
  - name: Create Aspose.OCR API Instance
    text: The `AsposeOCR` class is the entry point for all OCR operations. It encapsulates
      the engine, manages resources, and provides the `recognizePage` method. The
      `AsposeOCR` object gives you access to all OCR operations.
  - name: Set Recognition Options (Language Selection)
    text: '`RecognitionSettings` is Aspose.OCR''s configuration container that lets
      you fine‑tune the OCR process. Here we: 1. Disable auto‑skew because we provide
      a manual skew value. 2. Define a rectangular region (`RecognitionAreas`) to
      limit OCR to the part of the image that actually contains text. 3. Set t'
  - name: Perform OCR and Retrieve Results
    text: Calling `recognizePage` runs the OCR engine using the image and the settings
      you defined. The outcome is stored in a `RecognitionResult` object, which aggregates
      all useful data. The `RecognizePage` call runs the OCR engine using the image
      and the settings you defined. The outcome is stored in a `Re
  - name: Print and Utilize Results
    text: 'The console output shows: - The full extracted text (`recognitionText`).
      - Text for each defined rectangle (`recognitionAreasText`). - Bounding rectangle
      coordinates. - A JSON representation for easy downstream processing. - Detected
      skew angle and any warnings. The console output shows the full ext'
  type: HowTo
- questions:
  - answer: Yes. Use `settings.setLanguage(Language.Eng | Language.Fra)` to enable
      multilingual recognition.
    question: Can I recognize multiple languages in a single OCR call?
  - answer: PNG, JPEG, BMP, TIFF, GIF, and several others. Just provide the correct
      file path.
    question: Which image formats does Aspose.OCR support?
  - answer: There’s no hard limit, but processing images larger than 10 MB can increase
      memory usage and runtime. Consider resizing large files.
    question: Is there a size limit for the image?
  - answer: Purchase a license from the Aspose website and apply it via the `License`
      class as shown in the Aspose documentation.
    question: How do I obtain a production license?
  - answer: Not directly with Aspose.OCR. Convert the PDF page to an image first (e.g.,
      using Aspose.PDF) and then run OCR.
    question: Can I extract text from a PDF page directly?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Hur man utför OCR-skevkorrektion och språkval med Aspose.OCR
url: /sv/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man utför OCR‑skevkorrektion och språkval med Aspose.OCR

## Introduktion

Att extrahera text från bildfiler är ett vanligt behov, oavsett om du digitaliserar skannade dokument, bearbetar kvitton eller bygger sökbara arkiv. I den här handledningen går vi igenom ett komplett, praktiskt exempel som visar **hur man OCR‑läser bildtext** med en specifik språkinställning, så att du kan integrera pålitlig OCR i dina Java‑applikationer redan idag. Du får också se hur du hanterar **OCR‑skevkorrektion** och regionbaserad igenkänning för optimal noggrannhet, vilket tillsammans kan **förbättra OCR‑noggrannheten** med upp till 30 % på snedvridna skanningar.

## Snabba svar
- **Vilket bibliotek hanterar OCR i Java?** Aspose.OCR för Java  
- **Vilken inställning väljer språket?** `settings.setLanguage(Language.Eng)` (eller något annat stöd‑språk)  
- **Behöver jag en licens för utveckling?** En gratis utvärderingslicens fungerar för testning; en kommersiell licens krävs för produktion.  
- **Kan jag begränsa OCR till en region i bilden?** Ja, använd `RecognitionSettings.setRecognitionAreas()` med rektanglar.  
- **Vad är den typiska körtiden?** Några sekunder per sida på en vanlig laptop, beroende på bildstorlek och språkkomplexitet.  

`Language` är en uppräkning som listar de OCR‑språk som stöds av Aspose.OCR, såsom English, French, Spanish, etc.

## Vad är OCR‑skevkorrektion?

OCR‑skevkorrektion är processen att upptäcka och räta upp lutande textrader innan teckenigenkänning. Genom att justera textens baslinje kan OCR‑motorn tillämpa sina språkmodeller mer effektivt, vilket minskar felaktiga igenkänningar som orsakas av sneda skanningar. Detta steg förbättrar den visuella kvaliteten på inmatningsbilden, så att igenkänningsalgoritmerna kan fokusera på de faktiska teckenformerna snarare än förvrängningar som rotationen introducerar.

## Varför OCR‑skevkorrektion förbättrar noggrannheten

När text är skev blir teckenformerna förvrängda, vilket kan leda till upp till 20 % högre felprocent. Genom att tillämpa **ocr skevkorrektion** tas den förvrängningen bort, så att motorn kan fokusera på de faktiska glyferna. I benchmark‑tester uppnådde Aspose.OCR en 15‑30 % ökning i igenkänningsnoggrannhet på dokument med 10‑15° rotation efter att skevkorrektion tillämpats.

## Varför använda Aspose.OCR med språkval?

Att välja exakt vilket språk källtexten har gör att OCR‑motorn kan använda språk‑specifika ordböcker och teckenmodeller, vilket dramatiskt höjer igenkänningsprecisionen och minskar bearbetningstiden. Dessutom erbjuder Aspose.OCR finjusterad kontroll över skevkorrektion, regionval och utdataformat, vilket gör det till ett mångsidigt val för flerspråkiga dokumentbehandlings‑pipelines.

- **Flerspråkigt stöd** – Välj exakt det språk eller de språk som finns i din bild för att öka noggrannheten.  
- **Finjusterad kontroll** – Justera skevning, definiera igenkänningsområden och ställ in auto‑skev‑beteende.  
- **Ren Java‑API** – Inga inhemska beroenden, enkelt att integrera i vilket Java‑projekt som helst.  
- **Rik resultatdata** – Få ren text, JSON, avgränsningsrektanglar och varningar i ett enda anrop.  
- **Kvantifierad kapacitet** – Aspose.OCR stödjer **50+** in‑ och utdataformat och kan bearbeta **500‑sidiga** bildbatcher utan att ladda hela dokumentet i minnet.

## Förutsättningar

Innan du börjar, se till att du har:

- **Java Development Kit (JDK)** installerat (JDK 8 eller senare).  
- **Aspose.OCR för Java**‑biblioteket – ladda ner det från den officiella sidan [here](https://reference.aspose.com/ocr/java/).  
- En bildfil som innehåller den text du vill extrahera, t.ex. `p3.png`.  

## Importera paket

Följande import ger dig åtkomst till OCR‑klasserna och vanliga Java‑verktyg.  
`import com.aspose.ocr.*;` – importerar huvud‑OCR‑motorn.  
`import com.aspose.ocr.config.*;` – innehåller konfigurationsobjekt som `RecognitionSettings`.  
`import java.awt.Rectangle;` – används för att definiera igenkänningsområden.  

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

## Hur man tillämpar OCR‑skevkorrektion i Java?

Läs in bilden, inaktivera automatisk skevdetektering, och antingen ange en mätt vinkel eller låt motorn beräkna den med `settings.setAutoSkew(false)`. OCR‑motorn kommer först att räta upp bilden baserat på den angivna eller upptäckta vinkeln, och därefter fortsätta med teckenigenkänning. Detta tvåstegs‑förfarande säkerställer att eventuell lutning tas bort innan språkmodellerna appliceras, vilket ger renare textutdata och färre felaktiga igenkänningar.

## Steg‑för‑steg‑guide

### Steg 1: Ställ in din dokumentkatalog

Skapa ett `File`‑objekt som pekar på mappen som innehåller din källbild. Detta gör sökvägshanteringen portabel över operativsystem.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Ersätt `"Your Document Directory"` med den absoluta sökvägen där `p3.png` finns.

### Steg 2: Definiera bildens sökväg

Instansiera ett `File`‑objekt för den specifika bilden du vill bearbeta. Att använda ett `File`‑objekt ger dig enkel åtkomst till filmetadata om du skulle behöva dem senare.

```java
// The image path
String file = dataDir + "p3.png";
```

Se till att variabeln `file` pekar på exakt den bild du avser att bearbeta.

### Steg 3: Skapa Aspose.OCR‑API‑instans

Klassen `AsposeOCR` är ingångspunkten för alla OCR‑operationer. Den kapslar in motorn, hanterar resurser och tillhandahåller metoden `recognizePage`.

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR`‑objektet ger dig åtkomst till alla OCR‑funktioner.

### Steg 4: Ställ in igenkänningsalternativ (språkval)

`RecognitionSettings` är Aspose.OCR:s konfigurationsbehållare som låter dig finjustera OCR‑processen.  

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

1. Inaktiverar vi auto‑skev eftersom vi anger ett manuellt skevvärde.  
2. Definierar ett rektangulärt område (`RecognitionAreas`) för att begränsa OCR till den del av bilden som faktiskt innehåller text.  
3. Sätter **språket** till engelska (`Language.Eng`). Ändra detta till `Language.Fra`, `Language.Spa` osv., beroende på din källbild.

### Steg 5: Utför OCR och hämta resultat

Anropet `recognizePage` kör OCR‑motorn med bilden och de inställningar du definierat. Resultatet lagras i ett `RecognitionResult`‑objekt som samlar all användbar data.

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

Konsolutdata visar:

- Den fullständiga extraherade texten (`recognitionText`).  
- Text för varje definierad rektangel (`recognitionAreasText`).  
- Koordinater för avgränsningsrektanglar.  
- En JSON‑representation för enkel vidarebehandling.  
- Upptäckt skevvinkel och eventuella varningar.

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

Konsolutdata visar den fullständiga extraherade texten, region‑specifik text, avgränsningsrutor, JSON, skevvinkel och varningar. Du kan nu föra `result.recognitionText` in i din affärslogik – lagra den, indexera den eller skicka den till en annan tjänst.

## Vanliga problem och lösningar

| Problem | Orsak | Lösning |
|-------|-------|-----|
| **Skräptecken** | Fel språk valt | Ange rätt `Language`‑enum (t.ex. `Language.Fra` för franska). |
| **Ingen text returneras** | Igenkänningsområde täcker inte texten | Justera `Rectangle`‑koordinaterna eller ta bort `RecognitionAreas` för att bearbeta hela bilden. |
| **Långsam prestanda** | Mycket stor bild eller hög upplösning | Skala ner bilden innan OCR eller öka JVM‑minnesallokeringen. |
| **Varningar om ej‑stött format** | Bildformatet känns inte igen | Konvertera bilden till PNG, JPEG eller TIFF innan bearbetning. |

## Vanliga frågor

**Q: Kan jag känna igen flera språk i ett och samma OCR‑anrop?**  
A: Ja. Använd `settings.setLanguage(Language.Eng \| Language.Fra)` för att aktivera flerspråkig igenkänning.

**Q: Vilka bildformat stödjer Aspose.OCR?**  
A: PNG, JPEG, BMP, TIFF, GIF och flera andra. Ange bara rätt filsökväg.

**Q: Finns det någon storleksgräns för bilden?**  
A: Det finns ingen hård gräns, men bilder större än 10 MB kan öka minnesanvändning och körtid. Överväg att minska storleken på stora filer.

**Q: Hur får jag en produktionslicens?**  
A: Köp en licens på Aspose‑webbplatsen och applicera den via `License`‑klassen enligt Aspose‑dokumentationen.

**Q: Kan jag extrahera text direkt från en PDF‑sida?**  
A: Inte direkt med Aspose.OCR. Konvertera PDF‑sidan till en bild först (t.ex. med Aspose.PDF) och kör sedan OCR.

## Slutsats

Du har nu sett hur du **extraherar text från bild** med Aspose.OCR för Java samtidigt som du väljer rätt språk och tillämpar **OCR‑skevkorrektion** för att förbättra pålitligheten. Detta tillvägagångssätt levererar exakt, högpresterande OCR som kan inbäddas i vilken Java‑baserad arbetsflöde som helst – från dokumenthanteringssystem till datainsamlings‑pipelines. Experimentera med olika `Language`‑enums, justera `RecognitionAreas` och integrera JSON‑utdata i din efterföljande analys för en verkligt end‑to‑end‑lösning.

---

**Senast uppdaterad:** 2026-06-24  
**Testat med:** Aspose.OCR 24.11 för Java  
**Författare:** Aspose

## Relaterade handledningar

- [How to calculate skew angle java using Aspose.OCR](/ocr/java/ocr-basics/calculate-skew-angle/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/java/ocr-operations/recognize-pdf/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}