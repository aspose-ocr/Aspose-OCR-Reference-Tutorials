---
category: general
date: 2026-02-22
description: Wie man OCR in Java verwendet, um Text aus einem Bild zu extrahieren,
  die OCR‑Genauigkeit zu verbessern und ein Bild für OCR zu laden, mit praktischen
  Codebeispielen.
draft: false
keywords:
- how to use OCR
- extract text from image
- improve OCR accuracy
- load image for OCR
- OCR preprocessing
language: de
og_description: Wie man OCR in Java verwendet, um Text aus Bildern zu extrahieren
  und die OCR‑Genauigkeit zu verbessern. Folgen Sie diesem Leitfaden für ein sofort
  einsatzbereites Beispiel.
og_title: Wie man OCR in Java verwendet – Vollständige Schritt‑für‑Schritt‑Anleitung
tags:
- OCR
- Java
- Image Processing
title: Wie man OCR in Java verwendet – Vollständige Schritt‑für‑Schritt‑Anleitung
url: /de/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in Java verwendet – Vollständige Schritt‑für‑Schritt‑Anleitung

Hast du jemals **wie man OCR verwendet** auf einem schiefen Screenshot gebraucht und dich gefragt, warum die Ausgabe wie Kauderwelsch aussieht? Du bist nicht allein. In vielen realen Anwendungen – Belege scannen, Formulare digitalisieren oder Text aus Memes extrahieren – hängt das Erzielen zuverlässiger Ergebnisse von ein paar einfachen Einstellungen ab.

In diesem Tutorial gehen wir Schritt für Schritt durch **wie man OCR verwendet**, um *Text aus Bilddateien* zu extrahieren, zeigen dir, wie du **die OCR‑Genauigkeit verbessern** kannst, und demonstrieren die korrekte Art, **ein Bild für OCR zu laden** mit einer populären Java‑OCR‑Bibliothek. Am Ende hast du ein eigenständiges Programm, das du in jedes Projekt einbinden kannst.

## Was du lernen wirst

- Den genauen Code, den du brauchst, um **ein Bild für OCR zu laden** (keine versteckten Abhängigkeiten).
- Welche Vorverarbeitungs‑Flags die **OCR‑Genauigkeit verbessern** und warum sie wichtig sind.
- Wie du das OCR‑Ergebnis liest und in der Konsole ausgibst.
- Häufige Stolperfallen – wie das Vergessen, einen Interessensbereich (ROI) zu setzen oder die Rauschunterdrückung zu ignorieren – und wie du sie vermeidest.

### Voraussetzungen

- Java 17 oder neuer (der Code kompiliert mit jeder aktuellen JDK).
- Eine OCR‑Bibliothek, die die Klassen `OcrEngine`, `ImagePreprocessingOptions`, `OcrInput` und `OcrResult` bereitstellt (zum Beispiel das fiktive Paket `com.example.ocr`, das im Code‑Snippet verwendet wird). Ersetze es durch die reale Bibliothek, die du nutzt.
- Ein Beispielbild (`skewed_noisy.png`) in einem Ordner, auf den du verweisen kannst.

> **Pro‑Tipp:** Wenn du ein kommerzielles SDK nutzt, stelle sicher, dass die Lizenzdatei im Klassenpfad liegt; sonst wirft die Engine beim Initialisieren einen Fehler.

---

## Schritt 1: Eine OCR‑Engine‑Instanz erstellen – **wie man OCR effektiv verwendet**

Das Erste, was du brauchst, ist ein `OcrEngine`‑Objekt. Betrachte es als das Gehirn, das die Pixel interpretiert.

```java
// Step 1: Initialize the OCR engine
import com.example.ocr.OcrEngine;

OcrEngine ocrEngine = new OcrEngine();
```

*Warum das wichtig ist:* Ohne Engine hast du keinen Kontext für Sprachmodelle, Zeichensätze oder Bildheuristiken. Das frühe Instanziieren ermöglicht es dir, später Vorverarbeitungsoptionen anzuhängen.

---

## Schritt 2: Bildvorverarbeitung konfigurieren – **die OCR‑Genauigkeit verbessern**

Vorverarbeitung ist das Geheimrezept, das einen verrauschten Scan in sauberen, maschinenlesbaren Text verwandelt. Unten aktivieren wir Deskew, hochgradige Rauschunterdrückung, Auto‑Kontrast und einen Interessensbereich (ROI), um den relevanten Bildteil zu fokussieren.

```java
import com.example.ocr.ImagePreprocessingOptions;
import java.awt.Rectangle;

// Step 2: Set up preprocessing to improve OCR accuracy
ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
preprocessing.setDeskewEnabled(true); // Correct image rotation
preprocessing.setNoiseReductionLevel(
        ImagePreprocessingOptions.NoiseReduction.HIGH); // Reduce speckles
preprocessing.setAutoContrastEnabled(true); // Boost contrast
preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600)); // Process a sub‑region only

ocrEngine.setPreprocessingOptions(preprocessing);
```

*Warum das wichtig ist:*  
- **Deskew** richtet gedrehte Texte aus, was essenziell ist, wenn Belege nicht völlig flach gescannt werden.  
- **Rauschunterdrückung** entfernt streunende Pixel, die sonst als Zeichen interpretiert würden.  
- **Auto‑Kontrast** erweitert den Tonumfang, sodass schwache Buchstaben hervortreten.  
- **ROI** weist die Engine an, irrelevante Ränder zu ignorieren, was Zeit und Speicher spart.

Wenn du irgendeinen dieser Schritte überspringst, wirst du wahrscheinlich einen Rückgang der **OCR‑Genauigkeit** feststellen.

