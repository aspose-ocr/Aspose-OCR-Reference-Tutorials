---
date: 2026-04-23
description: Verbessern Sie die OCR‑Genauigkeit mit Aspose OCR für .NET, indem Sie
  Rechtschreibprüfung, Unterstützung von OCR‑Sprachpaketen und benutzerdefinierte
  Wörterbücher nutzen, um die OCR‑Qualität bei gescannten Dokumenten zu steigern.
keywords:
- improve ocr accuracy
- ocr language pack
- process scanned documents
- boost ocr quality
- ocr spell checking
linktitle: Verbessern Sie die OCR‑Genauigkeit mit Rechtschreibprüfung in Bildern
second_title: Aspose.OCR .NET API
title: Verbessern Sie die OCR‑Genauigkeit durch Rechtschreibprüfung in Bildern
url: /de/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Verbessern Sie die OCR-Genauigkeit mit Rechtschreibprüfung in Bildern

Wenn Sie mit Optical Character Recognition (OCR) arbeiten, ist das Hauptziel, die **OCR-Genauigkeit zu verbessern**, sodass der extrahierte Text perfekt mit dem Originalbild übereinstimmt. Rechtschreibfehler, verrauschte Hintergründe und ungewöhnliche Schriftarten sind häufige Ursachen, die das Ergebnis verschlechtern. Durch die Kombination der integrierten Rechtschreibprüfungs‑Engine von Aspose.OCR mit dem umfangreichen OCR‑Sprachpaket können Sie die **OCR‑Qualität** für jedes gescannte Dokument deutlich **steigern**.

## Wie man die OCR-Genauigkeit mit Rechtschreibprüfung verbessert

In diesem Abschnitt führen wir den gesamten Workflow durch – vom Laden eines Bildes über die Anwendung der Rechtschreibprüfung bis hin zur Feinabstimmung der Ausgabe mit einem benutzerdefinierten Wörterbuch. Sie sehen reale Vorher‑Nachher‑Beispiele, erfahren, warum das für die Verarbeitung gescannter Dokumente wichtig ist, und entdecken Tipps, um das Beste aus der OCR‑Rechtschreibprüfungs‑Funktion herauszuholen.

## Schnelle Antworten
- **Was bewirkt die Rechtschreibprüfung für OCR?** Sie erkennt automatisch Rechtschreibfehler im OCR‑Ausgabe und ersetzt sie durch die wahrscheinlichsten korrekten Alternativen.  
- **Welche Bibliothek stellt diese Funktion bereit?** Aspose.OCR für .NET enthält eine sofort einsetzbare Rechtschreibprüfungs‑API.  
- **Benötige ich eine Internetverbindung?** Nein, die Rechtschreibprüfungs‑Engine funktioniert vollständig offline.  
- **Kann ich eigene Terminologie hinzufügen?** Ja, Sie können ein benutzerdefiniertes Wörterbuch bereitstellen, um domänenspezifische Wörter zu behandeln.  
- **Welche Sprachen werden unterstützt?** Siehe den Abschnitt „aspose ocr language support“ für Details.

## Was ist Rechtschreibprüfung in OCR?

Die Rechtschreibprüfung untersucht den vom OCR‑Engine zurückgegebenen Rohtext, identifiziert Token, die nicht mit bekannten Wörtern im ausgewählten Sprachwörterbuch übereinstimmen, und schlägt Korrekturen vor oder wendet sie an. Dieser Schritt ist entscheidend für die **Verbesserung der OCR‑Genauigkeit**, insbesondere bei der Verarbeitung gescannter Dokumente, Quittungen oder Formulare, bei denen OCR Zeichen missinterpretieren kann.

## Warum das Aspose OCR‑Sprachpaket verwenden?

Aspose.OCR wird mit umfangreichen Sprachpaketen geliefert und ermöglicht das Einbinden zusätzlicher Wörterbücher. Die Nutzung von **aspose ocr language support** bedeutet, dass Sie mehrsprachige Dokumente verarbeiten können, ohne eigene Parser zu schreiben, und Sie erhalten Zugriff auf sprachspezifische Regeln, die die Erkennungsqualität weiter verbessern.

## Voraussetzungen

Bevor wir in die Magie der Rechtschreibprüfung eintauchen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

