---
category: general
date: 2026-04-29
description: Text aus Bild in Java mit Aspose OCR extrahieren – lernen Sie, wie Sie
  ein Bild für OCR laden und Text von einer Quittung im JSON-Format erkennen.
draft: false
keywords:
- extract text from image java
- load image for OCR
- recognize text from receipt
- Aspose OCR Java
- JSON OCR result
language: de
og_description: Text aus Bild mit Java und Aspose OCR extrahieren. Dieses Tutorial
  zeigt, wie man ein Bild für OCR lädt und Text von einer Quittung erkennt, wobei
  JSON ausgegeben wird.
og_title: Text aus Bild mit Java extrahieren – Vollständige Anleitung
tags:
- Java
- OCR
- Aspose
title: Text aus Bild extrahieren Java – Bild für OCR laden
url: /de/java/ocr-operations/extract-text-from-image-java-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild mit Java extrahieren – Vollständiger Leitfaden

Haben Sie jemals **extract text from image java** benötigt, wussten aber nicht, welche Bibliothek Sie wählen sollten? Sie sind nicht allein. Viele Entwickler stoßen an Grenzen, wenn sie versuchen, ein Bild für OCR zu laden und dann den Rohtext in einem schwer zu verarbeitenden Format erhalten.  

In diesem Tutorial führen wir Sie durch eine saubere End‑to‑End‑Lösung, die nicht nur **load image for OCR** ermöglicht, sondern auch **recognize text from receipt** und einen aufgeräumten JSON‑String ausgibt. Am Ende haben Sie eine einsatzbereite Java‑Klasse, die Sie in jedes Projekt einbinden können – ohne zusätzlichen Aufwand.

## Was Sie lernen werden

- Wie Sie Aspose OCR für Java einrichten (die Bibliothek, die das schwere Heben mühelos macht).  
- Die genauen Schritte, um **load image for OCR** von der Festplatte zu laden.  
- Wie Sie die Engine konfigurieren, damit sie Ergebnisse im JSON‑Format zurückgibt, was sich perfekt für die nachgelagerte Verarbeitung eignet.  
- Wie Sie **recognize text from receipt**‑Bilder erkennen und die Ausgabe überprüfen.  

Vorkenntnisse mit Aspose sind nicht erforderlich; Sie benötigen lediglich ein funktionierendes JDK und eine IDE, mit der Sie vertraut sind.

## Voraussetzungen

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| **Java 17+** (or any recent JDK) | Aspose OCR wird mit kompilierten Binärdateien für moderne Java‑Runtime‑Umgebungen geliefert. |
| **Maven or Gradle** (to pull the Aspose OCR dependency) | Erleichtert das Verwalten von Abhängigkeiten enorm. |
| **A sample receipt image** (e.g., `receipt.png`) | Wir verwenden diese Datei, um **recognize text from receipt** zu demonstrieren. |
| **Internet connection** (once) | Erforderlich, um das Aspose‑JAR beim ersten Mal herunterzuladen. |

Wenn Sie das bereits haben, großartig – lassen Sie uns loslegen.

## Schritt 1: Aspose OCR zu Ihrem Projekt hinzufügen

Das Erste, was Sie benötigen, ist die Aspose OCR‑Bibliothek. Wenn Sie Maven verwenden, fügen Sie den folgenden Ausschnitt zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

Für Gradle sieht es so aus:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Profi‑Tipp:** Sperren Sie die Versionsnummer. Ein späteres Upgrade kann subtile API‑Änderungen einführen, die Ihren Code brechen.

Sobald die Abhängigkeit aufgelöst ist, können Sie Java‑Code schreiben, der tatsächlich **extract text from image java**.

## Schritt 2: Bild für OCR laden

Jetzt zeigen wir die genaue Zeile, die **load image for OCR** ausführt. Aspose stellt einen praktischen Helfer `ImageStream.fromFile` bereit.

```java
// Step 2: Load the image you want to process
ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

Ersetzen Sie `YOUR_DIRECTORY` durch den absoluten oder relativen Pfad zu Ihrer Belegdatei. Ist der Pfad falsch, wirft die Engine eine `FileNotFoundException`, also überprüfen Sie die Schreibweise doppelt.

> **Warum das wichtig ist:** Das korrekte Laden des Bildes ist die Grundlage. Wenn das Bild nicht gelesen wird, hat die OCR‑Engine nichts zu erkennen und Sie erhalten ein leeres JSON‑Ergebnis.

## Schritt 3: Der Engine mitteilen, JSON zurückzugeben

Aspose OCR kann XML, Klartext oder JSON ausgeben. Für moderne APIs ist JSON am flexibelsten, daher setzen wir das Format explizit.

```java
ocrEngine.getResultSettings()
         .setResultFormat(OcrResultFormat.JSON); // XML is also available
```

Sie könnten mit einer einzigen Änderung zu `OcrResultFormat.XML` wechseln, falls Ihr nachgelagertes System XML bevorzugt. Die API ist dafür ausgelegt, austauschbar zu sein.

## Schritt 4: Erkennungsprozess ausführen

Nachdem das Bild geladen und das Format gesetzt ist, ist der nächste Schritt, tatsächlich **recognize text from receipt** auszuführen. Hier findet das schwere Heben statt.

```java
// Step 4: Perform OCR
OcrResult ocrResult = ocrEngine.recognize();
```

Der Aufruf `recognize()` blockiert, bis die Engine die Bildanalyse abgeschlossen hat. Bei großen Bildern möchten Sie dies möglicherweise in einem Hintergrund‑Thread ausführen, aber für einen typischen Beleg ist es in einem Bruchteil einer Sekunde erledigt.

## Schritt 5: Das JSON‑Ergebnis holen

Schließlich extrahieren wir den rohen JSON‑String und geben ihn aus. Dieser String enthält jedes erkannte Textstück, dessen Begrenzungsrahmen, Konfidenzwerte und mehr.

```java
// Step 5: Retrieve the JSON string
String jsonResult = ocrResult.getResultAsString();
System.out.println(jsonResult);
```

### Erwartete Ausgabe

Das Ausführen des vollständigen Programms mit einem klaren Beleg liefert etwa Folgendes:

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "rectangle": { "x": 12, "y": 15, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2026-04-28",
          "confidence": 0.95,
          "rectangle": { "x": 12, "y": 50, "width": 180, "height": 20 }
        },
        {
          "text": "Total $23.45",
          "confidence": 0.99,
          "rectangle": { "x": 12, "y": 120, "width": 150, "height": 25 }
        }
      ]
    }
  ]
}
```

