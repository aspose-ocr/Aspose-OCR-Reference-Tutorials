---
date: 2025-12-21
description: Erfahren Sie, wie Sie OCR durchführen und Text aus einem Bild mit Aspose.OCR
  für .NET extrahieren. Diese Schritt‑für‑Schritt‑Anleitung zeigt die mehrsprachige
  Texterkennung und die Sprachauswahl.
linktitle: How to Perform OCR with Language Selection in Aspose.OCR
second_title: Aspose.OCR .NET API
title: Wie man OCR mit Sprachauswahl in Aspose.OCR durchführt
url: /de/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR mit Sprachauswahl in Aspose.OCR durchführt

## Einführung

Wenn Sie **wie man OCR durchführt** auf Bildern und Text aus Bilddateien in einer .NET‑Anwendung extrahieren müssen, bietet Aspose.OCR für .NET eine schnelle, genaue und sprachbewusste Lösung. In diesem Tutorial führen wir Sie durch ein praxisnahes Beispiel, das die OCR‑Bilderkennung mit Sprachauswahl demonstriert, sodass Sie mehrsprachigen Text aus Bildern mit nur wenigen Codezeilen extrahieren können.

## Schnelle Antworten
- **Was macht Aspose.OCR?** Es erkennt gedruckten und handgeschriebenen Text in Bildern und gibt den extrahierten Text zurück.  
- **Kann ich die Sprache auswählen?** Ja – Sie können jede unterstützte Sprache wie Englisch, Deutsch, Spanisch, Chinesisch usw. angeben.  
- **Benötige ich eine Lizenz für die Entwicklung?** Eine kostenlose Testversion reicht für die Evaluierung; für den Produktionseinsatz ist eine Lizenz erforderlich.  
- **Welche .NET‑Versionen werden unterstützt?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Ist die Schräglagenkorrektur automatisch?** Sie können `AutoSkew` aktivieren und die Einstellung `SkewAngle` feinjustieren.

## Warum Aspose.OCR für OCR‑Aufgaben wählen?

- **Hohe Genauigkeit** über mehrere Schriftarten und Bildqualitäten hinweg.  
- **Eingebaute Sprachauswahl** eliminiert die Notwendigkeit externer Sprachpakete.  
- **Einfaches API**, das sich nahtlos in bestehende C#‑Projekte integrieren lässt.  
- **Keine externen Abhängigkeiten** – alles läuft lokal, wodurch Ihre Daten sicher bleiben.

## Voraussetzungen

Bevor wir in den Code eintauchen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllt haben:

- Aspose.OCR für .NET: Stellen Sie sicher, dass die Aspose.OCR‑Bibliothek installiert ist. Sie können sie von der [Aspose.OCR für .NET Download‑Seite](https://releases.aspose.com/ocr/net/) herunterladen.

- Entwicklungsumgebung: Richten Sie eine Arbeitsumgebung mit einer .NET‑Anwendung ein. Wenn Sie das noch nicht getan haben, lesen Sie die [Dokumentation](https://reference.aspose.com/ocr/net/) für detaillierte Anweisungen.

## Namespaces importieren

In Ihrer .NET‑Anwendung beginnen Sie mit dem Import der erforderlichen Namespaces:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Schritt 1: Aspose.OCR initialisieren

Beginnen Sie mit der Initialisierung einer Instanz der Aspose.OCR‑Klasse. Dies legt die Grundlage für die Nutzung der OCR‑Funktionen in Ihrer Anwendung.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Schritt 2: Bildpfad angeben

Definieren Sie anschließend den Pfad zu dem Bild, das Sie mit OCR verarbeiten möchten. Stellen Sie sicher, dass das Bild für Ihre Anwendung zugänglich ist.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## Schritt 3: Bild mit Sprachauswahl erkennen

Nun kommt die eigentliche OCR‑Operation. Verwenden Sie die Aspose.OCR‑Bibliothek, um Text aus dem angegebenen Bild zu erkennen. Passen Sie die Erkennungseinstellungen an, einschließlich der Sprachauswahl.

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## Schritt 4: Ergebnisse ausgeben und anzeigen

Nach der OCR‑Operation geben Sie die Ergebnisse aus und zeigen sie an, einschließlich des erkannten Textes, der Bereiche, Warnungen und der JSON‑Darstellung.

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## Häufige Probleme und Tipps

- **Falsche Sprachauswahl** – Wenn die Ausgabe unleserlich erscheint, prüfen Sie, ob die `Language`‑Eigenschaft mit der Sprache des Quellbildes übereinstimmt.  
- **Schräge Bilder** – Aktivieren Sie `AutoSkew` oder passen Sie `SkewAngle` manuell an, um die Genauigkeit bei geneigten Scans zu verbessern.  
- **Große Dateien** – Verarbeiten Sie große Bilder in Teilen oder reduzieren Sie die Auflösung, bevor Sie sie an `RecognizeImage` übergeben, um Speicher zu schonen.

## Fazit

Herzlichen Glückwunsch! Sie haben **wie man OCR durchführt** mit Sprachauswahl mithilfe von Aspose.OCR für .NET gelernt. Dieses Tutorial zeigte Ihnen, wie Sie Text aus Bilddateien extrahieren, Erkennungseinstellungen anpassen und mehrsprachige Inhalte mühelos verarbeiten können.

## FAQ

### Q1: Ist Aspose.OCR für die Erkennung mehrsprachiger Texte geeignet?

A1: Ja, Aspose.OCR unterstützt verschiedene Sprachen und bietet damit Flexibilität für mehrsprachige OCR‑Aufgaben.

### Q2: Kann ich OCR‑Einstellungen für bestimmte Bildmerkmale feinjustieren?

A2: Absolut! Passen Sie Parameter wie Schräglage, Zeilenerkennung und Bereichserkennung an, um OCR für unterschiedliche Szenarien zu optimieren.

### Q3: Wo finde ich zusätzliche Unterstützung oder Community‑Diskussionen?

A3: Besuchen Sie das [Aspose.OCR‑Forum](https://forum.aspose.com/c/ocr/16) für Support und Diskussionen mit der Community.

### Q4: Gibt es eine kostenlose Testversion?

A4: Ja, testen Sie die [kostenlose Testversion](https://releases.aspose.com/), um die Fähigkeiten von Aspose.OCR kennenzulernen.

### Q5: Wie kann ich Aspose.OCR für .NET erwerben?

A5: Zum Kauf besuchen Sie die [Kaufseite](https://purchase.aspose.com/buy).

---

**Zuletzt aktualisiert:** 2025-12-21  
**Getestet mit:** Aspose.OCR 24.11 für .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}