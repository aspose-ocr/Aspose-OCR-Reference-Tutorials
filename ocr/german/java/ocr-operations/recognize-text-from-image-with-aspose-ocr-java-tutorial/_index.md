---
category: general
date: 2026-02-17
description: Erfahren Sie, wie Sie Text aus einem Bild erkennen und ein Bild für OCR
  mit der Aspose OCR Java‑Bibliothek laden. Schritt‑für‑Schritt‑Anleitung mit Rechtschreibkorrektur.
draft: false
keywords:
- recognize text from image
- load image for OCR
- Aspose OCR Java
- spell corrector OCR
- OCR engine setup
language: de
og_description: Texterkennung aus Bildern mit Aspose OCR Java. Dieses Tutorial zeigt,
  wie man ein Bild für OCR lädt, die Rechtschreibkorrektur aktiviert und bereinigten
  Text ausgibt.
og_title: Text aus Bild erkennen – Vollständiger Aspose OCR Java Leitfaden
tags:
- Java
- OCR
- Aspose
title: Text aus Bild mit Aspose OCR erkennen – Java‑Tutorial
url: /de/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild mit Aspose OCR erkennen – Java‑Tutorial

Haben Sie jemals **Text aus Bild erkennen** müssen, waren sich aber nicht sicher, welche Bibliothek Sie wählen sollen? Sie sind nicht allein. In vielen realen Projekten – denken Sie an das Scannen von Rechnungen, das Digitalisieren handschriftlicher Notizen oder das Extrahieren von Bildunterschriften aus Screenshots – ist das Erzielen genauer OCR‑Ergebnisse entscheidend.  

In diesem Leitfaden führen wir Sie durch das Laden eines Bildes für OCR, das Aktivieren des integrierten Rechtschreibkorrektors von Aspose OCR und schließlich das Ausgeben des bereinigten Textes. Am Ende haben Sie ein sofort ausführbares Java‑Programm, das **Text aus Bild erkennt** mit nur wenigen Codezeilen.

## Was dieses Tutorial abdeckt

- Wie Sie Ihre Aspose OCR‑Lizenz anwenden (damit die Demo ohne Wasserzeichen läuft)  
- Erstellen einer `OcrEngine`‑Instanz und Auswahl von Englisch als Erkennungssprache  
- **Bild für OCR laden** using `OcrInput` and point it at a PNG that contains misspelled words  
- Aktivieren des Rechtschreibkorrektors, optional mit Verweis auf ein benutzerdefiniertes Wörterbuch  
- Durchführen der Erkennung und Ausgeben des korrigierten Ergebnisses  

Keine externen Dienste, keine versteckten Konfigurationsdateien – nur reines Java und das Aspose OCR‑JAR.

> **Profi‑Tipp:** Wenn Sie neu bei Aspose sind, holen Sie sich eine kostenlose 30‑Tage‑Testlizenz von der Aspose‑Website und legen Sie die `.lic`‑Datei in einen Ordner, den Sie in Ihrem Code referenzieren können.

## Voraussetzungen

- Java 8 oder neuer (der Code kompiliert auch mit JDK 11)  
- Aspose.OCR für Java JAR in Ihrem Klassenpfad  
- Eine gültige `Aspose.OCR.lic`‑Datei (oder Sie können im Evaluierungsmodus laufen, aber die Demo fügt ein Wasserzeichen ein)  
- Eine Bilddatei (`misspelled.png`), die Text mit absichtlichen Rechtschreibfehlern enthält – perfekt, um den Rechtschreibkorrektor in Aktion zu sehen  

Alles vorhanden? Großartig – lassen Sie uns eintauchen.

## Schritt 1: Ihre Aspose OCR‑Lizenz anwenden

Bevor die Engine irgendeine schwere Arbeit übernimmt, muss sie wissen, dass Sie lizenziert sind. Andernfalls erhalten Sie ein „Trial version“-Banner in der Ausgabe.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – replace the path with where you stored your .lic file
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

*Warum das wichtig ist:* Die Lizenzierung deaktiviert das Testwasserzeichen und schaltet das vollständige Wörterbuch des Rechtschreibkorrektors frei. Das Überspringen dieses Schrittes funktioniert, aber Ihre Ausgabe wird mit dem Text „Aspose OCR Demo“ verschmutzt.

## Schritt 2: Die OCR‑Engine erstellen und konfigurieren

Jetzt starten wir die Engine und geben ihr an, welche Sprache verwendet werden soll. Englisch ist am häufigsten, aber Aspose unterstützt Dutzende.

```java
        // Step 2: Instantiate the OCR engine
        OcrEngine engine = new OcrEngine();

        // Choose English for recognition – you could pick French, German, etc.
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);
```

*Warum wir die Sprache festlegen:* Das Sprachmodell bestimmt den Zeichensatz und beeinflusst die Vorschläge des Rechtschreibkorrektors. Die falsche Sprache zu verwenden kann die Genauigkeit drastisch verringern.

## Schritt 3: Rechtschreibkorrektur aktivieren und (optional) auf ein benutzerdefiniertes Wörterbuch verweisen

