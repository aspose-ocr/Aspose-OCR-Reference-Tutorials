---
category: general
date: 2026-05-06
description: Wie man OCR verwendet, um Text aus einem Bild in Java zu extrahieren.
  Lernen Sie die OCR‑Bild‑zu‑Text‑Konvertierung, korrigieren Sie OCR‑Fehler und laden
  Sie ein Bild für OCR mit Aspose OCR.
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: de
og_description: Wie man OCR in Java verwendet, um Text aus einem Bild zu extrahieren,
  OCR‑Fehler zu korrigieren und ein Bild für OCR mit Aspose OCR zu laden.
og_title: Wie man OCR in Java verwendet – Vollständiger Leitfaden
tags:
- OCR
- Java
- Aspose
title: Wie man OCR in Java verwendet – Text aus Bild extrahieren mit Rechtschreibkorrektur
url: /de/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in Java verwendet – Text aus Bild extrahieren mit Rechtschreibkorrektur

Haben Sie sich jemals gefragt, **wie man OCR** verwendet, um ein verschwommenes Belegfoto in sauberen, durchsuchbaren Text zu verwandeln? Sie sind nicht allein. In vielen Projekten – Ausgaben‑Tracking‑Apps, Rechnungs‑Digitalisierungspipelines oder sogar ein schnelles Notiz‑Skript – ist das zuverlässige Extrahieren von Text aus einem Bild das erste Hindernis.  

Dieses Tutorial zeigt Ihnen genau, wie man OCR in Java verwendet, und deckt alles ab, vom Laden des Bildes für OCR bis zur Korrektur von OCR‑Fehlern, sodass das Ergebnis wie von einem Menschen getippt wirkt. Am Ende können Sie **Text aus Bild extrahieren**, **OCR Bild zu Text**‑Konvertierung durchführen und häufige Erkennungsfehler automatisch beheben.

## Was Sie bauen werden

Wir erstellen ein kleines Java‑Konsolenprogramm, das:

1. Lädt ein PNG (oder ein beliebiges unterstütztes Format) in die Aspose OCR‑Engine.  
2. Aktiviert die integrierte Rechtschreibkorrektur‑Funktion, um **OCR‑Fehler zu korrigieren**.  
3. Führt den Erkennungsprozess aus und gibt den bereinigten Text aus.  

Keine externen Dienste, keine schweren Frameworks – nur ein einzelnes JAR und ein paar Codezeilen.

### Voraussetzungen

- Java Development Kit (JDK) 8 oder neuer.  
- Maven (oder ein beliebiges Build‑Tool), um die Aspose OCR‑Bibliothek zu beziehen.  
- Eine Bilddatei (z. B. `receipt.png`), die Sie analysieren möchten.  

Wenn Ihnen das Aspose OCR JAR fehlt, fügen Sie diese Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **Profi‑Tipp:** Die kostenlose Evaluationsversion funktioniert zum Testen, aber eine Lizenz entfernt das Evaluations‑Wasserzeichen.

## Schritt 1 – Initialisieren der OCR‑Engine (Primäres Schlüsselwort in Aktion)

Das Erste, was Sie tun müssen, ist eine Instanz von `OcrEngine` zu erstellen. Denken Sie daran als das Gehirn, das die Pixel liest und in Zeichen umwandelt.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*Warum das wichtig ist:* Das Initialisieren der Engine richtet interne Ressourcen ein (Sprachmodelle, Wörterbücher usw.). Das Überspringen dieses Schrittes würde später zu einer `NullPointerException` führen, wenn Sie versuchen, ein Bild zu laden.

## Schritt 2 – Bild für OCR laden

Jetzt **laden wir das Bild für OCR**. Aspose stellt einen praktischen Helfer `ImageStream.fromFile` bereit, aber Sie können auch ein `byte[]` übergeben, wenn Sie möchten.

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*Häufiges Stolpern:* Der Dateipfad muss absolut oder relativ zum Arbeitsverzeichnis sein. Wenn das Bild nicht gefunden wird, wirft die Engine eine `IOException`. Überprüfen Sie den Pfad, besonders wenn Sie aus einer IDE statt aus einem gepackten JAR ausführen.

## Schritt 3 – Rechtschreibkorrektur aktivieren, um **OCR‑Fehler zu korrigieren**

