---
category: general
date: 2026-01-12
description: Extrahieren Sie Text aus einem Bild mit Aspose OCR in Java. Erfahren
  Sie, wie Sie Text aus einem Rechnungsbild mit einem Java‑OCR‑Beispiel extrahieren
  und den ausgegebenen OCR‑Text erhalten.
draft: false
keywords:
- extract text from image
- how to extract text
- java ocr example
- process invoice image
- output ocr text
language: de
og_description: Extrahieren Sie Text aus einem Bild mit Aspose OCR in Java. Dieser
  Leitfaden zeigt, wie man Text aus einem Rechnungsbild extrahiert, enthält ein Java‑OCR‑Beispiel
  und gibt den OCR‑Text aus.
og_title: Text aus Bild in Java extrahieren – komplettes OCR-Beispiel
tags:
- OCR
- Java
- Aspose
title: Text aus Bild in Java extrahieren – Komplettes OCR‑Beispiel
url: /de/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild in Java extrahieren – Komplettes OCR-Beispiel

Haben Sie sich schon einmal gefragt, wie man **Text aus Bild** Dateien extrahiert, ohne sich die Haare zu raufen? Vielleicht haben Sie einen Stapel gescannter Rechnungen und benötigen die Zahlen schnell. Nach meiner Erfahrung ist der einfachste Weg, einer spezialisierten OCR‑Bibliothek die schwere Arbeit zu überlassen. Dieses Tutorial zeigt *wie man Text* aus einem typischen Rechnungsbild mit Aspose OCR für Java extrahiert und demonstriert ein **Java OCR Beispiel**, das den OCR‑Text ausgibt, den Sie in Ihr nachgelagertes System einspeisen können.

Wir gehen alles durch, was Sie wissen müssen: von der Einrichtung des Projekts, über die Definition des Regions of Interest (ROI), das sich auf die Kopfzeile und den Gesamtbetrag konzentriert, bis hin zum endgültigen Ausgeben des extrahierten Textes. Am Ende können Sie **Rechnungsbild verarbeiten** Dateien automatisch verarbeiten und sauberen, durchsuchbaren Text erhalten.

> **Was Sie erhalten:** ein sofort ausführbares Java‑Programm, klare Erklärungen zu jedem Schritt und praktische Tipps zum Umgang mit realen Rechnungen.

---

## Voraussetzungen

Bevor wir starten, stellen Sie sicher, dass Sie Folgendes haben:

- Java Development Kit (JDK) 8 oder neuer installiert.
- Maven oder Gradle für die Abhängigkeitsverwaltung (Maven‑Beispiel gezeigt).
- Eine Aspose OCR for Java Lizenz (die kostenlose Testversion funktioniert zum Testen).
- Ein Rechnungsbild (`invoice.png`) in einem bekannten Verzeichnis abgelegt.

Falls Ihnen das irgendwo unbekannt vorkommt, keine Sorge – die meisten Dinge sind nur einen Download entfernt, und der Code kompiliert auch mit der Community‑Edition.

---

## Schritt 1: Ihr Maven‑Projekt einrichten

Zuerst erstellen Sie ein neues Maven‑Projekt (oder fügen es einem bestehenden hinzu). In Ihrer `pom.xml` fügen Sie die Aspose OCR‑Abhängigkeit hinzu:

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Use the latest version available -->
    </dependency>
</dependencies>
```

> **Pro‑Tipp:** Halten Sie die Versionsnummer aktuell; neuere Releases verbessern häufig die Genauigkeit bei schwierigen Schriftarten, die auf Rechnungen vorkommen.

Nach dem Speichern der Datei führen Sie `mvn clean install` aus, um die Bibliothek in Ihr lokales Repository zu holen.

---

## Schritt 2: Das Rechnungsbild laden

Jetzt, wo die Bibliothek bereit ist, schreiben wir eine kleine Java‑Klasse. Das Erste, was wir tun, ist, eine `OcrEngine`‑Instanz zu erstellen und auf das Bild zu verweisen, das Sie lesen möchten.

```java
import com.aspose.ocr.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png"); // <-- replace with your path
```

Warum erstellen wir die Engine **vorher**, bevor das Bild geladen wird? Die Engine hält Konfigurationen wie Sprache, DPI und ROI. Das frühe Setzen des Bildes stellt sicher, dass diese Einstellungen auf die genaue Datei angewendet werden, die Sie gerade verarbeiten wollen.

---

## Schritt 3: Regionen von Interesse (ROI) definieren

Rechnungen enthalten oft viel Rauschen – Tabellen, Logos und Kleingedrucktes. Indem Sie die OCR auf nur die Kopfzeile und den Gesamtbetrag beschränken, steigern Sie sowohl Geschwindigkeit als auch Genauigkeit erheblich. Aspose lässt Sie diese Zonen mit Rechtecken beschreiben.

```java
        // Step 3: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Apply ROI to the engine
        engine.setRegion(region);
```

Die Koordinaten sind in Pixeln (`x`, `y`, `width`, `height`). Wenn Ihre Rechnungen unterschiedliche Größen haben, können Sie diese Werte dynamisch berechnen – etwa indem Sie zuerst die Bildabmessungen prüfen. Das ist eine nette Erweiterung, wenn Sie eine **Rechnungsbild verarbeiten** Lösung benötigen, die stapelweise funktioniert.

---

## Schritt 4: OCR auf den angegebenen Regionen ausführen

Mit dem ROI an Ort und Stelle kann die OCR‑Engine ihre Aufmerksamkeit dort fokussieren, wo es am wichtigsten ist. Die Methode `recognize()` liefert ein `OcrResult` mit dem extrahierten Text.

```java
        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();
