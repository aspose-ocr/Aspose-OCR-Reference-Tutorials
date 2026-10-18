---
category: general
date: 2026-10-18
description: Compileer een Java‑project met Maven en voer het uit vanaf de commandoregel
  met de Maven clean‑, compile‑ en exec‑commando’s. Leer hoe je een Java‑app efficiënt
  kunt bouwen en uitvoeren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- compile java project maven
- execute java class command line
- maven clean compile run
- build and run java app
- maven compile source code
language: nl
lastmod: 2026-10-18
og_description: Compileer een Java‑project met Maven en voer het uit vanaf de commandoregel
  met een stapsgewijze gids. Beheers Maven clean compile run om een Java‑app te bouwen
  en uit te voeren.
og_image_alt: Terminal screenshot showing mvn clean compile exec commands
og_title: Compileer Java‑project met Maven – voer uit vanaf de commandoregel
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
title: Compileer Java‑project met Maven en voer uit vanaf de commandoregel
url: /nl/java/ocr-basics/compile-java-project-maven-and-run-from-command-line/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Compileer Java‑project met Maven en voer het uit vanaf de opdrachtregel

Als je **compile java project maven** moet uitvoeren en de resulterende klasse direct vanuit een terminal wilt starten, laat deze gids je precies zien hoe. Aan het einde van de tutorial kun je oude artefacten opschonen, de broncode compileren en **execute java class command line** gebruiken met een enkele Maven‑commando keten.

De tutorial behandelt alles wat je moet weten om **build and run java app** met Maven, inclusief vereiste plugins, veelvoorkomende valkuilen en tips voor Windows‑ en Unix‑gebaseerde shells. Geen externe documentatie is nodig—volg gewoon de onderstaande stappen.

## Vereisten

* Java Development Kit (JDK) 8 of nieuwer geïnstalleerd en `JAVA_HOME` ingesteld.
* Apache Maven 3.6+ beschikbaar in je `PATH`.
* Een Maven‑project dat een `pom.xml` bevat en een Java‑klasse met een `public static void main(String[] args)`‑methode (voor dit voorbeeld is de klasse `com.aspose.ocr.examples.SimpleOcrDemo`).

## Compileer java project maven

De eerste stap is om alle eerder gecompileerde klassen en andere build‑artefacten te verwijderen. Het uitvoeren van `mvn clean` garandeert een frisse start en voorkomt dat verouderde bytecode runtime‑fouten veroorzaakt.

```bash
# Step 1: Clean previous build artifacts
mvn clean
```

*Waarom clean?* Maven slaat gecompileerde klassen op in `target/`. Als je de clean‑fase overslaat, kunnen oude `.class`‑bestanden blijven bestaan en compilatieproblemen verbergen, vooral na het refactoren van pakkettenamen.

## Voer java class command line uit

Na het opschonen compileer je de bronbestanden. De `compile`‑fase van Maven zet alle `src/main/java`‑bronnen om in bytecode en plaatst de resultaten in `target/classes`.

```bash
# Step 2: Compile the source code
mvn compile
```

Je hebt nu een **maven compile source code**‑output klaar voor uitvoering. Het volgende commando voert de gecompileerde klasse uit zonder een aparte JAR nodig te hebben.

```bash
# Step 3: Run the Simple OCR demo
mvn exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

Het `exec:java`‑doel van de **maven clean compile run**‑plugin start de opgegeven klasse direct vanuit de gecompileerde outputdirectory. Dit is de snelste manier om **execute java class command line** tijdens ontwikkeling uit te voeren.

### Verwachte output

Wanneer de demo succesvol draait, zie je iets vergelijkbaars met:

```
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Building SimpleOCR Demo 1.0
[INFO] ------------------------------------------------------------------------
Hello, OCR world!
Processing completed in 1.23 seconds.
```

Als je een `ClassNotFoundException` ontvangt, controleer dan de volledig gekwalificeerde klassenaam en zorg ervoor dat deze zich onder `src/main/java` bevindt.

## Maven clean compile run workflow

Door de drie commando's samen te voegen ontstaat een compacte, herhaalbare workflow:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

*Waarom ze combineren?* Door de fasen te combineren hoef je niet drie keer op **Enter** te drukken en verkleint de kans dat je een stap vergeet. Maven voert de fasen uit in de volgorde waarin ze verschijnen, waardoor een schone build vóór uitvoering gegarandeerd is.

### Tips voor een soepelere workflow

| Tip | Beschrijving |
|-----|--------------|
| **Gebruik een profiel** | Definieer een Maven‑profiel dat `clean`, `compile` en `exec:java` bundelt zodat je `mvn demo` kunt uitvoeren in plaats van de volledige keten te typen. |
| **Voeg JVM‑opties toe** | Geef `-Dexec.args="-Xmx512m"` door om de heap‑grootte te vergroten voor geheugenintensieve applicaties. |
| **Platform‑onafhankelijk** | Gebruik op Windows `mvn.cmd` terwijl Unix‑shells `mvn` gebruiken. Hetzelfde commando werkt in beide omgevingen. |

## Build en run java app met Maven

Als je de voorkeur geeft aan een distributie‑artefact, kun je Maven je gecompileerde klassen laten verpakken in een uitvoerbare JAR en deze vervolgens uitvoeren met het standaard `java -jar`‑commando:

```bash
# Package the app into a JAR (includes dependencies if you use the shade plugin)
mvn clean package

