---
category: general
date: 2026-03-13
description: Wie man OCR in C# durchführt und Text aus einem Bild mit OcrEngine extrahiert.
  Lernen Sie, Bilder schnell in Text umzuwandeln, mit einer vollständigen Schritt‑für‑Schritt‑Anleitung.
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- read text from picture
- how to extract text
language: de
og_description: Wie führt man OCR in C# durch? Dieser Leitfaden zeigt Ihnen, wie Sie
  Text aus einem Bild extrahieren, ein Bild in Text umwandeln und Text aus einem Bild
  mit OcrEngine lesen.
og_title: Wie man OCR in C# durchführt – Text aus Bild extrahieren
tags:
- OCR
- C#
- Image Processing
title: Wie man OCR in C# ausführt – Text aus einem Bild extrahieren
url: /de/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in C# durchführt – Text aus Bild extrahieren

Wie man OCR in C# durchführt, ist eine häufige Frage für Entwickler, die **Text aus Bild**‑Dateien lesen müssen. In diesem Leitfaden zeigen wir Ihnen, wie Sie Text aus einem Bild mit der `OcrEngine`‑Bibliothek extrahieren und Bilder mit nur wenigen Codezeilen in durchsuchbare Zeichenketten umwandeln.  

Wenn Sie jemals auf einer gescannten Rechnung, einer handschriftlichen Notiz oder einem Screenshot gestarrt haben und sich gefragt haben *„Wie extrahiere ich Text?“*, dann sind Sie hier richtig. Wir gehen auch darauf ein, wie man Bild‑zu‑Text für die Stapelverarbeitung konvertiert, sodass Sie den gesamten Arbeitsablauf automatisieren können.

---

## Was Sie benötigen

- **.NET 6.0 oder höher** (die von uns verwendete API funktioniert mit .NET Standard 2.0+)
- Das **OcrEngine** NuGet‑Paket (oder jede kompatible OCR‑Bibliothek, die die Eigenschaften `Language`, `Image`, `Recognize` und `Text` bereitstellt)
- Eine Beispiel‑Bilddatei, z. B. `hindi_page.jpg`, in einem Ordner, den Sie im Code referenzieren können
- Grundlegendes Verständnis der C#‑Syntax – keine fortgeschrittenen Tricks erforderlich

Das ist alles. Keine externen Dienste, keine API‑Schlüssel, nur eine lokale Bibliothek, die die schwere Arbeit übernimmt.

---

## Schritt‑für‑Schritt‑Implementierung

Im Folgenden zerlegen wir den Prozess in logische Abschnitte. Jeder Abschnitt hat eine klare Überschrift, ein kurzes Code‑Snippet und eine Erklärung, **warum** der Schritt wichtig ist – nicht nur **was** er tut.

### Wie man OCR durchführt – Kernschritte

Der gesamte Ablauf lässt sich in fünf Aktionen zusammenfassen:

1. **Erstellen** Sie eine OCR‑Engine‑Instanz
2. **Wählen** Sie die Sprache, die Sie erkennen möchten
3. **Laden** Sie das Bild, das den Text enthält
4. **Führen** Sie den Erkennungsalgorithmus aus
5. **Lesen** Sie den extrahierten Text

Das ist das Grundgerüst; die folgenden Abschnitte füllen es aus.

---

### Text aus Bild extrahieren – Engine erstellen

Zuerst benötigen wir ein Objekt, das mit der OCR‑Engine kommunizieren kann.

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

*Warum das wichtig ist:* Das Instanziieren von `OcrEngine` reserviert alle internen Puffer und lädt alle nativen DLLs, die für die Bildanalyse benötigt werden. Wenn Sie diesen Schritt überspringen, haben Sie später keinen Erkenner, den Sie aufrufen können.

> **Pro‑Tipp:** Wenn Sie vorhaben, viele Bilder nacheinander zu verarbeiten, behalten Sie dieselbe `ocrEngine`‑Instanz bei. Sie wiederverwendet Sprachmodelle und beschleunigt nachfolgende Aufrufe.

