---
title: Führen Sie in der OCR-Bilderkennung eine OCR für Bilder von einer URL durch
linktitle: Führen Sie in der OCR-Bilderkennung eine OCR für Bilder von einer URL durch
second_title: Aspose.OCR .NET API
description: Entdecken Sie die nahtlose OCR-Integration mit Aspose.OCR für .NET. Erkennen Sie Text präzise aus Bildern.
weight: 10
url: /de/net/ocr-optimization/perform-ocr-on-image-from-url/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Führen Sie in der OCR-Bilderkennung eine OCR für Bilder von einer URL durch

## Einführung

Im Bereich der optischen Zeichenerkennung (OCR) zeichnet sich Aspose.OCR für .NET als leistungsstarkes Tool aus, mit dem Entwickler Textinhalte präzise aus Bildern extrahieren können. Wenn Sie OCR-Funktionen in Ihre .NET-Anwendung integrieren und mühelos Texterkennung durchführen möchten, führt Sie diese Schritt-für-Schritt-Anleitung durch den Prozess der Durchführung von OCR für ein Bild von einer URL.

## Voraussetzungen

Bevor Sie sich mit dem Tutorial befassen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

-  Aspose.OCR für .NET: Stellen Sie sicher, dass die Aspose.OCR-Bibliothek in Ihr .NET-Projekt integriert ist. Sie können es hier herunterladen[Release-Seite](https://releases.aspose.com/ocr/net/).

- Entwicklungsumgebung: Richten Sie auf Ihrem Computer eine funktionierende .NET-Entwicklungsumgebung ein.

## Namespaces importieren

Fügen Sie in Ihr .NET-Projekt die erforderlichen Namespaces ein, um auf die Aspose.OCR-Funktionen zuzugreifen. Fügen Sie Ihrem Projekt den folgenden Codeausschnitt hinzu:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
```

## Schritt 1: Richten Sie Ihr Dokumentenverzeichnis ein

 Geben Sie zunächst das Verzeichnis an, in dem Ihre Dokumente gespeichert sind. Ersetzen`"Your Document Directory"` mit dem tatsächlichen Pfad zu Ihren Dokumenten.

```csharp
string dataDir = "Your Document Directory";
```

## Schritt 2: Holen Sie sich das Bild zur Erkennung

Geben Sie die URL des Bildes an, für das Sie OCR durchführen möchten. Stellen Sie sicher, dass das Bild öffentlich zugänglich ist.

```csharp
string uri = "https://qph.fs.quoracdn.net/main-qimg-0ff82d0dc3543dcd3b06028f5476c2e4";
```

## Schritt 3: AsposeOcr initialisieren

Erstellen Sie eine Instanz der AsposeOcr-Klasse, um auf OCR-Funktionen zuzugreifen.

```csharp
AsposeOcr api = new AsposeOcr();
```

## Schritt 4: Bild erkennen

Nutzen Sie die Aspose.OCR-Bibliothek, um Text aus der angegebenen Bild-URL zu erkennen. Passen Sie die Erkennungseinstellungen entsprechend Ihren Anforderungen an.

```csharp
RecognitionResult result = api.RecognizeImageFromUri(uri, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    RecognitionAreas = new List<Rectangle>()
    {
        new Rectangle(1,3,390,70),
        new Rectangle(1,72,390,70)
    }
});
```

## Schritt 5: Ergebnis drucken

Zeigen Sie das Erkennungsergebnis an, einschließlich des erkannten Textes, der erkannten Bereiche und etwaiger Warnungen.

```csharp
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
```

## Schritt 6: Ausführen und Überprüfen

Führen Sie Ihre Anwendung aus und wenn alles richtig eingerichtet ist, sollte der OCR-Prozess erfolgreich ausgeführt werden.

```csharp
Console.WriteLine("PerformOCROnImageFromUrl executed successfully");
```

## Abschluss

Mit Aspose.OCR für .NET wird die Integration von OCR-Funktionen in Ihre .NET-Anwendungen zu einem nahtlosen Erlebnis. Dieses Tutorial hat Sie durch den Prozess der Durchführung von OCR für ein Bild von einer URL geführt und Ihnen eine Grundlage gegeben, um die Leistungsfähigkeit der Texterkennung in Ihren Projekten zu nutzen.

## FAQs

### F1: Ist Aspose.OCR für die Verarbeitung mehrerer Sprachen geeignet?

A1: Ja, Aspose.OCR unterstützt die Texterkennung in verschiedenen Sprachen und ist somit vielseitig für internationale Anwendungen geeignet.

### F2: Kann ich Aspose.OCR sowohl für die einzeilige als auch für die mehrzeilige Texterkennung verwenden?

A2: Auf jeden Fall! Aspose.OCR bietet Flexibilität bei der Erkennung von einzeiligem und mehrzeiligem Text und passt sich so an Ihren spezifischen Anwendungsfall an.

### F3: Gibt es Lizenzoptionen für Aspose.OCR?

 A3: Ja, Sie können Lizenzoptionen erkunden und Einkäufe tätigen[Aspose-Laden](https://purchase.aspose.com/buy).

### F4: Gibt es eine kostenlose Testversion für Aspose.OCR?

 A4: Ja, Sie können Aspose.OCR kostenlos testen, indem Sie die besuchen[Veröffentlichungsseite](https://releases.aspose.com/).

### F5: Wo finde ich Support oder Community-Diskussionen zu Aspose.OCR?

 A5: Besuchen Sie die[Aspose.OCR-Forum](https://forum.aspose.com/c/ocr/16) für die Unterstützung und das Engagement in der Gemeinschaft.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
