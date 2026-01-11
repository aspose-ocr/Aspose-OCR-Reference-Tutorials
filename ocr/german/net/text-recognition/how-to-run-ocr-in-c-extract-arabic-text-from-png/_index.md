---
category: general
date: 2026-01-10
description: Wie man OCR schnell ausführt und arabischen Text aus einem Bild extrahiert.
  Lernen Sie, ein Bild in Text zu konvertieren, Text aus PNG zu lesen und zu sehen,
  wie man Text mit Aspose OCR extrahiert.
draft: false
keywords:
- how to run OCR
- extract arabic text
- convert image to text
- read text from png
- how to extract text
language: de
og_description: Wie man OCR in C# ausführt und arabischen Text aus einem PNG‑Bild
  extrahiert. Dieser Leitfaden zeigt Ihnen, wie Sie ein Bild in Text umwandeln und
  Text aus einem PNG Schritt für Schritt lesen.
og_title: Wie man OCR in C# ausführt – Arabischen Text aus PNG extrahieren
tags:
- OCR
- C#
- Aspose
title: Wie man OCR in C# ausführt – Arabischen Text aus PNG extrahieren
url: /de/net/text-recognition/how-to-run-ocr-in-c-extract-arabic-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in C# ausführt – Arabischen Text aus PNG extrahieren

Haben Sie sich jemals gefragt, **wie man OCR** auf einem Bild ausführt, das arabische Zeichen enthält? Sie sind nicht allein. Viele Entwickler stoßen auf ein Problem, wenn sie **arabischen Text** aus einer PNG extrahieren müssen, aber nicht wissen, welche Bibliothek rechts‑nach‑links‑Skripte ohne Kopfschmerzen verarbeitet.  

In diesem Tutorial führen wir Sie durch alles, was Sie wissen müssen, um **Bild zu Text zu konvertieren**, **Text aus PNG zu lesen** und schließlich **wie man Text extrahiert** mit Aspose.OCR in einer sauberen C#-Konsolenanwendung. Am Ende haben Sie ein sofort ausführbares Programm, das die arabische Zeichenkette direkt in Ihrem Terminal ausgibt.

## Was Sie lernen werden

- Installieren und referenzieren Sie das Aspose.OCR NuGet-Paket.  
- Konfigurieren Sie die OCR-Engine für arabische Sprachunterstützung.  
- Laden Sie ein PNG-Bild und führen Sie den Erkennungsprozess aus.  
- Rufen Sie den extrahierten Text ab und zeigen Sie ihn an.  
- Passen Sie die Einstellungen für bessere Genauigkeit an und behandeln Sie gängige Fallstricke.  

Vorkenntnisse mit OCR sind nicht erforderlich, nur ein grundlegendes Verständnis von C# und einer .NET-Entwicklungsumgebung (Visual Studio, Rider oder die `dotnet`-CLI reichen aus).

---

## Wie man OCR ausführt – Einrichtung von Aspose OCR

### Schritt 1: Das Aspose.OCR NuGet-Paket hinzufügen

Das Erste, was wir benötigen, ist die OCR-Bibliothek selbst. Aspose.OCR ist ein kommerzielles Produkt, bietet aber eine kostenlose Testversion, die für Lernzwecke perfekt funktioniert.

```bash
# Using the .NET CLI
dotnet add package Aspose.OCR
```

Alternativ öffnen Sie den **NuGet Package Manager** in Visual Studio, suchen nach **Aspose.OCR** und klicken auf **Installieren**.

> **Profi‑Tipp:** Wenn Sie die Bibliothek in einer CI‑Pipeline verwenden möchten, fügen Sie das `-v`‑Flag hinzu, um die Version zu sperren, z. B. `dotnet add package Aspose.OCR -v 23.10`.

