---
category: general
date: 2026-04-11
description: Erfahren Sie, wie Sie OCR in Aspose OCR für C# deaktivieren, um offline
  zu arbeiten, Text aus einem Bild ohne Internet zu extrahieren und das Bild für OCR
  korrekt zu laden.
draft: false
keywords:
- how to disable OCR
- extract text from image
- load image for OCR
- offline OCR C#
- Aspose OCR resources
language: de
og_description: Wie man OCR in Aspose OCR für C# deaktiviert und offline ausführt,
  Text aus einem Bild extrahiert, ohne Internet zu benötigen, und das Bild für OCR
  einfach lädt.
og_title: Wie man OCR in C# deaktiviert – Offline Aspose OCR Leitfaden
tags:
- C#
- OCR
- Aspose
- Offline Processing
title: Wie man OCR in C# deaktiviert – Offline Aspose OCR‑Leitfaden
url: /de/net/ocr-configuration/how-to-disable-ocr-in-c-offline-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in C# deaktiviert – Offline Aspose OCR‑Leitfaden

Haben Sie sich jemals gefragt, **wie man OCR deaktiviert**, wenn Sie eine wirklich offline Lösung benötigen? Vielleicht bauen Sie eine sichere Desktop‑App, die nicht auf eine Netzwerkverbindung angewiesen sein kann, oder Sie möchten einfach unerwartete Downloads vermeiden. In beiden Fällen gibt es gute Nachrichten: Aspose OCR lässt sich so konfigurieren, dass das automatische Abrufen von Ressourcen ausgeschaltet wird, Sie können einen lokalen Ordner angeben und alles bleibt on‑premises. In diesem Tutorial erfahren Sie außerdem, wie Sie **Text aus Bild**‑Dateien **extrahieren** und **ein Bild für OCR laden** können – ohne Probleme.

Wir gehen ein komplettes, sofort ausführbares Beispiel durch, das jeden Schritt zeigt – von der Initialisierung der Engine bis zum Ausgeben des erkannten japanischen Textes. Keine externen Dokumente, keine versteckte Magie; nur reiner C#‑Code, den Sie noch heute in Ihr Projekt übernehmen können. Am Ende wissen Sie, warum das Deaktivieren der Auto‑Download‑Funktion wichtig ist, wie Sie den Ressourcen‑Pfad setzen und welche Fallstricke zu beachten sind.

## Voraussetzungen

- .NET 6.0 (oder eine aktuelle .NET‑Version) auf Ihrem Rechner installiert.  
- Aspose.OCR für .NET NuGet‑Paket (`Install-Package Aspose.OCR`).  
- Ein Ordner, der bereits die benötigten Sprachressourcen enthält (z. B. das japanische Modell).  
- Eine Bilddatei (`japan_doc.png`), die Sie per OCR verarbeiten möchten.  

Falls Ihnen die Sprachpakete fehlen, holen Sie sie einmalig vom Aspose‑Portal, entpacken Sie sie in einen Ordner wie `AsposeOCRResources` und Sie sind fertig. Sobald Sie die Auto‑Download‑Funktion deaktiviert haben, erfolgen keine weiteren Downloads mehr.

![Wie man OCR offline deaktiviert](/images/how-to-disable-ocr.png "Illustration zum Deaktivieren von OCR")

## Schritt 1 – OCR‑Engine‑Instanz erstellen  

Als erstes instanziieren Sie `OcrEngine`. Dieses Objekt ist das „Gehirn“, das Ihr Bild liest.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Warum das wichtig ist:** Ohne eine Engine können Sie nichts konfigurieren. Das Objekt enthält alle Einstellungen, einschließlich des entscheidenden Flags, das der Bibliothek sagt, ob sie das Internet kontaktieren darf.

## Schritt 2 – Automatisches Herunterladen von Ressourcen deaktivieren  

Standardmäßig versucht Aspose OCR, fehlende Sprachdateien bei Bedarf nachzuladen. Um alles offline zu halten, setzen Sie den Schalter `AutoDownloadResources` auf `false`.

```csharp
        // Step 2: Disable automatic resource download to work offline
        ocrEngine.Settings.AutoDownloadResources = false;
```

> **Pro‑Tipp:** Das Ausschalten spart nicht nur Privatsphäre, sondern beschleunigt auch den ersten Erkennungsdurchlauf, weil die Engine nicht nach Updates sucht.

## Schritt 3 – Auf Ihren lokalen Ressourcen‑Ordner verweisen  

Jetzt teilen Sie der Engine mit, wo die vorab heruntergeladenen Sprachpakete liegen. Das ist der Pfad, den Sie in den Voraussetzungen eingerichtet haben.

```csharp
        // Step 3: Point the engine to the folder containing pre‑downloaded resources
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";
```

> **Was schiefgehen kann:** Ist der Pfad falsch oder fehlt die benötigte Sprachdatei, wirft die Engine eine `ResourceNotFoundException`. Prüfen Sie die Ordner‑Schreibweise und ob das japanische Modell (`jpn.traineddata`) vorhanden ist.

