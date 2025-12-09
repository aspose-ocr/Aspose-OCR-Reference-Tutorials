---
date: 2025-12-09
description: Lär dig hur du extraherar text från bilder med Aspose.OCR för Java och
  anger tillåtna tecken – en komplett Aspose OCR Java‑handledning.
linktitle: Specifying Allowed Characters in Aspose.OCR
second_title: Aspose.OCR Java API
title: Extrahera text från bilder med Aspose.OCR – Tillåtna tecken
url: /sv/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bilder med Aspose.OCR – Tillåtna tecken

## Introduction

Att extrahera text från bilder är ett vanligt krav i moderna applikationer—oavsett om du bearbetar fakturor, skannar kvitton eller digitaliserar tryckta dokument. **Aspose.OCR for Java** gör denna uppgift enkel och erbjuder hög noggrannhet i igenkänning samt flexibla konfigurationsalternativ, såsom att ange tillåtna tecken. I den här handledningen går vi igenom en komplett **aspose ocr java tutorial** som visar hur du installerar biblioteket, kör OCR och begränsar teckenuppsättningen efter dina behov.

## Quick Answers
- **Vad gör Aspose.OCR?** Det extraherar text från bilder med hög noggrannhet och stöder anpassade teckenuppsättningar.  
- **Behöver jag en licens?** En tillfällig eller permanent licens krävs för produktionsanvändning.  
- **Vilken JDK-version stöds?** De senaste JDK-utgåvorna är fullt kompatibla.  
- **Kan jag begränsa igenkända tecken?** Ja—använd API:t för tillåtna tecken för att begränsa resultatet.  
- **Hur lång tid tar installationen?** Ungefär 10‑15 minuter för en grundläggande implementation.

## What is “extract text from images”?

Att extrahera text från bilder avser processen att konvertera visuell text (t.ex. tryckt eller handskriven) till maskinläsbara strängar. Detta möjliggör efterföljande uppgifter som sökning, indexering eller dataanalys.

## Why Use Aspose.OCR for Java?
- **Hög noggrannhet** över flera språk och typsnitt.  
- **Enkelt API** som integreras med vilket Java‑projekt som helst.  
- **Anpassningsbart** teckenuppsättningar, språkpaket och bildförbehandling.  
- **Inga externa beroenden**—biblioteket är fristående.

## Prerequisites

### Java Development Kit (JDK)

Se till att du har den senaste Java Development Kit installerad på ditt system. Du kan ladda ner den från [here](https://www.oracle.com/java/technologies/javase-downloads.html).

### Aspose.OCR for Java Library

Ladda ner och installera Aspose.OCR for Java‑biblioteket från [download link](https://releases.aspose.com/ocr/java/).

### Aspose.OCR License

För att utnyttja hela potentialen i Aspose.OCR, skaffa en giltig licens. Du kan få en från [here](https://purchase.aspose.com/buy) eller utforska en [temporary license](https://purchase.aspose.com/temporary-license/) för en provperiod.

## Import Packages

När förutsättningarna är klara, importera de nödvändiga paketen i ditt Java‑projekt:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Step‑by‑Step Guide

### Step 1: Set Your Document Directory

Definiera en mapp där du kommer att lagra OCR‑bearbetade resultat. Denna sökväg används senare för att hitta bildfilen.

```java
String dataDir = "Your Document Directory";
```

### Step 2: Specify the Image Path

Peka API:t på den bild du vill analysera.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### Step 3: Create an Aspose.OCR Instance

Instansiera OCR‑motorn med din licensnyckel. Nyckeln kan vara en tillfällig eller permanent licenssträng.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### Step 4: Perform OCR Recognition

Anropa metoden `RecognizeLine` för att extrahera en rad text från bilden. Resultatet är en vanlig sträng som du kan bearbeta vidare eller lagra.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Pro tip:** Om du behöver begränsa resultatet till en specifik teckenuppsättning (t.ex. endast siffror), använd metoden `setAllowedCharacters` på `AsposeOCR`‑instansen innan du anropar `RecognizeLine`. Detta säkerställer att motorn ignorerar alla tecken utanför den definierade uppsättningen.

## Common Issues and Solutions

| Issue | Reason | Fix |
|-------|--------|-----|
| **Ingen utdata eller tom sträng** | Felaktig bildsökväg eller bildformat som inte stöds | Verifiera `imagePath` och använd ett stödd format (JPEG, PNG, BMP) |
| **Fel vid igenkänning** | Lågupplöst bild eller bullrigt bakgrund | Förbehandla bilden (öka kontrast, binarisera) innan OCR |
| **Licens inte tillämpad** | Saknad eller ogiltig licensnyckel | Säkerställ att licenssträngen är korrekt och placerad i `AsposeOCR`‑konstruktorn |

## Frequently Asked Questions

**Q: Hur kan jag skaffa en tillfällig licens för Aspose.OCR?**  
A: Besök [temporary license page](https://purchase.aspose.com/temporary-license/) för att begära en provlicens.

**Q: Var kan jag hitta support för Aspose.OCR?**  
A: Gå med i gemenskapen på [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16) för hjälp och diskussioner.

**Q: Kan jag ange tillåtna tecken i Aspose.OCR?**  
A: Ja, du kan anpassa teckenuppsättningen med `setAllowedCharacters`‑API:t. Se den officiella dokumentationen för detaljer.

**Q: Är Aspose.OCR kompatibel med de senaste JDK-versionerna?**  
A: Absolut—Aspose.OCR uppdateras regelbundet för att vara kompatibel med de senaste Java‑utgåvorna.

**Q: Finns det ytterligare OCR‑funktioner utöver radigenkänning?**  
A: Ja, biblioteket stöder block-, stycke- och helsidigenkänning, samt språkpaket och alternativ för bildförbehandling.

## Conclusion

Genom att följa denna **aspose ocr java tutorial** har du nu en fungerande lösning för att **extrahera text från bilder** och styra vilka tecken som känns igen. Utforska den fullständiga [documentation](https://reference.aspose.com/ocr/java/) för att upptäcka avancerade funktioner som flerspråksstöd, anpassad förbehandling och batch‑bearbetning.

---

**Last Updated:** 2025-12-09  
**Tested With:** Aspose.OCR for Java 24.11  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}