---
category: general
date: 2026-06-16
description: Das OCR‑Bounding‑Box‑Tutorial in Java zeigt, wie man Text aus einem Bild
  extrahiert, Text aus einem Bild liest und den OCR‑Vertrauenswert für JPG‑Dateien
  erhält.
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: de
og_description: OCR-Bounding-Box in Java ermöglicht das Erkennen von Text aus JPG-Dateien,
  das Extrahieren von Text aus Bildern und das Anzeigen von OCR-Vertrauenswerten –
  alles in einem einfachen Codebeispiel.
og_title: OCR-Bounding-Box in Java – Text aus Bild extrahieren
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: OCR-Bounding-Box in Java – Text aus Bild extrahieren
url: /de/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Bounding Box in Java – Text aus Bild extrahieren

Haben Sie sich jemals gefragt, wie man die **ocr bounding box** für jedes Textstück in einem Java‑Bild erhält? In diesem Tutorial zeigen wir Ihnen, wie Sie **extract text from image**‑Dateien **read text from image** und sogar den **ocr confidence score** sehen können, während Sie **recognize text from jpg**‑Dateien erkennen. Die kurze Antwort? Ein paar Codezeilen mit einer modernen OCR‑Bibliothek, plus eine kurze Erklärung, warum jeder Aufruf wichtig ist.

Unten finden Sie ein komplettes, sofort ausführbares Beispiel, eine Schritt‑für‑Schritt‑Aufschlüsselung und eine Handvoll praktischer Tipps, die Sie direkt in Ihr eigenes Projekt übernehmen können. Am Ende werden Sie in der Lage sein, etwas wie folgt auszugeben:

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## Was Sie benötigen

- **Java 11** oder neuer (die Syntax unten verwendet das Schlüsselwort `var` zur Kürze, Sie können es jedoch bei älteren JDKs weglassen).  
- Eine OCR‑Bibliothek, die eine Java‑API bereitstellt – für diesen Leitfaden verwenden wir **[Tesseract4J](https://github.com/nguyenq/tess4j)**, einen dünnen Wrapper um die beliebte Tesseract‑Engine.  
- Ein JPEG‑Bild (`.jpg`), das klaren, gedruckten Text enthält.  
- Ihre bevorzugte IDE (IntelliJ IDEA, Eclipse, VS Code…) – jede ist geeignet.

Falls Ihnen die Bibliothek fehlt, fügen Sie einfach diese Maven‑Abhängigkeit hinzu:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Jetzt legen wir los.

![Beispiel für OCR Bounding Box](ocr-bounding-box.png "Beispiel für OCR Bounding Box")

## OCR Bounding Box: Einrichtung der Engine

Das Erste, was Sie tun müssen, ist eine OCR‑Engine‑Instanz zu erstellen. Denken Sie daran wie das Einschalten des Scanners, der später die Pixel liest.

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**Warum das wichtig ist:**  
Ohne das Setzen des `datapath` weiß Tesseract nicht, wo seine Sprachpakete liegen, und Sie erhalten einen kryptischen Fehler „Failed loading language“. Der Aufruf `setLanguage` ist optional, wenn Sie nur das Standard‑Englisch‑Paket benötigen, aber explizit zu sein macht den Code für zukünftige Leser klarer.

## Laden Sie das Bild, das Sie verarbeiten möchten

Als Nächstes übergeben Sie der Engine das JPEG, das Sie analysieren möchten. Die Bibliothek akzeptiert ein `File` oder `BufferedImage`; wir verwenden aus Einfachheitsgründen ein `File`.

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**Pro‑Tipp:**  
Wenn Ihr Bild in den Ressourcen liegt (z. B. innerhalb eines JAR), verwenden Sie `getResourceAsStream` und wickeln Sie es mit `ImageIO.read` ein. So funktioniert das Tutorial sowohl lokal als auch in einer gepackten Anwendung.

## OCR‑Erkennung durchführen

Jetzt lassen wir die Engine tatsächlich das Bild lesen. Das Ergebnis ist ein reiner Text‑String, aber wir wollen auch den **ocr confidence score** und die **ocr bounding box** für jede Zeile.

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**Warum wir `getWords` anstelle von `doOCR` verwenden:**  
`doOCR` liefert Ihnen den rohen String, verwirft jedoch räumliche Informationen. Durch Aufruf von `getWords` mit `RIL_WORD` (oder `RIL_TEXTLINE`, wenn Sie Boxen auf Zeilenebene bevorzugen) erhalten wir eine Liste von `Word`‑Objekten, die jeweils den Text, das Vertrauen (confidence) und das Begrenzungsrechteck enthalten. Das ist das Herzstück der **ocr bounding box**‑Funktion.

## Verständnis der Ausgabe

Das Ausführen des obigen Snippets mit einem sauberen JPEG liefert eine Ausgabe ähnlich wie:

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Text** – die erkannten Zeichen.  
- **Confidence** – ein Fließkommawert zwischen 0 und 1; höher bedeutet, dass die Engine sicherer ist.  
- **Box** – das Rechteck, das das Wort in Pixelkoordinaten (x, y, Breite, Höhe) umschließt.

Sie können jetzt **read text from image** und zudem genau wissen, wo jeder Ausschnitt auf der Leinwand liegt – perfekt zum Hervorheben, Zuschneiden oder für die Weitergabe an nachgelagerte NLP‑Pipelines.

## Randfälle & häufige Stolperfallen

| Situation | Worauf zu achten ist | Lösung / Work‑around |
|-----------|----------------------|----------------------|
| Bild ist unscharf oder hat niedrigen Kontrast | Confidence‑Werte fallen dramatisch (oft unter 0,6). | Vorverarbeitung mit OpenCV: Kontrast erhöhen, Schwellenwert anwenden. |
| JPEG enthält gedrehten Text | Bounding‑Boxes erscheinen verzerrt oder fehlen. | Verwenden Sie `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)`, damit Tesseract die Orientierung automatisch erkennt. |
| Große Bilder verursachen OutOfMemoryError | Der Java‑Heap füllt sich beim Laden großer Bilder. | Skalieren Sie das Bild vor OCR herunter (`ImageIO.read` → `BufferedImage.getScaledInstance`). |
| Sie benötigen Zeilen‑Boxen statt Wort‑Boxen | `RIL_WORD` liefert Boxen pro Wort. | Wechseln Sie zu `ITesseract.PageIteratorLevel.RIL_TEXTLINE`. |
| Nicht‑englische Zeichen erscheinen als � | Sprachdaten nicht geladen. | Laden Sie die passende `.traineddata`‑Datei herunter und verweisen Sie mit `setDatapath` auf deren Ordner. |

Das frühzeitige Beheben dieser Probleme spart Ihnen später Stunden an Fehlersuche.

## Vollständiges funktionierendes Beispiel (Alle Schritte in einer Datei)

Unten finden Sie eine eigenständige Java‑Klasse, die Sie in einen `src/main/java`‑Ordner kopieren und mit `mvn exec:java` ausführen können. Sie fasst alles zusammen, was wir besprochen haben.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Text aus Bild extrahieren in Java mit Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Textbilder extrahieren – OCR‑Grundlagen mit Aspose.OCR für Java](/ocr/english/java/ocr-basics/)
- [Wie man Bildtext mit Sprache mittels Aspose.OCR erkennt](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}