## Schritt 4 – Lokales Sprachmodell auswählen  

Wählen Sie die Sprache, die Sie tatsächlich auf der Festplatte haben. In unserem Beispiel verwenden wir Japanisch, Sie können aber `Language.Japanese` durch jede andere heruntergeladene Sprache ersetzen.

```csharp
        // Step 4: Select the language model that is available locally
        ocrEngine.Settings.Language = Language.Japanese;
```

> **Randfall:** Einige Sprachen benötigen zusätzliche Wörterbücher (z. B. Chinesisch). Stellen Sie sicher, dass diese Hilfsdateien ebenfalls im selben Ressourcen‑Ordner liegen.

## Schritt 5 – Bild für OCR laden  

Hier **laden wir das Bild für OCR**. Die Methode `ImageStream.FromFile` liest die Datei in einen Stream, den Aspose verarbeiten kann.

```csharp
        // Step 5: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/japan_doc.png");
```

> **Tipp:** Unterstützte Formate sind PNG, JPEG, BMP und TIFF. Wenn Sie PDFs verarbeiten müssen, konvertieren Sie jede Seite zuerst in ein Bild.

## Schritt 6 – Erkennungsprozess starten  

Jetzt liest die Engine die Pixel und versucht, sie in Text umzuwandeln.

```csharp
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Warum dieser Schritt langsam sein kann:** OCR ist CPU‑intensiv, besonders bei hochauflösenden Bildern. Wenn die Performance kritisch ist, skalieren Sie das Bild vor der Erkennung herunter.

## Schritt 7 – Extrahierten Text ausgeben  

Abschließend **extrahieren wir Text aus dem Bild** und geben ihn in der Konsole aus.

```csharp
        // Step 7: Output the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Das Ausführen des Programms sollte die japanischen Zeichen aus `japan_doc.png` anzeigen. Wenn alles korrekt eingerichtet ist, sehen Sie einen sauberen Block Unicode‑Text in Ihrer Konsole.

### Erwartete Ausgabe

```
これはサンプルの日本語テキストです。
```

(Ihre tatsächliche Ausgabe hängt vom Inhalt des Bildes ab.)

## Häufige Fallstricke & wie man sie vermeidet  

| Problem | Warum es passiert | Lösung |
|-------|----------------|-----|
| **Fehlende Sprachdatei** | `AutoDownloadResources` ist deaktiviert, sodass die Engine sie nicht nachladen kann. | Prüfen Sie, ob `ResourcesPath` auf den Ordner mit `jpn.traineddata` zeigt. |
| **Falscher Bildpfad** | `ImageStream.FromFile` wirft `FileNotFoundException`. | Verwenden Sie absolute Pfade oder stellen Sie sicher, dass das Arbeitsverzeichnis korrekt ist. |
| **Nicht unterstütztes Bildformat** | Aspose liest nur bestimmte Formate. | Konvertieren Sie Ihr Bild vor dem Aufruf von `FromFile` zu PNG oder JPEG. |
| **Speicherüberlauf bei großen Bildern** | OCR lädt das gesamte Bild in den Speicher. | Bildgröße reduzieren oder in Kacheln verarbeiten, bzw. das Speicherlimit des Prozesses erhöhen. |

## Beispiel erweitern  

- **Batch‑Verarbeitung:** Durchlaufen Sie ein Verzeichnis mit Bildern, rufen Sie denselben Erkennungscode auf und schreiben Sie jedes Ergebnis in eine separate `.txt`‑Datei.  
- **Andere Sprachen:** Ersetzen Sie `Language.Japanese` durch `Language.English` (oder eine andere), nachdem Sie die entsprechenden Ressourcendateien bereitgestellt haben.  
- **Benutzerdefinierte Vorverarbeitung:** Nutzen Sie Aspose.Imaging, um das Bild zu deskewen oder den Kontrast zu verbessern, bevor Sie OCR ausführen – das erhöht die Genauigkeit.

## Fazit  

Sie wissen jetzt, **wie man OCR in Aspose OCR für C# deaktiviert** und komplett offline betreibt. Indem Sie `AutoDownloadResources` auf `false` setzen, die Engine auf einen lokalen Ressourcen‑Ordner verweisen und das **Bild für OCR korrekt laden**, können Sie zuverlässig **Text aus Bild** extrahieren, ohne jemals das Internet zu berühren. Dieses Vorgehen ist ideal für sichere Umgebungen, CI‑Pipelines oder jede Situation, in der Netzwerkzugriff eingeschränkt ist.

Bereit für den nächsten Schritt? Versuchen Sie, einen ganzen Ordner gescannter PDFs zu verarbeiten, experimentieren Sie mit verschiedenen Sprachpaketen oder integrieren Sie das OCR‑Ergebnis in eine durchsuchbare Datenbank. Die heute erstellte Offline‑Konfiguration bildet ein solides Fundament für jede On‑Premises‑Dokumenten‑Verarbeitungs‑Workflow.

Viel Spaß beim Coden und hinterlassen Sie gern einen Kommentar, falls Sie auf Probleme stoßen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}