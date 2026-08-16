---
category: general
date: 2026-03-28
description: Führen Sie OCR auf einem Bild in Java mit Aspose OCR aus, um das Bild
  in Text zu konvertieren, und extrahieren Sie thailändischen Text aus PNG schnell
  und zuverlässig.
draft: false
keywords:
- run OCR on image
- convert image to text
- extract text from PNG
- extract Thai text
- recognize Thai text
language: de
og_description: Führen Sie OCR auf einem Bild mit Java und Aspose OCR durch. Erfahren
  Sie, wie Sie ein Bild in Text umwandeln, thailändischen Text aus einer PNG extrahieren
  und gängige Fallstricke vermeiden.
og_title: OCR auf Bild mit Java ausführen – Thai‑Text schnell extrahieren
tags:
- OCR
- Java
- Aspose
- Image Processing
title: OCR auf Bild mit Java ausführen – Thailändischen Text aus PNG extrahieren
url: /de/java/ocr-operations/run-ocr-on-image-with-java-extract-thai-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf Bild mit Java ausführen – Vollständiges Tutorial

Haben Sie sich schon einmal gefragt, wie man **OCR auf Bild**‑Dateien direkt aus Java‑Code ausführt? Vielleicht haben Sie eine Sammlung thailändischer Quittungen, gescannte Dokumente oder Screenshots und benötigen den Text, ohne ihn manuell abzutippen. Das ist ein häufiges Problem, besonders wenn die Quelle ein PNG ist und die Sprache nicht‑lateinisch ist.  

In diesem Leitfaden zeigen wir Ihnen genau, wie Sie **OCR auf Bild** mit der Aspose OCR‑Bibliothek ausführen, das Bild in Klartext umwandeln und thailändische Zeichen zuverlässig extrahieren. Am Ende können Sie **Bild in Text konvertieren**, **Text aus PNG extrahieren** und sogar **thailändischen Text erkennen** – mit nur wenigen Code‑Zeilen.

## Was dieses Tutorial behandelt

* Einrichten der Aspose OCR‑Abhängigkeit in einem Maven/Gradle‑Projekt.  
* Initialisieren des `OcrEngine` und Konfigurieren für die thailändische Sprache.  
* Ausführen von OCR auf einer PNG‑Datei und Umgang mit möglichen Fehlern.  
* Ausgabe des Ergebnisses in der Konsole und Überprüfung der Ausgabe.  

Vorkenntnisse mit Aspose sind nicht erforderlich – ein einfaches Java‑IDE und eine Bilddatei, die Sie verarbeiten möchten, reichen aus.

## Voraussetzungen

* Java 8 oder neuer installiert (die Bibliothek funktioniert auch mit Java 11+).  
* Ein Build‑Tool – Maven oder Gradle (wir zeigen das Maven‑Snippet).  
* Eine Aspose OCR‑Lizenz (die kostenlose Testversion reicht zum Ausprobieren, aber eine Lizenz entfernt die Evaluations‑Beschränkungen).  
* Ein PNG, das thailändischen Text enthält, z. B. `input.png` im Ressourcen‑Ordner Ihres Projekts.

---

## Schritt 1: Aspose OCR zu Ihrem Projekt hinzufügen

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version -->
</dependency>
```

### Gradle (Kotlin DSL)

```kotlin
implementation("com.aspose:aspose-ocr:23.9")
```

> **Pro‑Tipp:** Halten Sie die Bibliotheks‑Version synchron mit den offiziellen Aspose‑Release‑Notes; neuere Versionen fügen Sprachpakete und Leistungsverbesserungen hinzu.

Sobald die Abhängigkeit aufgelöst ist, sollte Ihr IDE die benötigten Klassen automatisch importieren.

## Schritt 2: Die OCR‑Engine initialisieren

Die Engine ist das Herzstück des Prozesses – denken Sie an sie als das „Gehirn“, das Pixelmuster analysiert. Wir teilen ihr außerdem mit, dass wir nur an thailändischen Zeichen interessiert sind.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Tell the engine to look for Thai language patterns
        ocrEngine.getRecognitionSettings().setLanguage("th");
```

Warum die Sprache explizit setzen? Weil die Angabe von `"th"` den Zeichensatz einschränkt, was die Erkennung beschleunigt und Fehlinterpretationen ähnlicher Glyphen reduziert.

## Schritt 3: OCR auf der PNG‑Datei ausführen

Jetzt übergeben wir der Engine das Bild, das wir dekodieren wollen. Die Methode `recognizeImage` liefert ein `OcrResult`‑Objekt, das den extrahierten String und Konfidenzwerte enthält.

