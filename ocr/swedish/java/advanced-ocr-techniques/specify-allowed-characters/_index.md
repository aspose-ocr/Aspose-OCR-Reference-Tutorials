---
date: 2026-02-20
description: Lär dig hur du extraherar text från bilder med Aspose.OCR för Java, ställer
  in tillåtna tecken och tillämpar en tillfällig licens – en komplett Aspose OCR Java‑handledning.
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

## Introduktion

Att extrahera text från bilder är ett vanligt krav i moderna applikationer—oavsett om du bearbetar fakturor, skannar kvitton eller digitaliserar tryckta dokument. I den här handledningen går vi igenom en komplett **aspose ocr java tutorial** som visar hur du **extraherar text från bilder** med Aspose.OCR för Java, anger tillåtna tecken och använder en tillfällig licens när du bara testar biblioteket.

## Snabba svar
- **Vad gör Aspose.OCR?** Det extraherar text från bilder med hög noggrannhet och stöder anpassade teckenuppsättningar.  
- **Behöver jag en licens?** En tillfällig eller permanent licens krävs för produktionsanvändning.  
- **Vilken JDK-version stöds?** De senaste JDK-utgåvorna är fullt kompatibla.  
- **Kan jag begränsa erkända tecken?** Ja—använd `setAllowedCharacters`‑API:t för att begränsa utdata.  
- **Hur lång tid tar installationen?** Ungefär 10‑15 minuter för en grundläggande implementation.

## Vad betyder “extrahera text från bilder”?
Att extrahera text från bilder avser processen att omvandla visuell text (t.ex. tryckt eller handskriven) till maskinläsbara strängar. Detta möjliggör efterföljande uppgifter som sökning, indexering eller dataanalys.

## Varför använda Aspose.OCR för Java?
- **Hög noggrannhet** över flera språk och typsnitt.  
- **Enkelt API** som integreras med vilket Java‑projekt som helst.  
- **Anpassningsbart** teckenuppsättningar, språkpaket och bildförbehandling.  
- **Inga externa beroenden**—biblioteket är självständigt.

## Förutsättningar

Innan du börjar, se till att du har följande:

### Java Development Kit (JDK)

Säkerställ att du har den senaste Java Development Kit installerad på ditt system. Du kan ladda ner den [här](https://www.oracle.com/java/technologies/javase-downloads.html).

### Aspose.OCR for Java Library

Ladda ner och installera Aspose.OCR for Java‑biblioteket från [nedladdningslänken](https://releases.aspose.com/ocr/java/).

### Aspose.OCR License

För att få tillgång till hela potentialen i Aspose.OCR, skaffa en giltig licens. Du kan erhålla en från [här](https://purchase.aspose.com/buy) eller utforska en [tillfällig licens](https://purchase.aspose.com/temporary-license/) för en provperiod.

## Hur man använder tillfällig licens

När du utvärderar produkten tar en tillfällig licens bort utvärderingsvattenstämpeln och låser upp full funktionalitet under en begränsad period. Skapa licenssträngen i Aspose‑portalen och skicka den till `AsposeOCR`‑konstruktorn som visas i kodexemplet nedan. För produktionsdistributioner, ersätt den tillfälliga nyckeln med din permanenta licens.

## OCR‑förbehandlingstips för bilder

God bildkvalitet förbättrar igenkänningsresultaten avsevärt. Innan du anropar OCR‑motorn, överväg:

- Konvertera bilden till gråskala.  
- Öka kontrasten så att tecknen framträder tydligare.  
- Ta bort bakgrundsbrus med ett binariseringfilter.  
- Ändra storlek på lågupplösta bilder till minst 300 dpi.

Dessa steg är en del av **ocr image preprocessing** och kan utföras med vilket standard‑Java‑bildbibliotek som helst innan du anropar Aspose.OCR.

## Importera paket

När förutsättningarna är klara, importera de nödvändiga paketen till ditt Java‑projekt:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Steg‑för‑steg‑guide

### Steg 1: Ange din dokumentkatalog

Definiera en mapp där du kommer att lagra OCR‑behandlade resultat. Denna sökväg används senare för att hitta bildfilen.

```java
String dataDir = "Your Document Directory";
```

### Steg 2: Ange bildens sökväg

Peka API:t på den bild du vill analysera.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### Steg 3: Skapa en Aspose.OCR‑instans

Instansiera OCR‑motorn med din licensnyckel. Nyckeln kan vara en tillfällig eller permanent licenssträng.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### Steg 4: Utför OCR‑igenkänning

Anropa metoden `RecognizeLine` för att extrahera en rad text från bilden. Resultatet är en vanlig sträng som du kan vidarebearbeta eller lagra.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Pro tip:** Om du behöver begränsa utdata till en specifik teckenuppsättning (t.ex. endast siffror), använd `setAllowedCharacters`‑metoden på `AsposeOCR`‑instansen innan du anropar `RecognizeLine`. Detta säkerställer att motorn ignorerar alla tecken utanför den definierade mängden.

## Vanliga problem och lösningar

| Problem | Orsak | Lösning |
|-------|--------|-----|
| **Ingen utdata eller tom sträng** | Fel bildsökväg eller bildformat som inte stöds | Verifiera `imagePath` och använd ett stödd format (JPEG, PNG, BMP) |
| **Fel vid igenkänning** | Lågupplöst bild eller bullrigt bakgrund | Förbehandla bilden (öka kontrast, binarisera) innan OCR |
| **Licens ej tillämpad** | Saknad eller ogiltig licensnyckel | Säkerställ att licenssträngen är korrekt och placerad i `AsposeOCR`‑konstruktorn |

## Vanliga frågor

**Q: Hur kan jag skaffa en tillfällig licens för Aspose.OCR?**  
A: Besök [tillfällig licens‑sida](https://purchase.aspose.com/temporary-license/) för att begära en provlicens.

**Q: Var kan jag hitta support för Aspose.OCR?**  
A: Gå med i gemenskapen på [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16) för hjälp och diskussioner.

**Q: Kan jag ange tillåtna tecken i Aspose.OCR?**  
A: Ja, du kan anpassa teckenuppsättningen med `setAllowedCharacters`‑API:t. Se den officiella dokumentationen för detaljer.

**Q: Är Aspose.OCR kompatibel med de senaste JDK-versionerna?**  
A: Absolut—Aspose.OCR uppdateras regelbundet för att förbli kompatibel med de nyaste Java‑utgåvorna.

**Q: Finns det ytterligare OCR‑funktioner utöver radigenkänning?**  
A: Ja, biblioteket stödjer block‑, paragraf‑ och hel‑sidigenkänning, samt språkpaket och bildförbehandlingsalternativ.

## Slutsats

Genom att följa denna **aspose ocr java tutorial** har du nu en fungerande lösning för att **extrahera text från bilder** och kontrollera vilka tecken som känns igen. Utforska den fullständiga [dokumentationen](https://reference.aspose.com/ocr/java/) för att upptäcka avancerade funktioner som flerspråkigt stöd, anpassad förbehandling och batch‑bearbetning.

---

**Senast uppdaterad:** 2026-02-20  
**Testad med:** Aspose.OCR for Java 24.11  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}