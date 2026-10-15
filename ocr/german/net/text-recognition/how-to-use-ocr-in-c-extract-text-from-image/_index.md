---
category: general
date: 2026-03-05
description: Wie man OCR in C# verwendet, um Text aus einem Bild zu extrahieren. Lernen
  Sie, ein Bild in Text zu konvertieren, koreanische Zeichen zu lesen und ein Bild
  schnell für OCR zu laden.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert image to text
- read korean characters
- load image for OCR
language: de
og_description: Wie man OCR in C# verwendet und sofort Text aus einem Bild extrahiert.
  Dieser Leitfaden zeigt, wie man ein Bild in Text umwandelt, koreanische Zeichen
  liest und ein Bild für OCR lädt.
og_title: Wie man OCR in C# verwendet – Text aus Bild extrahieren
tags:
- OCR
- C#
- Aspose
title: Wie man OCR in C# verwendet – Text aus Bild extrahieren
url: /de/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in C# verwendet – Text aus Bild extrahieren

Haben Sie sich jemals gefragt **wie man OCR verwendet**, wenn Sie einen Screenshot voller koreanischer Texte haben und die reine Zeichenkette zurück benötigen? Sie sind nicht der Einzige, der darüber nachdenkt. In diesem Tutorial führen wir Sie durch ein komplettes, sofort ausführbares Beispiel, das **Text aus Bild extrahiert**, **Bild in Text umwandelt** und Ihnen sogar zeigt, wie man **koreanische Zeichen** mit Aspose.OCR **liest**.

Wir behandeln außerdem den oft übersehenen Schritt des **Ladens von Bildern für OCR**, damit Sie später nicht von einer „Datei nicht gefunden“-Überraschung überrascht werden. Am Ende haben Sie ein eigenständiges Programm, das Sie in jedes .NET‑Projekt einbinden können.

## Was Sie benötigen

- .NET 6+ (oder .NET Framework 4.7.2 und höher) – der Code funktioniert in beiden.
- Aspose.OCR für .NET – Sie können eine kostenlose Testversion von der Aspose-Website herunterladen.
- Ein Beispielbild (`korean_doc.png`), das koreanischen Text enthält.
- Ihre bevorzugte IDE (Visual Studio, Rider, VS Code – was immer Sie mögen).

Keine weiteren Drittanbieter‑Bibliotheken sind erforderlich.

## Schritt 1: Projekt einrichten und Aspose.OCR hinzufügen

Zuerst erstellen Sie eine neue Konsolenanwendung:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Fügen Sie dann das Aspose.OCR NuGet‑Paket hinzu:

```bash
dotnet add package Aspose.OCR
```

> **Pro Tipp:** Wenn Sie eine Lizenzdatei haben, platzieren Sie sie im Projektstammverzeichnis; andernfalls funktioniert die kostenlose Testversion, fügt dem Ergebnis jedoch ein Wasserzeichen hinzu.

## Schritt 2: Wie man OCR verwendet – Engine initialisieren

Jetzt schreiben wir den C#‑Code. Das Erste, was man tun muss, wenn man **wie man OCR verwendet**, ist, die `OcrEngine` zu instanziieren. Dieses Objekt ist das Herz der Bibliothek; es enthält alle Einstellungen, die Sie später benötigen.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: apply your license to remove trial limitations
            // Replace the path with the actual location of your .lic file
            ocrEngine.SetLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Warum das wichtig ist:** Ohne eine ordnungsgemäße Engine‑Instanz können Sie keine Sprache festlegen, Bilder laden oder Ergebnisse abrufen. Die Engine verwaltet außerdem interne Ressourcen, sodass das einmalige Erstellen und Wiederverwenden effizienter ist, als wiederholt neue Objekte zu konstruieren.

## Schritt 3: Sprache auswählen – Koreanische Zeichen lesen

Die nächste Zeile teilt der Engine mit, nach welcher Sprache gesucht werden soll. Da unser Ziel ist, **koreanische Zeichen zu lesen**, setzen wir `OcrLanguage.Korean`. Sie können dies je nach Anwendungsfall gegen Arabisch, Thailändisch, Gujarati usw. austauschen.

```csharp
            // Step 3: Tell the engine which language to recognize
            ocrEngine.Language = OcrLanguage.Korean; // alternatives: Arabic, Thai, Gujarati, etc.
```

**Warum das wichtig ist:** Die Sprachauswahl verbessert die Genauigkeit erheblich. Die OCR‑Engine verwendet sprachspezifische Wörterbücher und Zeichenmodelle; die falsche Sprache zu verwenden kann zu unleserlichen Ausgaben führen.

## Schritt 4: Bild für OCR laden – Bild in Text umwandeln

Bevor die Engine arbeiten kann, müssen Sie **Bild für OCR laden**. Die Methode `ImageStream.FromFile` liest die Datei in ein Format, das die Engine versteht.

```csharp
            // Step 4: Load the image that contains the text
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/korean_doc.png");
```

Wenn sich das Bild in einem anderen Ordner befindet, passen Sie einfach den Pfad an. Denken Sie daran, die *Build Action* der Datei auf „Copy if newer“ zu setzen, damit die ausführbare Datei sie zur Laufzeit finden kann.

