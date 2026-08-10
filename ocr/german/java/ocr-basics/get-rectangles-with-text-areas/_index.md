---
date: 2026-06-19
description: Erfahren Sie, wie Sie Bild in Text in Java konvertieren, Absätze aus
  dem Bild extrahieren und Textbereich-Rechtecke mithilfe der Aspose OCR Java library
  abrufen.
keywords:
- image to text java
- convert scanned image text
- extract paragraphs from image
- aspose ocr java tutorial
linktitle: Image to Text Java – Text aus Bild erkennen und Textbereich-Rechtecke abrufen
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  headline: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  type: TechArticle
- description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  name: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  steps:
  - name: Set Up Your Project
    text: Create a new Java project (or add to an existing one) and place the Aspose.OCR
      JAR on the classpath. If you use Maven, add the dependency as described in the
      download package.
  - name: Define Document Directory and Image Path
    text: 'Specify where your sample image resides:'
  - name: Create AsposeOCR Instance
    text: '`AsposeOCR` is the main class that provides OCR functionality. Instantiate
      the OCR engine:'
  - name: Recognize Text in the Image
    text: Load your image and call `RecognizePage` to convert the picture into plain
      text. This single method call performs image preprocessing, character segmentation,
      and language‑specific recognition in one step.
  - name: Get Rectangles with Text Areas
    text: Retrieve the bounding rectangles for each paragraph (or other area types).
      This step returns a collection of `Rectangle` objects that precisely enclose
      the detected text blocks, enabling you to highlight or further process individual
      sections. CODE_BLOCK_PLACEHOLDER_5_END
  type: HowTo
