---
category: general
date: 2026-01-15
description: Bild in JSON konvertieren mit Aspose OCR in C#. Erfahren Sie, wie Sie
  Text aus einem Bild extrahieren, JSON‑Bounding‑Boxes erhalten und ein Belegbild
  erkennen.
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: de
og_description: Bild in JSON konvertieren mit Aspose OCR in C#. Schritt‑für‑Schritt‑Anleitung
  zum Extrahieren von Text aus einem Bild, zum Erkennen von Belegbildern und zum Erhalten
  von JSON‑Bounding‑Boxes.
og_title: Bild in JSON konvertieren mit Aspose OCR C# Anleitung
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: Bild in JSON konvertieren mit Aspose OCR C#‑Leitfaden
url: /de/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bild in JSON konvertieren mit Aspose OCR C# Anleitung

Haben Sie jemals **Bild in JSON konvertieren** müssen, waren sich aber nicht sicher, welche Bibliothek Ihnen sowohl den Rohtext als auch die genauen Wortkoordinaten liefern kann? Sie sind nicht allein. Viele Entwickler stoßen auf dieses Problem, wenn sie Text aus Bilddateien – insbesondere Quittungen – extrahieren wollen und gleichzeitig ein maschinenlesbares JSON‑Payload für die nachgelagerte Verarbeitung benötigen.

In diesem Tutorial führen wir Sie durch ein vollständiges **Aspose OCR C# Beispiel**, das zeigt, wie Sie Text aus einem Bild extrahieren, ein Quittungsbild erkennen und **JSON‑Bounding‑Boxes** für jedes Wort ausgeben. Am Ende haben Sie eine sofort einsatzbereite Konsolenanwendung, die einen schön formatierten JSON‑String ausgibt, den Sie in jede API, Datenbank oder Analyse‑Pipeline einspeisen können.

> **Was Sie am Ende erhalten**  
> • Ein voll funktionsfähiges C#‑Projekt, das **Bild in JSON konvertiert**  
> • Einblick, warum wir `IncludeBoundingBoxes` aktivieren (es ist der Schlüssel zu `json bounding boxes`)  
> • Tipps zum Umgang mit verschiedenen Bildformaten und Sprachen  

Los geht's.

---

## Was Sie benötigen

- **.NET 6.0 SDK** (oder eine neuere Version) – der Code zielt auf .NET 6 ab, funktioniert aber auch mit .NET Framework 4.7+.  
- **Aspose.OCR for .NET** NuGet‑Paket – Sie können es über `dotnet add package Aspose.OCR` hinzufügen.  
- Ein Beispiel‑Quittungsbild (`receipt.jpg`), das in einem Ordner liegt, den Sie von Ihrem Projekt aus referenzieren können.  
- Visual Studio 2022, VS Code oder jede andere IDE Ihrer Wahl.

Es werden keine externen Dienste benötigt; alles läuft lokal.

---

## Bild in JSON konvert – Überblick

Die Grundidee ist einfach: Laden Sie ein Bild, lassen Sie Aspose OCR Englisch (oder jede unterstützte Sprache) erkennen, bitten Sie es, Bounding‑Boxes einzuschließen, und fordern Sie schließlich das Ergebnis im **JSON**‑Format an. Die Bibliothek übernimmt das gesamte schwere Heben – OCR, Layout‑Analyse und JSON‑Serialisierung.

Hier ist ein hoch‑level Diagramm des Ablaufs (stellen Sie sich ein kleines Bild vor):

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

Dieses kleine Diagramm erfasst die gesamte Pipeline, die wir implementieren werden.

---

## Schritt 1: Projekt einrichten und Aspose OCR installieren

Zuerst erstellen Sie ein neues Konsolenprojekt und binden das Aspose OCR‑Paket ein.

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **Pro‑Tipp:** Wenn Sie Visual Studio verwenden, klicken Sie mit der rechten Maustaste auf das Projekt → *NuGet‑Pakete verwalten* → Sie nach **Aspose.OCR** und installieren Sie die neueste stabile Version (derzeit 23.12).

---

## Schritt 2: Bild laden, das Sie erkennen möchten

Wir verwenden die Methode `OcrImage.FromFile`, um das Quittungsbild zu lesen. Stellen Sie sicher, dass der Pfad auf eine echte Datei zeigt; andernfalls erhalten Sie eine `FileNotFoundException`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Wenn sich Ihr `.csproj` befindet, können Sie einfach `"receipt.jpg"` verwenden.

---

## Schritt 3: OCR‑Optionen für JSON‑Bounding‑Boxes konfigurieren

