---
category: general
date: 2026-01-02
description: Erstellen Sie ein durchsuchbares PDF aus einem gescannten Bild‑PDF mit
  Aspose OCR. Erfahren Sie, wie Sie die OCR‑Sprache festlegen, eine Textebene einbetten
  und hochkomprimierte PDF‑Optionen anwenden.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- high compression pdf
- embed text layer pdf
- set OCR language
language: de
og_description: Erstellen Sie schnell durchsuchbare PDFs. Dieser Leitfaden zeigt,
  wie man gescannte Bild‑PDFs konvertiert, eine Textebene einbettet, die OCR‑Sprache
  festlegt und eine PDF mit hoher Kompression erstellt.
og_title: Erstellen Sie ein durchsuchbares PDF mit Aspose OCR – Vollständiger Leitfaden
tags:
- Aspose OCR
- Java PDF
- Document Automation
title: Erstellen Sie ein durchsuchbares PDF mit Aspose OCR – Schritt‑für‑Schritt‑Anleitung
url: /de/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Durchsuchbare PDF erstellen – Vollständiges Programmier‑Tutorial

Haben Sie jemals **durchsuchbare PDF**‑Dateien aus gescannten Bildern erstellen müssen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein. In vielen dokumentenintensiven Arbeitsabläufen ist ein reines Bild‑PDF eine Sackgasse für Suche und Indexierung.  

Die gute Nachricht ist, dass Sie mit Aspose OCR **gescannte Bild‑PDFs** in ein vollständig durchsuchbares Dokument mit nur wenigen Zeilen Java umwandeln können. Dieses Tutorial führt Sie durch jeden Schritt – Initialisierung der OCR‑Engine, Konfiguration von High‑Compression‑PDF‑Einstellungen, Einbetten einer versteckten Textebene und sogar die Auswahl der richtigen OCR‑Sprache.  

Am Ende dieses Leitfadens haben Sie ein ausführbares Programm, das ein durchsuchbares PDF erzeugt – eine Datei, die Sie problemlos in jede Suchmaschine oder jedes Dokumenten‑Management‑System einbinden können.

---

## Durchsuchbare PDF erstellen – Übersicht

Bevor wir in den Code eintauchen, lassen Sie uns klären, was „durchsuchbare PDF erstellen“ eigentlich bedeutet. Ein durchsuchbares PDF enthält zwei parallele Ebenen:

1. **Visuelle Ebene** – das originale gescannte Bild (oder gerenderte Seite).  
2. **Textebene** – unsichtbare, aber maschinenlesbare Zeichen, die durch OCR extrahiert wurden.

Wenn Sie ein solches PDF in Adobe Reader öffnen und Text auswählen, interagieren Sie tatsächlich mit der versteckten Textebene, nicht mit dem Bild. Dieser Dual‑Layer‑Ansatz ermöglicht die **embed text layer PDF**‑Funktionalität.

---

## Gescanntes Bild‑PDF mit Aspose OCR konvertieren

Das Erste, was Sie benötigen, ist ein gescanntes Bild (PNG, JPEG, TIFF), das Sie in ein PDF umwandeln möchten. Aspose OCR kann dieses Bild lesen, OCR ausführen und das Ergebnis an einen PDF‑Writer übergeben.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Step 2: Configure PDF save options to embed a searchable text layer
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // enable searchable PDF
        pdfSaveOptions.setCompressionLevel(9);        // optional: high compression

        // Step 3: Perform OCR on the scanned image and save the result as a searchable PDF
        ocrEngine.recognizeImageAndSave(
                "YOUR_DIRECTORY/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,                // set OCR language
                "YOUR_DIRECTORY/output.pdf",                // output PDF file
                pdfSaveOptions);                            // options defined above

        // Step 4: Indicate that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

**Warum das funktioniert:**  
- `setCreateSearchablePdf(true)` weist Aspose an, die versteckte Textebene zu erzeugen, wodurch die **embed text layer pdf**‑Anforderung erfüllt wird.  
- `setCompressionLevel(9)` bringt die Datei in den **high compression pdf**‑Bereich und reduziert die Endgröße, ohne die OCR‑Genauigkeit zu beeinträchtigen.  
- Das Argument `RecognitionLanguage.ENGLISH` zeigt, wie man **set OCR language** festlegt; Sie können es je nach Ausgangsmaterial gegen Französisch, Deutsch usw. austauschen.

---

## Einstellungen für hochkomprimierte PDFs

Große gescannte PDFs können schnell auf mehrere hundert Megabyte anwachsen. Aspose bietet eine einfache Kompressions‑API, die auf PDF‑Ebene arbeitet. Die Methode `setCompressionLevel` akzeptiert Werte von 0 (keine Kompression) bis 9 (maximale Kompression).

```java
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.setCompressionLevel(9); // 9 = strongest compression
```

