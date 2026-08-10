---
category: general
date: 2026-05-03
description: Das Aspose OCR Java‑Beispiel zeigt, wie man ein Bild für die OCR lädt
  und Text aus einem Bereich mit nur wenigen Codezeilen extrahiert.
draft: false
keywords:
- aspose ocr java example
- load image for OCR
- extract text from region
language: de
og_description: Das Aspose OCR Java‑Beispiel demonstriert das Laden eines Bildes für
  OCR und das Extrahieren von Text aus einem bestimmten Bereich, ideal für die Rechnungsverarbeitung.
og_title: Aspose OCR Java Beispiel – Regionstextextraktion
tags:
- Aspose OCR
- Java
- Image Processing
title: 'Aspose OCR Java Beispiel: Text aus einem Bereich extrahieren'
url: /de/java/ocr-operations/aspose-ocr-java-example-extract-text-from-a-region/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Java Beispiel: Text aus einem Bereich extrahieren

Suchen Sie ein **Aspose OCR Java Beispiel**, das Ihnen ermöglicht, nur den Teil zu extrahieren, den Sie aus einem Bild benötigen? In diesem Leitfaden gehen wir Schritt für Schritt durch **Laden eines Bildes für OCR** und **Extrahieren von Text aus einem Bereich**, ideal für Rechnungsnummern, Formularfelder oder jede Daten, die in einem größeren Bild versteckt sind.

Sie fragen sich vielleicht, warum man OCR auf ein Rechteck beschränkt, anstatt die gesamte Seite zu scannen. Die kurze Antwort: Geschwindigkeit und Genauigkeit. Wenn die Engine nur einen definierten Ausschnitt betrachtet, überspringt sie irrelevanten Lärm, arbeitet schneller und liefert oft sauberere Ergebnisse. Am Ende dieses Tutorials haben Sie ein eigenständiges Java‑Programm, das genau das tut, plus einige Tipps, um häufige Stolperfallen zu vermeiden.

## Was Sie benötigen

- **Java Development Kit (JDK) 11** oder neuer installiert.
- **Aspose.OCR for Java** Bibliothek (Sie können das neueste JAR aus dem Maven Central Repository oder dem Aspose‑Download‑Portal holen).
- Eine Bilddatei, die den Text enthält, den Sie lesen möchten – für unser Demo verwenden wir `invoice.png`, das irgendwo in der oberen rechten Ecke eine Rechnungsnummer enthält.
- Eine bevorzugte IDE oder ein einfacher Texteditor plus ein Terminal; jedes Build‑Tool (Maven, Gradle oder plain `javac`) funktioniert.

Das ist alles. Keine zusätzlichen OCR‑Engines, keine nativen Binärdateien, nur reines Java und Aspose.

![Aspose OCR Java Beispiel Screenshot](/images/aspose-ocr-java-example.png "Aspose OCR Java Beispiel zeigt Regionsextraktion")

## Aspose OCR Java Beispiel – Initialisierung der OCR‑Engine

Das Erste, was jeder OCR‑Workflow benötigt, ist eine Engine‑Instanz. Aspose liefert eine leichtgewichtige `OcrEngine`‑Klasse, die alles von Bild‑Laden bis zur Sprachauswahl übernimmt.

```java
import com.aspose.ocr.*;

public class RegionOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

**Warum das wichtig ist:** Das Erstellen der Engine im Voraus gibt Ihnen ein sauberes Objekt zum Konfigurieren. Sie können dieselbe `OcrEngine` für mehrere Bilder wiederverwenden, wenn Sie einen Stapel verarbeiten, was Speicher und Initialisierungszeit spart.

## Bild für OCR laden

Als Nächstes teilen wir der Engine mit, welches Bild gescannt werden soll. Aspose stellt den Helfer `ImageStream.fromFile` bereit, der die Low‑Level‑`FileInputStream`‑Boilerplate abstrahiert.

```java
        // Step 2: Load the image that contains the invoice
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Tipp:** Ersetzen Sie `YOUR_DIRECTORY` durch einen absoluten Pfad oder einen relativen Pfad, der zu dem Ort zeigt, an dem Sie `invoice.png` gespeichert haben. Wenn die Datei nicht gefunden wird, wirft Aspose eine `IOException`, sodass Sie diesen Code in einem try‑catch‑Block für Produktionscode einbinden sollten.

## Definieren und Extrahieren von Text aus einem Bereich

Jetzt kommt der Star der Show: das Rechteck, das der Engine sagt, wo sie schauen soll. Der Konstruktor `java.awt.Rectangle` nimmt `(x, y, width, height)` – alles in Pixeln gemessen.

```java
        // Step 3: Define the region where the invoice number is located (x, y, width, height)
        java.awt.Rectangle invoiceRegion = new java.awt.Rectangle(120, 250, 300, 80);
        ocrEngine.setRegion(invoiceRegion);   // restrict recognition to this area
```

