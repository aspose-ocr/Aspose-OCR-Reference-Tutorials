---
category: general
date: 2026-04-29
description: Erfahren Sie, wie Sie TIFF-Dateien mit dem Aspose OCR‑Streaming‑Modus
  OCRen. Dieser Leitfaden zeigt Ihnen, wie Sie Textkacheln aus geteilten TIFF‑Bildern
  effizient extrahieren.
draft: false
keywords:
- how to ocr tiff
- extract text tiles
language: de
og_description: wie man TIFF mit Aspose OCR Streaming OCRt. Schritt‑für‑Schritt‑Code
  zum Extrahieren von Textkacheln aus großen TIFF‑Bildern.
og_title: Wie man TIFF OCR – Vollständiger Streaming-Leitfaden
tags:
- OCR
- Java
- Aspose
- TIFF
title: Wie man TIFFs OCRt – Große TIFFs streamen und Textkacheln in Java extrahieren
url: /de/java/advanced-ocr-techniques/how-to-ocr-tiff-stream-large-tiffs-and-extract-text-tiles-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# wie man tiff OCR macht – Große TIFFs streamen und Textkacheln extrahieren in Java

Haben Sie sich jemals gefragt, **how to ocr tiff** Dateien, die zu groß sind, um sie auf einmal in den Speicher zu laden? Sie sind nicht der Einzige. Viele Entwickler stoßen an ihre Grenzen, wenn ihre TIFF‑Bilder in Dutzende von Kacheln aufgeteilt sind und der übliche Aufruf `ocrEngine.recognize()` einfach scheitert.  

Die gute Nachricht? Der Streaming‑Modus von Aspose OCR ermöglicht es Ihnen, jede Kachel als separaten Stream zu übergeben, sodass Sie **extract text tiles** ohne Speicherüberlauf ausführen können. In diesem Tutorial führen wir Sie durch ein komplettes, sofort ausführbares Java‑Beispiel, erklären, warum jede Zeile wichtig ist, und weisen auf Fallstricke hin, die Sie vermeiden sollten.

> **What you’ll get:** ein ausführbares Programm, das geteilte TIFFs zur Laufzeit zusammenfügt, den kombinierten Text ausgibt und Ihnen zeigt, wie Sie den Code für andere Sprachen oder Bildformate anpassen können.

---

## Voraussetzungen

- **Java 17** oder neuer (der Code verwendet try‑with‑resources, sodass JDK 8+ funktioniert, aber JDK 17 das aktuelle LTS ist).
- **Aspose.OCR for Java** Bibliothek (v23.10 oder später). Hinzufügen über Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- Ein Ordner, der die einzelnen TIFF‑Kacheln enthält (z. B. `tile_0.tif`, `tile_1.tif`, …).  
- Optional: eine IDE wie IntelliJ IDEA oder VS Code – aber ein einfacher Texteditor reicht aus.

---

## Schritt 1 – Tile‑Pfade vorbereiten (Warum das wichtig ist)

Bevor die OCR‑Engine etwas tun kann, muss sie wissen, wo jedes Bildstück liegt. Das Hard‑Coden der Pfade ist für eine Demo in Ordnung, aber in der Produktion würden Sie wahrscheinlich ein Verzeichnis scannen oder eine Manifest‑Datei lesen.

```java
// Define the absolute or relative paths to each TIFF tile
String[] tilePaths = {
    "YOUR_DIRECTORY/tile_0.tif",
    "YOUR_DIRECTORY/tile_1.tif",
    "YOUR_DIRECTORY/tile_2.tif"
};
```

> **Pro tip:** Halten Sie die Kacheln in lexikalischer Reihenfolge (0, 1, 2…) weil die Engine den erkannten Text in derselben Reihenfolge zusammenfügt, in der Sie die Streams übergeben.

---

## Schritt 2 – Streaming‑Modus in der OCR‑Engine aktivieren (Primäres Schlüsselwort)

