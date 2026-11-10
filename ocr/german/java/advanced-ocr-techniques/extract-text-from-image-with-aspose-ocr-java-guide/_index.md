---
category: general
date: 2026-02-14
description: Extrahieren Sie Text aus einem Bild mit Aspose OCR in Java. Erfahren
  Sie, wie Sie Text aus Formularfeldern mit Interessensbereichen für präzise Ergebnisse
  extrahieren.
draft: false
keywords:
- extract text from image
- extract text from form
language: de
og_description: Extrahieren Sie Text aus einem Bild mit Aspose OCR in Java. Dieses
  Tutorial zeigt, wie man Text aus Formularfeldern über Interessensbereiche extrahiert.
og_title: Text aus Bild mit Aspose OCR extrahieren – Java‑Leitfaden
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Text aus Bild mit Aspose OCR extrahieren – Java‑Leitfaden
url: /de/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild mit Aspose OCR extrahieren – Java‑Leitfaden

Haben Sie jemals **Text aus Bild extrahieren** müssen, aber dabei das ganze Bild geparst, CPU‑Zyklen verschwendet und verrauschte Ergebnisse erhalten? Sie sind nicht allein. In vielen realen Anwendungen – denken Sie an Rechnungsscanner, Reisepassleser oder Dateneingabeformulare – interessieren Sie sich nur für eine Handvoll Felder, nicht für die gesamte Leinwand.  

Die gute Nachricht ist, dass Aspose OCR Ihnen ermöglicht, **Text aus Bild zu extrahieren** *und* aus bestimmten Formularbereichen, indem Sie Polygone definieren. In diesem Tutorial sehen Sie genau, wie Sie **Text aus Formular**‑Felder mit Java extrahieren, warum dieser Ansatz wichtig ist und was Sie anpassen können, wenn etwas schiefgeht.

Im Folgenden behandeln wir alles, von der Einrichtung der Bibliothek bis zum Umgang mit kniffligen Randfällen, sodass Sie am Ende ein einsatzbereites Snippet haben, das nur die benötigten Daten extrahiert.

## Was Sie benötigen

- Java 17 (oder ein aktuelles JDK) – neuere Versionen bieten bessere Unicode‑Unterstützung.  
- Aspose.OCR für Java 23.10 (oder die neueste Version zum Zeitpunkt des Lesens).  
- Ein Beispielbild mit dem Namen `form.png`, das klar definierte Felder enthält.  
- Eine IDE oder ein einfacher Texteditor – IntelliJ IDEA, VS Code oder sogar Notepad reichen aus.

Für das Kern‑Demo ist keine Maven/Gradle‑Magie erforderlich; fügen Sie einfach die Aspose OCR‑JAR zu Ihrem Klassenpfad hinzu.

---

## Schritt 1 – OCR‑Engine initialisieren und Bild laden

Das Erste, was die Engine benötigt, ist ein Bitmap, auf dem sie arbeiten kann. Wir verweisen sie auf `form.png`, das im selben Ordner wie die Quelldatei liegt.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the source image – replace the path if your file lives elsewhere
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));
```

*Warum das wichtig ist:*  
Ein neues `OcrEngine`‑Objekt gibt Ihnen eine saubere Ausgangsbasis und stellt sicher, dass keine alten Einstellungen Ihren Durchlauf beeinflussen. Das frühe Laden des Bildes prüft zudem, ob die Datei existiert, sodass Sie eine hilfreiche Ausnahme erhalten, bevor Sie Zeit mit späteren Schritten verschwenden.

> **Pro‑Tipp:** Wenn Ihr Bild sehr groß ist (über 5 MB), sollten Sie es zuerst verkleinern. Aspose OCR arbeitet schneller mit Bildern, die in beiden Dimensionen unter 2000 px liegen.

## Schritt 2 – Polygone für die zu lesenden Felder definieren

Eine *Region of Interest* (ROI) ist einfach ein Polygon, das der Engine sagt, wo sie suchen soll. Unten erstellen wir zwei Rechtecke – eines für „Vorname“ und ein weiteres für „Geburtsdatum“. Passen Sie die Koordinaten an Ihr eigenes Formular an.

```java
        // Polygon for the first field (e.g., First Name)
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},   // X‑coordinates
                new int[]{100, 100, 150, 150}, // Y‑coordinates
                4);

        // Polygon for the second field (e.g., Date of Birth)
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);
```

*Warum Polygone statt Rechtecke?*  
Polygone bieten die Flexibilität, schiefe oder nicht‑rechteckige Felder zu verarbeiten – häufig bei gescannten Formularen, die nicht perfekt ausgerichtet sind.

## Schritt 3 – Aspose OCR nur auf diese Regionen fokussieren lassen

Jetzt binden wir die Polygone an die Engine. Die Methode `setRegionsOfInterest` akzeptiert eine Liste, sodass Sie beliebig viele Felder hinzufügen können.

```java
        // Limit OCR to the defined regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));
```

*Was passiert im Hintergrund?*  
Aspose OCR schneidet jedes Polygon zu einem separaten Bitmap zu, führt den Erkennungsalgorithmus aus und fügt anschließend die Ergebnisse zusammen. Dadurch werden Fehlalarme durch umliegende Grafiken drastisch reduziert.

## Schritt 4 – OCR‑Prozess ausführen

Nachdem alles konfiguriert ist, starten wir die OCR. Der Aufruf `process()` liefert ein `OcrResult`‑Objekt, das den extrahierten Text und die Konfidenzwerte enthält.

```java
        // Execute OCR on the selected ROIs
        OcrResult ocrResult = ocrEngine.process();
