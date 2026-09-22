---
category: general
date: 2026-02-13
description: Wie man Belege schnell mit Aspose OCR liest und den Betrag mit Regex
  extrahiert. Lernen Sie die schrittweise Verarbeitung von Belegen mit OCR.
draft: false
keywords:
- how to read receipt
- extract amount using regex
- regex find total
- process receipt with ocr
language: de
og_description: Wie man Quittungen in C# mit Aspose OCR und Regex liest. Dieser Leitfaden
  zeigt, wie man Quittungen mit OCR verarbeitet und den Gesamtbetrag extrahiert.
og_title: Wie man Quittungen in C# liest – Komplettes OCR‑ und Regex‑Tutorial
tags:
- OCR
- C#
- Regex
- Aspose
title: Wie man Quittungen in C# liest – OCR + Regex‑Anleitung
url: /de/net/text-recognition/how-to-read-receipt-in-c-ocr-regex-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Quittungen in C# liest – OCR + Regex Anleitung

Haben Sie sich jemals gefragt, **wie man Quittungen** aus Bildern liest, ohne jede Zeile manuell einzugeben? In vielen Kleinunternehmer‑Apps müssen Sie den Gesamtbetrag aus einem Foto einer Quittung extrahieren, und das manuell zu tun, macht die Automatisierung sinnlos. Die gute Nachricht? Mit Aspose OCR können Sie die Engine die schwere Arbeit erledigen lassen, dann findet ein einfacher regulärer Ausdruck den Gesamtbetrag. In diesem Tutorial gehen wir Schritt für Schritt durch **process receipt with OCR**, extrahieren den Betrag mit Regex und erhalten einen sofort nutzbaren Gesamtwert.

Sie werden ein vollständiges, ausführbares Beispiel sehen, erfahren, warum das Quittungs‑Sprachmodell wichtig ist, und erhalten Tipps zum Umgang mit Sonderfällen wie unterschiedlichen Währungssymbolen oder fehlenden „Total“-Bezeichnungen. Keine externen Dokumente sind erforderlich – alles, was Sie brauchen, finden Sie hier.

## Was Sie lernen werden

- Wie man Aspose OCR für die erkenntnis-spezifische Quittungs‑Erkennung einrichtet (das `Receipt`‑Sprachmodell korrigiert automatisch die Schräglage und reduziert das Rauschen des Bildes).  
- Wie man einen regulären Ausdruck anwendet, der **extract amount using regex** Muster verwendet, die für die meisten US‑artigen Quittungen funktionieren.  
- Wie man gängige Varianten wie „TOTAL“, „Total:“ oder „Grand Total – $12.34“ behandelt.  
- Wie man das Ergebnis sicher ausgibt und was zu tun ist, wenn das Muster nicht gefunden wird.  

**Voraussetzungen**: .NET 6+ (oder .NET Framework 4.7+), eine gültige Aspose OCR‑Lizenz oder Testversion und ein lokal gespeichertes Bild einer Quittung. Das ist alles – keine zusätzlichen NuGet‑Pakete außer Aspose.OCR.

---

## Schritt 1 – Aspose OCR installieren und das Projekt vorbereiten

### Warum das wichtig ist

Aspose OCR bietet ein speziell entwickeltes **process receipt with OCR**‑Modell, das weiß, wie man ein zerknittertes Blatt begradigt und Hintergrundgeräusche ignoriert. Die Verwendung des generischen Textmodells würde mehr Fehler erzeugen, besonders bei niedrig aufgelösten Scans.

### Code

```csharp
// Install the package via NuGet first:
//   dotnet add package Aspose.OCR
using Aspose.OCR;
using Aspose.OCR.Enums;
using System.Text.RegularExpressions;

// If you have a license file, load it now (optional but removes trial watermark)
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

> **Pro Tipp:** Bewahren Sie die Lizenzdatei außerhalb Ihres Quellcode‑Verzeichnisses auf, um versehentliche Commits zu vermeiden.

---

## Schritt 2 – OCR‑Engine für die Quittungserkennung konfigurieren

### Warum das wichtig ist

Das `Receipt`‑Sprachmodell enthält integrierte Schräglage‑ und Rauschkorrektur, was die Genauigkeit bei realen Quittungen, die oft gefaltet oder zerknittert sind, erheblich verbessert.

### Code

```csharp
// Step 2: Create and configure the OCR engine for receipt processing
var ocrEngine = new OcrEngine
{
    // Receipt model is optimized for invoices, grocery receipts, etc.
    Language = OcrLanguage.Receipt
};
```

---

## Schritt 3 – Text aus dem Quittungsbild erkennen

### Warum das wichtig ist

Sie benötigen den Rohtext, bevor Sie irgendeinen Regex anwenden können. Die Methode `RecognizeImage` gibt ein `OcrResult` zurück, das den gesamten String, Vertrauenswerte und mehr enthält, falls Sie diese später benötigen.

### Code

```csharp
// Step 3: Recognize text from the receipt image
// Replace the path with the actual location of your receipt file.
string receiptPath = @"C:\Receipts\sample-receipt.jpg";

OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

// Quick sanity check – print the whole OCR output (helps debugging)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(receiptResult.Text);
Console.WriteLine("===================\n");
```

**Erwartete OCR-Ausgabe (Beispiel)**  
```
Walmart Supercenter
123 Main St.
Anytown, USA
Date: 02/12/2026
Item A   $3.45
Item B   $7.89
Subtotal $11.34
Tax      $0.91
Total:   $12.25
Thank you!
```

---

## Schritt 4 – Einen Regex erstellen, um **Extract Amount Using Regex** zu extrahieren

### Warum das wichtig ist

Quittungen gibt es in vielen Formaten, aber das Wort „Total“ (oder eine nahe Variante) gefolgt von einem Dollarbetrag ist ein zuverlässiger Anker. Das untenstehende Muster toleriert optionale Leerzeichen, Doppelpunkte, Bindestriche und ein optionales `$`‑Zeichen.

### Code

```csharp
// Step 4: Use a regular expression to locate the total amount in the recognized text
string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
RegexOptions options = RegexOptions.IgnoreCase;

Match totalMatch = Regex.Match(receiptResult.Text, pattern, options);
```

**Erklärung des Musters**

| Teil | Bedeutung |
|------|-----------|
| `Total` | Sucht nach dem Wort „Total“ (case‑insensitive). |
| `\s*[:\-]?` | Erlaubt beliebige Leerzeichen, dann einen optionalen Doppelpunkt oder Bindestrich. |
| `\s*\$?` | Optionale Leerzeichen und optionales Dollarzeichen. |
| `(\d+(\.\d{2})?)` | Erfasst eine oder mehrere Ziffern, optional gefolgt von einem Dezimalpunkt und zwei Cent. |

---

## Schritt 5 – Den extrahierten Gesamtbetrag ausgeben oder fehlende Daten behandeln

### Warum das wichtig ist

Selbst das beste OCR kann ein Wort übersehen, besonders bei unscharfen Quittungen. Ein eleganter Fallback verhindert Abstürze und bietet Ihnen einen Ansatzpunkt für benutzerdefinierte Logik (z. B. den Benutzer um Bestätigung bitten).

### Code

```csharp
// Step 5: Output the extracted total, or indicate it wasn't found
if (totalMatch.Success)
{
    string amount = totalMatch.Groups[1].Value;
    Console.WriteLine($"Total: ${amount}");
}
else
{
    Console.WriteLine("Total amount not found. Consider reviewing the OCR output manually.");
}
```

**Beispielhafte Konsolenausgabe**

```
Total: $12.25
```

---

## Vollständiges funktionierendes Beispiel – Alle Schritte in einer Datei

Unten finden Sie ein einzelnes, eigenständiges Programm, das Sie in ein Konsolenprojekt kopieren können. Es enthält Kommentare, Fehlerbehandlung und das optionale Laden der Lizenz.

```csharp
// ---------------------------------------------------------------
// How to Read Receipt in C# – OCR + Regex (Complete Example)
// ---------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Enums;
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 0️⃣ Optional: Load your Aspose OCR license (remove trial watermark)
        try
        {
            var license = new Aspose.OCR.License();
            license.SetLicense("Aspose.OCR.lic"); // path to .lic file
        }
        catch (Exception ex)
        {
            Console.WriteLine("License not found – running in trial mode.");
        }

        // 1️⃣ Configure the OCR engine for receipt processing
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Receipt // receipt model = de‑skew + de‑noise
        };

        // 2️⃣ Path to the receipt image (change to your file)
        string receiptPath = @"YOUR_DIRECTORY/receipt.jpg";

        // 3️⃣ Perform OCR
        OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

        // 4️⃣ Debug: show full OCR text (helps when regex fails)
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(receiptResult.Text);
        Console.WriteLine("===================\n");

        // 5️⃣ Regex to **extract amount using regex** (find the total)
        string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
        Match totalMatch = Regex.Match(receiptResult.Text, pattern,
                                        RegexOptions.IgnoreCase);

        // 6️⃣ Output
        if (totalMatch.Success)
        {
            string amount = totalMatch.Groups[1].Value;
            Console.WriteLine($"Total: ${amount}");
        }
        else
        {
            Console.WriteLine("Total amount not found. You might need to adjust the regex or improve image quality.");
        }
    }
}
```

**Programm ausführen**

1. Erstellen Sie ein neues Konsolenprojekt (`dotnet new console -n ReceiptReader`).  
2. Fügen Sie das Aspose.OCR‑NuGet‑Paket hinzu (`dotnet add package Aspose.OCR`).  
3. Ersetzen Sie `YOUR_DIRECTORY/receipt.jpg` durch den tatsächlichen Pfad zu einem Quittungsbild.  
4. Bauen und führen Sie das Projekt aus (`dotnet run`).  

Sie sollten die OCR‑Ausgabe sehen, gefolgt von `Total: $xx.xx`, wenn alles passt.

---

## Umgang mit Sonderfällen & gängigen Variationen

### 1. Unterschiedliche Währungssymbole

If you deal with euros (€) or pounds (£), extend the pattern:

```csharp
string pattern = @"Total\s*[:\-]?\s*[$€£]?\s*(\d+(\.\d{2})?)";
```

### 2. Fehlende „Total“-Bezeichnung

Some receipts only show “Grand Total”. Add an alternation:

```csharp
string pattern = @"(?:Total|Grand\s*Total)\s*[:\-]?\s*[$]?\s*(\d+(\.\d{2})?)";
```

### 3. Mehrere Gesamtsummen (z. B. „Subtotal“ und „Total“)

If the regex matches the first occurrence, you may want the **last** match:

```csharp
MatchCollection matches = Regex.Matches(receiptResult.Text, pattern,
                                         RegexOptions.IgnoreCase);
