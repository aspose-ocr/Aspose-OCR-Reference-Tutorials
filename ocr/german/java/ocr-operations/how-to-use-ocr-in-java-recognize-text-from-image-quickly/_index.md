---
category: general
date: 2026-02-17
description: Erfahren Sie, wie Sie OCR in Java verwenden, um Text aus Bilddateien
  zu erkennen, Text aus PNG‑Quittungen zu extrahieren und Quittungen mit Aspose OCR
  in JSON zu konvertieren.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from png
- convert receipt to json
language: de
og_description: Schritt‑für‑Schritt‑Anleitung, wie man OCR in Java verwendet, um Text
  aus Bildern zu erkennen, Text aus PNG‑Belegen zu extrahieren und den Beleg in JSON
  zu konvertieren.
og_title: Wie man OCR in Java verwendet – Text aus Bild erkennen
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Wie man OCR in Java verwendet – Text schnell aus Bildern erkennen
url: /de/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/
---

:

Ever wondered **how to use OCR** to pull text out of a photo ... translate.

We'll translate.

Make sure to keep bold formatting.

Proceed.

Will produce final output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in Java verwendet – Text schnell aus Bild erkennen

Haben Sie sich schon einmal gefragt, **wie man OCR** nutzt, um Text aus einem Foto eines Kassenbons zu extrahieren? Vielleicht haben Sie ein paar Online‑Tools ausprobiert, nur um am Ende verzerrte Zeichen oder ein nicht auswertbares Format zu erhalten. Die gute Nachricht: Mit nur wenigen Zeilen Java‑Code können Sie **Text aus Bild**‑Dateien **erkennen**, **Text aus PNG**‑Belegen **extrahieren** und sogar **Beleg in JSON** konvertieren für die nachgelagerte Verarbeitung.

In diesem Tutorial führen wir Sie durch den kompletten Workflow – von der Lizenzierung der Aspose OCR‑Bibliothek bis hin zum sauberen JSON‑Payload, das Sie in eine Datenbank oder ein Machine‑Learning‑Modell einspeisen können. Kein Schnickschnack, nur ein praktisches, ausführbares Beispiel, das Sie in Ihre IDE kopieren‑und‑einfügen können. Am Ende haben Sie ein eigenständiges Programm, das `receipt.png` einliest und einen sofort einsetzbaren JSON‑String ausgibt.

## Was Sie benötigen

- **Java Development Kit (JDK) 8+** – jede aktuelle Version funktioniert.
- **Aspose OCR for Java**‑Bibliothek (das Maven‑Artifact lautet `com.aspose:aspose-ocr`).
- Eine **gültige Aspose OCR‑Lizenzdatei** (`Aspose.OCR.lic`). Die kostenlose Testversion reicht für Tests, aber eine richtige Lizenz entfernt Evaluations‑Beschränkungen.
- Eine Bilddatei (PNG, JPEG usw.), die den zu lesenden Text enthält – nennen wir sie `receipt.png` und legen sie in einem bekannten Ordner ab.
- Ihre bevorzugte IDE (IntelliJ IDEA, Eclipse, VS Code …) – Sie können wählen, was Ihnen gefällt.

> **Pro‑Tipp:** Bewahren Sie Ihre Lizenzdatei außerhalb des Quellordners auf und referenzieren Sie sie über einen absoluten oder relativen Pfad, um zu vermeiden, dass sie in die Versionskontrolle gelangt.

Jetzt, wo die Voraussetzungen klar sind, tauchen wir in den eigentlichen Code ein.

## Wie man OCR verwendet – Kernschritte

Im Folgenden ein Überblick über die Aktionen, die wir ausführen werden:

1. **Laden der Aspose OCR‑Bibliothek** und Anwenden Ihrer Lizenz.  
2. **Erstellen einer `OcrEngine`‑Instanz** – das ist die Engine, die die eigentliche Arbeit erledigt.  
3. **Vorbereiten eines `OcrInput`‑Objekts**, das auf das zu verarbeitende Bild zeigt.  
4. **Aufruf von `recognize` mit `ResultFormat.JSON`**, um eine JSON‑Darstellung des extrahierten Textes zu erhalten.  
5. **Verarbeiten der JSON‑Ausgabe** – ausgeben, in eine Datei schreiben oder weiterparsen.

Jeder Schritt wird in den nachfolgenden Abschnitten detailliert erklärt.

## Schritt 1 – Aspose OCR installieren und Lizenz anwenden

