---
category: general
date: 2026-02-19
description: Extrahiere Text aus einem Bild mit Java OCR. Lerne ein Java‑OCR‑Beispiel
  kennen, das ein Bild für OCR lädt und Text aus Rechnungsdateien in nur wenigen Schritten
  extrahiert.
draft: false
keywords:
- extract text from image
- java ocr example
- load image for ocr
- extract text from invoice
language: de
og_description: Extrahiere Text aus Bildern mit Java OCR. Dieser Leitfaden zeigt,
  wie man ein Bild für OCR lädt und Text aus Rechnungen mit einem einfachen Java-OCR-Beispiel
  extrahiert.
og_title: Text aus Bild in Java extrahieren – Vollständiges OCR‑Beispiel
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Text aus Bild in Java extrahieren – Vollständiges OCR‑Beispiel
url: /de/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild in Java extrahieren – Komplettes OCR-Beispiel

Haben Sie schon einmal **Text aus einem Bild extrahieren** müssen, wussten aber nicht, welche Bibliothek Sie wählen sollten? Sie sind nicht allein – viele Entwickler stoßen an diese Hürde, wenn sie die Rechnungsbearbeitung automatisieren oder durchsuchbare Archive erstellen. Die gute Nachricht? Mit wenigen Zeilen Java können Sie ein Bild für OCR laden, einen Interessensbereich (ROI) festlegen und den genauen Text erhalten, den Sie benötigen.  

In diesem Tutorial gehen wir Schritt für Schritt durch ein **java ocr example**, das genau zeigt, wie man **image for OCR lädt**, einen ROI setzt und **Text aus Rechnungen** mit Aspose.OCR extrahiert. Am Ende haben Sie ein lauffähiges Programm, das Sie in jedes Java‑Projekt einbinden können.

## Was Sie lernen werden

- Wie man eine `OcrEngine`‑Instanz erstellt und warum das wichtig ist.
- Der korrekte Weg, **image for OCR zu laden** mit Asposes `ImageStream`.
- Festlegen eines **region of interest (ROI)**, sodass Sie nur den Teil des Bildes verarbeiten, der den Rechnungsbetrag enthält.
- Extrahieren des erkannten Textes und Ausgabe in die Konsole.
- Häufige Stolperfallen (z. B. falsche Rechteckkoordinaten) und schnelle Lösungen.

**Voraussetzungen**

- Java 8 oder neuer installiert.
- Maven oder Gradle, um die Aspose.OCR‑Bibliothek (`com.aspose:aspose-ocr`) zu beziehen.
- Ein Beispiel‑Rechnungsbild (`invoice.png`) in einem bekannten Verzeichnis.

Alles bereit? Großartig – los geht’s.

![Text aus Bild mit Java OCR extrahieren](/images/extract-text-from-image-java.png "Beispiel für Textauszug aus Bild")

## Text aus Bild extrahieren – Schritt‑für‑Schritt Java OCR‑Beispiel

Unten finden Sie den vollständigen Quellcode. Kopieren Sie ihn gern in `RoiOcrExample.java` und führen Sie ihn direkt aus.

```java
import com.aspose.ocr.*;

public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance.
        // The engine holds all configuration and performs the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image.
        // You can point to any PNG, JPG, or TIFF file. Here we use a sample invoice.
        String imagePath = "YOUR_DIRECTORY/invoice.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Define the region of interest (ROI) you want to recognize.
        // x = 120, y = 340, width = 500, height = 120 – tweak these values for your own layout.
        Rectangle regionOfInterest = new Rectangle(120, 340, 500, 120);
        ocrEngine.setRegionOfInterest(regionOfInterest);

        // Step 4: Perform OCR on the specified ROI and retrieve the text.
        // recognize() returns an OcrResult object; getText() extracts the plain string.
        String extractedText = ocrEngine.recognize().getText();

        // Step 5: Output the recognized text.
        System.out.println("ROI text: " + extractedText);
    }
}
```

### Warum jeder Schritt wichtig ist