Jetzt erstellen wir die `OcrEngine`‑Instanz und schalten das Streaming ein. Das ist der Kern von **how to ocr tiff**, ohne das gesamte Bild in den RAM zu laden.

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Activate streaming – essential for large or tiled TIFFs
ocrEngine.getProcessingSettings().setEnableStreaming(true);

// Set the language to English; change as needed (e.g., "fr", "de")
ocrEngine.getLanguageSettings().setLanguage("en");
```

**Why streaming?**  
Wenn `setEnableStreaming(true)` aufgerufen wird, behandelt die Engine jeden eingehenden `ImageStream` als Fortsetzung des vorherigen. Sie erstellt eine interne virtuelle Leinwand, fügt die Kacheln virtuell zusammen und führt OCR einmal am Ende aus. Das verhindert den „OutOfMemoryError“, der auftreten würde, wenn Sie versuchen, ein mehrgigabytegroßes TIFF auf einmal zu laden.

---

## Schritt 3 – Jede Kachel als Input‑Stream anhängen (Sekundäres Schlüsselwort)

Hier ist die Schleife, die jede Kachel an die Engine übergibt. Der `try‑with‑resources`‑Block stellt sicher, dass das Dateihandle sofort geschlossen wird, was entscheidend ist, wenn Sie mit Dutzenden von Dateien arbeiten.

```java
for (String tilePath : tilePaths) {
    try (InputStream stream = new FileInputStream(tilePath)) {
        // Wrap the raw InputStream in Aspose's ImageStream wrapper
        ocrEngine.appendImage(ImageStream.fromStream(stream));
    } catch (IOException e) {
        // If a single tile fails, we log and continue – you might want to abort instead
        System.err.println("Failed to load tile: " + tilePath);
        e.printStackTrace();
    }
}
```

Beachten Sie, dass die Phrase **extract text tiles** natürlich eingebettet ist: Jede Iteration *extrahiert* den Text aus einer Kachel und fügt ihn dem wachsenden Ergebnis‑Set hinzu.

---

## Schritt 4 – Erkennung ausführen und kombinierten Text ausgeben (Primäres Schlüsselwort)

Nachdem alle Kacheln in die Warteschlange gestellt wurden, führt ein einziger Aufruf OCR auf dem virtuellen Bild aus. Das Ergebnis enthält den vollständigen Text, als hätten Sie ein einzelnes riesiges TIFF.

```java
// Perform OCR on the combined virtual image
OcrResult ocrResult = ocrEngine.recognize();

// Print the extracted text to the console
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Expected output** (angenommen, die Kacheln enthalten den Ausdruck „Hello World“, aufgeteilt über sie):

```
=== OCR Output ===
Hello World
```

Wenn Ihre Kacheln mehr Zeilen enthalten, erscheinen sie in derselben Reihenfolge, in der Sie sie bereitgestellt haben. Sie können `ocrResult.getText()` auch in eine Datei schreiben, um die weitere Verarbeitung zu ermöglichen.

---

## Schritt 5 – Vollständiges, ausführbares Beispiel (Alle Schritte an einem Ort)

Unten finden Sie das vollständige Programm, das Sie in `StreamingExample.java` kopieren und einfügen können. Es enthält alle Importe, Kommentare und Fehlerbehandlung.

