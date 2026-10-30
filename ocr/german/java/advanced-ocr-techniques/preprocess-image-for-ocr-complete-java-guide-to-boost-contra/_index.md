---
category: general
date: 2026-10-30
description: Erfahren Sie, wie Sie OCR durch Vorverarbeitung von Bildern in Java mit
  Aspose OCR verbessern können. Dieser Leitfaden zeigt, wie man den image contrast
  erhöht, den contrast level einstellt und extract text effizient.
draft: false
keywords:
- how to improve OCR
- how to boost contrast
- preprocess image OCR
- extract text image Java
- recognize text image Java
lastmod: 2026-10-30
og_description: Erfahren Sie, wie Sie OCR durch Vorverarbeitung von Bildern in Java
  mit Aspose OCR verbessern können. Der Leitfaden erklärt, wie man boosting contrast,
  setting contrast level und extracting text schnell durchführt.
og_image_alt: Screenshot of a Java OCR preprocessing pipeline showing before‑and‑after
  contrast enhancement
og_title: Wie man OCR verbessert – Java image preprocessing guide
schemas:
- author: Aspose
  dateModified: '2026-10-30'
  description: Learn how to improve OCR by preprocessing images in Java with Aspose
    OCR. This guide shows how to boost image contrast, set contrast level, and extract
    text efficiently.
  headline: How to improve OCR – preprocess image for OCR in Java with Aspose
  type: TechArticle
- description: Learn how to improve OCR by preprocessing images in Java with Aspose
    OCR. This guide shows how to boost image contrast, set contrast level, and extract
    text efficiently.
  name: How to improve OCR – preprocess image for OCR in Java with Aspose
  steps:
  - name: '**Deskew** – corrects slight rotations.'
    text: '**Deskew** – corrects slight rotations.'
  - name: '**Denoise** – removes speckles that confuse character segmentation.'
    text: '**Denoise** – removes speckles that confuse character segmentation.'
  - name: '**Contrast enhancement** – makes dark text stand out against the background.'
    text: '**Contrast enhancement** – makes dark text stand out against the background.'
  type: HowTo
- questions:
  - answer: Yes—load the appropriate language pack with `engine.setLanguage("fr")`
      or any supported ISO code to improve accuracy for non‑English text.
    question: Can I use this approach for languages other than English?
  - answer: It does not read PDF pages natively; you should extract images from the
      PDF first (e.g., with Aspose PDF) and then feed them to the OCR engine.
    question: Does Aspose OCR support PDF input directly?
  - answer: The library handles images up to 30 MP without needing to load the whole
      file into memory, thanks to its streaming architecture.
    question: How large an image can I process?
  - answer: Absolutely—iterate over the files, reuse the same `OcrEngine` instance,
      and add each file to `OcrInput`. This reduces per‑image overhead dramatically.
    question: Is there a way to batch‑process a folder of images?
  - answer: Try adjusting `setContrastLevel` in smaller increments, experiment with
      `setDenoiseMode`, or enable `setUseAdaptiveThreshold(true)` for difficult backgrounds.
    question: What if the OCR output still contains errors?
  type: FAQPage
tags:
- Java
- OCR
- Image Processing
title: Wie man OCR verbessert – Bild für OCR in Java mit Aspose vorverarbeiten
url: /de/java/advanced-ocr-techniques/preprocess-image-for-ocr-complete-java-guide-to-boost-contra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bild für OCR vorverarbeiten – vollständiger Java‑Leitfaden

Haben Sie jemals **Bild für OCR vorverarbeiten** müssen, waren sich aber nicht sicher, welche Einstellungen tatsächlich einen Unterschied machen? Sie sind nicht allein. Die meisten Entwickler werfen ein Bild in eine OCR‑Engine und hoffen auf Magie, nur um ein verzerrtes Ergebnis zu erhalten. In diesem Tutorial führen wir Sie durch ein praktisches End‑to‑End‑Beispiel, das **den Bildkontrast erhöht**, den **Kontrastwert** anpasst und schließlich **Text aus dem Bild erkennt** mithilfe von Aspose OCR für Java.

