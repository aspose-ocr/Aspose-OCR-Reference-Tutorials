---
category: general
date: 2026-03-13
description: Wie man OCR in C# verwendet, um Text aus Scans zu extrahieren. Lernen
  Sie, TIFF mit Aspose OCR, GPU‑Beschleunigung und Schritt‑für‑Schritt‑Code in Text
  zu konvertieren.
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: de
og_description: Wie man OCR in C# verwendet, um Text aus Scans zu extrahieren. Dieser
  Leitfaden zeigt, wie man TIFF mit Aspose OCR und GPU‑Beschleunigung in Text konvertiert.
og_title: Wie man OCR in C# verwendet – Text schnell aus Scans extrahieren
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Wie man OCR in C# verwendet – Text schnell aus Scans extrahieren
url: /de/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in C# verwendet – Text schnell aus Scans extrahieren

Haben Sie sich jemals gefragt, **wie man OCR** verwendet, um lesbaren Text aus einem Stapel gescannter TIFF‑Dateien zu extrahieren? Sie sind nicht der Einzige. In vielen realen Projekten – denken Sie an die Digitalisierung von Rechnungen, die Archivierung historischer Dokumente oder einfach das Durchsuchbar‑machen von PDFs – benötigen Entwickler eine zuverlässige Methode, **Text aus Scans zu extrahieren**, ohne ins Schwitzen zu geraten.

Die gute Nachricht? Mit Aspose OCR und ein paar Zeilen C# können Sie TIFF in Text umwandeln – und das in Sekundenschnelle, selbst auf einem bescheidenen Arbeitsplatz. Im Folgenden erhalten Sie ein vollständiges, sofort lauffähiges Beispiel sowie die Begründung jeder Entscheidung, damit Sie es an Ihren eigenen Workflow anpassen können.

## Was Sie benötigen

Bevor wir loslegen, stellen Sie sicher, dass Sie Folgendes zur Hand haben:

| Prerequisite | Why it matters |
|--------------|----------------|
| .NET 6+ (or .NET Framework 4.7+) | Das Aspose OCR NuGet‑Paket richtet sich an moderne .NET‑Runtimes. |
| Visual Studio 2022 (or any IDE you like) | Bietet Ihnen IntelliSense und einfaches Debugging. |
| A CUDA‑compatible GPU & driver (optional) | Ermöglicht `ocrEngine.UseGpu = true` für einen spürbaren Geschwindigkeitszuwachs bei großen Stapeln. |
| A folder of TIFF images you want to process | Dieses Tutorial verwendet `*.tif`‑Dateien, Sie können das Muster jedoch anpassen. |
| Aspose.OCR NuGet package (`Install-Package Aspose.OCR`) | Die Kernbibliothek, die die schwere Arbeit übernimmt. |

Falls Ihnen etwas davon fehlt, besorgen Sie es jetzt – es hat keinen Sinn, weiterzulesen, nur um später auf eine fehlende Abhängigkeit zu stoßen.

## Überblick über die Lösung

Auf hoher Ebene erledigt das Programm drei Dinge:

1. **Erstelle eine OCR‑Engine** und schalte optional die GPU‑Beschleunigung ein.  
2. **Iteriere über jede TIFF‑Datei** in einem Verzeichnis, führe die Erkennung aus und erfasse den resultierenden Klartext.  
3. **Schreibe den Text** in eine `.txt`‑Datei, die neben dem Originalbild liegt.

Das war's. Der Code ist bewusst klein, demonstriert jedoch Best Practices wie die explizite Sprachauswahl, korrekte Ressourcenfreigabe und Fehlerbehandlung für die häufigsten Randfälle.