1. **Erstellen der OCR‑Engine** – ohne Engine gibt es keinen Kontext für die Bildverarbeitung. Das Objekt ermöglicht später das Anpassen von Sprachpaketen, falls Sie Mehrsprachigkeit benötigen.  
2. **Laden des Bildes** – `ImageStream.fromFile` abstrahiert das Dateiformat und sorgt dafür, dass die Engine die Bytes korrekt einliest. Wenn Sie diesen Schritt überspringen, erhalten Sie eine `NullPointerException`.  
3. **Festlegen des ROI** – die gesamte Seite zu verarbeiten ist ineffizient. Durch Eingrenzen des Rechtecks auf den Bereich des Rechnungsbetrags beschleunigen Sie die Erkennung und reduzieren Rauschen.  
4. **Aufruf von `recognize()`** – hier geschieht die Magie. Die Methode führt den OCR‑Algorithmus über den ROI aus und erzeugt ein Ergebnisobjekt.  
5. **Ausgabe des Ergebnisses** – in echten Projekten würden Sie den Text wahrscheinlich in einer Datenbank speichern, aber `System.out.println` ist für eine schnelle Demo ideal.

## Bild für OCR laden

Falls Sie sich fragen, ob der Pfad absolut oder relativ sein muss: Beides funktioniert – stellen Sie nur sicher, dass der Java‑Prozess die Datei lesen kann. Unter Windows müssen Backslashes escaped werden (`C:\\images\\invoice.png`) oder Sie verwenden Vorwärtsschrägstriche (`C:/images/invoice.png`).  

**Pro‑Tipp:** Wenn Sie viele Rechnungen in einer Schleife verarbeiten, verwenden Sie dieselbe `OcrEngine`‑Instanz erneut; sie cached interne Ressourcen und erhöht den Durchsatz.

## Region of Interest (ROI) definieren

Die richtige Rechteckgröße zu finden, erfordert oft ein wenig Ausprobieren. Eine praktische Methode ist, das Bild in einem Grafik‑Editor (wie GIMP oder Paint.NET) zu öffnen und mit der Maus über den gewünschten Bereich zu fahren – die X/Y‑Werte erscheinen in der Statusleiste.  

Randfall: Einige Rechnungen haben variable Layouts. In diesem Fall können Sie zunächst einen schnellen Scan des gesamten Bildes durchführen, Schlüsselwörter wie „Total:“ per Regex finden und den ROI dann dynamisch anpassen.

## OCR ausführen und Text erhalten

Der Aufruf von `recognize()` ist synchron – Ihr Thread blockiert, bis die Engine fertig ist. Für große Stapel können Sie einen Thread‑Pool einsetzen und Bilder parallel verarbeiten. Denken Sie daran, dass jeder Thread seine eigene `OcrEngine`‑Instanz benötigt; die Engine ist nicht thread‑sicher.

## Ausführen und Ausgabe prüfen

Kompilieren und ausführen:

```bash
javac -cp "path/to/aspose-ocr.jar" RoiOcrExample.java
java -cp ".:path/to/aspose-ocr.jar" RoiOcrExample
```

Sie sollten etwa Folgendes sehen:

```
ROI text: $1,254.00
```

Wenn die Ausgabe unleserlich ist, überprüfen Sie die ROI‑Koordinaten und stellen Sie sicher, dass die Bildqualität hoch ist (300 dpi oder mehr liefert beste Ergebnisse).  

### Häufige Stolperfallen & Lösungen

| Symptom | Wahrscheinliche Ursache | Lösung |
|---------|--------------------------|--------|
| Leere Zeichenkette | ROI außerhalb der Bildgrenzen | Rechteckwerte gegen Bildabmessungen prüfen |
| Rechtschreibfehler | Niedrige Auflösung | Höher aufgelöste Quelle verwenden oder Bildvorverarbeitung (z. B. Binarisierung) |
| `java.lang.NoClassDefFoundError` | Fehlende Aspose‑JAR im Klassenpfad | `aspose-ocr.jar` zu `-cp` hinzufügen oder Maven/Gradle‑Abhängigkeitsverwaltung nutzen |

## Fazit

Sie wissen jetzt, wie man **Text aus Bild** in Java mit einem kompakten **java ocr example** extrahiert. Durch korrektes Laden des Bildes, Definieren eines fokussierten ROI und Aufruf von `recognize()` können Sie zuverlässig **Text aus Rechnungen** extrahieren und in nachgelagerte Systeme einspeisen.

Was kommt als Nächstes? Probieren Sie den ROI für andere Felder (Datum, Lieferant) aus, experimentieren Sie mit Sprachpaketen für mehrsprachige Rechnungen oder integrieren Sie den OCR‑Schritt in einen Spring‑Boot‑Microservice. Das gleiche Muster funktioniert für Quittungen, Reisepässe oder jedes Dokument, bei dem Sie präzise Textextraktion benötigen.

Wenn Sie Fragen zur Skalierung dieser Lösung oder zum Umgang mit verrauschten Scans haben, hinterlassen Sie einen Kommentar unten – happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}