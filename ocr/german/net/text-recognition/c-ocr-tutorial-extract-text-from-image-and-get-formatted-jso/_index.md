---
category: general
date: 2026-01-13
description: C# OCR‑Tutorial, das zeigt, wie man Text aus einem Bild extrahiert, ein
  Bild für OCR lädt und die JSON‑Ausgabe mit Aspose OCR formatiert. Lernen Sie, ein
  Objekt in JSON zu serialisieren.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- format json output
- serialize object to json
- load image for ocr
language: de
og_description: c# OCR‑Tutorial, das Sie Schritt für Schritt durch das Extrahieren
  von Text aus einem Bild, das Laden des Bildes für OCR und das Formatieren der JSON‑Ausgabe
  mit Aspose OCR führt.
og_title: C# OCR‑Tutorial – Text extrahieren & JSON formatieren
tags:
- OCR
- C#
- JSON
title: C# OCR‑Tutorial – Text aus Bild extrahieren und formatierte JSON erhalten
url: /de/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-get-formatted-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Text aus Bild extrahieren und JSON‑Ausgabe formatieren

Haben Sie sich jemals gefragt, wie man **Text aus Bild**‑Dateien in einem C#‑Projekt extrahiert, ohne sich mit pixel­niedrigem Processing herumzuschlagen? Genau das löst dieses *c# ocr tutorial*. In nur wenigen Minuten sehen Sie, wie man **Bild für OCR lädt**, Aspose OCR ausführt und **JSON‑Ausgabe formatiert**, sodass Sie die Daten direkt in Ihre API oder Datenbank einspeisen können.

Wir gehen jede Codezeile durch, erklären, warum jedes Stück wichtig ist, und zeigen Ihnen sogar das genaue JSON, das Sie erwarten sollten. Am Ende haben Sie eine sofort lauffähige Konsolen‑App, die ein Rechnungs‑PNG in sauberes, eingerücktes JSON verwandelt. Kein Schnickschnack, nur eine praktische Lösung, die Sie in jedes .NET 6+‑Projekt einbinden können.

## Was dieses c# ocr tutorial abdeckt

- Installation des Aspose.OCR‑NuGet‑Pakets  
- Laden einer Bilddatei für die OCR‑Verarbeitung  
- Erkennen von englischem Text (oder jeder unterstützten Sprache)  
- **Serialisieren des OCR‑Ergebnisses zu JSON** mit Pretty‑Printing  
- Anzeige des JSON in der Konsole und optionales Speichern  

Sie benötigen nur ein Grundverständnis von C# und ein aktuelles .NET‑SDK. Mehr nicht. Wenn Sie neugierig sind, **Text aus Bild**‑Dateien für Rechnungen, Quittungen oder gescannte Formulare zu extrahieren, lesen Sie weiter.

---

## Schritt 1: Umgebung für das c# ocr tutorial einrichten

Bevor Sie Code schreiben, stellen Sie sicher, dass Sie die richtigen Werkzeuge haben:

1. **.NET 6 SDK oder neuer** – Sie können es von der Microsoft‑Website herunterladen.  
2. **Visual Studio 2022** (Community funktioniert einwandfrei) oder ein beliebiger Editor Ihrer Wahl.  
3. **Aspose.OCR NuGet‑Paket** – führen Sie `dotnet add package Aspose.OCR` im Projektordner aus.

> **Pro‑Tipp:** Wenn Sie eine CI‑Pipeline verwenden, fügen Sie den Paket‑Verweis zu Ihrer `.csproj`‑Datei hinzu, damit der Build das Paket automatisch wiederherstellt.

---

## Schritt 2: Bild für OCR laden

Der erste eigentliche Schritt in unserem Tutorial ist, das Bild zu holen, das Sie verarbeiten möchten. Aspose OCR arbeitet mit gängigen Formaten wie PNG, JPEG und TIFF.

```csharp
using Aspose.OCR;
using System.Text.Json;

// Replace this with the actual path to your invoice image
string imagePath = @"C:\Invoices\invoice.png";

// Create an OcrImage instance from the file system
OcrImage inputImage = OcrImage.FromFile(imagePath);
```

> **Warum das wichtig ist:** Das Laden des Bildes als `OcrImage` gibt der Engine Zugriff auf die Bitmap‑Daten und eventuelle DPI‑Informationen, was die Erkennungsgenauigkeit verbessert. Das Überspringen dieses Schritts oder das Bereitstellen einer beschädigten Datei führt zu einer Laufzeit‑Exception.

---

## Schritt 3: Text aus Bild extrahieren

Jetzt führen wir die OCR‑Engine tatsächlich aus. Die Methode `Recognize` liefert ein reichhaltiges `OcrResult`‑Objekt zurück, das den Rohtext, Konfidenzwerte und Layout‑Details enthält.

```csharp
// Initialize the OCR engine – no license needed for a trial run
OcrEngine ocrEngine = new OcrEngine();

// Recognize English text (you can change the language enum if needed)
OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);
```

> **Randfall:** Wenn Sie ein mehrsprachiges Dokument verarbeiten müssen, rufen Sie `Recognize` zweimal mit unterschiedlichen `OcrLanguage`‑Werten auf und verketten die Ergebnisse. Die Engine ist thread‑sicher, sodass Sie große Stapel sogar parallelisieren können.

---

