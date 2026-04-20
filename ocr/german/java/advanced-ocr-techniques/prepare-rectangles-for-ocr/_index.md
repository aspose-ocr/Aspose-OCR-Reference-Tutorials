---
date: 2026-02-20
description: Erfahren Sie, wie Sie Seitenrechtecke mit Aspose.OCR für Java erkennen,
  Text aus Bild‑Java‑Projekten extrahieren und diesem Aspose OCR Java‑Tutorial für
  präzise OCR folgen.
linktitle: How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR
second_title: Aspose.OCR Java API
title: Wie man Seitenrechtecke für die OCR-Text-Erkennung in Aspose.OCR erkennt
url: /de/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Seitenrechtecke für die OCR-Text-Erkennung in Aspose.OCR erkennt

## Schnelle Antworten
- **Welche Bibliothek übernimmt die OCR-Text-Erkennung in Java?** Aspose.OCR for Java.  
- **Benötige ich eine Lizenz für den Produktionseinsatz?** Ja – eine gültige Aspose.OCR‑Lizenz schaltet die volle Funktionalität frei.  
- **Kann ich OCR auf bestimmte Bildbereiche beschränken?** Absolut; Sie definieren Rechtecke, die die Zielzonen begrenzen.  
- **Was sind die wichtigsten Voraussetzungen?** JDK 17+, Aspose.OCR for Java und eine Java‑IDE.  
- **Ist dieser Ansatz geeignet, um Text aus Bildern zu extrahieren?** Ja, es ist ein effizienter Weg, um **extract text image java**‑Projekte zu realisieren.

## Was bedeutet „Seitenrechtecke erkennen“?
Der Ausdruck bezieht sich auf die Praxis, dem OCR‑Engine eine Liste von `java.awt.Rectangle`‑Objekten zu übergeben, sodass nur diese spezifischen Regionen einer Seite verarbeitet werden. Dieser fokussierte Ansatz reduziert die Verarbeitungszeit und verbessert die Genauigkeit, besonders bei komplexen Dokumenten wie Rechnungen oder Formularen.

## Warum Rechtecke für die OCR-Text-Erkennung vorbereiten?
Das Definieren von Rechtecken fokussiert die Engine auf Bereiche, die tatsächlich Text enthalten, was:
* Die Verarbeitungszeit reduziert.  
* Die Genauigkeit verbessert, indem störende Hintergründe ignoriert werden.  
* Es Ihnen ermöglicht, nur die benötigten Daten zu extrahieren – ideal für Formulare, Rechnungen und Quittungen.  

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

- **Java Development Kit (JDK)** – Aspose.OCR for Java funktioniert mit JDK 17 oder höher. Laden Sie es von der Oracle‑Website herunter.  
- **Aspose.OCR for Java library** – Holen Sie sich das neueste JAR von der offiziellen Download‑Seite [hier](https://releases.aspose.com/ocr/java/). Folgen Sie dem Installationsleitfaden [hier](https://reference.aspose.com/ocr/java/).  
- **Entwicklungsumgebung** – Jede Java‑IDE (IntelliJ IDEA, Eclipse, VS Code usw.) ist geeignet.

## Pakete importieren

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

> *Wir importieren `java.awt.Rectangle`, weil die OCR‑API Rechtecke erwartet, die die zu scannenden Bereiche definieren.*

## Schritt 1: Lizenz einrichten

```java
SetLicense.main(null);
```

Der Aufruf von `SetLicense` aktiviert Ihre Aspose.OCR‑Lizenz, entfernt Evaluationsbeschränkungen und ermöglicht die vollständige OCR‑Text‑Erkennung.

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

Durch die Instanziierung von `AsposeOCR` erhalten Sie Zugriff auf die Methode `RecognizePage`, die das eigentliche OCR ausführt.

## Schritt 4: Rechtecke mit Texten vorbereiten

```java
ArrayList<Rectangle> rectArray = new ArrayList<Rectangle>();
rectArray.add(new Rectangle(138, 352, 2033, 537));
rectArray.add(new Rectangle(147, 890, 2033, 1157));
rectArray.add(new Rectangle(923, 2045, 465, 102));
rectArray.add(new Rectangle(104, 2147, 2076, 819));
```

Jedes `Rectangle(x, y, width, height)` teilt Aspose.OCR exakt mit, wo nach Text gesucht werden soll. Passen Sie die Koordinaten an das Layout Ihres Quellbildes an.

## Schritt 5: OCR-Erkennung durchführen

```java
try {
    String result = api.RecognizePage(imagePath, rectArray);
    System.out.println("Result with rect: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

Der Aufruf von `RecognizePage` verarbeitet nur die definierten Rechtecke und gibt den extrahierten String zurück. Die Konsolenausgabe ermöglicht es Ihnen, das Ergebnis der **ocr text recognition** sofort zu überprüfen.

## Häufige Probleme und Tipps

| Problem | Ursache | Lösung |
|---------|---------|--------|
| **Keine Ausgabe** | Falsche Rechteckkoordinaten oder Bildpfad | Überprüfen Sie den Wert von `dataDir` und stellen Sie sicher, dass die Rechtecke tatsächlich Textbereiche abdecken. |
| **Fehlerhafte Zeichen** | Niedrigauflösendes Bild oder nicht unterstützte Schriftart | Verwenden Sie eine höher aufgelöste Quelle oder wenden Sie Bildvorverarbeitung an (z. B. Binarisierung). |
| **Lizenz nicht angewendet** | `SetLicense` wurde nicht vor OCR aufgerufen | Stellen Sie sicher, dass `SetLicense.main(null);` vor allen API‑Aufrufen ausgeführt wird. |
| **Leistungsverzögerung** | Zu viele große Rechtecke | Begrenzen Sie die Anzahl der Rechtecke und halten Sie sie so eng wie möglich um den Text. |

## Häufig gestellte Fragen

**Q:** *Ist Aspose.OCR mit anderen Programmiersprachen kompatibel?*  
**A:** Ja, Aspose.OCR unterstützt auch .NET, C++ und Python. Weitere sprachspezifische Beispiele finden Sie in der offiziellen Dokumentation.

**Q:** *Kann ich Aspose.OCR in einem kommerziellen Projekt verwenden?*  
**A:** Absolut. Kaufen Sie eine kommerzielle Lizenz über den [Aspose store](https://purchase.aspose.com/buy).

**Q:** *Gibt es eine kostenlose Testversion?*  
**A:** Ja, Sie können eine Testversion [hier](https://releases.aspose.com/) herunterladen.

**Q:** *Wie erhalte ich eine temporäre Lizenz für die Evaluierung?*  
**A:** Temporäre Lizenzen werden über das [Aspose temporary‑license portal](https://purchase.aspose.com/temporary-license/) bereitgestellt.

**Q:** *Wo kann ich Community‑Support erhalten?*  
**A:** Besuchen Sie das Aspose.OCR [Forum](https://forum.aspose.com/c/ocr/16) für Fragen, Tipps und Codebeispiele.

## Fazit

Sie haben nun gelernt, wie Sie **Seitenrechtecke** mit Aspose.OCR für Java erkennen, eine Lizenz einrichten, Bildpfade definieren und – am wichtigsten – enge Rechtecke vorbereiten, um OCR auf die genauen Bildbereiche zu fokussieren, die Sie benötigen. Diese Technik ist ideal für jedes **aspose ocr java tutorial**, das eine präzise, leistungsstarke Textextraktion erfordert.

---

**Last Updated:** 2026-02-20  
**Tested With:** Aspose.OCR for Java 24.12  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}