Match last = matches.Count > 0 ? matches[matches.Count - 1] : null;
```

### 4. Niedrigauflösende Bilder

- Erhöhen Sie die DPI beim Scannen (`300 DPI` ist ein guter Wert).  
- Verarbeiten Sie das Bild mit einem einfachen Blur‑Reduktions‑Filter, bevor Sie es an Aspose übergeben (außerhalb des Umfangs dieses Leitfadens, aber lohnenswert).

---

## Pro‑Tipps für reale Projekte

- **Cache the OCR result** wenn Sie mehrere Felder (Steuer, Artikel usw.) extrahieren müssen – Sie zahlen die OCR‑Kosten nur einmal.  
- **Log the raw OCR text** in einer Datenbank; es wird zu einer wertvollen Prüfspur für strittige Ausgaben.  
- Beim Erstellen einer Web‑API **run OCR in a background worker**; es kann einige hundert Millisekunden dauern, was asynchron in Ordnung ist, aber für eine synchrone Anfrage nicht ideal.  
- **Validate the extracted amount** gegen Geschäftsregeln (z. B. Betrag muss > 0 sein) prüfen, bevor Sie ihn speichern.

---

## Fazit

Wir haben **how to read receipt** Bilder in C# mit Aspose OCR behandelt und anschließend **extract amount using regex**, um zuverlässig die Gesamtsumme zu finden. Durch die Nutzung des `Receipt`‑Sprachmodells erhalten Sie entkrümmten, rauschreduzierten Text, und ein kurzer regulärer Ausdruck bewältigt die meisten Formatierungs‑Eigenheiten. Das komplette Code‑Snippet oben kann in jedes .NET‑Konsolen‑ oder Service‑Projekt eingefügt werden, und die zusätzlichen Vorschläge für Sonderfälle bieten eine solide Grundlage für den Produktionseinsatz.

Bereit für den nächsten Schritt? Versuchen Sie, die Lösung zu erweitern, um einzelne Positionen zu extrahieren, die Steuer automatisch zu berechnen oder sie mit einer Ausgaben‑Tracking‑API zu integrieren. Und wenn Sie auf eine Quittung stoßen, die das Muster bricht, denken Sie daran, dass der **regex find total** Ansatz nur ein Ausgangspunkt ist – Sie können das Muster jederzeit an Ihre spezifische Region anpassen.

Viel Spaß beim Coden, und möge Ihre Quittungs‑Verarbeitung schnell, genau und vollständig automatisiert sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}