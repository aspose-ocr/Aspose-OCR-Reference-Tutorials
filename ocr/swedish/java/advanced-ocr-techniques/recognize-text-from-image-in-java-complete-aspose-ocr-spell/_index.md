---
category: general
date: 2026-06-19
description: Identifiera text från bild med Aspose OCR i Java. Lär dig hur du aktiverar
  stavningskontroll, lägger till en ordlista och utför OCR med stavningskontroll i
  en enda handledning.
draft: false
keywords:
- recognize text from image
- how to enable spellcheck
- how to add dictionary
- ocr with spell check
language: sv
og_description: Känn igen text från bild med Aspense OCR i Java. Denna guide visar
  hur du aktiverar stavningskontroll, lägger till en ordlista och kör OCR med stavningskontroll.
og_title: Känn igen text från bild – Aspose OCR stavningskontrollhandledning
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Recognize text from image with Aspose OCR in Java. Learn how to enable
    spellcheck, add dictionary, and perform OCR with spell check in a single tutorial.
  headline: Recognize Text from Image in Java – Complete Aspose OCR Spell‑Check Guide
  type: TechArticle
- description: Recognize text from image with Aspose OCR in Java. Learn how to enable
    spellcheck, add dictionary, and perform OCR with spell check in a single tutorial.
  name: Recognize Text from Image in Java – Complete Aspose OCR Spell‑Check Guide
  steps:
  - name: How to Enable SpellCheck
    text: 'The spell checker lives inside the engine, but it’s disabled by default.
      Flip the switch with a single line:'
  - name: Expected Output
    text: 'Assuming `receipt.png` contains the line “Totel: $12.99” and your custom
      dictionary includes “Total”, the console will display:'
  - name: What if I need multiple languages?
    text: You can call `ocrEngine.setLanguage(Language.English, Language.French)`
      to enable multilingual recognition. Spell‑checking will follow each language’s
      rules, but you still need to enable it with `setEnable(true)`.
  - name: How does the engine handle unknown words?
    text: If a word isn’t in the internal dictionary *and* not in your custom dictionary,
      the spell checker attempts a best‑guess correction based on Levenshtein distance.
      For truly unknown terms, add them to `my-terms.txt`.
  - name: Does the spell checker work on numbers?
    text: By default, numeric strings are left untouched. If you have alphanumeric
      codes (e.g., “AB12C”), add them to your custom dictionary; otherwise the engine
      may try to “fix” them to real words.
  - name: Performance considerations
    text: Enabling spell checking adds a modest overhead—roughly 10‑15 % extra CPU
      per page. For batch processing, consider disabling it on the first pass, then
      re‑run only on pages that failed quality checks.
  type: HowTo
tags:
- OCR
- Java
- SpellCheck
title: Känn igen text från bild i Java – Komplett Aspose OCR stavningskontrollguide
url: /sv/java/advanced-ocr-techniques/recognize-text-from-image-in-java-complete-aspose-ocr-spell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Känn igen text från bild i Java – Komplett Aspose OCR stavningskontrollguide

Har du någonsin behövt **känna igen text från bild** men oroat dig för att resultatet skulle vara fullt av stavfel? Du är inte ensam. I många kvitto‑skannings‑ eller dokument‑digitaliseringsprojekt ser den råa OCR‑texten ut som om den skrivits av en sömnig katt. De goda nyheterna? Med Aspose OCR kan du förvandla den bullriga dumpen till ren, stavningskontrollerad text—direkt i Java.

I den här handledningen går vi igenom ett färdigt exempel som visar **hur man aktiverar stavningskontroll**, **hur man lägger till ordboks**‑poster för domänspecifika termer, och slutligen hur man utför **ocr med stavningskontroll**. När du är klar har du ett självständigt program som läser en bildfil, korrigerar stavning i farten och skriver ut det polerade resultatet.

## Vad du kommer att lära dig

- Hur du applicerar en Aspose OCR‑licens så att API‑et körs med full hastighet.  
- De exakta stegen för att **aktivera stavningskontroll** på OCR‑motorn.  
- Det korrekta sättet att **lägga till en anpassad ordbok** för ord som produktkoder eller varumärkesnamn.  
- Hur du anropar `recognizeImage` och får ren, korrigerad text.  

