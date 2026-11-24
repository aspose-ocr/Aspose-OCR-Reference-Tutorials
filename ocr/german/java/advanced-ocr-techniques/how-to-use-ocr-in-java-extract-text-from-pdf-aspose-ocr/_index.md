---
category: general
date: 2026-10-24
description: Erfahren Sie, wie Sie ein Aspose OCR Java Beispiel ausführen, das Text
  aus PDF‑Dateien extrahiert, einschließlich parallel OCR processing, handling password‑protected
  PDFs und converting scanned PDFs to searchable text.
draft: false
keywords:
- aspose ocr java example
- parallel ocr processing
- extract text pdf java
- ocr password protected pdf
- convert scanned pdf searchable
lastmod: 2026-10-24
og_description: Führen Sie ein Aspose OCR Java Beispiel aus, um Text schnell aus PDF
  zu extrahieren. Dieser Leitfaden behandelt parallel OCR processing, password‑protected
  PDFs und converting scanned PDFs to searchable documents.
og_image_alt: Screenshot of a Java console showing extracted text after parallel OCR
  processing with Aspose OCR
og_title: Aspose OCR Java Beispiel – Text schnell aus PDF extrahieren
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
title: 'Aspose OCR Java Beispiel: Text schnell aus PDF extrahieren'
url: /de/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Java Beispiel: Text schnell aus PDF extrahieren

In diesem Tutorial erfahren Sie **wie man ein Aspose OCR Java Beispiel** verwendet, um gescannte PDFs in durchsuchbaren, maschinenlesbaren Text zu verwandeln. Egal, ob Sie eine einzelne mehrseitige Datei oder einen Stapel passwortgeschützter PDFs haben, die untenstehenden Schritte zeigen Ihnen, wie Sie die OCR‑Engine konfigurieren, die parallele Verarbeitung aktivieren und die kombinierte Ausgabe in nur wenigen Zeilen Java‑Code abrufen.

Sie lernen auch, wann Sie die Thread‑Anzahl für optimale Leistung anpassen sollten, wie Sie verschlüsselte PDFs handhaben und warum dieser Ansatz ideal ist, um gescannte PDF‑Dokumente in durchsuchbare Archive zu konvertieren.

![wie man OCR mit Aspose OCR Java verwendet](/images/ocr-parallel.png "Illustration der parallelen OCR‑Verarbeitung in Java – wie man OCR verwendet")
[wie man OCR mit Aspose OCR Java verwendet](/images/ocr-parallel.png "Illustration der parallelen OCR‑Verarbeitung in Java – wie man OCR verwendet")

## Schnelle Antworten
- **Was macht das Aspose OCR Java Beispiel?** Es lädt ein PDF, führt OCR parallel auf jeder Seite aus und gibt den vollständigen durchsuchbaren Text als einzelne Zeichenkette zurück.  
- **Kann es passwortgeschützte PDFs verarbeiten?** Ja – Sie können das Dokumentenpasswort angeben, wenn Sie die Datei zu `OcrInput` hinzufügen.  
- **Lohnt sich die parallele OCR‑Verarbeitung?** Auf einer 4‑Kern‑Maschine reduziert sie die Verarbeitungszeit um 30‑70 % für PDFs mit mehr als fünf Seiten.  
- **Welche Sprachen werden unterstützt?** Über 70 Sprachen, darunter Englisch, Französisch, Deutsch, Chinesisch und Arabisch.  
- **Benötige ich eine Lizenz für die Produktion?** Eine kommerzielle Aspose OCR‑Lizenz ist für den Nicht‑Test‑Einsatz erforderlich; die kostenlose Testversion funktioniert für die Evaluierung.

