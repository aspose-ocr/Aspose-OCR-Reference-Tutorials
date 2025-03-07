---
title: Διόρθωση αποτελεσμάτων με ορθογραφικό έλεγχο στην αναγνώριση εικόνας OCR
linktitle: Διόρθωση αποτελεσμάτων με ορθογραφικό έλεγχο στην αναγνώριση εικόνας OCR
second_title: Aspose.OCR .NET API
description: Βελτιώστε την ακρίβεια OCR με το Aspose.OCR για .NET. Διορθώστε την ορθογραφία, προσαρμόστε τα λεξικά και επιτύχετε την αναγνώριση κειμένου χωρίς σφάλματα χωρίς κόπο.
weight: 13
url: /el/net/ocr-optimization/result-correction-with-spell-checking/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Διόρθωση αποτελεσμάτων με ορθογραφικό έλεγχο στην αναγνώριση εικόνας OCR

## Εισαγωγή

Στον τομέα της οπτικής αναγνώρισης χαρακτήρων (OCR), η επίτευξη ακριβών αποτελεσμάτων είναι ζωτικής σημασίας για την εξαγωγή ουσιαστικών πληροφοριών από εικόνες. Μια κοινή πρόκληση είναι η αντιμετώπιση των λανθασμένων λέξεων στη διαδικασία αναγνώρισης. Ευτυχώς, το Aspose.OCR για .NET παρέχει μια ισχυρή λύση για τη βελτίωση των αποτελεσμάτων OCR μέσω ορθογραφικού ελέγχου.

Αυτό το σεμινάριο θα σας καθοδηγήσει στη διαδικασία διόρθωσης αποτελεσμάτων με ορθογραφικό έλεγχο χρησιμοποιώντας το Aspose.OCR για .NET. Στο τέλος, θα είστε εξοπλισμένοι για να βελτιώσετε την ακρίβεια του κειμένου που προέρχεται από OCR, διασφαλίζοντας μια πιο εκλεπτυσμένη και χωρίς σφάλματα έξοδο.

## Προαπαιτούμενα

Πριν βουτήξουμε στη μαγεία του ορθογραφικού ελέγχου, βεβαιωθείτε ότι έχετε τις ακόλουθες προϋποθέσεις:

-  Aspose.OCR για .NET Library: Κάντε λήψη και εγκατάσταση της βιβλιοθήκης Aspose.OCR από το[σελίδα έκδοσης](https://releases.aspose.com/ocr/net/).

- Κατάλογος εγγράφων: Βεβαιωθείτε ότι έχετε έναν καθορισμένο κατάλογο για τα έγγραφά σας. Αντικαταστήστε το "Ο Κατάλογος Εγγράφων σας" στα αποσπάσματα κώδικα με την πραγματική διαδρομή.

## Εισαγωγή χώρων ονομάτων

Ας ξεκινήσουμε εισάγοντας τους απαραίτητους χώρους ονομάτων στο έργο σας .NET:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Βήμα 1: Αρχικοποιήστε το Aspose.OCR

Ξεκινήστε μια παρουσία του Aspose.OCR για να ξεκινήσετε τη διαδικασία OCR.

```csharp
// Η διαδρομή προς τον κατάλογο εγγράφων.
string dataDir = "Your Document Directory";

// Αρχικοποιήστε μια παρουσία του AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Βήμα 2: Αναγνώριση εικόνας

Στη συνέχεια, αναγνωρίστε το κείμενο σε μια εικόνα χρησιμοποιώντας το Aspose.OCR. Ακολουθεί ένα απόσπασμα που δείχνει αυτή τη διαδικασία:

```csharp
// Αναγνώριση εικόνας
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Βήμα 3: Πριν από τη διόρθωση

Ανακτήστε το αποτέλεσμα OCR πριν από τη διόρθωση για σύγκριση με τη διορθωμένη έκδοση.

```csharp
// Λάβετε αποτέλεσμα
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Βήμα 4: Μετά τη διόρθωση

Εφαρμόστε ορθογραφικό έλεγχο για να λάβετε το διορθωμένο αποτέλεσμα. Το ακόλουθο απόσπασμα κώδικα απεικονίζει αυτό το βήμα:

```csharp
// Λάβετε διορθωμένο αποτέλεσμα
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Βήμα 5: Ανορθόγραφες λέξεις και προτάσεις

Λάβετε μια λίστα με ανορθόγραφες λέξεις μαζί με προτεινόμενες διορθώσεις χρησιμοποιώντας τον ακόλουθο κώδικα:

```csharp
// Λάβετε λίστα με ανορθόγραφες λέξεις με προτάσεις
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

## Βήμα 6: Διορθώστε το κείμενο χρήστη

Διορθώστε συγκεκριμένο κείμενο που παρέχεται από τον χρήστη χρησιμοποιώντας τη βιβλιοθήκη Aspose.OCR:

```csharp
// Σωστό κείμενο χρήστη
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Βήμα 7: Διόρθωση με το λεξικό χρήστη

Βελτιώστε περαιτέρω τη διόρθωση ενσωματώνοντας ένα προσαρμοσμένο λεξικό χρήστη:

```csharp
// Λάβετε διορθωμένο αποτέλεσμα με το λεξικό χρήστη
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## συμπέρασμα

Συγχαρητήρια! Πραγματοποιήσατε επιτυχή πλοήγηση στις δυνατότητες ορθογραφικού ελέγχου του Aspose.OCR για .NET. Αυτή η δυνατότητα σάς δίνει τη δυνατότητα να βελτιώσετε τα αποτελέσματα OCR, διασφαλίζοντας την ακρίβεια και εξαλείφοντας τα σφάλματα.

## Συχνές ερωτήσεις

### Ε1: Μπορώ να χρησιμοποιήσω το Aspose.OCR για άλλες γλώσσες εκτός από τα αγγλικά;

A1: Ναι, το Aspose.OCR υποστηρίζει πολλές γλώσσες. Προσαρμόστε τις ρυθμίσεις γλώσσας ανάλογα.

### Ε2: Πώς μπορώ να ενσωματώσω το Aspose.OCR στο έργο μου .NET;

 A2: Ανατρέξτε στο[τεκμηρίωση](https://reference.aspose.com/ocr/net/) για λεπτομερή βήματα ολοκλήρωσης.

### Ε3: Υπάρχει διαθέσιμη δοκιμαστική έκδοση για το Aspose.OCR;

 A3: Ναι, μπορείτε να εξερευνήσετε τις δυνατότητες με το[δωρεάν δοκιμαστική έκδοση](https://releases.aspose.com/).

### Ε4: Μπορώ να ανεβάσω ένα προσαρμοσμένο λεξικό για ορθογραφικό έλεγχο;

Α4: Απολύτως! Το σεμινάριο δείχνει πώς να βελτιώσετε τη διόρθωση χρησιμοποιώντας ένα λεξικό που παρέχεται από το χρήστη.

### Ε5: Πού μπορώ να αναζητήσω υποστήριξη για το Aspose.OCR;

 A5: Επισκεφθείτε το[Aspose.OCR φόρουμ](https://forum.aspose.com/c/ocr/16) για κοινοτική υποστήριξη και καθοδήγηση.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
