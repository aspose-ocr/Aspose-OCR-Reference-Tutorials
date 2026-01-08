---
category: general
date: 2026-01-07
description: Erstellen Sie ein durchsuchbares PDF aus einem Bild mit Aspose OCR in
  Java. Erfahren Sie, wie Sie ein Bild in PDF konvertieren, Text aus dem Bild erkennen
  und ein PDF aus JPG generieren.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- how to use ocr
- generate pdf from jpg
language: de
og_description: Erstellen Sie ein durchsuchbares PDF aus einem Bild mit Aspose OCR
  in Java. Schritt‑für‑Schritt‑Anleitung zum Konvertieren eines Bildes in PDF, zum
  Erkennen von Text im Bild und zum Generieren eines PDFs aus JPG.
og_title: Durchsuchbare PDF aus Bild erstellen – Java-OCR-Anleitung
tags:
- OCR
- Java
- PDF
- Aspose
title: Durchsuchbares PDF aus Bild mit OCR erstellen – Java‑Tutorial
url: /de/java/ocr-operations/create-searchable-pdf-from-image-with-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Durchsuchbares PDF aus Bild mit OCR erstellen – Java‑Tutorial

Hast du schon einmal **ein durchsuchbares PDF** aus einem gescannten Bild erstellen wollen, wusstest aber nicht, wo du anfangen sollst? Du bist nicht allein – vielen Entwicklern stößt das anfangs an diese Hürde, wenn sie versuchen, ein JPEG in ein PDF zu verwandeln, das man tatsächlich durchsuchen kann.  

In diesem Leitfaden gehen wir Schritt für Schritt durch ein vollständiges, ausführbares Beispiel, das zeigt, wie man **ein Bild in PDF konvertiert**, **Text aus einem Bild erkennt** und schließlich **ein PDF aus JPG erzeugt** mit Aspose OCR für Java. Keine vagen Verweise, nur Code, den du heute kopieren‑und‑einsetzen kannst.

## Was du brauchst

Bevor wir loslegen, stelle sicher, dass du Folgendes auf deinem Rechner hast:

* **Java 17** oder neuer (die API funktioniert mit jeder aktuellen JDK).  
* **Aspose.OCR für Java**‑Bibliothek – du kannst das neueste JAR von Maven Central oder der Aspose‑Webseite herunterladen.  
* Ein Beispielbild, z. B. `sample.jpg`, das in einem Ordner liegt, den du referenzieren kannst.  
* Eine IDE oder ein einfacher Texteditor plus ein Terminal – was dir am besten passt.

Das war’s. Keine schweren Frameworks, keine zusätzlichen nativen Abhängigkeiten. Auf geht’s.

## Schritt 1 – Durchsuchbares PDF erstellen: OCR‑Engine initialisieren

Das Erste, was wir tun, ist eine Instanz von `OcrEngine` zu erzeugen und sie auf das Quellbild zu verweisen. Dieses Objekt ist das Herzstück von Aspose OCR; es übernimmt alles vom Laden des Bitmaps bis zum Bereitstellen des erkannten Textes.

```java
import com.aspose.ocr.*;

public class HelloOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the image you want to turn into a searchable PDF
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

> **Warum das wichtig ist:** Die korrekte Initialisierung der Engine stellt sicher, dass die Bibliothek das Bildformat lesen kann, das du ihr übergibst. Ist der Pfad falsch, bekommst du eine `FileNotFoundException` und die gesamte Pipeline stoppt.

## Schritt 2 – Leistung steigern: GPU, Mehrkern‑CPU und Rechtschreibkorrektur aktivieren

OCR kann CPU‑intensiv sein, besonders bei großen Dokumenten. Aspose bietet dir mehrere Stellschrauben, die du umlegen kannst, um den Vorgang schneller und genauer zu machen.

```java
        // 2️⃣ Turn on performance helpers – GPU, multi‑core CPU, and spell correction
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)                 // uses GPU if one is available
                 .setUseMultiCore(true)           // spreads work across CPU cores
                 .setEnableSpellCorrection(true); // cleans up common OCR mistakes
```

> **Pro‑Tipp:** Wenn du auf einem Server ohne GPU arbeitest, schadet `setUseGpu(false)` nichts – du fällst einfach auf die Mehrkern‑CPU‑Verarbeitung zurück.

## Schritt 3 – Bildqualität verbessern: Deskew und Despeckle (optional, aber empfohlen)

Scans sind selten perfekt. Ein leichter Schräglauf oder Bildrauschen kann den Erkenner verwirren. Die Klasse `ImageProcessingOptions` ermöglicht es dir, das Bild aufzuräumen, bevor die Engine versucht, es zu lesen.

```java
        // 3️⃣ Pre‑process the image – straighten it and remove noise
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)   // automatically rotates tilted text
                 .setDespeckle(true); // reduces background speckles
