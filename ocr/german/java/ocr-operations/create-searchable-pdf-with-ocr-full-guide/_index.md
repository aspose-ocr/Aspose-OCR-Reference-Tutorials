---
category: general
date: 2026-06-22
description: Erstelle ein durchsuchbares PDF mit OCR in Java. Erfahre, wie du die
  Kompression deaktivierst und ein gescanntes Bild‑PDF schnell in ein durchsuchbares
  PDF umwandelst.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- ocr to searchable pdf
- how to disable compression
- pdf without compression
language: de
og_description: Erstelle ein durchsuchbares PDF mit OCR in Java. Dieser Leitfaden
  zeigt, wie man die Kompression deaktiviert, ein gescanntes Bild‑PDF konvertiert
  und ein PDF ohne Kompression erzeugt.
og_title: Durchsuchbares PDF mit OCR erstellen – Vollständiges Java‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  headline: Create Searchable PDF with OCR – Full Guide
  type: TechArticle
- description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  name: Create Searchable PDF with OCR – Full Guide
  steps:
  - name: Set the output format to `PDF_SEARCHABLE`.
    text: Set the output format to `PDF_SEARCHABLE`.
  - name: Turn off PDF compression with `PdfCompression.NONE`.
    text: Turn off PDF compression with `PdfCompression.NONE`.
  - name: Run OCR and capture the `PdfDocument`.
    text: Run OCR and capture the `PdfDocument`.
  - name: Save the file to disk.
    text: Save the file to disk.
  type: HowTo
tags:
- OCR
- PDF
- Java
- Document Processing
title: Erstelle durchsuchbare PDF mit OCR – Vollständiger Leitfaden
url: /de/java/ocr-operations/create-searchable-pdf-with-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Durchsuchbare PDF mit OCR erstellen – Vollständige Anleitung

Haben Sie schon einmal **durchsuchbare PDFs** aus einem Stapel gescannter Bilder erstellen müssen, waren sich aber nicht sicher, welche Einstellungen Sie ändern sollten? Sie sind nicht allein – die meisten Entwickler stoßen auf dasselbe Problem, wenn das Ergebnis ein riesiger, unlesbarer Blob wird.  

In diesem Tutorial führen wir Sie Schritt für Schritt durch ein sauberes End‑zu‑End‑Beispiel, das genau zeigt, wie Sie **durchsuchbare PDFs** mit einer Java‑OCR‑Engine erstellen, **gescannte Bild‑PDFs konvertieren** und – entscheidend – **die Kompression deaktivieren**, sodass die resultierende Datei den Originalmaßen treu bleibt. Am Ende haben Sie einen sofort einsatzbereiten Code‑Snippet und ein fundiertes Verständnis dafür, warum jede Konfiguration wichtig ist.

## Was Sie lernen werden

* Wie Sie die OCR‑Engine konfigurieren, um **ocr zu durchsuchbarem PDF** zu erzeugen.  
* Der Grund, warum die PDF‑Kompression ausgeschaltet werden sollte und wie Sie ein **PDF ohne Kompression** erhalten.  
* Ein vollständiges Java‑Programm, das ein gescanntes Bild einliest, OCR ausführt und ein **durchsuchbares PDF** speichert.  
* Tipps zum Umgang mit Sonderfällen wie Mehrseitenscans oder Quellen mit niedriger Auflösung.  

**Voraussetzungen** – Java 8+ installiert, ein kompatibles OCR‑SDK (der Code verwendet die ABBYY FineReader Engine API, die Konzepte gelten jedoch für jede Bibliothek, die `setOutputFormat` und `setPdfCompression` anbietet). Eine IDE wie IntelliJ IDEA oder Eclipse erleichtert die Arbeit, aber ein einfacher Texteditor reicht ebenfalls.

---

![Workflow zur Erstellung durchsuchbarer PDFs](image-placeholder.png "Diagramm, das den Prozess zur Erstellung durchsuchbarer PDFs von gescannten Bildern bis zum finalen PDF zeigt")

## Schritt 1: OCR‑Engine auf **Durchsuchbares PDF erstellen** einstellen

Das Erste, was Sie der OCR‑Engine mitteilen müssen, ist, welche Art von Ausgabe Sie erwarten. Viele SDKs geben standardmäßig Klartext oder ein Raster‑PDF aus, das nicht durchsuchbar ist. Das Ändern des Formats übernimmt die schwere Arbeit für Sie.

