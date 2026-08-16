---
category: general
date: 2026-03-28
description: Erfahren Sie, wie Sie Bildtext in Java mit Aspose OCR erkennen, Text‑PNG‑Dateien
  extrahieren und GPU‑Beschleunigung für schnelles OCR großer Bilder nutzen.
draft: false
keywords:
- recognize image text
- extract text png
- use gpu acceleration
- ocr large image
- java ocr example
language: de
og_description: Entdecken Sie, wie Sie Bildtext in Java erkennen, Text aus PNG‑Dateien
  extrahieren und GPU‑Beschleunigung für die OCR großer Bilder nutzen.
og_title: Bildtext mit Java OCR erkennen – GPU‑beschleunigtes Beispiel
tags:
- OCR
- Java
- GPU
title: Bildtext mit Java OCR erkennen – GPU‑beschleunigtes Beispiel
url: /de/java/advanced-ocr-techniques/recognize-image-text-with-java-ocr-gpu-accelerated-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bildtext erkennen mit Java OCR – GPU‑beschleunigtes Beispiel

Haben Sie jemals versucht, **Bildtext zu erkennen** aus einer riesigen PNG-Datei, nur um festzustellen, dass die CPU‑Version schleppend arbeitet? Sie sind nicht allein. In vielen realen Pipelines – denken Sie an Rechnungserfassung oder die Archivierung historischer Dokumente – kann die Bildgröße enorm werden, und die Standard‑OCR‑Engine kann einfach nicht mithalten.  

Gute Neuigkeiten: Aspose OCR für Java ermöglicht Ihnen **die Nutzung von GPU‑Beschleunigung**, um den Prozess zu beschleunigen, und der Code ist überraschend kompakt. In diesem Tutorial sehen Sie ein vollständiges, ausführbares Java‑OCR‑Beispiel, das **Text aus PNG‑Dateien extrahiert**, eine CUDA‑fähige GPU nutzt und ein **OCR‑großes Bild** mit nur wenigen Code‑Zeilen verarbeitet. Am Ende wissen Sie genau, wie Sie das in Ihr eigenes Java‑Projekt einbinden und warum jede Einstellung wichtig ist.

## Was Sie lernen werden

- Wie Sie Aspose OCR in einem Maven‑ oder Gradle‑Projekt einrichten.  
- Der Schritt‑für‑Schritt‑Prozess, um **Bildtext zu erkennen** auf der GPU.  
- Warum die Konfiguration der Anzahl von GPU‑Streams die Durchsatzrate erhöhen kann.  
- Wie Sie die Ausgabe überprüfen und häufige Stolpersteine beheben.  

> **Voraussetzungen** – Java 17 (oder neuer), eine CUDA‑kompatible GPU mit aktuellem Treiber und eine gültige Aspose OCR für Java‑Lizenz (die kostenlose Testversion reicht für Evaluierungen). Weitere externe Bibliotheken werden nicht benötigt.

---

## Schritt 1: Aspose OCR‑Abhängigkeit hinzufügen

Zuerst bringen Sie die Aspose OCR‑Bibliothek in Ihr Build‑System. Wenn Sie **Maven** verwenden, fügen Sie den folgenden Ausschnitt zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check Maven Central for the latest version -->
</dependency>
```

Für **Gradle** platzieren Sie dies in `build.gradle`:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro‑Tipp:** Die neueste Version (Stand März 2026) enthält Leistungsverbesserungen für GPU‑Workloads, holen Sie also immer das aktuellste Release.

---

## Schritt 2: OCR‑Engine initialisieren und GPU aktivieren

Eine OCR‑Engine zu erstellen ist unkompliziert. Der entscheidende Teil ist das Einschalten des GPU‑Flags – sonst fällt die Engine auf den CPU‑Modus zurück.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // 3️⃣ (Optional) Set the number of GPU streams for parallel processing
        //    More streams can improve throughput on multi‑core GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);
```

### Warum GPU aktivieren?

Wenn Sie `setUseGpu(true)` aktivieren, verlagert Aspose die schweren Berechnungen des Convolutional‑Neural‑Network auf die Grafikkarte. Das kann Sekunden vom Verarbeitungszeitraum eines **OCR‑großen Bildes** einsparen, besonders wenn das Bild größer als 4000 × 4000 px ist. Fehlt eine kompatible GPU, wird der Aufruf einfach zu einem No‑Op und die Engine arbeitet weiter auf der CPU – kein Absturz, nur langsamere Performance.

---

## Schritt 3: PNG‑Bild erkennen und dessen Text extrahieren

Jetzt zeigen Sie der Engine die Datei, die Sie verarbeiten möchten. Das Beispiel verwendet `sample-large.png`, Sie können es aber durch jede PNG‑ oder JPEG‑Datei ersetzen.

```java
        // 4️⃣ Perform OCR on the input image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // 5️⃣ Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Wenn Sie das Programm ausführen, sollte etwa Folgendes erscheinen:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑03‑27
Total: $1,234.56
...
```

Diese Ausgabe bestätigt, dass die **Bildtext‑Erkennung** erfolgreich war und Sie **Text aus PNG** erfolgreich extrahiert haben.

---

## Schritt 4: GPU‑Auslastung prüfen (optional, aber hilfreich)

Falls Sie wissen wollen, ob die GPU tatsächlich genutzt wird, öffnen Sie das GPU‑Überwachungstool Ihres Systems (z. B. `nvidia-smi` unter Linux). Während der Java‑Prozess läuft, sollten Sie einen leichten Anstieg von Speicher‑ und Compute‑Auslastung sehen.

