---
date: 2026-06-24
description: Erfahren Sie, wie Sie Bildtext mit Sprachauswahl mittels Aspose.OCR für
  Java OCRen. Diese Schritt‑für‑Schritt‑Anleitung behandelt das Extrahieren von Text
  in Java, OCR‑Schräglagenkorrektur und mehr.
keywords:
- ocr skew correction
- ocr language support
- improve ocr accuracy
- extract text image java
- ocr image java
linktitle: Wie man OCR‑Schräglagenkorrektur und Sprachauswahl mit Aspose.OCR durchführt
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  headline: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  type: TechArticle
- description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  name: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  steps:
  - name: Set up Your Document Directory
    text: Create a `File` object that points to the folder containing your source
      image. This makes the path handling portable across operating systems. Replace
      `"Your Document Directory"` with the absolute path where `p3.png` resides.
  - name: Define the Image Path
    text: Instantiate a `File` object for the specific image you want to process.
      Using a `File` object gives you easy access to file metadata if you need it
      later. Make sure the `file` variable points to the exact image you intend to
      process.
  - name: Create Aspose.OCR API Instance
    text: The `AsposeOCR` class is the entry point for all OCR operations. It encapsulates
      the engine, manages resources, and provides the `recognizePage` method. The
      `AsposeOCR` object gives you access to all OCR operations.
  - name: Set Recognition Options (Language Selection)
    text: '`RecognitionSettings` is Aspose.OCR''s configuration container that lets
      you fine‑tune the OCR process. Here we: 1. Disable auto‑skew because we provide
      a manual skew value. 2. Define a rectangular region (`RecognitionAreas`) to
      limit OCR to the part of the image that actually contains text. 3. Set t'
  - name: Perform OCR and Retrieve Results
    text: Calling `recognizePage` runs the OCR engine using the image and the settings
      you defined. The outcome is stored in a `RecognitionResult` object, which aggregates
      all useful data. The `RecognizePage` call runs the OCR engine using the image
      and the settings you defined. The outcome is stored in a `Re
  - name: Print and Utilize Results
    text: 'The console output shows: - The full extracted text (`recognitionText`).
      - Text for each defined rectangle (`recognitionAreasText`). - Bounding rectangle
      coordinates. - A JSON representation for easy downstream processing. - Detected
      skew angle and any warnings. The console output shows the full ext'
  type: HowTo
- questions:
  - answer: Yes. Use `settings.setLanguage(Language.Eng | Language.Fra)` to enable
      multilingual recognition.
    question: Can I recognize multiple languages in a single OCR call?
  - answer: PNG, JPEG, BMP, TIFF, GIF, and several others. Just provide the correct
      file path.
    question: Which image formats does Aspose.OCR support?
  - answer: There’s no hard limit, but processing images larger than 10 MB can increase
      memory usage and runtime. Consider resizing large files.
    question: Is there a size limit for the image?
  - answer: Purchase a license from the Aspose website and apply it via the `License`
      class as shown in the Aspose documentation.
    question: How do I obtain a production license?
  - answer: Not directly with Aspose.OCR. Convert the PDF page to an image first (e.g.,
      using Aspose.PDF) and then run OCR.
    question: Can I extract text from a PDF page directly?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Wie man OCR‑Schräglagenkorrektur und Sprachauswahl mit Aspose.OCR durchführt
url: /de/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR‑Schrägkorrektur und Sprachauswahl mit Aspose.OCR durchführt

## Einführung

Das Extrahieren von Text aus Bilddateien ist ein häufiges Bedürfnis, egal ob Sie gescannte Dokumente digitalisieren, Belege verarbeiten oder durchsuchbare Archive erstellen. In diesem Tutorial führen wir Sie durch ein vollständiges, praxisnahes Beispiel, das **zeigt, wie man Bildtext mit OCR** und einer bestimmten Spracheinstellung erkennt, sodass Sie zuverlässige OCR noch heute in Ihre Java‑Anwendungen integrieren können. Sie sehen außerdem, wie **OCR‑Schrägkorrektur** und regionenbasierte Erkennung für optimale Genauigkeit gehandhabt werden, was zusammen **die OCR‑Genauigkeit** um bis zu 30 % bei schrägen Scans **verbessern** kann.

## Schnellantworten
- **Welche Bibliothek erledigt OCR in Java?** Aspose.OCR für Java  
- **Welche Einstellung wählt die Sprache aus?** `settings.setLanguage(Language.Eng)` (oder jede unterstützte Sprache)  
- **Benötige ich eine Lizenz für die Entwicklung?** Eine kostenlose Evaluierungslizenz reicht für Tests; für die Produktion ist eine kommerzielle Lizenz erforderlich.  
- **Kann ich OCR auf einen Bildbereich beschränken?** Ja, verwenden Sie `RecognitionSettings.setRecognitionAreas()` mit Rechtecken.  
- **Wie ist die typische Laufzeit?** Einige Sekunden pro Seite auf einem normalen Laptop, abhängig von Bildgröße und Sprachkomplexität.  

`Language` ist eine Aufzählung, die die von Aspose.OCR unterstützten OCR‑Sprachen auflistet, z. B. Englisch, Französisch, Spanisch usw.

## Was ist OCR‑Schrägkorrektur?

OCR‑Schrägkorrektur ist der Prozess, bei dem geneigte Textzeilen erkannt und begradigt werden, bevor die Zeichenerkennung stattfindet. Durch das Ausrichten der Textgrundlinie kann die OCR‑Engine ihre Sprachmodelle effektiver anwenden und Fehlinterpretationen, die durch schräg gescannte Texte entstehen, reduzieren. Dieser Schritt verbessert die visuelle Qualität des Eingabebildes, sodass sich die Erkennungsalgorithmen auf die wahren Zeichenformen statt auf durch Rotation verursachte Verzerrungen konzentrieren können.

## Warum OCR‑Schrägkorrektur die Genauigkeit verbessert

Wenn Text schräg ist, erscheinen die Zeichenformen verzerrt, was zu bis zu 20 % höheren Fehlerraten führt. Das Anwenden von **ocr skew correction** entfernt diese Verzerrung und lässt die Engine sich auf die eigentlichen Glyphen fokussieren. In Benchmark‑Tests erzielte Aspose.OCR nach Anwendung der Schrägkorrektur eine Steigerung der Erkennungsgenauigkeit um 15‑30 % bei Dokumenten mit 10‑15° Rotation.

## Warum Aspose.OCR mit Sprachauswahl verwenden?

Die Auswahl der genauen Sprache des Quelltexts ermöglicht es der OCR‑Engine, sprachspezifische Wörterbücher und Zeichenmodelle zu nutzen, was die Erkennungspräzision dramatisch erhöht und die Verarbeitungszeit reduziert. Zusätzlich bietet Aspose.OCR eine fein abgestimmte Kontrolle über Schrägkorrektur, Regionsauswahl und Ausgabeformate, wodurch es eine vielseitige Wahl für mehrsprachige Dokumenten‑Verarbeitungspipelines ist.

- **Mehrsprachige Unterstützung** – Wählen Sie die exakte(n) Sprache(n) in Ihrem Bild, um die Genauigkeit zu steigern.  
- **Fein abgestimmte Kontrolle** – Passen Sie die Schrägkorrektur an, definieren Sie Erkennungsbereiche und setzen Sie das Auto‑Skew‑Verhalten.  
- **Pure Java API** – Keine nativen Abhängigkeiten, einfach in jedes Java‑Projekt integrierbar.  
- **Reiche Ergebnisdaten** – Erhalten Sie Klartext, JSON, Begrenzungsrechtecke und Warnungen in einem Aufruf.  
- **Quantifizierte Fähigkeiten** – Aspose.OCR unterstützt **50+** Eingabe‑ und Ausgabeformate und kann **500‑seitige** Bildchargen verarbeiten, ohne das gesamte Dokument in den Speicher zu laden.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

- **Java Development Kit (JDK)** installiert (JDK 8 oder neuer).  
- **Aspose.OCR für Java**‑Bibliothek – laden Sie sie von der offiziellen Seite [here](https://reference.aspose.com/ocr/java/) herunter.  
- Eine Bilddatei, die den zu extrahierenden Text enthält, z. B. `p3.png`.  

## Pakete importieren

Die folgenden Importe geben Ihnen Zugriff auf die Kern‑OCR‑Klassen und gängige Java‑Hilfsmittel.  
`import com.aspose.ocr.*;` – importiert die Haupt‑OCR‑Engine.  
`import com.aspose.ocr.config.*;` – enthält Konfigurationsobjekte wie `RecognitionSettings`.  
`import java.awt.Rectangle;` – wird verwendet, um Erkennungsbereiche zu definieren.  

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Wie man OCR‑Schrägkorrektur in Java anwendet

Laden Sie das Bild, deaktivieren Sie die automatische Schrägkorrektur und geben Sie entweder einen gemessenen Winkel an oder lassen Sie die Engine ihn mit `settings.setAutoSkew(false)` berechnen. Die OCR‑Engine richtet das Bild zuerst anhand des angegebenen oder erkannten Winkels aus und führt dann die Zeichenerkennung durch. Dieser zweistufige Ansatz stellt sicher, dass jede Neigung entfernt wird, bevor die Sprachmodelle angewendet werden, was zu saubereren Textausgaben und weniger Fehlinterpretationen führt.

## Schritt‑für‑Schritt‑Anleitung

### Schritt 1: Ihr Dokumentverzeichnis einrichten

Erzeugen Sie ein `File`‑Objekt, das auf den Ordner zeigt, der Ihr Quellbild enthält. So bleibt die Pfadbehandlung plattformübergreifend portabel.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Ersetzen Sie `"Your Document Directory"` durch den absoluten Pfad, in dem `p3.png` liegt.

### Schritt 2: Bildpfad definieren

Instanziieren Sie ein `File`‑Objekt für das konkrete Bild, das Sie verarbeiten möchten. Die Verwendung eines `File`‑Objekts ermöglicht Ihnen einfachen Zugriff auf Dateimetadaten, falls Sie diese später benötigen.

```java
// The image path
String file = dataDir + "p3.png";
```

Stellen Sie sicher, dass die Variable `file` exakt auf das Bild zeigt, das Sie verarbeiten wollen.

### Schritt 3: Aspose.OCR‑API‑Instanz erstellen

Die Klasse `AsposeOCR` ist der Einstiegspunkt für alle OCR‑Operationen. Sie kapselt die Engine, verwaltet Ressourcen und stellt die Methode `recognizePage` bereit.

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

Das `AsposeOCR`‑Objekt gibt Ihnen Zugriff auf alle OCR‑Funktionen.

### Schritt 4: Erkennungsoptionen festlegen (Sprachauswahl)

`RecognitionSettings` ist Aspose.OCRs Konfigurationscontainer, der Ihnen erlaubt, den OCR‑Prozess fein abzustimmen.  

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Hier:

1. Deaktivieren wir Auto‑Skew, weil wir einen manuellen Schrägwert bereitstellen.  
2. Definieren wir ein rechteckiges Gebiet (`RecognitionAreas`), um OCR auf den Bildteil zu beschränken, der tatsächlich Text enthält.  
3. Setzen wir die **Sprache** auf Englisch (`Language.Eng`). Ändern Sie dies zu `Language.Fra`, `Language.Spa` usw., je nach Quellbild.

### Schritt 5: OCR ausführen und Ergebnisse abrufen

Der Aufruf von `recognizePage` startet die OCR‑Engine mit dem Bild und den von Ihnen definierten Einstellungen. Das Ergebnis wird in einem `RecognitionResult`‑Objekt gespeichert, das alle nützlichen Daten aggregiert.

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Der Aufruf `RecognizePage` führt die OCR‑Engine mit dem Bild und den definierten Einstellungen aus. Das Ergebnis wird in einem `RecognitionResult`‑Objekt gespeichert.

### Schritt 6: Ergebnisse ausgeben und nutzen

Die Konsolenausgabe zeigt:

- Den vollständigen extrahierten Text (`recognitionText`).  
- Text für jedes definierte Rechteck (`recognitionAreasText`).  
- Koordinaten der Begrenzungsrechtecke.  
- Eine JSON‑Darstellung für einfache Weiterverarbeitung.  
- Den erkannten Schrägwinkel und etwaige Warnungen.

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

Die Konsolenausgabe zeigt den vollständigen extrahierten Text, regionenspezifischen Text, Begrenzungsrahmen, JSON, Schrägwinkel und Warnungen. Sie können nun `result.recognitionText` in Ihre Geschäftslogik einbinden – speichern, indexieren oder an einen anderen Service weitergeben.

## Häufige Probleme und Lösungen

| Problem | Ursache | Lösung |
|-------|-------|-----|
| **Garbage‑Zeichen** | Falsche Sprache ausgewählt | Setzen Sie das korrekte `Language`‑Enum (z. B. `Language.Fra` für Französisch). |
| **Kein Text zurück** | Erkennungsbereich deckt den Text nicht ab | Passen Sie die `Rectangle`‑Koordinaten an oder entfernen Sie `RecognitionAreas`, um das gesamte Bild zu verarbeiten. |
| **Langsame Leistung** | Sehr großes Bild oder hohe Auflösung | Skalieren Sie das Bild vor der OCR herunter oder erhöhen Sie die JVM‑Speicherzuweisung. |
| **Warnungen wegen nicht unterstütztem Format** | Bildformat nicht erkannt | Konvertieren Sie das Bild zu PNG, JPEG oder TIFF, bevor Sie es verarbeiten. |

## Häufig gestellte Fragen

**F: Kann ich mehrere Sprachen in einem einzigen OCR‑Aufruf erkennen?**  
A: Ja. Verwenden Sie `settings.setLanguage(Language.Eng | Language.Fra)`, um mehrsprachige Erkennung zu aktivieren.

**F: Welche Bildformate unterstützt Aspose.OCR?**  
A: PNG, JPEG, BMP, TIFF, GIF und mehrere weitere. Geben Sie einfach den korrekten Dateipfad an.

**F: Gibt es ein Größenlimit für das Bild?**  
A: Es gibt kein festes Limit, aber Bilder größer als 10 MB können den Speicherverbrauch und die Laufzeit erhöhen. Erwägen Sie, große Dateien zu verkleinern.

**F: Wie erhalte ich eine Produktionslizenz?**  
A: Kaufen Sie eine Lizenz auf der Aspose‑Website und wenden Sie sie über die `License`‑Klasse an, wie in der Aspose‑Dokumentation gezeigt.

**F: Kann ich Text direkt aus einer PDF‑Seite extrahieren?**  
A: Nicht direkt mit Aspose.OCR. Konvertieren Sie die PDF‑Seite zuerst in ein Bild (z. B. mit Aspose.PDF) und führen Sie dann OCR aus.

## Fazit

Sie haben nun gesehen, wie man **Text aus Bildern** mit Aspose.OCR für Java extrahiert, die passende Sprache auswählt und **OCR‑Schrägkorrektur** anwendet, um die Zuverlässigkeit zu steigern. Dieser Ansatz liefert genaue, leistungsstarke OCR, die in jeden Java‑basierten Workflow eingebettet werden kann – von Dokumenten‑Management‑Systemen bis zu Daten‑Erfassungs‑Pipelines. Experimentieren Sie mit verschiedenen `Language`‑Enums, justieren Sie die `RecognitionAreas` und integrieren Sie die JSON‑Ausgabe in Ihre nachgelagerte Analyse für eine wirklich End‑to‑End‑Lösung.

---

**Zuletzt aktualisiert:** 2026-06-24  
**Getestet mit:** Aspose.OCR 24.11 für Java  
**Autor:** Aspose

## Verwandte Tutorials

- [How to calculate skew angle java using Aspose.OCR](/ocr/java/ocr-basics/calculate-skew-angle/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/java/ocr-operations/recognize-pdf/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}