```java
// Step 1: Tell the engine we want a searchable PDF
engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

*Warum das wichtig ist*: Das Flag `PDF_SEARCHABLE` weist die Engine an, eine unsichtbare Textebene unter dem gescannten Bild einzubetten. Suchwerkzeuge können dann das Dokument indexieren, sodass es sich wie jedes native PDF in Adobe Reader verhält.

## Schritt 2: Kompression deaktivieren – **Kompression richtig deaktivieren**

Wenn Sie diesen Schritt überspringen, komprimiert die Engine jede Seite, um Speicher zu sparen, aber die Kompression kann feine Details verwischen – besonders problematisch, wenn Sie später hochauflösende Bilder extrahieren müssen.

```java
// Step 2: Turn off PDF compression to keep original image quality
engine.getConfig().setPdfCompression(PdfCompression.NONE);
```

**Pro‑Tipp**: Das Deaktivieren der Kompression ist essenziell, wenn Sie rechtliche Dokumente oder medizinische Scans archivieren, bei denen jedes Pixel zählt. Die resultierende Datei ist möglicherweise größer, aber Sie bewahren die Originalabmessungen und Klarheit.

## Schritt 3: OCR ausführen und das resultierende Dokument erhalten

Jetzt, wo die Engine weiß, was sie ausgeben soll und wie die Bilder behandelt werden, können Sie die Erkennung starten. Der Aufruf liefert ein `PdfDocument`‑Objekt, das bereit ist, gespeichert oder weiter verarbeitet zu werden.

```java
// Step 3: Run OCR and capture the searchable PDF in memory
PdfDocument pdf = engine.recognizeToPdf();
```

*Was passiert im Hintergrund?* Die Engine verarbeitet jede Eingangsseite, führt die Zeichenerkennung durch und fügt die versteckte Textebene dem Bild hinzu. Bei mehreren Seiten werden diese automatisch zusammengefügt.

## Schritt 4: **Durchsuchbares PDF** auf die Festplatte speichern

Zum Schluss schreiben Sie das im Speicher befindliche PDF in eine Datei. Wählen Sie einen Ort, für den Sie Schreibrechte besitzen, und geben Sie der Datei einen aussagekräftigen Namen.

```java
// Step 4: Persist the searchable PDF on disk
pdf.save("YOUR_DIRECTORY/searchable.pdf");
```

Wenn Sie `searchable.pdf` in einem Viewer öffnen, werden Sie feststellen, dass Sie den Text auswählen und durchsuchen können – obwohl der sichtbare Inhalt weiterhin das ursprüngliche gescannte Bild ist.

### Vollständiges funktionierendes Beispiel

Unten finden Sie eine eigenständige Java‑Klasse, die alle vier Schritte kombiniert. Kopieren Sie den Code, passen Sie den Eingabepfad an und führen Sie ihn unverändert aus.

```java
import com.abbyy.ocrsdk.Engine;
import com.abbyy.ocrsdk.OcrOutputFormat;
import com.abbyy.ocrsdk.PdfCompression;
import com.abbyy.ocrsdk.PdfDocument;

/**
 * Demonstrates how to create searchable PDF from scanned images.
 * This example uses the ABBYY FineReader Engine Java API.
 */
public class SearchablePdfCreator {

    public static void main(String[] args) {
        // ---- 1. Initialize the OCR engine -------------------------------------------------
        Engine engine = new Engine();
        // (Assume license activation and engine initialization are handled elsewhere)

        // ---- 2. Configure output to be a searchable PDF ----------------------------------
        engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);

        // ---- 3. Disable compression for a PDF without compression -------------------------
        engine.getConfig().setPdfCompression(PdfCompression.NONE);

        // ---- 4. Load the scanned image(s) --------------------------------------------------
        // For simplicity, we let the engine auto‑detect images in the working folder.
        // You could also call engine.addImage("path/to/image.tif") for explicit control.
        engine.addImage("YOUR_DIRECTORY/scanned-page.tif");

        // ---- 5. Perform OCR and retrieve the PDF -----------------------------------------
        PdfDocument pdf = engine.recognizeToPdf();

        // ---- 6. Save the result -----------------------------------------------------------
        pdf.save("YOUR_DIRECTORY/searchable.pdf");

