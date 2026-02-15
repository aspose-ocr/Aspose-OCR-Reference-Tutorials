---
category: general
date: 2026-02-14
description: Erfahren Sie, wie Sie OCR auf Bildern durchführen und Text aus Bildern
  mit Aspose OCR in Java extrahieren. Enthält das Laden von Bildern für OCR, ein benutzerdefiniertes
  Wörterbuch und Rechtschreibkorrektur.
draft: false
keywords:
- perform OCR on image
- extract text from image
- load image for OCR
- Aspose OCR Java
- spell correction OCR
language: de
og_description: Führen Sie OCR auf einem Bild in Java mit Aspose OCR durch. Dieser
  Leitfaden zeigt, wie man ein Bild für OCR lädt, Text aus dem Bild extrahiert und
  die Rechtschreibkorrektur aktiviert.
og_title: OCR auf Bild ausführen – Komplettes Java‑Tutorial
tags:
- OCR
- Java
- Aspose
title: OCR auf Bild mit Aspose OCR durchführen – Java Schritt‑für‑Schritt‑Anleitung
url: /de/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf Bild – Vollständiges Java‑Tutorial

Haben Sie jemals **OCR auf Bild**‑Dateien durchführen müssen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein; viele Entwickler stoßen beim ersten Versuch, Text aus Bilddaten zu extrahieren, auf dieselbe Hürde. Die gute Nachricht ist, dass Sie mit Aspose OCR für Java zuverlässige Ergebnisse in nur wenigen Codezeilen erzielen können – und die Genauigkeit mit einem benutzerdefinierten Wörterbuch und Rechtschreibprüfung noch weiter steigern können.

In diesem Leitfaden gehen wir alles durch, was Sie wissen müssen: vom Laden des Bildes für OCR, über das Aktivieren der Rechtschreibkorrektur bis hin zum Ausgeben des bereinigten Textes. Am Ende werden Sie in der Lage sein, **OCR auf Bild**‑Assets in Ihren eigenen Java‑Projekten durchzuführen, und Sie sehen außerdem, wie man **Text aus Bild**‑Dateien extrahiert, und das sogar bei verrauschten Scans.

## Was Sie benötigen

- **Java Development Kit (JDK) 8+** – der Code verwendet standardmäßige Java‑APIs.
- **Aspose OCR for Java**‑Bibliothek (Sie können die neueste JAR von der Aspose‑Website oder Maven Central herunterladen).
- Eine Bilddatei (z. B. `invoice.png`), die Sie verarbeiten möchten.
- (Optional) Eine Klartextdatei `custom_dict.txt` mit domänenspezifischen Wörtern, ein Wort pro Zeile.

Das war’s – keine schweren Frameworks, keine externen Dienste. Nur reines Java und die Aspose OCR JAR.

## Schritt 1: Projekt einrichten und Abhängigkeiten importieren

Zuerst erstellen Sie ein neues Maven‑ (oder Gradle‑)Projekt und fügen die Aspose OCR‑Abhängigkeit hinzu. Wenn Sie Maven verwenden, sollte Ihre `pom.xml` folgendes enthalten:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

Wenn Sie die JAR lieber manuell herunterladen, legen Sie sie in Ihren `libs`‑Ordner und fügen sie dem Klassenpfad hinzu.

> **Pro‑Tipp:** Überprüfen Sie stets die Versionsnummer zum Zeitpunkt des Schreibens; neuere Releases können zusätzliche Funktionen wie Sprachpakete einführen.

## Schritt 2: Bild für OCR laden

Der erste eigentliche Codeschritt besteht darin, die OCR‑Engine auf das Bild zu richten, das Sie analysieren möchten. Aspose OCR verwendet einen `ImageStream`‑Wrapper, der aus einer Datei, einem Byte‑Array oder sogar einer URL lesen kann.

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

Beachten Sie, wie wir **Bild für OCR laden** mit einem einzigen Methodenaufruf – keine umständlichen `BufferedImage`‑Gymnastiken nötig. Wenn Ihr Bild in den Ressourcen liegt, ersetzen Sie einfach den Pfad durch `getClass().getResourceAsStream(...)`.

## Schritt 3: Rechtschreibkorrektur aktivieren (optional, aber leistungsstark)

Aspose OCR kann häufige OCR‑Fehler automatisch korrigieren (z. B. „l“ vs. „1“). Diese Funktion zu aktivieren ist so einfach wie das Umschalten eines Flags:

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

Warum das? Stellen Sie sich vor, Sie scannen eine gedruckte Rechnung, bei der die Schrift klein ist und der Scanner störende Punkte einführt. Die Rechtschreibkorrektur wandelt oft „Inv0ice“ wieder in „Invoice“ um, ohne dass Sie zusätzlichen Aufwand haben.

## Schritt 4: Benutzerdefiniertes Wörterbuch bereitstellen (Engine anpassen)

Wenn Sie mit branchenspezifischer Terminologie arbeiten – denken Sie an medizinische Codes, juristisches Fachvokabular oder Produkt‑SKUs – kann ein benutzerdefiniertes Wörterbuch die Genauigkeit dramatisch erhöhen. Das Wörterbuch ist einfach eine Textdatei mit einem Wort pro Zeile.

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