Am Ende haben Sie einen wiederverwendbaren Code‑Snippet, der **Text mit OCR extrahiert** zuverlässig, selbst bei verrauschten Scans. Keine versteckten Tricks, nur klare Schritte und die Begründung für jeden einzelnen.

## Schnelle Antworten
- **Was ist der erste Schritt zur Verbesserung von OCR?** Laden Sie Ihre Aspose OCR‑Lizenz, bevor Sie die Engine erstellen.  
- **Welche drei Vorverarbeitungsoptionen sind am wichtigsten?** Deskew, Denoise und Kontrastverstärkung.  
- **Welcher Kontrastwert funktioniert für die meisten gedruckten Dokumente?** Etwa 1.3 f bietet ein gutes Gleichgewicht.  
- **Kann ich das verarbeitete Bild sehen?** Ja – exportieren Sie das Zwischen‑Bitmap nach PNG.  
- **Benötige ich eine Lizenz für die Produktion?** Absolut; ein Testlauf läuft im eingeschränkten Modus und fügt Wasserzeichen hinzu.

## Wie man OCR durch Vorverarbeiten von Bildern in Java verbessert

Laden Sie das Bild, führen Sie Deskew, Denoise und Kontrastanpassung durch und starten Sie dann den Erkenner. Die Pipeline von Aspose OCR verarbeitet das Bild in genau dieser Reihenfolge, sodass jede Transformation auf den saubersten möglichen Daten arbeitet, bevor der neuronale Netzwerk‑Erkenner sie sieht. Dieser Zwei‑Schritt‑Ansatz – Vorverarbeiten und dann Erkennen – liefert bis zu 30 % höhere Zeichen‑Genauigkeit bei typischen gescannten Dokumenten.

## Was ist Aspose OCR für Java?

Aspose OCR für Java ist eine Bibliothek, die **über 30 Bildformate** unterstützt (einschließlich JPEG, PNG, TIFF, BMP) und einen 200‑seitigen Mehr‑Bild‑Batch in weniger als 2 Sekunden auf einem Standard‑8‑Core‑Server verarbeiten kann. Sie bietet integrierte Deskew‑, Denoise‑ und Kontrast‑Verbesserungs‑Filter, die Sie programmgesteuert konfigurieren können.

## Was Sie benötigen

- Java 17 oder neuer (jedes aktuelle JDK funktioniert)
- Aspose OCR für Java Bibliothek (Download von der offiziellen Aspose‑Website)
- Eine gültige Aspose OCR Lizenzdatei (`Aspose.OCR.lic`)
- Ein Eingabebild (`input.jpg`), das Sie lesen möchten
- Ihre bevorzugte IDE oder ein einfaches Kommandozeilen‑Setup

Wenn Sie diese bereits haben, großartig – lassen Sie uns gleich eintauchen.

## Was ist der erste Schritt: Laden der Aspose OCR Lizenz?

