---
category: general
date: 2026-02-20
description: Erfahren Sie, wie Sie Quittungen in C# lesen, indem Sie Text aus einem
  Bild extrahieren und in JSON konvertieren. Schritt‑für‑Schritt‑Code mit Aspose OCR.
draft: false
keywords:
- how to read receipt
- extract text from image
- convert image to json
- load image file c#
- OCR receipt C#
- Aspose OCR tutorial
language: de
og_description: Entdecken Sie, wie Sie Quittungen in C# lesen, indem Sie eine Bilddatei
  laden, Text mit Aspose OCR extrahieren und das Ergebnis in JSON konvertieren. Vollständiges
  Codebeispiel.
og_title: Wie man Quittungen in C# liest – Text extrahieren, in JSON konvertieren
tags:
- C#
- OCR
- Image Processing
- JSON
title: Wie man Quittungen in C# liest – Vollständige Anleitung zum Extrahieren von
  Text aus Bildern
url: /de/net/text-recognition/how-to-read-receipt-in-c-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Quittungen in C# liest – Komplettanleitung

Haben Sie sich schon einmal gefragt, **wie man Quittungs‑Bilder** programmgesteuert ausliest? Vielleicht entwickeln Sie eine Ausgaben‑Tracking‑App und müssen Positionen aus einem Foto einer Supermarkt‑Quittung extrahieren. In meiner Erfahrung ist der größte Schmerzpunkt, das verschwommene JPEG in strukturierte Daten zu verwandeln, die Sie tatsächlich nutzen können. Die gute Nachricht? Mit ein paar Zeilen C# und Aspose OCR können Sie **Text aus Bild extrahieren** und dann **Bild zu JSON konvertieren** – fast wie Magie.

In diesem Tutorial erhalten Sie eine sofort einsatzbereite Lösung, die **ein Bild in C# lädt**, OCR ausführt und ein detailliertes JSON‑Payload ausgibt. Keine externen Dienste, keine umständlichen REST‑Aufrufe – nur reiner .NET‑Code, den Sie in jedes Konsolen‑ oder ASP.NET‑Projekt einbinden können. Am Ende verstehen Sie, warum jeder Schritt wichtig ist, wie Sie gängige Sonderfälle (wie nicht‑standardisierte Quittungsgrößen) behandeln und wie das JSON‑Ergebnis tatsächlich aussieht.

## Was Sie benötigen

- **.NET 6.0 oder höher** – der Code verwendet `System.Drawing.Common`, das unter Windows, Linux und macOS unterstützt wird.  
- **Aspose.OCR für .NET** – Sie können das kostenlose Test‑NuGet‑Paket (`Aspose.OCR`) herunterladen oder eine lizenzierte Kopie verwenden, falls Sie eine besitzen.  
- Ein **Beispiel‑Quittungs‑Bild** (`receipt.jpg`), das an einem Ort liegt, den Ihre Anwendung lesen kann.  
- Beliebige IDE (Visual Studio, Rider, VS Code).  

Das ist alles. Keine zusätzliche Konfiguration, keine API‑Schlüssel.

---

## Schritt 1 – Bilddatei in C# laden (Primary Keyword in Action)

Bevor die OCR‑Engine ihre Magie entfalten kann, müssen Sie das Bild in den Speicher laden. Das ist der klassische „load image file C#“‑Schritt, den viele Entwickler übersehen.

```csharp
using System.Drawing;          // Required for Image
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to your receipt image – adjust as needed
string imagePath = @"C:\Receipts\receipt.jpg";

// Load the image into a System.Drawing.Image object
Image receiptImage = Image.FromFile(imagePath);
```

**Warum das wichtig ist:**  
`Image.FromFile` liest die Datei *einmal* und hält einen Handle offen, was für einen schnellen OCR‑Durchlauf ideal ist. Wenn Sie viele Quittungen in einer Schleife verarbeiten, sollten Sie `Image.FromStream` verwenden, um das Sperren der Datei zu vermeiden.

> **Pro‑Tipp:** Wenn Sie eine *FileNotFoundException* erhalten, prüfen Sie den Pfad und stellen Sie sicher, dass das Bild tatsächlich vorhanden ist. Relative Pfade funktionieren ebenfalls (`"./receipt.jpg"`), aber absolute Pfade sind für Produktionsjobs sicherer.

