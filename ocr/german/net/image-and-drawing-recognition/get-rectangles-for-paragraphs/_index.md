---
date: 2025-12-17
description: Erfahren Sie, wie Sie Rechtecke für Absätze in OCR‑Bildern mit Aspose.OCR
  für .NET extrahieren – der umfassende Leitfaden zum Extrahieren von Rechtecken und
  Absatzkoordinaten.
linktitle: Get Rectangles for Paragraphs in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Wie man Rechtecke für Absätze bei der OCR-Bilderkennung extrahiert
url: /de/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Rechtecke für Absätze in der OCR‑Bilderkennung extrahiert

## Einführung

Willkommen zu unserem umfassenden Leitfaden, **wie man Rechtecke** für Absätze in der OCR‑Bilderkennung mit Aspose.OCR für .NET extrahiert. Wenn Sie Ihre Dokumenten‑Verarbeitungspipeline verbessern, Absatzgrenzen herausziehen und die Datenerfassung automatisieren möchten, sind Sie hier genau richtig. Wir führen Sie Schritt für Schritt – von der Einrichtung der Umgebung bis zum Ausgeben der Rechteckkoordinaten – damit Sie die OCR‑Ergebnisse sofort nutzen können.

## Schnellantworten
- **Was bedeutet „Rechtecke extrahieren“?** Es liefert die Begrenzungsrahmen (x, y, Breite, Höhe) der erkannten Textbereiche.  
- **Welche API‑Methode liefert die Rechtecke?** `AsposeOcr.GetRectangles` mit `AreasType.PARAGRAPHS`.  
- **Benötige ich eine Lizenz für die Entwicklung?** Eine kostenlose Testversion reicht für Tests; für den Produktionseinsatz ist eine kommerzielle Lizenz erforderlich.  
- **Kann ich mehrere Bilder gleichzeitig verarbeiten?** Ja – iterieren Sie über Ihre Bildliste und rufen Sie `GetRectangles` für jede Datei auf.  
- **Welche Formate werden unterstützt?** PNG, JPEG, TIFF, BMP und viele weitere.

## Was bedeutet „wie man Rechtecke extrahiert“ in OCR?
Im OCR‑Kontext bedeutet das Extrahieren von Rechtecken, die geometrischen Grenzen zu identifizieren, die jeden Absatz oder jede Textzeile innerhalb eines Bildes umschließen. Diese Koordinaten ermöglichen es Ihnen, bestimmte Abschnitte eines gescannten Dokuments hervorzuheben, zuzuschneiden oder weiter zu analysieren.

## Warum Absatzkoordinaten extrahieren?
- **Präzise Nachbearbeitung** – Sie können jedes Rechteck in nachgelagerte Workflows einspeisen (z. B. Übersetzung, Schwärzung).  
- **Verbessertes UI/UX** – Überlagern Sie Begrenzungsrahmen auf dem Originalbild, um den Benutzern zu zeigen, wo Text gefunden wurde.  
- **Batch‑Automatisierung** – Schnell Absätze in großen Dokumentensammlungen lokalisieren und isolieren.

## Voraussetzungen

- Grundkenntnisse in C# und .NET‑Entwicklung.  
- Eine Entwicklungsumgebung mit installiertem Aspose.OCR für .NET – Sie können es [hier](https://releases.aspose.com/ocr/net/) herunterladen.  
- Vertrautheit mit Bildverarbeitungs‑Konzepten und dem Grund, warum OCR für die Textextraktion aus gescannten Dateien unverzichtbar ist.

## Namespaces importieren

Importieren Sie in Ihrer C#‑Datei die erforderlichen Namespaces, damit die OCR‑Klassen verfügbar sind:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Schritt 1: Dokumentverzeichnis festlegen

Definieren Sie den Ordner, der die zu analysierenden Bilder enthält:

```csharp
string dataDir = "Your Document Directory";
```

## Schritt 2: AsposeOcr‑Instanz initialisieren

Erzeugen Sie ein `AsposeOcr`‑Objekt – damit erhalten Sie Zugriff auf alle OCR‑Funktionen:

```csharp
AsposeOcr api = new AsposeOcr();
```

## Schritt 3: Bildpfad angeben

Verweisen Sie auf die genaue Bilddatei, die Sie verarbeiten möchten:

```csharp
string fullPath = dataDir + "sample.png";
```

## Schritt 4: Bild erkennen und Absatz‑Rechtecke erhalten

Rufen Sie die Methode `GetRectangles` auf. Das Setzen von `detect_areas` auf `true` veranlasst die Engine, **Absatz**‑Rechtecke zurückzugeben:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## Schritt 5: Ergebnisse ausgeben

Geben Sie die Koordinaten aus, damit Sie die **extrahierten Absatzkoordinaten** sehen können, die erkannt wurden:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## Häufige Probleme und Lösungen

| Problem | Grund | Lösung |
|---------|-------|--------|
| Keine Rechtecke zurückgegeben | Bildqualität zu niedrig oder falscher `AreasType` | Stellen Sie sicher, dass das Bild klar ist und verwenden Sie `AreasType.PARAGRAPHS`. |
| Koordinaten sind um eins verschoben | DPI‑Skalierungsabweichung | Setzen Sie den korrekten DPI‑Wert beim Laden des Bildes oder verwenden Sie `api.Config.Dpi`. |
| Lizenz‑Ausnahme | Ausführung ohne gültige Lizenz in der Produktion | Laden Sie eine temporäre oder permanente Lizenz über `api.SetLicense` hoch. |

## Häufig gestellte Fragen

**F: Ist Aspose.OCR mit verschiedenen Bildformaten kompatibel?**  
A: Ja, Aspose.OCR unterstützt PNG, JPEG, TIFF, BMP und viele weitere gängige Formate.

**F: Kann ich Aspose.OCR für die Batch‑Verarbeitung mehrerer Bilder nutzen?**  
A: Absolut! Durchlaufen Sie eine Sammlung von Dateipfaden und rufen Sie `GetRectangles` für jedes Bild auf.

**F: Gibt es eine kostenlose Testversion von Aspose.OCR für .NET?**  
A: Ja, Sie können eine kostenlose Testversion [hier](https://releases.aspose.com/) erkunden.

**F: Wie kann ich eine temporäre Lizenz für Aspose.OCR erhalten?**  
A: Sie können eine temporäre Lizenz [hier](https://purchase.aspose.com/temporary-license/) erwerben.

**F: Wo finde ich zusätzlichen Support und Diskussionen zu Aspose.OCR?**  
A: Besuchen Sie das [Aspose.OCR‑Forum](https://forum.aspose.com/c/ocr/16) für Community‑Support und Diskussionen.

## Fazit

In diesem Tutorial haben wir gezeigt, **wie man Rechtecke** für Absätze mit Aspose.OCR für .NET extrahiert, jeden Code‑Abschnitt durchgegangen und erklärt, wie die zurückgegebenen Koordinaten zu interpretieren sind. Durch die Integration dieser Schritte in Ihre Anwendung können Sie zuverlässig Absatzgrenzen herausziehen, Dokumenten‑Workflows verbessern und intelligentere OCR‑gesteuerte Lösungen bauen.

---

**Zuletzt aktualisiert:** 2025-12-17  
**Getestet mit:** Aspose.OCR 24.11 für .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}