## Schritt 4: Objekt zu JSON serialisieren – JSON‑Ausgabe formatieren

Das `OcrResult`‑Objekt ist eine einfache C#‑Klasse, das bedeutet, wir können es an `System.Text.Json` übergeben. Durch Aktivieren von `WriteIndented` wird die Ausgabe menschenlesbar.

```csharp
// Serialize the OCR result with pretty printing
string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
{
    WriteIndented = true
});
```

> **Was Sie erhalten:** Einen schön eingerückten JSON‑String, der den erkannten Text, die Konfidenz und das Seitenlayout enthält. Perfekt für Logging, das Senden an einen Webservice oder das Speichern in einer NoSQL‑Datenbank.

---

## Schritt 5: Formatiertes JSON anzeigen und (optional) speichern

Zum Schluss geben wir das JSON in der Konsole aus. Sie können es auch mit `File.WriteAllText` in eine Datei schreiben, wenn Sie möchten.

```csharp
// Show the JSON in the console
Console.WriteLine(json);

// Optional: Save to a .json file next to the image
string jsonPath = Path.ChangeExtension(imagePath, ".json");
File.WriteAllText(jsonPath, json);
Console.WriteLine($"\nJSON saved to: {jsonPath}");
```

**Erwartete Konsolenausgabe (gekürzt für Übersicht):**

```json
{
  "Text": "Invoice #12345\nDate: 2025‑12‑01\nTotal: $250.00",
  "Confidence": 0.97,
  "Pages": [
    {
      "PageNumber": 1,
      "Blocks": [
        {
          "Text": "Invoice #12345",
          "Confidence": 0.99,
          "Rectangle": { "X": 50, "Y": 30, "Width": 200, "Height": 30 }
        }
        // …more blocks…
      ]
    }
  ]
}
```

Wenn die OCR‑Engine keinen Text findet, ist das Feld `Text` ein leerer String und `Confidence` ist `0`. Das ist ein gutes Signal, die Bildqualität zu überprüfen.

---

## Schritt 6: Vollständiges funktionierendes Beispiel

Alles zusammengefügt, hier das komplette Programm, das Sie in eine neue Konsolen‑App kopieren‑und‑einfügen können:

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonResultDemo
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the source image (replace with your own path)
        string imagePath = @"C:\Invoices\invoice.png";
        OcrImage inputImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Recognize text – this is the core of our c# ocr tutorial
        OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);

        // 4️⃣ Serialize the result with pretty formatting
        string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
        {
            WriteIndented = true
        });

        // 5️⃣ Output to console and optionally write to a file
        Console.WriteLine(json);
        string jsonPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"\nJSON saved to: {jsonPath}");
    }
}
```

Führen Sie das Programm aus (`dotnet run` im Projektordner) und beobachten Sie, wie die Konsole eine schön formatierte JSON‑Darstellung Ihrer gescannten Rechnung ausgibt.

---

## Häufige Stolperfallen & Tipps (c# ocr tutorial Extras)

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| **Leeres `Text`‑Feld** | Bild hat niedrigen Kontrast oder ist gedreht. | Bild vorverarbeiten (Kontrast erhöhen, Deskew) oder `OcrEngine.ImagePreprocess` verwenden. |
| **`System.DllNotFoundException`** | Native Aspose OCR‑Binärdateien fehlen. | Sicherstellen, dass das NuGet‑Paket korrekt wiederhergestellt wurde und die Laufzeit‑Architektur (x64/x86) zu Ihrem OS passt. |
| **Leistungs‑Einbruch bei großen PDFs** | OCR verarbeitet jede Seite sequenziell. | Parallelisieren, indem Sie separate `OcrEngine`‑Instanzen pro Seite erstellen (Engine ist thread‑sicher). |
| **JSON zu groß** | Sie serialisieren jedes Detail, inklusive Bounding‑Boxes. | Ein DTO verwenden, das nur `Text` und `Confidence` enthält, bevor Sie serialisieren. |

> **Denken Sie daran:** Ziel dieses Tutorials ist es, einen sauberen End‑zu‑End‑Ablauf zu zeigen. Sie können das JSON jederzeit kürzen oder später weitere Metadaten hinzufügen.

---

## Fazit

Sie haben gerade ein **c# ocr tutorial** abgeschlossen, das ein Bild lädt, **Text aus Bild** extrahiert und eine **format json output** erzeugt, indem es **object to json serialisiert**. Die Schritte sind einfach, der Code ist sofort ausführbar und das JSON ist perfekt eingerückt für die Weiterverarbeitung.

Was kommt als Nächstes? Tauschen Sie `OcrLanguage.English` gegen `OcrLanguage.French` aus oder verarbeiten Sie einen Ordner mit Quittungen in einer Schleife. Vielleicht möchten Sie das JSON direkt in Azure Blob Storage speichern oder in ein Machine‑Learning‑Modell einspeisen.

Falls Sie Probleme haben, prüfen Sie, ob der Bildpfad korrekt ist und ob die Aspose OCR‑Lizenz (falls vorhanden) geladen wurde, bevor Sie `Recognize` aufrufen. Viel Spaß beim Coden und mögen Ihre OCR‑Ergebnisse stets gestochen scharf sein! 

*Image illustrating the OCR flow (alt text: "c# ocr tutorial diagram showing load image, recognize text, serialize to JSON")*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}