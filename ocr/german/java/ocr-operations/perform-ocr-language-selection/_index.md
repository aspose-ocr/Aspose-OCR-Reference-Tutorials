---
date: 2026-02-12
description: Erfahren Sie, wie Sie Bildtext mit Sprachauswahl mithilfe von Aspose.OCR
  für Java OCRen. Dieser Schritt‑für‑Schritt‑Leitfaden behandelt das Extrahieren von
  Text in Java, die Korrektur von Schräglagen beim OCR und mehr.
linktitle: How to OCR Image Text with Language Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Wie man Bildtext mit Sprache mittels Aspose.OCR OCRt
url: /de/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Bildtext mit Sprache mithilfe von Aspose.OCR erkennt

## Einführung

Das Extrahieren von Text aus Bilddateien ist ein häufiges Bedürfnis, egal ob Sie gescannte Dokumente digitalisieren, Belege verarbeiten oder durchsuchbare Archive erstellen. In diesem Tutorial führen wir Sie durch ein vollständiges, praxisnahes Beispiel, das **zeigt, wie man Bildtext OCR‑t** mit einer bestimmten Spracheinstellung, sodass Sie zuverlässige OCR noch heute in Ihre Java‑Anwendungen integrieren können. Außerdem sehen Sie, wie Sie OCR‑Schrägkorrektur und regionsbasierte Erkennung für optimale Genauigkeit handhaben.

## Schnelle Antworten
- **Welche Bibliothek übernimmt OCR in Java?** Aspose.OCR for Java  
- **Welche Einstellung wählt die Sprache aus?** `settings.setLanguage(Language.Eng)` (oder jede unterstützte Sprache)  
- **Benötige ich eine Lizenz für die Entwicklung?** Eine kostenlose Evaluierungslizenz funktioniert für Tests; für die Produktion ist eine kommerzielle Lizenz erforderlich.  
- **Kann ich OCR auf einen Bildbereich beschränken?** Ja, verwenden Sie `RecognitionSettings.setRecognitionAreas()` mit Rechtecken.  
- **Wie lange dauert die Ausführung typischerweise?** Ein paar Sekunden pro Seite auf einem Standard‑Laptop, abhängig von Bildgröße und Sprachkomplexität.

## Wie man Bildtext mit Sprachauswahl OCR‑t
In diesem Abschnitt beantworten wir die Kernfrage **wie man ein Bild OCR‑t**, wenn die Sprache des Textes bekannt ist. Die Auswahl der richtigen Sprache verbessert die Erkennungsgenauigkeit erheblich, da die OCR‑Engine sprachspezifische Wörterbücher und Zeichenmodelle anwenden kann.

### Warum das wichtig ist
- **Höhere Genauigkeit** – sprachspezifische Modelle reduzieren Fehlinterpretationen.  
- **Leistungssteigerung** – die Engine überspringt unnötige Sprachprüfungen.  
- **Bessere Behandlung von Diakritika** – Französisch, Spanisch, Deutsch usw. werden korrekt erkannt, wenn das passende `Language`‑Enum verwendet wird.

## Was bedeutet „Text aus Bild extrahieren“?
Das Extrahieren von Text aus einem Bild (OCR) wandelt die visuelle Darstellung von Zeichen in maschinenlesbare Zeichenketten um. Dies ermöglicht Such‑, Analyse‑ und Datenextraktions‑Workflows, die sonst manuelle Transkription erfordern würden.

## Warum Aspose.OCR mit Sprachauswahl verwenden?
- **Mehrsprachige Unterstützung** – Wählen Sie die exakte Sprache(n) im Bild, um die Genauigkeit zu steigern.  
- **Fein abgestimmte Kontrolle** – Passen Sie Schrägkorrektur an, definieren Sie Erkennungsbereiche und setzen Sie das Auto‑Skew‑Verhalten.  
- **Pure Java API** – Keine nativen Abhängigkeiten, einfach in jedes Java‑Projekt integrierbar.  
- **Reiche Ergebnisdaten** – Erhalten Sie Klartext, JSON, Begrenzungsrechtecke und Warnungen in einem Aufruf.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

