---
category: general
date: 2026-10-18
description: Kompiliere das Java‑Projekt mit Maven und führe es über die Befehlszeile
  mit den Maven‑Befehlen clean, compile und exec aus. Erfahre, wie man Java‑Anwendungen
  effizient baut und ausführt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- compile java project maven
- execute java class command line
- maven clean compile run
- build and run java app
- maven compile source code
language: de
lastmod: 2026-10-18
og_description: Kompiliere ein Java‑Projekt mit Maven und führe es über die Befehlszeile
  aus – mit einer Schritt‑für‑Schritt‑Anleitung. Beherrsche Maven clean compile run,
  um eine Java‑App zu bauen und auszuführen.
og_image_alt: Terminal screenshot showing mvn clean compile exec commands
og_title: Java-Projekt mit Maven kompilieren – aus der Befehlszeile ausführen
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
title: Java‑Projekt mit Maven kompilieren und über die Befehlszeile ausführen
url: /de/java/ocr-basics/compile-java-project-maven-and-run-from-command-line/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java-Projekt mit Maven kompilieren und von der Befehlszeile aus ausführen

Wenn Sie **compile java project maven** und die resultierende Klasse direkt von einem Terminal aus starten müssen, zeigt Ihnen dieser Leitfaden genau, wie das geht. Am Ende des Tutorials können Sie alte Artefakte bereinigen, den Quellcode kompilieren und **execute java class command line** mit einer einzigen Maven‑Befehlsverkettung.

Das Tutorial deckt alles ab, was Sie wissen müssen, um **build and run java app** mit Maven zu erledigen, einschließlich erforderlicher Plugins, gängiger Fallstricke und Tipps für Windows‑ und Unix‑basierte Shells. Keine externe Dokumentation ist nötig – folgen Sie einfach den untenstehenden Schritten.

## Voraussetzungen

* Java Development Kit (JDK) 8 oder neuer installiert und `JAVA_HOME` gesetzt.
* Apache Maven 3.6+ in Ihrem `PATH` verfügbar.
* Ein Maven‑Projekt, das eine `pom.xml` und eine Java‑Klasse mit einer `public static void main(String[] args)`‑Methode enthält (für dieses Beispiel ist die Klasse `com.aspose.ocr.examples.SimpleOcrDemo`).

## Java-Projekt mit Maven kompilieren

Der erste Schritt besteht darin, alle zuvor kompilierten Klassen und anderen Build‑Artefakte zu entfernen. Das Ausführen von `mvn clean` garantiert einen frischen Start und verhindert, dass veralteter Bytecode Laufzeitfehler verursacht.

```bash
# Step 1: Clean previous build artifacts
mvn clean
```

*Warum bereinigen?* Maven speichert kompilierte Klassen in `target/`. Wenn Sie die Clean‑Phase überspringen, können alte `.class`‑Dateien verbleiben und Kompilierungsprobleme verbergen, insbesondere nach einer Umbenennung von Paketen.

## Java‑Klasse von der Befehlszeile aus ausführen

Nach dem Bereinigen kompilieren Sie die Quelldateien. Mavens `compile`‑Phase übersetzt alle `src/main/java`‑Quellen in Bytecode und legt die Ergebnisse in `target/classes` ab.

```bash
# Step 2: Compile the source code
mvn compile
```

Sie haben nun ein **maven compile source code**‑Ergebnis, das zur Ausführung bereitsteht. Der nächste Befehl führt die kompilierte Klasse aus, ohne dass ein separates JAR benötigt wird.

```bash
# Step 3: Run the Simple OCR demo
mvn exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

Das Ziel `exec:java` des **maven clean compile run**‑Plugins startet die angegebene Klasse direkt aus dem kompilierten Ausgabeverzeichnis. Dies ist der schnellste Weg, um **execute java class command line** während der Entwicklung auszuführen.

### Erwartete Ausgabe

Wenn das Demo erfolgreich läuft, sollten Sie etwas Ähnliches sehen:

```
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Building SimpleOCR Demo 1.0
[INFO] ------------------------------------------------------------------------
Hello, OCR world!
Processing completed in 1.23 seconds.
```

Falls Sie eine `ClassNotFoundException` erhalten, überprüfen Sie den vollqualifizierten Klassennamen und stellen Sie sicher, dass er sich unter `src/main/java` befindet.

## Maven clean compile run Arbeitsablauf

Das Zusammenführen der drei Befehle ergibt einen kompakten, wiederholbaren Arbeitsablauf:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

*Warum sie verketten?* Das Kombinieren der Phasen eliminiert die Notwendigkeit, **Enter** dreimal zu drücken, und verringert die Gefahr, einen Schritt zu vergessen. Maven führt die Phasen in der Reihenfolge aus, in der sie erscheinen, und garantiert einen sauberen Build vor der Ausführung.

### Tipps für einen reibungsloseren Arbeitsablauf

| Tip | Description |
|-----|-------------|
| **Profil verwenden** | Definieren Sie ein Maven‑Profil, das `clean`, `compile` und `exec:java` bündelt, sodass Sie `mvn demo` ausführen können, anstatt die gesamte Kette einzugeben. |
| **JVM-Optionen hinzufügen** | Übergeben Sie `-Dexec.args="-Xmx512m"`, um den Heap für speicherintensive Anwendungen zu vergrößern. |
| **Plattformübergreifend** | Unter Windows verwenden Sie `mvn.cmd`, während Unix‑Shells `mvn` nutzen. Der gleiche Befehl funktioniert in beiden Umgebungen. |

## Java‑App mit Maven bauen und ausführen

Wenn Sie ein verteilbares Artefakt bevorzugen, können Sie Maven Ihre kompilierten Klassen in ein ausführbares JAR packen und es dann mit dem Standardbefehl `java -jar` ausführen:

```bash
# Package the app into a JAR (includes dependencies if you use the shade plugin)
mvn clean package

