---
title: Bereiten Sie Rechtecke in der OCR-Bilderkennung vor
linktitle: Bereiten Sie Rechtecke in der OCR-Bilderkennung vor
second_title: Aspose.OCR .NET API
description: Nutzen Sie das Potenzial von Aspose.OCR für .NET mit unserem umfassenden Leitfaden. Erfahren Sie Schritt für Schritt, wie Sie Rechtecke für die Bilderkennung vorbereiten. Erweitern Sie Ihre .NET-Anwendungen durch nahtlose OCR-Integration.
weight: 11
url: /de/net/ocr-optimization/prepare-rectangles/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bereiten Sie Rechtecke in der OCR-Bilderkennung vor

## Einführung

In der sich ständig weiterentwickelnden Technologielandschaft spielt die optische Zeichenerkennung (OCR) eine zentrale Rolle bei der Umwandlung von Bildern in maschinenlesbaren Text. Aspose.OCR für .NET zeichnet sich als robuste Lösung für Entwickler aus, die eine nahtlose Integration von OCR-Funktionen in ihre .NET-Anwendungen suchen. In diesem umfassenden Leitfaden untersuchen wir den Prozess der Vorbereitung von Rechtecken bei der OCR-Bilderkennung mit Aspose.OCR für .NET.

## Voraussetzungen

Bevor Sie mit dem Tutorial beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

- Grundkenntnisse in der .NET-Entwicklung.
-  Aspose.OCR für .NET-Bibliothek installiert. Sie können es herunterladen[Hier](https://releases.aspose.com/ocr/net/).
- Ein grundlegendes Verständnis der Bilderkennungskonzepte.

## Namespaces importieren

Beginnen wir mit dem Importieren der erforderlichen Namespaces, um unsere OCR-Reise in Gang zu bringen:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Schritt 1: Richten Sie Ihr Dokumentenverzeichnis ein

 Geben Sie zunächst das Verzeichnis an, in dem Ihre Dokumente gespeichert sind. Ersetzen`"Your Document Directory"` mit dem tatsächlichen Pfad zu Ihren Dokumenten.

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "Your Document Directory";

// Initialisieren Sie eine Instanz von AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Schritt 2: Bild mit mehreren Rechtecken erkennen

In diesem Schritt zeigen wir, wie man mithilfe mehrerer Rechtecke Text aus einem Bild erkennt. Befolgen Sie diese Unterschritte:

### 2.1 Rechtecke definieren

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### 2.2 OCR-Erkennung durchführen

```csharp
// erster Fall
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Zeigt den erkannten Text an
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## Schritt 3: Bild mit den Erkennungseinstellungen erkennen

In diesem Schritt stellen wir eine alternative Methode vor, die RecognitionSettings für die Bilderkennung verwendet:

### 3.1 Erkennungseinstellungen definieren

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### 3.2 Erkannten Text anzeigen

```csharp
// Zeigt den erkannten Text an
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Abschluss

Glückwunsch! Sie haben den Prozess der Vorbereitung von Rechtecken in der OCR-Bilderkennung mit Aspose.OCR für .NET erfolgreich gemeistert. Mit diesem Leitfaden können Sie OCR nahtlos in Ihre .NET-Anwendungen integrieren und so deren Texterkennungsfunktionen verbessern.

### FAQs

### F1: Kann ich Aspose.OCR für .NET mit anderen .NET-Frameworks verwenden?

A1: Ja, Aspose.OCR für .NET ist mit verschiedenen .NET-Frameworks kompatibel.

### F2: Gibt es eine kostenlose Testversion für Aspose.OCR für .NET?

 A2: Auf jeden Fall! Sie können auf die kostenlose Testversion zugreifen[Hier](https://releases.aspose.com/).

### F3: Wie erhalte ich Unterstützung für Aspose.OCR für .NET?

 A3: Besuchen Sie die[Aspose.OCR-Forum](https://forum.aspose.com/c/ocr/16) für engagierte Unterstützung.

### F4: Kann ich zu Testzwecken eine temporäre Lizenz erhalten?

 A4: Ja, Sie können eine temporäre Lizenz erwerben[Hier](https://purchase.aspose.com/temporary-license/).

### F5: Wo finde ich die Dokumentation für Aspose.OCR für .NET?

 A5: Die Dokumentation ist verfügbar[Hier](https://reference.aspose.com/ocr/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
