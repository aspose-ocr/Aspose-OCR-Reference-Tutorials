---
title: Ergebniskorrektur mit Rechtschreibprüfung in der OCR-Bilderkennung
linktitle: Ergebniskorrektur mit Rechtschreibprüfung in der OCR-Bilderkennung
second_title: Aspose.OCR .NET API
description: Verbessern Sie die OCR-Genauigkeit mit Aspose.OCR für .NET. Korrigieren Sie die Rechtschreibung, passen Sie Wörterbücher an und erreichen Sie mühelos eine fehlerfreie Texterkennung.
weight: 13
url: /de/net/ocr-optimization/result-correction-with-spell-checking/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ergebniskorrektur mit Rechtschreibprüfung in der OCR-Bilderkennung

## Einführung

Im Bereich der optischen Zeichenerkennung (OCR) ist die Erzielung genauer Ergebnisse von entscheidender Bedeutung, um aus Bildern aussagekräftige Informationen zu extrahieren. Eine häufige Herausforderung ist der Umgang mit falsch geschriebenen Wörtern im Erkennungsprozess. Glücklicherweise bietet Aspose.OCR für .NET eine leistungsstarke Lösung zur Verbesserung der OCR-Ergebnisse durch Rechtschreibprüfung.

Dieses Tutorial führt Sie durch den Prozess der Ergebniskorrektur mit Rechtschreibprüfung mit Aspose.OCR für .NET. Am Ende sind Sie in der Lage, die Genauigkeit von OCR-abgeleitetem Text zu verbessern und so eine verfeinerte und fehlerfreie Ausgabe zu gewährleisten.

## Voraussetzungen

Bevor wir uns mit der Magie der Rechtschreibprüfung befassen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

-  Aspose.OCR für .NET-Bibliothek: Laden Sie die Aspose.OCR-Bibliothek von herunter und installieren Sie sie[Release-Seite](https://releases.aspose.com/ocr/net/).

- Dokumentenverzeichnis: Stellen Sie sicher, dass Sie über ein bestimmtes Verzeichnis für Ihre Dokumente verfügen. Ersetzen Sie „Ihr Dokumentverzeichnis“ in den Codefragmenten durch den tatsächlichen Pfad.

## Namespaces importieren

Beginnen wir mit dem Importieren der erforderlichen Namespaces in Ihr .NET-Projekt:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Schritt 1: Aspose.OCR initialisieren

Initialisieren Sie eine Instanz von Aspose.OCR, um den OCR-Prozess zu starten.

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "Your Document Directory";

// Initialisieren Sie eine Instanz von AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Schritt 2: Bild erkennen

Als nächstes erkennen Sie den Text in einem Bild mit Aspose.OCR. Hier ist ein Ausschnitt, der diesen Prozess demonstriert:

```csharp
// Bild erkennen
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Schritt 3: Vor der Korrektur

Rufen Sie das OCR-Ergebnis vor der Korrektur ab, um es mit der korrigierten Version zu vergleichen.

```csharp
// Ergebnis erhalten
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Schritt 4: Nach der Korrektur

Führen Sie eine Rechtschreibprüfung durch, um das korrigierte Ergebnis zu erhalten. Der folgende Codeausschnitt veranschaulicht diesen Schritt:

```csharp
// Korrigiertes Ergebnis erhalten
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Schritt 5: Falsch geschriebene Wörter und Vorschläge

Rufen Sie mithilfe des folgenden Codes eine Liste falsch geschriebener Wörter mit Korrekturvorschlägen ab:

```csharp
// Erhalten Sie eine Liste falsch geschriebener Wörter mit Vorschlägen
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

## Schritt 6: Korrigieren Sie den Benutzertext

Korrigieren Sie bestimmten vom Benutzer bereitgestellten Text mithilfe der Aspose.OCR-Bibliothek:

```csharp
// Korrekter Benutzertext
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Schritt 7: Korrektur mit Benutzerwörterbuch

Verbessern Sie die Korrektur noch weiter, indem Sie ein benutzerdefiniertes Benutzerwörterbuch integrieren:

```csharp
// Erhalten Sie korrigierte Ergebnisse mit dem Benutzerwörterbuch
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Abschluss

Glückwunsch! Sie haben die Rechtschreibprüfungsfunktionen von Aspose.OCR für .NET erfolgreich bewältigt. Mit dieser Funktion können Sie OCR-Ergebnisse verfeinern, um Genauigkeit sicherzustellen und Fehler zu vermeiden.

## FAQs

### F1: Kann ich Aspose.OCR für andere Sprachen als Englisch verwenden?

A1: Ja, Aspose.OCR unterstützt mehrere Sprachen. Passen Sie die Spracheinstellungen entsprechend an.

### F2: Wie integriere ich Aspose.OCR in mein .NET-Projekt?

 A2: Siehe[Dokumentation](https://reference.aspose.com/ocr/net/) für detaillierte Integrationsschritte.

### F3: Gibt es eine Testversion für Aspose.OCR?

 A3: Ja, Sie können die Funktionen mit dem erkunden[kostenlose Testversion](https://releases.aspose.com/).

### F4: Kann ich ein benutzerdefiniertes Wörterbuch zur Rechtschreibprüfung hochladen?

A4: Auf jeden Fall! Das Tutorial zeigt, wie Sie die Korrektur mithilfe eines vom Benutzer bereitgestellten Wörterbuchs verbessern können.

### F5: Wo kann ich Unterstützung für Aspose.OCR suchen?

 A5: Besuchen Sie die[Aspose.OCR-Forum](https://forum.aspose.com/c/ocr/16) für gemeinschaftliche Unterstützung und Anleitung.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
