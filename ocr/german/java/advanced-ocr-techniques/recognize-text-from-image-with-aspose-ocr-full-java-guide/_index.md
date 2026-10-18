---
category: general
date: 2026-02-09
description: Erfahren Sie, wie Sie Text aus Bildern mit Aspose OCR in Java erkennen.
  Dieses Schritt‑für‑Schritt‑Tutorial behandelt außerdem Rechtschreibprüfung, benutzerdefinierte
  Wörterbücher und die Konfiguration der OCR‑Engine.
draft: false
keywords:
- recognize text from image
- Aspose OCR Java
- OCR spell checking
- custom OCR dictionary
- Java image processing
language: de
og_description: Erkennen Sie Text aus einem Bild in Java mit Aspose OCR. Folgen Sie
  dieser Anleitung, um die Rechtschreibprüfung zu aktivieren, die Sprache einzustellen
  und sofort korrigierte Ausgaben zu erhalten.
og_title: Text aus Bild mit Aspose OCR erkennen – Komplettes Java‑Tutorial
tags:
- OCR
- Java
- Aspose
title: Text aus Bild erkennen mit Aspose OCR – Vollständiger Java-Leitfaden
url: /de/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild erkennen – Vollständiges Java‑Tutorial

Haben Sie jemals **Text aus Bild erkennen** müssen, waren sich aber nicht sicher, welche API vertrauenswürdig ist? Sie sind nicht allein. In vielen Projekten – Rechnungsscan, Digitalisierung handschriftlicher Notizen oder Aufbau eines durchsuchbaren Archivs – ist die Fähigkeit, sauberen, lesbaren Text aus einem Bild zu extrahieren, ein echter Wendepunkt.  

Die gute Nachricht? Mit Aspose OCR für Java können Sie das in wenigen Zeilen erledigen, und Sie erhalten sogar eine integrierte Rechtschreibprüfung, um das OCR‑Ergebnis zu bereinigen. In diesem Tutorial führen wir Sie durch den gesamten Prozess, vom Erstellen der OCR‑Engine bis zum Ausgeben des korrigierten Ergebnisses. Am Ende haben Sie eine sofort ausführbare Java‑Klasse, die **Text aus Bild erkennt** zuverlässig.

---

## Was Sie benötigen

- **Java 8+** (der Code funktioniert mit jedem aktuellen JDK)
- **Aspose OCR for Java** Bibliothek – Sie können das neueste JAR aus dem Aspose Maven‑Repository holen oder es direkt von der Aspose‑Website herunterladen.
- Eine Bilddatei, die getippten oder gedruckten Text enthält (z. B. `typed_scanned_doc.png`).
- Eine bescheidene Menge RAM; OCR ist nicht ressourcenintensiv, aber ein 1 GB‑Heap reicht für die meisten Scans aus.

> *Pro‑Tipp:* Wenn Sie Maven verwenden, fügen Sie die folgende Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Jetzt, wo die Voraussetzungen erledigt sind, tauchen wir in den Code ein.

---

## Schritt 1: OCR‑Engine initialisieren und ihre Konfiguration abrufen

Das Erste, was Sie tun, ist eine Instanz von `OcrEngine` zu erstellen. Dieses Objekt ist das Herz der Bibliothek; es enthält alle Einstellungen, die Sie später anpassen werden.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class SpellCheckExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and obtain its configuration object
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration ocrConfig = ocrEngine.getConfiguration();
```

Warum das wichtig ist: Das Konfigurationsobjekt gibt Ihnen direkten Zugriff auf die Sprachauswahl, Rechtschreibprüfungs‑Flags und Wörterbuchpfade. Ohne dieses wären Sie auf die Vorgaben beschränkt, die möglicherweise nicht zu Ihrem Ausgangsmaterial passen.

---

## Schritt 2: Sprache auswählen und Rechtschreibprüfung aktivieren

Als Nächstes teilen Sie der Engine mit, welche Sprache im Bild erwartet wird. Hier wählen wir Englisch, aber Aspose unterstützt Dutzende von Locale‑Einstellungen.

```java
        // Step 2: Choose the language for recognition and turn on spell‑checking
        ocrConfig.setLanguage(Language.ENGLISH);
        ocrConfig.setSpellCheckEnabled(true);