**Wie es funktioniert:** Durch Aufruf von `setRegion` begrenzen Sie den OCR‑Scan auf einen 300 Pixel breiten Ausschnitt, der 120 Pixel vom linken Rand und 250 Pixel vom oberen Rand beginnt. Passen Sie diese Zahlen an Ihr eigenes Layout an; ein schneller Weg, sie zu finden, ist, das Bild in einem Grafik‑Editor zu öffnen, der Pixelkoordinaten anzeigt.

## Sprache aktivieren und Erkennung ausführen

Aspose OCR unterstützt Dutzende von Sprachen, aber für eine Rechnungsnummer benötigen wir nur Englisch. Das Aktivieren der richtigen Sprache reduziert Fehlalarme dramatisch.

```java
        // Step 4: Enable English language for recognition
        ocrEngine.getLanguage().setEnglish(true);

        // Step 5: Perform recognition and output the extracted text
        if (ocrEngine.recognize()) {
            System.out.println("Extracted region text: " + ocrEngine.getText());
        } else {
            System.err.println("OCR recognition failed.");
        }
    }
}
```

**Warum nur Englisch aktivieren?** Die OCR‑Engine versucht, Zeichen aus jedem aktivierten Sprachset zuzuordnen, was verwirren kann, wenn der Text einfache alphanumerische Zeichen enthält. Das Eingrenzen des Sprachumfangs verbessert sowohl Geschwindigkeit als auch Präzision.

### Erwartete Ausgabe

Wenn alles passt, sehen Sie etwa Folgendes:

```
Extracted region text: INV-12345
```

Ist das Rechteck um ein paar Pixel verschoben, kann die Ausgabe verzerrt oder leer sein. Das ist ein einfacher Plausibilitätstest: Programm ausführen, Konsole ansehen und prüfen, ob der Text mit dem im Bild sichtbaren übereinstimmt.

## Code ausführen und Ausgabe überprüfen

Angenommen, Sie verwenden Maven, fügen Sie die Aspose OCR‑Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

Kompilieren und ausführen:

```bash
mvn compile exec:java -Dexec.mainClass=RegionOcrExample
```

Oder, wenn Sie lieber plain `javac` nutzen:

```bash
javac -cp "aspose-ocr-23.10.jar" RegionOcrExample.java
java -cp ".:aspose-ocr-23.10.jar" RegionOcrExample
```

Sie sollten die Zeile **Extracted region text** in der Konsole sehen. Wenn Sie „OCR recognition failed“ erhalten, überprüfen Sie den Dateipfad und stellen Sie sicher, dass der Bereich tatsächlich lesbare Zeichen enthält.

## Randfälle & Häufige Variationen

| Situation | Was zu ändern |
|-----------|----------------|
| **Mehrere Sprachen** (z.B. Englisch + Spanisch) | Call `ocrEngine.getLanguage().setSpanish(true);` alongside English. |
| **Region außerhalb der Bildgrenzen** | Aspose will silently clip the rectangle, but you’ll lose data. Use `ImageInfo` (`ocrEngine.getImage().getWidth()`) to verify dimensions before setting the region. |
| **Dynamische Rechnungen** (verschiedene Layouts) | Consider running a lightweight pre‑scan on the whole image to locate keywords like “Invoice #” and then compute the rectangle programmatically. |
| **Bilder mit höherer DPI** | Increase `ocrEngine.getImage().setResolution(300);` for better accuracy on scanned documents. |
| **Performance‑Optimierung** | Disable unnecessary languages, keep the region as small as possible, and reuse a single `OcrEngine` instance across many files. |

## Profi‑Tipps aus der Praxis

- **Pro tip:** If you only need digits (common for invoice numbers), enable the numeric mode with `ocrEngine.getLanguage().setDigits(true);`. This eliminates alphabetic noise.
- **Watch out for:** Transparent PNGs. Aspose sometimes misinterprets the alpha channel; converting the image to a solid‑background JPEG first can solve odd blank outputs.
- **Remember:** The rectangle uses the image’s native coordinate system, not any UI scaling you might see on screen. Always test with the exact file you’ll process in production.

## Was kommt als Nächstes?

Jetzt, wo Sie ein solides **Aspose OCR Java Beispiel** für region‑basiertes Extrahieren haben, können Sie es in mehrere nützliche Richtungen erweitern:

- **Batch processing:** Loop over a folder of invoices, reusing the same `OcrEngine` to improve throughput.
- **Data validation:** Pipe the extracted text through a regex like `INV-\\d{5}` to ensure you captured a valid invoice number.
- **Integration with PDF:** Use Aspose.PDF to overlay the extracted text back onto the original document for audit trails.
- **Cloud deployment:** Wrap the code in a lightweight REST service (Spring Boot) so other systems can call it on demand.

Jeder dieser Schritte verwendet natürlich dieselben Kernkonzepte—**load image for OCR**, **extract text from a region**, und die Ergebnisverarbeitung—so wird der Übergang reibungslos sein.

---

*Viel Spaß beim Programmieren! Wenn Sie auf Probleme stoßen, hinterlassen Sie unten einen Kommentar oder besuchen Sie die Aspose‑Foren, wo die Community praxisnahe Tipps für knifflige Layouts teilt.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}