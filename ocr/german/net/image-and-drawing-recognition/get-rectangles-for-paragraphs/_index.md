---
title: Erhalten Sie Rechtecke für Absätze in der OCR-Bilderkennung
linktitle: Erhalten Sie Rechtecke für Absätze in der OCR-Bilderkennung
second_title: Aspose.OCR .NET API
description: Nutzen Sie erweiterte OCR-Funktionen mit Aspose.OCR für .NET. Extrahieren Sie Absatzrechtecke mühelos.
weight: 11
url: /de/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Erhalten Sie Rechtecke für Absätze in der OCR-Bilderkennung

## Einführung

Willkommen zu unserem umfassenden Leitfaden zur Nutzung von Aspose.OCR für .NET zum Extrahieren von Absatzrechtecken in der OCR-Bilderkennung. Wenn Sie Ihre Dokumentverarbeitungsfähigkeiten verbessern und die Leistungsfähigkeit der optischen Zeichenerkennung (OCR) in Ihren .NET-Anwendungen nutzen möchten, sind Sie hier richtig.

## Voraussetzungen

Bevor wir uns mit dem Tutorial befassen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

- Grundkenntnisse in C#- und .NET-Entwicklung.
-  Eine mit Aspose.OCR für .NET eingerichtete Entwicklungsumgebung. Wenn Sie es noch nicht getan haben, können Sie es herunterladen[Hier](https://releases.aspose.com/ocr/net/).
- Ein Verständnis der Bildverarbeitungskonzepte und der Bedeutung von OCR beim Extrahieren von Text aus Bildern.

## Namespaces importieren

Stellen Sie sicher, dass in Ihrem C#-Code die erforderlichen Namespaces importiert sind, um Aspose.OCR effizient zu nutzen. Fügen Sie am Anfang Ihrer Datei Folgendes ein:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Schritt 1: Richten Sie Ihr Dokumentenverzeichnis ein

Beginnen Sie mit der Initialisierung des Pfads zu Ihrem Dokumentverzeichnis, in dem die Bilder für die OCR-Verarbeitung gespeichert sind:

```csharp
string dataDir = "Your Document Directory";
```

## Schritt 2: Initialisieren Sie die AsposeOcr-Instanz

Erstellen Sie eine Instanz der AsposeOcr-Klasse, um Zugriff auf OCR-Funktionen zu erhalten:

```csharp
AsposeOcr api = new AsposeOcr();
```

## Schritt 3: Geben Sie den Bildpfad an

Definieren Sie den vollständigen Pfad zu dem Bild, das Sie verarbeiten möchten:

```csharp
string fullPath = dataDir + "sample.png";
```

## Schritt 4: Bild erkennen und Absatzrechtecke abrufen

 Rufen Sie die auf`GetRectangles` Methode zum Erhalten von Rechtecken für Absätze im OCR-Bild. Satz`detect_areas` Zu`true` Wenn Sie Absätze extrahieren möchten:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## Schritt 5: Ergebnisse drucken

Drucken Sie die Koordinaten der identifizierten Bereiche aus:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## Schritt 6: Fazit

Glückwunsch! Sie haben den OCR-Bilderkennungsprozess erfolgreich ausgeführt, um mit Aspose.OCR für .NET Rechtecke für Absätze zu erhalten.

## Abschluss

In diesem Tutorial haben wir die grundlegenden Schritte zur Integration von Aspose.OCR für .NET in Ihre Anwendungen untersucht, sodass Sie Absatzrechtecke aus OCR-verarbeiteten Bildern extrahieren können. Aspose.OCR vereinfacht die Implementierung von OCR und macht es zu einem wertvollen Werkzeug für die Dokumentenverarbeitung und Textextraktion.

## FAQs

### F1: Ist Aspose.OCR mit verschiedenen Bildformaten kompatibel?

A1: Ja, Aspose.OCR unterstützt verschiedene Bildformate, darunter PNG, JPEG und TIFF.

### F2: Kann ich Aspose.OCR für die Stapelverarbeitung mehrerer Bilder verwenden?

A2: Auf jeden Fall! Aspose.OCR erleichtert die Stapelverarbeitung, um mehrere Bilder nahtlos zu verarbeiten.

### F3: Gibt es eine kostenlose Testversion für Aspose.OCR für .NET?

 A3: Ja, Sie können eine kostenlose Testversion ausprobieren[Hier](https://releases.aspose.com/).

### F4: Wie kann ich eine temporäre Lizenz für Aspose.OCR erhalten?

 A4: Sie können eine temporäre Lizenz erwerben[Hier](https://purchase.aspose.com/temporary-license/).

### F5: Wo finde ich zusätzliche Unterstützung und Diskussionen zu Aspose.OCR?

 A5: Gehen Sie rüber zum[Aspose.OCR-Forum](https://forum.aspose.com/c/ocr/16) für Community-Unterstützung und Diskussionen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
