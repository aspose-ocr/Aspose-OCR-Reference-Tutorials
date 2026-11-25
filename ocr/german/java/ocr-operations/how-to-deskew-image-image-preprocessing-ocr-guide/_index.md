---
category: general
date: 2026-06-22
description: 'Wie man ein Bild für OCR entkippelt: Bildvorverarbeitungsschritte für
  OCR erlernen, Salz‑und‑Pfeffer‑Rauschen entfernen und die Genauigkeit steigern.'
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: de
og_description: Wie man ein Bild für OCR entneigt, Salz‑und‑Pfeffer‑Rauschen entfernt
  und Bildvorverarbeitungs‑OCR‑Techniken in einem vollständigen Java‑Beispiel anwendet.
og_title: Wie man ein Bild entzerrt – Leitfaden zur Bildvorverarbeitung für OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: 'How to deskew image for OCR: learn image preprocessing OCR steps,
    remove salt pepper noise, and boost accuracy.'
  headline: How to Deskew Image – Image Preprocessing OCR Guide
  type: TechArticle
tags:
- OCR
- image-processing
- Java
title: Wie man ein Bild entzerrt – Leitfaden zur Bildvorverarbeitung für OCR
url: /de/java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein Bild entneigt – Bildvorverarbeitung OCR Leitfaden

Haben Sie sich jemals gefragt, **wie man ein Bild entneigt**, damit Ihre OCR‑Engine den Text tatsächlich liest? Sie sind nicht der Einzige. Ein schräg gescannter Scan kann ein perfektes Dokument in ein wirres Durcheinander verwandeln, und die meisten Entwickler stoßen mindestens einmal darauf.

In diesem Tutorial führen wir Sie durch eine vollständige **image preprocessing OCR**‑Pipeline, die nicht nur die Drehung korrigiert, sondern auch **remove[s] salt pepper**‑Artefakte entfernt und den Kontrast erhöht – im Grunde alles, was Sie benötigen, um **preprocess images OCR**‑artig vorzubereiten, bevor Sie sie an die Engine übergeben. Am Ende haben Sie ein sofort ausführbares Java‑Snippet und ein klares mentales Modell, warum jeder Schritt wichtig ist.

## Wie man ein Bild entneigt – Aufbau der Vorverarbeitungspipeline

Das Herzstück jedes OCR‑freundlichen Workflows ist ein **preprocess options**‑Objekt, das eine Reihe von Filtern hintereinander schaltet. Stellen Sie sich das wie ein Förderband vor: Jeder Filter erledigt eine Aufgabe und gibt das Bild dann an den nächsten weiter. Unten finden Sie ein minimales, aber vollständiges Beispiel, das eine hypothetische OCR‑Bibliothek verwendet, die `DeskewFilter`, `DenoiseFilter` und `ContrastBoostFilter` bereitstellt.

```java
import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.DeskewFilter;
import com.example.ocr.filters.DenoiseFilter;
import com.example.ocr.filters.ContrastBoostFilter;

/**
 * Demonstrates how to deskew image and apply common OCR preprocessing steps.
 */
public class OcrPreprocessDemo {

    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine (replace with your actual implementation)
        Engine engine = new Engine();

        // 2️⃣ Build the preprocessing pipeline
        ImagePreprocessOptions preprocessOptions = new ImagePreprocessOptions();

        // 2a️⃣ Deskew – correct rotation up to ±15°
        preprocessOptions.addFilter(new DeskewFilter(15));

        // 2b️⃣ Denoise – remove salt‑and‑pepper noise
        preprocessOptions.addFilter(new DenoiseFilter());

        // 2c️⃣ Contrast boost – make low‑contrast scans more readable
        preprocessOptions.addFilter(new ContrastBoostFilter(1.5f));

        // 3️⃣ Attach the pipeline to the engine
        engine.setPreprocessOptions(preprocessOptions);

        // 4️⃣ Run OCR on a sample image
        String result = engine.recognizeText("sample-scanned-page.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== OCR RESULT ===");
        System.out.println(result);
    }
}
```

