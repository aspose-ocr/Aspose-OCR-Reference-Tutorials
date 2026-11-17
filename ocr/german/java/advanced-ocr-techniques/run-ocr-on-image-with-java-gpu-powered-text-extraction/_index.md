---
category: general
date: 2026-03-07
description: Führen Sie OCR auf einem Bild mit Java aus. Erfahren Sie, wie Sie Text
  aus PNG erkennen, Text von einer Quittung extrahieren und ein Bild für OCR laden
  – mit einem vollständigen Java-OCR‑Beispiel.
draft: false
keywords:
- run OCR on image
- recognize text from png
- extract text from receipt
- java OCR example
- load image for OCR
language: de
og_description: Führen Sie OCR auf einem Bild mit Java aus. Dieser Leitfaden zeigt,
  wie man Text aus einer PNG erkennt, Text von einem Beleg extrahiert und ein Bild
  für OCR lädt, anhand eines vollständigen Java‑OCR‑Beispiels.
og_title: Run OCR on Image with Java – GPU Powered Text Extraction
tags:
- OCR
- Java
- GPU
- Image Processing
title: OCR auf Bild mit Java ausführen – GPU‑gestützte Textextraktion
url: /de/java/advanced-ocr-techniques/run-ocr-on-image-with-java-gpu-powered-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf Bild mit Java ausführen – GPU‑beschleunigte Textextraktion

Hast du jemals **OCR auf Bild**‑Dateien ausführen müssen, warst dir aber nicht sicher, wo du in Java anfangen sollst? Du bist nicht allein – viele Entwickler stoßen beim ersten Versuch, Text aus einem gescannten Kassenbon oder einem PNG‑Screenshot zu extrahieren, auf dieselbe Hürde.  

In diesem Tutorial führen wir dich durch ein **komplettes Java‑OCR‑Beispiel**, das nicht nur **Text aus PNG**‑Dateien erkennt, sondern auch zeigt, wie man **Text aus Kassenbon‑Bildern** extrahiert, und das alles mit GPU‑Beschleunigung für höhere Geschwindigkeit. Am Ende hast du ein einsatzbereites Programm, das ein Bild für OCR lädt, verarbeitet und das Ergebnis als Klartext ausgibt.

## Was du lernen wirst

- Wie man **Bild für OCR lädt** mit einem einfachen `ImageInputStream`.
- GPU‑Unterstützung aktivieren, damit die Engine auf moderner Hardware schneller läuft.
- Die genauen Schritte, um **Text aus PNG** zu erkennen und nützliche Zeichenketten aus einem Kassenbon zu ziehen.
- Häufige Stolperfallen (z. B. falsche GPU‑Device‑ID) und Best‑Practice‑Tipps.
- Ein vollständiges, ausführbares Code‑Snippet, das du in deine IDE kopieren‑und‑einfügen kannst.

**Voraussetzungen**

- Java 17 oder neuer (der Code verwendet das `var`‑Schlüsselwort für Kürze, du kannst es bei Java 8 durch explizite Typen ersetzen).
- Eine OCR‑Bibliothek, die die Klassen `OcrEngine`, `ImageInputStream` und `OcrResult` bereitstellt (z. B. das fiktive *FastOCR* SDK; ersetze es durch die reale Bibliothek, die du nutzt).
- Ein GPU‑fähiger Rechner, wenn du den Performance‑Boost nutzen willst (optional, aber empfohlen).

---

## Schritt 1: OCR auf Bild ausführen – GPU‑Beschleunigung aktivieren

Als erstes muss die OCR‑Engine erstellt und angewiesen werden, die GPU zu nutzen. Dieser Schritt ist entscheidend, weil die Engine ohne GPU‑Unterstützung auf die CPU zurückfällt, was bei hochauflösenden Bons deutlich langsamer sein kann.

```java
// Step 1: Create the OCR engine and enable GPU acceleration
OcrEngine ocrEngine = new OcrEngine();

// Turn on GPU usage – this makes the recognition much faster
ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage

// Optional: select which GPU device to use (0 = first GPU)
ocrEngine.getConfig().setGpuDeviceId(0);
```

**Warum das wichtig ist:**  
GPU‑Beschleunigung verlagert die schweren Matrix‑Berechnungen, die OCR‑Engines durchführen, auf die Grafikkarte. Wenn du mehrere GPUs hast, kannst du die mit dem meisten Speicher auswählen, indem du den Wert von `setGpuDeviceId` änderst. Das Vergessen, die GPU zu aktivieren, ist eine häufige Ursache für „Warum ist mein OCR so langsam?“-Beschwerden.

> **Pro‑Tipp:** Wenn dein Rechner keine kompatible GPU hat, wird der Aufruf `setUseGpu(true)` einfach ignoriert – kein Absturz, nur langsamere Verarbeitung.

---

## Schritt 2: Bild für OCR laden

Jetzt, wo die Engine bereit ist, müssen wir ihr ein Bild zuführen. Das Beispiel unten zeigt, wie man einen PNG‑Kassenbon von der Festplatte lädt. Du kannst den Pfad durch jedes von deiner OCR‑Bibliothek unterstützte Bildformat ersetzen.

```java
// Step 2: Load the image you want to recognize
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
```