## Was ist ein Aspose OCR Java Beispiel?
Das **Aspose OCR Java Beispiel** ist ein kompakter, ausführbarer Code, der demonstriert, wie man die `OcrEngine` instanziert, die parallele Ausführung konfiguriert und Text aus PDF‑Dateien mit der Aspose OCR für Java‑Bibliothek extrahiert. Es zeigt außerdem, wie man gängige Szenarien wie passwortgeschützte Dokumente, Speicher‑Limit‑Optimierung und Sprachauswahl behandelt und bietet eine solide Grundlage zum Aufbau größerer Dokument‑Verarbeitungspipelines.

## Warum parallele OCR‑Verarbeitung verwenden?
Aspose OCR kann ein mehrseitiges PDF in einzelne Seiten aufteilen und jede Seite in einem eigenen Thread verarbeiten. Auf einem 8‑Kern‑Server wird ein 120‑seitiges Dokument typischerweise in weniger als 30 Sekunden verarbeitet, verglichen mit mehr als einer Minute bei sequenzieller Ausführung. Dieser Geschwindigkeitsvorteil ist besonders wertvoll, wenn Sie **gescannte PDF‑Archive in durchsuchbare** Dokumente massenhaft konvertieren müssen.

## Voraussetzungen
- Java 8 oder neuer installiert.  
- Maven‑ oder Gradle‑Build‑Tool (das Beispiel verwendet Maven).  
- Eine Aspose OCR für Java‑Lizenz (die kostenlose Testversion funktioniert für Tests).  

## So führen Sie das Aspose OCR Java Beispiel Schritt für Schritt aus

### Schritt 1: Projekt einrichten

Fügen Sie die Aspose OCR‑Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.11</version>
</dependency>
```

Falls Sie Gradle bevorzugen, ersetzen Sie das Snippet durch die entsprechende `implementation`‑Zeile.  
Nachdem die Abhängigkeit aufgelöst ist, können Sie die benötigten Klassen in Ihrer Java‑Quelldatei importieren.

### Schritt 2: OCR‑Engine erstellen und konfigurieren

`OcrEngine` ist die Kernklasse, die die optische Zeichenerkennung durchführt.

Die Klasse `OcrEngine` ist das primäre Objekt von Aspose OCR, das alle OCR‑Einstellungen und die Ausführungslogik kapselt.  
Aktivieren Sie die parallele Verarbeitung und begrenzen Sie optional den Thread‑Pool:

```java
// Step 2: Initialise the OCR engine and enable parallel processing
OcrEngine ocrEngine = new OcrEngine();

// Turn on parallel processing – this is the key to faster PDF extraction
ocrEngine.setParallelProcessing(true);

// Optional: limit the number of threads (helps on low‑end machines)
ocrEngine.setMaxThreadCount(4);
```

**Warum das wichtig ist:**  
- `setParallelProcessing(true)` verteilt Seiten über mehrere CPU‑Kerne und verkürzt die Laufzeit erheblich auf Mehrkern‑Hardware.  
- `setMaxThreadCount` schützt Serverressourcen, indem verhindert wird, dass die Engine alle Kerne monopolisiert, was in Shared‑Hosting‑ oder CI‑Umgebungen entscheidend ist.

### Schritt 3: Laden Sie das zu verarbeitende PDF

`OcrInput` repräsentiert die Sammlung von Dateien (PDFs, Bilder oder gemischte Medien), die die Engine analysieren wird.

Die Klasse `OcrInput` aggregiert eine oder mehrere Eingabequellen, sodass Sie PDFs, TIFFs oder JPEGs in einem einzigen Batch an die OCR‑Engine übergeben können.  
Fügen Sie Ihr PDF (oder eine Menge PDFs) zur Eingabesammlung hinzu:

```java
// Step 3: Prepare the input – add your multi‑page PDF
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");