```

Im Hintergrund führt Aspose mehrere Vorverarbeitungsschritte aus: Binarisierung, Rauschunterdrückung und Zeichen­segmentierung. Sie müssen diese nicht manuell aufrufen – lassen Sie einfach `recognize()` seine Arbeit tun.

---

## Schritt 5: Den extrahierten Text ausgeben

Zum Schluss geben wir den Text auf der Konsole aus. In einer echten Anwendung würden Sie ihn vielleicht in einer Datenbank speichern, in eine nachgelagerte Analyse‑Pipeline einspeisen oder sogar ein durchsuchbares PDF erzeugen.

```java
        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

Wenn Sie das Programm ausführen, sollten Sie etwa Folgendes sehen:

```
ROI text:
Acme Corp.
Invoice #12345
Date: 2025-12-31
Total Amount: $1,250.00
```

Sieht die Ausgabe verzerrt aus, prüfen Sie die Rechteckkoordinaten oder erhöhen Sie die Bildauflösung. OCR‑Engines lieben klare, hoch‑DPI‑Scans.

---

## Vollständiges funktionierendes Beispiel

Unten finden Sie die komplette, eigenständige Java‑Datei, die Sie in `src/main/java/RoiExample.java` einfügen können. Keine externen Snippets nötig – alles, was Sie brauchen, ist hier.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.region.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png");

        // Step 2: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Step 3: Apply the ROI configuration to the engine
        engine.setRegion(region);

        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

> **Hinweis:** Ersetzen Sie `YOUR_DIRECTORY` durch den absoluten Pfad zu Ihrem Rechnungsbild. Wenn Sie einen relativen Pfad verwenden, stellen Sie sicher, dass das Arbeitsverzeichnis dem Ort entspricht, von dem Sie den `java`‑Befehl ausführen.

---

## Häufige Fragen & Randfälle

### Was, wenn sich die Rechnungsgröße ändert?

Sie können das ROI dynamisch berechnen:

```java
int imgWidth = engine.getImage().getWidth();
int imgHeight = engine.getImage().getHeight();

int headerHeight = imgHeight / 10;
int totalHeight = imgHeight / 8;

OcrRegion region = OcrRegion.builder()
        .addRectangle(0, 0, imgWidth, headerHeight)
        .addRectangle(0, imgHeight - totalHeight, imgWidth, totalHeight)
        .build();
```

### Wie gehe ich mit mehreren Sprachen um?

Aspose OCR unterstützt Sprachpakete. Setzen Sie einfach die Sprache, bevor Sie `recognize()` aufrufen:

```java
engine.setLanguage(OcrLanguage.Spanish); // or OcrLanguage.English, etc.
```

### Was, wenn die OCR leere Zeichenketten zurückgibt?

Typische Ursachen sind:

- Niedrige Bildauflösung (< 300 DPI). Hochskalieren oder Scans höherer Qualität anfordern.
- Zu dunkle oder zu helle Hintergründe. Vor der OCR einen einfachen Kontrast‑Verbesserungsfilter anwenden.
- Falsche ROI‑Koordinaten, die den Text vollständig verfehlen.

---

## Tipps für produktionsreife OCR

1. **Batch Processing:** Verpacken Sie die Logik in einer Schleife, die über ein Verzeichnis von Rechnungsdateien iteriert. Loggen Sie jedes Ergebnis für Nachvollziehbarkeit.
2. **Error Handling:** Fangen Sie `OcrException`, um beschädigte Bilder elegant zu überspringen, ohne den gesamten Job zu stoppen.
3. **Performance:** Wiederverwenden Sie eine einzige `OcrEngine`‑Instanz für mehrere Bilder; das Erzeugen einer neuen Engine pro Datei verursacht unnötigen Overhead.
4. **Validation:** Nach der Extraktion führen Sie eine Regex‑Prüfung des Gesamtbetrags (`\$\d{1,3}(,\d{3})*(\.\d{2})?`) durch, um sicherzustellen, dass die Zahl realistisch aussieht.

Durch die Umsetzung dieser Vorschläge wird ein einfaches **Java OCR Beispiel** zu einer robusten, skalierbaren Lösung für jedes Unternehmen, das **Rechnungsbild verarbeiten** Dateien nachts verarbeitet.

---

## Fazit

Wir haben gerade gezeigt, wie man **Text aus Bild** Dateien in Java mit Aspose OCR extrahiert, wobei wir ein praktisches Szenario der Rechnungsverarbeitung betrachtet haben. Durch das Definieren eines Regions of Interest, das Ausführen der OCR‑Engine und das Ausgeben des **OCR‑Textes** haben Sie nun eine solide Basis, um automatisierte Datenerfassungs‑Pipelines zu bauen.

Nächste Schritte? Erweitern Sie das ROI, um Zeilen‑Artikel‑Tabellen einzuschließen, experimentieren Sie mit verschiedenen Spracheinstellungen oder leiten Sie die extrahierten Zeichenketten an eine PDF‑Generierungsbibliothek für durchsuchbare Dokumente weiter. Der Himmel ist das Limit, wenn Sie OCR mit modernem Java‑Tooling kombinieren.

Haben Sie weitere Fragen dazu, **wie man Text** aus anderen Dokumenttypen extrahiert, oder benötigen Sie Hilfe beim Anpassen des ROI für ungewöhnliche Layouts? Hinterlassen Sie einen Kommentar unten – happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}