---

### Bild zu Text konvertieren – Sprache auswählen

Die OCR‑Genauigkeit hängt stark vom Sprachmodell ab, das Sie ihr geben. Für Hindi, Tamil oder jede andere Schrift setzen Sie die Eigenschaft `Language` entsprechend.

```csharp
// Step 2: Select the language of the text to recognize (e.g., Hindi)
ocrEngine.Language = Language.Hindi;   // You can also use Language.Tamil, Language.English, etc.
```

*Warum das wichtig ist:* Die Engine verwendet sprachspezifische Zeichensätze und statistische Modelle. Die Angabe einer falschen Sprache führt häufig zu fehlerhaften Ausgaben, besonders bei nicht‑lateinischen Schriften.

> **Sonderfall:** Wenn Sie Mehrsprachen‑Unterstützung benötigen, erlauben einige Bibliotheken das Setzen einer Ausweichliste, z. B. `ocrEngine.Language = Language.Multilingual;`.

---

### Text aus Bild lesen – Quellbild laden

Jetzt richten wir die Engine auf die Datei, die den visuellen Text enthält.

```csharp
// Step 3: Load the image that contains the text
ocrEngine.Image = ImageStream.FromFile(@"C:\OCR\Samples\hindi_page.jpg");
```

*Warum das wichtig ist:* `ImageStream.FromFile` konvertiert die Rohdatei in ein Bitmap‑Format, das der OCR‑Kern verstehen kann. Das Bereitstellen einer beschädigten oder nicht unterstützten Datei (wie SVG) führt zu einer Ausnahme.

> **Achtung:** Große Bilder können viel Speicher verbrauchen. Wenn Sie hochauflösende Scans verarbeiten, sollten Sie sie vor dem Übergabe an die Engine mit `Image.Resize` verkleinern.

---

### Bild zu Text konvertieren – Erkennung ausführen

Mit der bereitstehenden Engine und dem geladenen Bild rufen wir schließlich den OCR‑Prozess auf.

```csharp
// Step 4: Perform the OCR operation
ocrEngine.Recognize();
```

*Warum das wichtig ist:* `Recognize` löst eine Reihe interner Schritte aus – Vorverarbeitung, Segmentierung, Zeichenklassifizierung und Nachverarbeitung. Der Aufruf ist blockierend, das heißt, der Thread wartet, bis der Text fertig ist.

> **Leistungshinweis:** Auf einem typischen Desktop dauert das Erkennen einer 300 dpi‑Seite < 1 Sekunde. Auf einem Server sollten Sie dies in einer Hintergrundaufgabe ausführen, um UI‑Einbrüche zu vermeiden.

---

### Wie man Text extrahiert – Ergebnis abrufen

Sobald die Erkennung abgeschlossen ist, speichert die Engine die reine Textausgabe in der Eigenschaft `Text`.

```csharp
// Step 5: Output the recognized text
Console.WriteLine(ocrEngine.Text);
```

*Warum das wichtig ist:* Die Eigenschaft `Text` liefert Ihnen eine saubere UTF‑8‑Zeichenkette, die Sie in eine Datei schreiben, in eine Datenbank einspeisen oder an nachgelagerte NLP‑Pipelines weitergeben können.

> **Erwartete Ausgabe:** Für die Beispiel‑Hindi‑Seite könnte etwas wie  
> `यह एक उदाहरण पाठ है जो OCR द्वारा पहचाना गया है।`  
> (Die genaue Ausgabe hängt von Bildqualität und Sprachmodell ab.)

---

## Zusätzliche Überlegungen für reale Projekte

Im Folgenden finden Sie einige „Was‑wenn“‑Szenarien, denen Sie wahrscheinlich begegnen, wenn Sie in der Produktion **Text aus Bild extrahieren** wollen.

### Mehrere Bilder in einer Schleife verarbeiten

Wenn Sie **Bild zu Text konvertieren** für Dutzende von Dateien benötigen, verpacken Sie die Schritte in eine `foreach`‑Schleife und verwenden dieselbe `ocrEngine` erneut:

