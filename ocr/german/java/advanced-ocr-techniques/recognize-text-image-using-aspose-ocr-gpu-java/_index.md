---
category: general
date: 2026-02-17
description: Erkennen Sie Textbilder schnell mit Aspose OCR GPU‑Unterstützung in Java.
  Lernen Sie, Text aus Bildern zu extrahieren und die GPU‑Geräte‑ID für optimale Leistung
  festzulegen.
draft: false
keywords:
- recognize text image
- extract text from image
- set gpu device id
- Aspose OCR Java
- GPU acceleration OCR
language: de
og_description: Erkennen Sie Textbilder schnell mit Aspose OCR GPU‑Unterstützung in
  Java. Dieser Leitfaden zeigt, wie man Text aus einem Bild extrahiert und die GPU‑Geräte‑ID
  festlegt.
og_title: Texterkennung im Bild mit Aspose OCR GPU – Java
tags:
- Java
- OCR
- Aspose
- GPU
title: Text aus Bild mit Aspose OCR GPU – Java erkennen
url: /de/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text in Bildern erkennen mit Aspose OCR GPU – Java

Haben Sie jemals **Text in Bildern erkennen** in einer Java‑Anwendung benötigt, aber die CPU kam bei großen Dateien nicht mehr hinterher? Sie sind nicht der Einzige – viele Entwickler stoßen an diese Grenze, wenn sie hochauflösende Scans verarbeiten. Die gute Nachricht? Aspose OCR ermöglicht es Ihnen, **Text aus Bild zu extrahieren** auf der GPU, wodurch die Verarbeitungszeit drastisch verkürzt wird.  

In diesem Tutorial führen wir Sie durch ein komplettes, sofort ausführbares Beispiel, das genau zeigt, wie Sie die Lizenz einrichten, die GPU‑Beschleunigung aktivieren und **set gpu device id** festlegen, wenn Sie mehrere Grafikkarten besitzen. Am Ende haben Sie ein eigenständiges Programm, das den erkannten Text in der Konsole ausgibt – ohne weitere Schritte.

## Was Sie benötigen

- **Java 17** oder neuer (die API ist kompatibel mit Java 8+, aber das neueste LTS bietet bessere Leistung).  
- **Aspose OCR for Java** Bibliothek (laden Sie das JAR von der Aspose‑Website herunter).  
- Eine gültige **Aspose OCR Lizenzdatei** (`Aspose.OCR.lic`). Die kostenlose Testversion funktioniert, aber GPU‑Funktionen sind hinter einer lizenzierten Version gesperrt.  
- Eine Bilddatei (`sample-image.png`), die klaren, maschinenlesbaren Text enthält.  
- Eine GPU‑fähige Umgebung (eine NVIDIA‑CUDA‑kompatible Karte funktioniert am besten).  

Wenn Ihnen einer dieser Punkte unbekannt ist, keine Sorge – jeder Aufzählungspunkt wird im Verlauf erklärt.

## Schritt 1: Aspose OCR zu Ihrem Projekt hinzufügen

Zuerst fügen Sie das Aspose OCR JAR Ihrem Klassenpfad hinzu. Wenn Sie Maven verwenden, ergänzen Sie die folgende Abhängigkeit in `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Für Gradle lautet sie:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Wenn Sie den manuellen Weg bevorzugen, legen Sie das JAR in Ihren `libs/`‑Ordner und fügen Sie es dem Modulpfad Ihrer IDE hinzu.

> **Pro‑Tipp:** Halten Sie die Versionsnummer synchron mit den Release‑Notes der Bibliothek; neuere Versionen bringen häufig Performance‑Optimierungen für die GPU‑Verarbeitung.

## Schritt 2: Laden Sie die Aspose OCR Lizenz (erforderlich für GPU‑Nutzung)

Ohne Lizenz fällt der Aufruf `setEnableGpu(true)` stillschweigend in den CPU‑Modus zurück. Laden Sie die Lizenz gleich zu Beginn von `main`:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

Ersetzen Sie `YOUR_DIRECTORY` durch den absoluten oder relativen Pfad, in dem Sie die `.lic`‑Datei abgelegt haben. Ist der Pfad falsch, wirft Aspose eine `FileNotFoundException`, prüfen Sie also die Schreibweise genau.

## Schritt 3: Erstellen Sie die OCR‑Engine und aktivieren Sie die GPU‑Beschleunigung

Jetzt instanziieren wir `OcrEngine` und weisen ihr die GPU zu. Die Methode `setGpuDeviceId` ermöglicht es Ihnen, eine bestimmte Karte auszuwählen, wenn mehr als eine vorhanden ist.

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

Warum die Geräte‑ID? In einem Multi‑GPU‑Server können Sie eine Karte für die Bildvorverarbeitung und eine andere für die OCR reservieren. Das Setzen der ID stellt sicher, dass die richtige Hardware die schwere Arbeit übernimmt.

## Schritt 4: Bereiten Sie das Eingabebild vor

Aspose OCR arbeitet mit einer Vielzahl von Formaten (PNG, JPG, BMP, TIFF). Verpacken Sie Ihre Datei in ein `OcrInput`‑Objekt:

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

Falls Sie einen Stream verarbeiten müssen (z. B. eine hochgeladene Datei), verwenden Sie stattdessen `ocrInput.add(InputStream)`.

## Schritt 5: Führen Sie den Erkennungsprozess aus und holen Sie das Ergebnis ab

Die Methode `recognize` liefert ein `OcrResult`, das den Klartext, Konfidenzwerte und sogar Layout‑Informationen enthält, falls Sie diese benötigen.

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

Die Konsole zeigt etwa Folgendes:

```
Recognized text:
Hello, world!
This is a sample image.
```

Ist das Bild unscharf oder wird die Sprache nicht unterstützt, kann das Ergebnis leer sein. Prüfen Sie in diesem Fall den Wert von `ocrResult.getConfidence()` (0‑100), um zu entscheiden, ob Sie mit einer Vorverarbeitung erneut versuchen sollten.

## Vollständiges, ausführbares Beispiel

Alle Bausteine zusammengefügt ergeben eine einzelne Java‑Klasse, die Sie in Ihre IDE kopieren‑und‑einfügen können:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license – required for GPU usage
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // 2️⃣ Create OCR engine and turn on GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getDevice().setEnableGpu(true);      // enable GPU acceleration
        ocrEngine.getDevice().setGpuDeviceId(0);       // optional: select GPU index

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/sample-image.png");

        // 4️⃣ Perform recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + ocrResult.getText());
    }
}
```

