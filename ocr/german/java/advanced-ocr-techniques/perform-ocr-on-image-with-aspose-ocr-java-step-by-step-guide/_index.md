---
category: general
date: 2026-09-23
description: Erfahren Sie, wie Sie OCR auf Bildern in Java mit Aspose OCR durchführen,
  Text aus einem Bild extrahieren und Rechtschreibkorrektur mit einem benutzerdefinierten
  Wörterbuch aktivieren.
draft: false
keywords:
- how to perform ocr
- how to extract text from image
- java ocr maven dependency
- java image to text conversion
- aspose ocr java
lastmod: 2026-09-23
og_description: Wie man OCR auf Bildern in Java mit Aspose OCR durchführt. Dieser
  Leitfaden zeigt das Laden eines Bildes, das Extrahieren von Text aus dem Bild und
  das Hinzufügen einer Rechtschreibkorrektur für genaue Ergebnisse.
og_image_alt: 'Aspose OCR Java tutorial: extracting text from images with spell correction'
og_title: Wie man OCR auf Bildern mit Aspose OCR in Java durchführt
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  headline: How to perform OCR on images with Aspose OCR in Java
  type: TechArticle
- description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  name: How to perform OCR on images with Aspose OCR in Java
  steps:
  - name: set up the project and import dependencies
    text: Add the Aspose OCR Maven dependency to your `pom.xml`. This single line
      pulls in the core OCR engine and all required transitive libraries. > **Pro
      tip:** Verify the version number on Maven Central; newer releases add language
      packs and performance improvements.
  - name: load the image for OCR
    text: '`OcrEngine` works with any `InputStream`. Use `ImageStream` to wrap a file
      path, byte array, or URL. **Definition anchor:** `ImageStream` is Aspose OCR’s
      lightweight wrapper that reads image data from various sources without converting
      it to a `BufferedImage` first.'
  - name: enable spell‑correction (optional but powerful)
    text: Turn on the built‑in spell‑correction flag to automatically fix common OCR
      mis‑recognitions such as “l” vs “1”. Spell‑correction can improve accuracy by
      up to **80 %** on low‑contrast scans, turning “Inv0ice” into “Invoice” without
      extra code.
  - name: provide a custom dictionary (tailor the engine)
    text: Supply a plain‑text dictionary for industry‑specific terminology—medical
      codes, legal terms, product SKUs, etc. **Definition anchor:** `CustomDictionary`
      loads a UTF‑8 word list that the OCR engine consults during post‑processing
      to prefer your domain vocabulary.
  - name: run the OCR process
    text: Invoke `process()` to get an `OcrResult` containing the recognized text,
      confidence scores, and optional layout data. If an error occurs, `ocrResult.getErrorMessage()`
      returns a detailed description you can log or display.
  - name: output the recognized (and corrected) text
    text: 'Print the extracted string to the console or write it to a file. For quick
      testing, a simple `System.out.println` is sufficient. Running the program should
      produce clean, searchable text similar to: If you notice stray characters, revisit
      your custom dictionary and consider pre‑processing the image '
  type: HowTo
- questions:
  - answer: No. The library runs entirely offline; all recognition happens locally
      on your JVM.
    question: Does Aspose OCR require an internet connection?
  - answer: Aspose OCR supports Java 8 through Java 21, including both standard and
      OpenJDK distributions.
    question: Which Java versions are supported?
  - answer: Yes. The engine streams data and can handle images up to 500 MB, limited
      only by available heap memory.
    question: Can I process images larger than 10 MB?
  - answer: Purchase a commercial license from the Aspose store and set the license
      file with `License license = new License(); license.setLicense("Aspose.OCR.lic");`.
    question: How do I license Aspose OCR for production?
  - answer: Aspose OCR includes a handwriting mode that can be enabled via `ocrEngine.getEngineOptions().setHandwriting(true);`,
      improving accuracy on cursive scripts.
    question: Is there built‑in support for handwritten text?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
- image to text
- OCR Maven dependency
title: Wie man OCR auf Bildern mit Aspose OCR in Java durchführt
url: /de/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Durchführen von OCR auf Bild – vollständiges Java‑Tutorial

Wenn Sie nach einer zuverlässigen Möglichkeit suchen, **how to perform OCR** auf Bilddateien mit Java durchzuführen, sind Sie hier genau richtig. Mit Aspose OCR für Java können Sie Text aus Bilddateien in nur wenigen Codezeilen extrahieren, die Genauigkeit mit einem benutzerdefinierten Wörterbuch steigern und die Rechtschreibkorrektur aktivieren, um verrauschte Scans zu bereinigen. Dieses Tutorial führt Sie durch jeden Schritt – vom Laden des Bildes für OCR bis zum Ausgeben des korrigierten Textes – sodass Sie die Bild‑zu‑Text‑Konvertierung noch heute in Ihre Anwendungen integrieren können.

