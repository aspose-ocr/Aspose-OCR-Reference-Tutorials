---
category: general
date: 2026-10-24
description: Lär dig hur du kör ett Aspose OCR Java-exempel som extraherar text från
  PDF-filer, inklusive parallell OCR‑behandling, hantering av lösenordsskyddade PDF‑filer
  och konvertering av skannade PDF‑filer till sökbar text.
draft: false
keywords:
- aspose ocr java example
- parallel ocr processing
- extract text pdf java
- ocr password protected pdf
- convert scanned pdf searchable
lastmod: 2026-10-24
og_description: Kör ett Aspose OCR Java-exempel för att extrahera text från PDF snabbt.
  Denna guide täcker parallell OCR‑behandling, lösenordsskyddade PDF‑filer och konvertering
  av skannade PDF‑filer till sökbara dokument.
og_image_alt: Screenshot of a Java console showing extracted text after parallel OCR
  processing with Aspose OCR
og_title: Aspose OCR Java-exempel – extrahera text från PDF snabbt
schemas:
- author: Aspose
  dateModified: '2026-10-24'
  description: Learn how to run an Aspose OCR Java example that extracts text from
    PDF files, including parallel OCR processing, handling password‑protected PDFs,
    and converting scanned PDFs to searchable text.
  headline: 'Aspose OCR Java example: extract text from PDF quickly'
  type: TechArticle
