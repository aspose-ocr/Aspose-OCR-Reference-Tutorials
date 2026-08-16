---
category: general
date: 2026-04-26
description: Erfahren Sie, wie Sie OCR ausführen und Text aus einem Bild mit Aspose
  OCR extrahieren. Dieser Leitfaden zeigt, wie Sie ein Bild für OCR laden, die automatische
  Spracherkennung aktivieren und die Sprache automatisch bei OCR erkennen.
draft: false
keywords:
- how to perform OCR
- extract text from image
- load image for OCR
- enable automatic language detection
- auto detect language OCR
language: de
og_description: Wie man OCR in Java mit Aspose OCR durchführt. Erfahren Sie, wie Sie
  ein Bild für OCR laden, die automatische Spracherkennung aktivieren und Text aus
  dem Bild extrahieren.
og_title: Wie man OCR in Java durchführt – Sprache automatisch erkennen
tags:
- OCR
- Java
- Aspose
title: Wie man OCR in Java durchführt – Sprache automatisch erkennen und Text extrahieren
url: /de/java/advanced-ocr-techniques/how-to-perform-ocr-in-java-auto-detect-language-and-extract/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in Java durchführt – automatische Spracherkennung und Textextraktion

Haben Sie jemals wissen wollen, **wie man OCR** auf einem Foto durchführt, das Englisch, Spanisch und vielleicht einige japanische Zeichen mischt? Sie sind nicht allein – Entwickler stoßen ständig auf dieses Problem, wenn ihre Apps Text aus gescannten Dokumenten, Quittungen oder mehrsprachigen Schildern lesen müssen.  

Die gute Nachricht? Mit ein paar Zeilen Java und Aspose OCR können Sie **load image for OCR**, **enable automatic language detection** aktivieren und sofort **extract text from image** durchführen, ohne die Sprache vorher raten zu müssen. In diesem Tutorial gehen wir das vollständige, ausführbare Beispiel durch, erklären, warum jeder Schritt wichtig ist, und zeigen Ihnen, wie Sie das Ergebnis von **auto detect language OCR** überprüfen können.

> **Was Sie am Ende haben**  
> * Ein funktionierendes Java‑Programm, das ein mehrsprachiges PNG liest.  
> * Wissen über die wichtigsten OCR‑Einstellungen, die die Spracherkennung mühelos machen.  
> * Tipps zum Umgang mit fehlenden Dateien, nicht unterstützten Sprachen und Leistungsoptimierungen.

## Voraussetzungen

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| Java 17 (or newer) | Aspose OCR zielt auf moderne JVMs ab; ältere Versionen könnten API‑Funktionen fehlen. |
| Aspose OCR for Java library (latest version) | Stellt `OcrEngine` und language‑auto‑detect‑Fähigkeiten bereit. |
| An image file (`mixed_lang.png`) containing text in at least two languages | Demonstriert die **auto detect language OCR**‑Funktion. |
| A Java IDE or simple command‑line setup | Zum Kompilieren und Ausführen des Beispielcodes. |

Falls Sie das Aspose OCR JAR noch nicht heruntergeladen haben, holen Sie es aus dem offiziellen Maven‑Repository:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- replace with the latest -->
</dependency>
```

## Schritt 1: Erstellen der OCR‑Engine‑Instanz – Wie man OCR durchführt

Das allererste, was Sie tun, wenn Sie **perform OCR** möchten, ist die Engine zu instanziieren. Denken Sie an `OcrEngine` als das Gehirn, das das Bitmap analysiert und Pixel in Zeichen umwandelt.

```java
// Step 1: Initialize the OCR engine
import com.aspose.ocr.*;