```bash
$ nvidia-smi
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   PID   Type   Process name                  GPU Memory               |
|  0    12345 C++    java                           1024MiB                  |
+-----------------------------------------------------------------------------+
```

Wenn Sie keinerlei Aktivität sehen, prüfen Sie folgendes:

1. Der CUDA‑Treiber passt zum GPU‑Modell.  
2. Der Aufruf `setUseGpu(true)` wird später im Code nicht überschrieben.  
3. Ihre Lizenzdatei (falls vorhanden) beschränkt die GPU‑Nutzung nicht.

---

## Schritt 5: Umgang mit gängigen Randfällen

### Große Bilder, die den GPU‑Speicher überschreiten

Ist ein Bild sehr groß (z. B. 8000 × 8000 px), kann der GPU‑Speicher knapp werden. Eine schnelle Lösung ist, das Bild vor dem Weitergeben an Aspose herunterzuskalieren:

```java
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

BufferedImage original = ImageIO.read(new File("sample-large.png"));
int maxDim = 4000; // target max dimension
int width = original.getWidth();
int height = original.getHeight();

float scale = Math.min((float)maxDim / width, (float)maxDim / height);
int newWidth = Math.round(width * scale);
int newHeight = Math.round(height * scale);

BufferedImage resized = new BufferedImage(newWidth, newHeight, original.getType());
// Simple scaling (for demo purposes)
resized.getGraphics().drawImage(original, 0, 0, newWidth, newHeight, null);
ImageIO.write(resized, "png", new File("sample-resized.png"));
```

Anschließend übergeben Sie `"sample-resized.png"` an `recognizeImage`. So bleibt die OCR‑Genauigkeit erhalten, während Sie innerhalb der GPU‑Grenzen bleiben.

### Mehrseitige PDFs

Aspose OCR kann auch PDFs seitenweise verarbeiten. Durchlaufen Sie jede Seite, konvertieren Sie sie in ein Bild und geben Sie es an die Engine weiter. Das gleiche **use gpu acceleration**‑Flag gilt und liefert Ihnen eine schnelle PDF‑zu‑Text‑Pipeline.

---

## Vollständiges funktionierendes Beispiel (Copy‑Paste‑bereit)

Unten finden Sie die komplette Java‑Klasse, sofort kompilier‑ und ausführbar. Ersetzen Sie `YOUR_DIRECTORY` durch den Pfad zu Ihrer PNG‑Datei.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // Step 3: (Optional) Set the number of GPU streams for parallel processing
        // Using 2 streams works well on most modern GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);

        // Step 4: Perform OCR on the input image
        // This will **recognize image text** from a PNG file.
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // Step 5: Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Erwartete Ausgabe** – eine reine Textdarstellung von allem, was die Engine aus dem Bild lesen konnte. Enthält das Bild eine Tabelle, erhalten Sie die Zellinhalte hintereinander mit Zeilenumbrüchen; Aspose bewahrt das Layout nicht, Sie können den String jedoch bei Bedarf nachbearbeiten.

---

## Häufig gestellte Fragen

| Frage | Antwort |
|----------|--------|
| **Benötige ich eine kostenpflichtige Lizenz?** | Die Testversion funktioniert für bis zu 200 Seiten und entfernt das Wasserzeichen für OCR. Für den Produktionseinsatz entfernt eine Lizenz die Beschränkungen und schaltet den vollen GPU‑Stack frei. |
| **Was, wenn meine GPU älter ist (z. B. GTX 750)?** | Ältere GPUs können funktionieren, jedoch mit geringerer Geschwindigkeit; stellen Sie sicher, dass mindestens Compute Capability 3.0 unterstützt wird. |
| **Kann ich JPG‑ oder BMP‑Dateien verarbeiten?** | Absolut – `recognizeImage` akzeptiert jedes Format, das von Java ImageIO unterstützt wird. |
| **Gibt es eine Möglichkeit, viele Bilder stapelweise zu verarbeiten?** | Wickeln Sie den OCR‑Aufruf in eine Schleife und erhöhen Sie ggf. `setGpuStreams`, um die gewünschte Anzahl gleichzeitiger Streams zu nutzen. |
| **Wie kann ich das Layout erhalten?** | Verwenden Sie Aspose OCRs `LayoutOptions`, um Begrenzungsrahmen zu erhalten; das geht über den Rahmen dieses kurzen Leitfadens hinaus, ist aber in der API dokumentiert. |

---

## Fazit

Sie besitzen nun ein kompaktes, End‑to‑End‑**Java‑OCR‑Beispiel**, das **Bildtext erkennt**, **Text aus PNG extrahiert** und **GPU‑Beschleunigung** nutzt, um die Verarbeitung eines **OCR‑großen Bildes** zu beschleunigen. Durch Anpassen der GPU‑Stream‑Anzahl und ggf. Herunterskalieren übergroßer Bilder lässt sich die Lösung an praktisch jede Hardware‑Konfiguration anpassen.

Bereit für den nächsten Schritt? Versuchen Sie, einen Ordner mit gescannten Belegen in dieselbe Pipeline zu speisen, oder experimentieren Sie mit Aspose’s `TextRegion`‑API, um das ursprüngliche Layout beizubehalten. Und falls Sie auf Probleme stoßen, sind die Aspose‑Foren und das Javadoc hervorragende Ressourcen – denken Sie nur an die Grundlagen, die wir hier behandelt haben.

Viel Spaß beim Coden und möge Ihre OCR blitzschnell sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}