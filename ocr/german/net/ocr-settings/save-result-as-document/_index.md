---
title: Ergebnis als Dokument in der OCR-Bilderkennung speichern
linktitle: Ergebnis als Dokument in der OCR-Bilderkennung speichern
second_title: Aspose.OCR .NET API
description: Nutzen Sie das Potenzial von Aspose.OCR für .NET. Erkennen Sie problemlos Text in Bildern und speichern Sie die Ergebnisse in verschiedenen Dokumentformaten.
type: docs
weight: 10
url: /de/net/ocr-settings/save-result-as-document/
---
## Einführung

Willkommen in der aufregenden Welt der optischen Zeichenerkennung (OCR) mit Aspose.OCR für .NET! In diesem umfassenden Tutorial befassen wir uns mit den Feinheiten der Verwendung von Aspose.OCR zur Texterkennung in Bildern und zeigen, wie die Ergebnisse in verschiedenen Dokumentformaten gespeichert werden.

## Voraussetzungen

Bevor wir uns auf die OCR-Reise begeben, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

-  Aspose.OCR für .NET. Stellen Sie sicher, dass Sie die Aspose.OCR-Bibliothek installiert haben. Sie können es herunterladen[Hier](https://releases.aspose.com/ocr/net/).

-  Dokumentenverzeichnis: Richten Sie ein bestimmtes Verzeichnis für Ihre Dokumente ein und aktualisieren Sie das`dataDir` Variable im bereitgestellten Code entsprechend.

## Namespaces importieren

Beginnen Sie mit dem Importieren der erforderlichen Namespaces. Dies sind die Bausteine, die Ihren Code mit OCR-Funktionen ausstatten.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Lassen Sie uns das Beispiel nun in mehrere Schritte unterteilen:

## Schritt 1: Aspose.OCR initialisieren

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "Your Document Directory";

// Initialisieren Sie eine Instanz von AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Dieser Schritt bereitet die Bühne, indem er die Aspose.OCR-API initialisiert.

## Schritt 2: Bild erkennen

```csharp
// Bild erkennen
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

Hier verwenden wir Aspose.OCR, um Text im angegebenen Bild zu erkennen (ersetzen Sie „sample.png“ durch Ihre Bilddatei).

## Schritt 3: Ergebnis in verschiedenen Formaten speichern

```csharp
// Speichern Sie das Ergebnis in Ihrem bevorzugten Format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

Passen Sie diesen Schritt an Ihre Bedürfnisse an. Mit Aspose.OCR können Sie den erkannten Text in verschiedenen Dokumentformaten wie DOCX, TXT, PDF und XLSX speichern.

## Schritt 4: Erfolgsmeldung anzeigen

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

Eine einfache Bestätigungsnachricht, die Sie darüber informiert, dass der Vorgang reibungslos abgeschlossen wurde.

Indem Sie diese Schritte befolgen, haben Sie die Leistungsfähigkeit von Aspose.OCR für .NET erfolgreich genutzt, um Text in Bildern zu erkennen und die Ergebnisse in verschiedenen Dokumentformaten zu speichern.

## Abschluss

Zusammenfassend eröffnet Aspose.OCR für .NET eine Welt voller Möglichkeiten für die Texterkennung in Bildern. Ob Sie Daten extrahieren oder durchsuchbare Dokumente erstellen, Aspose.OCR vereinfacht den Prozess mit seiner intuitiven API.

## FAQs

### Q1. Ist Aspose.OCR mit verschiedenen Bildformaten kompatibel?

A1: Ja, Aspose.OCR unterstützt eine Vielzahl von Bildformaten und sorgt so für Flexibilität bei Ihren OCR-Aufgaben.

### F2: Kann ich die Erkennungseinstellungen für eine bessere Genauigkeit anpassen?

A2: Auf jeden Fall! Aspose.OCR bietet Erkennungseinstellungen zur Feinabstimmung des OCR-Prozesses entsprechend Ihren spezifischen Anforderungen.

### F3: Gibt es eine kostenlose Testversion?

 A3: Ja, Sie können mit einer kostenlosen Testversion beginnen[Hier](https://releases.aspose.com/).

### F4: Wie kann ich temporäre Lizenzen für Aspose.OCR erhalten?

 A4: Es können temporäre Lizenzen erworben werden[Hier](https://purchase.aspose.com/temporary-license/).

### F5: Wo kann ich Hilfe suchen oder mit der Community in Kontakt treten?

 A5: Treten Sie der Aspose.OCR-Community bei[Aspose-Forum](https://forum.aspose.com/c/ocr/16) für Unterstützung und Diskussionen.