- description: Learn how to run an Aspose OCR Java example that extracts text from
    PDF files, including parallel OCR processing, handling password‑protected PDFs,
    and converting scanned PDFs to searchable text.
  name: 'Aspose OCR Java example: extract text from PDF quickly'
  steps:
  - name: set up your project
    text: 'Add the Aspose OCR dependency to your `pom.xml`: If you prefer Gradle,
      replace the snippet with the equivalent `implementation` line. After the dependency
      resolves, you can import the required classes in your Java source file.'
  - name: create and configure the OCR engine
    text: '`OcrEngine` is the core class that performs optical character recognition.
      The `OcrEngine` class is Aspose OCR''s primary object that encapsulates all
      OCR settings and execution logic. Enable parallel processing and optionally
      limit the thread pool: **Why this matters:** - `setParallelProcessing(true'
  - name: load the PDF you want to process
    text: '`OcrInput` represents the collection of files (PDFs, images, or mixed media)
      that the engine will analyze. The `OcrInput` class aggregates one or more input
      sources, allowing you to feed PDFs, TIFFs, or JPEGs to the OCR engine in a single
      batch. Add your PDF (or a set of PDFs) to the input collectio'
  - name: run OCR across all pages in parallel
    text: '`OcrResult` holds the combined text output and per‑page confidence information
      after recognition completes. The `OcrResult` object contains the concatenated
      plain‑text result and a list of `PageResult` objects that expose confidence
      scores for each processed page. Execute the recognition: **Under th'
  - name: retrieve and display the combined text
    text: '`OcrResult.getText()` returns the full searchable string. The `getText()`
      method of `OcrResult` returns a single `String` that contains the OCR‑extracted
      text from every page, with line breaks preserved as they appeared in the source
      PDF. **Expected output:** The console prints one continuous string'
  - name: handle special scenarios
    text: '#### How does the engine deal with password‑protected PDFs? Supply the
      password when adding the file to `OcrInput`: The `add` method overload that
      accepts a password decrypts the document on the fly, allowing seamless OCR without
      manual decryption.'
  type: HowTo
- questions:
  - answer: Yes, the Aspose OCR free trial works for development and testing; a commercial
      license is required for production deployments.
    question: Can I use this example with a free trial license?
  - answer: Absolutely – pass the password to `OcrInput.add(filePath, password)` and
      the engine will decrypt the document automatically.
    question: Does the example support OCR on password‑protected PDFs?
  - answer: Over 70 languages, including right‑to‑left scripts such as Arabic and
      Hebrew.
    question: How many languages does Aspose OCR recognise?
  - answer: The engine can handle multi‑hundred‑page PDFs; you can set a memory limit
      to keep RAM usage predictable.
    question: What is the maximum PDF size I can process?
  - answer: Yes, by configuring `setMaxThreadCount` you control the maximum number
      of concurrent threads, preventing resource exhaustion.
    question: Is parallel OCR safe on shared servers?
  type: FAQPage
tags:
- ocr
- java
- aspose
- pdf
title: 'Aspose OCR Java-exempel: extrahera text från PDF snabbt'
url: /sv/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Java-exempel: extrahera text från PDF snabbt

I den här handledningen kommer du att upptäcka **hur du använder ett Aspose OCR Java-exempel** för att omvandla skannade PDF-filer till sökbar, maskinläsbar text. Oavsett om du har en enda flersidig fil eller en batch av lösenordsskyddade PDF-filer, visar stegen nedan hur du konfigurerar OCR-motorn, aktiverar parallell bearbetning och hämtar den kombinerade utdata med bara några få rader Java‑kod.

Du kommer också att lära dig när du ska justera trådräkningar för optimal prestanda, hur du hanterar krypterade PDF-filer och varför detta tillvägagångssätt är idealiskt för att konvertera skannade PDF-dokument till sökbara arkiv.

![how to use OCR with Aspose OCR Java](/images/ocr-parallel.png "Illustration of parallel OCR processing in Java – how to use OCR")
[how to use OCR with Aspose OCR Java](/images/ocr-parallel.png "Illustration of parallel OCR processing in Java – how to use OCR")

## Snabba svar
- **Vad gör Aspose OCR Java-exemplet?** Det laddar en PDF, kör OCR på varje sida parallellt och returnerar hela den sökbara texten som en enda sträng.  
- **Kan det bearbeta lösenordsskyddade PDF-filer?** Ja – du kan ange dokumentets lösenord när du lägger till filen i `OcrInput`.  
- **Är parallell OCR‑bearbetning värt det?** På en 4‑kärnig maskin minskar den bearbetningstiden med 30‑70 % för PDF-filer med mer än fem sidor.  
- **Vilka språk stöds?** Över 70 språk, inklusive engelska, franska, tyska, kinesiska och arabiska.  
- **Behöver jag en licens för produktion?** En kommersiell Aspose OCR‑licens krävs för icke‑testanvändning; gratisprovan fungerar för utvärdering.

## Vad är ett Aspose OCR Java-exempel?
**Aspose OCR Java-exemplet** är ett kort, körbart program som demonstrerar hur man instansierar `OcrEngine`, konfigurerar parallell körning och extraherar text från PDF-filer med Aspose OCR för Java‑biblioteket. Det visar också hur man hanterar vanliga scenarier såsom lösenordsskyddade dokument, justering av minnesgräns och språkval, och ger en solid grund för att bygga större dokument‑bearbetnings‑pipelines.

## Varför använda parallell OCR‑bearbetning?
Aspose OCR kan dela en flersidig PDF i separata sidor och bearbeta varje sida i sin egen tråd. På en 8‑kärnig server bearbetas ett 120‑sidigt dokument vanligtvis på under 30 sekunder, jämfört med mer än en minut vid sekventiell körning. Denna hastighetsökning är särskilt värdefull när du behöver **konvertera skannade PDF‑arkiv till sökbara** i bulk.

## Förutsättningar
- Java 8 eller nyare installerat.  
- Maven‑ eller Gradle‑byggverktyg (exemplet använder Maven).  
- En Aspose OCR för Java‑licens (gratisprov fungerar för testning).  

## Så kör du Aspose OCR Java‑exemplet steg för steg

### Steg 1: konfigurera ditt projekt

Lägg till Aspose OCR‑beroendet i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.11</version>
</dependency>
```

Om du föredrar Gradle, ersätt kodsnutten med motsvarande `implementation`‑rad.  
När beroendet har lösts kan du importera de nödvändiga klasserna i din Java‑källfil.

### Steg 2: skapa och konfigurera OCR‑motorn

`OcrEngine` är kärnklassen som utför optisk teckenigenkänning.

`OcrEngine`‑klassen är Aspose OCR:s primära objekt som kapslar in alla OCR‑inställningar och exekveringslogik.  
Aktivera parallell bearbetning och begränsa eventuellt trådpoolen:

```java
// Step 2: Initialise the OCR engine and enable parallel processing
OcrEngine ocrEngine = new OcrEngine();

// Turn on parallel processing – this is the key to faster PDF extraction
ocrEngine.setParallelProcessing(true);

// Optional: limit the number of threads (helps on low‑end machines)
ocrEngine.setMaxThreadCount(4);
```