## Schnelle Antworten
- **What is the main class to start OCR?** `OcrEngine` ist die Kernklasse von Aspose OCR, die die optische Zeichenerkennung durchführt.
- **Which Maven artifact adds OCR support?** Fügen Sie `com.aspose:aspose-ocr` zu Ihrer `pom.xml` hinzu.
- **Do I need a license for development?** Eine kostenlose temporäre Lizenz funktioniert für Tests; für die Produktion ist eine kommerzielle Lizenz erforderlich.
- **Can I improve accuracy on low‑quality scans?** Ja – aktivieren Sie die Rechtschreibkorrektur und stellen Sie ein benutzerdefiniertes Wörterbuch bereit.
- **Is multi‑page support built‑in?** Verarbeiten Sie jedes Seitenbild in einer Schleife; die Engine ist thread‑sicher für gleichzeitige Ausführungen.

## Was ist how to perform OCR?
Der Ausdruck **how to perform OCR** bezieht sich auf den Vorgang, gedruckten oder handschriftlichen Text in einem Bild in editierbare, durchsuchbare digitale Zeichen zu konvertieren, wobei optische Zeichenerkennungstechnologie verwendet wird. Aspose OCR implementiert diesen Prozess mit einer Single‑Pass‑Engine, die über 20 Rasterformate und mehr als 50 Sprachen unterstützt.

## Warum Aspose OCR für Java verwenden?
Aspose OCR unterstützt **20+ Bildformate** (einschließlich PNG, JPEG, TIFF, BMP und GIF) und kann **Mehrhundert‑Seiten‑Batches** verarbeiten, ohne das gesamte Dokument in den Speicher zu laden, und liefert bis zu **300 Seiten pro Minute** auf einem typischen 4‑Kern‑Server. Die integrierte Rechtschreibkorrektur und die Funktionen für benutzerdefinierte Wörterbücher reduzieren die typischen OCR‑Fehlerraten von 12 % auf unter 2 % bei verrauschten Rechnungen.

## Voraussetzungen
- **Java Development Kit (JDK) 8+** – Standard‑Java‑Runtime.
- **Aspose OCR for Java** Bibliothek – holen Sie sich das neueste JAR von Maven Central oder dem Aspose‑Download‑Portal.
- Eine Bilddatei (z. B. `invoice.png`), die Sie verarbeiten möchten.
- (Optional) `custom_dict.txt` – eine UTF‑8‑Textdatei, die domänenspezifische Wörter enthält, eines pro Zeile.

Das ist alles, was Sie benötigen – keine externen Dienste oder schweren Frameworks.

## Wie man OCR auf einem Bild in Java durchführt?
Laden Sie Ihr Bild, aktivieren Sie die Rechtschreibkorrektur, geben Sie optional ein benutzerdefiniertes Wörterbuch an, führen Sie die Engine aus und lesen Sie das Ergebnis. Dieser Ansatz funktioniert sowohl für Einzelseiten‑Dateien als auch für die Batch‑Verarbeitung, und die Engine übernimmt automatisch die Bilddekodierung, Spracherkennung und Confidence‑Scoring, sodass Sie eine zuverlässige Textausgabe erhalten, die für die weitere Verarbeitung bereit ist. Die folgenden Abschnitte zerlegen jeden Schritt mit klaren Erklärungen und dem genauen Code, den Sie kopieren müssen.

### Schritt 1: Projekt einrichten und Abhängigkeiten importieren

Fügen Sie die Aspose OCR Maven‑Abhängigkeit zu Ihrer `pom.xml` hinzu. Diese eine Zeile zieht die Kern‑OCR‑Engine und alle erforderlichen transitiven Bibliotheken ein.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

> **Pro‑Tipp:** Überprüfen Sie die Versionsnummer auf Maven Central; neuere Releases fügen Sprachpakete und Leistungsverbesserungen hinzu.

### Schritt 2: Bild für OCR laden

`OcrEngine` funktioniert mit jedem `InputStream`. Verwenden Sie `ImageStream`, um einen Dateipfad, ein Byte‑Array oder eine URL zu umschließen.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you wish to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Definition‑Anker:** `ImageStream` ist Aspose OCRs leichtgewichtiger Wrapper, der Bilddaten aus verschiedenen Quellen liest, ohne sie zuerst in ein `BufferedImage` zu konvertieren.

### Schritt 3: Rechtschreibkorrektur aktivieren (optional aber leistungsstark)

Aktivieren Sie das integrierte Rechtschreibkorrektur‑Flag, um häufige OCR‑Fehler wie „l“ vs. „1“ automatisch zu korrigieren.

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

