---
date: 2025-12-06
description: Lär dig hur du använder Aspose.OCR för Java för att utföra OCR‑textigenkänning,
  extrahera text från bilder och förbereda rektanglar för riktad igenkänning.
language: sv
linktitle: Preparing Rectangles for OCR Text Recognition in Aspose.OCR
second_title: Aspose.OCR Java API
title: Förbereda rektanglar för OCR‑textigenkänning i Aspose.OCR
url: /java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Förbereda rektanglar för OCR‑textigenkänning i Aspose.OCR

## Introduction

I dagens datadrivna värld är **ocr text recognition** en hörnsten för att omvandla skannade dokument, skärmdumpar och foton till sökbart, redigerbart innehåll. Aspose.OCR för Java gör denna process snabb och pålitlig, särskilt när du behöver fokusera på specifika områden i en bild. I den här handledningen går vi igenom varje steg som krävs för att förbereda rektanglar som begränsar OCR till de regioner du bryr dig om, vilket ger dig exakt kontroll och bättre prestanda.

## Quick Answers
- **Vilket bibliotek hanterar OCR‑textigenkänning i Java?** Aspose.OCR for Java.  
- **Behöver jag en licens för produktionsbruk?** Ja – en giltig Aspose.OCR‑licens låser upp full funktionalitet.  
- **Kan jag begränsa OCR till vissa delar av en bild?** Absolut; du definierar rektanglar som avgränsar målzonerna.  
- **Vad är de viktigaste förutsättningarna?** JDK 17+, Aspose.OCR för Java och en Java‑IDE.  
- **Är detta tillvägagångssätt lämpligt för att extrahera text från bilder?** Ja, det är ett effektivt sätt att **extract text image java** projekt.

## What is OCR Text Recognition?
OCR (Optical Character Recognition) textigenkänning omvandlar pixelbaserade bilder till maskinläsbara tecken. Det gör det möjligt att söka, redigera och analysera innehåll som ursprungligen bara fanns som bilder.

## Why Prepare Rectangles for OCR Text Recognition?
Varför förbereda rektanglar för OCR‑textigenkänning?

* Minskar bearbetningstiden.
* Förbättrar noggrannheten genom att ignorera brusiga bakgrunder.
* Gör det möjligt att extrahera endast den data du behöver – perfekt för formulär, fakturor och kvitton.

## Prerequisites

Innan du börjar, se till att du har:

- **Java Development Kit (JDK)** – Aspose.OCR för Java fungerar med JDK 17 eller senare. Ladda ner det från Oracles webbplats.
- **Aspose.OCR för Java‑bibliotek** – Hämta den senaste JAR‑filen från den officiella nedladdningssidan [here](https://releases.aspose.com/ocr/java/). Följ installationsguiden [here](https://reference.aspose.com/ocr/java/).
- **Utvecklingsmiljö** – Vilken Java‑IDE som helst (IntelliJ IDEA, Eclipse, VS Code, etc.) fungerar.

## Import Packages

I din Java‑källfil importerar du de nödvändiga Aspose.OCR‑klasserna och standard‑Java‑verktygen:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

*Vi importerar `java.awt.Rectangle` eftersom OCR‑API:t förväntar sig rektanglar som definierar de områden som ska skannas.*

## Step 1: Set Up License

```java
SetLicense.main(null);
```

Genom att anropa `SetLicense` aktiveras din Aspose.OCR‑licens, vilket tar bort utvärderingsbegränsningar och möjliggör full‑funktionell OCR‑textigenkänning.

## Step 2: Define Document Directory and Image Path

```java
String dataDir = "Your Document Directory";
String imagePath = dataDir + "p.png";
```

Byt ut `"Your Document Directory"` mot den absoluta sökvägen där din bild (`p.png`) finns. Detta är bilden som kommer att bearbetas.

## Step 3: Create Aspose.OCR Instance

```java
AsposeOCR api = new AsposeOCR();
```

Genom att instansiera `AsposeOCR` får du tillgång till metoden `RecognizePage`, som utför den faktiska OCR‑processen.

## Step 4: Prepare Rectangles with Texts

```java
ArrayList<Rectangle> rectArray = new ArrayList<Rectangle>();
rectArray.add(new Rectangle(138, 352, 2033, 537));
rectArray.add(new Rectangle(147, 890, 2033, 1157));
rectArray.add(new Rectangle(923, 2045, 465, 102));
rectArray.add(new Rectangle(104, 2147, 2076, 819));
```

Varje `Rectangle(x, y, width, height)` talar om för AsposeOCR exakt var den ska leta efter text. Justera koordinaterna så att de matchar layouten på din källbild.

## Step 5: Perform OCR Recognition

```java
try {
    String result = api.RecognizePage(imagePath, rectArray);
    System.out.println("Result with rect: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

`RecognizePage`‑anropet bearbetar endast de definierade rektanglarna och returnerar den extraherade strängen. Konsolutdata låter dig omedelbart verifiera resultatet av **ocr text recognition**.

## Common Issues and Tips

| Problem | Orsak | Lösning |
|-------|-------|----------|
| **Ingen utdata** | Felaktiga rektangelkoordinater eller bildsökväg | Dubbelkolla värdet på `dataDir` och säkerställ att rektanglarna faktiskt täcker textområden. |
| **Skräptecken** | Lågupplöst bild eller teckensnitt som inte stöds | Använd en bild med högre upplösning eller tillämpa bildförbehandling (t.ex. binarisering). |
| **Licens ej tillämpad** | `SetLicense` anropades inte före OCR | Säkerställ att `SetLicense.main(null);` körs före några API‑anrop. |
| **Prestandafördröjning** | För många stora rektanglar | Begränsa antalet rektanglar och håll dem så tätt som möjligt kring texten. |

## Conclusion

Du har nu lärt dig hur du integrerar Aspose.OCR för Java, ställer in en licens, definierar bildsökvägar och – viktigast av allt – förbereder rektanglar för att fokusera **ocr text recognition** på specifika delar av en bild. Denna teknik är idealisk för alla **java ocr tutorial** som kräver exakt, högpresterande textutvinning.

## Frequently Asked Questions

**Q: Är Aspose.OCR kompatibel med andra programmeringsspråk?**  
A: Ja, Aspose.OCR stödjer även .NET, C++ och Python. Se den officiella dokumentationen för språk‑specifika exempel.

**Q: Kan jag använda Aspose.OCR i ett kommersiellt projekt?**  
A: Absolut. Köp en kommersiell licens via [Aspose store](https://purchase.aspose.com/buy).

**Q: Finns det en gratis provversion?**  
A: Ja, du kan ladda ner en provversion [here](https://releases.aspose.com/).

**Q: Hur får jag en tillfällig licens för utvärdering?**  
A: Tillfälliga licenser tillhandahålls via [Aspose temporary‑license portal](https://purchase.aspose.com/temporary-license/).

**Q: Var kan jag få community‑support?**  
A: Besök Aspose.OCR‑[forum](https://forum.aspose.com/c/ocr/16) för frågor, tips och kodexempel.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-06  
**Tested With:** Aspose.OCR for Java 24.12  
**Author:** Aspose  

---