---
category: general
date: 2026-06-16
description: Führen Sie OCR auf einem Dokument mit Java in nur wenigen Schritten aus.
  Erfahren Sie, wie Sie OCR konfigurieren, Text aus TIFF erkennen und Text aus mehrseitigen
  Bildern extrahieren.
draft: false
keywords:
- run OCR on document
- how to configure OCR
- recognize text from TIFF
- extract text from multi-page
language: de
og_description: Führen Sie OCR auf Dokumenten mit Java aus. Dieser Leitfaden zeigt,
  wie man OCR konfiguriert, Text aus TIFF‑Dateien erkennt und Text aus mehrseitigen
  Bildern extrahiert.
og_title: OCR auf Dokument in Java ausführen – Schritt‑für‑Schritt‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Run OCR on document using Java in just a few steps. Learn how to configure
    OCR, recognize text from TIFF, and extract text from multi‑page images.
  headline: Run OCR on Document in Java – Complete Guide
  type: TechArticle
- description: Run OCR on document using Java in just a few steps. Learn how to configure
    OCR, recognize text from TIFF, and extract text from multi‑page images.
  name: Run OCR on Document in Java – Complete Guide
  steps:
  - name: '**Streamed processing** – Some OCR SDKs let you feed pages one‑by‑one instead
      of loading the entire TIFF into memory. Look for methods like `engine.setImageStream(...)`
      that accept an `InputStream`.'
    text: '**Streamed processing** – Some OCR SDKs let you feed pages one‑by‑one instead
      of loading the entire TIFF into memory. Look for methods like `engine.setImageStream(...)`
      that accept an `InputStream`.'
  - name: '**Memory limits** – If you hit `OutOfMemoryError`, lower the thread count
      or increase the JVM heap (`-Xmx2g`).'
    text: '**Memory limits** – If you hit `OutOfMemoryError`, lower the thread count
      or increase the JVM heap (`-Xmx2g`).'
  - name: '**Post‑processing** – Use regex or natural‑language libraries to clean
      up line breaks, remove headers/footers, or extract specific fields (e.g., invoice
      numbers).'
    text: '**Post‑processing** – Use regex or natural‑language libraries to clean
      up line breaks, remove headers/footers, or extract specific fields (e.g., invoice
      numbers).'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: OCR auf Dokument in Java ausführen – Komplettanleitung
url: /de/java/ocr-operations/run-ocr-on-document-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf Dokumenten in Java ausführen – Vollständiger Leitfaden

Haben Sie schon einmal **OCR auf Dokumentdateien** ausführen müssen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein. Egal, ob Sie alte Archive digitalisieren oder Daten aus gescannten Formularen extrahieren – zuverlässigen Text aus Bildern zu erhalten, ist ein häufiges Problem.

In diesem Tutorial gehen wir Schritt für Schritt durch ein praktisches End‑to‑End‑Beispiel, das zeigt, **wie man OCR konfiguriert**, **Text aus TIFF erkennt** und **Text aus mehrseitigen** Dokumenten extrahiert – und das alles mit nur wenigen Zeilen Java. Kein Schnickschnack, nur eine funktionierende Lösung, die Sie noch heute in Ihr Projekt übernehmen können.

## Was Sie lernen werden

- Ein OCR‑Engine‑Objekt in Java einrichten  
- Ein mehrseitiges TIFF‑Bild zum Verarbeiten laden  
- Die Engine durch Konfiguration der Thread‑Anzahl optimieren (der Teil „wie man OCR konfiguriert“)  
- Erkennung durchführen und den extrahierten Text ausgeben  
- Sonderfälle wie große Dateien und Speichergrenzen behandeln  

Am Ende dieses Leitfadens können Sie **OCR auf Dokumenten‑Bildern** sicher ausführen und haben eine solide Basis, um die Lösung auf PDFs, PNGs oder sogar Live‑Kamerastreams auszudehnen.

## Voraussetzungen

- Java 17 oder neuer (der Code verwendet das Schlüsselwort `var` zur Kürze)  
- Eine OCR‑Bibliothek, die eine `OcrEngine`‑Klasse bereitstellt (z. B. *Aspose.OCR for Java* oder *Tesseract‑Java* Wrapper).  
- Eine mehrseitige TIFF‑Datei namens `multi_page.tif` in einem bekannten Verzeichnis.  

