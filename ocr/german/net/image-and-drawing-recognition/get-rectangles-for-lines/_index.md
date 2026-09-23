---
date: 2026-02-22
description: Lernen Sie, wie Sie Layout‑Analyse‑OCR durchführen, indem Sie Textzeilen
  in einem Bild erkennen und Zeilenrechtecke mit Aspose.OCR für .NET extrahieren.
linktitle: Layout Analysis OCR – Get Line Rectangles from Images
second_title: Aspose.OCR .NET API
title: Layout-Analyse OCR – Zeilenrechtecke aus Bildern erhalten
url: /de/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Layout‑Analyse OCR – Zeilenrechtecke aus Bildern erhalten

## Einführung

In diesem Tutorial erfahren Sie **wie Sie OCR‑Zeilenrechtecke** mit Aspose.OCR für .NET erhalten. Am Ende der Anleitung können Sie **Textzeilen in einem Bild erkennen** und **Zeilenkoordinaten** für jede erkannte Zeile extrahieren – ideal für nachgelagerte Verarbeitung wie **Layout‑Analyse OCR**, Datenaus extraction oder benutzerdefiniertes Rendering.

## Schnelle Antworten
- **Was bedeutet „get OCR line rectangles“?** Es gibt die Begrenzungsrahmen jeder im Bild erkannten Textzeile zurück.  
- **Welche API‑Methode wird verwendet?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion funktioniert für die Entwicklung; für die Produktion ist eine kommerzielle Lizenz erforderlich.  
- **Unterstützte Bildformate?** PNG, JPEG, BMP, TIFF und weitere.  
- **Läuft das auf .NET Core?** Ja, Aspose.OCR unterstützt .NET Core sowie .NET 5/6 vollständig.

## Voraussetzungen

Bevor Sie in das Tutorial einsteigen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllt haben:

