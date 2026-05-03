---
category: general
date: 2026-05-03
description: Wie man OCR verwendet, um Text aus PDF‑Dateien in Java zu extrahieren.
  Erfahren Sie, wie man Text aus PDFs erkennt, PDFs in Text umwandelt und OCR für
  mehrseitige PDFs effizient verarbeitet.
draft: false
keywords:
- how to use ocr
- extract text from pdf
- recognize text from pdf
- convert pdf to text
- ocr multi page pdf
language: de
og_description: Wie man OCR verwendet, um Text aus PDF-Dateien in Java zu extrahieren.
  Dieser Leitfaden zeigt, wie man Text aus PDFs erkennt, PDFs in Text konvertiert
  und OCR für mehrseitige PDFs verarbeitet.
og_title: Wie man OCR in Java verwendet – Text aus mehrseitigen PDFs extrahieren
tags:
- ocr
- java
- pdf
- aspose
title: Wie man OCR in Java verwendet – Text aus mehrseitigen PDFs extrahieren
url: /de/python-java/general/how-to-use-ocr-in-java-extract-text-from-multi-page-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in Java verwendet – Text aus mehrseitigen PDFs extrahieren

**How to use OCR** in einem Java‑Projekt? Wenn Sie jemals Text aus PDF‑Dateien extrahieren mussten, ohne sich auf die interne Textebene des PDFs zu verlassen, sind Sie hier genau richtig. Dieses Tutorial führt Sie durch eine vollständige, ausführbare Lösung, die **Text aus PDF erkennt**, PDF in Text konvertiert und sogar ein **OCR‑Mehrseitiges‑PDF** mit einem einzigen Aufruf verarbeitet.

Stellen Sie sich vor, Sie erhalten einen gescannten Vertrag — ein 12‑seitiges TIFF in einem PDF. Sie benötigen den durchsuchbaren Text für die Indexierung, aber die Datei enthält keine eingebetteten Zeichen. Kein Problem; wir zeigen Ihnen genau, wie Sie das Schritt für Schritt erledigen.

> **Was Sie erhalten:** ein sofort einsatzbereites Java‑Snippet mit Aspose.OCR, Erklärungen, warum jede Zeile wichtig ist, Tipps zu häufigen Fallstricken und ein Beispiel‑Ausgabe, die Sie sofort überprüfen können.

## Was Sie benötigen

* **Java 17** (oder ein aktuelles JDK) – der Code funktioniert auch mit älteren Versionen, aber 17 ist der optimale Punkt.
* **Aspose OCR for Java** Bibliothek – Sie können das JAR von der Aspose‑Website herunterladen oder über Maven/Gradle einbinden.
* Ein **mehrseitiges PDF** (oder TIFF), das Sie verarbeiten möchten. In unseren Beispielen verwenden wir `contract_multipage.pdf`, das in einem Ordner namens `YOUR_DIRECTORY` liegt.
* Eine gültige **Aspose OCR Lizenzdatei** (`Aspose.OCR.Java.lic`). Ohne diese läuft die Bibliothek im Evaluierungsmodus, was für einen schnellen Test in Ordnung ist, aber ein Wasserzeichen hinzufügt.

Das war’s – keine zusätzlichen OCR‑Engines, keine nativen Binärdateien, nur ein einzelnes JAR und eine Lizenz.

