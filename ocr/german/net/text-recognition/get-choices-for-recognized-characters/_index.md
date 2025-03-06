---
title: Erhalten Sie Auswahlmöglichkeiten für erkannte Zeichen bei der OCR-Bilderkennung
linktitle: Erhalten Sie Auswahlmöglichkeiten für erkannte Zeichen bei der OCR-Bilderkennung
second_title: Aspose.OCR .NET API
description: Erweitern Sie Ihre .NET-Anwendungen mit Aspose.OCR für eine genaue Zeichenerkennung. Befolgen Sie unsere Schritt-für-Schritt-Anleitung, um Auswahlmöglichkeiten für erkannte Zeichen bei der Bilderkennung abzurufen.
weight: 10
url: /de/net/text-recognition/get-choices-for-recognized-characters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Erhalten Sie Auswahlmöglichkeiten für erkannte Zeichen bei der OCR-Bilderkennung

## Einführung

Die Nutzung der Leistungsfähigkeit der optischen Zeichenerkennung (OCR) ist im heutigen digitalen Zeitalter von entscheidender Bedeutung, und Aspose.OCR für .NET zeichnet sich als robuste Lösung für die genaue Zeichenerkennung aus. In diesem Tutorial befassen wir uns mit einer bestimmten Funktion: dem Abrufen von Auswahlmöglichkeiten für erkannte Zeichen. Am Ende dieses Handbuchs werden Sie diese Funktionalität nahtlos in Ihre .NET-Anwendungen integrieren.

## Voraussetzungen

Bevor Sie mit dem Tutorial beginnen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:

- Grundkenntnisse in C#- und .NET-Entwicklung.
- Visual Studio ist auf Ihrem Computer installiert.
-  Aspose.OCR für .NET-Bibliothek, die Sie herunterladen können[Hier](https://releases.aspose.com/ocr/net/).

## Namespaces importieren

Beginnen Sie in Ihrem C#-Projekt mit dem Importieren der erforderlichen Namespaces:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Schritt 1: Aspose.OCR initialisieren

Beginnen Sie mit der Initialisierung einer Instanz von Aspose.OCR:

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "Your Document Directory";

// Initialisieren Sie eine Instanz von AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Schritt 2: Geben Sie den Bildpfad an

Legen Sie den Pfad für das Bild fest, das Sie analysieren möchten:

```csharp
//Bildpfad
string fullPath = dataDir + "sample.png";
```

## Schritt 3: Bild erkennen

Führen Sie den Bilderkennungsprozess aus:

```csharp
// Bild erkennen
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    // Standard- oder benutzerdefinierte Einstellungen
});
```

## Schritt 4: Holen Sie sich Auswahlmöglichkeiten für erkannte Charaktere

Auswahlmöglichkeiten für erkannte Zeichen abrufen:

```csharp
List<char[]> resultWithChoices = result.RecognitionCharactersList;
```

## Schritt 5: Drucken Sie die Ergebnisse aus

Erkennungstext und Auswahlmöglichkeiten anzeigen:

```csharp
// Ergebnis drucken
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Choices:");
resultWithChoices.ForEach(a => Console.WriteLine($"character: {a[0]} . Choices: {a[1]} {a[2]} {a[3]} {a[4]}"));

Console.WriteLine("GetChoiceForRecognizedCharacters executed successfully");
```

Wiederholen Sie diese Schritte und passen Sie sie entsprechend den Anforderungen Ihrer Anwendung an.

## Abschluss

In diesem Tutorial haben wir untersucht, wie Sie Aspose.OCR für .NET nutzen können, um Auswahlmöglichkeiten für erkannte Zeichen bei der Bilderkennung zu erhalten. Diese Funktion erweitert Ihre OCR-Funktionen um eine neue Dimension und erhöht die Vielseitigkeit Ihrer Anwendungen.

## FAQs

### F1: Ist Aspose.OCR für .NET für die Verarbeitung umfangreicher Dokumente geeignet?

A1: Auf jeden Fall! Aspose.OCR für .NET wurde für die effiziente und genaue Verarbeitung großer Dokumentenmengen entwickelt.

### F2: Kann ich Aspose.OCR für .NET in einer Webanwendung verwenden?

A2: Ja, Sie können Aspose.OCR für .NET in Webanwendungen integrieren, wodurch es für verschiedene Entwicklungsszenarien vielseitig einsetzbar ist.

### F3: Gibt es Lizenzoptionen für Aspose.OCR für .NET?

 A3: Ja, Sie können Lizenzoptionen erkunden und einen Kauf tätigen[Hier](https://purchase.aspose.com/buy).

### F4: Wie kann ich Unterstützung erhalten oder Fragen zu Aspose.OCR für .NET stellen?

 A4: Besuchen Sie die[Aspose.OCR-Forum](https://forum.aspose.com/c/ocr/16) um Unterstützung zu erhalten, Fragen zu stellen und mit der Community in Kontakt zu treten.

### F5: Gibt es eine kostenlose Testversion für Aspose.OCR für .NET?

 A5: Ja, Sie können auf eine kostenlose Testversion zugreifen[Hier](https://releases.aspose.com/) um die Möglichkeiten von Aspose.OCR für .NET kennenzulernen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