Stellen Sie sicher, dass die Datei UTF‑8‑Kodierung verwendet; andernfalls könnten Sie bei Nicht‑ASCII‑Wörtern unlesbare Zeichen sehen.

## Schritt 5: OCR‑Prozess ausführen

Jetzt lassen wir die Engine endlich ihre Magie wirken. Der Aufruf `process()` gibt ein `OcrResult`‑Objekt zurück, das den erkannten Text, Vertrauenswerte und sogar das Layout enthält, falls Sie es später benötigen.

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

Falls Sie sich jemals fragen, ob die Engine eine Ausnahme geworfen hat, umschließen Sie diesen Aufruf in einem try‑catch‑Block und prüfen Sie `ocrResult.getErrorMessage()` für Details.

## Schritt 6: Erkannten (und korrigierten) Text ausgeben

Der letzte Schritt besteht darin, die extrahierte Zeichenkette anzuzeigen – oder zu speichern. Für eine schnelle Demo geben wir sie einfach in der Konsole aus:

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

Das Ausführen des Programms sollte etwa Folgendes ausgeben:

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

Wenn Sie fremde Zeichen sehen, überprüfen Sie Ihr benutzerdefiniertes Wörterbuch erneut und überlegen Sie, die Bildqualität anzupassen (z. B. den Kontrast erhöhen, bevor Sie es an die Engine übergeben).

### Vollständiges funktionierendes Beispiel

Alles zusammengeführt, hier ist die komplette, sofort ausführbare Klasse:

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

Speichern Sie diese Datei als `SpellCorrectDemo.java`, passen Sie die Pfade an, kompilieren Sie mit `javac` und führen Sie sie mit `java SpellCorrectDemo` aus. Sie sollten nun **OCR auf Bild**‑Dateien durchführen können und den extrahierten Text ausgegeben sehen.

## Häufige Fragen & Sonderfälle

### Was ist, wenn das Bild in einem anderen Format vorliegt (PDF, TIFF usw.)?

Aspose OCR kann viele Rasterformate sofort verarbeiten. Für PDFs müssen Sie zunächst jede Seite als Bild extrahieren – Aspose PDF für Java erledigt das gut. Der gleiche `setImage`‑Aufruf funktioniert, sobald Sie ein `BufferedImage` oder einen Byte‑Stream haben.

### Wie gehe ich mit mehrseitigen Dokumenten um?

Iterieren Sie über jedes Seitenbild, führen Sie die OCR‑Schritte aus und verketten Sie die Ergebnisse. Denken Sie daran, für jede Seite die `OcrEngine` zurückzusetzen oder neu zu erstellen, wenn Sie unabhängige Rechtschreib‑Kontexte wünschen.

### Kann ich die Sprache oder den Zeichensatz einschränken?

Ja. Verwenden Sie `ocrEngine.getEngineOptions().setLanguage(Language.English);` (oder eine andere unterstützte Sprache), um Fehlalarme zu reduzieren und die Verarbeitung zu beschleunigen.

### Wie sieht es mit der Leistung bei großen Stapeln aus?

Aspose OCR ist für reine Lesevorgänge thread‑sicher. Sie können einen Thread‑Pool starten und Bilder gleichzeitig verarbeiten – vermeiden Sie jedoch, dieselbe `OcrEngine`‑Instanz über mehrere Threads zu teilen.

## Tipps für bessere Genauigkeit

- **Bild vorverarbeiten**: Kontrast erhöhen, Hintergrundgeräusche entfernen oder in Graustufen konvertieren.
- **Hochauflösenden Scan verwenden** (300 dpi oder höher). Niedrigere Auflösungen erzeugen oft unlesbare Zeichen.
- **Benutzerdefiniertes Wörterbuch schlank halten**: zu viele unverwandte Wörter können die Rechtschreibprüfung verwirren.
- **Ausgabe validieren**: Wenn Sie das erwartete Format kennen (z. B. Daten, Zahlen), führen Sie nachträglich ein Regex‑Post‑Processing durch, um Anomalien zu erkennen.

## Nächste Schritte

Jetzt, da Sie **OCR auf Bild**‑Dateien durchführen und **Text aus Bild** extrahieren können mit Aspose OCR, möchten Sie vielleicht Folgendes erkunden:

- **Speichern der OCR‑Ausgabe in ein PDF** mit durchsuchbaren Textebenen.
- **Integration mit einer Datenbank**, um extrahierte Rechnungsdaten automatisch zu speichern.
- **Anwenden von Machine‑Learning‑Post‑Processing** für noch höhere Genauigkeit bei handschriftlichen Notizen.
- **Verwendung des `load image for OCR`‑Flags** in einem Webservice, der vom Benutzer hochgeladene Bilder akzeptiert.

Jedes dieser Themen baut auf den Kernschritten auf, die wir behandelt haben, sodass Sie den Übergang reibungslos finden werden.

---

*Viel Spaß beim Coden! Wenn Sie auf Probleme stoßen, hinterlassen Sie gerne einen Kommentar – nichts geht über das Lernen an realen Beispielen.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}