Die Rechtschreibkorrektur kann die Genauigkeit bei kontrastreichen Scans um bis zu **80 %** verbessern und „Inv0ice“ in „Invoice“ umwandeln, ohne zusätzlichen Code.

### Schritt 4: Benutzerdefiniertes Wörterbuch bereitstellen (Engine anpassen)

Stellen Sie ein Klartext‑Wörterbuch für branchenspezifische Terminologie bereit – medizinische Codes, juristische Begriffe, Produkt‑SKUs usw.

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

**Definition‑Anker:** `CustomDictionary` lädt eine UTF‑8‑Wortliste, die die OCR‑Engine während der Nachbearbeitung konsultiert, um Ihre Domänen‑Vokabeln zu bevorzugen.

### Schritt 5: OCR‑Prozess ausführen

Rufen Sie `process()` auf, um ein `OcrResult` zu erhalten, das den erkannten Text, Confidence‑Scores und optionale Layout‑Daten enthält.

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

Wenn ein Fehler auftritt, gibt `ocrResult.getErrorMessage()` eine detaillierte Beschreibung zurück, die Sie protokollieren oder anzeigen können.

### Schritt 6: Erkannten (und korrigierten) Text ausgeben

Geben Sie die extrahierte Zeichenkette in der Konsole aus oder schreiben Sie sie in eine Datei. Für schnelle Tests reicht ein einfaches `System.out.println` aus.

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

Das Ausführen des Programms sollte sauberen, durchsuchbaren Text erzeugen, ähnlich wie:

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

Wenn Sie fremde Zeichen bemerken, überprüfen Sie Ihr benutzerdefiniertes Wörterbuch und erwägen Sie eine Vorverarbeitung des Bildes (Kontrast erhöhen, Rauschen entfernen oder in Graustufen konvertieren).

## Wie man Text aus Bild mit einem benutzerdefinierten Wörterbuch extrahiert

Laden Sie das Wörterbuch vor der Verarbeitung, dann rufen Sie `ocrEngine.setCustomDictionary(customDict)` auf. Die Engine wird Wörter aus der Liste priorisieren und dadurch Fehlalarme bei spezialisierten Vokabularen drastisch reduzieren. Durch die Bereitstellung domänenspezifischer Begriffe unterstützen Sie den OCR‑Nachbearbeiter dabei, mehrdeutige Zeichen zu lösen, z. B. den Buchstaben „O“ von der Ziffer „0“ zu unterscheiden, was die Gesamte‑Genauigkeit bei technischen Dokumenten verbessert.

## Wie man die Java‑OCR‑Maven‑Abhängigkeit korrekt hinzufügt

Fügen Sie das folgende Snippet zu Ihrer `pom.xml` im Abschnitt `<dependencies>` hinzu. Diese Abhängigkeit zieht die Kern‑Aspose‑OCR‑Bibliothek zusammen mit allen erforderlichen transitiven Komponenten, sodass die OCR‑Engine ohne zusätzliche Konfiguration instanziiert werden kann. Stellen Sie sicher, dass Sie nach dem Aktualisieren der Datei `mvn clean install` ausführen, damit Maven die neueste Version aus dem zentralen Repository auflöst.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

## Häufige Fragen & Randfälle

### Was ist, wenn das Bild in einem anderen Format vorliegt (PDF, TIFF usw.)?
Aspose OCR verarbeitet Rasterformate direkt. Für PDFs extrahieren Sie zunächst jede Seite als Bild – Aspose PDF für Java stellt `PdfExtractor` zur effizienten Durchführung bereit. Sobald Sie ein `BufferedImage` oder einen Byte‑Stream haben, funktioniert derselbe `setImage`‑Aufruf. Dieser Ansatz ermöglicht die Verarbeitung von mehrseitigen Dokumenten, ohne das gesamte PDF in den Speicher zu konvertieren, und hält den Arbeitsablauf schnell und skalierbar.

### Wie gehe ich mit mehrseitigen Dokumenten um?
Iterieren Sie über jedes Seitenbild, instanziieren Sie eine neue `OcrEngine` (oder setzen Sie die bestehende zurück) und verketten Sie die Werte von `OcrResult.getText()`. Dieser Ansatz hält die Rechtschreib‑Kontexte pro Seite unabhängig. Durch die Verarbeitung von Seiten sequenziell oder in parallelen Threads können Sie einen hohen Durchsatz beibehalten und gleichzeitig sicherstellen, dass jede Seite von demselben Wörterbuch und denselben Rechtschreibkorrektureinstellungen profitiert.