### Warum das funktioniert

* **DeskewFilter** analysiert die dominanten Textzeilen des Bildes, schätzt den Winkel und dreht das Bitmap wieder horizontal. Die meisten Bibliotheken begrenzen die Korrektur auf ±15°, weil größere Winkel meist auf eine schlecht gescannte Seite hinweisen, die manuell nachbearbeitet werden muss.
* **DenoiseFilter** zielt auf das klassische *salt‑and‑pepper*-Muster ab – isolierte schwarze oder weiße Pixel, die wie Störgeräusche auf einem Fernseher aussehen. Das Entfernen verhindert, dass die OCR‑Engine Rauschen mit Zeichen verwechselt.
* **ContrastBoostFilter** dehnt das Histogramm aus und lässt schwache Striche hervorstechen. Ein Multiplikator von `1.5f` ist ein sicherer Standard; Sie können ihn erhöhen, wenn Ihre Scans besonders ausgewaschen sind.

> **Pro Tipp:** Wenn Sie wissen, dass Ihre Dokumente nie mehr als 10° schräg sind, übergeben Sie diesen kleineren Grenzwert an `DeskewFilter` – der Algorithmus läuft schneller und korrigiert weniger stark.

## Image Preprocessing OCR: Filter in der richtigen Reihenfolge hinzufügen

Die Reihenfolge ist wichtig. Stellen Sie sich vor, Sie entfernen das Rauschen *vor* dem Entneigen; das Rauschen könnte die Winkelerkennung verfälschen und zu einem falsch ausgerichteten Ergebnis führen. Umgekehrt stellt das Anwenden von Kontrastverstärkung *nach* dem Entneigen sicher, dass die Drehung keine neuen Artefakte einführt.

Unten finden Sie eine schnelle Checkliste, die Sie in jedes Projekt kopieren können:

| Schritt | Filter | Grund |
|------|--------|--------|
| 1 | `DeskewFilter` | Richtet die Textgrundlinie aus |
| 2 | `DenoiseFilter` | Entfernt isoliertes Pixelrauschen |
| 3 | `ContrastBoostFilter` | Verbessert die Lesbarkeit für OCR |

Wenn Sie zusätzliche Schritte einfügen müssen – zum Beispiel einen **binarization**‑Filter für binäres OCR – würden Sie ihn **nach** der Kontrastverstärkung einfügen, weil ein sauberes, hochkontrastiertes Bild genauer binarisiert.

## Salz‑und‑Pfeffer‑Rauschen mit DenoiseFilter entfernen

Salt‑and‑pepper‑Rauschen ist berüchtigt bei Scans von geringer Qualität, besonders bei solchen von günstigen Handykameras. Der `DenoiseFilter` in unserer Bibliothek implementiert einen Median‑Filter‑Kernel, der jedes Pixel durch den Median seiner Umgebung ersetzt. Der Effekt? Diese Punkte verschwinden, ohne die eigentlichen Zeichen zu verwischen.

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*Wann die Kernelgröße erhöhen?* Wenn Ihre Quellbilder von großen Punkten übersät sind, wird ein größerer Kernel sie bereinigen, aber Vorsicht: Ist er zu groß, könnten feine Striche in winzigen Schriften gelöscht werden.

## Preprocess Images OCR – Anwendung der Pipeline

Sobald Sie die Filterkette zusammengestellt haben, ist das Anbinden an die Engine ein Einzeiler (`engine.setPreprocessOptions`). Ab diesem Moment wird jeder Aufruf von `recognizeText` automatisch durch die Pipeline geleitet. Es ist nicht nötig, jeden Filter manuell aufzurufen – Ihr Code bleibt übersichtlich, und zukünftige Änderungen (Hinzufügen eines neuen Filters, Anpassen von Parametern) sind zentralisiert.

