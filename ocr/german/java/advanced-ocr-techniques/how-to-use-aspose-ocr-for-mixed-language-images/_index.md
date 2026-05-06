---
category: general
date: 2026-05-06
description: Wie man Aspose OCR verwendet, um Text aus einem Bild zu erkennen, die
  automatische Spracherkennung zu aktivieren und die OCR‑Geschwindigkeit in Java zu
  verbessern.
draft: false
keywords:
- how to use aspose
- recognize text from image
- improve ocr speed
- load image for ocr
- enable automatic language detection
language: de
og_description: Wie man Aspose OCR verwendet, um Text aus Bildern schnell zu erkennen,
  die automatische Spracherkennung zu aktivieren und die OCR‑Geschwindigkeit in Java
  zu verbessern.
og_title: Wie man Aspose OCR für mehrsprachige Bilder verwendet
tags:
- Aspose
- OCR
- Java
- Image Processing
title: Wie man Aspose OCR für mehrsprachige Bilder verwendet
url: /de/java/advanced-ocr-techniques/how-to-use-aspose-ocr-for-mixed-language-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# So verwenden Sie Aspose OCR für mehrsprachige Bilder

Haben Sie sich jemals gefragt, **wie man Aspose** verwendet, um Text aus einem Bild zu extrahieren, das mehrere Sprachen gleichzeitig enthält? Sie sind nicht allein – Entwickler stoßen häufig an Grenzen, wenn ein Bild Englisch, Russisch, Hindi oder irgendeine andere Schriftart mischt. Die gute Nachricht ist, dass Aspose OCR dies elegant handhabt, und Sie können sogar **Text aus Bild erkennen** schneller, indem Sie den Sprachensatz eingrenzen.

In diesem Tutorial führen wir Sie durch ein vollständiges, sofort ausführbares Java‑Beispiel, das **lädt Bild für OCR**, die **automatische Spracherkennung** aktiviert und einen einfachen Trick zeigt, um **OCR‑Geschwindigkeit zu verbessern**. Am Ende haben Sie ein eigenständiges Programm, das den extrahierten Text in der Konsole ausgibt, und Sie verstehen, warum jede Einstellung wichtig ist.

> **Voraussetzungen** – Java 17+ installiert, Maven oder Gradle für das Abhängigkeitsmanagement und eine Aspose OCR‑Lizenz (die kostenlose Testversion funktioniert für die Evaluierung). Keine weiteren Bibliotheken sind erforderlich.

---

## Schritt 1 – Aspose OCR zu Ihrem Projekt hinzufügen

Bevor Sie **Aspose verwenden** können, benötigen Sie die Bibliothek im Klassenpfad. Mit Maven sieht das so aus:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

Falls Sie Gradle bevorzugen:

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Profi‑Tipp:** Bleiben Sie bei der neuesten stabilen Version; neuere Releases enthalten oft Leistungsverbesserungen, die sich direkt auf **OCR‑Geschwindigkeit verbessern** auswirken.

---

## Schritt 2 – Instanz der OCR‑Engine erstellen  

Das Herzstück jedes Aspose OCR‑Workflows ist die `OcrEngine`. Das Instanziieren ist unkompliziert, aber es ist erwähnenswert, dass die Engine interne Caches hält. Die Wiederverwendung einer einzelnen Instanz über viele Bilder hinweg kann tatsächlich **OCR‑Geschwindigkeit verbessern**, weil die Bibliothek wiederholte native Initialisierungen vermeidet.

```java
import com.aspose.ocr.*;

public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialise the OCR engine – one instance per application is ideal
        OcrEngine ocrEngine = new OcrEngine();
```

## Schritt 3 – **Bild für OCR laden**  

Aspose unterstützt viele Bildformate (PNG, JPEG, TIFF, BMP). Hier demonstrieren wir das Laden einer PNG, die englischen, russischen und Hindi‑Text enthält. Der Helfer `ImageStream.fromFile` abstrahiert die Datei‑I/O‑Details und stellt sicher, dass das Bild korrekt in die Engine gestreamt wird.

```java
        // Step 3: Load the picture that holds mixed languages
        // Replace the path with the actual location of your image file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));
```

> **Was, wenn das Bild im Speicher liegt?** Verwenden Sie stattdessen `ImageStream.fromByteArray(byte[])` – perfekt für Web‑Services, die Bilder als Bytestreams erhalten.

## Schritt 4 – Automatische Spracherkennung aktivieren  

Standardmäßig geht Aspose OCR von einer einzigen Sprache aus, was bei mehrsprachigen Bildern zu verzerrten Ausgaben führen kann. Das Aktivieren der automatischen Erkennung veranlasst die Engine, das Schriftsystem jedes Textblocks vor der Erkennung zu erkennen.