```

Wenn Sie pro Feld Konfidenz benötigen, können Sie `ocrResult.getRegions()` untersuchen – jede Region enthält ihren eigenen Score. Für die meisten einfachen Formulare reicht der Gesamtext aus.

## Schritt 5 – Extrahierten Text anzeigen (oder speichern)

Zum Schluss geben wir das Ergebnis in der Konsole aus. In einer echten Anwendung könnten Sie es in eine Datenbank, eine JSON‑Datei schreiben oder über eine API senden.

```java
        // Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Erwartete Ausgabe (Beispiel):**

```
=== Extracted Text ===
John Doe
12/04/1990
```

Die beiden Zeilen entsprechen den beiden definierten Polygonen. Wenn Sie überflüssige Leerzeichen sehen, entfernen Sie diese mit `String.trim()`.

## Wie man Text aus Formular extrahiert, wenn man viele Felder hat

Wenn ein Formular Dutzende Eingaben enthält, wird das manuelle Eingeben von Koordinaten mühsam. Hier ein schnelles Muster, das Sie übernehmen können:

1. **Erstellen Sie eine CSV**, in der jede Zeile `fieldName, x1, y1, x2, y2, x3, y3, x4, y4` enthält.  
2. **Laden Sie die CSV** zur Laufzeit, iterieren Sie über jede Zeile, bauen Sie ein `Polygon` und fügen Sie der ROI‑Liste hinzu.  

```java
List<Polygon> rois = new ArrayList<>();
try (BufferedReader br = new BufferedReader(new FileReader("fields.csv"))) {
    String line;
    while ((line = br.readLine()) != null) {
        String[] parts = line.split(",");
        int[] xs = { Integer.parseInt(parts[1]), Integer.parseInt(parts[3]),
                    Integer.parseInt(parts[5]), Integer.parseInt(parts[7]) };
        int[] ys = { Integer.parseInt(parts[2]), Integer.parseInt(parts[4]),
                    Integer.parseInt(parts[6]), Integer.parseInt(parts[8]) };
        rois.add(new Polygon(xs, ys, 4));
    }
}
ocrEngine.getEngineOptions().setRegionsOfInterest(rois);
```

*Warum das Ganze?*  
Die Automatisierung der ROI‑Erstellung ermöglicht die Wiederverwendung desselben Java‑Codes für verschiedene Formular‑Layouts und hält Ihr Projekt DRY (Don’t Repeat Yourself).

## Randfälle & Tipps, an die Sie vielleicht nicht gedacht haben

- **Gedrehte Scans:** Wenn das gesamte Bild gedreht ist, rufen Sie `ocrEngine.getEngineOptions().setRotateAngle(degrees)` auf.  
- **Geringer Kontrast:** Setzen Sie `ocrEngine.getEngineOptions().setContrast(1.5f)`, um die Lesbarkeit zu erhöhen.  
- **Nicht‑lateinische Schriften:** Wechseln Sie die Sprache mit `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.Spanish)` (oder einer anderen unterstützten Sprache).  
- **Teilweise OCR‑Fehler:** Prüfen Sie stets `ocrResult.getConfidence()`; fällt dieser unter 80 %, sollten Sie den Benutzer zur manuellen Überprüfung auffordern.  

## Vollständiges funktionierendes Beispiel (Copy‑Paste‑bereit)

Unten finden Sie das komplette Programm, bereit zum Kompilieren und Ausführen. Ersetzen Sie `YOUR_DIRECTORY` durch den Ordner, der `form.png` enthält.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Step 1 – Initialize engine and load image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));

        // Step 2 – Define polygons for each form field
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},
                new int[]{100, 100, 150, 150},
                4);
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);

        // Step 3 – Limit OCR to those regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));

        // Step 4 – Run OCR
        OcrResult ocrResult = ocrEngine.process();

        // Step 5 – Show the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Kompilieren mit:

```bash
javac -cp "aspose-ocr-23.10.jar" MultiRoiDemo.java
java -cp ".:aspose-ocr-23.10.jar" MultiRoiDemo
```

Sie sollten die beiden Textzeilen sehen, die zu den definierten ROIs gehören.

## Häufig gestellte Fragen

**F: Funktioniert das mit PDFs?**  
A: Nicht direkt. Konvertieren Sie jede PDF‑Seite zuerst in ein Bild (z. B. mit Aspose PDF) und übergeben Sie das Bild dann an die OCR‑Engine.

**F: Was ist, wenn mein Formular Checkboxen enthält?**  
A: OCR kann boolesche Zustände nicht lesen, aber Sie können den Checkbox‑Bereich als ROI behandeln und die Pixeldichte prüfen, um ein Häkchen zu ermitteln.

**F: Kann ich Text aus einem mehrseitigen Formular auf einmal extrahieren?**  
A: Durchlaufen Sie jedes Seitenbild, verwenden Sie dieselbe ROI‑Liste erneut und verketten Sie die Ergebnisse.

## Fazit

Wir haben eine vollständige End‑zu‑End‑Lösung für **Text aus Bild extrahieren** mit Aspose OCR durchgegangen und gezeigt, wie dieselbe Technik Ihnen ermöglicht, **Text aus Formular**‑Felder mit punktgenauer Genauigkeit zu extrahieren. Durch das Definieren von Polygonen, das Begrenzen des Fokus der Engine und das Handhaben gängiger Fallstricke erhalten Sie schnelle, saubere Daten ohne den Aufwand, das gesamte Bild zu verarbeiten.

Bereit für den nächsten Schritt? Versuchen Sie, die OCR‑Ausgabe in ein JSON‑Payload zu verketten oder an ein Machine‑Learning‑Modell zur Validierung zu übergeben. Der Himmel ist die Grenze, und jetzt Sie

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}