> **Erwartete Ausgabe:** Die Konsole gibt den genauen Text aus, der in `sample-image.png` zu sehen ist. Ist die GPU aktiv, werden Sie feststellen, dass die Verarbeitungszeit von mehreren Sekunden (CPU) auf unter eine Sekunde für typische 300 dpi‑Scans sinkt.

## Häufige Fragen & Sonderfälle

### Funktioniert das auf einem headless Server?

Ja. Der GPU‑Treiber muss installiert sein, aber ein Display wird nicht benötigt. Stellen Sie lediglich sicher, dass das `CUDA`‑Toolkit (oder das Äquivalent für Ihre GPU) im System‑`PATH` liegt.

### Was ist, wenn ich mehr als eine GPU habe und GPU 1 verwenden möchte?

Ändern Sie die Geräte‑ID:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

### Wie extrahiere ich Text aus einem Bild in einer anderen Sprache?

Setzen Sie die Sprache, bevor Sie `recognize` aufrufen:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose unterstützt über 30 Sprachen; siehe die API‑Dokumentation für die vollständige Aufzählung.

### Was ist, wenn das Bild mehrere Seiten enthält (z. B. ein PDF, das in Bilder konvertiert wurde)?

Erstellen Sie für jede Seite einen separaten `OcrInput`‑Eintrag oder iterieren Sie über die Dateien:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

Die Engine verkettet die Ergebnisse in der richtigen Reihenfolge.

### Wie gehe ich mit Ergebnissen niedriger Konfidenz um?

Prüfen Sie den Konfidenzwert:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

Typische Vorverarbeitungsschritte umfassen Binärisierung, Rauschreduktion oder das Skalieren auf 300 dpi.

## Leistungstipps

- **Batch‑Verarbeitung:** Das Hinzufügen vieler Bilder zu einem einzigen `OcrInput` reduziert den Overhead, der durch wiederholtes Initialisieren des GPU‑Kontexts entsteht.  
- **Warm‑up:** Führen Sie nach dem Starten der JVM einmal eine Dummy‑Erkennung aus; der erste Aufruf verursacht eine Treiber‑Initialisierungslatenz.  
- **Speicherverwaltung:** Entsorgen Sie große `OcrInput`‑Objekte (`ocrInput.clear()`) nach deren Verwendung, um GPU‑Speicher freizugeben.  

## Fazit

Sie wissen jetzt, wie Sie **Text in Bildern erkennen** effizient mit Aspose OCRs GPU‑Engine in Java, wie Sie **Text aus Bild** in jeder unterstützten Sprache **extrahieren** und wie Sie **set gpu device id** festlegen, wenn Sie mit mehreren Grafikkarten arbeiten. Der komplette, ausführbare Code oben sollte sofort funktionieren – tauschen Sie lediglich Ihre Lizenz‑ und Bildpfade aus.

Bereit für den nächsten Schritt? Versuchen Sie, einen Ordner mit gescannten PDFs zu verarbeiten, experimentieren Sie mit verschiedenen `setLanguage`‑Optionen oder kombinieren Sie OCR mit einem Machine‑Learning‑Modell für die Nachbearbeitung. Die Möglichkeiten sind endlos, und die Leistungsgewinne durch GPU‑Beschleunigung machen selbst groß angelegte Projekte machbar.

Viel Spaß beim Coden, und hinterlassen Sie gern einen Kommentar, falls Sie auf Probleme stoßen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}