Fehlt Ihnen die OCR‑Bibliothek, fügen Sie sie Ihrer `pom.xml` (Maven) oder `build.gradle` (Gradle) hinzu – die genauen Koordinaten hängen vom Anbieter ab, meist reicht ein einzelnes JAR, das Sie referenzieren können.

---

## Schritt 1: OCR‑Engine initialisieren – Wie man OCR auf Dokumenten ausführt

Zuerst benötigen Sie ein Engine‑Objekt, das die eigentliche Arbeit übernimmt. Denken Sie daran als das Gehirn hinter dem Vorgang.

```java
import com.example.ocr.OcrEngine;   // Replace with your actual package
import com.example.ocr.ImageStream;
import com.example.ocr.OcrResult;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();
```

> **Warum das wichtig ist:** Die `OcrEngine` kapselt alle Erkennungseinstellungen, Sprachpakete und Optionen zur Hardware‑Nutzung. Sie einmal zu erstellen und für mehrere Bilder wiederzuverwenden, ist effizienter, als sie jedes Mal neu zu instanziieren.

---

## Schritt 2: Mehrseitiges TIFF laden – Text aus mehrseitigen Bildern extrahieren

Jetzt zeigen wir der Engine, welche Datei verarbeitet werden soll. TIFF ist ein gängiges Format für gescannte Dokumente, weil es mehrere Seiten in einer einzigen Datei speichern kann.

```java
        // Step 2: Load the multi‑page image to be processed
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page.tif"));
```

> **Pro‑Tipp:** Wenn Ihr TIFF auf einem Netzwerk‑Share liegt, verwenden Sie `ImageStream.fromUrl(...)` stattdessen. Das verhindert, dass die gesamte Datei vor Beginn der OCR in den Speicher kopiert wird.

---

## Schritt 3: Wie man OCR für maximale Durchsatzrate konfiguriert

Standard‑OCR‑Bibliotheken laufen oft nur in einem einzigen Thread, was auf modernen Mehrkern‑Maschinen zum Engpass werden kann. Hier beantworten wir den Teil des Puzzles „**wie man OCR konfiguriert**“.

```java
        // Step 3: Configure the engine to use all available CPU cores
        int availableCores = Runtime.getRuntime().availableProcessors();
        engine.getRecognitionSettings().setThreadCount(availableCores);
```

> **Warum das funktioniert:** Durch die Anpassung der Thread‑Anzahl an die Zahl der logischen Prozessoren kann die OCR‑Engine verschiedene Seiten parallel verarbeiten. Auf einem 4‑Kern‑Laptop sehen Sie etwa eine 3‑ bis 4‑fache Geschwindigkeitssteigerung bei mehrseitigen Dokumenten.  
> **Sonderfall:** Einige Umgebungen (z. B. Docker‑Container mit begrenzten CPU‑Quoten) melden mehr Kerne, als sie tatsächlich nutzen dürfen. In solchen Fällen begrenzen Sie die Thread‑Anzahl manuell: `engine.getRecognitionSettings().setThreadCount(Math.min(availableCores, 2));`

---

## Schritt 4: Text aus TIFF erkennen – Der zentrale OCR‑Aufruf

Nachdem alles verkabelt ist, können wir die Erkennung starten. Dieser einzelne Aufruf iteriert über jede Seite des TIFF, wendet die Sprachmodelle an und liefert ein zusammengesetztes Ergebnis.

```java
        // Step 4: Perform the OCR recognition
        OcrResult result = engine.recognize();
```

> **Was im Hintergrund passiert:** Die Engine zerlegt das TIFF in einzelne Rasterbilder, übergibt jedes dem OCR‑Neuronalen Netz und fügt die textuellen Ausgaben zusammen. Wenn Sie die Granularität pro Seite benötigen, liefert `result.getPages()` eine Liste von `OcrPageResult`‑Objekten.

---

## Schritt 5: Erkannten Text ausgeben – Extraktion verifizieren