---

## Schritt 3: Das Bild für OCR laden – **ein Bild für OCR korrekt laden**

Jetzt zeigen wir der Engine, welche Datei sie lesen soll. Die Klasse `OcrInput` kann mehrere Bilder akzeptieren, aber für dieses Beispiel halten wir es einfach.

```java
import com.example.ocr.OcrInput;

// Step 3: Load the image you want to extract text from
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png"); // replace with your real path
```

*Warum das wichtig ist:* Der Pfad muss absolut oder relativ zum Arbeitsverzeichnis sein; sonst wirft die Engine eine `FileNotFoundException`. Beachte außerdem, dass der Methodenname `add` darauf hinweist, dass du mehrere Bilder in die Warteschlange stellen kannst – praktisch für Batch‑Verarbeitung.

---

## Schritt 4: OCR ausführen und den erkannten Text ausgeben – **wie man OCR end‑to‑end verwendet**

Schließlich lassen wir die Engine den Text erkennen und geben ihn aus. Das `OcrResult`‑Objekt enthält den Roh‑String, Vertrauenswerte und Zeilen‑Metadata (falls du sie später brauchst).

```java
import com.example.ocr.OcrResult;

// Step 4: Run OCR and print the extracted text
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Erwartete Ausgabe** (unter der Annahme, dass das Beispielbild „Hello, OCR World!“ enthält):

```
=== OCR Output ===
Hello, OCR World!
```

Sieht das Ergebnis verzerrt aus, gehe zurück zu Schritt 2 und passe die Vorverarbeitungsoptionen an – vielleicht die Rauschunterdrückungsstufe senken oder das ROI‑Rechteck anpassen.

---

## Vollständiges, ausführbares Beispiel

Unten findest du ein komplettes Java‑Programm, das du in eine Datei namens `OcrDemo.java` kopieren kannst. Es verbindet alle besprochenen Schritte.

```java
// OcrDemo.java – A complete, runnable example showing how to use OCR in Java
import com.example.ocr.OcrEngine;
import com.example.ocr.ImagePreprocessingOptions;
import com.example.ocr.OcrInput;
import com.example.ocr.OcrResult;
import java.awt.Rectangle;

public class OcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing (this is the key to improve OCR accuracy)
        ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
        preprocessing.setDeskewEnabled(true);
        preprocessing.setNoiseReductionLevel(
                ImagePreprocessingOptions.NoiseReduction.HIGH);
        preprocessing.setAutoContrastEnabled(true);
        preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600));
        ocrEngine.setPreprocessingOptions(preprocessing);

        // 3️⃣ Load the image you want to extract text from
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace the path with your own image location
        ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run the OCR engine and print the result
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Speichere die Datei, kompiliere sie mit `javac OcrDemo.java` und führe `java OcrDemo` aus. Wenn alles korrekt eingerichtet ist, wird der extrahierte Text in der Konsole angezeigt.

---

## Häufige Fragen & Sonderfälle

| Frage | Antwort |
|----------|--------|
| **Was, wenn mein Bild im JPEG‑Format vorliegt?** | Die Methode `OcrInput.add()` akzeptiert jedes unterstützte Rasterformat – PNG, JPEG, BMP, TIFF. Ändere einfach die Dateierweiterung im Pfad. |
| **Kann ich mehrere Seiten gleichzeitig verarbeiten?** | Absolut. Rufe `ocrInput.add()` für jede Datei auf und übergebe dann denselben `ocrInput` an `recognize()`. Die Engine liefert ein zusammengefügtes `OcrResult`. |
| **Was, wenn das OCR‑Ergebnis leer ist?** | Prüfe, ob das ROI tatsächlich Text enthält. Stelle außerdem sicher, dass `setDeskewEnabled(true)` aktiviert ist; eine 90°‑Drehung lässt die Engine das Bild für leer halten. |
| **Wie ändere ich das Sprachmodell?** | Die meisten Bibliotheken bieten eine Methode `setLanguage(String)` auf `OcrEngine`. Rufe sie vor `recognize()` auf, z. B. `ocrEngine.setLanguage("eng")`. |
| **Gibt es eine Möglichkeit, Vertrauenswerte zu erhalten?** | Ja, `OcrResult` liefert häufig `getConfidence()` pro Zeile oder Zeichen. Nutze das, um Ergebnisse mit niedriger Vertrauenswürdigkeit zu filtern. |

---

## Fazit

Wir haben **wie man OCR in Java** von Anfang bis Ende behandelt: die Engine erstellen, die Vorverarbeitung konfigurieren, um die **OCR‑Genauigkeit zu verbessern**, das **Bild korrekt für OCR laden** und schließlich den extrahierten Text ausgeben. Der komplette Code‑Snippet ist einsatzbereit, und die Erklärungen beantworten das „Warum“ hinter jeder Zeile.

Bereit für den nächsten Schritt? Probiere, das ROI‑Rechteck zu ändern, um andere Bildbereiche zu fokussieren, experimentiere mit `NoiseReduction.MEDIUM` oder integriere die Ausgabe in ein durchsuchbares PDF. Du kannst auch verwandte Themen wie **Text aus Bild extrahieren** mit Cloud‑Diensten erkunden oder tausende Dateien mit einer multithread‑basierten Warteschlange stapelweise verarbeiten.

Hast du weitere Fragen zu OCR, Bildvorverarbeitung oder Java‑Integration? Hinterlasse einen Kommentar – happy coding!

![How to use OCR example](/images/ocr-demo.png "wie man OCR – Java‑Beispiel mit Vorverarbeitung und Ergebnis")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}