**Varför detta är viktigt:**  
- `setParallelProcessing(true)` fördelar sidor över flera CPU‑kärnor, vilket kraftigt minskar körtiden på flerkärnig hårdvara.  
- `setMaxThreadCount` skyddar serverresurser genom att förhindra att motorn monopoliserar alla kärnor, vilket är avgörande i delad hosting eller CI‑miljöer.

### Steg 3: ladda PDF-filen du vill bearbeta

`OcrInput` representerar samlingen av filer (PDF‑filer, bilder eller blandade medier) som motorn kommer att analysera.

`OcrInput`‑klassen samlar en eller flera inmatningskällor, vilket låter dig skicka PDF‑filer, TIFF‑ eller JPEG‑filer till OCR‑motorn i en enda batch.  
Lägg till din PDF (eller en uppsättning PDF‑filer) i inmatningssamlingen:

```java
// Step 3: Prepare the input – add your multi‑page PDF
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");

// If the PDF is password‑protected, supply the password like this:
// ocrInput.add("protected.pdf", "mySecretPassword");
```

**Tips:** Använd en absolut sökväg eller en sökväg relativ till arbetskatalogen för att undvika `FileNotFoundException`. `add`‑metoden kan anropas upprepade gånger för att köa flera dokument för batch‑bearbetning.

### Steg 4: kör OCR på alla sidor parallellt

`OcrResult` innehåller den kombinerade textutdata samt för‑sidans förtroendeinformation efter att igenkänning slutförts.

`OcrResult`‑objektet innehåller det sammanslagna ren‑textresultatet och en lista med `PageResult`‑objekt som visar förtroendesiffror för varje bearbetad sida.  
Utför igenkänningen:

```java
// Step 4: Perform OCR – this will run on multiple threads
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Bakom kulisserna:** Varje sida överlämnas till en separat arbetstråd (upp till det `maxThreadCount` du definierat). Biblioteket synkroniserar resultaten så att den slutgiltiga `OcrResult` bevarar den ursprungliga sidordningen.

### Steg 5: hämta och visa den kombinerade texten

`OcrResult.getText()` returnerar den fullständiga sökbara strängen.

`getText()`‑metoden i `OcrResult` returnerar en enda `String` som innehåller den OCR‑extraherade texten från varje sida, med radbrytningar bevarade som de förekom i käll‑PDF‑filen.

```java
// Step 5: Output the combined OCR result
System.out.println("Combined text from all pages:");
System.out.println(ocrResult.getText());
```

**Förväntad utskrift:** Konsolen skriver ut en kontinuerlig sträng som innehåller den läsbara texten från alla sidor, redo för indexering, lagring eller vidare bearbetning.

### Steg 6: hantera speciella scenarier

#### Hur hanterar motorn lösenordsskyddade PDF-filer?

Ange lösenordet när du lägger till filen i `OcrInput`:

```java
ocrEngine.getLanguageEngine().setLanguage(OcrLanguage.FRENCH);
```

`add`‑metodens överlagring som accepterar ett lösenord dekrypterar dokumentet i realtid, vilket möjliggör sömlös OCR utan manuell dekryptering.

#### Hur kan jag begränsa minnesanvändning för mycket stora filer?

Anropa `ocrEngine.setMemoryLimit(256);` för att begränsa RAM‑förbrukningen till 256 MB. Motorn kommer automatiskt att skriva överflödig data till temporära filer, vilket förhindrar minnesbrist‑krascher även på PDF‑filer med flera hundra sidor.

## Vanliga frågor & kantfall

### Behöver jag verkligen parallell bearbetning?

Om din PDF innehåller **mer än ett fåtal sidor** och du har minst fyra CPU‑kärnor, minskar aktivering av parallell bearbetning vanligtvis den totala körtiden med **30‑70 %**. För en en‑sidig skanning kan tråduppskattningen överväga fördelen, så du kan inaktivera den med `ocrEngine.setParallelProcessing(false)`.

### Vad händer när en sida misslyckas med OCR?

Aspose OCR kastar ett `OcrException` endast för kritiska fel som en korrupt fil. Sidor som inte kan kännas igen returnerar helt enkelt en tom sträng, vilket motorn tyst sammanslår. Du kan inspektera `ocrResult.getPageResults()` för att hämta för‑sidans förtroendesiffror och hantera låg‑förtroendesidor manuellt.

### Hur ändrar jag igenkänningsspråket?

Motorn använder som standard engelska, men du kan byta språk med:

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing and optionally limit threads
        ocrEngine.setParallelProcessing(true);
        ocrEngine.setMaxThreadCount(4); // Adjust based on your hardware

        // Step 3: Load the multi‑page PDF to be processed
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");
        // Uncomment and set password if needed:
        // ocrInput.add("protected.pdf", "mySecretPassword");

        // Step 4: Recognize text from all pages in parallel
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the combined OCR result
        System.out.println("Combined text from all pages:");
        System.out.println(ocrResult.getText());
    }
}
```