- questions:
  - answer: Yes, Aspose.OCR works with Java 11 and later versions.
    question: Is Aspose.OCR compatible with Java 11?
  - answer: Yes, you can use it in any type of project. For licensing details, visit
      [here](https://purchase.aspose.com/buy).
    question: Can I use Aspose.OCR for both personal and commercial projects?
  - answer: You can obtain a temporary license [here](https://purchase.aspose.com/temporary-license/).
    question: How do I obtain a temporary license for evaluation?
  - answer: For support and discussions, visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).
    question: Where can I find community support or official assistance?
  - answer: Yes, the library is thread‑safe and can be used in concurrent environments
      for better performance.
    question: Does Aspose.OCR support multithreading?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Image to Text Java – Bild in Text umwandeln und Textbereich-Rechtecke abrufen
url: /de/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bild zu Text Java – Bild in Text konvertieren und Textbereich‑Rechtecke ermitteln

## Einleitung

Wenn Sie in einer Java‑Anwendung **Bild in Text konvertieren** müssen, liefert Aspose.OCR für Java eine schnelle, genaue Lösung. In diesem Tutorial führen wir Sie durch die genauen Schritte, die erforderlich sind, um Absätze aus einem Bild zu extrahieren, die Begrenzungsrechtecke für jeden Textbereich zu erhalten und diese Koordinaten in der Konsole auszugeben. Am Ende verstehen Sie, warum dieser Ansatz funktioniert, wie Sie die Bibliothek integrieren und wo Sie sie für Ihre eigenen Anwendungsfälle erweitern können.

## Schnelle Antworten
`AreasType` ist eine Aufzählung, die das Niveau der Textsegmentierung (Wörter, Zeilen, Absätze) angibt.

- **Was bedeutet „Text aus Bild erkennen“?** Es bedeutet, visuelle Zeichen in einem Bild in editierbare Zeichenketten zu konvertieren.  
- **Welche Bibliothek erledigt das in Java?** Aspose.OCR für Java.  
- **Benötige ich eine Lizenz für die Entwicklung?** Eine temporäre Lizenz ist zum Testen verfügbar; für die Produktion ist eine Voll‑Lizenz erforderlich.  
- **Kann ich Absätze statt einzelner Wörter extrahieren?** Ja – verwenden Sie `AreasType.PARAGRAPHS`, um Rechtecke auf Absatz‑Ebene zu erhalten.  
- **Ist der Code mit Java 11+ kompatibel?** Absolut, die API funktioniert mit Java 11 und später.

## Was bedeutet „Bild in Text konvertieren“ in Aspose.OCR?

`convert image to text` bezieht sich auf den Vorgang, ein Bitmap zu analysieren, OCR‑Algorithmen anzuwenden und die erkannten Zeichen als Zeichenkette zurückzugeben. Die Methode `RecognizePage` von Aspose.OCR führt diese Konvertierung durch und liefert optional die genauen `Rectangle`‑Koordinaten für jeden erkannten Textblock.

## Warum diese **java ocr library** verwenden?

Aspose.OCR unterstützt **30+ Sprachen** und kann Bilder bis zu **50 MB** verarbeiten, ohne die gesamte Datei in den Speicher zu laden, und liefert sub‑sekundäre Antwortzeiten auf typischer Server‑Hardware. Die Bibliothek ist thread‑sicher, erfordert nur ein einziges JAR und bietet flexible Ausgabeformate – einschließlich Rohtext, HTML und präziser Text‑Bereich‑Rechtecke – und ist damit ideal für Hochdurchsatz‑Enterprise‑Szenarien.

## Voraussetzungen

- **Java Development Kit** (JDK 11 oder neuer) auf Ihrem Rechner installiert.  
- **Aspose.OCR for Java** Bibliothek – laden Sie sie von der offiziellen Seite [hier](https://releases.aspose.com/ocr/java/) herunter.  
- Eine IDE oder ein Build‑Tool (Maven/Gradle), um die JAR‑Abhängigkeit zu verwalten.

## Pakete importieren

In Ihrem Java‑Projekt importieren Sie die notwendigen Klassen:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Schritt‑für‑Schritt‑Anleitung

### Schritt 1: Projekt einrichten
Erstellen Sie ein neues Java‑Projekt (oder fügen Sie es zu einem bestehenden hinzu) und platzieren Sie das Aspose.OCR‑JAR im Klassenpfad. Wenn Sie Maven verwenden, fügen Sie die Abhängigkeit wie im Download‑Paket beschrieben hinzu.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Schritt 2: Dokumentverzeichnis und Bildpfad festlegen
Geben Sie an, wo Ihr Beispielbild liegt:

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### Schritt 3: AsposeOCR‑Instanz erstellen
`AsposeOCR` ist die Hauptklasse, die OCR‑Funktionalität bereitstellt.

Instanziieren Sie die OCR‑Engine:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Schritt 4: Text im Bild erkennen
Laden Sie Ihr Bild und rufen Sie `RecognizePage` auf, um das Bild in Klartext zu konvertieren. Dieser einzelne Methodenaufruf führt Bildvorverarbeitung, Zeichensegmentierung und sprachspezifische Erkennung in einem Schritt durch.

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

### Schritt 5: Rechtecke mit Textbereichen erhalten
Rufen Sie die Begrenzungsrechtecke für jeden Absatz (oder andere Bereichstypen) ab. Dieser Schritt gibt eine Sammlung von `Rectangle`‑Objekten zurück, die die erkannten Textblöcke exakt umschließen und es Ihnen ermöglichen, einzelne Abschnitte hervorzuheben oder weiter zu verarbeiten.

CODE_BLOCK_PLACEHOLDER_5_END

## Häufige Probleme & Fehlerbehebung

| Symptom | Wahrscheinliche Ursache | Lösung |
|---------|--------------------------|--------|
| `IOException` on `RecognizePage` | Falscher Dateipfad oder fehlende Leseberechtigung | Stellen Sie sicher, dass `imagePath` auf ein vorhandenes PNG/JPG zeigt und die Anwendung Zugriff auf das Dateisystem hat. |
| Leere Ergebniszeichenkette | Bild von schlechter Qualität oder nicht unterstützte Sprache | Bild vorverarbeiten (Kontrast erhöhen, binarisieren) oder die korrekte Sprache mit `api.setLanguage("eng")` angeben. |
| Keine Rechtecke zurückgegeben | Falschen `AreasType` verwendet (z. B. `WORDS` statt Absätze) | Wechseln Sie bei Bedarf zu `AreasType.PARAGRAPHS` oder `AreasType.LINES`. |

## Häufig gestellte Fragen

**Q: Ist Aspose.OCR mit Java 11 kompatibel?**  
A: Ja, Aspose.OCR funktioniert mit Java 11 und späteren Versionen.

**Q: Kann ich Aspose.OCR sowohl für private als auch kommerzielle Projekte nutzen?**  
A: Ja, Sie können es in jeder Art von Projekt verwenden. Für Lizenzdetails besuchen Sie [hier](https://purchase.aspose.com/buy).

**Q: Wie erhalte ich eine temporäre Lizenz für die Evaluierung?**  
A: Sie können eine temporäre Lizenz [hier](https://purchase.aspose.com/temporary-license/) erhalten.

**Q: Wo finde ich Community‑Support oder offizielle Hilfe?**  
A: Für Support und Diskussionen besuchen Sie das [Aspose.OCR‑Forum](https://forum.aspose.com/c/ocr/16).

**Q: Unterstützt Aspose.OCR Multithreading?**  
A: Ja, die Bibliothek ist thread‑sicher und kann in gleichzeitigen Umgebungen für bessere Leistung verwendet werden.

## Fazit

In diesem **aspose ocr java tutorial** haben Sie gelernt, wie man **Bild in Text konvertiert** mit Aspose.OCR für Java, Absätze extrahiert und die genauen Rechtecke ermittelt, die jeden Textblock umgeben. Diese Möglichkeiten ermöglichen es Ihnen, durchsuchbare PDFs zu erstellen, Text in UI‑Overlays hervorzuheben oder strukturierte Daten in nachgelagerte Prozesse einzuspeisen. Erkunden Sie die API weiter, um Spracheinstellungen anzupassen, verschiedene Bildformate zu verarbeiten oder die Integration mit Cloud‑Speicher zu realisieren.

---

**Zuletzt aktualisiert:** 2026-06-19  
**Getestet mit:** Aspose.OCR 23.10 for Java  
**Autor:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Verwandte Tutorials

- [Text aus Bildern extrahieren – OCR‑Grundlagen mit Aspose.OCR für Java](/ocr/java/ocr-basics/)
- [Text aus Bild in Java extrahieren mit Aspose.OCR Detect Areas‑Modus](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Bild in Text konvertieren in Java mit Aspose.OCR BufferedImage](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}