Fügen Sie zunächst die Aspose OCR‑Abhängigkeit zu Ihrer `pom.xml` hinzu, wenn Sie Maven verwenden:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Laden Sie nun in Ihrem Java‑Code die Lizenz. Dieser Schritt ist essenziell; ohne Lizenz läuft die Bibliothek im Evaluationsmodus und kann Wasserzeichen in die Ausgabe einbetten.

```java
import com.aspose.ocr.*;

public class OcrSetup {
    public static void applyLicense() throws Exception {
        // Replace the path with the actual location of your Aspose.OCR.lic file
        License ocrLicense = new License();
        ocrLicense.setLicense("C:/licenses/Aspose.OCR.lic");
    }
}
```

> **Warum das wichtig ist:** Das `License`‑Objekt teilt der OCR‑Engine mit, dass Sie berechtigt sind, das volle Funktionsspektrum zu nutzen, einschließlich hochpräziser Erkennung und JSON‑Export. Wird dieser Schritt übersprungen, können Sie weiterhin **Text aus Bild** erkennen, aber die Ergebnisse können gedrosselt sein.

## Schritt 2 – OCR‑Engine‑Instanz erstellen

Die Klasse `OcrEngine` ist der Einstiegspunkt für alle OCR‑Operationen. Denken Sie an sie als das „Gehirn“, das die Pixel liest und entscheidet, welche Zeichen sie darstellen.

```java
import com.aspose.ocr.*;

public class OcrEngineFactory {
    public static OcrEngine createEngine() {
        // No special configuration needed for basic usage
        return new OcrEngine();
    }
}
```

Sie können die Engine später anpassen (z. B. Sprache setzen, Deskew aktivieren), falls Ihre Belege nicht‑lateinische Schriften enthalten oder schräg gescannt wurden. Für die meisten US‑basierten Belege funktionieren die Standardeinstellungen einwandfrei.

## Schritt 3 – Bild laden, das verarbeitet werden soll

Jetzt weisen wir die OCR‑Engine auf die Datei, die den Beleg enthält. Die Klasse `OcrInput` kann mehrere Bilder aufnehmen, aber für dieses Tutorial halten wir es bei einem einzigen PNG einfach.

```java
import com.aspose.ocr.*;

public class ImageLoader {
    public static OcrInput loadImage(String imagePath) {
        OcrInput input = new OcrInput();
        // Add the PNG receipt – this is where we **extract text from PNG**
        input.add(imagePath);
        return input;
    }
}
```

Falls Sie jemals **Text aus PNG**‑Dateien massenhaft **extrahieren** müssen, rufen Sie einfach wiederholt `input.add()` auf oder übergeben Sie eine Liste von Dateipfaden.

## Schritt 4 – Text erkennen und Beleg in JSON konvertieren

Hier kommt das Herzstück des Tutorials. Wir lassen die Engine den Text erkennen und fordern das Ergebnis im JSON‑Format an. Das Flag `ResultFormat.JSON` erledigt die schwere Arbeit für uns.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonRecognizer {
    public static String recognizeToJson(OcrEngine engine, OcrInput input) throws Exception {
        // Perform OCR and request JSON output
        OcrResult result = engine.recognize(input, ResultFormat.JSON);
        // Retrieve the JSON string
        return result.getJson();
    }
}
```

Das JSON‑Payload enthält jede erkannte Zeile, deren Begrenzungsrahmen, den Vertrauenswert und den Rohtext. Diese Struktur macht es trivial, **Beleg in JSON** zu konvertieren und anschließend in jede nachgelagerte API zu speisen.

## Schritt 5 – Alles zusammenfügen und das Programm ausführen

Unten finden Sie die komplette, sofort ausführbare Java‑Klasse, die alles zusammenbringt. Speichern Sie sie als `JsonExportDemo.java` (oder wie Sie möchten) und führen Sie sie in Ihrer IDE oder über die Kommandozeile aus.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonExportDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license (replace with your actual license file)
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.lic"); // <-- adjust path if needed

        // 2️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Prepare the input image that contains the text to be recognized
        OcrInput ocrInput = new OcrInput();
        // Replace with the absolute or relative path to your receipt PNG
        ocrInput.add("YOUR_DIRECTORY/receipt.png"); // <-- **extract text from PNG** here

        // 4️⃣ Perform recognition and request the result in JSON format
        OcrResult ocrResult = ocrEngine.recognize(ocrInput, ResultFormat.JSON);

        // 5️⃣ Retrieve the JSON string from the result
        String jsonResult = ocrResult.getJson();

        // 6️⃣ Output the JSON (or save it to a file for further processing)
        System.out.println(jsonResult);
    }
}
```

