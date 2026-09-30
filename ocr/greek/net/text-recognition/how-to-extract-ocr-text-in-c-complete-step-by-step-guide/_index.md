---
category: general
date: 2025-12-30
description: Μάθετε πώς να εξάγετε κείμενο OCR από εικόνες χρησιμοποιώντας C#. Αυτό
  το σεμινάριο καλύπτει την εξαγωγή κειμένου από αρχεία εικόνας, την ανάγνωση κειμένου
  από PNG και περιλαμβάνει ένα πλήρες σεμινάριο OCR σε C#.
draft: false
keywords:
- how to extract ocr
- extract text from image
- read text from png
- c# ocr tutorial
language: el
og_description: Πώς να εξάγετε κείμενο OCR από εικόνες χρησιμοποιώντας C#. Ακολουθήστε
  αυτό το tutorial OCR σε C# για να διαβάσετε κείμενο από αρχεία PNG και να εξάγετε
  κείμενο από εικόνα χωρίς κόπο.
og_title: Πώς να εξάγετε κείμενο OCR σε C# – Πλήρης οδηγός
tags:
- OCR
- C#
- Aspose
title: Πώς να εξάγετε κείμενο OCR σε C# – Πλήρης οδηγός βήμα‑βήμα
url: /el/net/text-recognition/how-to-extract-ocr-text-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξάγετε Κείμενο OCR σε C# – Ολοκληρωμένος Οδηγός Βήμα‑Βήμα

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε OCR** από μια σαρωμένη φόρμα χωρίς να ξοδεύετε ώρες γράφοντας προσαρμοσμένους αναλυτές; Δεν είστε οι μόνοι. Σε πολλά πραγματικά έργα—όπως επεξεργασία τιμολογίων, σάρωση διαβατηρίων ή ψηφιοποίηση παλιών αρχείων—χρειάζεστε έναν αξιόπιστο τρόπο για να αποσύρετε κείμενο από ένα αρχείο εικόνας. Τα καλά νέα; Με το Aspose.OCR μπορείτε να το κάνετε με λίγες μόνο γραμμές C#.

Σε αυτό το tutorial θα περάσουμε από ένα **c# ocr tutorial** που δείχνει πώς να **εξάγετε κείμενο από εικόνα**, συγκεκριμένα PNG, και πώς να **διαβάσετε κείμενο από png** διατηρώντας μεταδεδομένα ανά χαρακτήρα. Στο τέλος θα έχετε μια έτοιμη για εκτέλεση εφαρμογή console που εκτυπώνει μια ωραία μορφοποιημένη συμβολοσειρά JSON με όλα όσα κατέγραψε το Aspose.

> **Prerequisites**  
> • .NET 6.0 ή νεότερο εγκατεστημένο  
> • Visual Studio 2022 (ή οποιοδήποτε IDE προτιμάτε)  
> • Πακέτο NuGet Aspose.OCR for .NET (`Aspose.OCR`)  

Αν έχετε καλύψει αυτά τα βασικά, ας βουτήξουμε.

---

## Πώς να Εξάγετε Κείμενο OCR από Εικόνα σε C# – Ρύθμιση του Έργου

Πριν ξεκινήσουμε τον κώδικα, χρειαζόμαστε ένα καθαρό έργο και τη σωστή εξάρτηση.

```bash
# Create a new console app
dotnet new console -n OcrDemo
cd OcrDemo

# Add Aspose.OCR package
dotnet add package Aspose.OCR
```

> **Pro tip:** Αν χρησιμοποιείτε Visual Studio, μπορείτε να προσθέσετε το πακέτο μέσω του UI του NuGet Package Manager—απλώς αναζητήστε “Aspose.OCR”.

Μόλις εγκατασταθεί το πακέτο, ανοίξτε το `Program.cs`. Θα δείτε τη προεπιλεγμένη μέθοδο `Main` έτοιμη να γεμίσει.

---

## Βήμα 1 – Αρχικοποίηση του OCR Engine (Γιατί Είναι Σημαντικό)