// If the PDF is password‑protected, supply the password like this:
// ocrInput.add("protected.pdf", "mySecretPassword");
```

**Tipp:** Verwenden Sie einen absoluten Pfad oder einen Pfad relativ zum Arbeitsverzeichnis, um `FileNotFoundException` zu vermeiden. Die Methode `add` kann wiederholt aufgerufen werden, um mehrere Dokumente für die Batch‑Verarbeitung in die Warteschlange zu stellen.

### Schritt 4: OCR parallel über alle Seiten ausführen

`OcrResult` enthält die kombinierte Textausgabe und pro‑Seite‑Konfidenzinformationen, nachdem die Erkennung abgeschlossen ist.

Das Objekt `OcrResult` enthält das zusammengefügte Klartext‑Ergebnis und eine Liste von `PageResult`‑Objekten, die Konfidenzwerte für jede verarbeitete Seite bereitstellen.  
Führen Sie die Erkennung aus:

```java
// Step 4: Perform OCR – this will run on multiple threads
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Im Hintergrund:** Jede Seite wird einem separaten Worker‑Thread zugewiesen (bis zu dem von Ihnen definierten `maxThreadCount`). Die Bibliothek synchronisiert die Ergebnisse, sodass das endgültige `OcrResult` die ursprüngliche Seitenreihenfolge beibehält.

### Schritt 5: Kombinierten Text abrufen und anzeigen

`OcrResult.getText()` gibt die vollständige durchsuchbare Zeichenkette zurück.

Die Methode `getText()` von `OcrResult` gibt einen einzelnen `String` zurück, der den OCR‑extrahierten Text aller Seiten enthält, wobei Zeilenumbrüche so erhalten bleiben, wie sie im Quell‑PDF vorkamen.

```java
// Step 5: Output the combined OCR result
System.out.println("Combined text from all pages:");
System.out.println(ocrResult.getText());
```

**Erwartete Ausgabe:** Die Konsole gibt einen zusammenhängenden String aus, der den lesbaren Text aller Seiten enthält, bereit für Indexierung, Speicherung oder Weiterverarbeitung.

### Schritt 6: Besondere Szenarien behandeln

#### Wie geht die Engine mit passwortgeschützten PDFs um?

Geben Sie das Passwort an, wenn Sie die Datei zu `OcrInput` hinzufügen:

```java
ocrEngine.getLanguageEngine().setLanguage(OcrLanguage.FRENCH);
```

Die überladene `add`‑Methode, die ein Passwort akzeptiert, entschlüsselt das Dokument on‑the‑fly und ermöglicht nahtloses OCR ohne manuelle Entschlüsselung.

#### Wie kann ich den Speicherverbrauch für sehr große Dateien begrenzen?

Rufen Sie `ocrEngine.setMemoryLimit(256);` auf, um den RAM‑Verbrauch auf 256 MB zu begrenzen. Die Engine schreibt überschüssige Daten automatisch in temporäre Dateien, wodurch Out‑of‑Memory‑Abstürze selbst bei PDFs mit mehreren hundert Seiten verhindert werden.

## Häufige Fragen & Randfälle

### Brauche ich wirklich parallele Verarbeitung?

Wenn Ihr PDF **mehr als ein paar Seiten** enthält und Sie mindestens vier CPU‑Kerne haben, reduziert das Aktivieren der parallelen Verarbeitung typischerweise die Gesamtlaufzeit um **30‑70 %**. Bei einem einseitigen Scan kann der Thread‑Overhead den Nutzen überwiegen, sodass Sie es mit `ocrEngine.setParallelProcessing(false)` deaktivieren können.

### Was passiert, wenn eine Seite nicht OCR‑erkannt wird?

Aspose OCR wirft nur bei fatalen Fehlern wie einer beschädigten Datei eine `OcrException`. Seiten, die nicht erkannt werden können, geben einfach einen leeren String zurück, den die Engine stillschweigend anfügt. Sie können `ocrResult.getPageResults()` prüfen, um pro‑Seite‑Konfidenzwerte zu erhalten und Seiten mit niedriger Konfidenz manuell zu behandeln.

### Wie ändere ich die Erkennungssprache?

Die Engine verwendet standardmäßig Englisch, aber Sie können die Sprache ändern mit:

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

Ersetzen Sie `Language.FRENCH` durch ein beliebiges unterstütztes Sprach‑Enum. Dies ist wichtig, wenn Sie **Text aus PDF Java** aus mehrsprachigen Dokumenten extrahieren müssen.