Standard‑OCR kann verrauscht sein – denken Sie an „l0ve“ statt „love“ oder „0“ für „O“. Das Aktivieren der Rechtschreibkorrektur veranlasst die Engine, einen Nachbearbeitungsschritt auszuführen, der typische Fehler korrigiert.

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*Warum Sie das wollen:* Ohne Rechtschreibkorrektur müssten Sie die Ausgabe manuell bereinigen, was den Zweck der Automatisierung zunichte macht. Das integrierte Wörterbuch funktioniert gut für Englisch und mehrere andere Sprachen.

## Schritt 4 – Erkennung durchführen (**OCR Bild zu Text**)

Mit dem geladenen Bild und aktivierter Rechtschreibkorrektur können wir die Engine schließlich bitten, den Text zu erkennen.

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*Randfall:* Wenn das Bild wenig Kontrast hat oder stark verzerrt ist, kann das Ergebnis immer noch Kauderwelsch enthalten. Erwägen Sie eine Vorverarbeitung (z. B. Binärisierung, Entzerrung), bevor Sie es an die Engine übergeben.

## Schritt 5 – Bereinigten Text ausgeben

Der letzte Schritt besteht einfach darin, das Ergebnis auszugeben. In einer echten Anwendung könnten Sie es in eine Datenbank oder eine Datei schreiben, aber für diese Demo reicht `System.out` aus.

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Erwartete Ausgabe

Angenommen, `receipt.png` enthält eine klare Artikelliste, dann könnte die Ausgabe etwa so aussehen:

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

Beachten Sie, dass „Qty“ und „Price“ korrekt geschrieben sind, selbst wenn der ursprüngliche Scan ein verirrtes „Qy“ enthielt.

## Vollständiges funktionierendes Beispiel

Unten finden Sie das vollständige Programm, das Sie in eine Datei namens `SpellCorrectDemo.java` kopieren können. Stellen Sie sicher, dass das Aspose OCR‑JAR in Ihrem Klassenpfad liegt.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

Führen Sie es aus mit:

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

Sie sollten nun den bereinigten Text in der Konsole sehen.

## Bonus: Einstellungen für bessere Genauigkeit anpassen

Obwohl die Standardkonfiguration für die meisten gedruckten Dokumente funktioniert, müssen Sie möglicherweise einige Parameter für spezielle Szenarien anpassen:

| Einstellung | Was es macht | Wann ändern |
|------------|--------------|-------------|
| `setLanguage(OcrLanguage.English)` | Erzwingt englisches Wörterbuch (reduziert Fehlalarme) | Wenn Ihr Bild nur englischen Text enthält. |
| `setResolution(300)` | Teilt der Engine die DPI des Quellbildes mit | Für hochauflösende Scans. |
| `setEnableAutoSkewCorrection(true)` | Dreht leicht geneigte Seiten automatisch | Wenn Bilder mit einem Telefon aufgenommen wurden. |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## Häufig gestellte Fragen

**F: Funktioniert das mit PDFs?**  
A: Ja. Konvertieren Sie jede PDF‑Seite in ein Bild (z. B. mit Aspose PDF) und übergeben Sie das Bild an die OCR‑Engine.

**F: Was ist, wenn mein Bild im BMP‑Format vorliegt?**  
A: `ImageStream.fromFile` unterstützt PNG, JPEG, BMP, TIFF und GIF von Haus aus. Ändern Sie einfach die Dateierweiterung.

**F: Kann ich die Rechtschreibkorrektur deaktivieren?**  
A: Absolut – setzen Sie `setEnableSpellCorrection(false)`, wenn Sie rohe OCR‑Ausgabe für nachgelagerte Verarbeitung benötigen.

## Fazit

Sie wissen jetzt, **wie man OCR** in Java verwendet, um **Text aus Bild zu extrahieren**, automatisch **OCR‑Fehler zu korrigieren** und korrekt **Bild für OCR zu laden** mit Aspose OCR. Der fünf‑schrittige Ablauf – initialisieren, laden, Rechtschreibkorrektur aktivieren, erkennen und ausgeben – deckt die meisten alltäglichen OCR‑Aufgaben ab.  

Ab hier sollten Sie überlegen, diese Logik mit einem Datenbank‑Write‑Back, einem REST‑Endpunkt oder einem Batch‑Prozessor zu verketten, um Dutzende von Belegen gleichzeitig zu verarbeiten. Experimentieren Sie mit der obigen Tabelle zusätzlicher Einstellungen, um jede letzte Genauigkeit herauszuholen.

Viel Spaß beim Programmieren, und möge Ihr OCR‑Ergebnis immer sauberer sein als Ihre kaffeefleckigen Belege! 

![Diagramm zur Verwendung von OCR, das Bild → OCR‑Engine → korrigierten Textfluss zeigt]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}