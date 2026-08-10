---
category: general
date: 2026-02-17
description: Wie man OCR in Java verwendet, um Text aus PDFs zu extrahieren, PDFs
  in Bilder zu konvertieren und OCR auf gescannten PDF‑Dateien mit Aspose.OCR durchführt.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- convert pdf to images
- perform OCR on pdf
- recognize scanned pdf
language: de
og_description: Wie man OCR in Java nutzt, um Text aus PDF-Dateien zu extrahieren.
  Lernen Sie, PDFs in Bilder zu konvertieren und gescannte PDFs mit Aspose.OCR zu
  erkennen.
og_title: Wie man OCR in Java verwendet – Vollständiger Leitfaden
tags:
- OCR
- Java
- Aspose
title: Wie man OCR in Java verwendet – Text aus PDF mit Aspose.OCR extrahieren
url: /de/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in Java verwendet – Text aus PDF mit Aspose.OCR extrahieren

Haben Sie sich jemals gefragt **wie man OCR** verwendet, um ein gescanntes PDF in durchsuchbaren Text zu verwandeln? Sie sind nicht allein. Die meisten Entwickler stoßen an eine Grenze, wenn ein PDF als eine Reihe von Bildern ankommt und die üblichen Text‑Extraktoren einfach nichts zurückgeben. Die gute Nachricht? Mit ein paar Zeilen Java und Aspose.OCR können Sie **Text aus PDF extrahieren**, **PDF in Bilder konvertieren** und **gescannte PDFs erkennen** in einem einzigen, mühelosen Workflow.

In diesem Tutorial führen wir Sie durch alles, was Sie wissen müssen – von der Lizenzierung der Bibliothek bis zum Ausgeben des Endergebnisses. Am Ende haben Sie ein einsatzbereites Programm, das Klartext aus jedem gescannten Bericht, jeder Rechnung oder jedem E‑Book extrahiert. Keine externen Dienste, keine Magie – nur reiner Java‑Code, den Sie kontrollieren.

## Was Sie benötigen

- **Java Development Kit (JDK) 8+** – jede aktuelle Version funktioniert.
- **Aspose.OCR for Java** JAR (von der Aspose-Website herunterladen).  
- Eine **gültige Aspose.OCR-Lizenzdatei** (`Aspose.OCR.lic`). Die kostenlose Testversion funktioniert, aber eine Lizenz schaltet die volle Genauigkeit frei.
- Ein **Beispiel‑gescanntes PDF** (z. B. `scanned-report.pdf`).  
- Eine IDE oder ein einfacher Texteditor plus ein Terminal.

Das war’s. Kein Maven, kein Gradle, keine zusätzlichen Abhängigkeiten – nur das Aspose.OCR‑JAR im Klassenpfad.

![Beispiel zur Verwendung von OCR](image-placeholder.png "Beispiel zur Verwendung von OCR")

## Schritt 1 – Laden Sie Ihre Aspose.OCR‑Lizenz (Warum das wichtig ist)

Bevor die Engine mit voller Geschwindigkeit laufen kann, müssen Sie ihr mitteilen, wo Ihre Lizenz liegt. Das Überspringen dieses Schrittes versetzt die Bibliothek in den Evaluierungsmodus, der Wasserzeichen zum Ergebnis hinzufügt und die Genauigkeit einschränken kann.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – required for unrestricted OCR
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**Warum das funktioniert:** Die Klasse `License` liest die `.lic`‑Datei und registriert sie global. Sobald sie gesetzt ist, verwendet jede von Ihnen erstellte `OcrEngine` automatisch die lizenzierten Funktionen.

## Schritt 2 – Erstellen Sie die OCR‑Engine (Die Engine hinter der Magie)

Eine `OcrEngine`‑Instanz ist das Arbeitspferd, das Bilder scannt und Text ausgibt. Denken Sie an sie als das Gehirn, das Pixelmuster interpretiert.

```java
        // Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Profi‑Tipp:** Sie können Sprache, Konfidenz‑Schwellenwerte anpassen oder sogar GPU‑Beschleunigung über die Eigenschaften der Engine aktivieren. Für die meisten englischen PDFs sind die Vorgaben ausreichend.

## Schritt 3 – Eingabe vorbereiten: PDF hinzufügen (PDF intern in Bilder konvertieren)

Aspose.OCR behandelt jede Seite eines PDFs als Bild. Wenn Sie `addPdf` aufrufen, rastert die Bibliothek jede Seite stillschweigend, was genau das ist, was Sie benötigen, um **PDF in Bilder zu konvertieren** bevor die Erkennung erfolgt.

```java
        // Prepare OCR input – each PDF page becomes an image internally
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");
```

**Was passiert:**  
- Das PDF wird geöffnet.  
- Jede Seite wird mit 300 dpi (Standard) gerendert, um Detailgenauigkeit der Zeichen zu erhalten.  
- Die gerenderten Bitmap‑Objekte werden in der `OcrInput`‑Sammlung gespeichert.

Falls Sie jemals die Rohbilder benötigen (zum Debuggen oder für benutzerdefinierte Vorverarbeitung), rufen Sie nach diesem Schritt `ocrInput.getPages()` auf.

## Schritt 4 – OCR‑Prozess ausführen (OCR auf PDF anwenden)

Jetzt beginnt die schwere Arbeit. Die Methode `recognize` durchläuft jedes Bild, führt den Erkennungsalgorithmus aus und fasst die Ergebnisse in einem `OcrResult` zusammen.

```java
        // Run OCR on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Warum das wichtig ist:** Das `OcrResult` enthält nicht nur Klartext, sondern auch Konfidenzwerte, Begrenzungsrahmen und die Referenz zum Originalbild. Für die meisten Anwendungsfälle benötigen Sie nur `getText()`.