![Beispiel zur Verwendung von OCR](https://example.com/ocr-demo.png "Wie man OCR in Java verwendet – visuelle Übersicht des Prozesses")

*Bildbeschreibung: Wie man OCR in Java verwendet – visuelle Übersicht über das Laden, Erkennen und Ausgeben von Text.*

## Schritt 1: OCR‑Engine einrichten – **How to Use OCR** korrekt

Das Erste, was Sie tun müssen, ist eine Instanz der OCR‑Engine zu erstellen und Ihre Lizenz anzuwenden. Ohne Lizenz funktioniert die Engine zwar, aber Sie sehen ein Test‑Wasserzeichen in der Ausgabe.

```java
// Import the Aspose OCR package
import com.aspose.ocr.*;

public class OcrPdfDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Apply your license – replace the path with your actual .lic file
        ocrEngine.setLicense(new License().setLicense("Aspose.OCR.Java.lic"));
```

**Warum das wichtig ist:**  
Der `OcrEngine` ist das Kernobjekt, das die Bildanalyse, Spracherkennung und Textextraktion steuert. Das frühe Setzen der Lizenz verhindert, dass die Engine später in den Testmodus zurückfällt, was die Genauigkeit beeinträchtigen könnte.

## Schritt 2: Dokument laden – **Extract Text from PDF** effizient

Aspose OCR kann sowohl PDF‑ als auch TIFF‑Container direkt lesen. Hier laden wir ein mehrseitiges PDF, das gescannte Bilder enthält.

```java
        // 3️⃣ Load a multi‑page PDF (or TIFF) from disk
        PdfDocument pdfDoc = PdfDocument.fromFile("YOUR_DIRECTORY/contract_multipage.pdf");
```

**Warum das wichtig ist:**  
`PdfDocument.fromFile` analysiert den Container und gibt Ihnen Zugriff auf jede Seite als Bild. Diese Abstraktion ermöglicht es der OCR‑Engine, jede Seite einheitlich zu behandeln, unabhängig vom ursprünglichen Format.

**Tipp:** Wenn Ihre Quelldatei ein TIFF ist, funktioniert derselbe Aufruf – Aspose erkennt das Format automatisch. Kein zusätzlicher Code erforderlich.

## Schritt 3: Alle Seiten auf einmal erkennen – **Recognize Text from PDF** nahtlos

Statt selbst über die Seiten zu iterieren, können Sie die Engine auffordern, das gesamte Dokument in einem einzigen Aufruf zu verarbeiten. Dies ist der effizienteste Weg, **PDF in Text zu konvertieren**, wenn Sie ein **OCR‑Mehrseitiges‑PDF** verarbeiten.

```java
        // 4️⃣ Recognize text on all pages with a single method call
        List<OcrPageResult> recognizedPages = ocrEngine.recognizeDocument(pdfDoc);
```

**Warum das wichtig ist:**  
Einmal `recognizeDocument` aufzurufen reduziert den Overhead, der durch wiederholtes Initialisieren der Engine entsteht. Es garantiert zudem konsistente Spracheinstellungen über alle Seiten hinweg, was bei juristischen Dokumenten, die häufig verschiedene Schriftarten mischen, entscheidend ist.

## Schritt 4: Erkannten Text ausgeben – **Convert PDF to Text** für die Indexierung

Jetzt, da jede Seite verarbeitet wurde, iterieren wir einfach über die Ergebnisse und geben die extrahierten Zeichenketten aus. Sie können sie auch in eine Datei, eine Datenbank schreiben oder in einen Suchindex einspeisen.

```java
        // 5️⃣ Loop through each page's result and print the text
        for (int i = 0; i < recognizedPages.size(); i++) {
            OcrPageResult pageResult = recognizedPages.get(i);
            System.out.println("--- Page " + (i + 1) + " ---");
            System.out.println(pageResult.getText());
        }
    }
}
```

**Erwartete Ausgabe (gekürzt):**

```
--- Page 1 ---
THIS AGREEMENT is made on the 1st day of January 2024...
--- Page 2 ---
WHEREAS, the Parties desire to...
...
```

Enthält das PDF 12 Seiten, sehen Sie zwölf `--- Page X ---`‑Abschnitte, jeweils gefolgt vom OCR‑extrahierten Text.

## Erweiterte Tipps für ein **OCR Multi Page PDF**

### 1. Spracheinstellungen anpassen

Standardmäßig versucht Aspose, die Sprache automatisch zu erkennen, aber Sie können den Vorgang beschleunigen, indem Sie sie angeben:

```java
ocrEngine.getLanguage().setLanguage(Language.ENGLISH);
```

### 2. Bildvorverarbeitung steuern

Gescannte Verträge enthalten oft Rauschen. Sie können Entzerrung und Binarisierung aktivieren:

```java
ocrEngine.getImageProcessingOptions()
        .setDeskew(true)
        .setBinarization(true);
```

### 3. Große Dateien elegant verarbeiten

Wenn Sie PDFs größer als 100 MB verarbeiten, sollten Sie das Streaming von Seiten in Betracht ziehen, anstatt das gesamte Dokument auf einmal zu laden:

```java
for (int pageNum = 1; pageNum <= pdfDoc.getPageCount(); pageNum++) {
    OcrPageResult result = ocrEngine.recognizePage(pdfDoc.getPage(pageNum));
    // process result...
}
```

Dieses Muster reduziert den Speicherverbrauch und ist praktisch für Batch‑Jobs.

### 4. Export in strukturierte Formate

Neben einfachem Text können Sie in JSON oder XML für die Weiterverarbeitung exportieren:

```java
String json = pageResult.toJson();
System.out.println(json);
```

## Häufige Fallstricke & wie man sie vermeidet

| Fallstrick | Warum es passiert | Lösung |
|------------|-------------------|--------|
| **Leere Ausgabe** | Lizenz nicht angewendet oder Dateipfad falsch. | Überprüfen Sie den Pfad von `setLicense` und stellen Sie sicher, dass die Datei existiert. |
| **Fehlerhafte Zeichen** | Falsche Spracheinstellung oder Quelle mit niedriger Auflösung. | Setzen Sie die korrekte `Language` und stellen Sie sicher, dass Quellbilder ≥300 dpi haben. |
| **Speicher‑Fehler** | Ein riesiges PDF auf einmal laden. | Verwenden Sie den oben gezeigten Streaming‑Ansatz. |
| **Teilweise Seitenerkennung** | PDF enthält gemischte Raster‑/Vektorschichten. | Flachlegen Sie das PDF zuerst: `pdfDoc.flatten();` vor OCR. |

## Zusammenfassung – Was wir behandelt haben

* **How to use OCR** mit Aspose in Java.
* **Extract text from PDF** (oder TIFF) in einem einzigen Aufruf.
* **Recognize text from PDF** über alle Seiten hinweg ohne manuelle Schleifen.
* **Convert PDF to Text** und geben es sauber aus.
* Tipps zum Umgang mit einem **OCR multi page PDF**, einschließlich Sprachanpassungen und speichereffizientem Streaming.

Sie haben jetzt ein vollständiges, produktionsreifes Snippet, das Sie in jedes Java‑Projekt einbinden können. Passen Sie gern die Bildverarbeitungsoptionen an, ändern Sie das Ausgabeziel oder integrieren Sie das Ergebnis in einen Suchindex.

## Nächste Schritte

* **Entdecken Sie die erweiterten Funktionen von Aspose OCR** – wie Handschriftenerkennung oder PDF/A‑Konformität.
* **Kombinieren Sie OCR mit PDF‑Manipulation** (z. B. eine versteckte Textebene wieder in das PDF einfügen, um durchsuchbare PDFs zu erhalten).
* **Automatisieren Sie die Batch‑Verarbeitung**, indem Sie einen Ordner mit PDFs einlesen und jedes Ergebnis in eine entsprechende `.txt`‑Datei schreiben.

Wenn Sie auf Probleme stoßen, sind die Aspose‑Foren ein guter Ort, um Hilfe zu erhalten, und die API‑Referenz liefert ausführliche Details zu jeder hier verwendeten Methode.

Viel Spaß beim Coden und beim Umwandeln dieser hartnäckigen Scans in durchsuchbaren Text!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}