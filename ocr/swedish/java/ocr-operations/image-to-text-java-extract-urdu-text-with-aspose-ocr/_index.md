---
category: general
date: 2026-02-17
description: 'bild till text java-handledning: lär dig hur du extraherar urdutext
  från en bild med Aspose OCR. Komplett java OCR‑exempel inkluderat.'
draft: false
keywords:
- image to text java
- how to extract text
- extract urdu text
- java ocr example
- load image ocr
language: sv
og_description: image to text java tutorial visar hur man extraherar urdutext från
  en bild med Aspose OCR. Följ det kompletta java OCR‑exemplet steg för steg.
og_title: 'Bild till text Java: Extrahera urdustext med Aspose OCR'
tags:
- OCR
- Java
- Aspose
title: 'Bild till text Java: Extrahera Urdu‑text med Aspose OCR'
url: /sv/java/ocr-operations/image-to-text-java-extract-urdu-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# image to text java: Extrahera Urdu-text med Aspose OCR

Om du behöver göra **image to text java**-konvertering för Urdu-dokument, är du på rätt plats. Har du någonsin undrat *hur man extraherar text* från en bild av en handskriven anteckning eller en skannad tidningssida? Den här guiden går igenom ett **java ocr example** som hämtar Urdu-tecken direkt från en bild med hjälp av Aspose OCR.

Vi kommer att gå igenom allt från licensiering av biblioteket till att skriva ut resultatet i konsolen. I slutet kommer du att kunna **load image ocr**-filer, ställa in språket till Urdu och få ren Unicode-utdata—utan extra verktyg.  

## Vad du behöver

- **Java Development Kit (JDK) 8+** – koden fungerar på alla moderna JDK.
- **Aspose.OCR for Java** JAR (ladda ner från Aspose webbplats).  
- En giltig **Aspose OCR license**-fil (`Aspose.OCR.lic`).  
- En bild som innehåller Urdu-text, t.ex. `urdu-sample.png`.  

Att ha dessa grundläggande komponenter på plats betyder att du kan hoppa rakt in i koden utan att leta efter saknade beroenden.

## image to text java – Konfigurera Aspose OCR

Först måste vi meddela Aspose att vi har en licens. Utan den körs biblioteket i utvärderingsläge och lägger till vattenstämplar i resultatet.

```java
import com.aspose.ocr.*;

public class UrduDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**Varför detta är viktigt:** Licensiering tar bort 5‑sekunders begränsningen och låser upp hela Urdu-språkpaketet som lades till under 2025‑Q3. Om du hoppar över detta steg fungerar OCR-motorn fortfarande, men du kommer att se en liten “Evaluation”-etikett i resultaten.

## Så extraherar du text – Initiera OCR-motorn

Nu skapar vi motorn och talar explicit om att vi är intresserade av Urdu. Konstanten `OcrLanguage.URDU` aktiverar rätt teckenuppsättning och segmenteringsregler.

```java
        // Step 2: Create the OCR engine and set the language to Urdu
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU); // added in 2025‑Q3
```

**Proffstips:** Om du någonsin behöver bearbeta flera språk i ett körning kan du skicka en kommaseparerad lista, t.ex. `OcrLanguage.ENGLISH, OcrLanguage.URDU`. Motorn kommer automatiskt att upptäcka varje region.

## Ladda bild OCR – Förbereda indata

Aspose arbetar med ett `OcrInput`-objekt som kan hålla en eller flera bilder. Här **load image ocr**-data från en lokal fil.

```java
        // Step 3: Load the image that contains Urdu text
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/urdu-sample.png");
```

> **Obs:** Ersätt `YOUR_DIRECTORY` med den absoluta sökvägen eller en relativ sökväg från ditt projekts rot. Om filen inte hittas kastar Aspose ett `FileNotFoundException`. En snabb kontroll med `new File(path).exists()` kan spara dig mycket felsökningstid.

## Känn igen texten – Köra OCR-processen

När motorn är konfigurerad och bilden laddad, anropar vi slutligen `recognize`. Metoden returnerar ett `OcrResult` som innehåller den extraherade strängen.

```java
        // Step 4: Recognize the text from the image
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Vad händer under huven?** OCR-motorn delar upp bilden i rader, sedan tecken, och tillämpar Urdu‑specifika formningsregler (som sammanslagna former). Detta är varför det är avgörande att ställa in språket tidigt; annars får du förvrängda latinska platshållare.