Ersätt `Language.FRENCH` med någon annan stödjande språk‑enum. Detta är viktigt när du behöver **extrahera text PDF Java** från flerspråkiga dokument.

## Proffstips för produktionsklar OCR

- **Batch‑bearbetning:** Inslå flödet i en loop som läser filnamn från en katalog, vilket gör demon till en skalbar tjänst.  
- **Loggning:** Ställ in `ocrEngine.setLogLevel(LogLevel.ERROR)` i produktion för att undertrycka utförlig output.  
- **Resultat‑rengöring:** Efterbehandla `ocrResult.getText()` med reguljära uttryck för att ta bort oönskat blanksteg eller artefakter.  
- **Trådpool‑justering:** Använd `ocrEngine.setMaxThreadCount(Runtime.getRuntime().availableProcessors())` på servrar med många kärnor för maximal genomströmning.  
- **Prestandamätning:** På en 8‑kärnig Intel Xeon bearbetas en 200‑sidig PDF (300 MB) på ~22 sekunder med parallell OCR aktiverad.

## Slutsats

Du har nu ett komplett **Aspose OCR Java‑exempel** som extraherar sökbar text från vilken skannad PDF som helst, stöder lösenordsskyddade filer och utnyttjar parallell bearbetning för hastighet. Genom att integrera denna kod i dina egna applikationer kan du bygga kraftfulla dokument‑digitaliserings‑pipelines, mata OCR‑utdata till sökindex eller kombinera den med översättningstjänster för flerspråkiga arkiv.

Redo för nästa steg? Prova att mata den extraherade texten till Elasticsearch för fulltextsökning, eller kedja utdata med ett språk‑översättnings‑API för att skapa ett flerspråkigt sökbart arkiv. Lycka till med kodningen!

---

**Senast uppdaterad:** 2026-10-24  
**Testat med:** Aspose OCR for Java 24.11  
**Författare:** Aspose  

## Vanliga frågor

**Q: Kan jag använda detta exempel med en gratis provlicens?**  
A: Ja, Aspose OCR‑gratisprovan fungerar för utveckling och testning; en kommersiell licens krävs för produktionsdistributioner.

**Q: Stöder exemplet OCR på lösenordsskyddade PDF-filer?**  
A: Absolut – skicka lösenordet till `OcrInput.add(filePath, password)` så dekrypterar motorn dokumentet automatiskt.

**Q: Hur många språk känner Aspose OCR igen?**  
A: Över 70 språk, inklusive skript som läses från höger till vänster såsom arabiska och hebreiska.

**Q: Vad är den maximala PDF‑storleken jag kan bearbeta?**  
A: Motorn kan hantera PDF‑filer med flera hundra sidor; du kan sätta en minnesgräns för att hålla RAM‑användning förutsägbar.

**Q: Är parallell OCR säker på delade servrar?**  
A: Ja, genom att konfigurera `setMaxThreadCount` styr du det maximala antalet samtidiga trådar, vilket förhindrar resursutarmning.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

```bash
javac -cp "path/to/aspose-ocr.jar" ParallelOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" ParallelOcrDemo
```

## Relaterade handledningar

- [Hur man använder OCR i Java parallell bearbetning med Aspose](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/)
- [Skapa sökbar PDF med Aspose OCR Java‑guide](/ocr/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/)
- [Hur man använder OCR i Java för att extrahera text från PDF med Aspose OCR](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}