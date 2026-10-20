---
date: 2026-05-24
description: Upptäck hur du använder OCR med Aspose.OCR för Java, extrahera text från
  bilder, ange tillåtna tecken och tillämpa en tillfällig licens på några minuter.
keywords:
- how to use OCR
- extract text from images
- how to apply license
- how to set characters
linktitle: Specificera tillåtna tecken i Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-05-24'
  description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  headline: How to Use OCR – Extract Text from Images with Aspose.OCR
  type: TechArticle
- description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  name: How to Use OCR – Extract Text from Images with Aspose.OCR
  steps:
  - name: Set Your Document Directory
    text: Choose a folder where OCR results and temporary files will be stored. This
      path is later used to locate the image you want to process.
  - name: Specify the Image Path
    text: Provide the full file system path or a class‑path resource location that
      points to the image you wish to analyse.
  - name: Create an Aspose.OCR Instance
    text: '`AsposeOCR` is the core engine that performs optical character recognition.
      Instantiate it with either a temporary or permanent license string.'
  - name: Perform OCR Recognition
    text: '`RecognizeLine` extracts a single line of text from the supplied image
      and returns it as a plain Java `String`. You can call this method repeatedly
      for multi‑line documents. > **Pro tip:** If you need to restrict the output
      to digits only (e.g., for invoice numbers), call `setAllowedCharacters("0123'
  type: HowTo
- questions:
  - answer: Visit the [temporary license page](https://purchase.aspose.com/temporary-license/)
      to request a trial key that removes evaluation watermarks.
    question: How can I obtain a temporary license for Aspose.OCR?
  - answer: Join the community at the [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16)
      for help and discussions.
    question: Where can I find support for Aspose.OCR?
  - answer: Yes, use the `setAllowedCharacters` API to define a custom whitelist of
      characters. This is ideal for numeric‑only fields.
    question: Can I specify allowed characters in Aspose.OCR?
  - answer: Absolutely—Aspose.OCR is regularly updated to stay compatible with the
      newest Java releases.
    question: Is Aspose.OCR compatible with the latest JDK versions?
  - answer: The library also supports block, paragraph, and full‑page recognition,
      language packs, and advanced image preprocessing.
    question: Are there additional OCR features beyond line recognition?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Hur man använder OCR – Extrahera text från bilder med Aspose.OCR
url: /sv/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder OCR – Extrahera text från bilder med Aspose.OCR

I moderna Java‑applikationer är **how to use OCR** en vanlig fråga, särskilt när du behöver omvandla skannade fakturor, kvitton eller utskrivna formulär till sökbar text. Denna handledning guidar dig genom ett komplett **Aspose.OCR for Java**‑exempel: extrahera text från bilder, begränsa resultatet till en anpassad teckenuppsättning och tillämpa en temporär licens för snabb utvärdering.

## Snabba svar
- **What does Aspose.OCR do?** Den extraherar text från bilder med hög noggrannhet och låter dig begränsa erkända tecken.  
- **Do I need a license?** En temporär eller permanent licens krävs för produktionsanvändning; den temporära nyckeln tar bort vattenstämplar.  
- **Which JDK version is supported?** Biblioteket fungerar med de senaste JDK‑utgåvorna (JDK 17, 19, 21).  
- **Can I limit recognized characters?** Ja—använd metoden `setAllowedCharacters` för att begränsa resultatet.  
- **How long does the setup take?** Ungefär 10‑15 minuter för en grundläggande end‑to‑end‑implementation.

## Vad är “extrahera text från bilder”?
Att extrahera text från bilder, även känt som optisk teckenigenkänning (OCR), omvandlar visuella tecken—oavsett om de är tryckta, handskrivna eller maskinskrivna—till maskinläsbara strängar. Denna transformation gör det möjligt för applikationer att söka, indexera, redigera och analysera innehållet programmässigt, vilket stödjer arbetsflöden såsom fakturabehandling, dokumentarkivering och automatisering av datainmatning.

## Varför använda Aspose.OCR för Java?
Aspose.OCR stödjer **60+ språk**, kan bearbeta bilder upp till **10 MB** utan att ladda hela filen i minnet, och levererar **>95 % noggrannhet** på rena skanningar. Biblioteket är självständigt och kräver inga externa OCR‑motorer, vilket förenklar distribution och minskar licenskostnader.

## Förutsättningar

### Java Development Kit (JDK)

Se till att du har den senaste Java Development Kit installerad. Du kan ladda ner den från [here](https://www.oracle.com/java/technologies/javase-downloads.html).

### Aspose.OCR for Java Library

Ladda ner och installera Aspose.OCR for Java‑biblioteket från [download link](https://releases.aspose.com/ocr/java/).

### Aspose.OCR License

För att låsa upp full funktionalitet, skaffa en licens. Du kan köpa en från [here](https://purchase.aspose.com/buy) eller begära en [temporary license](https://purchase.aspose.com/temporary-license/) för provändamål.

## Hur man använder OCR med Aspose.OCR för Java?

Läs in din bild, konfigurera OCR‑motorn och anropa igenkänningsmetoden—allt i några enkla rader. Detta direkt‑svars‑avsnitt berättar exakt vad du ska göra: skapa en `AsposeOCR`‑instans med din licenssträng, ange eventuella tillåtna tecken och anropa `RecognizeLine` på målbilden för att få den extraherade texten. API‑et hanterar bildförbehandling internt, så du får rena resultat utan extra kod.

### Importera paket

`AsposeOCR`‑klassen finns i paketet `com.aspose.ocr`. Importera de nödvändiga klasserna innan du börjar koda.

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Steg‑för‑steg‑guide

### Steg 1: Ange din dokumentkatalog

Välj en mapp där OCR‑resultat och temporära filer ska lagras. Denna sökväg används senare för att hitta bilden du vill bearbeta.

```java
String dataDir = "Your Document Directory";
```

### Steg 2: Ange bildens sökväg

Ange den fullständiga filsystemssökvägen eller en class‑path‑resursplats som pekar på bilden du vill analysera.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### Steg 3: Skapa en Aspose.OCR‑instans

`AsposeOCR` är kärnmotorn som utför optisk teckenigenkänning. Skapa en instans med antingen en temporär eller permanent licenssträng.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### Steg 4: Utför OCR‑igenkänning

`RecognizeLine` extraherar en enskild textrad från den angivna bilden och returnerar den som en vanlig Java `String`. Du kan anropa denna metod upprepade gånger för flerradiga dokument.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Pro tip:** Om du behöver begränsa resultatet till enbart siffror (t.ex. för fakturanummer), anropa `setAllowedCharacters("0123456789")` på `AsposeOCR`‑instansen innan du anropar `RecognizeLine`. Detta tvingar motorn att ignorera icke‑numeriska symboler.  
> `setAllowedCharacters` är en metod i `AsposeOCR` som begränsar OCR‑utdata till en specificerad vitlista av tecken.

## Vanliga problem och lösningar

| Problem | Orsak | Lösning |
|-------|--------|-----|
| **No output or empty string** | Felaktig bildsökväg eller format som inte stöds | Verifiera `imagePath` och använd ett stödformat (JPEG, PNG, BMP) |
| **Recognition errors** | Lågupplöst bild eller bullrigt bakgrund | Förbehandla bilden (öka kontrast, binarisera) före OCR |
| **License not applied** | Saknad eller ogiltig licensnyckel | Säkerställ att licenssträngen är korrekt och skickas till `AsposeOCR`‑konstruktorn |

## Vanliga frågor

**Q: Hur kan jag skaffa en temporär licens för Aspose.OCR?**  
A: Besök [temporary license page](https://purchase.aspose.com/temporary-license/) för att begära en provnyckel som tar bort utvärderingsvattenstämplar.

**Q: Var kan jag hitta support för Aspose.OCR?**  
A: Gå med i gemenskapen på [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16) för hjälp och diskussioner.

**Q: Kan jag ange tillåtna tecken i Aspose.OCR?**  
A: Ja, använd `setAllowedCharacters`‑API:t för att definiera en anpassad vitlista av tecken. Detta är idealiskt för fält som bara ska innehålla siffror.

**Q: Är Aspose.OCR kompatibel med de senaste JDK‑versionerna?**  
A: Absolut—Aspose.OCR uppdateras regelbundet för att vara kompatibel med de senaste Java‑utgåvorna.

**Q: Finns det ytterligare OCR‑funktioner utöver radigenkänning?**  
A: Biblioteket stödjer även block-, paragraf- och helsidigenkänning, språkpaket och avancerad bildförbehandling.

## Slutsats

Genom att följa denna **Aspose OCR Java‑handledning** vet du nu **how to use OCR** för att extrahera text från bilder, begränsa teckenuppsättningen och tillämpa en temporär licens för snabb testning. Fördjupa dig i den fullständiga [documentation](https://reference.aspose.com/ocr/java/) för att utforska flerspråksstöd, batch‑behandling och anpassade förbehandlings‑pipelines.

---

**Last Updated:** 2026-05-24  
**Tested With:** Aspose.OCR for Java 24.11  
**Author:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Relaterade handledningar

- [Hur man ställer in licens och verifierar Aspose.OCR‑licens i Java](/ocr/java/ocr-basics/set-license/)
- [Konvertera bild till text i Java med Aspose.OCR BufferedImage](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Aspose OCR Java‑exempel – känna igen rader i bilder](/ocr/java/advanced-ocr-techniques/recognize-lines/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}