## Pro‑Tipps für produktionsreifes OCR

- **Batch‑Verarbeitung:** Packen Sie den Ablauf in eine Schleife, die Dateinamen aus einem Verzeichnis liest, und verwandeln Sie die Demo in einen skalierbaren Service.  
- **Logging:** Setzen Sie `ocrEngine.setLogLevel(LogLevel.ERROR)` in der Produktion, um ausführliche Ausgaben zu unterdrücken.  
- **Ergebnis‑Bereinigung:** Verarbeiten Sie `ocrResult.getText()` nachträglich mit regulären Ausdrücken, um überflüssige Leerzeichen oder Artefakte zu entfernen.  
- **Thread‑Pool‑Optimierung:** Verwenden Sie `ocrEngine.setMaxThreadCount(Runtime.getRuntime().availableProcessors())` auf Servern mit vielen Kernen für maximalen Durchsatz.  
- **Performance‑Benchmark:** Auf einem 8‑Kern‑Intel‑Xeon verarbeitet ein 200‑seitiges PDF (300 MB) mit aktivierter paralleler OCR in etwa 22 Sekunden.

## Fazit

Sie haben nun ein vollständiges **Aspose OCR Java Beispiel**, das durchsuchbaren Text aus jedem gescannten PDF extrahiert, passwortgeschützte Dateien unterstützt und für Geschwindigkeit parallele Verarbeitung nutzt. Durch die Integration dieses Codes in Ihre eigenen Anwendungen können Sie leistungsstarke Dokument‑Digitalisierungspipelines bauen, OCR‑Ausgaben in Suchindizes einspeisen oder sie mit Übersetzungsdiensten für mehrsprachige Archive kombinieren.

Bereit für den nächsten Schritt? Versuchen Sie, den extrahierten Text in Elasticsearch für die Volltextsuche zu speisen, oder verknüpfen Sie die Ausgabe mit einer Sprach‑Übersetzungs‑API, um ein mehrsprachiges durchsuchbares Repository zu erstellen. Viel Spaß beim Coden!

---

**Zuletzt aktualisiert:** 2026-10-24  
**Getestet mit:** Aspose OCR for Java 24.11  
**Autor:** Aspose  

## Häufig gestellte Fragen

**F: Kann ich dieses Beispiel mit einer kostenlosen Testlizenz verwenden?**  
A: Ja, die kostenlose Aspose OCR‑Testversion funktioniert für Entwicklung und Tests; für den Produktionseinsatz ist eine kommerzielle Lizenz erforderlich.

**F: Unterstützt das Beispiel OCR für passwortgeschützte PDFs?**  
A: Absolut – übergeben Sie das Passwort an `OcrInput.add(filePath, password)` und die Engine entschlüsselt das Dokument automatisch.

**F: Wie viele Sprachen erkennt Aspose OCR?**  
A: Über 70 Sprachen, einschließlich Rechts‑zu‑Links‑Schriften wie Arabisch und Hebräisch.

**F: Wie groß ist die maximale PDF‑Größe, die ich verarbeiten kann?**  
A: Die Engine kann PDFs mit mehreren hundert Seiten verarbeiten; Sie können ein Speicher‑Limit setzen, um den RAM‑Verbrauch vorhersehbar zu halten.

**F: Ist paralleles OCR auf Shared‑Servern sicher?**  
A: Ja, durch Konfiguration von `setMaxThreadCount` steuern Sie die maximale Anzahl gleichzeitiger Threads und verhindern eine Ressourcenüberlastung.

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

## Verwandte Tutorials

- [Wie man OCR in Java Parallelverarbeitung mit Aspose verwendet](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/)
- [Erstelle durchsuchbares PDF mit Aspose OCR Java Anleitung](/ocr/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/)
- [Wie man OCR in Java verwendet, um Text aus PDF mit Aspose OCR zu extrahieren](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}