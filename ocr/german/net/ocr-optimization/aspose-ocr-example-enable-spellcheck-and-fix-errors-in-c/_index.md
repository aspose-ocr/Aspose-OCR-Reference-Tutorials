---
category: general
date: 2026-03-07
description: Aspose OCR‑Beispiel, das zeigt, wie man die Rechtschreibprüfung aktiviert,
  ein benutzerdefiniertes Wörterbuch hinzufügt, Bild‑OCR lädt und OCR‑Fehler schnell
  behebt.
draft: false
keywords:
- aspose ocr example
- how to enable spellcheck
- how to add dictionary
- load image ocr
- how to fix ocr errors
language: de
og_description: Aspose OCR‑Beispiel, das Sie Schritt für Schritt durch das Aktivieren
  der Rechtschreibprüfung, das Hinzufügen eines benutzerdefinierten Wörterbuchs, das
  Laden eines Bildes für OCR und das Korrigieren häufiger OCR‑Fehler führt.
og_title: Aspose OCR‑Beispiel – Rechtschreibprüfung aktivieren & Fehler beheben
tags:
- Aspose
- OCR
- C#
- SpellCheck
title: Aspose OCR Beispiel – Rechtschreibprüfung aktivieren und Fehler in C# beheben
url: /de/net/ocr-optimization/aspose-ocr-example-enable-spellcheck-and-fix-errors-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Beispiel – Rechtschreibprüfung aktivieren und Fehler in C# beheben

Haben Sie jemals ein **Aspose OCR Beispiel** gebraucht, das nicht nur Text aus einem Bild liest, sondern auch diese lästigen Rechtschreibfehler bereinigt? Sie sind nicht allein. In vielen realen Projekten ist die rohe OCR‑Ausgabe voller Tippfehler, besonders wenn das Quellbild Schriftarten mit geringem Kontrast oder handschriftliche Notizen enthält.  

Die gute Nachricht? Mit Aspose.OCR können Sie **spellcheck aktivieren**, Ihr eigenes Wörterbuch einbinden und in nur wenigen Codezeilen einen bereinigten String erhalten. Im Folgenden sehen Sie genau **wie man spellcheck aktiviert**, **wie man ein Wörterbuch hinzufügt** und **wie man Bild‑OCR lädt**, sodass Sie endlich **OCR‑Fehler beheben** können, ohne sich die Haare zu raufen.

In diesem Tutorial behandeln wir alles, was Sie benötigen – von der NuGet‑Installation bis zu einem vollständigen, ausführbaren Programm, das korrigierten Text ausgibt. Am Ende haben Sie ein solides **Aspose OCR Beispiel**, das Sie direkt in jedes .NET‑Projekt einbinden können.

## Voraussetzungen

- .NET 6.0 SDK oder neuer (der Code funktioniert auch mit .NET Core und .NET Framework)
- Visual Studio 2022 oder jede C#‑kompatible IDE
- Eine Bilddatei (`typed_text.png`), die klaren, getippten englischen Text enthält
- Internetzugang, um das Aspose.OCR NuGet‑Paket zu beziehen

Keine weiteren Drittanbieter‑Bibliotheken sind erforderlich.

---

## Schritt 1 – Installieren des Aspose.OCR NuGet‑Pakets (Load Image OCR)

Bevor wir Code schreiben können, benötigen wir die Bibliothek, die die OCR‑Engine antreibt.

```bash
dotnet add package Aspose.OCR
```

> **Pro Tipp:** Wenn Sie Visual Studio verwenden, klicken Sie mit der rechten Maustaste auf das Projekt → *Manage NuGet Packages* → suchen Sie nach **Aspose.OCR** und klicken Sie auf *Install*.  

Die Installation des Pakets gibt Ihnen Zugriff auf `OcrEngine`, `ImageStream` und die integrierten Rechtschreibprüfungs‑Utilities, die wir später verwenden werden. Sobald das Paket vorhanden ist, sind Sie bereit, **load image OCR** zu starten.

