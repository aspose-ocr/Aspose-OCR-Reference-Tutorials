---
date: 2025-12-17
description: Erfahren Sie, wie Sie mit Aspose.OCR für .NET OCR‑Zeilenrechtecke erhalten,
  um Textzeilen in Bildern zu erkennen und Zeilenkoordinaten einfach zu extrahieren.
linktitle: Get OCR Line Rectangles for Image Text Lines
second_title: Aspose.OCR .NET API
title: OCR‑Zeilenrechtecke für Bildtextzeilen abrufen
url: /de/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR‑Linienrechtecke für Bildtextzeilen erhalten

## Einleitung

In diesem Tutorial erfahren Sie **wie man OCR‑Linienrechtecke** mit Aspose.OCR für .NET erhält. Am Ende des Leitfadens können Sie **Textzeilen in einem Bild erkennen** und **Linienkoordinaten** für jede erkannte Zeile extrahieren – perfekt für nachgelagerte Verarbeitung wie Layout‑Analyse, Datenerfassung oder benutzerdefiniertes Rendering.

## Schnelle Antworten
- **Was bedeutet „get OCR line rectangles“?** Es gibt die Begrenzungsrahmen jeder im Bild erkannten Textzeile zurück.  
- **Welche API‑Methode wird verwendet?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion funktioniert für die Entwicklung; für die Produktion ist eine kommerzielle Lizenz erforderlich.  
- **Unterstützte Bildformate?** PNG, JPEG, BMP, TIFF und mehr.  
- **Kann ich das auf .NET Core ausführen?** Ja, Aspose.OCR unterstützt .NET Core sowie .NET 5/6 vollständig.

## Voraussetzungen

Bevor Sie in das Tutorial einsteigen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

