---
title: Durchführen von OCR mit Sprachauswahl in Aspose.OCR
linktitle: Durchführen von OCR mit Sprachauswahl in Aspose.OCR
second_title: Aspose.OCR Java-API
description: Nutzen Sie die präzise Textextraktion aus Bildern mit Aspose.OCR für Java. Befolgen Sie unsere Schritt-für-Schritt-Anleitung für eine genaue OCR mit Sprachauswahl.
type: docs
weight: 11
url: /de/java/ocr-operations/perform-ocr-language-selection/
---
## Einführung

In der sich ständig weiterentwickelnden Technologielandschaft spielt die optische Zeichenerkennung (OCR) eine zentrale Rolle bei der Extraktion aussagekräftiger Informationen aus Bildern. Aspose.OCR für Java zeichnet sich durch ein leistungsstarkes Tool aus, mit dem Entwickler OCR-Funktionen nahtlos in ihre Java-Anwendungen integrieren können. In dieser Schritt-für-Schritt-Anleitung erfahren Sie, wie Sie mit Aspose.OCR OCR mit Sprachauswahl durchführen und so das Potenzial für die präzise Verarbeitung verschiedener Inhalte freisetzen.

## Voraussetzungen

Bevor Sie mit dem Tutorial beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

- Java-Entwicklungsumgebung: Stellen Sie sicher, dass Java auf Ihrem System installiert und Ihre Entwicklungsumgebung eingerichtet ist.

-  Aspose.OCR-Bibliothek: Laden Sie die Aspose.OCR-Bibliothek für Java herunter und installieren Sie sie. Hier finden Sie die Bibliothek und die zugehörige Dokumentation[Hier](https://reference.aspose.com/ocr/java/).

- Bilddatei: Bereiten Sie eine Bilddatei mit dem Text vor, den Sie extrahieren möchten. Verwenden wir beispielsweise eine Datei mit dem Namen „p3.png“.

## Pakete importieren

Importieren Sie in Ihrem Java-Projekt die erforderlichen Pakete, um die Aspose.OCR-Funktionalität zu nutzen. Fügen Sie am Anfang Ihrer Java-Datei die folgenden Zeilen hinzu:

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

## Schritt 1: Richten Sie Ihr Dokumentenverzeichnis ein

```java
// Der Pfad zum Dokumentenverzeichnis.
String dataDir = "Your Document Directory";
```

Ersetzen Sie „Ihr Dokumentverzeichnis“ durch den tatsächlichen Pfad zu dem Verzeichnis, in dem sich Ihre Bilddatei befindet.

## Schritt 2: Definieren Sie den Bildpfad

```java
// Der Bildpfad
String file = dataDir + "p3.png";
```

Passen Sie die Dateivariable so an, dass sie auf Ihre spezifische Bilddatei verweist.

## Schritt 3: Erstellen Sie eine Aspose.OCR-API-Instanz

```java
// Erstellen Sie eine API-Instanz
AsposeOCR api = new AsposeOCR();
```

Initialisieren Sie das AsposeOCR-Objekt, um auf seine Funktionen zuzugreifen.

## Schritt 4: Erkennungsoptionen festlegen

```java
// Erkennungsoptionen festlegen
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Passen Sie die Erkennungseinstellungen entsprechend Ihren Anforderungen an. Passen Sie Parameter wie Neigung, Sprache und Erkennungsbereiche an.

## Schritt 5: OCR durchführen und Ergebnisse abrufen

```java
// Ergebnisobjekt abrufen
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Führen Sie den OCR-Vorgang mit der angegebenen Bilddatei und den angegebenen Einstellungen aus. Erfassen Sie das Ergebnis im RecognitionResult-Objekt.

## Schritt 6: Ergebnisse ausdrucken und nutzen

```java
// Ergebnis drucken
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

Drucken Sie den extrahierten Text, die Erkennungsbereiche, die JSON-Darstellung, den Schräglaufwinkel und alle Warnungen. Nutzen Sie die Ergebnisse nach Bedarf in Ihrer Bewerbung.

## Abschluss

In diesem Tutorial haben wir uns mit der nahtlosen Integration von Aspose.OCR für Java befasst, um OCR mit Sprachauswahl durchzuführen. Diese leistungsstarke Bibliothek eröffnet Entwicklern, die Text präzise aus Bildern extrahieren möchten, eine Welt voller Möglichkeiten.

## FAQs

### F1: Kann ich Aspose.OCR für mehrere Sprachen in einem einzigen Erkennungsprozess verwenden?

A1: Ja, Sie können in den RecognitionSettings mehrere Sprachen festlegen, um die Erkennungsgenauigkeit für mehrsprachige Inhalte zu verbessern.

### F2: Wie kann ich mit Aspose.OCR mit verschiedenen Bildformaten umgehen?

A2: Aspose.OCR unterstützt verschiedene Bildformate, darunter PNG, JPEG und TIFF. Geben Sie einfach den richtigen Dateipfad in der Bildpfadvariablen an.

### F3: Gibt es eine Grenze für die Größe des Bildes, das Aspose.OCR verarbeiten kann?

A3: Aspose.OCR kann Bilder unterschiedlicher Größe verarbeiten, größere Bilder erfordern jedoch möglicherweise mehr Verarbeitungszeit und Ressourcen.

### F4: Kann ich die Erkennungseinstellungen für bestimmte Bereiche innerhalb eines Bildes optimieren?

A4: Auf jeden Fall. Nutzen Sie die RecognitionAreas-Funktion, um bestimmte Rechtecke innerhalb des Bildes für eine gezielte Erkennung zu definieren.

### F5: Ist Aspose.OCR sowohl für private als auch für kommerzielle Projekte geeignet?

A5: Ja, Aspose.OCR bietet flexible Lizenzoptionen, sodass es sowohl für den persönlichen als auch für den kommerziellen Gebrauch geeignet ist.