Aspose OCR wird mit einem integrierten englischen Wörterbuch geliefert, aber Sie können Ihr eigenes bereitstellen, wenn Sie domänenspezifische Begriffe haben (denken Sie an medizinischen Jargon oder Produktcodes).

```java
        // Step 3: Turn on the spell corrector
        engine.getSpellCorrector().setEnable(true); // activate spell‑checking

        // Optional: use a custom dictionary folder
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english");
```

*Was der Korrektor macht:* Wenn die OCR‑Engine ein Wort findet, das nicht im Wörterbuch steht, versucht sie, es durch die nächstgelegene Übereinstimmung zu ersetzen. Deshalb kann die Demo „recieve“ automatisch in „receive“ umwandeln.

## Schritt 4: Bild für OCR laden

Hier ist der Teil, der direkt **Bild für OCR laden** beantwortet. Wir erstellen ein `OcrInput`‑Objekt und fügen unsere PNG‑Datei hinzu.

```java
        // Step 4: Prepare the image input
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // path to the image you want to process
```

*Warum wir `OcrInput` verwenden:* Es abstrahiert die Dateileselogik und ermöglicht es Ihnen, später mehrere Seiten hinzuzufügen, falls Sie ein mehrseitiges PDF oder eine Reihe von Bildern verarbeiten müssen.

## Schritt 5: Die Erkennung ausführen und korrigierten Text abrufen

Die Engine übernimmt jetzt die schwere Arbeit – sie erkennt Zeichen, wendet das Sprachmodell an und korrigiert schließlich die Rechtschreibung.

```java
        // Step 5: Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Step 6: Output the corrected text to the console
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

*Erwartete Ausgabe:* Angenommen, `misspelled.png` enthält den Satz „Ths is a smple test“, dann gibt die Konsole aus:

```
Corrected text:
This is a simple test
```

Beachten Sie, wie die falsch geschriebenen Wörter (`Ths`, `smple`) automatisch korrigiert wurden.

## Vollständiges, sofort ausführbares Beispiel

Unten finden Sie das gesamte Programm in einem Block. Kopieren‑einfügen, passen Sie die Pfade an und klicken Sie auf **Run**.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose.OCR license (replace with your license file)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Select the language for recognition (e.g., English)
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);

        // Enable the built‑in spell corrector and optionally set a custom dictionary
        engine.getSpellCorrector().setEnable(true);                     // activate spell‑checking
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english"); // optional

        // Prepare the input image containing the text to be recognized
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // load image for OCR

        // Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Output the corrected text
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

**Tipp:** Wenn Sie ein JPEG oder BMP anstelle von PNG verarbeiten möchten, ändern Sie einfach die Dateierweiterung – Aspose OCR unterstützt alle gängigen Rasterformate.

## Häufige Fragen & Sonderfälle

- **Was ist, wenn mein Bild eine niedrige Auflösung hat?**  
  Erhöhen Sie die DPI, bevor Sie es an Aspose übergeben, indem Sie es mit einer Bibliothek wie `java.awt.Image` neu skalieren. Höhere DPI geben der Engine mehr Pixel zum Arbeiten, was normalerweise die Genauigkeit verbessert.

- **Kann ich mehrere Sprachen im selben Bild erkennen?**  
  Ja. Rufen Sie `engine.getLanguage().setLanguage(OcrLanguage.MULTI_LANGUAGE);` auf und geben Sie optional eine Liste von Sprachen über `engine.getLanguage().addLanguage(OcrLanguage.SPANISH);` an.

- **Mein benutzerdefiniertes Wörterbuch wird nicht verwendet – warum?**  
  Stellen Sie sicher, dass der Ordner Textdateien mit einem Wort pro Zeile enthält und dass der Pfad absolut oder korrekt relativ zu Ihrem Arbeitsverzeichnis ist.

- **Wie extrahiere ich Vertrauenswerte?**  
  `result.getConfidence()` gibt einen Float zwischen 0 und 1 für die gesamte Seite zurück. Für Vertrauenswerte pro Zeichen schauen Sie sich `result.getWordList()` an.

## Fazit

Sie wissen jetzt, wie Sie **Text aus Bild erkennen** mit Aspose OCR für Java, wie Sie **Bild für OCR laden** und wie Sie den Rechtschreibkorrektor aktivieren, um gängige Tippfehler zu bereinigen. Das obige vollständige Beispiel kann in jedes Maven‑ oder Gradle‑Projekt eingefügt werden, und mit wenigen Anpassungen können Sie es skalieren, um Ordner stapelweise zu verarbeiten, es in einen Web‑Service einzubinden oder es in ein Dokumenten‑Management‑System zu integrieren.

Bereit für den nächsten Schritt? Versuchen Sie, ein mehrseitiges PDF zu verarbeiten, experimentieren Sie mit einem benutzerdefinierten Wörterbuch für branchenspezifische Terminologie oder leiten Sie die Ausgabe an eine Übersetzungs‑API weiter. Die Möglichkeiten sind endlos, und das Kernmuster – Lizenz → Engine → Sprache → Rechtschreibkorrektor → Eingabe → Erkennung → Ausgabe – bleibt gleich.

Viel Spaß beim Programmieren, und möge Ihre OCR‑Ergebnisse stets punktgenau sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}