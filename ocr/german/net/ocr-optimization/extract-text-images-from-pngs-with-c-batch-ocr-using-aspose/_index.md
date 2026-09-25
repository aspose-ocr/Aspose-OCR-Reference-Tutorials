---
category: general
date: 2026-02-09
description: Extrahiere Text aus Bildern schnell mit C#, indem du die maximale Parallelität
  für Batch-OCR festlegst – lerne, gescannte Seiten zu konvertieren, mehrere Bild‑OCRs
  zu verarbeiten und PNG‑Text effizient zu lesen.
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: de
og_description: Extrahiere Text aus Bildern in C# durch Festlegen der maximalen Parallelität.
  Dieses Tutorial zeigt, wie man gescannte Seiten konvertiert, mehrere Bild‑OCRs ausführt
  und PNG‑Text mit Aspose OCR liest.
og_title: Texte aus PNG-Bildern mit C# extrahieren – Vollständiger Batch-OCR-Leitfaden
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: Texte aus PNGs mit C# extrahieren – Batch-OCR mit Aspose OCR
url: /de/net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus PNGs mit C# extrahieren – Batch-OCR mit Aspose OCR

Haben Sie schon einmal **Text aus Bildern** aus einem Ordner mit gescannten PNGs extrahieren müssen, aber sind an der Frage „Wie mache ich das schnell?“ hängen geblieben? Sie sind nicht allein. In vielen realen Projekten müssen Entwickler **maximale Parallelität festlegen**, damit Dutzende von Seiten in Sekunden statt Minuten verarbeitet werden.

In diesem Leitfaden gehen wir Schritt für Schritt durch ein vollständiges, ausführbares Beispiel, das **gescannte Seiten konvertiert**, **mehrere Bild‑OCRs** ausführt und schließlich **PNG‑Text liest**, ohne ins Schwitzen zu geraten. Keine vagen „siehe die Docs“-Links – nur Code, den Sie copy‑pasten können, Erklärungen, warum jede Zeile wichtig ist, und Tipps, um die üblichen Stolperfallen zu vermeiden.

> **Pro‑Tipp:** Wenn Sie Aspose OCR bereits anderweitig einsetzen, werden Sie hier dieselbe `OcrEngine`‑Klasse sehen, aber wir passen ihre Konfiguration für echtes Parallel‑Processing an.

---

## Was Sie benötigen

- **.NET 6+** (oder .NET Framework 4.6+). Die API funktioniert identisch, aber neuere Laufzeiten bieten bessere Thread‑Steuerung.  
- **Aspose.OCR für .NET** – Installation via NuGet: `Install-Package Aspose.OCR`.  
- Ein Ordner, der einige PNG‑Scans enthält (`page1.png`, `page2.png`, …).  
- Eine IDE oder ein Editor Ihrer Wahl (Visual Studio, Rider, VS Code …).

Das war’s. Keine zusätzlichen Services, keine Cloud‑Keys, nur reine lokale Verarbeitung.

---

## extract text images – Maximale Parallelität für Batch‑OCR festlegen

Wenn Sie OCR für mehrere Dateien starten, verwendet die Engine standardmäßig einen einzelnen Thread. Das ist sicher, aber quälend langsam. Durch das Setzen von `MaxDegreeOfParallelism` teilen Sie der Engine mit, wie viele Threads gleichzeitig laufen dürfen.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**Warum 4?**  
Vier ist auf den meisten modernen Laptops ein guter Kompromiss – genug Kerne, um die CPU auszulasten, aber nicht so viele, dass andere Prozesse zu kurz kommen. Auf einem Server mit 16 Kernen können Sie die Zahl auf 12 oder 14 erhöhen, um einen spürbaren Geschwindigkeitsschub zu erhalten.

---

## Convert scanned pages – Aufbau der Image‑Stream‑Sammlung

Aspose erwartet jedes Bild als `ImageStream`. Der Helfer `FromFile` liest die Datei, hält sie im Speicher und übergibt sie an die OCR‑Engine. Sie können auch einen `MemoryStream` verwenden, wenn Ihre Bilder aus einer Datenbank oder einer HTTP‑Antwort stammen.

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**Randfall:** Wenn eine Datei fehlt oder beschädigt ist, wirft `FromFile` eine `FileNotFoundException`. Packen Sie die Erstellung in ein `try/catch`, falls Sie mit unzuverlässigen Eingaben rechnen.