Die Magie passiert, wenn wir `OutputFormat = OutputFormat.Json` **und** `IncludeBoundingBoxes = true` aktivieren. Ersteres weist Aspose an, das Ergebnis als JSON zu serialisieren, während letzteres `x`, `y`, `width` und `height` für jedes Wort hinzufügt – genau das, was Sie für `json bounding boxes` benötigen.

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

Sie können auch `ocrOptions.Dpi` `Options.Language` anpassen, wenn Sie eine höhere Auflösung oder eine andere Sprache benötigen.

---

## Schritt 4: Erkennung durchführen – Text aus Bild extrahieren

Jetzt rufen wir `Recognize` auf. Die Methode gibt ein `OcrResult`‑Objekt zurück, das den JSON‑String, den Rohtext und mehr enthält.

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

Wenn Sie andere Sprachen verarbeiten müssen, ersetzen Sie `Language.English` durch `Language.Spanish`, `Language.French` usw. Aspose unterstützt von Haus aus über 30 Sprachen.

---

## Schritt 5: Ergebnis ausgeben – Ihr JSON‑Payload

Abschließend geben wir das JSON in der Konsole aus. In einer echten Anwendung würden Sie es wahrscheinlich in eine Datei schreiben oder an einen Dienst senden.

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

Das Ausführen des Programms sollte ein JSON‑Dokument erzeugen, das dem untenstehenden Ausschnitt ähnelt.

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

Beachten Sie, dass jedes Wort jetzt seine **JSON‑Bounding‑Box** enthält – perfekt, um es in ein UI‑Overlay oder einen nachgelagerten Parser einzuspeisen.

---

## Voll funktionsfähiges Beispiel

Unten finden Sie das komplette, sofort kopier‑fertige Programm. Keine versteckten Teile, keine externen Aufrufe – nur reines C#.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **Achten Sie auf:**  
> • **Dateipfad‑Fehler** – überprüfen Sie den Bildort doppelt.  
> • **Fehlendes NuGet‑Paket** – stellen Sie sicher, dass `Aspose.OCR` referenziert wird.  
> • **Nicht unterstützte Bildformate** – verwenden Sie JPEG, PNG, BMP oder TIFF für beste Ergebnisse.

---

## Häufige Fragen & Randfälle

### Kann ich eine **PDF‑Seite** statt eines JPEG in JSON konvertieren?

Ja. Konvertieren Sie die PDF‑Seite zuerst in ein Bild (z. B. mit `Aspose.PDF`), und geben Sie dieses Bild dann in dieselbe OCR‑Pipeline ein. Die JSON‑Ausgabe ist identisch, da der OCR‑Schritt nur Rasterdaten benötigt.

### Was, wenn die Quittung unscharf ist?

Erhöhen Sie die DPI in `ocrOptions`. Zum Beispiel:

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

### Ich brauche **mehrere Sprachen** auf derselben Quittung (z. B. Englisch + Spanisch).

Sie können ein Array von Sprachen übergeben:

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

### Wie schreibe ich das JSON in eine Datei?

Ersetzen Sie einfach die Zeile `Console.WriteLine` durch:

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

---

## Visuelle Zusammenfassung

![Beispiel Bild in JSON konvertieren](convert-image-to-json.png "Beispiel Bild in JSON konvertieren")

*Der Screenshot zeigt die Konsolenausgabe des JSON‑Payloads nach dem Ausführen der Demo.*

---

## Fazit

Wir haben Ihnen gerade gezeigt, wie Sie **Bild in JSON konvertieren** mit Aspose OCR in C# können. Durch die Konfiguration von `OutputFormat` und `IncludeBoundingBoxes` können Sie **Text aus Bild extrahieren**, **Quittungsbild erkennen** und präzise **JSON‑Bounding‑Boxes** für jedes Wort erhalten. Der komplette, ausführbare Code befindet sich im obigen Snippet, sodass Sie ihn sofort in jedes .NET‑Projekt einfügen können.

Was kommt als Nächstes? Versuchen Sie, das JSON in einen Front‑End‑Viewer zu speisen, der jedes Wort hervorhebt, oder senden Sie die Daten an ein Machine‑Learning‑Modell, das Positionen auf Quittungen klassifiziert. Sie können auch mit anderen Sprachen, höheren DPI‑Einstellungen oder der Stapelverarbeitung mehrerer Bilder in einer Schleife experimentieren.

Wenn Sie auf Probleme stoßen, denken Sie an die Tipps zu Dateipfaden, DPI und Sprach‑Arrays. Hinterlassen Sie gerne einen Kommentar oder öffnen Sie ein Issue im GitHub‑Repo, das Sie für dieses Demo erstellen. Viel Spaß beim Programmieren und beim Umwandeln von Bildern in strukturiertes JSON!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}