---

## Schritt 2 – OCR‑Engine erstellen und konfigurieren

Aspose OCR liefert eine sofort einsatzbereite `OcrEngine`. Sie müssen kein Modell trainieren; die Bibliothek kennt bereits die meisten gedruckten Texte, die auf Quittungen verwendet werden.

```csharp
// Instantiate the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Optional: tweak recognition settings if your receipts are low‑contrast
ocrEngine.Config.Language = OcrLanguage.English;
ocrEngine.Config.DetectOrientation = true;   // Handles rotated receipts
```

**Warum wir diese Optionen setzen:**  
`DetectOrientation` weist die Engine an, das Bild automatisch zu drehen, falls die Quittung verkehrt herum gescannt wurde. Das Festlegen der Sprache reduziert den Zeichensatz und kann die Genauigkeit erhöhen – besonders wenn Sie nur englische alphanumerische Daten benötigen.

---

## Schritt 3 – Bild erkennen und in JSON konvertieren

Jetzt kommt der spaßige Teil: **Text aus Bild extrahieren** und **Bild zu JSON konvertieren** in einem einzigen Aufruf.

```csharp
// Perform OCR and get the result as a JSON string
string jsonResult = ocrEngine.RecognizeToJson(receiptImage);
```

Die Methode `RecognizeToJson` liefert eine umfangreiche JSON‑Struktur, die enthält:

- `Text`: der reine, zusammengefügte Text.  
- `Lines`: ein Array von Zeilen‑Objekten mit Koordinaten.  
- `Words`: jedes Wort mit Vertrauenswerten.  
- `Regions`: Begrenzungsrahmen für erkannte Textblöcke.

Sie können dieses JSON in ein C#‑Objekt deserialisieren, wenn Sie typisierten Zugriff benötigen, aber für viele Szenarien reicht das Ausgeben des rohen JSON aus.

---

## Schritt 4 – JSON ausgeben (oder speichern)

Sehen wir uns die Ausgabe an und besprechen, was Sie damit tun können.

```csharp
// Write the JSON to the console – perfect for quick debugging
Console.WriteLine(jsonResult);

// Bonus: Save the JSON to a file for later processing
File.WriteAllText("receipt_output.json", jsonResult);
```

### Beispielausgabe

```json
{
  "Text":"Walmart\n123 Main St\nItem A  $2.99\nItem B  $5.49\nTotal   $8.48",
  "Lines":[
    {"Text":"Walmart","BoundingBox":{"X":10,"Y":15,"Width":200,"Height":30}},
    {"Text":"123 Main St","BoundingBox":{"X":10,"Y":50,"Width":180,"Height":25}},
    {"Text":"Item A  $2.99","BoundingBox":{"X":10,"Y":85,"Width":210,"Height":28}},
    {"Text":"Item B  $5.49","BoundingBox":{"X":10,"Y":120,"Width":210,"Height":28}},
    {"Text":"Total   $8.48","BoundingBox":{"X":10,"Y":155,"Width":210,"Height":30}}
  ],
  "Words":[
    {"Text":"Walmart","Confidence":0.99,"BoundingBox":{...}},
    …
  ]
}
```

**Was nun?**  
Parsen Sie das `Lines`‑Array, um den `Total`‑Betrag herauszuholen, oder übergeben Sie das JSON an einen nachgelagerten Service, der Ausgabeposten speichert. Da das Ergebnis bereits JSON ist, können Sie es direkt in jede NoSQL‑Datenbank, Azure Function oder Power Automate‑Flow einspeisen.

---

## Schritt 5 – Umgang mit gängigen Sonderfällen

Selbst die besten OCR‑Engines stolpern über ein paar Dinge. Im Folgenden finden Sie Szenarien, denen Sie beim Erlernen von **how to read receipt**‑Bildern begegnen könnten.