# Run the packaged JAR
java -jar target/simple-ocr-demo-1.0.jar
```

Dieser Ansatz ist nützlich, wenn Sie **build and run java app** auf einem Server benötigen, auf dem Maven nicht installiert ist. Für die schnelle Entwicklung ist jedoch die **maven clean compile run**‑Sequenz schneller, da sie den Verpackungsschritt überspringt.

## Maven compile source code – häufige Fallstricke

Obwohl die Befehle einfach sind, stoßen Entwickler häufig auf die folgenden Probleme:

1. **Missing `exec-maven-plugin`**  
   Wenn Maven das Ziel `exec:java` nicht finden kann, fügen Sie das Plugin zu Ihrer `pom.xml` hinzu:

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
   Maven kompiliert nach `target/classes`. Wenn Sie Dateien manuell verschieben oder das Standardausgabeverzeichnis ändern, kann das Ziel `exec:java` Ihre Klasse nicht finden. Behalten Sie das Standard‑Layout bei, es sei denn, Sie haben einen konkreten Grund, es zu ändern.

3. **Using the wrong JDK version**  
   Maven erbt das JDK von `JAVA_HOME`. Das Kompilieren von Quellcode für JDK 11 bei Ausführung mit JDK 8 führt zu `UnsupportedClassVersionError`. Überprüfen Sie die JDK‑Version mit `java -version` und `mvn -v`.

4. **Shell quoting problems**  
   Unter Unix setzen Sie den Wert von `-Dexec.mainClass` in einfache Anführungszeichen, wenn er Sonderzeichen enthält:  
   `mvn exec:java -Dexec.mainClass='com.example.Main'`.  
   Unter Windows funktionieren doppelte Anführungszeichen einwandfrei.

Durch die Beachtung dieser Punkte können Sie zuverlässig **execute java class command line** in jeder Umgebung ausführen.

## Pro‑Tipp: Automatisierung mit einem Skript

Für Teams, die das Demo häufig neu bauen, erstellen Sie ein kleines Shell‑ oder Batch‑Skript:

```bash
#!/usr/bin/env bash
# run-demo.sh – clean, compile, and execute the OCR demo
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

Machen Sie es ausführbar (`chmod +x run-demo.sh`) und führen Sie `./run-demo.sh` aus. Das eliminiert Tippfehler und stellt sicher, dass jeder Entwickler die exakte **maven clean compile run**‑Sequenz befolgt.

## Fazit

Sie wissen jetzt, wie Sie **compile java project maven** und sofort **execute java class command line** mit Mavens clean-, compile- und exec‑Zielen verwenden. Der Schritt‑für‑Schritt‑Arbeitsablauf garantiert einen frischen Build, eliminiert veraltete Artefakte und ermöglicht Ihnen, **build and run java app** mit einer einzigen Befehlszeile.  

Als Nächstes könnten Sie erkunden:

* Hinzufügen des **shade plugin**, um ein Uber‑JAR für die Bereitstellung zu erzeugen.  
* Konfigurieren von Maven‑Profilen für verschiedene Umgebungen (dev, test, prod).  
* Integration von Unit‑Tests mit `mvn test` vor dem Kompilierungsschritt.

Experimentieren Sie mit diesen Varianten, um den Arbeitsablauf in Ihre eigenen Projekte zu integrieren, und Sie erhalten eine robuste, wiederholbare Build‑Pipeline, die unter Windows, macOS und Linux funktioniert. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to Use OCR in Java – Complete Step‑by‑Step Guide](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/)
- [Run OCR on Image with Java – Complete Aspose OCR Guide](/ocr/english/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)
- [How to Perform OCR with Aspose OCR in Java – Step‑by‑Step Guide](/ocr/english/java/ocr-operations/how-to-perform-ocr-with-aspose-ocr-in-java-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}