- **Verwenden Sie verlustfreie Bildformate** (PNG) für textintensive Scans; JPEG ist besser für Fotos.  
- **Aktivieren Sie Font‑Subsetting**, wenn Sie benutzerdefinierte Schriften einbetten – Aspose erledigt dies automatisch, wenn Sie ein durchsuchbares PDF erstellen.  
- **Testen Sie die Ausgabedateigröße** nach jeder Änderung; manchmal liefert eine Kompression auf Stufe 8 eine 10 %ige Größenreduktion bei vernachlässigbarem Qualitätsverlust im Vergleich zu Stufe 9.

---

## Textebene in PDF für Durchsuchbarkeit einbetten

Wenn Sie den Aufruf `setCreateSearchablePdf(true)` weglassen, sieht die resultierende Datei zwar gut aus, Sie können jedoch deren Inhalt nicht durchsuchen. Die versteckte Textebene wird erstellt, indem jedes erkannte Zeichen seiner Position auf der Seite zugeordnet wird.

```java
pdfSaveOptions.setCreateSearchablePdf(true);
```

**Worauf Sie achten sollten:**  

- **Dokumente mit gemischten Sprachen** – Sie müssen möglicherweise OCR zweimal ausführen, einmal pro Sprache, und dann die Textebenen zusammenführen.  
- **Komplexe Layouts** (Tabellen, mehrspaltig) – Aspose leistet gute Arbeit, aber überprüfen Sie die Ausgabe mit einem PDF‑Viewer, der versteckten Text anzeigt (z. B. Adobe Acrobat „PDF bearbeiten“-Modus).

---

## OCR‑Sprache für genaue Erkennung festlegen

Die Genauigkeit der OCR‑Engine hängt von der Sprache ab, die Sie ihr vorgeben. Aspose liefert eine Reihe integrierter Sprachen, und Sie können auch benutzerdefinierte Sprachpakete hinzufügen.

```java
ocrEngine.recognizeImageAndSave(
        "input.png",
        RecognitionLanguage.ENGLISH, // change to RecognitionLanguage.FRENCH, etc.
        "output.pdf",
        pdfSaveOptions);
```

**Wann Sie die Sprache ändern sollten:**  

- Dokumente enthalten **nicht‑lateinische Schriften** (Kyrillisch, Arabisch) – wechseln Sie zur entsprechenden `RecognitionLanguage`.  
- Seiten mit gemischten Sprachen – Sie können `recognizeImageAndSave` zweimal aufrufen, jedes Mal mit einer anderen Sprache, und anschließend die PDFs zusammenführen.

---

## Ausführen des vollständigen Beispiels

Unten finden Sie das vollständige, sofort ausführbare Programm. Ersetzen Sie die Platzhalter‑Pfade durch echte Dateipfade, stellen Sie sicher, dass die Aspose OCR‑JAR in Ihrem Klassenpfad liegt, und führen Sie das Programm aus.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Configure PDF save options
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // embed text layer PDF
        pdfSaveOptions.setCompressionLevel(9);        // high compression PDF

        // Perform OCR and save searchable PDF
        ocrEngine.recognizeImageAndSave(
                "C:/scans/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,          // set OCR language
                "C:/output/searchable.pdf",           // output PDF
                pdfSaveOptions);                      // options defined above

        System.out.println("Searchable PDF created.");
    }
}
```

**Erwartete Ausgabe:** Wenn Sie das Programm ausführen, gibt die Konsole aus:

```
Searchable PDF created.
```

Öffnen Sie `searchable.pdf` in einem beliebigen PDF‑Viewer, versuchen Sie, Text auszuwählen, und Sie werden die unsichtbare Ebene in Aktion sehen. Sie haben erfolgreich **durchsuchbare PDF** aus einem gescannten Bild erstellt.

---

![Beispiel für durchsuchbare PDF erstellen](image-placeholder.png "Beispiel für durchsuchbare PDF erstellen")

*Der obige Screenshot (Platzhalter) würde typischerweise den PDF‑Viewer mit auswählbarem Text über einer gescannten Seite zeigen.*

---

## Fazit

Wir haben alles behandelt, was Sie benötigen, um **durchsuchbare PDF**‑Dateien mit Aspose OCR zu **erstellen**:

- Initialisieren Sie die OCR‑Engine.  
- **Gescanntes Bild‑PDF konvertieren**, indem Sie ein PNG/JPEG an `recognizeImageAndSave` übergeben.  
- Verwenden Sie `setCreateSearchablePdf(true)`, um **embed text layer PDF** zu erzeugen.  
- Wenden Sie `setCompressionLevel(9)` an für ein **high compression PDF**, das leicht bleibt.  
- Wählen Sie die passende `RecognitionLanguage`, um **set OCR language** für maximale Genauigkeit festzulegen.

Ab hier können Sie mit Batch‑Verarbeitung, verschiedenen Sprachen experimentieren oder sogar mehrere gescannte Seiten zu einem einzigen durchsuchbaren PDF kombinieren. Das gleiche Muster funktioniert für andere Sprachen wie Spanisch oder Japanisch – einfach das `RecognitionLanguage`‑Enum austauschen.

Zögern Sie nicht, einen Kommentar zu hinterlassen, falls Sie auf Probleme stoßen, und viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}