| Situation | Lösung / Empfehlung |
|-----------|----------------------|
| **Niedrigauflösende Quittung (≤ 150 dpi)** | Bild zuerst mit `Bitmap` und `Graphics` hochskalieren (`InterpolationMode.HighQualityBicubic`). |
| **Gedrehte oder schiefe Quittung** | `DetectOrientation = true` beibehalten. Bei starker Schräglage vorher mit `Image.RotateFlip` oder einer Drittanbieter‑Bibliothek wie OpenCV vorverarbeiten. |
| **Farbiger Hintergrund (z. B. Quittung auf einem Tisch)** | Vor dem OCR in Graustufen konvertieren und den Kontrast erhöhen (`ImageAttributes`). |
| **Mehrere Quittungen in einem Foto** | Jede Quittungsregion manuell zuschneiden oder `ocrEngine.Config.RecognizeMultipleRegions = true` verwenden. |
| **Große Dateien führen zu OutOfMemory** | `using`‑Anweisungen nutzen, um `Image`‑Objekte sofort zu entsorgen, oder in Teilen verarbeiten. |

```csharp
// Example: simple grayscale conversion
using (Bitmap bmp = new Bitmap(receiptImage))
{
    for (int y = 0; y < bmp.Height; y++)
        for (int x = 0; x < bmp.Width; x++)
        {
            Color c = bmp.GetPixel(x, y);
            int gray = (int)(c.R * 0.3 + c.G * 0.59 + c.B * 0.11);
            bmp.SetPixel(x, y, Color.FromArgb(gray, gray, gray));
        }
    receiptImage = (Image)bmp.Clone();
}
```

---

## Schritt 6 – Vollständiges Beispiel (Copy‑Paste‑bereit)

Unten finden Sie das *komplette* Programm, das Sie sofort kompilieren können. Es enthält alle Schritte, die richtigen `using`‑Direktiven und eine elegante Fehlerbehandlung.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptReaderDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image file C#
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\receipt.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found: {imagePath}");
                return;
            }

            Image receiptImage;
            try
            {
                receiptImage = Image.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ Failed to load image: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Create and configure OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine
            {
                Config =
                {
                    Language = OcrLanguage.English,
                    DetectOrientation = true
                }
            };

            // -------------------------------------------------
            // 3️⃣ Recognize and convert to JSON
            // -------------------------------------------------
            string jsonResult;
            try
            {
                jsonResult = ocrEngine.RecognizeToJson(receiptImage);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"🛑 OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 4️⃣ Output results
            // -------------------------------------------------
            Console.WriteLine("🗂️ OCR JSON Result:");
            Console.WriteLine(jsonResult);

            // Optionally persist the JSON
            string outputPath = Path.Combine(
                Path.GetDirectoryName(imagePath) ?? ".", "receipt_output.json");
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"✅ JSON saved to {outputPath}");
        }
    }
}
```

**Ausführen:**  
`dotnet run` im Projektordner. Wenn alles korrekt eingerichtet ist, sehen Sie das JSON in der Konsole und neben Ihrem Quittungs‑Bild gespeichert.

---

## Fazit

Wir haben gerade **how to read receipt**‑Bilder in C# von Anfang bis Ende behandelt. Durch das Laden des Bildes, das Konfigurieren von Aspose OCR und den Aufruf von `RecognizeToJson` können Sie **Text aus Bild extrahieren** und **Bild zu JSON konvertieren** mit praktisch keinem Boilerplate‑Code. Der Ansatz skaliert – von einer Ein‑Quittungs‑Demo bis zu einem Batch‑Prozessor, der nachts Hunderte von Quittungen verarbeitet.

Mögliche nächste Schritte:

- **JSON parsen**, um Daten wie Datum, Gesamtsumme und Positionen zu extrahieren (mit `System.Text.Json` oder `Newtonsoft.Json`).  
- **Integration in eine Datenbank** (SQL, Cosmos DB), um Ausgaben automatisch zu speichern.  
- **UI hinzufügen** (WinForms, WPF oder Blazor), damit Nutzer Quittungen per Drag‑and‑Drop hochladen können.  
- **Aspose OCR** durch eine andere Engine (Tesseract, Microsoft Azure OCR) ersetzen, falls Lizenzkosten ein Thema sind – behalten Sie einfach das gleiche „load image file C#“‑Muster bei.

Experimentieren Sie, brechen Sie Dinge und kommen Sie dann hier für eine Auffrischung zurück. Wenn Sie auf Probleme stoßen, sind die Community (und die Aspose‑Foren) großartige Anlaufstellen. Viel Spaß beim Coden und beim Umwandeln von Papier‑Quittungen in saubere, durchsuchbare Daten!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}