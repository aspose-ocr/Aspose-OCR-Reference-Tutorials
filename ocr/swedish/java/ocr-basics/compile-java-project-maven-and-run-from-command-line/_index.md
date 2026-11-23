---
category: general
date: 2026-10-18
description: Kompilera Java‑projekt med Maven och kör från kommandoraden med Maven
  clean, compile och exec‑kommandon. Lär dig hur du bygger och kör Java‑appen effektivt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- compile java project maven
- execute java class command line
- maven clean compile run
- build and run java app
- maven compile source code
language: sv
lastmod: 2026-10-18
og_description: Kompilera Java‑projekt med Maven och kör från kommandoraden med en
  steg‑för‑steg‑guide. Bemästra Maven clean compile run för att bygga och köra Java‑appen.
og_image_alt: Terminal screenshot showing mvn clean compile exec commands
og_title: Kompilera java‑projekt med Maven – kör från kommandoraden
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Compile java project maven and run from command line using Maven clean,
    compile, and exec commands. Learn how to build and run java app efficiently.
  headline: Compile java project maven and run from command line
  type: TechArticle
- description: Compile java project maven and run from command line using Maven clean,
    compile, and exec commands. Learn how to build and run java app efficiently.
  name: Compile java project maven and run from command line
  steps:
  - name: '**Missing `exec-maven-plugin`**'
    text: '**Missing `exec-maven-plugin`**'
  - name: '**Incorrect classpath**'
    text: '**Incorrect classpath**'
  - name: '**Using the wrong JDK version**'
    text: '**Using the wrong JDK version**'
  - name: '**Shell quoting problems**'
    text: '**Shell quoting problems**'
  type: HowTo
tags:
- Maven
- Java
- Command line
title: Kompilera java‑projekt med Maven och kör från kommandoraden
url: /sv/java/ocr-basics/compile-java-project-maven-and-run-from-command-line/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kompilera java‑projekt med Maven och kör från kommandoraden

Om du behöver **kompilera java‑projekt med Maven** och starta den resulterande klassen direkt från en terminal, visar den här guiden exakt hur du gör. I slutet av tutorialen kan du rensa gamla artefakter, kompilera källkoden och **köra java‑klass från kommandoraden** med en enda Maven‑kommandokedja.

Tutorialen täcker allt du behöver veta för att **bygga och köra java‑app** med Maven, inklusive nödvändiga plugins, vanliga fallgropar och tips för Windows‑ och Unix‑baserade skal. Ingen extern dokumentation behövs – följ bara stegen nedan.

## Förutsättningar

Innan du börjar, se till att du har:

* Java Development Kit (JDK) 8 eller nyare installerat och `JAVA_HOME` satt.
* Apache Maven 3.6+ tillgängligt i din `PATH`.
* Ett Maven‑projekt som innehåller en `pom.xml` och en Java‑klass med en `public static void main(String[] args)`‑metod (för detta exempel är klassen `com.aspose.ocr.examples.SimpleOcrDemo`).

## Kompilera java‑projekt med Maven

Det första steget är att ta bort eventuella tidigare kompilerade klasser och andra byggartefakter. Att köra `mvn clean` garanterar en ren start och förhindrar gammal bytekod från att orsaka körfel.

```bash
# Step 1: Clean previous build artifacts
mvn clean
```

*Varför rensa?* Maven lagrar kompilerade klasser i `target/`. Om du hoppar över rensningsfasen kan gamla `.class`‑filer finnas kvar och dölja kompileringsproblem, särskilt efter refaktorering av paketnamn.

## Köra java‑klass från kommandoraden

Efter rensning, kompilera källfilerna. Maven‑fasen `compile` översätter alla `src/main/java`‑källor till bytekod och placerar resultatet i `target/classes`.

```bash
# Step 2: Compile the source code
mvn compile
```

Du har nu en **maven compile source code**‑utdata klar för körning. Nästa kommando kör den kompilerade klassen utan att behöva en separat JAR.

