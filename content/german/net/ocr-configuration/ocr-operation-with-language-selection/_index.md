---
title: OCROperation mit Sprachauswahl bei der OCR-Bilderkennung
linktitle: OCROperation mit Sprachauswahl bei der OCR-Bilderkennung
second_title: Aspose.OCR .NET API
description: Nutzen Sie leistungsstarke OCR-Funktionen mit Aspose.OCR für .NET. Extrahieren Sie nahtlos Text aus Bildern.
type: docs
weight: 12
url: /de/net/ocr-configuration/ocr-operation-with-language-selection/
---
## Einführung

In der Welt der Bilderkennung und optischen Zeichenerkennung (OCR) zeichnet sich Aspose.OCR für .NET als leistungsstarkes Tool für Entwickler aus, die eine genaue und effiziente Textextraktion aus Bildern suchen. Diese Schritt-für-Schritt-Anleitung führt Sie durch den Prozess der OCR-Bilderkennung mit Aspose.OCR für .NET und konzentriert sich dabei auf die Bedienung mit Sprachauswahl.

## Voraussetzungen

Bevor wir uns mit dem Tutorial befassen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

-  Aspose.OCR für .NET: Stellen Sie sicher, dass die Aspose.OCR-Bibliothek installiert ist. Sie können es hier herunterladen[Aspose.OCR für .NET-Downloadseite](https://releases.aspose.com/ocr/net/).

- Entwicklungsumgebung: Richten Sie eine Arbeitsumgebung mit einer .NET-Anwendung ein. Wenn Sie dies noch nicht getan haben, lesen Sie die[Dokumentation](https://reference.aspose.com/ocr/net/) für detaillierte Anweisungen.

## Namespaces importieren

Beginnen Sie in Ihrer .NET-Anwendung mit dem Importieren der erforderlichen Namespaces:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Schritt 1: Aspose.OCR initialisieren

Beginnen Sie mit der Initialisierung einer Instanz der Aspose.OCR-Klasse. Dies schafft die Voraussetzungen für die Nutzung der OCR-Funktionen in Ihrer Anwendung.

```csharp
// ExStart:1
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "Your Document Directory";

// Initialisieren Sie eine Instanz von AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Schritt 2: Geben Sie den Bildpfad an

Definieren Sie als Nächstes den Pfad zu dem Bild, für das Sie OCR durchführen möchten. Stellen Sie sicher, dass das Bild über Ihre Anwendung zugänglich ist.

```csharp
//Bildpfad
string fullPath = dataDir + "sample.png";
```

## Schritt 3: Bild mit Sprachauswahl erkennen

Jetzt kommt der Kernvorgang der OCR. Nutzen Sie die Aspose.OCR-Bibliothek, um Text aus dem angegebenen Bild zu erkennen. Passen Sie die Erkennungseinstellungen an, einschließlich der Sprachauswahl.

```csharp
// Bild erkennen
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Wählen Sie die Sprache: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## Schritt 4: Ergebnisse drucken und anzeigen

Drucken Sie nach dem OCR-Vorgang die Ergebnisse aus und zeigen Sie sie an, einschließlich erkanntem Text, Bereichen, Warnungen und JSON-Darstellung.

```csharp
// Ergebnis drucken
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## Abschluss

Glückwunsch! Sie haben die OCR-Bilderkennung mit Sprachauswahl mit Aspose.OCR für .NET erfolgreich durchgeführt. In diesem Tutorial wurden die wesentlichen Schritte zum Extrahieren von Text aus Bildern demonstriert und die Flexibilität der Sprachoptionen hervorgehoben.

## FAQs

### F1: Ist Aspose.OCR für die mehrsprachige Texterkennung geeignet?

A1: Ja, Aspose.OCR unterstützt verschiedene Sprachen und bietet so Flexibilität für mehrsprachige OCR-Aufgaben.

### F2: Kann ich die OCR-Einstellungen für bestimmte Bildeigenschaften optimieren?

A2: Auf jeden Fall! Passen Sie Parameter wie Schräglaufwinkel, Linienerkennung und Bereichserkennung an, um die OCR für verschiedene Szenarien zu optimieren.

### F3: Wo finde ich zusätzlichen Support oder Community-Diskussionen?

 A3: Besuchen Sie die[Aspose.OCR-Forum](https://forum.aspose.com/c/ocr/16) für Unterstützung und Diskussionen mit der Community.

### F4: Gibt es eine kostenlose Testversion?

 A4: Ja, erkunden Sie das[Kostenlose Testphase](https://releases.aspose.com/) um die Möglichkeiten von Aspose.OCR kennenzulernen.

### F5: Wie kann ich Aspose.OCR für .NET erwerben?

 A5: Um zu kaufen, besuchen Sie die[Kaufseite](https://purchase.aspose.com/buy).