---

## multiple image ocr – Batch‑OCR ausführen

Jetzt passiert das Schwergewicht. `RecognizeBatch` startet bis zu der zuvor festgelegten Anzahl von Threads, verarbeitet jedes Bild und gibt eine Liste von `OcrResult`‑Objekten zurück.

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

Im Hintergrund lädt jeder Thread sein Bild, führt das neuronale Netzwerk aus und extrahiert Klartext. Die Reihenfolge der Ergebnisse entspricht der Reihenfolge der Eingabeliste, sodass Sie sicher Seite 1 → Ergebnis 0 usw. zuordnen können.

---

## read png text – Extrahierten Inhalt anzeigen

Zum Schluss iterieren wir über die Ergebnisse und geben den Klartext in der Konsole aus. Hier können Sie die Ausgabe in eine Datei, eine Datenbank oder sogar in einen nachgelagerten NLP‑Dienst leiten.

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### Erwartete Konsolenausgabe

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

Falls Sie leere Abschnitte sehen, prüfen Sie, ob die PNGs nicht rein weiße Bilder sind – OCR benötigt etwas Kontrast.

---

## Praktische Tipps & häufige Stolperfallen

| Situation | Was zu tun ist |
|-----------|----------------|
| **Speicherbelastung** bei großen Stapeln | Bilder in Chargen von 10‑20 Dateien verarbeiten und bei Bedarf `GC.Collect()` aufrufen, wenn Sie Spitzen bemerken. |
| **Falsche Spracherkennung** | Setzen Sie `ocrEngine.Configuration.Language = OcrLanguage.English;` (oder Ihre Zielsprache) bevor Sie `RecognizeBatch` aufrufen. |
| **Langsame Performance trotz Parallelität** | Prüfen Sie, ob Ihre SSD I/O drosselt; lesen Sie alle Dateien zuerst in den Speicher (wie wir es mit `ImageStream.FromFile` tun). |
| **Fehlende Zeichen** | Erhöhen Sie `ocrEngine.Configuration.DPI = 300;` für eine höherauflösende Verarbeitung. |

---

## Beispiel erweitern – Von PNG zu PDF oder DOCX

Falls Sie irgendwann **gescannte Seiten** in durchsuchbare PDFs umwandeln wollen, übergeben Sie einfach das gleiche `ocrResults[i].PlainText` an eine PDF‑Bibliothek (z. B. Aspose.PDF) und legen Sie den Text als unsichtbare Ebene darüber. Der gleiche Parallelitäts‑Trick funktioniert dort ebenfalls.

---

## Vollständiger Quellcode (Copy‑Paste‑bereit)

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

Speichern Sie die Datei als `BatchExample.cs`, führen Sie `dotnet run` aus und beobachten Sie, wie Ihre Konsole mit dem Text gefüllt wird, der zuvor in den PNG‑Scans verborgen war.

---

## Visuelle Zusammenfassung

![extract text images example](images/ocr-batch.png){alt="Beispiel für das Extrahieren von Text aus Bildern"}

Das Diagramm zeigt den Ablauf: **PNG‑Dateien → ImageStream‑Sammlung → OcrEngine (maximale Parallelität) → OCR‑Ergebnisse → Konsole / nachgelagerte Speicherung**.

---

## Fazit

Sie haben nun ein solides, durchgängiges Rezept, wie Sie **Text aus Bildern** in C# extrahieren, **maximale Parallelität setzen**, **gescannte Seiten konvertieren**, **mehrere Bild‑OCRs** durchführen und **PNG‑Text** effizient lesen. Der Code ist eigenständig, die Erklärungen decken sowohl das „Wie“ als auch das „Warum“ ab, und die Tipps bewahren Sie vor gängigen Problemen.

Was kommt als Nächstes? Ersetzen Sie die PNG‑Liste durch eine dynamische `Directory.GetFiles`‑Schleife, experimentieren Sie mit verschiedenen Thread‑Zahlen oder leiten Sie die Ausgabe in ein durchsuchbares PDF weiter. Das gleiche Muster skaliert auf Hunderte von Seiten mit kaum zusätzlichem Code.

Fragen oder ein kniffliger Randfall? Hinterlassen Sie einen Kommentar unten – und happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}