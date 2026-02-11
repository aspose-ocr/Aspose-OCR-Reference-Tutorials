---
date: 2025-12-25
description: Verbessern Sie die OCR‑Genauigkeit mit Aspose OCR für .NET, indem Sie
  Rechtschreibprüfung und Sprachunterstützung nutzen, um Rechtschreibfehler zu korrigieren
  und Wörterbücher für fehlerfreie Texterkennung anzupassen.
linktitle: Improve OCR Accuracy with Spell Checking in Images
second_title: Aspose.OCR .NET API
title: Verbessern Sie die OCR‑Genauigkeit durch Rechtschreibprüfung in Bildern
url: /de/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Verbessern Sie die OCR-Genauigkeit mit Rechtschreibprüfung in Bildern

## Einführung

Wenn Sie mit Optical Character Recognition (OCR) arbeiten, ist das Hauptziel, **die OCR‑Genauigkeit zu verbessern**, sodass der extrahierte Text perfekt mit dem Originalbild übereinstimmt. Rechtschreibfehler sind eine häufige Fehlerquelle, besonders wenn das Quellbild verrauscht ist oder ungewöhnliche Schriftarten enthält. Aspose.OCR für .NET bietet integrierte Rechtschreibprüfungs‑Funktionen, die nicht nur diese Fehler korrigieren, sondern Ihnen auch ermöglichen, die Engine mit benutzerdefinierten Wörterbüchern zu erweitern. In diesem Tutorial lernen Sie, wie Sie die Rechtschreibprüfung einsetzen, um OCR‑Ergebnisse zu steigern, sehen das Vorher‑Nachher‑Ergebnis und erfahren, wie Sie den Korrekturprozess an Ihre spezifischen Sprachbedürfnisse anpassen können.

## Schnelle Antworten
- **Was bewirkt die Rechtschreibprüfung für OCR?** Sie erkennt automatisch falsch geschriebene Wörter in der OCR‑Ausgabe und ersetzt sie durch die wahrscheinlichsten korrekten Alternativen.  
- **Welche Bibliothek stellt diese Funktion bereit?** Aspose.OCR für .NET enthält eine sofort einsetzbare Rechtschreibprüf‑API.  
- **Benötige ich eine Internetverbindung?** Nein, die Rechtschreibprüfungs‑Engine arbeitet vollständig offline.  
- **Kann ich eigene Fachbegriffe hinzufügen?** Ja, Sie können ein benutzerdefiniertes Nutzer‑Wörterbuch bereitstellen, um domänenspezifische Wörter zu behandeln.  
- **Welche Sprachen werden unterstützt?** Siehe den Abschnitt „aspose ocr language support“ für Details.

## Was ist Rechtschreibprüfung in OCR?

Die Rechtschreibprüfung untersucht den vom OCR‑Engine zurückgegebenen Rohtext, identifiziert Token, die nicht mit bekannten Wörtern im ausgewählten Sprachwörterbuch übereinstimmen, und schlägt Korrekturen vor oder wendet sie an. Dieser Schritt ist entscheidend, um **die OCR‑Genauigkeit zu verbessern**, besonders beim Verarbeiten von gescannten Dokumenten, Quittungen oder Formularen, bei denen OCR Zeichen missinterpretieren kann.

## Warum Aspose OCR Sprachunterstützung verwenden?

Aspose.OCR wird mit umfangreichen Sprachpaketen ausgeliefert und ermöglicht das Einbinden zusätzlicher Wörterbücher. Die Nutzung von **aspose ocr language support** bedeutet, dass Sie mehrsprachige Dokumente verarbeiten können, ohne eigene Parser zu schreiben, und Sie erhalten Zugriff auf sprachspezifische Regeln, die die Erkennungsqualität weiter verbessern.

## Voraussetzungen

Bevor wir in die Magie der Rechtschreibprüfung eintauchen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

- Aspose.OCR für .NET Bibliothek: Laden Sie die Aspose.OCR‑Bibliothek von der [Release‑Seite](https://releases.aspose.com/ocr/net/) herunter und installieren Sie sie.
- Dokumentverzeichnis: Stellen Sie sicher, dass Sie ein zugewiesenes Verzeichnis für Ihre Dokumente haben. Ersetzen Sie `"Your Document Directory"` in den Code‑Snippets durch den tatsächlichen Pfad.

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

Als Nächstes erkennen Sie den Text in einem Bild mit Aspose.OCR. Hier ein Snippet, das diesen Vorgang demonstriert:

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

Wenden Sie die Rechtschreibprüfung an, um das korrigierte Ergebnis zu erhalten. Das folgende Code‑Snippet veranschaulicht diesen Schritt:

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Schritt 5: Falsch geschriebene Wörter und Vorschläge

Erhalten Sie eine Liste falsch geschriebener Wörter zusammen mit vorgeschlagenen Korrekturen mittels des folgenden Codes:

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

Verbessern Sie die Korrektur weiter, indem Sie ein benutzerdefiniertes Nutzer‑Wörterbuch einbinden:

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Häufige Probleme und Lösungen

| Problem | Warum es passiert | Wie zu beheben |
|---------|-------------------|----------------|
| Keine Vorschläge zurückgegeben | Das Sprachpaket ist nicht geladen oder der Text ist zu kurz. | Stellen Sie sicher, dass `RecognitionSettings(Language.Eng)` mit der Sprache des Quellbildes übereinstimmt und dass das OCR‑Ergebnis genügend Zeichen enthält. |
| Benutzerdefiniertes Wörterbuch nicht angewendet | Falscher Pfad oder falsches Dateiformat. | Vergewissern Sie sich, dass `dictionary.txt` am angegebenen Ort existiert und ein Wort pro Zeile verwendet. |
| Rechtschreibprüfung verlangsamt große Dokumente | Die Verarbeitung jedes Wortes einzeln verursacht Overhead. | Verarbeiten Sie Seiten stapelweise oder erhöhen Sie die Speicherzuweisung, wenn Sie .NET Core verwenden. |

## Häufig gestellte Fragen

### Q1: Kann ich Aspose.OCR für andere Sprachen als Englisch verwenden?

A1: Ja, Aspose.OCR unterstützt mehrere Sprachen. Passen Sie die Spracheinstellungen entsprechend an.

### Q2: Wie integriere ich Aspose.OCR in mein .NET‑Projekt?

A2: Siehe die [Dokumentation](https://reference.aspose.com/ocr/net/) für detaillierte Integrationsschritte.

### Q3: Gibt es eine Testversion von Aspose.OCR?

A3: Ja, Sie können die Funktionen mit der [kostenlosen Testversion](https://releases.aspose.com/) erkunden.

### Q4: Kann ich ein benutzerdefiniertes Wörterbuch für die Rechtschreibprüfung hochladen?

A4: Absolut! Das Tutorial zeigt, wie Sie die Korrektur mit einem benutzerdefinierten Wörterbuch verbessern.

### Q5: Wo kann ich Unterstützung für Aspose.OCR erhalten?

A5: Besuchen Sie das [Aspose.OCR‑Forum](https://forum.aspose.com/c/ocr/16) für Community‑Support und Anleitung.

---

**Last Updated:** 2025-12-25  
**Tested With:** Aspose.OCR for .NET latest version  
**Author:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