public class AutoDetectDemo {
    public static void main(String[] args) throws Exception {

        // Create a fresh OcrEngine object – this is where the magic starts
        OcrEngine ocrEngine = new OcrEngine();
```

> **Pro‑Tipp:** Die Wiederverwendung derselben `OcrEngine` für viele Bilder kann die Leistung steigern, weil die Engine Sprachmodelle intern cached.

## Schritt 2: Automatische Spracherkennung aktivieren – Enable Automatic Language Detection

Standardmäßig geht Aspose OCR von Englisch aus. Für mehrsprachige Bilder müssen Sie ihm mitteilen, die Sprache pro Textblock zu „raten“. Genau das bewirkt das **enable automatic language detection**‑Flag.

```java
        // Step 2: Turn on auto‑language detection for each region
        ocrEngine.getRecognitionSettings()
                 .setLanguage(OcrLanguage.AUTO_DETECT);
```

Warum das wichtig ist: Die Engine untersucht nun jedes Segment des Bildes, wählt die wahrscheinlichste Sprache aus und wendet den korrekten Zeichensatz an. Ohne diese Einstellung erhalten Sie ein unleserliches Ergebnis für nicht‑englische Abschnitte.

## Schritt 3: Bild für OCR laden – Load Image for OCR

Jetzt **load image for OCR** wir tatsächlich. Der Pfad kann absolut oder relativ sein; stellen Sie einfach sicher, dass die Datei existiert, sonst erhalten Sie eine `FileNotFoundException`.

```java
        // Step 3: Point the engine at the image that contains mixed‑language text
        ocrEngine.setImage("YOUR_DIRECTORY/mixed_lang.png");
```

> **Randfall:** Wenn sich Ihr Bild im resources‑Ordner eines Maven‑Projekts befindet, verwenden Sie `getClass().getResource("/mixed_lang.png")`, um hartkodierte Pfade zu vermeiden.

## Schritt 4: Erkennung ausführen und Text aus Bild extrahieren – Extract Text from Image

Mit der konfigurierten Engine und dem geladenen Bild ist es Zeit, tatsächlich **perform OCR** auszuführen. Der Aufruf `recognize()` erledigt die schwere Arbeit, während `getText()` einen einfachen `String` zurückgibt.

```java
        // Step 4: Execute OCR and fetch the recognized text
        String recognizedText = ocrEngine.recognize().getText();
```

Zu diesem Zeitpunkt hat die Bibliothek bereits **auto detect language OCR** für jeden Block durchgeführt, sodass die Variable `recognizedText` eine saubere, sprachbewusste Transkription enthält.

## Schritt 5: Ergebnis anzeigen – Verify Auto‑Detect Language OCR Output

Abschließend geben wir das Ergebnis in der Konsole aus. In einer echten Anwendung könnten Sie es in eine Datei, eine Datenbank schreiben oder an einen Übersetzungsdienst weitergeben.

```java
        // Step 5: Show the output – you’ll see language tags if you enable them
        System.out.println("Auto‑detected language output:\n" + recognizedText);
    }
}
```

### Erwartete Ausgabe

Angenommen, `mixed_lang.png` enthält „Hello“ (Englisch) und „¡Hola!“ (Spanisch), dann sehen Sie etwa Folgendes:

```
Auto‑detected language output:
Hello
¡Hola!
```

Wenn Sie `setShowLanguage(true)` in den Einstellungen aktivieren, fügt die Engine jeder Zeile einen Sprachcode hinzu, z. B. `[en] Hello` und `[es] ¡Hola!]`.

## Häufige Fragen & Fallstricke

### Was ist, wenn der Bildpfad falsch ist?

Die Engine wirft eine `FileNotFoundException`. Umgeben Sie den Aufruf mit einem try‑catch‑Block und geben Sie dem Benutzer eine freundliche Meldung aus:

```java
try {
    ocrEngine.setImage("path/to/image.png");
} catch (FileNotFoundException e) {
    System.err.println("Image not found – check the file path!");
    return;
}
```

### Kann ich die Sprachen einschränken, um die Erkennung zu beschleunigen?

Ja. Anstelle von `AUTO_DETECT` können Sie eine Liste bereitstellen:

```java
ocrEngine.getRecognitionSettings()
         .setLanguage(new OcrLanguage[]{OcrLanguage.ENGLISH, OcrLanguage.SPANISH});