# Run the packaged JAR
java -jar target/simple-ocr-demo-1.0.jar
```

Deze aanpak is handig wanneer je **build and run java app** moet uitvoeren op een server waar Maven niet geïnstalleerd is. Voor snelle ontwikkeling is de **maven clean compile run**‑reeks echter sneller omdat deze de verpakkingsstap overslaat.

## Maven compile source code – veelvoorkomende valkuilen

Hoewel de commando's eenvoudig zijn, komen ontwikkelaars vaak de volgende problemen tegen:

1. **Missing `exec-maven-plugin`**  
   Als Maven het `exec:java`‑doel niet kan vinden, voeg dan de plugin toe aan je `pom.xml`:

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

2. **Incorrect classpath**  
   Maven compileert naar `target/classes`. Als je handmatig bestanden verplaatst of de standaard outputdirectory wijzigt, kan het `exec:java`‑doel je klasse niet vinden. Houd de standaardindeling aan tenzij je een specifieke reden hebt om deze te wijzigen.

3. **Using the wrong JDK version**  
   Maven erft de JDK van `JAVA_HOME`. Compileren met JDK 11 broncode terwijl je draait op JDK 8 veroorzaakt een `UnsupportedClassVersionError`. Controleer de JDK‑versie met `java -version` en `mvn -v`.

4. **Shell quoting problems**  
   Op Unix, zet de `-Dexec.mainClass`‑waarde tussen enkele aanhalingstekens als deze speciale tekens bevat:  
   `mvn exec:java -Dexec.mainClass='com.example.Main'`.  
   Op Windows werken dubbele aanhalingstekens prima.

Door deze punten aan te pakken kun je betrouwbaar **execute java class command line** uitvoeren in elke omgeving.

## Pro tip: automatiseren met een script

Voor teams die de demo vaak opnieuw bouwen, maak een klein shell‑ of batch‑script:

```bash
#!/usr/bin/env bash
# run-demo.sh – clean, compile, and execute the OCR demo
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

Maak het uitvoerbaar (`chmod +x run-demo.sh`) en voer `./run-demo.sh` uit. Dit elimineert typefouten en zorgt ervoor dat elke ontwikkelaar de exacte **maven clean compile run**‑reeks volgt.

## Conclusie

Je weet nu hoe je **compile java project maven** en direct **execute java class command line** kunt uitvoeren met de clean, compile en exec‑doelen van Maven. De stap‑voor‑stap workflow garandeert een schone build, verwijdert verouderde artefacten, en laat je **build and run java app** uitvoeren met één opdrachtregel.  

Vervolgens kun je het volgende verkennen:

* Het toevoegen van de **shade plugin** om een uber‑JAR voor implementatie te produceren.  
* Het configureren van Maven‑profielen voor verschillende omgevingen (dev, test, prod).  
* Het integreren van unit‑tests met `mvn test` vóór de compile‑stap.

Experimenteer met deze variaties om de workflow in je eigen projecten te passen, en je hebt een robuuste, herhaalbare build‑pipeline die werkt op Windows, macOS en Linux. Veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe OCR te gebruiken in Java – Complete stapsgewijze gids](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/)
- [OCR uitvoeren op afbeelding met Java – Complete Aspose OCR-gids](/ocr/english/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)
- [Hoe OCR uit te voeren met Aspose OCR in Java – Stapsgewijze gids](/ocr/english/java/ocr-operations/how-to-perform-ocr-with-aspose-ocr-in-java-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}