## Skriv ut den igenkända Urdu-texten

Det sista steget är helt enkelt att skriva ut resultatet. Eftersom Urdu använder en höger‑till‑vänster-skrift, se till att din konsol stödjer Unicode (de flesta moderna terminaler gör det).

```java
        // Step 5: Print the recognized Urdu text
        System.out.println("Urdu text:\n" + ocrResult.getText());
    }
}
```

**Förväntat resultat (exempel):**

```
Urdu text:
یہ ایک مثال کا متن ہے جو تصویر سے نکالا گیا ہے۔
```

Om du ser frågetecken eller tomma strängar, dubbelkolla att din konsolkodning är satt till UTF‑8 (`chcp 65001` på Windows, eller kör Java med `-Dfile.encoding=UTF-8`).

## Fullt fungerande exempel – Alla steg på ett ställe

Nedan är det kompletta, kopiera‑och‑klistra‑klara programmet. Inga externa referenser, bara en enda Java-fil.

```java
import com.aspose.ocr.*;

public class UrduDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Create the OCR engine and set the language to Urdu
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU); // added in 2025‑Q3

        // Load the image that contains Urdu text
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/urdu-sample.png");

        // Recognize the text from the image
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Print the recognized Urdu text
        System.out.println("Urdu text:\n" + ocrResult.getText());
    }
}
```

Kör det med:

```bash
javac -cp "aspose-ocr-23.10.jar" UrduDemo.java
java -cp ".:aspose-ocr-23.10.jar" UrduDemo
```

Ersätt JAR-versionen (`23.10`) med den du laddade ner. Konsolen bör visa den Urdu-sats som extraherats från din PNG.

## Vanliga fallgropar & kantfall

| Problem | Varför det händer | Hur man åtgärdar |
|-------|----------------|------------|
| **Tomt resultat** | Bilden är för mörk eller låg upplösning. | Förprocessa bilden (öka kontrast, binarisera) med `BufferedImage` innan du skickar den till Aspose. |
| **Skräptecken** | Fel språk inställt (standard är engelska). | Se till att `ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU);` anropas innan `recognize`. |
| **Licens saknas** | Felaktig sökväg eller fil saknas. | Använd en absolut sökväg eller placera `.lic`-filen i classpath och anropa `license.setLicense("Aspose.OCR.lic");`. |
| **Out‑of‑memory på stora bilder** | Stora PNG-filer förbrukar heapen. | Anropa `ocrEngine.setMaxImageSize(2000);` för att skala ner internt, eller ändra storlek på bilden själv. |

## Utöka demonstrationen

- **Batchbearbetning:** Loopa över en mapp, lägg till varje fil i samma `OcrInput` och samla resultat i en CSV.  
- **Olika språk:** Byt `OcrLanguage.URDU` mot `OcrLanguage.ARABIC` eller kombinera flera språk.  
- **Spara till fil:** Använd `Files.write(Paths.get("output.txt"), ocrResult.getText().getBytes(StandardCharsets.UTF_8));`.  

Alla dessa idéer bygger på **java ocr example** som vi just skapade, vilket låter dig anpassa lösningen till verkliga projekt.

## Slutsats

Du har nu ett robust **image to text java**-arbetsflöde som extraherar Urdu-tecken från en bild med hjälp av Aspose OCR. Handledningen täckte varje steg—från licensiering och språkval till att ladda bilden och skriva ut resultatet—så att du kan klistra in koden i vilket Java‑projekt som helst och se den fungera.

Nästa steg, prova att experimentera med större PDF-filer, olika skript, eller till och med integrera OCR-steget i en Spring Boot REST‑endpoint. Samma principer—**how to extract text**, **load image o

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}