```

Dies reduziert den Suchraum und kann die Leistung bei großen Stapeln verbessern.

### Wie geht **auto detect language OCR** mit handgeschriebenem Text um?

Aspose OCR konzentriert sich auf gedruckten Text. Handschriftliche Skripte benötigen in der Regel eine andere Engine (z. B. Aspose OCR for Handwriting). Der Versuch, die Erkennung zu erzwingen, führt zu schlechten Ergebnissen.

## Vollständiges funktionierendes Beispiel (Copy‑Paste‑bereit)

Unten finden Sie das gesamte Programm, bereit zum Kompilieren und Ausführen. Ersetzen Sie `YOUR_DIRECTORY` durch den tatsächlichen Ordner, der `mixed_lang.png` enthält.

```java
import com.aspose.ocr.*;

public class AutoDetectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine – this is where the magic starts
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection for each text block
        ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.AUTO_DETECT);

        // Step 3: Load the image that contains mixed‑language text
        // Make sure the file exists; otherwise an exception is thrown
        ocrEngine.setImage("YOUR_DIRECTORY/mixed_lang.png");

        // Step 4: Run the recognition process and obtain the extracted text
        String recognizedText = ocrEngine.recognize().getText();

        // Step 5: Display the auto‑detected language output
        System.out.println("Auto‑detected language output:\n" + recognizedText);
    }
}
```

Führen Sie es aus mit:

```bash
javac -cp "aspose-ocr-23.10.jar" AutoDetectDemo.java
java -cp ".:aspose-ocr-23.10.jar" AutoDetectDemo
```

Sie sollten die zuvor beschriebene Konsolenausgabe sehen.

## Erweiterung der Lösung

Jetzt, da Sie **how to perform OCR** kennen, betrachten Sie die nächsten Schritte:

* **Batchverarbeitung** – Durchlaufen Sie einen Ordner mit Bildern und verwenden Sie dieselbe `OcrEngine`‑Instanz erneut für mehr Geschwindigkeit.
* **Ergebnisse speichern** – Schreiben Sie den extrahierten Text in `.txt`‑Dateien oder speichern Sie ihn in einer Datenbank.
* **Nachbearbeitung** – Verwenden Sie reguläre Ausdrücke, um Zeilenumbrüche zu bereinigen oder unerwünschte Zeichen zu entfernen.
* **Integration** – Leiten Sie die Ausgabe an eine Übersetzungs‑API (Google Translate, Azure Translator) für mehrsprachige Anwendungen weiter.

Jede dieser Erweiterungen baut weiterhin auf den Kernkonzepten auf, die wir behandelt haben: Bild laden, Spracherkennung aktivieren und Text extrahieren.

## Fazit

Wir haben ein vollständiges End‑zu‑Ende‑Beispiel durchgearbeitet, das **how to perform OCR** in Java zeigt, während Sprachen automatisch erkannt werden. Durch Befolgen der fünf Schritte – Engine erstellen, automatische Spracherkennung aktivieren, Bild laden, Erkennung ausführen und Ergebnisse anzeigen – können Sie zuverlässig **extract text from image**‑Dateien extrahieren, die mehrere Schriftsysteme enthalten.  

Denken Sie daran, dass der Schlüssel zu einer reibungslosen **auto detect language OCR** darin liegt, die Engine pro Block entscheiden zu lassen; das Erzwingen einer einzelnen Sprache führt häufig zu unleserlichen Ausgaben. Experimentieren Sie mit verschiedenen Bildqualitäten, Sprachlisten und Leistungsoptimierungen, um das Erlebnis für Ihren Anwendungsfall zu verfeinern.  

Haben Sie ein Szenario, das hier nicht behandelt wird? Hinterlassen Sie einen Kommentar, und wir lösen das gemeinsam. Viel Spaß beim Programmieren!  

![Beispiel für OCR durchführen](/images/ocr-demo.png "Screenshot, der zeigt, wie man OCR mit Aspose OCR in Java durchführt")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}