---
category: general
date: 2026-02-17
description: Lär dig att känna igen text från bild och ladda bild för OCR med Aspose
  OCR Java‑biblioteket. Steg‑för‑steg‑guide med stavningskorrigerare.
draft: false
keywords:
- recognize text from image
- load image for OCR
- Aspose OCR Java
- spell corrector OCR
- OCR engine setup
language: sv
og_description: Igenkänn text från bild med Aspose OCR Java. Denna handledning visar
  hur du laddar en bild för OCR, aktiverar stavningskorrigering och får ut ren text.
og_title: igenkänna text från bild – Komplett Aspose OCR Java-guide
tags:
- Java
- OCR
- Aspose
title: Känna igen text från bild med Aspose OCR – Java-handledning
url: /sv/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# igenkänna text från bild med Aspose OCR – Java‑handledning

Har du någonsin behövt **igenkänna text från bild** men varit osäker på vilket bibliotek du ska välja? Du är inte ensam. I många verkliga projekt—tänk på att skanna fakturor, digitalisera handskrivna anteckningar eller extrahera bildtexter från skärmdumpar—är det avgörande att få korrekta OCR‑resultat.  

I den här guiden går vi igenom hur du laddar en bild för OCR, slår på Aspose OCR:s inbyggda stavningskorrigerare och slutligen skriver ut den rensade texten. När du är klar har du ett färdigt Java‑program som **igenkänner text från bild** med bara några rader kod.

## Vad den här handledningen täcker

- Hur du tillämpar din Aspose OCR‑licens (så att demonstrationen körs utan vattenstämplar)  
- Skapa en `OcrEngine`‑instans och välja engelska som igenkänningsspråk  
- **Ladda bild för OCR** med `OcrInput` och peka på en PNG som innehåller felstavade ord  
- Aktivera stavningskorrigeraren, eventuellt peka på en anpassad ordlista  
- Köra igenkänningen och skriva ut det korrigerade resultatet  

Inga externa tjänster, inga dolda konfigurationsfiler—bara ren Java och Aspose OCR‑JAR.

> **Pro tip:** Om du är ny på Aspose, skaffa en gratis 30‑dagars provlicens från Aspose‑webbplatsen och lägg `.lic`‑filen i en mapp som du kan referera till från din kod.

## Förutsättningar

- Java 8 eller nyare (koden kompileras även med JDK 11)  
- Aspose.OCR för Java‑JAR på din klassväg  
- En giltig `Aspose.OCR.lic`‑fil (eller så kan du köra i utvärderingsläge, men demonstrationen kommer då att bädda in en vattenstämpel)  
- En bildfil (`misspelled.png`) som innehåller text med avsiktliga stavfel—perfekt för att se stavningskorrigeraren i aktion  

Har du allt? Bra—låt oss dyka ner.

## Steg 1: Tillämpa din Aspose OCR‑licens

Innan motorn gör något tungt arbete måste den veta att du har licens. Annars får du en “Trial version”-banner i utskriften.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – replace the path with where you stored your .lic file
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

*Varför detta är viktigt:* Licensiering inaktiverar provvattenstämpeln och låser upp hela stavningskorrigerar‑ordlistan. Att hoppa över detta steg fungerar, men din utskrift blir förorenad med texten “Aspose OCR Demo”.

## Steg 2: Skapa och konfigurera OCR‑motorn

Nu startar vi motorn och talar om vilket språk som ska användas. Engelska är det vanligaste, men Aspose stödjer dussintals språk.

```java
        // Step 2: Instantiate the OCR engine
        OcrEngine engine = new OcrEngine();

        // Choose English for recognition – you could pick French, German, etc.
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);
```

*Varför vi ställer in språket:* Språkmodellen bestämmer teckenuppsättningen och påverkar stavningskorrigerarens förslag. Att använda fel språk kan dramatiskt minska noggrannheten.

## Steg 3: Aktivera stavningskorrigering och (valfritt) peka på en anpassad ordlista

Aspose OCR levereras med en inbyggd engelsk ordlista, men du kan ange din egen om du har domänspecifika termer (tänk medicinsk jargong eller produktkoder).