## Schritt 5 – Extrahierten Text abrufen und anzeigen

Zum Schluss holen Sie die Klartext‑Zeichenkette aus dem Ergebnis und geben sie aus. Sie können sie auch in eine Datei schreiben, an einen Suchindex übergeben oder in eine nachgelagerte NLP‑Pipeline einspeisen.

```java
        // Output the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

### Erwartete Ausgabe

Wenn `scanned-report.pdf` einen einfachen Absatz enthält, sehen Sie etwa Folgendes:

```
Extracted text:
Quarterly Sales Report
Region: North America
Total Revenue: $4,527,000
...
```

Die genaue Formatierung spiegelt das ursprüngliche Layout wider und bewahrt Zeilenumbrüche, wo möglich.

## Umgang mit häufigen Sonderfällen

### 1. Mehrsprachige PDFs

Wenn Ihr Dokument französischen oder spanischen Text enthält, setzen Sie die Sprache, bevor Sie `recognize` aufrufen:

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);
```

Sie können ein Array von Sprachen übergeben, damit die Engine automatisch erkennt.

### 2. Scans mit niedriger Auflösung

Bei Scans mit 150 dpi sollten Sie die interne Rendering‑DPI erhöhen:

```java
ocrInput.addPdf("low-res.pdf", 600); // render at 600 dpi for better accuracy
```

Eine höhere DPI verbessert die Zeichenklarheit, verbraucht jedoch mehr Speicher.

### 3. Große PDFs (Speichermanagement)

Für PDFs mit Dutzenden von Seiten verarbeiten Sie sie in Batches:

```java
int batchSize = 10;
for (int i = 0; i < ocrInput.getPages().size(); i += batchSize) {
    List<OcrPage> batch = ocrInput.getPages().subList(i, Math.min(i + batchSize, ocrInput.getPages().size()));
    OcrInput batchInput = new OcrInput();
    batchInput.getPages().addAll(batch);
    OcrResult batchResult = ocrEngine.recognize(batchInput);
    // Append batchResult.getText() to your final output
}
```

Dieser Ansatz verhindert, dass der JVM‑Heap zu stark anwächst.

## Vollständiges, sofort ausführbares Beispiel

Unten finden Sie das komplette Programm – einschließlich Imports und Lizenzverwaltung – sodass Sie es sofort kopieren und ausführen können.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (required for full functionality)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Step 2: Create an OCR engine instance that will perform the recognition
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Prepare the OCR input by adding the PDF file.
        // Each page of the PDF is internally converted to an image.
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");

        // Step 4: Run the OCR process on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

Führen Sie es aus mit:

```bash
javac -cp "path/to/aspose-ocr.jar" PdfOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" PdfOcrDemo
```

Sie sollten den extrahierten Text in der Konsole ausgegeben sehen.

## Zusammenfassung – Was wir behandelt haben

- **Wie man OCR** in Java mit Aspose.OCR verwendet.  
- Den Workflow zum **Extrahieren von Text aus PDF**‑Dateien.  
- Intern konvertiert die Bibliothek **PDF in Bilder**, bevor Zeichen erkannt werden.  
- Tipps zum **Durchführen von OCR auf PDF** mit mehreren Sprachen, Scans niedriger Auflösung und großen Dokumenten.  
- Ein vollständiges, ausführbares Code‑Beispiel, das Sie in jedes Java‑Projekt einbinden können.

## Nächste Schritte & verwandte Themen

Jetzt, da Sie **gescannte PDFs erkennen** können, denken Sie an diese weiterführenden Ideen:

- **Erstellung durchsuchbarer PDFs** – den OCR‑Text wieder über das Original‑PDF legen, um ein durchsuchbares Dokument zu erzeugen.  
- **Batch‑Verarbeitungs‑Service** – den Code in einen Spring‑Boot‑Microservice einbetten, der PDFs per REST entgegennimmt.  
- **Integration mit Elasticsearch** – den extrahierten Text indexieren für schnelle Volltextsuche in Ihrem Dokumenten‑Repository.  
- **Bild‑Vorverarbeitung** – OpenCV verwenden, um Seiten zu entzerren oder zu entrauschen, bevor OCR angewendet wird, für noch höhere Genauigkeit.

Jedes dieser Themen baut auf den Kernkonzepten auf, die wir behandelt haben, also experimentieren Sie gern und lassen Sie die OCR‑Engine die schwere Arbeit erledigen.

---

*Viel Spaß beim Coden! Wenn Sie auf Probleme stoßen – etwa Lizenzfehler oder unerwartete Null‑Ergebnisse – hinterlassen Sie unten einen Kommentar. Ich helfe gern bei einer Debug‑Sitzung.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}