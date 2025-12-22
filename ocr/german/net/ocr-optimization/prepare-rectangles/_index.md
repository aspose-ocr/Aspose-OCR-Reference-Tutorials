---
date: 2025-12-22
description: Erfahren Sie, wie Sie Text aus einem Bild mit Aspose.OCR für .NET extrahieren.
  Dieser Leitfaden führt Sie durch die Vorbereitung von Rechtecken für die OCR‑Bilderkennung
  und die Steigerung der Genauigkeit.
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Wie man Text aus einem Bild extrahiert, indem man Rechtecke für die OCR vorbereitet
url: /de/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rechtecke für die OCR-Bilderkennung vorbereiten

## Einführung

Optische Zeichenerkennung (OCR) ist unerlässlich, um visuelle Inhalte in durchsuchbaren, editierbaren Text umzuwandeln. In diesem Tutorial **extrahieren Sie Text aus einem Bild**, indem Sie benutzerdefinierte Rechtecke vorbereiten, die die OCR-Engine auf bestimmte Bereiche fokussieren. Mit Aspose.OCR für .NET führen wir Sie durch jeden Schritt – vom Einrichten Ihres Projekts bis zum Abrufen des erkannten Textes – damit Sie leistungsstarke Bild‑zu‑Text‑Funktionen in Ihre .NET‑Anwendungen integrieren können.

## Schnelle Antworten
- **Was bedeutet „Text aus Bild extrahieren“?** Es bedeutet, die visuellen Zeichen in einem Bild in maschinenlesbare Zeichenketten umzuwandeln.  
- **Welche Bibliothek unterstützt dies in .NET?** Aspose.OCR für .NET.  
- **Benötige ich eine Lizenz für die Entwicklung?** Eine kostenlose Testversion reicht für Tests; für die Produktion ist eine Lizenz erforderlich.  
- **Kann ich bestimmte Bereiche anvisieren?** Ja, indem Sie Rechtecke definieren, die den OCR‑Umfang begrenzen.  
- **Welche .NET‑Versionen werden unterstützt?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Was bedeutet „Text aus Bild extrahieren“ mit Rechtecken?

Wenn Sie rechteckige Zonen auf einem Bild definieren, verarbeitet die OCR‑Engine nur diese Zonen. Das verbessert die Genauigkeit, reduziert die Verarbeitungszeit und ermöglicht das Ignorieren von störenden Hintergründen oder irrelevanten Abschnitten.

## Warum Rechtecke vor der OCR vorbereiten?

- **Fokus auf relevante Inhalte:** Überschriften, Fußzeilen oder dekorative Grafiken überspringen.  
- **Leistungssteigerung:** Kleinere Bereiche bedeuten schnellere Erkennung.  
- **Genauigkeit verbessern:** Weniger Bildrauschen führt zu saubereren Ergebnissen.

## Voraussetzungen

- Vertrautheit mit C# und .NET-Entwicklung.  
- Aspose.OCR für .NET Bibliothek installiert – Sie können sie **[hier](https://releases.aspose.com/ocr/net/)** herunterladen.  
- Ein Beispielbild (z. B. `sample.png`), das den Text enthält, den Sie extrahieren möchten.

## Namespaces importieren

Zuerst bringen Sie die erforderlichen Namespaces in den Gültigkeitsbereich:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Schritt 1: Dokumentverzeichnis einrichten

Geben Sie an, wo Ihre Bilddateien gespeichert sind, und erstellen Sie eine Instanz der OCR‑Engine.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Wie man Text aus Bild mit mehreren Rechtecken extrahiert

### Schritt 2: Bild mit mehreren Rechtecken erkennen

#### 2.1 Rechtecke definieren

Erstellen Sie eine Liste von `Rectangle`‑Objekten, die die Bereiche umreißen, die die OCR‑Engine scannen soll.

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 OCR‑Erkennung durchführen

Übergeben Sie den Bildpfad und die Rechteckliste an `RecognizeImage`. Die Methode gibt eine Sammlung von Zeichenketten zurück – jeder Eintrag entspricht einem Rechteck.

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### Schritt 3: Bild mit Recognition Settings erkennen (alternativer Ansatz)

Wenn Sie lieber `RecognitionSettings` verwenden, können Sie dasselbe Ergebnis mit einem leicht anderen API‑Aufruf erzielen.

#### 3.1 Erkennungs‑Einstellungen definieren

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 Erkannten Text anzeigen

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Häufige Probleme & Tipps

- **Falsche Rechteckkoordinaten:** Stellen Sie sicher, dass die Werte `X`, `Y`, `Width` und `Height` korrekt auf den gewünschten Bereich abgebildet sind.  
- **Bildqualität:** Niedrigauflösende Bilder können schlechte OCR‑Ergebnisse liefern; erwägen Sie eine Vorverarbeitung (z. B. Binärisierung).  
- **Leere Ergebnisse:** Prüfen Sie, ob die Rechtecke tatsächlich Text enthalten; andernfalls gibt die Engine leere Zeichenketten zurück.

## Fazit

Sie haben nun gelernt, wie Sie **Text aus Bild** extrahieren, indem Sie benutzerdefinierte Rechtecke mit Aspose.OCR für .NET vorbereiten. Diese Technik gibt Ihnen eine feinkörnige Kontrolle über die OCR‑Verarbeitung und hilft Ihnen, schnellere, genauere Textextraktions‑Features in Ihren Anwendungen zu bauen.

## Häufig gestellte Fragen

**Q:** Kann ich Aspose.OCR für .NET mit anderen .NET‑Frameworks verwenden?  
**A:** Ja, Aspose.OCR für .NET ist mit verschiedenen .NET‑Frameworks kompatibel.

**Q:** Gibt es eine kostenlose Testversion für Aspose.OCR für .NET?  
**A:** Auf jeden Fall! Sie können die kostenlose Testversion **[hier](https://releases.aspose.com/)** abrufen.

**Q:** Wie erhalte ich Support für Aspose.OCR für .NET?  
**A:** Besuchen Sie das **[Aspose.OCR‑Forum](https://forum.aspose.com/c/ocr/16)** für dedizierten Support.

**Q:** Kann ich eine temporäre Lizenz für Testzwecke erhalten?  
**A:** Ja, Sie können eine temporäre Lizenz **[hier](https://purchase.aspose.com/temporary-license/)** erwerben.

**Q:** Wo finde ich die Dokumentation für Aspose.OCR für .NET?  
**A:** Die Dokumentation ist **[hier](https://reference.aspose.com/ocr/net/)** verfügbar.

**Zuletzt aktualisiert:** 2025-12-22  
**Getestet mit:** Aspose.OCR 24.11 für .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}