Beachten Sie, dass jede Zeile des Belegs ein separates Block mit einem Konfidenzwert ist. Sie können dieses JSON nun in jedes nachgelagerte System einspeisen – in einer Datenbank speichern, über HTTP senden oder an ein Machine‑Learning‑Modell weitergeben.

## Vollständiges funktionierendes Beispiel

Unten finden Sie die komplette, eigenständige Java‑Klasse, die alles zusammenführt. Kopieren Sie sie, passen Sie den Bildpfad an und führen Sie `mvn compile exec:java` aus (oder den entsprechenden Gradle‑Befehl).

```java
import com.aspose.ocr.*;

public class JsonExportExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Make sure the path points to a real receipt image on your machine
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Configure the engine to return results in JSON format
        ocrEngine.getResultSettings()
                 .setResultFormat(OcrResultFormat.JSON); // XML is also available

        // Step 4: Run the OCR recognition process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Retrieve the raw JSON string and output it
        String jsonResult = ocrResult.getResultAsString();
        System.out.println(jsonResult);
    }
}
```

> **Achten Sie auf:**  
> • **Dateipfad‑Fehler** – prüfen Sie die Schrägstriche unter Windows vs. macOS/Linux.  
> • **Speicher‑Ausnahme** – große Bilder benötigen möglicherweise `ocrEngine.setMemoryOptimization(true)`.  
> • **Spracheinstellungen** – enthält Ihr Beleg nicht‑lateinische Zeichen, rufen Sie `ocrEngine.setLanguage(OcrLanguage.SPANISH)` (oder eine andere unterstützte Sprache) vor `recognize()` auf.

## Lösung testen

1. **Programm ausführen** – Sie sollten ein JSON‑Blob in der Konsole sehen.  
2. **JSON validieren** – kopieren Sie die Ausgabe zu <https://jsonlint.com/>, um sicherzustellen, dass sie wohlgeformt ist.  
3. **Parsen** – in einem realen Projekt würden Sie eine Bibliothek wie Jackson oder Gson verwenden, um das JSON in POJOs zu überführen für einfachere Handhabung.

Wenn Sie ein leeres `pages`‑Array erhalten, sind die häufigsten Ursachen: Die Bilddatei wurde nicht gefunden oder das Bild ist für die Standardeinstellungen der Engine zu unscharf. Im letzteren Fall versuchen Sie, die DPI zu erhöhen oder einen Vorverarbeitungsschritt (z. B. Binärisierung) anzuwenden, bevor Sie es an Aspose übergeben.

## Variationen & Sonderfälle

| Szenario | Was zu ändern ist |
|----------|-------------------|
| **Multiple pages** (e.g., multi‑page PDF converted to images) | Iterieren Sie über jedes Bild, rufen Sie `ocrEngine.setImage(...)` innerhalb der Schleife auf und aggregieren Sie die JSON‑Ergebnisse. |
| **Different output format** | Ersetzen Sie `OcrResultFormat.JSON` durch `OcrResultFormat.XML` oder `OcrResultFormat.PLAIN_TEXT`. |
| **Performance tuning** | Verwenden Sie `ocrEngine.setRecognitionMode(OcrRecognitionMode.FAST)` für Geschwindigkeit oder `OcrRecognitionMode.ACCURATE` für Qualität. |
| **Non‑receipt documents** | Passen Sie `ocrEngine.getPageSegmentationSettings().setDetectTables(true)` an, falls Sie Tabellenerkennung benötigen. |

Diese Anpassungen ermöglichen es Ihnen, den Kern‑Workflow **extract text from image java** an ein breites Spektrum realer Probleme anzupassen.

## Fazit

Wir haben gerade einen kompakten, produktionsbereiten Weg vorgestellt, um **extract text from image java** mit Aspose OCR zu realisieren. Indem Sie die fünf Schritte befolgen – Engine erstellen, **load image for OCR**, JSON‑Ausgabe setzen, **recognize text from receipt** und schließlich das JSON lesen – können Sie OCR in jedes Java‑Backend mit minimalem Aufwand integrieren.

Ab hier könnten Sie folgendes tun:

- Das JSON in einer NoSQL‑Datenbank für spätere Analysen speichern.  
- Das Ergebnis an einen Chatbot weiterleiten, der Fragen zu Belegen beantwortet.  
- Dies mit Apache Tika kombinieren, um PDFs, DOCX und andere Formate zu verarbeiten.

Probieren Sie es aus, passen Sie die Einstellungen an Ihre spezifischen Dokumente an und lassen Sie die Maschine das schwere Heben erledigen, während Sie sich auf den Mehrwert konzentrieren.

---

![extract text from image java](placeholder-image.png "extract text from image java")

*Abbildung: Visuelle Darstellung der OCR‑Pipeline – vom Bilddatei zum JSON‑Ausgabe.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}