### Schritt 2: Ein neues Konsolenprojekt erstellen (falls Sie noch keins haben)

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
```

Jetzt haben Sie eine frische `Program.cs`-Datei, bereit für unseren Code.

---

## Arabischen Text extrahieren – Schreiben des OCR-Codes

Unten finden Sie das vollständige, sofort ausführbare Programm. Speichern Sie es als `Program.cs` (oder ersetzen Sie die automatisch generierte Datei).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Choose the language for recognition.
            // Here we use Arabic. You can swap this for
            // OcrLanguage.Korean, OcrLanguage.SerbianCyrillic, etc.
            // -------------------------------------------------
            ocrEngine.Language = OcrLanguage.Arabic;

            // -------------------------------------------------
            // Step 3: Load the image containing the text.
            // Replace the path with the location of your PNG.
            // -------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // Step 4: Run the OCR process.
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Display the extracted text.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### Warum jede Zeile wichtig ist

- **`OcrEngine`**: Die zentrale Klasse, die das Laden von Bildern, die Sprachauswahl und die Erkennung koordiniert.  
- **`Language = OcrLanguage.Arabic`**: Arabisch verwendet ein Rechts‑nach‑Links‑Schriftsystem und einzigartige Glyphen; das Setzen der Sprache weist die Engine an, die richtigen Zeichenmodelle zu verwenden.  
- **`ImageStream.FromFile`**: Unterstützt PNG, JPEG, BMP und viele weitere Formate. Wenn Sie jemals aus einem `MemoryStream` lesen müssen (z. B. eine hochgeladene Datei), ersetzen Sie diesen Aufruf entsprechend.  
- **`Recognize()`**: Führt die eigentliche Arbeit aus – Pixelanalyse, Segmentierung und Zeichenklassifizierung.  
- **`ocrEngine.Text`**: Die endgültige Unicode‑Zeichenkette, bereit für weitere Verarbeitung, Speicherung oder Anzeige.

### Erwartete Ausgabe

Wenn `arabic_sample.png` den Satz “مرحبا بالعالم” (Hello World) enthält, gibt die Konsole aus:

```
=== Extracted Arabic Text ===
مرحبا بالعالم
```

Wenn die Ausgabe verzerrt aussieht, überprüfen Sie, ob das Bild klar ist, die Sprache auf Arabisch eingestellt ist und die OCR‑Engine-Version mit der Dokumentation übereinstimmt.

---

## Bild zu Text konvertieren – Genauigkeit optimieren

Während die Standardeinstellungen für die meisten sauberen Scans funktionieren, benötigen reale Bilder oft ein wenig zusätzliche Nachbearbeitung.

| Einstellung | Was es macht | Wann zu verwenden |
|------------|--------------|-------------------|
| `ocrEngine.Config.Preprocess = true` | Aktiviert automatische Binärisierung und Rauschunterdrückung. | Gescannte Dokumente mit Schatten. |
| `ocrEngine.Config.Deskew = true` | Dreht das Bild, um leichte Neigungen zu korrigieren. | Fotos, die aus einem Winkel aufgenommen wurden. |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock` | Behandelt das gesamte Bild als einen Textblock. | Einfache Bildunterschriften oder einzeilige Beschriftungen. |
| `ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزس شصضطظعغفقكلمنهوية"` | Begrenzt die Erkennung auf arabische Zeichen. | Reduziert Fehlalarme bei mehrsprachigen Seiten. |

Sie können diese Zeilen direkt nach der Erstellung der Engine hinzufügen:

```csharp
ocrEngine.Config.Preprocess = true;
ocrEngine.Config.Deskew = true;
ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزسشصضطظعغفقكلمنهوية";
```

---

## Text aus PNG lesen – Umgang mit verschiedenen Bildquellen

Manchmal befindet sich das PNG in einer Datenbank oder stammt aus einer Webanfrage. Hier ist eine schnelle Variante, die aus einem `byte[]` liest:

```csharp
byte[] pngBytes = File.ReadAllBytes("YOUR_DIRECTORY/arabic_sample.png");
using var ms = new MemoryStream(pngBytes);
ocrEngine.Image = ImageStream.FromStream(ms);
ocrEngine.Recognize();
Console.WriteLine(ocrEngine.Text);
```

Der Rest des Ablaufs bleibt identisch, was bedeutet, dass **wie man Text extrahiert** unabhängig von der Quelle konsistent bleibt.

---

## Wie man Text extrahiert – Erweiterte Optionen & Sonderfälle

### 1. Mehrseitige PDFs oder TIFFs

Wenn Sie ein mehrseitiges Dokument OCR‑verarbeiten müssen, iterieren Sie über jede Seite:

```csharp
var pdfDoc = new Aspose.Pdf.Document("multi_page.pdf");
foreach (var page in pdfDoc.Pages)
{
    using var img = page.ConvertToImage();
    ocrEngine.Image = ImageStream.FromBitmap(img);
    ocrEngine.Recognize();
    Console.WriteLine($"Page {page.Number}: {ocrEngine.Text}");
}
```

> **Hinweis:** Für diesen Codeausschnitt benötigen Sie das `Aspose.PDF`‑Paket.

### 2. Sprache automatisch erkennen

Aspose.OCR bietet auch Auto‑Detect, ist jedoch langsamer. Wenn Sie nicht sicher sind, ob das Bild Arabisch oder ein anderes Skript enthält, aktivieren Sie es:

```csharp
ocrEngine.Language = OcrLanguage.AutoDetect;
```

Die Engine wird jedes Sprachmodell ausprobieren und das beste Ergebnis auswählen.

### 3. Leistungstipps

- **`OcrEngine`**‑Objekt für mehrere Bilder wiederverwenden; jedes Mal eine neue Instanz zu erstellen, verursacht zusätzlichen Aufwand.  
- Nur **parallel ausführen**, wenn Sie separate Engine‑Instanzen pro Thread haben – das Teilen einer Instanz führt zu Race‑Conditions.

---

## Fazit

Wir haben **wie man OCR** in C# von Anfang bis Ende behandelt und gezeigt, wie man **arabischen Text extrahiert**, **Bild zu Text konvertiert**, **Text aus PNG liest** und **wie man Text extrahiert** in verschiedenen Szenarien beantwortet. Der Beispielcode ist vollständig, eigenständig und bereit, in jedes .NET‑Konsolenprojekt eingefügt zu werden.

Nächste Schritte? Tauschen Sie `OcrLanguage.Arabic` gegen Koreanisch oder serbisches Kyrillisch aus, um die mehrsprachige Leistungsfähigkeit der Bibliothek zu sehen. Experimentieren Sie mit den Pre‑Processing‑Flags, um die Genauigkeit bei verrauschten Scans zu erhöhen, oder integrieren Sie die OCR‑Routine in eine Web‑API, sodass Benutzer Bilder hochladen und sofortige Textresultate erhalten können.

Viel Spaß beim Programmieren, und möge Ihr OCR‑Ergebnis stets kristallklar sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}