```java
        // Step 3: Perform OCR on the target image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

Falls die Datei nicht gefunden wird, wirft Aspose eine `FileNotFoundException`. Es ist ratsam, den Aufruf in Produktionscode in einen `try‑catch`‑Block zu packen, aber für dieses Tutorial halten wir es einfach.

## Schritt 4: Erkannten Text ausgeben

Abschließend geben wir das Ergebnis aus. Die Methode `getText()` liefert einen normalen Java‑`String`, den Sie speichern, über ein Netzwerk senden oder in eine Datei schreiben können.

```java
        // Step 4: Display the extracted Thai text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Wenn Sie das Programm ausführen, sollte etwas Ähnliches erscheinen:

```
=== Recognized Thai Text ===
สวัสดีครับ นี่คือข้อความจากรูปภาพ
```

Sieht die Ausgabe verzerrt aus, prüfen Sie, ob das Quell‑PNG hochauflösend ist (mindestens 300 dpi) und ob der Sprachcode `"th"` Ihrer Zielsprache entspricht.

### Vollständiges Listing

Unten finden Sie die komplette, sofort ausführbare Java‑Datei. Kopieren Sie sie in Ihr IDE, passen Sie ggf. den Bildpfad an und klicken Sie auf **Run**.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Select Thai language for recognition
        ocrEngine.getRecognitionSettings().setLanguage("th");

        // Run OCR on the PNG image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // Output the recognized text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

![Beispiel für OCR auf Bild](image.png "Beispiel für OCR auf Bild – Java-Code, der thailändischen Text aus PNG extrahiert")

## Schritt 5: Häufige Varianten & Sonderfälle

### Bild in Text in anderen Formaten konvertieren

Wenn Sie **Bild in Text** für ein JPEG oder BMP **konvertieren** möchten, ändern Sie einfach die Dateierweiterung in `imagePath`. Aspose OCR unterstützt PNG, JPEG, BMP, TIFF und sogar PDF‑Seiten.

### Text aus PNG mit mehreren Sprachen extrahieren

Sie können die Engine anweisen, mehrere Sprachen gleichzeitig zu erkennen:

```java
ocrEngine.getRecognitionSettings().setLanguage("th,en");
```

Das Ergebnis enthält dann eine Mischung aus thailändischen und englischen Zeichen – praktisch für zweisprachige Quittungen.

### Umgang mit Bildern niedriger Qualität

Für unscharfe Scans sollten Sie die Vorverarbeitung aktivieren:

```java
ocrEngine.getRecognitionSettings().setPreprocessMode(PreprocessMode.Auto);
```

Damit werden eingebaute Rausch‑ und Kontrast‑Verbesserungs‑Algorithmen ausgelöst, was den Schritt **Text aus PNG extrahieren** verbessert.

### Lizenzaktivierung

Ohne Lizenz fügt Aspose nach 100 Seiten eine Wasserzeichen‑Zeile in die Ausgabe ein. Aktivieren Sie Ihre Lizenz frühzeitig:

```java
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

Platzieren Sie die `.lic`‑Datei neben Ihrer JAR oder referenzieren Sie sie über einen absoluten Pfad.

## Häufig gestellte Fragen

**F: Funktioniert das unter Linux?**  
A: Absolut. Aspose OCR ist reines Java, daher läuft es auf jedem JVM‑kompatiblen Betriebssystem.

**F: Was, wenn das PNG handschriftliches Thai enthält?**  
A: Handschriftliche Erkennung ist eingeschränkt; Sie benötigen eventuell ein spezielles neuronales Netzwerk‑Modell. Aspose OCR glänzt bei gedrucktem Text.

**F: Kann ich einen Ordner mit Bildern stapelweise verarbeiten?**  
A: Verpacken Sie den Aufruf von `recognizeImage` in eine Schleife über `Files.list(Paths.get("folder"))`. Denken Sie daran, dieselbe `OcrEngine`‑Instanz für bessere Performance wiederzuverwenden.

## Fazit

Wir haben ein vollständiges, End‑to‑End‑Beispiel durchgegangen, wie man **OCR auf Bild**‑Dateien in Java ausführt, speziell um **thailändischen Text** aus einem PNG zu **extrahieren**. Durch Initialisieren des `OcrEngine`, Setzen der Sprache, Aufrufen von `recognizeImage` und Ausgeben des Ergebnisses haben Sie nun eine zuverlässige Methode, **Bild in Text zu konvertieren**, ohne Drittanbieter‑Dienste zu nutzen.

Von hier aus können Sie:

* **Text aus PNG**‑Dateien massenhaft für Data‑Mining‑Projekte **extrahieren**.  
* Die OCR‑Ausgabe mit einer Übersetzungs‑API kombinieren, um englische Entsprechungen zu erhalten.  
* Weitere von Aspose unterstützte Sprachen erkunden, z. B. Chinesisch oder Arabisch, indem Sie den Sprachcode austauschen.

Probieren Sie es mit Ihren eigenen Bildern aus – passen Sie die Vorverarbeitungs‑Einstellungen an, experimentieren Sie mit verschiedenen Dateiformaten und prüfen Sie, wie robust die Lösung in Ihrem realen Workflow ist.

Viel Spaß beim Coden und möge Ihre OCR‑Pipeline stets präzise sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}