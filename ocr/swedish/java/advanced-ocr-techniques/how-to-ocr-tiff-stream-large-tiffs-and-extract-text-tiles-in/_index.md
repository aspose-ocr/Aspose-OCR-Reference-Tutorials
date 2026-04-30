---
category: general
date: 2026-04-29
description: Lär dig hur du OCR:ar TIFF-filer med Aspose OCR streaming‑läge. Denna
  guide visar hur du effektivt extraherar textbrickor från kaklade TIFF‑bilder.
draft: false
keywords:
- how to ocr tiff
- extract text tiles
language: sv
og_description: hur man OCR:ar TIFF med Aspose OCR streaming. Steg‑för‑steg‑kod för
  att extrahera textbrickor från stora TIFF‑bilder.
og_title: hur man OCR:ar TIFF – Komplett streamingguide
tags:
- OCR
- Java
- Aspose
- TIFF
title: hur man OCR:ar TIFF – strömma stora TIFF-filer och extrahera textbrickor i
  Java
url: /sv/java/advanced-ocr-techniques/how-to-ocr-tiff-stream-large-tiffs-and-extract-text-tiles-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hur man ocr tiff – strömma stora TIFF-filer och extrahera textbrickor i Java

Har du någonsin undrat **hur man ocr tiff** filer som är för stora för att laddas in i minnet på en gång? Du är inte ensam. Många utvecklare stöter på problem när deras TIFF-bilder är delade i dussintals brickor, och det vanliga anropet `ocrEngine.recognize()` bara hänger.  

Den goda nyheten? Aspose OCR:s strömningsläge låter dig mata varje bricka som en separat ström, så att du kan **extrahera textbrickor** utan att fylla upp heapen. I den här handledningen går vi igenom ett komplett, färdigt att köra Java‑exempel, förklarar varför varje rad är viktig, och pekar på fallgropar du bör undvika.

> **Vad du får:** ett körbart program som sy ihop delade TIFF-filer i farten, skriver ut den kombinerade texten, och visar hur du anpassar koden för andra språk eller bildformat.

---

## Förutsättningar

- **Java 17** eller nyare (koden använder try‑with‑resources, så JDK 8+ fungerar, men JDK 17 är den nuvarande LTS).
- **Aspose.OCR for Java**-biblioteket (v23.10 eller senare). Lägg till det via Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- En mapp som innehåller de enskilda TIFF‑brickorna (t.ex. `tile_0.tif`, `tile_1.tif`, …).  
- Valfritt: en IDE som IntelliJ IDEA eller VS Code – men en enkel textredigerare fungerar bra.

## Steg 1 – Förbered sökvägarna till brickorna (Varför det är viktigt)

Innan OCR‑motorn kan göra någonting måste den veta var varje bilddel finns. Att hårdkoda sökvägarna är okej för en demo, men i produktion skulle du troligen skanna en katalog eller läsa en manifestfil.

```java
// Define the absolute or relative paths to each TIFF tile
String[] tilePaths = {
    "YOUR_DIRECTORY/tile_0.tif",
    "YOUR_DIRECTORY/tile_1.tif",
    "YOUR_DIRECTORY/tile_2.tif"
};
```

> **Proffstips:** håll brickorna i lexikografisk ordning (0, 1, 2…) eftersom motorn kommer att sammanfoga den igenkända texten i samma sekvens som du matar strömmarna.

## Steg 2 – Aktivera strömningsläge på OCR‑motorn (Primärt nyckelord)

Nu skapar vi en `OcrEngine`‑instans och slår på strömning. Detta är kärnan i **hur man ocr tiff** utan att ladda hela bilden i RAM.

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Activate streaming – essential for large or tiled TIFFs
ocrEngine.getProcessingSettings().setEnableStreaming(true);

// Set the language to English; change as needed (e.g., "fr", "de")
ocrEngine.getLanguageSettings().setLanguage("en");
```

**Varför strömning?**  
När `setEnableStreaming(true)` anropas behandlar motorn varje inkommande `ImageStream` som en fortsättning på den föregående. Den bygger en intern virtuell canvas, syr ihop brickorna virtuellt och kör OCR en gång i slutet. Detta undviker “OutOfMemoryError” som skulle uppstå om du försökte ladda en multi‑gigabyte TIFF på en gång.

## Steg 3 – Lägg till varje bricka som en inmatningsström (Sekundärt nyckelord)

Här är loopen som matar varje bricka till motorn. `try‑with‑resources`‑blocket garanterar att filhandtaget stängs omedelbart, vilket är avgörande när du hanterar dussintals filer.

```java
for (String tilePath : tilePaths) {
    try (InputStream stream = new FileInputStream(tilePath)) {
        // Wrap the raw InputStream in Aspose's ImageStream wrapper
        ocrEngine.appendImage(ImageStream.fromStream(stream));
    } catch (IOException e) {
        // If a single tile fails, we log and continue – you might want to abort instead
        System.err.println("Failed to load tile: " + tilePath);
        e.printStackTrace();
    }
}
```

Observera att frasen **extrahera textbrickor** är naturligt inbäddad: varje iteration *extraherar* texten från en bricka och lägger till den i den växande resultatuppsättningen.

## Steg 4 – Kör igenkänning och skriv ut den kombinerade texten (Primärt nyckelord)

Efter att alla brickor har köats, utför ett enda anrop OCR på den virtuella bilden. Resultatet innehåller hela texten, precis som om du hade en enda massiv TIFF.

```java
// Perform OCR on the combined virtual image
OcrResult ocrResult = ocrEngine.recognize();