## Schritt 2 – Erstellen der OCR‑Engine‑Instanz

Das Erstellen der Engine ist der erste konkrete Schritt in jedem **Aspose OCR Beispiel**. Denken Sie an `OcrEngine` als das Gehirn, das das Bitmap analysiert und Text ausgibt.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Step 2: Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

Der `OcrEngine`‑Konstruktor benötigt keine Parameter, was ihn für schnelle Prototypen praktisch und übersichtlich macht.

## Schritt 3 – Wie man spellcheck aktiviert (und warum es wichtig ist)

Roh‑OCR‑Ausgaben enthalten oft falsch erkannte Wörter wie „teh“ anstelle von „the“. Durch das Aktivieren der integrierten Rechtschreibprüfung lässt Aspose diese Fehler automatisch durch die wahrscheinlich korrekte Schreibweise ersetzen.

```csharp
// Step 3: Turn on spell checking and set the language to English
ocrEngine.Settings.SpellCheck.Enabled = true;
ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;
```

> **Warum spellcheck aktivieren?**  
> - **Genauigkeit:** Eine nachgelagerte Rechtschreibprüfung kann die Gesamtexaktheit des Textes bei gedruckten Dokumenten um 10‑15 % steigern.  
> - **Benutzererlebnis:** Sauberer Text bedeutet weniger nachträgliche Bereinigung, wenn Sie das Ergebnis in Suchindizes oder Analyse‑Pipelines einspeisen.

## Schritt 4 – Wie man ein Wörterbuch hinzufügt (benutzerdefinierte Wörter)

Manchmal kennt das Standard‑Wörterbuch Ihre Markennamen, Produktcodes oder fachspezifischen Jargon nicht. Hier kommt **how to add dictionary** ins Spiel.

```csharp
// Step 4: Add custom words that the spell checker should accept
ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
{
    "AsposeOCR",   // our library name
    "OCRify",      // a fictional product
    "CSharpify"    // another custom term
});
```

Sie können ein Array, eine Liste übergeben oder sogar aus einer Datei lesen, wenn Sie ein großes benutzerdefiniertes Vokabular haben. Die Rechtschreibprüfung wird diese Einträge nun als gültig behandeln und falsche Korrekturen verhindern.

## Schritt 5 – Bild für OCR laden (Load Image OCR)

Jetzt, wo die Engine konfiguriert ist, müssen wir sie auf das Bild zeigen, das wir lesen wollen. Der Helfer `ImageStream.FromFile` abstrahiert die Dateilesedetails.

```csharp
// Step 5: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");
```

> **Tipp:** Wenn sich Ihr Bild in einem Unterordner des Projekts befindet, setzen Sie die Eigenschaft *Copy to Output Directory* auf *Copy always*, damit der Pfad zur Laufzeit aufgelöst wird.

## Schritt 6 – Erkennung durchführen und OCR‑Fehler beheben

Wenn alles eingestellt ist, führt ein einziger Aufruf von `Recognize()` die OCR‑Pipeline aus, wendet die Rechtschreibprüfung an und speichert das bereinigte Ergebnis in `ocrEngine.Text`.

```csharp
// Step 6: Run OCR and let the spell checker clean the output
ocrEngine.Recognize();

// Step 7: Output the corrected text to the console
Console.WriteLine("Corrected text:");
Console.WriteLine(ocrEngine.Text);
```

### Erwartete Ausgabe

Angenommen, `typed_text.png` enthält den Satz `The quick brown fox jumps over teh lazy dog`, dann wird die Konsole anzeigen:

```
Corrected text:
The quick brown fox jumps over the lazy dog
```

Beachten Sie, wie „teh“ automatisch zu „the“ korrigiert wurde. Wenn Sie „OCRify“ zum benutzerdefinierten Wörterbuch hinzugefügt hätten und das Bild dieses Wort enthielte, würde die Engine es unverändert lassen.

---

## Vollständiges funktionierendes Beispiel (Copy‑Paste bereit)