Zum Schluss geben wir den extrahierten Text in der Konsole aus. In einer echten Anwendung würden Sie ihn wahrscheinlich in einer Datenbank oder einer JSON‑Datei speichern.

```java
        // Step 5: Output the recognized text
        System.out.println(result.getText());
    }
}
```

**Erwartete Ausgabe (gekürzt):**

```
Page 1:
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00

Page 2:
Terms and Conditions...
```

Wenn Sie statt sauberer Zeichen Kauderwelsch sehen, prüfen Sie, ob die richtigen Sprachpakete installiert sind und das Bild nicht zu verrauscht ist. Vorverarbeitungsschritte wie Deskewing oder Binarisierung können die Genauigkeit dramatisch erhöhen.

---

## Umgang mit großen mehrseitigen Dateien – Tipps zur Extraktion

Obwohl wir bereits den Grundablauf gezeigt haben, können reale Dokumente riesig sein. Hier ein paar zusätzliche Überlegungen:

1. **Gestreamte Verarbeitung** – Einige OCR‑SDKs erlauben das Einspeisen von Seiten einzeln, anstatt das gesamte TIFF in den Speicher zu laden. Suchen Sie nach Methoden wie `engine.setImageStream(...)`, die einen `InputStream` akzeptieren.  
2. **Speichergrenzen** – Bei einem `OutOfMemoryError` reduzieren Sie die Thread‑Anzahl oder erhöhen den JVM‑Heap (`-Xmx2g`).  
3. **Nachbearbeitung** – Verwenden Sie Regex‑ oder Natural‑Language‑Bibliotheken, um Zeilenumbrüche zu bereinigen, Kopf‑/Fußzeilen zu entfernen oder bestimmte Felder (z. B. Rechnungsnummern) zu extrahieren.

---

## Vollständiges funktionierendes Beispiel (Alle Schritte kombiniert)

Unten finden Sie die komplette, sofort ausführbare Java‑Klasse. Kopieren Sie sie in Ihre IDE, passen Sie das Paket/Importe an und führen Sie sie aus.

```java
package com.example.ocrdemo;

import com.example.ocr.OcrEngine;
import com.example.ocr.ImageStream;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to run OCR on document images, configure the engine,
 * recognize text from TIFF files, and extract text from multi‑page documents.
 */
public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Create the OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Load the multi‑page TIFF image
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page.tif"));

        // Configure the engine to use all CPU cores (how to configure OCR)
        int cores = Runtime.getRuntime().availableProcessors();
        engine.getRecognitionSettings().setThreadCount(cores);

        // Perform recognition (recognize text from TIFF)
        OcrResult result = engine.recognize();

        // Output the extracted text (extract text from multi‑page)
        System.out.println(result.getText());
    }
}
```

> **Pro‑Tipp:** Packen Sie den Aufruf `recognize()` in einen `try‑catch`‑Block, um `OcrException` elegant zu behandeln, besonders wenn beschädigte Bilddateien verarbeitet werden.

---

## Fazit

Wir haben Ihnen gezeigt, wie Sie **OCR auf Dokumenten‑Bildern** mit Java ausführen, von der Engine‑Initialisierung bis zur mehrseitigen Textextraktion. Durch das Verständnis **wie man OCR konfiguriert**, können Sie jede moderne CPU voll ausnutzen, während die Schritte zum **Erkennen von Text aus TIFF** und **Extrahieren von Text aus mehrseitigen** Dateien Ihnen eine solide Basis für jedes Dokument‑Digitalisierungsprojekt geben.

Was kommt als Nächstes? Ersetzen Sie das TIFF durch ein PDF, experimentieren Sie mit benutzerdefinierten Sprachmodellen oder leiten Sie die Ausgabe in einen Suchindex weiter. Sobald Sie dieses Fundament haben, sind Ihrer Kreativität keine Grenzen gesetzt.

Falls Sie auf Probleme stoßen – etwa weil die von Ihnen gewählte OCR‑Bibliothek eine andere API verwendet – hinterlassen Sie einen Kommentar unten. Viel Spaß beim Coden und beim Umwandeln gescannter Seiten in durchsuchbaren Text!

## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to recognize tiff with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}