```java
        // Step 4: Turn on auto‑detect – this is the key to handling mixed‑language images
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

## Schritt 5 – **OCR‑Geschwindigkeit verbessern** durch Einschränkung des Sprachpools  

Die vollständige Auto‑Erkennung scannt jede von Aspose unterstützte Sprache (über 70). Wenn Sie die möglichen Sprachen im Voraus kennen, können Sie der Engine einen Hinweis geben. Das Bereitstellen eines kleineren Arrays reduziert den Suchraum und **verbessert OCR‑Geschwindigkeit**.

```java
        // Step 5 (optional but recommended): Limit detection to known languages
        // "en" = English, "ru" = Russian, "hi" = Hindi
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });
```

> **Warum hilft das?** Die Engine überspringt Sprachmodelle, die sie nicht benötigt, und spart CPU‑Zyklen sowie Speicher. Wenn Sie später weitere Sprachen hinzufügen, aktualisieren Sie einfach das Array – kein Code‑Rewrite erforderlich.

## Schritt 6 – Durchführung der Erkennung und **Text aus Bild erkennen**  

Jetzt findet die eigentliche Verarbeitung statt. `recognize()` gibt ein `OcrResult`‑Objekt zurück, das den Klartext, Konfidenzwerte und sogar die Layout‑Informationen enthält, falls Sie diese später benötigen.

```java
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 7: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Erwartete Konsolenausgabe

```
=== Extracted Text ===
Hello world!
Привет мир!
नमस्ते दुनिया!
```

Wenn das Bild zusätzliches Rauschen oder schiefen Text enthält, können Sie für diese Zeilen niedrigere Konfidenzwerte sehen. In diesem Fall sollten Sie das Bild vorverarbeiten (Entzerrung, Binärisierung), bevor Sie es an Aspose übergeben.

## Häufige Fragen & Sonderfälle

### Was, wenn das Bild riesig ist (z. B. >10 MP)?

Große Bilder verbrauchen mehr Speicher und können die Verarbeitung verlangsamen. Eine schnelle Möglichkeit, **OCR‑Geschwindigkeit zu verbessern**, besteht darin, das Bild zu verkleinern, während die Lesbarkeit erhalten bleibt:

```java
// Example using java.awt for simple resizing (optional)
BufferedImage original = ImageIO.read(new File("large.png"));
int targetWidth = 2000; // adjust based on your needs
BufferedImage resized = new BufferedImage(targetWidth,
        (original.getHeight() * targetWidth) / original.getWidth(),
        BufferedImage.TYPE_INT_RGB);
Graphics2D g = resized.createGraphics();
g.drawImage(original, 0, 0, targetWidth, resized.getHeight(), null);
g.dispose();
ocrEngine.setImage(ImageStream.fromImage(resized));
```

### Wie gehe ich mit Rechts‑nach‑Links‑Schriften wie Arabisch um?

Aspose OCR respektiert automatisch die Schreibrichtung, aber Sie möchten möglicherweise das `RightToLeft`‑Flag für die Nachbearbeitung setzen:

```java
ocrEngine.getSettings().setRightToLeft(true);
```

### Kann ich Text aus PDFs statt aus Bildern extrahieren?

Ja – konvertieren Sie jede PDF‑Seite in ein Bild (mit Aspose PDF oder einem beliebigen Rasterisierer) und geben Sie das Ergebnis an dieselbe OCR‑Pipeline weiter. Die gleiche **Text aus Bild erkennen**‑Logik gilt.

## Vollständiges funktionierendes Beispiel (zum Kopieren‑Einfügen bereit)

```java
import com.aspose.ocr.*;
import java.io.File;

/**
 * Demonstrates how to use Aspose OCR to recognize text from an image
 * that contains multiple languages, with automatic language detection
 * and a speed‑optimising language whitelist.
 */
public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine – reuse this instance for many images
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that holds mixed languages (replace with your path)
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));

        // Enable automatic detection of language per text block
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // OPTIONAL: Restrict detection to English, Russian, and Hindi to boost speed
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });

        // Run OCR and capture the result
        OcrResult ocrResult = ocrEngine.recognize();

        // Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Speichern Sie die Datei als `MixedLanguageDemo.java`, kompilieren Sie sie mit `javac` und führen Sie sie mit `java MixedLanguageDemo` aus. Wenn alles korrekt eingerichtet ist, wird der mehrsprachige Text in der Konsole ausgegeben.

## Fazit

Sie wissen jetzt, **wie man Aspose** verwendet, um **Text aus Bild**‑Dateien zu **erkennen**, die mehrere Sprachen enthalten, wie man **automatische Spracherkennung aktiviert** und einen praktischen Hinweis, **OCR‑Geschwindigkeit zu verbessern**, indem man den Sprachpool begrenzt. Der vollständige Code oben ist zum Kopieren‑Einfügen bereit, und die Erklärungen sollten Ihnen das Vertrauen geben, die Lösung anzupassen – egal, ob Sie **Bild für OCR laden** aus einem Stream, einem Byte‑Array oder sogar einem Webcam‑Snapshot benötigen.

Nächste Schritte? Probieren Sie Folgendes aus:

* Bildvorverarbeitung hinzufügen (Rauschen entfernen, binarisieren) für Scans von geringer Qualität.  
* `OcrResult` als JSON exportieren für nachgelagerte Dienste.  
* Die Engine in einen Spring‑Boot‑REST‑Endpoint integrieren, sodass Clients Bilder hochladen und sofort extrahierten Text erhalten können.

Viel Spaß beim Programmieren, und mögen Ihre OCR‑Pipelines schnell, genau und mehrsprachig sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}