**Randfall:**  
Falls die Datei nicht existiert oder der Pfad falsch ist, wirft `ImageInputStream` eine `IOException`. Umschließe den Aufruf daher mit einem try‑catch‑Block und protokolliere eine hilfreiche Meldung:

```java
try {
    ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
} catch (IOException e) {
    System.err.println("Failed to load image: " + e.getMessage());
    return;
}
```

---

## Schritt 3: Text aus PNG erkennen

Nachdem das Bild geladen ist, kann die OCR‑Engine nun ihr Werk tun. Dieser Schritt **erkennt Text aus PNG** (oder jedem anderen unterstützten Format) und liefert ein `OcrResult`‑Objekt zurück.

```java
// Step 3: Run the OCR process on the image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

**Was im Hintergrund passiert:**  
Die Engine führt Vorverarbeitung (Entzerrung, Binarisierung) durch, lässt ein neuronales Netzwerk Zeichen erkennen und fügt diese anschließend zu Textzeilen zusammen. Da wir die GPU bereits aktiviert haben, erfolgen diese neuronalen Netzwerk‑Berechnungen auf der Grafikkarte, was Sekunden vom Gesamtlaufzeit spart.

---

## Schritt 4: Text aus Kassenbon extrahieren

Nach der Erkennung möchtest du in der Regel nur den Rohtext. Die Klasse `OcrResult` stellt normalerweise eine Methode `getText()` bereit, die einen einzelnen `String` zurückgibt. Anschließend kannst du diesen weiterverarbeiten (z. B. mit Regex Gesamtsummen, Daten usw. herausziehen).

```java
// Step 4: Print the recognized plain‑text result
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Typische Kassenbon‑Ausgabe:**  

```
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Jetzt kannst du diesen String in deinen eigenen Parser einspeisen, um den Gesamtbetrag, einzelne Positionen oder Steuerinformationen zu extrahieren.

---

## Schritt 5: Vollständiges Java‑OCR‑Beispiel – sofort lauffähig

Alles zusammengeführt, hier das **komplette Java‑OCR‑Beispiel**, das du in eine `Main.java`‑Datei einfügen kannst. Stelle sicher, dass die OCR‑Bibliothek im Klassenpfad liegt.

```java
import com.fastocr.OcrEngine;
import com.fastocr.ImageInputStream;
import com.fastocr.OcrResult;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ Create OCR engine and enable GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage
        ocrEngine.getConfig().setGpuDeviceId(0);        // optional: select GPU #0

        // 2️⃣ Load the image you want to recognize
        ImageInputStream imageStream;
        try {
            imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return;
        }

        // 3️⃣ Run OCR on the image
        OcrResult ocrResult = ocrEngine.recognize(imageStream);

        // 4️⃣ Output the plain‑text result
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Erwartete Konsolenausgabe** (bei dem Beispiel‑Kassenbon oben):

```
Recognized text:
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Sieht die Ausgabe verzerrt aus, prüfe, ob das Bild klar (hohe DPI) ist und ob das OCR‑Sprachpaket zu der Sprache deines Bons passt.

---

## Häufige Fragen & Stolperfallen

| Frage | Antwort |
|----------|--------|
| *Was, wenn meine GPU nicht erkannt wird?* | Die Engine fällt automatisch auf die CPU zurück. Überprüfe Treiber und dass `setGpuDeviceId` zu einem existierenden Gerät passt (`nvidia-smi` unter Linux kann helfen). |
| *Kann ich JPEG‑ oder TIFF‑Dateien verarbeiten?* | Ja – ändere einfach die Dateierweiterung in `ImageInputStream`. Die OCR‑Bibliothek erkennt das Format meist automatisch. |
| *Gibt es eine Möglichkeit, viele Bons stapelweise zu verarbeiten?* | Packe den Erkennungscode in eine Schleife und verwende dieselbe `OcrEngine`‑Instanz; ein erneutes Initialisieren pro Bild verschwendet GPU‑Speicher. |
| *Wie verbessere ich die Genauigkeit bei kontrastarmen Bons?* | Vorverarbeite das Bild (Kontrast erhöhen, in Graustufen konvertieren), bevor du es an die OCR‑Engine übergibst. Einige Bibliotheken bieten eine `preprocess`‑API. |

---

## Fazit

Du weißt jetzt **wie man OCR auf Bild**‑Dateien in Java ausführt – vom Laden des Bildes bis zum Extrahieren sauberen Textes aus einem Kassenbon. Der Leitfaden behandelte **Text aus PNG erkennen**, **Text aus Kassenbon extrahieren** und zeigte ein **Java‑OCR‑Beispiel**, das du in jedes Projekt einbinden kannst.  

Nächste Schritte? Schalte das GPU‑Flag aus, um den Leistungsunterschied zu sehen, experimentiere mit verschiedenen Bildauflösungen oder integriere einen Regex‑basierten Parser, um Beträge automatisch zu extrahieren. Wenn du mehr über fortgeschrittene Themen erfahren willst, sieh dir **OCR‑Nachbearbeitung**, **Sprachmodell‑Korrektur** oder **Batch‑Verarbeitungspipelines** an.

Viel Spaß beim Coden, und mögen deine Bons immer lesbar sein!  

![run OCR on image example](/images/run-ocr-on-image.png "run OCR on image – Java example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}