Inga externa verktyg, inga egenbyggda stavningskontroller‑bibliotek—bara ren Java och Aspose OCR.

## Förutsättningar

- Java 8+ (koden kompileras med vilken recent JDK som helst).  
- En Aspose OCR‑licensfil (`Aspose.OCR.lic`). Om du bara testar fungerar den fria utvärderingen men lägger till ett vattenmärke.  
- Maven eller Gradle för att hämta `aspose-ocr`‑beroendet, eller så kan du lägga till JAR‑filerna manuellt.  
- En exempelbild (t.ex. en kvitto‑PNG) och en textfil som innehåller anpassade termer.

> **Pro tip:** Håll din anpassade ordbok i UTF‑8 och en term per rad—Aspose OCR läser den direkt från filsystemet.

---

## Steg 1: Ställ in projektet och lägg till Aspose OCR‑beroendet

Om du använder Maven, lägg till följande kodsnutt i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.8</version> <!-- use the latest version -->
</dependency>
```

För Gradle är det samma idé:

```groovy
implementation 'com.aspose:aspose-ocr:23.8'
```

När beroendet har lösts, skapa en ny Java‑klass som heter `SpellCheckDemo`. Här sker magin.

## Steg 2: Applicera Aspose OCR‑licensen

Innan någon OCR‑behandling måste du tala om för Aspose att den får köras utan begränsningar. Att hoppa över detta steg utlöser ett runtime‑undantag.

```java
// Apply the Aspose OCR license – this removes evaluation watermarks
License license = new License();
license.setLicense("Aspose.OCR.lic");   // path to your .lic file
```

> **Varför detta är viktigt:** Licensen låser upp hela OCR‑motorn, inklusive den inbyggda stavningskontrollmodulen. Utan den fungerar motorn fortfarande men vägrar använda vissa premium‑funktioner.

## Steg 3: Skapa och konfigurera OCR‑motorn

Nu instansierar vi kärnan `OcrEngine` och sätter språket till English. Detta är baslinjen för både igenkänning och stavningskontroll.

```java
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.setLanguage(Language.English);   // choose the language that matches your image
```

### Hur man aktiverar SpellCheck

Stavningskontrollen finns inuti motorn, men den är inaktiverad som standard. Slå på den med en enda rad:

```java
ocrEngine.getSpellChecker().setEnable(true);   // enables spell‑checking
```

Den raden uppfyller kravet **hur man aktiverar stavningskontroll**. När den är aktiverad kommer motorn automatiskt att jämföra varje igenkänt ord mot sin interna ordbok och föreslå korrigeringar.

## Steg 4: Ladda en anpassad ordbok (Hur man lägger till ordbok)

Om dina dokument innehåller fackspråk—tänk produkt‑SKU:n, medicinska termer eller varumärkesnamn—vill du lära stavningskontrollen dem. Aspose OCR låter dig peka på en vanlig textfil, en term per rad.

```java
// Load a custom word list for spell‑checking
Path customDict = java.nio.file.Paths.get("YOUR_DIRECTORY/my-terms.txt");
ocrEngine.getSpellChecker().addUserDictionary(customDict);
```

> **Vad händer om filen inte hittas?** API‑et kastar ett `FileNotFoundException`. Omge anropet med ett `try/catch` om du behöver en mjuk nedtrappning.

Nu känner motorn till “AcmeWidget” eller “RX‑9000” och flaggar dem inte som felstavade.

## Steg 5: Känn igen text från bilden

Med motorn förberedd kan du äntligen **känna igen text från bild**. Metoden `recognizeImage` returnerar ett `OcrResult`‑objekt som innehåller både rå‑ och korrigerad text.

```java
// Recognize text from the image file
OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/receipt.png");
```

Eftersom vi aktiverade stavningskontrollen tidigare, returnerar anropet `getText()` redan den korrigerade versionen.

## Steg 6: Skriv ut den korrigerade texten

Allt som återstår är att skriva ut (eller lagra) den rensade strängen.

```java
// Output the corrected, spell‑checked text
System.out.println(ocrResult.getText());
```

När du kör programmet bör du se ett snyggt formaterat kvitto med korrekt stavning, även om den ursprungliga bilden innehöll suddiga tecken.

---

## Fullt fungerande exempel

Nedan är det kompletta, färdiga Java‑programmet. Kopiera‑klistra in det i din IDE, justera filvägarna och tryck på **Run**.

```java
import com.aspose.ocr.*;

