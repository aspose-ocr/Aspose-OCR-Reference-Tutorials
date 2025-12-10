---
date: 2025-12-10
description: Lernen Sie, wie Sie Text aus einem Bild erkennen und Absätze aus einem
  Bild extrahieren, mit Aspose.OCR für Java. Schritt‑für‑Schritt‑Anleitung mit Codebeispielen.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: Texterkennung aus Bild und Ermittlung von Textbereichs‑Rechtecken
url: /de/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild erkennen und Textbereich‑Rechtecke abrufen

## Introduction

Wenn Sie **recognize text from image**‑Dateien in einer Java‑Anwendung benötigen, bietet Aspose.OCR für Java eine schnelle, genaue Möglichkeit, dies zu tun. In diesem Tutorial führen wir Sie Schritt für Schritt durch die erforderlichen Vorgänge, um Absätze aus einem Bild zu extrahieren, die Begrenzungsrechtecke für jeden Textbereich zu erhalten und diese Koordinaten in der Konsole auszugeben. Am Ende verstehen Sie, warum dieser Ansatz funktioniert, wie Sie die Bibliothek integrieren und wo Sie sie für Ihre eigenen Anwendungsfälle erweitern können.

## Quick Answers
- **Was bedeutet “recognize text from image”?** Es bedeutet, visuelle Zeichen in einem Bild in editierbare Zeichenketten zu konvertieren.  
- **Welche Bibliothek erledigt das in Java?** Aspose.OCR für Java.  
- **Benötige ich eine Lizenz für die Entwicklung?** Eine temporäre Lizenz ist zum Testen verfügbar; für die Produktion ist eine Voll‑Lizenz erforderlich.  
- **Kann ich Absätze statt einzelner Wörter extrahieren?** Ja – verwenden Sie `AreasType.PARAGRAPHS`, um Rechtecke auf Absatz‑Ebene zu erhalten.  
- **Ist der Code mit Java 11+ kompatibel?** Absolut, die API funktioniert mit Java 11 und neueren Versionen.

## What is “recognize text from image” in Aspose.OCR?
Die `RecognizePage`‑Methode von Aspose.OCR analysiert das Bitmap, wendet OCR‑Algorithmen an und gibt die erkannte Zeichenkette zurück. Wenn Sie Textbereiche anfordern, berechnet die Bibliothek zudem die genauen `Rectangle`‑Koordinaten für jeden Textblock, sodass Sie später bestimmte Abschnitte leicht hervorheben oder verarbeiten können.

## Why use Aspose.OCR for Java?
- **Hohe Genauigkeit** – unterstützt mehrere Sprachen und komplexe Schriftarten.  
- **Einfache Integration** – ein einzelnes JAR fügt vollständige OCR‑Funktionen hinzu.  
- **Flexibler Output** – Sie können Rohtext, formatiertes HTML oder präzise Text‑Bereich‑Rechtecke abrufen.  
- **Thread‑sicher** – geeignet für Hochdurchsatz‑Serverumgebungen.

## Prerequisites

- **Java Development Kit** (JDK 11 oder neuer) auf Ihrem Rechner installiert.  
- **Aspose.OCR für Java** Bibliothek – laden Sie sie von der offiziellen Seite [hier](https://releases.aspose.com/ocr/java/) herunter.  
- Eine IDE oder ein Build‑Tool (Maven/Gradle), um die JAR‑Abhängigkeit zu verwalten.

## Import Packages

Importieren Sie in Ihrem Java‑Projekt die erforderlichen Klassen:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Step‑by‑Step Guide

### Step 1: Set Up Your Project
Erstellen Sie ein neues Java‑Projekt (oder fügen Sie es zu einem bestehenden hinzu) und platzieren Sie das Aspose.OCR‑JAR im Klassenpfad. Wenn Sie Maven verwenden, fügen Sie die Abhängigkeit wie im Download‑Paket beschrieben hinzu.

### Step 2: Define Document Directory and Image Path
Geben Sie an, wo Ihr Beispielbild liegt:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Step 3: Create Aspose.OCR Instance
Instanziieren Sie die OCR‑Engine:

```java
// Create Aspose.OCR instance
AsposeOCR api = new AsposeOCR();
```

### Step 4: Recognize Text in the Image
Rufen Sie `RecognizePage` auf, um das Bild in Klartext zu konvertieren. Dieser Schritt demonstriert die Kern‑**recognize text from image**‑Funktionalität:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Step 5: Get Rectangles with Text Areas
Jetzt rufen Sie die Begrenzungsrechtecke für jeden Absatz (oder andere Bereichstypen) ab. Hier extrahieren Sie **paragraphs from image** und erhalten deren Koordinaten:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Common Issues & Troubleshooting

| Symptom | Wahrscheinliche Ursache | Lösung |
|---------|--------------------------|--------|
| `IOException` bei `RecognizePage` | Falscher Dateipfad oder fehlende Leseberechtigung | Stellen Sie sicher, dass `imagePath` auf ein vorhandenes PNG/JPG zeigt und die Anwendung Zugriff auf das Dateisystem hat. |
| Leere Ergebniszeichenkette | Bild von schlechter Qualität oder nicht unterstützte Sprache | Bild vorverarbeiten (Kontrast erhöhen, binarisieren) oder die korrekte Sprache mit `api.setLanguage("eng")` angeben. |
| Keine Rechtecke zurückgegeben | Falscher `AreasType` verwendet (z. B. `WORDS` statt Absätzen) | Wechseln Sie zu `AreasType.PARAGRAPHS` oder `AreasType.LINES` nach Bedarf. |

## Frequently Asked Questions

**F: Ist Aspose.OCR mit Java 11 kompatibel?**  
A: Ja, Aspose.OCR funktioniert mit Java 11 und neueren Versionen.

**F: Kann ich Aspose.OCR sowohl für private als auch kommerzielle Projekte nutzen?**  
A: Ja, Sie können es in jeder Art von Projekt verwenden. Lizenzdetails finden Sie [hier](https://purchase.aspose.com/buy).

**F: Wie erhalte ich eine temporäre Lizenz für die Evaluierung?**  
A: Sie können eine temporäre Lizenz [hier](https://purchase.aspose.com/temporary-license/) erhalten.

**F: Wo finde ich Community‑Support oder offizielle Hilfe?**  
A: Für Support und Diskussionen besuchen Sie das [Aspose.OCR‑Forum](https://forum.aspose.com/c/ocr/16).

**F: Unterstützt Aspose.OCR Multithreading?**  
A: Ja, die Bibliothek ist thread‑sicher und kann in gleichzeitigen Umgebungen für bessere Leistung verwendet werden.

## Conclusion

In diesem Tutorial haben Sie gelernt, wie man **recognize text from image**‑Dateien mit Aspose.OCR für Java erkennt, Absätze extrahiert und die genauen Rechtecke abruft, die jeden Textblock umgeben. Diese Möglichkeiten ermöglichen Ihnen, durchsuchbare PDFs zu erstellen, Text in UI‑Overlays hervorzuheben oder strukturierte Daten in nachgelagerte Prozesse einzuspeisen. Erkunden Sie die API weiter, um Spracheinstellungen anzupassen, verschiedene Bildformate zu verarbeiten oder die Integration mit Cloud‑Speicher vorzunehmen.

---

**Zuletzt aktualisiert:** 2025-12-10  
**Getestet mit:** Aspose.OCR 23.10 für Java  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}