```

Die Aktivierung der Rechtschreibprüfung ist optional, verbessert jedoch die Lesbarkeit der Ausgabe erheblich – besonders bei gescannten Dokumenten, bei denen die OCR‑Engine eine „0“ fälschlicherweise als „O“ interpretieren könnte.

---

## Schritt 3: (Optional) Eigenes Rechtschreibwörterbuch laden

Wenn Sie mit branchenspezifischem Jargon arbeiten – denken Sie an medizinische Begriffe, juristische Abkürzungen oder benutzerdefinierte Produktcodes – ermöglicht Ihnen Aspose, Ihr eigenes Wörterbuch einzubinden.

```java
        // Step 3: (Optional) Provide a custom spell‑check dictionary
        ocrConfig.setSpellCheckDictionary("en_US"); // use a locale‑specific dictionary
```

Sie können `setSpellCheckDictionary` auch auf eine `.dic`‑Datei mit vollständigem Pfad verweisen, wenn Sie eine maßgeschneiderte Liste besitzen. Die Engine wird Ihre benutzerdefinierten Wörter mit dem integrierten Wörterbuch zusammenführen, sodass domänenspezifisches Vokabular erhalten bleibt.

---

## Schritt 4: OCR auf Ihrer Bilddatei ausführen

Jetzt beginnt die eigentliche Arbeit. Geben Sie den Pfad zu Ihrem Bild an und lassen Sie die Engine ihre Magie wirken.

```java
        // Step 4: Run OCR on the input image file
        RecognitionResult recognitionResult = ocrEngine.recognize("YOUR_DIRECTORY/typed_scanned_doc.png");
```

Im Hintergrund wendet Aspose eine Reihe von Vorverarbeitungsschritten an – Entzerrung, Binarisierung und Zeichensegmentierung – bevor die Pixeldaten an den neuronalen Erkenner übergeben werden. Das Ergebnis wird in einem `RecognitionResult`‑Objekt verpackt, das sowohl den Roh‑ als auch den korrigierten Text enthält.

---

## Schritt 5: Korrigierten Text anzeigen

Zum Schluss geben Sie die bereinigte Zeichenkette in der Konsole aus. Sie sehen das OCR‑Ergebnis **mit angewandter Rechtschreibprüfung**, das häufig bereits direkt in einer Datenbank gespeichert oder in einen Suchindex eingespeist werden kann.

```java
        // Step 5: Display the corrected text returned by the engine
        System.out.println("Corrected text:");
        System.out.println(recognitionResult.getText());
    }
}
```

### Erwartete Ausgabe

Angenommen, `typed_scanned_doc.png` enthält den Satz *„The quick brown fox jumps over the lazy dog.“*, dann wird die Konsole Folgendes anzeigen:

```
Corrected text:
The quick brown fox jumps over the lazy dog.
```

Wenn der ursprüngliche Scan einen Fleck hatte, der „quick“ in „qu1ck“ verwandelte, würde die Rechtschreibprüfung es automatisch wieder zu „quick“ korrigieren.

---

## Umgang mit häufigen Sonderfällen

### 1. Bilder mit niedriger Auflösung

Die OCR‑Genauigkeit sinkt stark unter 150 dpi. Wenn Ihre Quellbilder eine niedrige Auflösung haben, sollten Sie sie zuerst hochskalieren (z. B. mit OpenCV) oder einen Scan in höherer Qualität anfordern.  

### 2. Dokumente mit mehreren Sprachen

Aspose OCR kann Sprachen unterwegs wechseln, aber Sie müssen das passende `Language`‑Enum vor jedem `recognize`‑Aufruf setzen. Für gemischte Sprachseiten müssen Sie das Bild möglicherweise zweimal durch die Engine laufen lassen – einmal pro Sprache – und anschließend die Ergebnisse zusammenführen.

### 3. Große PDFs oder mehrseitige TIFFs

Wenn Sie **Text aus Bild erkennen** Dateien, die in PDFs eingebettet sind, benötigen, extrahieren Sie jede Seite als Bild (mit Aspose PDF oder einer anderen Bibliothek) und übergeben Sie sie einzeln an die OCR‑Engine. Die Engine ist zustandslos, sodass Sie dieselbe `OcrEngine`‑Instanz über mehrere Seiten hinweg wiederverwenden können.

### 4. Empfindlichkeit der Rechtschreibprüfung anpassen

Der standardmäßige Schwellenwert der Rechtschreibprüfung funktioniert für die meisten englischen Texte. Für stark technische Dokumente können Sie die Empfindlichkeit senken, indem Sie die internen `SpellCheckOptions` anpassen – wobei dies ein Eintauchen in Asposes erweiterte API erfordert, was den Rahmen dieses Einsteiger‑Leitfadens sprengt.

---

## Vollständiges funktionierendes Beispiel (Copy‑Paste‑bereit)

Unten finden Sie die vollständige Java‑Klasse, bereit zum Kompilieren und Ausführen. Ersetzen Sie `YOUR_DIRECTORY/typed_scanned_doc.png` durch den tatsächlichen Pfad zu Ihrem Bild.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class SpellCheckExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and obtain its configuration object
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration ocrConfig = ocrEngine.getConfiguration();

        // Step 2: Choose the language for recognition and turn on spell‑checking
        ocrConfig.setLanguage(Language.ENGLISH);
        ocrConfig.setSpellCheckEnabled(true);

        // Step 3: (Optional) Provide a custom spell‑check dictionary
        ocrConfig.setSpellCheckDictionary("en_US"); // or a full path to your .dic file

        // Step 4: Run OCR on the input image file
        RecognitionResult recognitionResult = ocrEngine.recognize("YOUR_DIRECTORY/typed_scanned_doc.png");

        // Step 5: Display the corrected text returned by the engine
        System.out.println("Corrected text:");
        System.out.println(recognitionResult.getText());
    }
}
```