![How to use OCR in C# example](/images/how-to-use-ocr-csharp.png "Illustration of how to use OCR in C# to extract text from scans")

## Schritt 1: Initialisieren der OCR‑Engine (Wie man OCR verwendet)

Das Erste, was Sie benötigen, ist eine Instanz von `OcrEngine`. Dieses Objekt ist das Tor zu allen Aspose‑OCR‑Funktionen. Standardmäßig arbeitet es auf der CPU, aber das Setzen von `UseGpu = true` weist die Bibliothek an, die schweren Matrixberechnungen auf Ihre Grafikkarte auszulagern – vorausgesetzt, Sie haben einen CUDA‑kompatiblen Treiber installiert.

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**Warum das wichtig ist:**  
- **GPU‑Beschleunigung** kann die Verarbeitungszeit bei hochauflösenden Scans um bis zu 70 % reduzieren.  
- **Explizite Sprachauswahl** verhindert, dass die Engine rät, und verbessert die Genauigkeit, besonders bei nicht‑lateinischen Schriften.

## Schritt 2: Die Engine auf Ihre Scans ausrichten (TIFF in Text konvertieren)

Als Nächstes teilen wir dem Programm mit, wo nach den Bildern gesucht werden soll. Die Verwendung von `Directory.GetFiles` mit einem `*.tif`‑Filter hält die Logik einfach und verhindert das Einbeziehen von nicht verwandten Dateien wie `.jpg` oder `.png`.

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**Hinweis zum Randfall:** Wenn das Verzeichnis leer ist, wird die nachfolgende Schleife einfach nie ausgeführt, was völlig in Ordnung ist. Später sehen Sie eine freundliche Meldung „No files found“.

## Schritt 3: Jede TIFF‑Datei verarbeiten (Text aus Scans extrahieren)

Jetzt das Herzstück des Programms: Laden jedes Bildes, Ausführen von OCR und Speichern der Ausgabe. Der Helfer `ImageStream.FromFile` streamt die Datei direkt in den Speicher, was effizienter ist, als zuerst ein `Bitmap` zu laden.

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**Warum wir jede Iteration in ein `try/catch` einbetten:**  
Das Scannen einer Dokumentencharge ist unordentlich; ein beschädigtes TIFF oder ein Out‑of‑Memory‑Fehler sollte den gesamten Durchlauf nicht abbrechen. Der Catch‑Block protokolliert das Problem und fährt fort, wodurch die Pipeline robust bleibt.

### Erwartete Ausgabe

Für jedes `example.tif` finden Sie eine zugehörige `example.txt`, die etwa Folgendes enthält:

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

Wenn die OCR‑Engine eine Zeile nicht lesen kann, lässt sie einfach eine leere Zeile oder ein verzerrtes Zeichen zurück – es kommt zu keinem Absturz.

## Schritt 4: Aufräumen und Entsorgen (Best Practice)

`OcrEngine` implementiert `IDisposable`, daher ist es höflich, native Ressourcen freizugeben, wenn Sie fertig sind. In einer kurzen Konsolen‑App könnten Sie sich auf den GC verlassen, aber explizites Entsorgen ist eine Gewohnheit, die es wert ist, sich anzueignen.

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## Vollständiges funktionierendes Beispiel (Einfaches Kopieren‑Einfügen)

Unten finden Sie das komplette Programm, das Sie in ein neues Console‑App‑Projekt einfügen können. Es kompiliert unverändert, vorausgesetzt, Sie haben das Aspose.OCR‑NuGet‑Paket hinzugefügt.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### Schnelle Checkliste

- **GPU‑Flag** – entfernen oder auf `false` setzen, wenn Sie keinen CUDA‑Treiber haben.  
- **Sprache** – `Language.English` durch eine andere unterstützte Sprache ersetzen.  
- **Dateimuster** – ändern Sie `"*.tif"` zu `"*.png"` oder `"*.*"`, wenn Ihre Scans ein anderes Format haben.  

## Häufige Fallstricke & Profi‑Tipps (c# OCR‑Tutorial)

| Pitfall | How to avoid it |
|---------|-----------------|
| **Out‑of‑memory errors** on huge batches | Verarbeiten Sie Dateien in kleineren Stapeln oder rufen Sie `GC.Collect()` nach jeweils 50 Dateien auf (selten nötig). |
| **GPU not detected** but `UseGpu = true` | Die Engine wechselt stillschweigend zur CPU, aber Sie können nach der Erstellung `ocrEngine.IsGpuAvailable` prüfen. |
| **Wrong language pack** leads to garbled output | Setzen Sie immer `ocrEngine.Language` explizit; der Standard kann `Language.Unknown` sein. |
| **File path contains Unicode characters** | Verwenden Sie `Path.GetFullPath`, um zu normalisieren, oder fügen Sie unter Windows das Präfix `@\"\\\\?\\\"` hinzu, wenn Pfade die Länge überschreiten |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}