```bash
# Step 3: Run the Simple OCR demo
mvn exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

`exec:java`‑målet i **maven clean compile run**‑pluginet startar den angivna klassen direkt från den kompilerade utmatningskatalogen. Detta är det snabbaste sättet att **köra java‑klass från kommandoraden** under utveckling.

### Förväntad utdata

När demon körs framgångsrikt bör du se något liknande:

```
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Building SimpleOCR Demo 1.0
[INFO] ------------------------------------------------------------------------
Hello, OCR world!
Processing completed in 1.23 seconds.
```

Om du får ett `ClassNotFoundException`, dubbelkolla det fullständiga klassnamnet och säkerställ att det finns under `src/main/java`.

## Maven clean compile run‑arbetsflöde

Att sätta ihop de tre kommandona ger ett kompakt, repeterbart arbetsflöde:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

*Varför kedja dem?* Att kombinera faserna eliminerar behovet av att trycka **Enter** tre gånger och minskar risken att glömma ett steg. Maven kör faserna i den ordning de anges, vilket garanterar en ren byggnad före körning.

### Tips för ett smidigare arbetsflöde

| Tips | Beskrivning |
|-----|-------------|
| **Använd en profil** | Definiera en Maven‑profil som samlar `clean`, `compile` och `exec:java` så att du kan köra `mvn demo` istället för att skriva hela kedjan. |
| **Lägg till JVM‑alternativ** | Skicka `-Dexec.args="-Xmx512m"` för att öka heap‑storleken för minnesintensiva appar. |
| **Plattformsoberoende** | På Windows använd `mvn.cmd` medan Unix‑skal använder `mvn`. Samma kommando fungerar i båda miljöerna. |

## Bygg och kör java‑app med Maven

Om du föredrar en distribuerbar artefakt kan du låta Maven paketera dina kompilerade klasser i en körbar JAR och sedan köra den med standardkommandot `java -jar`:

```bash
# Package the app into a JAR (includes dependencies if you use the shade plugin)
mvn clean package

# Run the packaged JAR
java -jar target/simple-ocr-demo-1.0.jar
```

Detta tillvägagångssätt är användbart när du behöver **bygga och köra java‑app** på en server där Maven inte är installerat. För snabb utveckling är dock sekvensen **maven clean compile run** snabbare eftersom den hoppar över paketeringssteget.

## Maven compile source code – vanliga fallgropar

Även om kommandona är enkla stöter utvecklare ofta på följande problem:

1. **Saknad `exec-maven-plugin`**  
   Om Maven inte hittar målet `exec:java`, lägg till pluginet i din `pom.xml`:

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.codehaus.mojo</groupId>
         <artifactId>exec-maven-plugin</artifactId>
         <version>3.1.0</version>
         <configuration>
           <mainClass>com.aspose.ocr.examples.SimpleOcrDemo</mainClass>
         </configuration>
       </plugin>
     </plugins>
   </build>
   ```

2. **Felaktig klassväg**  
   Maven kompilerar till `target/classes`. Om du manuellt flyttar filer eller ändrar standardutmatningskatalogen kan `exec:java`‑målet misslyckas med att hitta din klass. Behåll standardlayouten om du inte har ett specifikt skäl att ändra den.

3. **Fel JDK‑version**  
   Maven ärver JDK från `JAVA_HOME`. Att kompilera med JDK 11‑källkod medan du kör på JDK 8 ger `UnsupportedClassVersionError`. Verifiera JDK‑versionen med `java -version` och `mvn -v`.

4. **Problem med skal‑citat**  
   På Unix, omge värdet för `-Dexec.mainClass` med enkla citattecken om det innehåller specialtecken:  
   `mvn exec:java -Dexec.mainClass='com.example.Main'`.  
   På Windows fungerar dubbla citattecken bra.

Genom att adressera dessa punkter kan du på ett pålitligt sätt **köra java‑klass från kommandoraden** i vilken miljö som helst.

## Pro‑tips: automatisera med ett skript

För team som ofta bygger om demot, skapa ett litet shell‑ eller batch‑skript:

```bash
#!/usr/bin/env bash
# run-demo.sh – clean, compile, and execute the OCR demo
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

Gör det körbart (`chmod +x run-demo.sh`) och kör `./run-demo.sh`. Detta eliminerar skrivfel och säkerställer att varje utvecklare följer exakt **maven clean compile run**‑sekvensen.

## Slutsats

Du vet nu hur du **kompilerar java‑projekt med Maven** och omedelbart **kör java‑klass från kommandoraden** med Maven:s clean-, compile- och exec‑mål. Det steg‑för‑steg‑arbetsflödet garanterar en ren byggnad, eliminerar föråldrade artefakter och låter dig **bygga och köra java‑app** med ett enda kommandorad.  

Nästa steg kan vara att utforska:

* Att lägga till **shade‑plugin** för att producera en uber‑JAR för distribution.  
* Konfigurera Maven‑profiler för olika miljöer (dev, test, prod).  
* Integrera enhetstester med `mvn test` före kompileringssteget.

Experimentera med dessa variationer för att anpassa arbetsflödet till dina egna projekt, så får du en robust, repeterbar byggpipeline som fungerar på Windows, macOS och Linux. Lycka till med kodandet!


## Vad bör du lära dig härnäst?


Följande tutorials täcker närbesläktade ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Use OCR in Java – Complete Step‑by‑Step Guide](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/)
- [Run OCR on Image with Java – Complete Aspose OCR Guide](/ocr/english/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)
- [How to Perform OCR with Aspose OCR in Java – Step‑by‑Step Guide](/ocr/english/java/ocr-operations/how-to-perform-ocr-with-aspose-ocr-in-java-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}