Kompilieren mit:

```bash
javac -cp "path/to/aspose-ocr.jar" SpellCheckExample.java
java -cp ".;path/to/aspose-ocr.jar" SpellCheckExample
```

Sie sollten den korrigierten Text in der Konsole sehen, was bestätigt, dass Sie erfolgreich **Text aus Bild erkannt** und die Rechtschreibprüfung angewendet haben.

---

## Häufig gestellte Fragen

**Q: Unterstützt Aspose OCR Handschrift?**  
A: Die Bibliothek ist für gedruckten Text optimiert. Handschriftliche Erkennung ist in einem separaten Modul (`aspose-ocr-handwriting`) verfügbar, das Sie ähnlich integrieren können.

**Q: Kann ich Bilder von einer URL statt einer lokalen Datei verarbeiten?**  
A: Ja. Laden Sie das Bild in einen temporären Puffer (z. B. mit `java.net.URL`) und übergeben Sie das Byte‑Array an `ocrEngine.recognize(InputStream)`.

**Q: Was, wenn ich nur bestimmte Bildbereiche extrahieren muss?**  
A: Verwenden Sie `ocrEngine.setRegion(Rectangle)` vor dem Aufruf von `recognize`. Dadurch wird die OCR auf das definierte Rechteck beschränkt, was Zeit spart und Fehlalarme reduziert.

---

## Fazit

Wir haben gerade ein vollständiges End‑zu‑Ende‑Beispiel durchlaufen, wie man **Text aus Bild erkennt** mit Aspose OCR für Java. Durch die Konfiguration der OCR‑Engine, das Aktivieren der Rechtschreibprüfung und optionales Laden eines eigenen Wörterbuchs können Sie verrauschte Scans in sauberen, durchsuchbaren Text verwandeln – mit minimalem Code.

Von hier aus könnten Sie folgendes erkunden:

- **Batch‑Verarbeitung** – über einen Ordner mit Bildern iterieren und jedes Ergebnis in einer Datenbank speichern.  
- **Integration mit Aspose PDF** – Bilder aus PDFs extrahieren und an die OCR‑Engine übergeben.  
- **Erweiterte Sprachunterstützung** – `ocrConfig.setLanguage` zu `Language.FRENCH` oder `Language.SPANISH` wechseln für mehrsprachige Projekte.  

Probieren Sie es aus, passen Sie die Einstellungen an und sehen Sie, wie sich die Qualität für Ihren konkreten Anwendungsfall verbessert. Viel Spaß beim Programmieren, und mögen Ihre Scans stets scharf sein!  

![Diagram showing OCR workflow to recognize text from image](/images/ocr-workflow.png "recognize text from image workflow")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}