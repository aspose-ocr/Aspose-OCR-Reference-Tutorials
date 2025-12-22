---
date: 2025-12-22
description: Erfahren Sie, wie Sie Text aus Bildern mit Aspose.OCR für .NET erkennen
  und Bilder mit präzisen OCR‑Erkennungseinstellungen in Text umwandeln.
linktitle: recognize text from image – Perform OCR on Image from URL
second_title: Aspose.OCR .NET API
title: Text aus Bild erkennen – OCR für Bild von URL ausführen
url: /de/net/ocr-optimization/perform-ocr-on-image-from-url/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf Bild von URL in OCR-Bilderkennung durchführen

## Einleitung

Im Bereich der optischen Zeichenerkennung (OCR) ermöglicht Aspose.OCR für .NET das **Erkennen von Text aus Bild** mit hoher Präzision und befähigt Entwickler, Inhalte aus Bildern mühelos zu extrahieren. Wenn Sie OCR‑Funktionen in Ihre .NET‑Anwendung integrieren und Texterkennung von einer entfernten Quelle durchführen möchten, führt Sie diese Schritt‑für‑Schritt‑Anleitung durch den Prozess, OCR auf einem Bild von einer URL auszuführen.

## Schnelle Antworten
- **Worum geht es in diesem Tutorial?** Erkennen von Text aus einem Bild, das sich an einer öffentlichen URL befindet, mit Aspose.OCR für .NET.  
- **Welches Hauptkeyword wird angesprochen?** *recognize text from image*  
- **Benötige ich eine Lizenz?** Es gibt eine Testversion, aber für den Produktionseinsatz ist eine kommerzielle Lizenz erforderlich.  
- **Welche .NET-Versionen werden unterstützt?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Wie lange dauert die Implementierung?** In der Regel weniger als 10 Minuten für eine Grundkonfiguration.

## Was bedeutet „recognize text from image“?
Das Erkennen von Text aus Bild bedeutet, die visuelle Darstellung von Zeichen in editierbaren, durchsuchbaren Text umzuwandeln. Dieser Vorgang wird häufig als **convert image to text** oder **extract text from image** bezeichnet und ermöglicht Szenarien wie Dokumentendigitalisierung, Automatisierung der Dateneingabe und Verbesserungen der Barrierefreiheit.

## Warum Aspose.OCR für .NET verwenden?
- **Hohe Genauigkeit** mit integrierter Sprachunterstützung.  
- **Fein abgestimmte OCR-Erkennungseinstellungen** (z. B. Auto‑Skew, Flächenerkennung).  
- **Einfache API**, die sowohl mit .NET Framework als auch mit .NET Core funktioniert.  
- **Keine externen Abhängigkeiten** – alles läuft lokal.

## Voraussetzungen

Bevor Sie mit dem Tutorial beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

- Aspose.OCR für .NET: Stellen Sie sicher, dass die Aspose.OCR‑Bibliothek in Ihr .NET‑Projekt integriert ist. Sie können sie von der [release page](https://releases.aspose.com/ocr/net/) herunterladen.
- Entwicklungsumgebung: Richten Sie eine funktionierende .NET‑Entwicklungsumgebung auf Ihrem Rechner ein.

## Namespaces importieren

Fügen Sie in Ihrem .NET‑Projekt die erforderlichen Namespaces hinzu, um auf die Aspose.OCR‑Funktionen zuzugreifen. Ergänzen Sie den folgenden Code‑Abschnitt in Ihrem Projekt:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
```

## Wie erkennt man Text aus Bild mithilfe einer URL?

### Schritt 1: Dokumentverzeichnis einrichten

Beginnen Sie damit, das Verzeichnis anzugeben, in dem Ihre Dokumente gespeichert sind. Ersetzen Sie `"Your Document Directory"` durch den tatsächlichen Pfad zu Ihren Dokumenten.

```csharp
string dataDir = "Your Document Directory";
```

### Schritt 2: Bild für die Erkennung abrufen

Geben Sie die URL des Bildes an, das Sie mit OCR verarbeiten möchten. Stellen Sie sicher, dass das Bild öffentlich zugänglich ist.

```csharp
string uri = "https://qph.fs.quoracdn.net/main-qimg-0ff82d0dc3543dcd3b06028f5476c2e4";
```

### Schritt 3: AsposeOcr initialisieren

Erzeugen Sie eine Instanz der Klasse AsposeOcr, um auf die OCR‑Funktionen zuzugreifen.

```csharp
AsposeOcr api = new AsposeOcr();
```

### Schritt 4: Bild erkennen

Verwenden Sie die Aspose.OCR‑Bibliothek, um Text von der angegebenen Bild‑URL zu erkennen. Passen Sie die Erkennungseinstellungen an Ihre Anforderungen an.

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

### Schritt 5: Ergebnis ausgeben

Geben Sie das Erkennungsergebnis aus, einschließlich des erkannten Textes, der Bereiche und etwaiger Warnungen.

```csharp
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
```

### Schritt 6: Ausführen und prüfen

Führen Sie Ihre Anwendung aus, und wenn alles korrekt eingerichtet ist, sollten Sie den OCR‑Vorgang erfolgreich ausgeführt sehen.

```csharp
Console.WriteLine("PerformOCROnImageFromUrl executed successfully");
```

## Häufige Probleme und Lösungen

- **Bild nicht öffentlich zugänglich** – Überprüfen Sie, ob die URL im Browser funktioniert. Wenn das Bild eine Authentifizierung erfordert, laden Sie es zuerst herunter und verwenden Sie `RecognizeImageFromStream`.
- **Falsche Erkennungsbereiche** – Passen Sie die `Rectangle`‑Werte an oder setzen Sie `DetectAreas = false`, damit die Engine die Bereiche automatisch erkennt.
- **Sprache nicht erkannt** – Stellen Sie sicher, dass das passende Sprachpaket installiert ist oder setzen Sie `Language = "eng"` (oder einen anderen ISO‑Code) in `RecognitionSettings`.

## Häufig gestellte Fragen

### Q1: Ist Aspose.OCR für die Verarbeitung mehrerer Sprachen geeignet?

A1: Ja, Aspose.OCR unterstützt die Erkennung von Text in verschiedenen Sprachen und ist damit vielseitig für internationale Anwendungen.

### Q2: Kann ich Aspose.OCR sowohl für einzeilige als auch mehrzeilige Texterkennung verwenden?

A2: Absolut! Aspose.OCR bietet Flexibilität, sowohl einzeiligen als auch mehrzeiligen Text zu erkennen, und passt sich Ihrem spezifischen Anwendungsfall an.

### Q3: Gibt es Lizenzoptionen für Aspose.OCR?

A3: Ja, Sie können Lizenzoptionen prüfen und Käufe im [Aspose store](https://purchase.aspose.com/buy) tätigen.

### Q4: Gibt es eine kostenlose Testversion für Aspose.OCR?

A4: Ja, Sie können Aspose.OCR kostenlos testen, indem Sie die [releases page](https://releases.aspose.com/) besuchen.

### Q5: Wo finde ich Support oder Community‑Diskussionen zu Aspose.OCR?

A5: Besuchen Sie das [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) für Support und den Austausch mit der Community.

## Fazit

Mit Aspose.OCR für .NET wird die Integration von OCR‑Funktionen in Ihre .NET‑Anwendungen zu einem nahtlosen Erlebnis. Dieses Tutorial hat Sie durch den Prozess des **recognize text from image** mithilfe einer URL geführt und bietet eine solide Grundlage, um die Textextraktion in Ihren Projekten zu nutzen.

---

**Last Updated:** 2025-12-22  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}