```java
import com.aspose.ocr.*;
import java.io.*;

public class StreamingExample {
    public static void main(String[] args) throws Exception {
        // ------------------------------------------------------------
        // Step 1: List the TIFF tile files
        // ------------------------------------------------------------
        String[] tilePaths = {
            "YOUR_DIRECTORY/tile_0.tif",
            "YOUR_DIRECTORY/tile_1.tif",
            "YOUR_DIRECTORY/tile_2.tif"
        };

        // ------------------------------------------------------------
        // Step 2: Set up the OCR engine in streaming mode
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getProcessingSettings().setEnableStreaming(true);
        ocrEngine.getLanguageSettings().setLanguage("en");

        // ------------------------------------------------------------
        // Step 3: Feed each tile as a separate stream
        // ------------------------------------------------------------
        for (String tilePath : tilePaths) {
            try (InputStream stream = new FileInputStream(tilePath)) {
                ocrEngine.appendImage(ImageStream.fromStream(stream));
            } catch (IOException e) {
                System.err.println("Unable to read tile: " + tilePath);
                e.printStackTrace();
                // Optionally: return; // abort on missing tile
            }
        }

        // ------------------------------------------------------------
        // Step 4: Recognize the combined image and display the text
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Speichern, kompilieren und ausführen:

```bash
javac -cp "path/to/aspose-ocr.jar" StreamingExample.java
java -cp ".:path/to/aspose-ocr.jar" StreamingExample
```

Sie sollten den zusammengefügten OCR‑Text in der Konsole ausgegeben sehen.

---

## Erweiterte Tipps & häufige Fallstricke (Warum das funktioniert)

| Problem | Warum es passiert | Wie zu beheben / optimieren |
|---------|-------------------|-----------------------------|
| **Out‑of‑memory errors** | Das Laden eines TIFF in voller Größe in ein `BufferedImage` verbraucht den gesamten Heap. | Verwenden Sie den Streaming‑Modus (`setEnableStreaming(true)`) – die Engine materialisiert das gesamte Bild nie. |
| **Tile order mismatch** | Dateien werden alphabetisch statt numerisch sortiert (z. B. `tile_10.tif` vor `tile_2.tif`). | Null‑auffüllen der Zahlen (`tile_00.tif`, `tile_01.tif`) oder programmatisch mit `Comparator` sortieren. |
| **Wrong language** | OCR verwendet standardmäßig Englisch; nicht‑englischer Text wird unleserlich. | Rufen Sie `ocrEngine.getLanguageSettings().setLanguage("fr")` auf (oder einen anderen unterstützten ISO‑Code). |
| **Partial failures** | Eine beschädigte Kachel stoppt den gesamten Prozess. | Fangen Sie `IOException` pro Kachel ab, protokollieren Sie und entscheiden Sie, ob Sie fortfahren oder abbrechen. |
| **Performance bottleneck** | Disk‑I/O dominiert beim Lesen vieler kleiner Dateien. | Packen Sie Kacheln in ein ZIP und streamen Sie aus dem Speicher, oder verwenden Sie eine schnelle SSD. |

---

## Wann Streaming vs. Einzel‑Bild OCR verwenden

- **Streaming** ist ideal für:
  - Mehrseitige TIFFs oder Gigapixel‑Scans.
  - Situationen, in denen der Speicher begrenzt ist (z. B. Docker‑Container, mobile Geräte).
  - Pipelines, die bereits Bildabschnitte erhalten (z. B. Kamerafeeds).

- **Single‑image OCR** funktioniert gut für:
  - Kleine PNG/JPEG‑Dateien (< 5 MB).
  - Einmalige Scans, bei denen Einfachheit die Leistung überwiegt.

---

## Fazit

Sie haben nun ein solides Verständnis davon, **how to ocr tiff** Dateien mit den Streaming‑Funktionen von Aspose OCR zu verarbeiten, und wissen, wie man **extract text tiles** effizient extrahiert. Die komplette Lösung – die Engine initialisieren, Streaming aktivieren, jede Kachel anhängen und schließlich die virtuelle Leinwand erkennen – deckt das „Was“, „Warum“ und „Wie“ ab, das Sie für produktionsreiferen Code benötigen.

Nächste Schritte? Tauschen Sie `"en"` gegen eine andere Sprache aus oder experimentieren Sie mit verschiedenen Bildformaten (`.png`, `.jpg`). Sie könnten das OCR‑Ergebnis auch direkt in einen Suchindex oder einen PDF‑Generator einspeisen. Das Muster bleibt gleich: streamen, zusammenfügen, erkennen.

Haben Sie Fragen zur Skalierung auf Hunderte von Kacheln oder benötigen Sie Hilfe bei der Fehlerbehandlung? Hinterlassen Sie unten einen Kommentar, und viel Spaß beim Programmieren!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}