// Print the extracted text to the console
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Förväntad utskrift** (förutsatt att brickorna innehåller frasen “Hello World” uppdelad över dem):

```
=== OCR Output ===
Hello World
```

Om dina brickor innehåller fler rader kommer de att visas i samma ordning som du levererade dem. Du kan också skriva `ocrResult.getText()` till en fil för vidare bearbetning.

## Steg 5 – Fullt, körbart exempel (Alla steg på ett ställe)

Nedan är det kompletta programmet som du kan kopiera‑och‑klistra in i `StreamingExample.java`. Det inkluderar alla imports, kommentarer och felhantering.

```java
import com.aspose.ocr.*;
import java.io.*;

public class StreamingExample {
    public static void main(String[] args) throws Exception {
        // ------------------------------------------------------------
        // Step 1: List the TIFF tile files
        // ------------------------------------------------------------
        String[] tilePaths = {
            "YOUR_DIRECTORY/tile_0.tif",
            "YOUR_DIRECTORY/tile_1.tif",
            "YOUR_DIRECTORY/tile_2.tif"
        };

        // ------------------------------------------------------------
        // Step 2: Set up the OCR engine in streaming mode
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getProcessingSettings().setEnableStreaming(true);
        ocrEngine.getLanguageSettings().setLanguage("en");

        // ------------------------------------------------------------
        // Step 3: Feed each tile as a separate stream
        // ------------------------------------------------------------
        for (String tilePath : tilePaths) {
            try (InputStream stream = new FileInputStream(tilePath)) {
                ocrEngine.appendImage(ImageStream.fromStream(stream));
            } catch (IOException e) {
                System.err.println("Unable to read tile: " + tilePath);
                e.printStackTrace();
                // Optionally: return; // abort on missing tile
            }
        }

        // ------------------------------------------------------------
        // Step 4: Recognize the combined image and display the text
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Spara, kompilera och kör:

```bash
javac -cp "path/to/aspose-ocr.jar" StreamingExample.java
java -cp ".:path/to/aspose-ocr.jar" StreamingExample
```

Du bör se den sammanslagna OCR‑texten skriven till konsolen.

## Avancerade tips & vanliga fallgropar (Varför detta fungerar)

| Issue | Why It Happens | How to Fix / Optimize |
|-------|----------------|-----------------------|
| **Out‑of‑memory‑fel** | Att ladda en full‑stor TIFF i en `BufferedImage` förbrukar hela heapen. | Använd strömningsläge (`setEnableStreaming(true)`) – motorn materialiserar aldrig hela bilden. |
| **Felaktig brickordning** | Filer sorterade alfabetiskt istället för numerisk ordning (t.ex. `tile_10.tif` före `tile_2.tif`). | Nollutfyll nummer (`tile_00.tif`, `tile_01.tif`) eller sortera programatiskt med `Comparator`. |
| **Fel språk** | OCR standardinställning är engelska; icke‑engelsk text blir förvrängd. | Anropa `ocrEngine.getLanguageSettings().setLanguage("fr")` (eller någon annan stödjande ISO‑kod). |
| **Delvisa fel** | En korrupt bricka stoppar hela processen. | Fånga `IOException` per bricka, logga och bestäm om du ska fortsätta eller avbryta. |
| **Prestandaflaskhals** | Disk‑I/O dominerar när många små filer läses. | Packa brickorna i en ZIP och strömma från minnet, eller använd en snabb SSD. |

## När du ska använda strömning vs. OCR på en enskild bild

- **Streaming** är idealiskt för:
  - Fler‑sidiga TIFF‑filer eller gigapixel‑skanningar.
  - Situationer där minnet är begränsat (t.ex. Docker‑behållare, mobila enheter).
  - Pipelines som redan tar emot bilddelar (t.ex. kameraflöden).

- **Single‑image OCR** fungerar bra för:
  - Små PNG/JPEG‑filer (< 5 MB).
  - Enstaka skanningar där enkelhet väger tyngre än prestanda.

## Slutsats

Du har nu en solid förståelse för **hur man ocr tiff** filer med Aspose OCR:s strömningsfunktioner, och du vet hur du **extraherar textbrickor** effektivt. Den kompletta lösningen – initiering av motorn, aktivering av strömning, tillägg av varje bricka och slutligen igenkänning av den virtuella canvasen – täcker “vad”, “varför” och “hur” du behöver för produktionsklar kod.

Nästa steg? Prova att byta `"en"` mot ett annat språk, eller experimentera med olika bildformat (`.png`, `.jpg`). Du kan också mata OCR‑resultatet direkt in i ett sökindex eller en PDF‑generator. Mönstret förblir detsamma: strömma, sy ihop, känna igen.

Har du frågor om att skala till hundratals brickor, eller behöver du hjälp med felhantering? Lämna en kommentar nedan, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}