import java.nio.file.Path;
import java.nio.file.Paths;

public class SpellCheckDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");   // <-- replace with your license path

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setLanguage(Language.English);

        // Step 3: Load a custom word list for spell‑checking
        Path dictPath = Paths.get("YOUR_DIRECTORY/my-terms.txt"); // <-- your dictionary file
        ocrEngine.getSpellChecker().addUserDictionary(dictPath);
        ocrEngine.getSpellChecker().setEnable(true); // <-- how to enable spellcheck

        // Step 4: Recognize text from the image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/receipt.png"); // <-- your image

        // Step 5: Output the corrected text
        System.out.println(ocrResult.getText());
    }
}
```

### Förväntad utskrift

Om `receipt.png` innehåller raden “Totel: $12.99” och din anpassade ordbok inkluderar “Total”, kommer konsolen att visa:

```
Total: $12.99
```

Stavfelet “Totel” har automatiskt korrigerats tack vare **ocr med stavningskontroll**.

---

## Vanliga frågor & kantfall

### Vad händer om jag behöver flera språk?

Du kan anropa `ocrEngine.setLanguage(Language.English, Language.French)` för att aktivera flerspråkig igenkänning. Stavningskontrollen följer varje språks regler, men du måste fortfarande aktivera den med `setEnable(true)`.

### Hur hanterar motorn okända ord?

Om ett ord varken finns i den interna ordboken *och* inte i din anpassade ordbok, försöker stavningskontrollen göra en bästa‑gissning baserad på Levenshtein‑avstånd. För riktigt okända termer, lägg till dem i `my-terms.txt`.

### Fungerar stavningskontrollen på siffror?

Som standard lämnas numeriska strängar orörda. Om du har alfanumeriska koder (t.ex. “AB12C”), lägg till dem i din anpassade ordbok; annars kan motorn försöka “fixa” dem till riktiga ord.

### Prestandaöverväganden

Att aktivera stavningskontroll ger en måttlig extra belastning—ungefär 10‑15 % mer CPU per sida. För batch‑behandling, överväg att inaktivera den på första passet och sedan köra om endast de sidor som misslyckades med kvalitetskontrollen.

---

## Sammanfattning

Vi har gått igenom allt du behöver för att **känna igen text från bild** med Aspose OCR i Java samtidigt som du håller resultatet rent. Stegen var:

1. Applicera licensen.  
2. Skapa `OcrEngine` och sätt språket.  
3. **Hur man lägger till ordbok** – ladda en anpassad ordlista.  
4. **Hur man aktiverar stavningskontroll** – slå på stavningskontrollen.  
5. Kör `recognizeImage` (kärnan i **ocr med stavningskontroll**).  
6. Skriv ut den korrigerade texten.

Det är hela pipeline:n—from råa pixlar till polerade, stavningskontrollerade strängar.

---

## Vad blir nästa steg?

- **Batch‑behandling:** Loopa över en mapp med bilder och skriv varje resultat till en separat `.txt`‑fil.  
- **PDF‑utmatning:** Använd Aspose PDF för att bädda in den korrigerade texten i en sökbar PDF.  
- **Avancerade ordböcker:** Ladda flera användar‑ordböcker för olika domäner (t.ex. finans vs. medicin).  
- **Konfidenspoäng:** Inspektera `ocrResult.getConfidence()` för att filtrera resultat med låg säkerhet.

Känn dig fri att experimentera—byt språk, justera ordboken eller kombinera detta med bild‑förbehandlingsbibliotek för ännu bättre precision.

Om du stöter på problem, lämna en kommentar nedan. Lycka till med kodandet, och må din OCR alltid vara stavningskontrollerad!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [känna igen text bild med Aspose OCR – Fullständig Java OCR‑handledning](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Hur man OCR‑bilder med språk med Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Hur man extraherar text från bild från URL med Aspose.OCR för Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}