        System.out.println("✅ Searchable PDF created successfully at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**Erwartete Ausgabe** – Nach dem Ausführen des Programms sehen Sie die Konsolennachricht oben, und die Datei `searchable.pdf` erscheint in `YOUR_DIRECTORY`. Beim Öffnen in einem beliebigen PDF‑Reader können Sie:

* Text markieren.  
* Die integrierte Suche (Strg + F) nutzen, um Wörter zu finden.  
* Bei Bedarf die versteckte Textebene exportieren.

---

## Warum Kompression deaktivieren? Verständnis von **PDF ohne Kompression**

Sie fragen sich vielleicht: „Ist Kompression nicht immer sinnvoll?“ Die Antwort ist differenziert:

| Situation | Kompression beibehalten (`NORMAL`) | Kompression deaktivieren (`NONE`) |
|-----------|------------------------------------|-----------------------------------|
| Archivierung von Rechtsverträgen | ❌ Kann Pixel‑Treue verändern | ✅ Garantiert das Original‑Aussehen |
| Große Menge niedriger Auflösung‑Scans | ✅ Spart Speicher | ❌ Erhöht die Größe ohne Nutzen |
| OCR‑Genauigkeit bei winzigen Schriften | ❌ Verwischt feine Details | ✅ Bewahrt jeden Strich |

Kurz gesagt, **wie man Kompression deaktiviert** ist ein Kompromiss zwischen Speicherbedarf und Bildtreue. Für die meisten Workflows, bei denen Sie den Text durchsuchen statt die Bilder neu zu drucken, ist das Ausschalten der Kompression die sicherste Wahl.

## **Gescanntes Bild‑PDF** direkt konvertieren

Manchmal besitzen Sie bereits ein PDF, das gescannte Bilder enthält (ein „reines Bild‑PDF“). Um **gescanntes Bild‑PDF** in eine durchsuchbare Version zu **konvertieren**, können Sie das gesamte PDF an die Engine übergeben, anstatt einzelne Bilder zu verwenden:

```java
engine.addPdf("YOUR_DIRECTORY/scanned-image-only.pdf");
PdfDocument searchable = engine.recognizeToPdf();
searchable.save("YOUR_DIRECTORY/searchable-from-pdf.pdf");
```

Die gleichen Konfigurations‑Flags (`PDF_SEARCHABLE` und `PdfCompression.NONE`) gelten, sodass Sie ein **PDF ohne Kompression** erhalten, selbst wenn Sie von einem PDF‑Container ausgehen.

## Häufige Stolperfallen & wie man sie vermeidet

* **Ausgabeformat nicht gesetzt** – Die Engine verwendet standardmäßig Raster‑PDF, das nicht durchsuchbar ist. Rufen Sie immer `setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE)` vor `recognizeToPdf()` auf.  
* **Speicherengpässe bei großen Stapeln** – Laden und verarbeiten Sie Seiten in Batches oder nutzen Sie die Streaming‑API, falls Ihr SDK diese bereitstellt.  
* **Falsche Dateipfade** – Verwenden Sie absolute Pfade oder stellen Sie sicher, dass das Arbeitsverzeichnis korrekt gesetzt ist; sonst wirft `pdf.save()` eine `IOException`.  
* **Lizenz nicht aktiviert** – Die meisten kommerziellen OCR‑SDKs benötigen eine gültige Lizenz; die Engine wirft eine Laufzeit‑Exception, wenn sie fehlt.

---

## Fazit

Sie haben nun eine komplette, sofort einsatzbereite Lösung, die zeigt, **wie man durchsuchbare PDFs** aus gescannten Bildern erstellt, **wie man gescannte Bild‑PDFs konvertiert** und exakt **wie man Kompression deaktiviert**, um ein **PDF ohne Kompression** zu erzeugen. Die wichtigsten Schritte sind:

1. Ausgabeformat auf `PDF_SEARCHABLE` setzen.  
2. PDF‑Kompression mit `PdfCompression.NONE` ausschalten.  
3. OCR ausführen und das `PdfDocument` erfassen.  
4. Datei auf die Festplatte speichern.

Ab hier können Sie mit Schriftarten experimentieren, Wasserzeichen hinzufügen oder ganze Ordner stapelweise verarbeiten. Wenn Sie mehr über das Hinzufügen von OCR‑Sprachpaketen, den Umgang mit mehrseitigen TIFFs oder die Integration dieses Workflows in einen Web‑Service erfahren möchten, schauen Sie sich unsere kommenden Tutorials zu „OCR‑Sprachauswahl in Java“ und „Streaming‑OCR für große Dokumentensätze“ an.

Fragen oder ein gefundenes Problem? Hinterlassen Sie einen Kommentar unten – happy coding, und viel Spaß mit Ihren neu durchsuchbaren PDFs!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [PDF‑Text erkennen – OCR‑Operationen mit Aspose.OCR für Java](/ocr/english/java/ocr-operations/)
- [OCR‑Erkennung von PDF‑Dokumenten in Aspose.OCR für Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Bilder zu PDF konvertieren C# – Mehrseitiges OCR‑Ergebnis speichern](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}