### Erwartete Ausgabe

Beim Ausführen des Programms wird ein JSON‑String ähnlich dem folgenden ausgegeben (der genaue Inhalt hängt von Ihrem Beleg ab):

```json
{
  "pages": [
    {
      "lines": [
        {
          "text": "Store Name",
          "confidence": 0.99,
          "boundingBox": [12, 34, 200, 45]
        },
        {
          "text": "Date: 2024-02-15",
          "confidence": 0.98,
          "boundingBox": [12, 60, 180, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.97,
          "boundingBox": [12, 120, 150, 45]
        }
      ]
    }
  ]
}
```

Sie können dieses JSON nun in eine Datenbank, einen REST‑Endpoint oder eine Datenanalyse‑Pipeline einspeisen. Der **Beleg‑zu‑JSON**‑Schritt ist bereits für Sie erledigt.

## Häufige Fragen und Sonderfälle

### Was, wenn das Bild gedreht ist?

Aspose OCR erkennt und korrigiert leichte Rotationen automatisch. Bei stark verzerrten Bildern rufen Sie vor der Erkennung `engine.getImagePreprocessingOptions().setDeskew(true)` auf.

### Wie gehe ich mit mehreren Sprachen um?

Verwenden Sie `engine.getLanguage()`, um die gewünschte Sprache zu setzen, z. B. `engine.setLanguage(Language.FRENCH)`. Das ist praktisch, wenn Sie **Text aus Bild** erkennen müssen, das mehrsprachige Belege enthält.

### Kann ich reinen Text statt JSON ausgeben?

Natürlich. Ersetzen Sie `ResultFormat.JSON` durch `ResultFormat.TEXT` und rufen Sie `result.getText()` auf.

### Gibt es eine Möglichkeit, die OCR auf einen bestimmten Bereich zu beschränken?

Ja – nutzen Sie `ocrInput.add(imagePath, new Rectangle(x, y, width, height))`, um sich auf den Beleg‑Bereich zu fokussieren. Das kann Geschwindigkeit und Genauigkeit verbessern.

## Pro‑Tipps für produktionsreifes OCR

- **Lizenz‑Objekt cachen**, wenn Sie viele Dateien in einer Schleife verarbeiten; das wiederholte Erzeugen verursacht Overhead.
- **Batch‑Verarbeitung**: Laden Sie alle Beleg‑Pfade in ein einziges `OcrInput` und rufen Sie einmal `recognize` auf. Das JSON enthält dann ein Array von Seiten, jede mit ihren Zeilen.
- **JSON validieren**: Parsen Sie den String nach dem Erhalt mit einer Bibliothek wie Jackson, um sicherzustellen, dass er wohlgeformt ist, bevor Sie ihn speichern.
- **Vertrauenswerte überwachen**: Das JSON enthält ein Feld `confidence` pro Zeile. Filtern Sie Zeilen unter einem Schwellenwert (z. B. 0,85) heraus, um Mülldaten zu vermeiden.
- **Lizenz sichern**: Lagern Sie `Aspose.OCR.lic` in einem sicheren Tresor oder einer Umgebungsvariable, besonders bei Cloud‑Deployments.

## Fazit

Wir haben behandelt, **wie man OCR** in Java nutzt, um **Text aus Bild** zu **erkennen**, **Text aus PNG**‑Belegen zu **extrahieren** und **Beleg in JSON** zu **konvertieren** – alles mit einem knappen, End‑to‑End‑Beispiel. Die Schritte sind unkompliziert, der Code vollständig ausführbar, und die JSON‑Ausgabe liefert Ihnen eine strukturierte Darstellung, die für jedes nachgelagerte System bereitsteht.

Als Nächstes könnten Sie fortgeschrittene Szenarien erkunden: das JSON in Apache Kafka für Echtzeit‑Verarbeitung einspeisen, Regex‑Muster anwenden, um Zeilen‑Summen herauszufiltern, oder eine Cloud‑OCR‑Service‑Lösung für Skalierbarkeit integrieren. Was immer Sie wählen, die Grundlagen, die Sie gerade gelernt haben, bleiben gleich.

Haben Sie Fragen oder sind Sie beim Ausprobieren auf ein Problem gestoßen? Hinterlassen Sie einen Kommentar unten, und wir helfen gern beim Troubleshooting. Viel Spaß beim Coden und beim Umwandeln dieser unordentlichen Beleg‑Bilder in saubere, durchsuchbare Daten!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}