### Kann ich die Sprache oder den Zeichensatz einschränken?
Ja. Rufen Sie `ocrEngine.getEngineOptions().setLanguage(Language.English)` (oder eine beliebige unterstützte Sprache) auf, um den Erkennungsumfang einzugrenzen, was die Verarbeitung um bis zu **30 %** beschleunigt. Die Einschränkung der Sprache reduziert den Zeichensatz, den die Engine berücksichtigen muss, verringert Mehrdeutigkeiten und verbessert sowohl Geschwindigkeit als auch Genauigkeit, insbesondere bei Dokumenten, die nur lateinische Zeichen enthalten.

### Wie sieht die Leistung bei großen Batches aus?
Die Engine ist für Lese‑Only‑Operationen thread‑sicher. Erstellen Sie einen Thread‑Pool und weisen Sie jedem Bild eine eigene `OcrEngine`‑Instanz zu. Auf einer 4‑Kern‑Maschine können Sie mit paralleler Ausführung **≈250 Seiten/Minute** erreichen. Stellen Sie sicher, dass ausreichend Heap‑Speicher zugewiesen ist, und überwachen Sie die CPU‑Auslastung, um Engpässe bei der Verarbeitung von Tausenden hochauflösender Bilder zu vermeiden.

## Tipps für bessere Genauigkeit

- **Bild vorverarbeiten**: Kontrast erhöhen, Median‑Filter anwenden oder vor OCR in Graustufen konvertieren.
- **Verwenden Sie Scans mit 300 dpi oder höher**; niedrigere Auflösungen erhöhen die Fehlerraten dramatisch.
- **Halten Sie das benutzerdefinierte Wörterbuch fokussiert**: zu viele nicht verwandte Wörter können die Rechtschreibprüfung verwirren.
- **Nachbearbeitung mit Regex**: Validieren Sie nach der Extraktion Daten, Zahlen oder IDs, um verbleibende Anomalien zu erfassen.

## Nächste Schritte

Jetzt, da Sie wissen, **how to perform OCR** auf Bildern und **how to extract text from image** Dateien zu verwenden, könnten Sie erkunden:

- Das OCR‑Ergebnis als durchsuchbares PDF mit einer versteckten Textebene speichern.
- Extrahierte Rechnungsdaten direkt in einer relationalen Datenbank speichern.
- Machine‑Learning‑Modelle anwenden, um handschriftliche Notizen weiter zu bereinigen.
- Den OCR‑Workflow als REST‑Webservice für vom Benutzer hochgeladene Bilder bereitstellen.

Jede dieser Erweiterungen baut auf den oben behandelten Kernschritten auf, sodass Sie den Übergang reibungslos finden werden.

---

**Zuletzt aktualisiert:** 2026-09-23  
**Getestet mit:** Aspose OCR 24.12 für Java  
**Autor:** Aspose  



## Häufig gestellte Fragen

**F: Benötigt Aspose OCR eine Internetverbindung?**  
A: Nein. Die Bibliothek läuft vollständig offline; die gesamte Erkennung erfolgt lokal auf Ihrer JVM.

**F: Welche Java‑Versionen werden unterstützt?**  
A: Aspose OCR unterstützt Java 8 bis Java 21, einschließlich sowohl Standard‑ als auch OpenJDK‑Distributionen.

**F: Kann ich Bilder größer als 10 MB verarbeiten?**  
A: Ja. Die Engine streamt Daten und kann Bilder bis zu 500 MB verarbeiten, nur durch verfügbaren Heap‑Speicher begrenzt.

**F: Wie lizenziere ich Aspose OCR für die Produktion?**  
A: Kaufen Sie eine kommerzielle Lizenz im Aspose‑Store und setzen Sie die Lizenzdatei mit `License license = new License(); license.setLicense("Aspose.OCR.lic");`.

**F: Gibt es integrierte Unterstützung für handgeschriebenen Text?**  
A: Aspose OCR enthält einen Handschrifterkennungs‑Modus, der über `ocrEngine.getEngineOptions().setHandwriting(true);` aktiviert werden kann und die Genauigkeit bei kursiven Schriften verbessert.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you wish to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));

        // Step 3: Enable spell‑checking for the OCR result
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);

        // Step 4: Provide a custom dictionary (one word per line)
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));

        // Step 5: Run the OCR process
        OcrResult ocrResult = ocrEngine.process();

        // Step 6: Output the recognized (and corrected) text
        System.out.println(ocrResult.getText());
    }
}
```

## Verwandte Tutorials

- [OCR auf Bild mit Aspose OCR Java Schritt‑für‑Schritt‑Anleitung](/ocr/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/)
- [Bild‑OCR in Java vorverarbeiten – Genauigkeit steigern, Text extrahieren](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)
- [GPU für OCR in Java aktivieren – Text aus Bild erkennen](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}