So sieht ein erfolgreicher Durchlauf mit einem Beispiel‑Scan aus, der ursprünglich eine 12°‑Neigung und deutliches Pfefferrauschen hatte:

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Beachten Sie, wie der Text sauber, korrekt ausgerichtet und frei von fremden Zeichen ist, die sonst als „I n v o i c e“ oder „$‑‑‑“ erschienen wären.

## Randfälle & häufige Stolperfallen

| Situation | Worauf zu achten ist | Empfohlene Lösung |
|-----------|----------------------|-------------------|
| Rotation > 15° | DeskewFilter gibt möglicherweise auf | Manuell vorrotieren oder einen Filter mit größerem Bereich verwenden |
| Extrem niedrige Auflösung ( < 100 dpi ) | Kontrastverstärkung kann Details nicht wiederherstellen | Bild zuerst neu sampeln (z. B. `ResampleFilter`) |
| Gemischtes Rauschen (Gaussian + salt‑pepper) | DenoiseFilter allein reicht nicht | Einen `GaussianBlurFilter` vor dem `DenoiseFilter` verketten |
| Farbscans mit farbigem Text | Graustufen‑Umwandlung nötig | `GrayscaleFilter` vor der Kontrastverstärkung einfügen |

Wenn Sie diese Szenarien antizipieren, sparen Sie später Stunden an Fehlersuche.

## Vollständiges funktionierendes Beispiel (Alles‑in‑einem)

Unten finden Sie eine eigenständige Java‑Klasse, die Sie in jedes Maven‑ oder Gradle‑Projekt einbinden können, das die `com.example.ocr`‑Abhängigkeit enthält. Sie demonstriert **how to deskew image**, **remove salt pepper**‑Rauschen und **preprocess images OCR**‑artig.

```java
package com.myapp.demo;

import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.*;

public class CompleteOcrPipeline {

    public static void main(String[] args) {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine (replace with your own)
        // -------------------------------------------------
        Engine engine = new Engine();

        // -------------------------------------------------
        // 2️⃣ Configure preprocessing pipeline
        // -------------------------------------------------
        ImagePreprocessOptions options = new ImagePreprocessOptions();

        // Deskew up to ±15° – the core of "how to deskew image"
        options.addFilter(new DeskewFilter(15));

        // Remove salt‑and‑pepper artifacts
        options.addFilter(new DenoiseFilter());

        // Boost contrast by 1.5× to aid OCR recognition
        options.addFilter(new ContrastBoostFilter(1.5f));

        // (Optional) Convert to grayscale – often improves OCR accuracy
        options.addFilter(new GrayscaleFilter());

        // Attach the pipeline
        engine.setPreprocessOptions(options);

        // -------------------------------------------------
        // 3️⃣ Perform OCR on a test file
        // -------------------------------------------------
        String imagePath = "src/main/resources/scanned-document.png";
        String text = engine.recognizeText(imagePath);

        // -------------------------------------------------
        // 4️⃣ Show the result
        // -------------------------------------------------
        System.out.println("=== OCR RESULT ===");
        System.out.println(text);
    }
}
```

**Erwartete Ausgabe** (unter der Annahme, dass `scanned-document.png` eine klare Rechnung enthält):

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

Wenn Sie das Bild durch eines ersetzen, das bereits perfekt ausgerichtet ist, werden Sie feststellen, dass die Pipeline weiterhin läuft – es bricht nichts, und die OCR‑Genauigkeit bleibt hoch.

## Fazit

Sie haben nun ein solides Verständnis von **how to deskew image** und warum jeder Vorverarbeitungsschritt – **image preprocessing OCR**, **remove salt pepper** und **preprocess images OCR** – eine entscheidende Rolle dabei spielt, sauberen, durchsuchbaren Text zu liefern. Das obige Beispiel ist ein vollständiges,

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man AspOCR verwendet: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Skew‑Winkel für OCR‑Bildvorverarbeitung berechnen](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [Wie man den Schwellenwert in OCR‑Bilderkennung festlegt](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}