Unten finden Sie das komplette Programm, das Sie in ein neues Konsolenprojekt einfügen können. Es enthält alle oben genannten Schritte sowie einige Kommentare zur Klarheit.

```csharp
// ---------------------------------------------------------------
// Aspose OCR Example – Enable Spellcheck and Fix Errors
// ---------------------------------------------------------------

using System;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable spell checking (how to enable spellcheck)
            ocrEngine.Settings.SpellCheck.Enabled = true;
            ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;

            // 3️⃣ Add custom words (how to add dictionary)
            ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
            {
                "AsposeOCR",
                "OCRify",
                "CSharpify"
            });

            // 4️⃣ Load the image (load image OCR)
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");

            // 5️⃣ Run OCR – this also fixes common OCR errors (how to fix ocr errors)
            ocrEngine.Recognize();

            // 6️⃣ Show the corrected result
            Console.WriteLine("Corrected text:");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

Speichern Sie dies als `Program.cs`, führen Sie `dotnet run` aus, und Sie sollten den korrigierten Satz in der Konsole sehen.

---

## Häufig gestellte Fragen & Sonderfälle

| Frage | Antwort |
|----------|--------|
| **Was ist, wenn das Bild ein mehrseitiges PDF ist?** | Aspose.OCR kann PDF‑Seiten als Bilder verarbeiten. Verwenden Sie `ocrEngine.Image = ImageStream.FromPdf("file.pdf", pageNumber: 1);` und iterieren Sie über die Seiten. |
| **Kann ich die Sprache auf etwas anderes als Englisch ändern?** | Natürlich. Setzen Sie `ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.French;` (oder jede unterstützte Sprache). |
| **Mein benutzerdefiniertes Wörterbuch ist riesig – wirkt sich das auf die Leistung aus?** | Das Hinzufügen von tausenden Wörtern verursacht einen kleinen anfänglichen Aufwand, aber die Suche ist dank eines Hash‑Sets O(1). Bei sehr großen Vokabularen sollten Sie sie einmalig beim Anwendungsstart laden. |
| **Was passiert, wenn die OCR‑Engine bei einem beschädigten Bild eine Ausnahme wirft?** | Umgeben Sie `Recognize()` mit einem try‑catch‑Block und prüfen Sie `ocrEngine.LastError`. Sie können außerdem die Bildabmessungen vorab mit `ocrEngine.Image.Width` und `Height` validieren. |
| **Benötige ich eine Lizenz für den Produktionseinsatz?** | Die kostenlose Evaluation funktioniert für Tests, aber eine kommerzielle Lizenz entfernt das Evaluations‑Wasserzeichen und schaltet die volle Leistung frei. |

---

## Fazit

Sie haben jetzt ein **vollständiges Aspose OCR Beispiel**, das **zeigt, wie man spellcheck aktiviert**, **wie man ein Wörterbuch hinzufügt**, **Bild‑OCR lädt** und **wie man OCR‑Fehler** auf saubere, produktionsbereite Weise behebt. Durch die Konfiguration der Rechtschreibprüfung und das Einbinden einer benutzerdefinierten Wortliste verbessern Sie die Qualität des extrahierten Textes erheblich, ohne eigene Nachbearbeitungs‑Logik schreiben zu müssen.

Bereit für den nächsten Schritt? Versuchen Sie, die Sprache auf Spanisch umzustellen, ein mehrseitiges PDF zu verarbeiten oder die Ausgabe in einen durchsuchbaren Azure Cognitive Search‑Index zu integrieren. Das gleiche Muster gilt – passen Sie einfach das Sprach‑Flag an und erweitern Sie ggf. das benutzerdefinierte Wörterbuch.

Wenn Ihnen diese Anleitung geholfen hat, geben Sie ihr einen Stern auf GitHub, teilen Sie sie mit Kolleg*innen oder hinterlassen Sie einen Kommentar unten. Viel Spaß beim Programmieren und möge Ihr OCR‑Ergebnis stets fehlerfrei sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}