Η μηχανή OCR είναι η καρδιά της διαδικασίας. Η αρχικοποίησή της λέει στο Aspose ποια μοντέλα γλώσσας σκοπεύετε να χρησιμοποιήσετε αργότερα.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create the OCR engine instance
            var ocrEngine = new OcrEngine();

            // The rest of the steps will follow here...
        }
    }
}
```

*Γιατί αυτό το βήμα;*  
Η δημιουργία ενός αντικειμένου `OcrEngine` διανέμει τους πόρους που απαιτούνται για την ανάλυση εικόνας. Χωρίς αυτό, δεν υπάρχει κάτι στο οποίο να τροφοδοτήσετε την εικόνα, και η βιβλιοθήκη δεν μπορεί να εφαρμόσει τους εξελιγμένους αλγόριθμους αναγνώρισης προτύπων.

---

## Βήμα 2 – Φόρτωση του Μοντέλου Αγγλικής Γλώσσας (Extract Text from Image)

Το Aspose παρέχει πολλαπλά πακέτα γλωσσών. Η φόρτωση του σωστού βελτιώνει δραματικά την ακρίβεια.

```csharp
// Step 2: Load the English language model
ocrEngine.LoadLanguage(LanguageModel.English);
```

Αν χρειαστεί ποτέ να **διαβάσετε κείμενο από png** που περιέχει άλλη γλώσσα, απλώς αντικαταστήστε το `LanguageModel.English` με την κατάλληλη τιμή enum (π.χ., `LanguageModel.French`). Αυτή η ευελιξία είναι ο λόγος που το Aspose είναι δημοφιλές για παγκόσμιες εφαρμογές.

---

## Βήμα 3 – Αναγνώριση Κειμένου από το PNG Αρχείο Σας (Read Text from PNG)

Τώρα δείχνουμε στη μηχανή την πραγματική εικόνα. Για αυτή τη demo, τοποθετήστε ένα PNG με όνομα `form_image.png` μέσα σε φάκελο που ονομάζεται `YOUR_DIRECTORY` σε σχέση με το εκτελέσιμο.

```csharp
// Step 3: Perform OCR on the image
var recognitionResult = ocrEngine.Recognize("YOUR_DIRECTORY/form_image.png");
```

> **Τι γίνεται αν το αρχείο δεν βρεθεί;**  
> Η μέθοδος `Recognize` ρίχνει μια `FileNotFoundException`. Τυλίξτε την κλήση σε μπλοκ try‑catch αν θέλετε πιο ευγενική διαχείριση σφαλμάτων σε παραγωγικό περιβάλλον.

---

## Βήμα 4 – Μετατροπή του Αποτελέσματος σε Καλασχεδιασμένο JSON (Why JSON?)

Το Aspose επιστρέφει ένα πλούσιο αντικείμενο `RecognitionResult` που περιέχει όχι μόνο το ακατέργαστο κείμενο αλλά και πλαίσια περιορισμού, βαθμούς εμπιστοσύνης και πληροφορίες γραμμής. Η σειριοποίηση σε JSON το κάνει εύκολο για καταγραφή, αποθήκευση ή αποστολή μέσω API.

```csharp
// Step 4: Serialize the result to a nicely indented JSON string
string json = JsonResult.FromRecognitionResult(recognitionResult)
                        .ToString(prettyPrint: true);

// Optional: Write the JSON to a file for later inspection
System.IO.File.WriteAllText("ocr_output.json", json);
```

Η σημαία `prettyPrint: true` προσθέτει αλλαγές γραμμής και εσοχές, κάτι τέλειο για αποσφαλμάτωση. Αν χρειάζεστε μόνο το ακατέργαστο κείμενο, μπορείτε απλώς να χρησιμοποιήσετε `recognitionResult.Text`.

---

## Βήμα 5 – Εμφάνιση του JSON Αποτελέσματος (Seeing the Result)

Τέλος, ας εκτυπώσουμε το JSON στην κονσόλα ώστε να επαληθεύσετε ότι όλα λειτούργησαν.

```csharp
// Step 5: Output the JSON to the console
Console.WriteLine(json);
```

Τρέχοντας το πρόγραμμα τώρα θα πρέπει να παραχθεί έξοδος παρόμοια με το παρακάτω απόσπασμα (συντομευμένο για συντομία):

```json
{
  "Text": "John Doe\n123 Main St\nAnytown, USA",
  "Characters": [
    {
      "Value": "J",
      "Confidence": 0.99,
      "Bounds": { "X": 12, "Y": 8, "Width": 10, "Height": 14 }
    },
    // ... more character objects ...
  ],
  "Lines": [
    { "Text": "John Doe", "Confidence": 0.98 },
    { "Text": "123 Main St", "Confidence": 0.97 },
    { "Text": "Anytown, USA", "Confidence": 0.96 }
  ]
}
```

Παρατηρήστε τα μεταδεδομένα ανά χαρακτήρα—αυτή είναι η επιπλέον αξία που παρέχει το Aspose σε σχέση με πολλές δωρεάν βιβλιοθήκες OCR. Τώρα μπορείτε να φιλτράρετε χαρακτήρες χαμηλής εμπιστοσύνης ή να χαρτογραφήσετε το κείμενο πίσω στην αρχική εικόνα για επισήμανση.

---

## Πλήρες Παράδειγμα Εργασίας (All Steps in One Place)

Παρακάτω είναι το ολοκληρωμένο πρόγραμμα, έτοιμο για αντιγραφή‑και‑επικόλληση. Δεν λείπουν κομμάτια.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Step 2: Load the English language model
            ocrEngine.LoadLanguage(LanguageModel.English);

            // Step 3: Recognize text from the PNG image
            var recognitionResult = ocrEngine.Recognize("YOUR_DIRECTORY/form_image.png");

            // Step 4: Convert the result to pretty‑printed JSON
            string json = JsonResult.FromRecognitionResult(recognitionResult)
                                    .ToString(prettyPrint: true);

            // Optional: Save JSON to a file
            System.IO.File.WriteAllText("ocr_output.json", json);

            // Step 5: Display the JSON output
            Console.WriteLine(json);
        }
    }
}
```