```csharp
string[] files = Directory.GetFiles(@"C:\OCR\Batch\", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    ocrEngine.Recognize();
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), ocrEngine.Text);
}
```

### Umgang mit minderwertigen Scans

- **Vorverarbeiten** mit Binarisierung (`Image.Binarize()`), Rauschunterdrückung oder Entzerrung.
- **DPI erhöhen** beim Scannen (300 dpi ist ein sicherer Ausgangspunkt).
- **Ein Sprachmodell wählen**, das die Ligaturen der Schrift unterstützt (z. B. Devanagari für Hindi).

### Text aus Bild im Web lesen

Wenn das Bild von einer URL stammt, laden Sie es zuerst in einen Memory‑Stream herunter:

```csharp
using (HttpClient client = new())
{
    byte[] data = await client.GetByteArrayAsync(imageUrl);
    using var ms = new MemoryStream(data);
    ocrEngine.Image = ImageStream.FromStream(ms);
    ocrEngine.Recognize();
    Console.WriteLine(ocrEngine.Text);
}
```

### Thread‑Sicherheit und Parallelität

Die meisten OCR‑Bibliotheken sind **nicht** von Haus aus thread‑sicher. Wenn Sie **Text aus Bild** gleichzeitig lesen wollen, starten Sie separate `OcrEngine`‑Instanzen pro Thread oder verwenden eine Producer‑Consumer‑Warteschlange, um den Zugriff zu serialisieren.

---

## Vollständiges funktionierendes Beispiel

Wenn wir alles zusammenfügen, erhalten Sie eine sofort ausführbare Konsolen‑App, die **wie man OCR durchführt**, **Text aus Bild extrahiert** und **Text aus Bild liest** in einem zusammenhängenden Programm demonstriert.

```csharp
using System;
using OcrLibrary;               // Adjust to your OCR library's namespace
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Choose the language (Hindi in this case)
        ocrEngine.Language = Language.Hindi;

        // Load the image file
        string imagePath = @"C:\OCR\Samples\hindi_page.jpg";
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }

        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // Run the recognition process
        ocrEngine.Recognize();

        // Output the extracted text
        string result = ocrEngine.Text;
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(result);

        // Optional: Save to a .txt file
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, result);
        Console.WriteLine($"Text saved to {txtPath}");
    }
}
```

**Was Sie sehen sollten:** Die Konsole gibt den aus `hindi_page.jpg` extrahierten Hindi‑Satz aus, gefolgt von einer Bestätigung, dass die Textdatei erstellt wurde. Wenn das Bild sauber ist, wird die Ausgabe praktisch identisch zum originalen gedruckten Text sein.

---

## Fazit

Sie wissen jetzt, **wie man OCR** in C# von Anfang bis Ende durchführt, wie man **Text aus Bild extrahiert**, **Bild zu Text konvertiert** und **Text aus Bild liest** mit einem einfachen `OcrEngine`‑Workflow. Das Fünf‑Schritte‑Muster – erstellen, Sprache setzen, laden, erkennen, lesen – deckt die meisten Anwendungsfälle ab, und die zusätzlichen Tipps helfen Ihnen, Stapelaufgaben, minderwertige Scans und webbasierte Quellen zu bewältigen.

Bereit für die nächste Herausforderung? Versuchen Sie, die Sprache auf Englisch zu wechseln, eine als Bild gerenderte PDF‑Seite zu verarbeiten oder die OCR‑Ausgabe in eine Such‑Index‑Pipeline zu integrieren. Der Himmel ist die Grenze, sobald Sie die Grundlagen von OCR in C# beherrschen.

Haben Sie Fragen oder ein kniffliges Bild, das nicht mitmacht? Hinterlassen Sie unten einen Kommentar, und wir lösen das Problem gemeinsam. Viel Spaß beim Coden!  

![Beispiel für OCR durchführen](images/ocr-example.png "Beispiel für OCR durchführen")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}