- Aspose.OCR für .NET Bibliothek: Laden Sie die Aspose.OCR‑Bibliothek von der [release page](https://releases.aspose.com/ocr/net/) herunter und installieren Sie sie.
- Dokumentverzeichnis: Stellen Sie sicher, dass Sie ein vorgesehenes Verzeichnis für Ihre Dokumente haben. Ersetzen Sie `"Your Document Directory"` in den Code‑Snippets durch den tatsächlichen Pfad.

## Namespaces importieren

Beginnen wir damit, die erforderlichen Namespaces in Ihrem .NET‑Projekt zu importieren:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Schritt 1: Aspose.OCR initialisieren

Initialisieren Sie eine Instanz von Aspose.OCR, um den OCR‑Prozess zu starten.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Schritt 2: Bild erkennen

Als Nächstes erkennen Sie den Text in einem Bild mit Aspose.OCR. Hier ist ein Ausschnitt, der diesen Vorgang demonstriert:

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Schritt 3: Vor Korrektur

Rufen Sie das OCR‑Ergebnis vor der Korrektur ab, um es mit der korrigierten Version zu vergleichen.

```csharp
// Get result
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Schritt 4: Nach Korrektur

Wenden Sie die Rechtschreibprüfung an, um das korrigierte Ergebnis zu erhalten. Der folgende Code‑Ausschnitt veranschaulicht diesen Schritt:

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Schritt 5: Rechtschreibfehler und Vorschläge

Erhalten Sie eine Liste von Rechtschreibfehlern zusammen mit vorgeschlagenen Korrekturen mittels des folgenden Codes:

```csharp
// Get list of misspelled words with suggestions
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
	Console.Write("Word:" + word.Word);
	Console.Write(" StartPosition:" + word.StartPosition);
	Console.WriteLine(" Length:" + word.Length);
	Console.WriteLine("SuggestedWords:");
	foreach (var suggest in word.SuggestedWords)
	{
		Console.Write(suggest.Word + " ");
	}
	Console.WriteLine();
}
```

## Schritt 6: Benutzertext korrigieren

Korrigieren Sie spezifischen vom Benutzer bereitgestellten Text mit der Aspose.OCR‑Bibliothek:

```csharp
// Correct user text
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Schritt 7: Korrektur mit Benutzerwörterbuch

Verbessern Sie die Korrektur weiter, indem Sie ein benutzerdefiniertes Wörterbuch einbinden:

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Tipps zur Verbesserung der OCR‑Qualität

- **Wählen Sie das richtige OCR‑Sprachpaket** aus, das zum Quell‑Dokument passt. Die Verwendung von `Language.Eng` bei einem französischen Dokument reduziert die Genauigkeit drastisch.  
- **Bilder vorverarbeiten** (Entzerrung, Rauschunterdrückung, Kontrast erhöhen), bevor Sie sie an die OCR‑Engine übergeben; sauberere Bilder führen zu weniger Rechtschreibfehlern.  
- **Ein prägnantes Benutzerwörterbuch pflegen** – ein Wort pro Zeile – damit die Rechtschreibprüfung benutzerdefinierte Begriffe schnell finden kann, ohne große Stapel zu verlangsamen.  
- **Seiten stapelweise verarbeiten** bei mehrseitigen PDFs; das reduziert den Speicherverbrauch und beschleunigt die Rechtschreibprüfungs‑Phase.

## Häufige Probleme und Lösungen

| Problem | Warum es passiert | Wie zu beheben |
|-------|----------------|------------|
| Keine Vorschläge zurückgegeben | Das Sprachpaket ist nicht geladen oder der Text ist zu kurz. | Stellen Sie sicher, dass `RecognitionSettings(Language.Eng)` mit der Sprache des Quellbildes übereinstimmt und dass das OCR‑Ergebnis genügend Zeichen enthält. |
| Benutzerdefiniertes Wörterbuch nicht angewendet | Falscher Pfad oder Dateiformat. | Überprüfen Sie, dass `dictionary.txt` am angegebenen Ort existiert und ein Wort pro Zeile verwendet. |
| Rechtschreibprüfung verlangsamt bei großen Dokumenten | Die Verarbeitung jedes Wortes einzeln verursacht zusätzlichen Aufwand. | Verarbeiten Sie Seiten stapelweise oder erhöhen Sie die Speicherzuweisung, wenn Sie .NET Core verwenden. |

## Häufig gestellte Fragen

### Q1: Kann ich Aspose.OCR für andere Sprachen als Englisch verwenden?

A1: Ja, Aspose.OCR unterstützt mehrere Sprachen. Passen Sie die Spracheinstellungen entsprechend an.

### Q2: Wie integriere ich Aspose.OCR in mein .NET‑Projekt?

A2: Siehe die [documentation](https://reference.aspose.com/ocr/net/) für detaillierte Integrationsschritte.

### Q3: Gibt es eine Testversion von Aspose.OCR?

A3: Ja, Sie können die Funktionen mit der [free trial version](https://releases.aspose.com/) ausprobieren.

### Q4: Kann ich ein benutzerdefiniertes Wörterbuch für die Rechtschreibprüfung hochladen?

A4: Auf jeden Fall! Das Tutorial zeigt, wie man die Korrektur mit einem benutzerdefinierten Wörterbuch verbessern kann.

### Q5: Wo kann ich Unterstützung für Aspose.OCR erhalten?

A5: Besuchen Sie das [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) für Community‑Support und Anleitung.

---

**Zuletzt aktualisiert:** 2026-04-23  
**Getestet mit:** Aspose.OCR für .NET latest version  
**Autor:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}