Αποθηκεύστε το ως `Program.cs`, τοποθετήστε το PNG σας, τρέξτε `dotnet run`, και θα δείτε το JSON να εκτυπώνεται.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις (Answering the “What If?”)

### Τι γίνεται αν η εικόνα είναι JPEG αντί για PNG;

Η μέθοδος `Recognize` δέχεται οποιαδήποτε μορφή υποστηρίζεται από το Aspose (JPEG, BMP, TIFF, κ.λπ.). Απλώς αλλάξτε την επέκταση του αρχείου στη διαδρομή.

### Πώς βελτιώνω την ακρίβεια για σαρώσεις χαμηλής ανάλυσης;

1. **Προεπεξεργασία εικόνας** – αυξήστε την αντίθεση, μετατρέψτε σε κλίμακα του γκρι ή εφαρμόστε φίλτρο ακμής.  
2. **Χρησιμοποιήστε πηγή υψηλότερης ανάλυσης** – οι μηχανές OCR συνήθως χρειάζονται τουλάχιστον 300 dpi για αξιόπιστα αποτελέσματα.  
3. **Ενεργοποιήστε την αυτόματη περιστροφή** – καλέστε `ocrEngine.AutoRotate = true;` πριν από την αναγνώριση.

### Μπορώ να εξάγω μόνο το ακατέργαστο κείμενο χωρίς JSON;

Ναι. Μετά το `Recognize`, απλώς διαβάστε `recognitionResult.Text`:

```csharp
Console.WriteLine(recognitionResult.Text);
```

### Υπάρχει τρόπος να εξάγω κείμενο από PDF πολλαπλών σελίδων;

Το Aspose.OCR λειτουργεί σε εικόνες, αλλά μπορείτε να το συνδυάσετε με το Aspose.PDF για να μετατρέψετε κάθε σελίδα PDF σε εικόνα, και στη συνέχεια να τροφοδοτήσετε αυτές τις εικόνες στη μηχανή OCR μέσα σε βρόχο.

---

## Pro Tips για ένα Αξιόπιστο c# OCR Tutorial

- **Κλείσιμο της μηχανής**: Τυλίξτε το `OcrEngine` σε μπλοκ `using` αν επεξεργάζεστε πολλές εικόνες ώστε να ελευθερώνονται άμεσα οι εγγενείς πόροι.  
- **Επεξεργασία παρτίδας**: Για μεγάλους φακέλους, κάντε enumerate τα αρχεία με `Directory.GetFiles` και επεξεργαστείτε καθένα μέσα σε try‑catch ώστε ένα κακό αρχείο να μην σταματήσει όλη τη διαδικασία.  
- **Καταγραφή**: Αποθηκεύστε τους βαθμούς εμπιστοσύνης· είναι ανεκτίμητοι όταν χρειάζεται να επισημάνετε αποτελέσματα χαμηλής ποιότητας για χειροκίνητη ανασκόπηση.  
- **Ασφάλεια νήματος**: Τα αντικείμενα `OcrEngine` **δεν** είναι thread‑safe. Δημιουργήστε ξεχωριστό στιγμιότυπο ανά νήμα αν παράλληλα επεξεργάζεστε.

---

## Συμπέρασμα

Μόλις μάθατε **πώς να εξάγετε OCR** κείμενο από εικόνα χρησιμοποιώντας C#. Αρχικοποιώντας τη μηχανή OCR, φορτώνοντας το κατάλληλο μοντέλο γλώσσας, αναγνωρίζοντας ένα PNG και σειριοποιώντας το αποτέλεσμα σε καλασχεδιασμένο JSON, έχετε τώρα μια σταθερή βάση για οποιοδήποτε έργο ψηφιοποίησης εγγράφων. Αυτό το **c# ocr tutorial** κάλυψε επίσης πώς να **εξάγετε κείμενο από εικόνα**, **διαβάσετε κείμενο από png**, και να αντιμετωπίσετε κοινές παγίδες.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να τροφοδοτήσετε μια παρτίδα σαρωμένων τιμολογίων στην ίδια ροή, πειραματιστείτε με διαφορετικά πακέτα γλωσσών, ή ενσωματώστε το JSON σε μια αναζητήσιμη βάση δεδομένων. Ο ουρανός είναι το όριο, και ο κώδικας που μόλις γράψατε είναι η πλατφόρμα εκτόξευσης.

Αν βρήκατε αυτόν τον οδηγό χρήσιμο, μοιραστείτε τον με συναδέλφους, δώστε αστέρι στο αποθετήριο, ή αφήστε ένα σχόλιο με τις δικές σας ιστορίες επιτυχίας OCR. Καλό κώδικα!

![how to extract ocr example](https://example.com/ocr-demo.png "how to extract ocr example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}