- **Java Development Kit (JDK)** installiert (JDK 8 oder neuer).  
- **Aspose.OCR for Java** Bibliothek – laden Sie sie von der offiziellen Seite [here](https://reference.aspose.com/ocr/java/) herunter.  
- Eine Bilddatei, die den zu extrahierenden Text enthält, z. B. `p3.png`.

## Pakete importieren

In Ihrer Java‑Quelldatei fügen Sie die erforderlichen Aspose.OCR‑Klassen und gängige Java‑Utilities ein:

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

## Schritt‑für‑Schritt‑Anleitung

### Schritt 1: Dokumentverzeichnis einrichten

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Ersetzen Sie `"Your Document Directory"` durch den absoluten Pfad, in dem sich `p3.png` befindet.

### Schritt 2: Bildpfad definieren

```java
// The image path
String file = dataDir + "p3.png";
```

Stellen Sie sicher, dass die Variable `file` exakt auf das Bild zeigt, das Sie verarbeiten möchten.

### Schritt 3: Aspose.OCR API‑Instanz erstellen

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

Das Objekt `AsposeOCR` gibt Ihnen Zugriff auf alle OCR‑Operationen.

### Schritt 4: Erkennungsoptionen festlegen (Sprachauswahl)

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

1. Deaktivieren Sie auto‑skew, weil wir einen manuellen Schrägwinkelwert bereitstellen.  
2. Definieren Sie einen rechteckigen Bereich (`RecognitionAreas`), um OCR auf den Teil des Bildes zu beschränken, der tatsächlich Text enthält.  
3. Setzen Sie die **Sprache** auf Englisch (`Language.Eng`). Ändern Sie dies zu `Language.Fra`, `Language.Spa` usw., je nach Quellbild.

### Schritt 5: OCR ausführen und Ergebnisse abrufen

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Der Aufruf `RecognizePage` startet die OCR‑Engine mit dem Bild und den von Ihnen definierten Einstellungen. Das Ergebnis wird in einem `RecognitionResult`‑Objekt gespeichert.

### Schritt 6: Ergebnisse ausgeben und nutzen

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

Die Konsolenausgabe zeigt:

- Den vollständig extrahierten Text (`recognitionText`).  
- Text für jedes definierte Rechteck (`recognitionAreasText`).  
- Koordinaten des Begrenzungsrechtecks.  
- Eine JSON‑Darstellung für einfache nachgelagerte Verarbeitung.  
- Erkannten Schrägwinkel und etwaige Warnungen.

Sie können nun `result.recognitionText` in Ihre Geschäftslogik einfließen lassen – speichern, indexieren oder an einen anderen Service weitergeben.

## Häufige Probleme und Lösungen

| Problem | Ursache | Lösung |
|---------|---------|--------|
| **Garbage characters** | Falsche Sprache ausgewählt | Setzen Sie das korrekte `Language`‑Enum (z. B. `Language.Fra` für Französisch). |
| **No text returned** | Der Erkennungsbereich deckt den Text nicht ab | Passen Sie die `Rectangle`‑Koordinaten an oder entfernen Sie `RecognitionAreas`, um das gesamte Bild zu verarbeiten. |
| **Slow performance** | Sehr großes Bild oder hohe Auflösung | Skalieren Sie das Bild vor der OCR herunter oder erhöhen Sie die Speicherzuweisung für die JVM. |
| **Warnings about unsupported format** | Bildformat nicht erkannt | Konvertieren Sie das Bild vor der Verarbeitung zu PNG, JPEG oder TIFF. |

## FAQ

**Q: Kann ich mehrere Sprachen in einem einzigen OCR‑Aufruf erkennen?**  
A: Ja. Verwenden Sie `settings.setLanguage(Language.Eng | Language.Fra)`, um mehrsprachige Erkennung zu aktivieren.

**Q: Welche Bildformate unterstützt Aspose.OCR?**  
A: PNG, JPEG, BMP, TIFF, GIF und mehrere weitere. Geben Sie einfach den korrekten Dateipfad an.

**Q: Gibt es ein Größenlimit für das Bild?**  
A: Es gibt kein festes Limit, aber sehr große Bilder erhöhen den Speicherverbrauch und die Verarbeitungszeit. Erwägen Sie, große Dateien zu verkleinern.

**Q: Wie erhalte ich eine Produktionslizenz?**  
A: Kaufen Sie eine Lizenz auf der Aspose‑Website und wenden Sie sie über die `License`‑Klasse an, wie in der Aspose‑Dokumentation gezeigt.

**Q: Kann ich Text direkt aus einer PDF‑Seite extrahieren?**  
A: Nicht direkt mit Aspose.OCR. Konvertieren Sie die PDF‑Seite zuerst in ein Bild (z. B. mit Aspose.PDF) und führen Sie dann OCR aus.

## Fazit

Sie haben nun gesehen, **wie man Text aus einem Bild extrahiert** mit Aspose.OCR für Java, dabei die passende Sprache auswählt und die Erkennung auf bestimmte Regionen beschränkt. Dieser Ansatz liefert genaue, leistungsstarke OCR, die in jeden Java‑basierten Workflow eingebettet werden kann – von Dokumentenmanagement‑Systemen bis hin zu Daten‑Erfassungs‑Pipelines. Bereit für den nächsten Schritt? Probieren Sie verschiedene `Language`‑Enums, experimentieren Sie mit unterschiedlichen Erkennungsbereichen und integrieren Sie die Ergebnisse in Ihre eigene Anwendungslogik.

---

**Last Updated:** 2026-02-12  
**Tested With:** Aspose.OCR 24.11 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}