- Grundkenntnisse in C# und .NET‑Entwicklung.  
- Eine integrierte Entwicklungsumgebung (IDE) wie Visual Studio.  
- Die Aspose.OCR für .NET‑Bibliothek installiert. Sie können sie [hier](https://releases.aspose.com/ocr/net/) herunterladen.  
- Ein Beispielbild, das Text für die OCR‑Erkennung enthält.

## Namespaces importieren

Stellen Sie sicher, dass die erforderlichen Namespaces in Ihr Projekt importiert wurden. Fügen Sie die folgenden Zeilen am Anfang Ihrer C#‑Datei hinzu:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Nun brechen wir den Prozess des Erhaltens von Rechtecken für Zeilen in der OCR‑Bilderkennung in leicht nachvollziehbare Schritte herunter.

## Layout‑Analyse OCR – Schritt‑für‑Schritt‑Anleitung

### Schritt 1: Dokumentverzeichnis einrichten

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Ersetzen Sie `"Your Document Directory"` durch den tatsächlichen Pfad zu dem Ordner, der Ihr Beispielbild enthält.

### Schritt 2: Aspose.OCR initialisieren

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Erzeugen Sie eine Instanz der Klasse `AsposeOcr`, um auf die OCR‑Funktionalität zuzugreifen.

### Schritt 3: Bildpfad angeben

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Definieren Sie den vollständigen Pfad zu dem Bild, das Sie mit OCR verarbeiten möchten.

### Schritt 4: Bild erkennen und Rechtecke erhalten

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

Die Methode `GetRectangles` gibt eine Liste von `Rectangle`‑Objekten zurück, wobei jedes die Koordinaten einer erkannten Textzeile darstellt. Dies ist der Kern des **Erhaltens von OCR‑Zeilenrechtecken** und ermöglicht **Layout‑Analyse OCR**.

### Schritt 5: Ergebnis ausgeben

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Geben Sie die Koordinaten der erkannten Bereiche in der Konsole aus. Sie sehen Werte, die Sie später verwenden können, um **Zeilenkoordinaten** für benutzerdefinierte Verarbeitung zu **extrahieren**.

## Warum Aspose.OCR für Zeilenrechtecke verwenden?

- **Hohe Genauigkeit** – Fortgeschrittene Algorithmen erkennen Zeilen selbst in verrauschten oder schiefen Bildern.  
- **Plattformübergreifend** – Funktioniert unter .NET Framework, .NET Core und .NET 5/6.  
- **Keine externen Abhängigkeiten** – Reine .NET‑Bibliothek, keine nativen DLLs zum Ausliefern.  
- **Umfangreiche Ausgabe** – Neben Zeilenrechtecken können Sie auch Wörter, Zeichen und Vertrauenswerte abrufen.

## Häufige Probleme und Lösungen

| Problem | Lösung |
|-------|----------|
| **Keine Rechtecke zurückgegeben** | Stellen Sie sicher, dass das Bild klaren, horizontalen Text enthält und `AreasType.LINES` angegeben ist. |
| **Falsche Koordinaten** | Überprüfen Sie die DPI des Bildes; Bilder mit niedriger Auflösung können ungenaue Grenzen erzeugen. |
| **Leistungsengpass bei großen Bildern** | Skalieren Sie das Bild auf eine angemessene Auflösung, bevor Sie `GetRectangles` aufrufen. |
| **Lizenz‑Ausnahme** | Verwenden Sie eine Testlizenz für die Entwicklung; setzen Sie eine Voll‑Lizenz in der Produktion ein, um Evaluationsbeschränkungen zu vermeiden. |

## Häufig gestellte Fragen

**F: Kann ich einzelne Wörter statt ganzer Zeilen extrahieren?**  
A: Ja, verwenden Sie `AreasType.WORDS` mit derselben `GetRectangles`‑Methode, um Wort‑Bounding‑Boxes zu erhalten.

**F: Unterstützt die API mehrseitige PDFs?**  
A: Konvertieren Sie jede PDF‑Seite zuerst in ein Bild und rufen Sie dann `GetRectangles` für jedes Bild auf.

**F: Wie gehe ich mit gedrehtem Text um?**  
A: Aktivieren Sie die Auto‑Rotate‑Option in den OCR‑Einstellungen oder drehen Sie das Bild vor der Verarbeitung manuell.

**F: Gibt es eine Möglichkeit, Vertrauenswerte für jede Zeile zu erhalten?**  
A: Nachdem Sie die Rechtecke erhalten haben, rufen Sie `api.RecognizeImage(...).Lines` auf, um Zeilenobjekte mit Vertrauenswerten zu erhalten.

**F: Welche .NET‑Versionen sind kompatibel?**  
A: Die Bibliothek funktioniert mit .NET Framework 4.5+, .NET Core 3.1+ und .NET 5/6.

## Praxisbeispiele

- **Dokument‑Layout‑Analyse OCR** – Füttern Sie Zeilenrechtecke in eine Layout‑Engine, um Spaltenstrukturen zu rekonstruieren.  
- **Automatisierte Datenaus extraction** – Nutzen Sie die Koordinaten, um einzelne Zeilen für nachgelagerte NLP‑Pipelines zuzuschneiden.  
- **Benutzerdefiniertes Rendering** – Überlagern Sie Bounding‑Boxes auf dem Originalbild für visuelle Verifikation oder UI‑Overlays.  

## Fazit

Herzlichen Glückwunsch! Sie haben erfolgreich **OCR‑Zeilenrechtecke** für ein Bild mit Aspose.OCR für .NET erhalten. Mit den Bounding‑Boxes in der Hand können Sie nun Zeilenkoordinaten in nachgelagerte Workflows wie benutzerdefiniertes Rendering, Datenaus extraction oder **Layout‑Analyse OCR** einspeisen.

---

**Zuletzt aktualisiert:** 2026-02-22  
**Getestet mit:** Aspose.OCR 24.11 für .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}