```

> **Randfall:** Wenn dein Quellbild bereits sauber ist, kannst du diesen Schritt überspringen. Er schadet nicht, kostet aber ein paar Millisekunden Rechenzeit.

## Schritt 4 – Text aus Bild erkennen und PDF erzeugen

Jetzt passiert die Magie. Wir rufen `recognize()` auf und die Engine liefert ein `OcrResult`. Damit können wir das Ergebnis in verschiedenen Formaten speichern – PDF ist dabei das gängigste für durchsuchbare Dokumente.

```java
        // 4️⃣ Perform OCR and get the result object
        OcrResult ocrResult = ocrEngine.recognize();

        // 5️⃣ Save the result as a searchable PDF (you could also choose TXT, DOCX, etc.)
        ocrResult.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);
    }
}
```

> **Was du sehen wirst:** `sample-output.pdf` enthält das Originalbild als Hintergrundschicht, während der erkannte Text als unsichtbare Überlagerung oben liegt. Öffne es in Adobe Reader und versuche, Text zu markieren – du wirst überrascht sein.

## Schritt 5 – Ausgabe des durchsuchbaren PDFs überprüfen

Nachdem die Datei geschrieben wurde, ist es gute Praxis, zu prüfen, ob das PDF wirklich durchsuchbar ist.

```java
import java.awt.Desktop;
import java.io.File;

public class VerifyPdf {
    public static void main(String[] args) throws Exception {
        File pdf = new File("YOUR_DIRECTORY/sample-output.pdf");
        if (pdf.exists() && Desktop.isDesktopSupported()) {
            Desktop.getDesktop().open(pdf); // opens the PDF in the default viewer
        } else {
            System.out.println("PDF not found or cannot be opened on this platform.");
        }
    }
}
```

Öffne das PDF, drücke **Strg F**, gib ein Wort ein, von dem du weißt, dass es im Bild vorkommt – wenn die Suche es findet, hast du erfolgreich **ein durchsuchbares PDF erstellt**!

## OCR in realen Szenarien einsetzen (Bonus)

* **Batch‑Verarbeitung:** Packe den Code in eine Schleife, die über einen Ordner mit JPGs iteriert. Denk daran, eine einzelne `OcrEngine`‑Instanz wiederzuverwenden, um den Speicherverbrauch gering zu halten.  
* **Sprachunterstützung:** Aspose OCR unterstützt über 60 Sprachen. Rufe einfach `ocrEngine.getEngineOptions().setLanguage(Language.English);` (oder einen anderen Enum‑Wert) auf.  
* **Fehlerbehandlung:** Fange `OcrException`, um beschädigte Dateien elegant zu behandeln.  

Diese Anpassungen machen die Lösung robust genug für Produktionspipelines.

## Vollständiges Java‑Beispiel – Durchsuchbares PDF aus JPG erstellen

Unten findest du das komplette, eigenständige Programm, das du unverändert kompilieren und ausführen kannst. Ersetze `YOUR_DIRECTORY` durch den tatsächlichen Pfad auf deinem Rechner.

```java
import com.aspose.ocr.*;

public class CreateSearchablePdf {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // -------------------------------------------------
        // 2️⃣ Performance helpers
        // -------------------------------------------------
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)
                 .setUseMultiCore(true)
                 .setEnableSpellCorrection(true);

        // -------------------------------------------------
        // 3️⃣ Image pre‑processing (optional but helpful)
        // -------------------------------------------------
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)
                 .setDespeckle(true);

        // -------------------------------------------------
        // 4️⃣ Run OCR and save as searchable PDF
        // -------------------------------------------------
        OcrResult result = ocrEngine.recognize();
        result.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);

        System.out.println("✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf");
    }
}
```

**Erwartete Ausgabe:**  

```
✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf
```

Öffne das erzeugte PDF und du solltest jedes Wort, das in `sample.jpg` vorkam, suchen können. Siehst du die Textebene nicht, prüfe den Bildpfad und stelle sicher, dass die OCR‑Engine keine versteckten Ausnahmen wirft.

## Fazit

Wir haben dir gezeigt, wie du **ein durchsuchbares PDF** aus einem JPEG mit Aspose OCR für Java erstellst. Vom Laden des Bildes, über das Anpassen von Performance‑Einstellungen, das Aufräumen des Bildes, bis hin zum Erkennen des Textes und dem Speichern eines durchsuchbaren PDFs – jeder Schritt wurde mit dem *Warum* und *Wie* erklärt.  

Jetzt kannst du **ein Bild in PDF konvertieren**, **Text aus Bild erkennen** und **ein PDF aus JPG generieren** in deinen eigenen Anwendungen. Als Nächstes probiere die Verarbeitung eines ganzen Ordners von Scans, experimentiere mit verschiedenen Sprachen oder füge dem Ausgabe‑PDF einen Passwortschutz hinzu. Der Himmel ist die Grenze.

Hast du Fragen zu Randfällen, Lizenzierung oder Performance‑Optimierung? Hinterlasse einen Kommentar unten, und happy coding! 

![Diagram illustrating OCR pipeline – create searchable pdf](/images/ocr-pipeline.png "Create searchable PDF diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}