- Grundkenntnisse in C# und .NET‑Entwicklung.  
- Eine integrierte Entwicklungsumgebung (IDE) wie Visual Studio.  
- Aspose.OCR für .NET Bibliothek installiert. Sie können sie [hier](https://releases.aspose.com/ocr/net/) herunterladen.  
- Ein Beispielbild mit Text für die OCR‑Erkennung.

## Namespaces importieren

Stellen Sie sicher, dass die erforderlichen Namespaces in Ihr Projekt importiert sind. Fügen Sie die folgenden Zeilen am Anfang Ihrer C#‑Datei hinzu:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Nun zerlegen wir den Prozess, Rechtecke für Zeilen in der OCR‑Bilderkennung zu erhalten, in leicht nachvollziehbare Schritte.

## Schritt 1: Dokumentverzeichnis einrichten

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Ersetzen Sie `"Your Document Directory"` durch den tatsächlichen Pfad zu dem Ordner, der Ihr Beispielbild enthält.

## Schritt 2: Aspose.OCR initialisieren

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Erstellen Sie eine Instanz der Klasse `AsposeOcr`, um auf die OCR‑Funktionalität zuzugreifen.

## Schritt 3: Bildpfad angeben

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Definieren Sie den vollständigen Pfad zu dem Bild, das Sie mit OCR verarbeiten möchten.

## Schritt 4: Bild erkennen und Rechtecke erhalten

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

Die Methode `GetRectangles` gibt eine Liste von `Rectangle`‑Objekten zurück, von denen jedes die Koordinaten einer erkannten Textzeile darstellt. Dies ist das Kernstück des **Erhaltens von OCR‑Linienrechtecken**.

## Schritt 5: Ergebnis ausgeben

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Geben Sie die Koordinaten der erkannten Bereiche in der Konsole aus. Sie sehen Werte, die Sie später verwenden können, um **Linienkoordinaten** für benutzerdefinierte Verarbeitung zu **extrahieren**.

## Warum Aspose.OCR für Linienrechtecke verwenden?

- **Hohe Genauigkeit** – Fortgeschrittene Algorithmen erkennen Zeilen selbst in verrauschten oder schiefen Bildern.  
- **Plattformübergreifend** – Funktioniert auf .NET Framework, .NET Core und .NET 5/6.  
- **Keine externen Abhängigkeiten** – Reine .NET‑Bibliothek, keine nativen DLLs zum Ausliefern.  
- **Umfangreiche Ausgabe** – Neben Linienrechtecken können Sie auch Wörter, Zeichen Vertrauenswerte abrufen.

## Häufige Probleme und Lösungen

| Problem | Lösung |
|---------|--------|
| **Keine Rechtecke zurückgegeben** | Stellen Sie sicher, dass das Bild klaren, horizontalen Text enthält und dass `AreasType.LINES` angegeben ist. |
| **Falsche Koordinaten** | Überprüfen Sie die DPI des Bildes; Bilder mit niedriger Auflösung können ungenaue Grenzen verursachen. |
| **Leistungsengpass bei großen Bildern** | Skalieren Sie das Bild auf eine angemessene Auflösung, bevor Sie `GetRectangles` aufrufen. |
| **Lizenzausnahme** | Verwenden Sie eine Testlizenz zum Testen; setzen Sie eine Voll‑lizenz für die Produktion ein, um Evaluationsbeschränkungen zu vermeiden. |

## FAQ

### Q1: Kann ich Aspose.OCR für .NET mit jedem Bildtyp verwenden?

Aspose.OCR unterstützt eine breite Palette von Bildformaten und bietet damit Flexibilität in Ihren OCR‑Anwendungen.

### Q2: Wie genau ist die OCR‑Erkennung?

Aspose.OCR nutzt fortschrittliche Algorithmen für hohe Genauigkeit und ist damit für verschiedene Texterkennungsszenarien geeignet.

### Q3: Gibt es eine Testversion?

Ja, Sie können die Funktionen von Aspose.OCR für .NET mit dem [kostenlosen Test](https://releases.aspose.com/) erkunden.

### Q4: Wo finde ich umfassende Dokumentation?

Siehe die [Dokumentation](https://reference.aspose.com/ocr/net/) für detaillierte Informationen und Nutzungshinweise.

### Q5: Benötigen Sie Unterstützung oder haben Sie spezifische Fragen?

Besuchen Sie das [Aspose.OCR‑Forum](https://forum.aspose.com/c/ocr/16) für Community‑Support und Diskussionen.

## Häufig gestellte Fragen

**Q: Kann ich einzelne Wörter statt ganzer Zeilen extrahieren?**  
A: Ja, verwenden Sie `AreasType.WORDS` mit derselben `GetRectangles`‑Methode, um wortbezogene Begrenzungsrahmen zu erhalten.

**Q: Unterstützt die API mehrseitige PDFs?**  
A: Konvertieren Sie zunächst jede PDF‑Seite in ein Bild und rufen Sie dann `GetRectangles` für jedes Bild auf.

**Q: Wie gehe ich mit gedrehtem Text um?**  
A: Aktivieren Sie die Auto‑Rotate‑Option in den OCR‑Einstellungen oder drehen Sie das Bild vor der Verarbeitung vor.

**Q: Gibt es eine Möglichkeit, Vertrauenswerte für jede Zeile zu erhalten?**  
A: Nachdem Sie die Rechtecke erhalten haben, rufen Sie `api.RecognizeImage(...).Lines` auf, um Zeilenobjekte mit Vertrauenswerten zu erhalten.

**Q: Welche .NET‑Versionen sind kompatibel?**  
A: Die Bibliothek funktioniert mit .NET Framework 4.5+, .NET Core 3.1+ und .NET 5/6.

## Fazit

Herzlichen Glückwunsch! Sie haben erfolgreich **OCR‑Linienrechtecke** für ein Bild mit Aspose.OCR für .NET erhalten. Mit den Begrenzungsrahmen können Sie nun die Linienkoordinaten in nachgelagerte Workflows wie benutzerdefiniertes Rendering, Datenerfassung oder Layout‑Analyse einspeisen.

---

**Zuletzt aktualisiert:** 2025-12-17  
**Getestet mit:** Aspose.OCR 24.11 für .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}