> **Häufiges Problem:** Wenn Sie einen Pfad mit Backslashes (`\`) in einem String‑Literal angeben, ohne sie zu escapen, führt das zu einem Kompilierfehler. Verwenden Sie entweder doppelte Backslashes (`\\`) oder einen wörtlichen String (`@"C:\\path\\file.png"`).

## Schritt 5: OCR ausführen – Text aus Bild extrahieren

Jetzt wird die eigentliche Arbeit erledigt. Der Aufruf von `Recognize()` führt den OCR‑Algorithmus aus, und die Eigenschaft `Text` liefert Ihnen die rohe Zeichenkette.

```csharp
            // Step 5: Run OCR and get the recognized text
            string recognizedText = ocrEngine.Recognize().Text;
```

An diesem Punkt haben Sie **Text aus Bild extrahiert** und effektiv **Bild in Text umgewandelt**. Das Ergebnis kann Zeilenumbrüche enthalten, wenn das ursprüngliche Layout Zeilenumbrüche hatte.

## Schritt 6: Ergebnis anzeigen – Ausgabe überprüfen

Zum Schluss geben wir das Ergebnis in der Konsole aus, damit Sie überprüfen können, ob es funktioniert hat.

```csharp
            // Step 6: Output the result to the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

Programm ausführen:

```bash
dotnet run
```

### Erwartete Ausgabe

```
=== Recognized Text ===
안녕하세요. 이것은 OCR 테스트 문서입니다.
```

Wenn Sie koreanische Zeichen sehen, die dem Bild ähneln, herzlichen Glückwunsch – Sie haben **wie man OCR verwendet** mit Aspose.OCR gemeistert!

![Beispiel für die Verwendung von OCR](image.png)

*Bild-Alt-Text: Beispiel‑Diagramm zur Verwendung von OCR, das den Ablauf vom Laden eines Bildes bis zum Ausdrucken des erkannten Textes zeigt.*

## Randfälle & Variationen

### 1. Mehrere Seiten verarbeiten

Wenn Sie **Text aus Bild**‑Dateien extrahieren müssen, die mehrere Seiten enthalten (z. B. ein mehrseitiges TIFF), iterieren Sie über jede Seite und rufen `Recognize()` für jede `ImageStream`‑Instanz auf.

### 2. Umgang mit niedrig‑qualitativen Scans

Bilder mit niedriger Auflösung können die Genauigkeit beeinträchtigen. Vor dem Aufruf von `Recognize()` können Sie das Bild mit den Vorverarbeitungs‑Tools von Aspose verbessern:

```csharp
ocrEngine.Image = ImageProcessing.Preprocess(ocrEngine.Image, ImageProcessingOptions.Deskew);
```

### 3. Sprachen zur Laufzeit wechseln

Angenommen, Sie haben ein Dokument mit gemischten Sprachen. Sie können `ocrEngine.Language` zwischen den Erkennungen ändern:

```csharp
ocrEngine.Language = OcrLanguage.English;
string english = ocrEngine.Recognize().Text;

ocrEngine.Language = OcrLanguage.Korean;
string korean = ocrEngine.Recognize().Text;
```

### 4. Ergebnis in einer Datei speichern

Wenn Sie lieber **Bild in Text umwandeln** und speichern möchten, schreiben Sie die Zeichenkette einfach in eine `.txt`‑Datei:

```csharp
System.IO.File.WriteAllText("output.txt", recognizedText);
```

## Häufig gestellte Fragen

- **Benötige ich eine Lizenz, um diesen Code auszuführen?**  
  Nein. Die kostenlose Testversion funktioniert gut für Experimente, fügt dem Ergebnis jedoch ein Wasserzeichen hinzu. Eine gekaufte Lizenz entfernt das Wasserzeichen und schaltet die volle Leistung frei.

- **Kann ich das unter Linux verwenden?**  
  Absolut. Aspose.OCR ist plattformübergreifend; stellen Sie lediglich sicher, dass Sie die erforderlichen nativen Abhängigkeiten haben (libgdiplus für .NET Core unter Linux).

- **Was ist, wenn mein Bild in einem Stream statt einer Datei vorliegt?**  
  Verwenden Sie `ImageStream.FromStream(yourStream)` – die API akzeptiert jeden `System.IO.Stream`.

## Fazit

Wir haben Sie Schritt für Schritt durch **wie man OCR verwendet** in C# geführt, um **Text aus Bild zu extrahieren**, **Bild in Text umzuwandeln** und **koreanische Zeichen zu lesen**, während wir **Bild für OCR laden**. Das komplette, ausführbare Beispiel oben sollte sofort funktionieren, und die zusätzlichen Tipps bieten Ihnen einen Leitfaden für fortgeschrittenere Szenarien.

Bereit für die nächste Herausforderung? Versuchen Sie, eine andere Sprache zu verwenden, PDFs Seite für Seite zu verarbeiten oder den OCR‑Aufruf in eine Web‑API zu integrieren, sodass Benutzer Bilder hochladen und sofortige Textergebnisse erhalten können. Die Möglichkeiten sind endlos, und Sie haben nun ein solides Fundament zum Weiterbauen.

Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}