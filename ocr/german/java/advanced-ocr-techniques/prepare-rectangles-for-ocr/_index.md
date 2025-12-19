---
date: 2025-12-06
description: Erfahren Sie, wie Sie Aspose.OCR für Java verwenden, um OCR-Text-Erkennung
  durchzuführen, Text aus Bildern zu extrahieren und Rechtecke für gezielte Erkennung
  vorzubereiten.
linktitle: Preparing Rectangles for OCR Text Recognition in Aspose.OCR
second_title: Aspose.OCR Java API
title: Rechtecke für die OCR-Text-Erkennung in Aspose.OCR vorbereiten
url: /de/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vorbereiten von Rechtecken für die OCR-Text-Erkennung in Aspose.OCR

## Einleitung

In der heutigen datengetriebenen Welt ist **ocr text recognition** ein Grundpfeiler, um gescannte Dokumente, Screenshots und Fotos in durchsuchbare, editierbare Inhalte zu verwandeln. Aspose.OCR for Java macht diesen Prozess schnell und zuverlässig, besonders wenn Sie sich auf bestimmte Bereiche eines Bildes konzentrieren müssen. In diesem Tutorial führen wir Sie durch jeden Schritt, der erforderlich ist, um Rechtecke vorzubereiten, die OCR auf die gewünschten Regionen beschränken, und Ihnen so präzise Kontrolle und bessere Leistung zu geben.

## Schnelle Antworten
- **Welche Bibliothek übernimmt die OCR-Text-Erkennung in Java?** Aspose.OCR for Java.  
- **Benötige ich eine Lizenz für den Produktionseinsatz?** Ja – eine gültige Aspose.OCR-Lizenz schaltet die volle Funktionalität frei.  
- **Kann ich OCR auf bestimmte Bildbereiche beschränken?** Absolut; Sie definieren Rechtecke, die die Zielzonen begrenzen.  
- **Was sind die wichtigsten Voraussetzungen?** JDK 17+, Aspose.OCR for Java und eine Java‑IDE.  
- **Ist dieser Ansatz geeignet, um Text aus Bildern zu extrahieren?** Ja, es ist ein effizienter Weg, um **extract text image java** Projekte zu realisieren.

## Was ist OCR-Text-Erkennung?

OCR (Optical Character Recognition) Text-Erkennung wandelt pixelbasierte Bilder in maschinenlesbare Zeichen um. Sie ermöglicht das Suchen, Bearbeiten und Analysieren von Inhalten, die ursprünglich nur als Bilder vorlagen.

## Warum Rechtecke für die OCR-Text-Erkennung vorbereiten?

Das Definieren von Rechtecken fokussiert die Engine auf Bereiche, die tatsächlich Text enthalten, was:
* Die Verarbeitungszeit reduziert.
* Die Genauigkeit verbessert, indem störende Hintergründe ignoriert werden.
* Es Ihnen ermöglicht, nur die benötigten Daten zu extrahieren – ideal für Formulare, Rechnungen und Quittungen.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie folgendes haben:

- **Java Development Kit (JDK)** – Aspose.OCR for Java funktioniert mit JDK 17 oder höher. Laden Sie es von der Oracle-Website herunter.
- **Aspose.OCR for Java library** – Holen Sie sich die neueste JAR von der offiziellen Download‑Seite [here](https://releases.aspose.com/ocr/java/). Folgen Sie der Installationsanleitung [here](https://reference.aspose.com/ocr/java/).
- **Development Environment** – Jede Java‑IDE (IntelliJ IDEA, Eclipse, VS Code usw.) ist geeignet.

## Pakete importieren

In Ihrer Java-Quelldatei importieren Sie die erforderlichen Aspose.OCR‑Klassen und Standard‑Java‑Utilities:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

> *Wir importieren `java.awt.Rectangle`, weil die OCR‑API Rechtecke erwartet, die die zu scannenden Regionen definieren.*

## Schritt 1: Lizenz einrichten

```java
SetLicense.main(null);
```

Der Aufruf von `SetLicense` aktiviert Ihre Aspose.OCR‑Lizenz, entfernt Evaluationsbeschränkungen und ermöglicht die vollumfängliche OCR‑Text‑Erkennung.

## Schritt 2: Dokumentverzeichnis und Bildpfad festlegen

```java
String dataDir = "Your Document Directory";
String imagePath = dataDir + "p.png";
```

Ersetzen Sie `"Your Document Directory"` durch den absoluten Pfad, in dem Ihr Bild (`p.png`) liegt. Dies ist das Bild, das verarbeitet wird.

## Schritt 3: Aspose.OCR‑Instanz erstellen

```java
AsposeOCR api = new AsposeOCR();
```

Durch das Instanziieren von `AsposeOCR` erhalten Sie Zugriff auf die Methode `RecognizePage`, die das eigentliche OCR durchführt.

## Schritt 4: Rechtecke mit Texten vorbereiten

```java
ArrayList<Rectangle> rectArray = new ArrayList<Rectangle>();
rectArray.add(new Rectangle(138, 352, 2033, 537));
rectArray.add(new Rectangle(147, 890, 2033, 1157));
rectArray.add(new Rectangle(923, 2045, 465, 102));
rectArray.add(new Rectangle(104, 2147, 2076, 819));
```

Jedes `Rectangle(x, y, width, height)` teilt Aspose.OCR genau mit, wo nach Text gesucht werden soll. Passen Sie die Koordinaten an das Layout Ihres Quellbildes an.

## Schritt 5: OCR‑Erkennung durchführen

```java
try {
    String result = api.RecognizePage(imagePath, rectArray);
    System.out.println("Result with rect: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

Der Aufruf von `RecognizePage` verarbeitet nur die definierten Rechtecke und gibt die extrahierte Zeichenkette zurück. Die Konsolenausgabe ermöglicht es Ihnen, das Ergebnis der **ocr text recognition** sofort zu überprüfen.

## Häufige Probleme und Tipps

| Problem | Ursache | Lösung |
|---------|---------|--------|
| **Keine Ausgabe** | Falsche Rechteckkoordinaten oder Bildpfad | Überprüfen Sie den Wert von `dataDir` und stellen Sie sicher, dass die Rechtecke tatsächlich Textbereiche abdecken. |
| **Fehlerhafte Zeichen** | Bild mit niedriger Auflösung oder nicht unterstützte Schriftart | Verwenden Sie eine höher aufgelöste Quelle oder wenden Sie Bildvorverarbeitung an (z. B. Binarisierung). |
| **Lizenz nicht angewendet** | `SetLicense` nicht vor OCR aufgerufen | Stellen Sie sicher, dass `SetLicense.main(null);` vor allen API-Aufrufen ausgeführt wird. |
| **Leistungsverzögerung** | Zu viele große Rechtecke | Begrenzen Sie die Anzahl der Rechtecke und halten Sie sie so eng wie möglich um den Text. |

## Fazit

Sie haben nun gelernt, wie Sie Aspose.OCR for Java integrieren, eine Lizenz einrichten, Bildpfade definieren und – am wichtigsten – Rechtecke vorbereiten, um die **ocr text recognition** auf bestimmte Bildbereiche zu fokussieren. Diese Technik ist ideal für jedes **java ocr tutorial**, das eine präzise, hochleistungsfähige Textextraktion benötigt.

## Häufig gestellte Fragen

**Q: Ist Aspose.OCR mit anderen Programmiersprachen kompatibel?**  
A: Ja, Aspose.OCR unterstützt auch .NET, C++ und Python. Prüfen Sie die offiziellen Dokumente für sprachspezifische Beispiele.

**Q: Kann ich Aspose.OCR in einem kommerziellen Projekt verwenden?**  
A: Absolut. Kaufen Sie eine kommerzielle Lizenz über den [Aspose store](https://purchase.aspose.com/buy).

**Q: Gibt es eine kostenlose Testversion?**  
A: Ja, Sie können eine Testversion [here](https://releases.aspose.com/) herunterladen.

**Q: Wie erhalte ich eine temporäre Lizenz für die Evaluierung?**  
A: Temporäre Lizenzen werden über das [Aspose temporary‑license portal](https://purchase.aspose.com/temporary-license/) bereitgestellt.

**Q: Wo finde ich Community‑Support?**  
A: Besuchen Sie das Aspose.OCR [forum](https://forum.aspose.com/c/ocr/16) für Fragen, Tipps und Code‑Beispiele.

---

**Last Updated:** 2025-12-06  
**Tested With:** Aspose.OCR for Java 24.12  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