```java
        // Step 3: Turn on the spell corrector
        engine.getSpellCorrector().setEnable(true); // activate spell‑checking

        // Optional: use a custom dictionary folder
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english");
```

*Vad korrigeraren gör:* När OCR‑motorn upptäcker ett ord som inte finns i ordlistan försöker den ersätta det med det närmaste matchande ordet. Detta är anledningen till att demonstrationen kan omvandla “recieve” till “receive” automatiskt.

## Steg 4: Ladda bilden för OCR

Här är delen som svarar direkt på **ladda bild för OCR**. Vi skapar ett `OcrInput`‑objekt och lägger till vår PNG‑fil.

```java
        // Step 4: Prepare the image input
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // path to the image you want to process
```

*Varför vi använder `OcrInput`:* Det abstraherar bort fil‑läsningslogiken och låter dig lägga till flera sidor senare om du behöver bearbeta en flersidig PDF eller en samling bilder.

## Steg 5: Kör igenkänningen och hämta korrigerad text

Motorn gör det tunga arbetet nu—igenkänner tecken, tillämpar språkmodellen och korrigerar slutligen stavningen.

```java
        // Step 5: Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Step 6: Output the corrected text to the console
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

*Förväntad utskrift:* Om `misspelled.png` innehåller frasen “Ths is a smple test” kommer konsolen att skriva ut:

```
Corrected text:
This is a simple test
```

Lägg märke till hur de felstavade orden (`Ths`, `smple`) har rättats automatiskt.

## Fullt, kör‑klart exempel

Nedan är hela programmet i ett block. Kopiera‑klistra, justera sökvägarna och tryck **Run**.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose.OCR license (replace with your license file)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Select the language for recognition (e.g., English)
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);

        // Enable the built‑in spell corrector and optionally set a custom dictionary
        engine.getSpellCorrector().setEnable(true);                     // activate spell‑checking
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english"); // optional

        // Prepare the input image containing the text to be recognized
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // load image for OCR

        // Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Output the corrected text
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

**Tips:** Om du vill bearbeta en JPEG eller BMP istället för PNG, ändra bara filändelsen—Aspose OCR stödjer alla vanliga rasterformat.

## Vanliga frågor & kantfall

- **Vad händer om min bild har låg upplösning?**  
  Öka DPI innan du skickar den till Aspose genom att skala om med ett bibliotek som `java.awt.Image`. Högre DPI ger motorn fler pixlar att arbeta med, vilket vanligtvis förbättrar noggrannheten.

- **Kan jag känna igen flera språk i samma bild?**  
  Ja. Anropa `engine.getLanguage().setLanguage(OcrLanguage.MULTI_LANGUAGE);` och ange eventuellt en lista med språk via `engine.getLanguage().addLanguage(OcrLanguage.SPANISH);`.

- **Min anpassade ordlista används inte—varför?**  
  Kontrollera att mappen innehåller rena textfiler med ett ord per rad och att sökvägen är absolut eller korrekt relativ till din arbetskatalog.

- **Hur extraherar jag förtroendesiffror?**  
  `result.getConfidence()` returnerar ett flyttal mellan 0 och 1 för hela sidan. För förtroende per tecken, utforska `result.getWordList()`.

## Slutsats

Du vet nu hur du **igenkänner text från bild** med Aspose OCR för Java, hur du **laddar bild för OCR**, och hur du aktiverar stavningskorrigeraren för att rensa vanliga stavfel. Det kompletta exemplet ovan är redo att placeras i vilket Maven‑ eller Gradle‑projekt som helst, och med några justeringar kan du skala upp till att batch‑processa mappar, koppla in det i en webbtjänst eller integrera det med ett dokumenthanteringssystem.

Redo för nästa steg? Prova att mata in en flersidig PDF, experimentera med en anpassad ordlista för branschspecifik terminologi, eller kedja resultatet till ett översättnings‑API. Möjligheterna är oändliga, och det grundläggande mönstret—licens → motor → språk → stavningskorrigerare → indata → igenkänning → utdata—förblir detsamma.

Lycka till med kodandet, och må dina OCR‑resultat alltid vara prick‑perfekta!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}