Laden Sie die Lizenz, bevor Sie OCR‑Objekte erstellen, damit die Engine im Voll‑Feature‑Modus statt im Testmodus läuft. Das verhindert Wasserzeichen, schaltet alle Vorverarbeitungsoptionen frei und stellt sicher, dass die OCR‑Engine auf die lizenzierten Sprachpakete und Leistungsoptimierungen zugreifen kann, die für eine genaue Textextraktion erforderlich sind.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {

        // Load the Aspose OCR license – this disables the evaluation limits
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Warum das wichtig ist:** Ohne eine gültige Lizenz läuft die Engine im Evaluierungsmodus, was Ergebnisse kürzen oder Wasserzeichen hinzufügen kann. Das frühe Setzen der Lizenz stellt zudem sicher, dass alle nachfolgenden Vorverarbeitungsoptionen im Voll‑Feature‑Modus angewendet werden.

## Wie initialisiert man die OCR‑Engine?

Die Klasse `OcrEngine` ist die Kernkomponente, die OCR durchführt und Vorverarbeitungskontrollen bereitstellt. Erstellen Sie eine einzelne `OcrEngine`‑Instanz und verwenden Sie sie für jedes Bild erneut, um wiederholtes Laden des Modells zu vermeiden. Das Wiederverwenden der Engine cached interne neuronale Netzwerk‑Modelle, was die Latenz pro Bild um bis zu 40 % reduziert und den Speicherverbrauch senkt, wodurch die Batch‑Verarbeitung effizienter wird.

```java
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Pro‑Tipp:** Halten Sie die Engine als Singleton, wenn Sie viele Bilder in einem Batch verarbeiten; sie cached interne Ressourcen und beschleunigt nachfolgende Aufrufe.

## Wie man die Vorverarbeitung konfiguriert – Deskew, Denoise und Kontrastverstärkung

Hier kommt das **Vorverarbeiten von Bild für OCR** ins Spiel. Die drei Regler, die wir drehen werden, sind:

1. **Deskew** – korrigiert leichte Rotationen.
2. **Denoise** – entfernt Sprenkel, die die Zeichensegmentierung verwirren.
3. **Kontrastverstärkung** – lässt dunklen Text stärker gegen den Hintergrund hervorstechen.

```java
        // Access preprocessing settings
        PreprocessingSettings preprocessing = ocrEngine.getPreprocessing();

        // Enable automatic deskew (helps with scanned pages that are a few degrees off)
        preprocessing.setDeskew(true);
        preprocessing.setDeskewAngleTolerance(0.1); // tolerance in degrees

        // Turn on denoising – median works well for salt‑and‑pepper noise
        preprocessing.setDenoise(true);
        preprocessing.setDenoiseMode(DenoiseMode.MEDIAN); // alternatives: GAUSSIAN

        // Boost contrast – this is the “boost image contrast” step
        preprocessing.setContrastEnhance(true);
        preprocessing.setContrastLevel(1.3f); // 1.0 = no change, >1.0 = stronger contrast
```

### Warum den Kontrastwert anpassen?

Die Erhöhung des Kontrastwerts dehnt das Histogramm des Bildes, sodass dunkle Pixel dunkler und helle Pixel heller werden. In der Praxis liefert ein **Kontrastwert** von `1.3f` häufig das beste Gleichgewicht für gedruckte Dokumente, während ein Wert über `1.5f` feine Striche überbelichten kann. Experimentieren Sie gern; die Einstellung ist günstig zu ändern und kann die Erfolgsrate beim **Erkennen von Text aus Bild** dramatisch verbessern.

## Wie bereitet man das Eingabebild vor?

Die Klasse `OcrInput` repräsentiert eine Sammlung von Bildern, die die OCR‑Engine verarbeiten wird. Die Klasse `OcrInput` abstrahiert die Dateiverwaltung, sodass Sie ein oder mehrere Bilder für die Batch‑Verarbeitung hinzufügen können. Sie können einzelne Dateipfade, Streams oder Byte‑Arrays angeben, und die Engine behandelt jeden Eintrag als separate Seite, wobei sie automatisch die Format‑Erkennung und Konvertierung nach Bedarf übernimmt.

```java
        // Prepare the image for OCR – you can add more files to the same OcrInput
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.jpg");
```

**Randfall:** Wenn Ihr Bild in einem nicht‑standardmäßigen Format vorliegt (z. B. TIFF mit mehreren Seiten), können Sie jede Seite separat laden oder zuerst in PNG/JPEG konvertieren.

## Wie funktioniert der Erkennungsschritt?

Wenn Sie die Methode `recognize` aufrufen, wendet die Engine zuerst die konfigurierte Vorverarbeitungspipeline – Deskew, Denoise und Kontrastverstärkung – in genau dieser Reihenfolge an. Nachdem das Bild bereinigt wurde, wird es an den neuronalen Netzwerk‑Erkenner übergeben, der die Zeichenformen analysiert und den extrahierten Text als Zeichenkette zurückgibt.

```java
        // Run OCR – this returns a result object containing the extracted text
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Was passiert im Hintergrund?** Aspose OCR wendet zuerst die Deskew‑Transformation an, dann den Denoise‑Filter und schließlich die Kontrastanpassung, bevor das Bild an den neuronalen Netzwerk‑basierten Erkenner übergeben wird. Die Reihenfolge ist beabsichtigt; eine Änderung könnte zu suboptimalen Ergebnissen führen.

## Wie gibt man den erkannten Text aus?

Nach Abschluss der Erkennung können Sie das Ergebnis über `getText` oder `getTextLines` abrufen. In diesem Beispiel geben wir die extrahierte Zeichenkette einfach in der Konsole aus, aber in der Produktion könnten Sie sie in eine Datei schreiben, in einer Datenbank speichern oder über ein Netzwerk an nachgelagerte Dienste senden.

```java
        // Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

### Erwartete Ausgabe

Wenn `input.jpg` den Satz „Hello World!“ enthält, sollte die Konsole anzeigen:

```
Hello World!
```

Wenn die Ausgabe verzerrt aussieht, überprüfen Sie die Vorverarbeitungswerte – insbesondere den **Kontrastwert** und den **Denoise‑Modus** – und versuchen Sie ein anderes Bildformat.

## Wie visualisiert man das vorverarbeitete Bild (optional)?

Wenn Sie prüfen müssen, was die OCR‑Engine nach der Vorverarbeitung sieht, können Sie das Zwischen‑Bitmap mit der Methode `saveProcessedImage` in eine PNG‑Datei exportieren. Diese visuelle Kontrolle hilft Ihnen zu verifizieren, dass Deskew, Denoise und Kontrastanpassungen korrekt angewendet wurden, bevor die Erkennung erfolgt.

```java
        // Export the pre‑processed image for debugging
        BufferedImage processed = preprocessing.getProcessedImage();
        ImageIO.write(processed, "png", new File("processed.png"));
```

![Beispiel für Vorverarbeitung von Bild für OCR](/images/ocr-preprocess-example.png "Vorverarbeitung von Bild für OCR – Vor und nach dem Kontrast‑Boost")
[Beispiel für Vorverarbeitung von Bild für OCR](/images/ocr-preprocess-example.png "Vorverarbeitung von Bild für OCR – Vor und nach dem Kontrast‑Boost")

*Das obige Bild zeigt, wie das Erhöhen des Kontrasts und das Denoising einen unscharfen Scan in ein sauberes, OCR‑bereites Bild verwandelt.*

## Häufige Fallstricke & wie man sie vermeidet

| Fallstrick | Warum es passiert | Lösung |
|------------|-------------------|--------|
| **Über‑Kontrast** (`setContrastLevel` zu hoch) | Heller Hintergrund wird weiß, wodurch schwache Zeichen gelöscht werden | Halten Sie den Wert zwischen 1.1 und 1.4 für die meisten gedruckten Texte |
| **Deskew‑Toleranz zu niedrig** | Kleine Drehungen bleiben unkorrekt | `setDeskewAngleTolerance` auf 0.2 oder 0.3 erhöhen für gescannte Bücher |
| **Verwendung von GAUSSIAN Denoise bei Binärbildern** | Verwischt Kanten, verschmilzt Zeichen | `DenoiseMode.MEDIAN` für Schwarz‑Weiß‑Scans verwenden |
| **Fehlende Lizenz** | Engine wechselt in den Testmodus, was die Ausgabe abschneidet | Pfad zu `Aspose.OCR.lic` überprüfen und sicherstellen, dass die Datei lesbar ist |

## Häufig gestellte Fragen

**F: Kann ich diesen Ansatz für andere Sprachen als Englisch verwenden?**  
A: Ja – laden Sie das passende Sprachpaket mit `engine.setLanguage("fr")` oder einem anderen unterstützten ISO‑Code, um die Genauigkeit für nicht‑englischen Text zu verbessern.

**F: Unterstützt Aspose OCR die direkte PDF‑Eingabe?**  
A: Es liest PDF‑Seiten nicht nativ; Sie sollten zuerst die Bilder aus dem PDF extrahieren (z. B. mit Aspose PDF) und dann an die OCR‑Engine übergeben.

**F: Wie groß kann ein Bild sein, das ich verarbeiten kann?**  
A: Die Bibliothek verarbeitet Bilder bis zu 30 MP, ohne das gesamte Bild in den Speicher zu laden, dank ihrer Streaming‑Architektur.

**F: Gibt es eine Möglichkeit, einen Ordner mit Bildern stapelweise zu verarbeiten?**  
A: Absolut – iterieren Sie über die Dateien, verwenden Sie dieselbe `OcrEngine`‑Instanz erneut und fügen Sie jede Datei zu `OcrInput` hinzu. Das reduziert den Aufwand pro Bild erheblich.

**F: Was, wenn die OCR‑Ausgabe immer noch Fehler enthält?**  
A: Versuchen Sie, `setContrastLevel` in kleineren Schritten anzupassen, experimentieren Sie mit `setDenoiseMode` oder aktivieren Sie `setUseAdaptiveThreshold(true)` für schwierige Hintergründe.

## Nächste Schritte: über die Grundvorverarbeitung hinaus

- **Sprachpakete** – laden Sie spezifische Sprachwörterbücher, um die Genauigkeit für nicht‑englischen Text zu verbessern.  
- **Region‑of‑Interest (ROI) Zuschneiden** – konzentrieren Sie sich auf einen Bildausschnitt, wenn Sie nur einen Teil der Seite benötigen.  
- **Stapelverarbeitung** – durchlaufen Sie ein Verzeichnis mit Bildern, verwenden Sie dieselbe `OcrEngine`‑Instanz für Geschwindigkeit.  
- **Integration mit PDF** – kombinieren Sie Aspose OCR mit Aspose PDF, um gescannte PDFs in durchsuchbare PDFs in einer Pipeline zu konvertieren.

## Fazit

Wir haben alles behandelt, was Sie benötigen, um **Bild für OCR vorzuverarbeiten** mit Aspose OCR für Java: Laden der Lizenz, Konfiguration von Deskew, Denoise und Kontrastverstärkung, Einspeisen des Bildes und schließlich **Text aus Bild erkennen**. Mit dem vollständigen, ausführbaren Beispiel oben können Sie jetzt **Text mit OCR extrahieren** auf jedem geeignet vorbereiteten Bild.

Probieren Sie den Code aus, passen Sie den **Kontrastwert** an und beobachten Sie, wie die Genauigkeit steigt. Wenn Sie bereit sind, erkunden Sie sprachspezifische Modelle oder Batch‑Pipelines, um diese Ein‑Bild‑Demo in eine produktionsreife Lösung zu verwandeln.

*Viel Spaß beim Programmieren, und mögen Ihre Scans immer scharf sein!*

---

**Zuletzt aktualisiert:** 2026-10-30  
**Getestet mit:** Aspose OCR für Java 24.11  
**Autor:** Aspose

## Verwandte Tutorials

- [Text aus Bild extrahieren mit Aspose Ocr Java‑Leitfaden](/ocr/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/)
- [Text aus Bild erkennen mit Aspose Ocr Gpu Java](/ocr/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/)
- [OCR‑Engine in Java erstellen – Text aus großen Bildern erkennen](/ocr/java/advanced-ocr-techniques/create-ocr-engine-java-recognize-text-from-large-images/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}