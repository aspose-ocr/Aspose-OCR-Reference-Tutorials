---
category: general
date: 2026-04-17
description: Μάθετε πώς να κάνετε OCR σε C# για να αναγνωρίζετε κείμενο από εικόνα,
  να εξάγετε κείμενο από jpg και να μετατρέπετε την εικόνα σε κείμενο γρήγορα.
draft: false
keywords:
- how to perform OCR
- recognize text from image
- extract text from jpg
- convert image to text
- how to extract text
language: el
og_description: Πώς να εκτελέσετε OCR σε C#; Αυτός ο οδηγός σας δείχνει πώς να αναγνωρίζετε
  κείμενο από εικόνα, να εξάγετε κείμενο από jpg και να μετατρέψετε την εικόνα σε
  κείμενο σε λίγα λεπτά.
og_title: Πώς να εκτελέσετε OCR σε C# – Αναγνώριση κειμένου από εικόνα
tags:
- OCR
- C#
- Aspose
title: Πώς να εκτελέσετε OCR σε C# – Αναγνώριση κειμένου από εικόνα
url: /el/net/text-recognition/how-to-perform-ocr-in-c-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε C# – Αναγνώριση Κειμένου από Εικόνα

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε μια εικόνα που πήρατε από σαρωτή ή κινητό; Σε πολλά έργα θα χρειαστεί να **αναγνωρίσετε κείμενο από εικόνα**—είτε πρόκειται για απόδειξη, χειρόγραφη σημείωση ή σελίδα PDF που μετατράπηκε σε JPEG. Τα καλά νέα είναι ότι με το Aspose.OCR μπορείτε να **εξάγετε κείμενο από jpg** αρχεία και να **μετατρέψετε εικόνα σε κείμενο** με λίγες μόνο γραμμές C#.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία, από την εγκατάσταση της βιβλιοθήκης μέχρι τη διαχείριση περιπτώσεων όπως η έλλειψη γλωσσών. Στο τέλος θα ξέρετε ακριβώς **πώς να εκτελέσετε OCR**, και θα έχετε ένα έτοιμο πρόγραμμα που εκτυπώνει το εξαγόμενο κείμενο στην κονσόλα. Χωρίς ασαφείς «δείτε τα docs» συντομεύσεις—απλώς μια πλήρης, αυτόνομη λύση.

## Τι Θα Χρειαστείτε

- **.NET 6+** (ο κώδικας λειτουργεί και σε .NET Framework, αλλά το .NET 6 είναι το τρέχον LTS)
- **Aspose.OCR for .NET** πακέτο NuGet – εγκαταστήστε το με `dotnet add package Aspose.OCR`
- Ένα αρχείο εικόνας (JPEG, PNG, BMP) που θέλετε να δοκιμάσετε – θα το ονομάσουμε `input.jpg`
- Οποιοδήποτε IDE προτιμάτε (Visual Studio, Rider, VS Code)

Αυτό είναι όλο. Χωρίς επιπλέον ρυθμίσεις, χωρίς εξωτερικές υπηρεσίες και χωρίς κρυφά βήματα.

## Βήμα 1: Εγκατάσταση Aspose.OCR και Προσθήκη Αναφοράς

Πρώτα, φέρετε τη βιβλιοθήκη OCR στο έργο σας. Ανοίξτε ένα τερματικό στον φάκελο του έργου και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Η εντολή κατεβάζει την πιο πρόσφατη σταθερή έκδοση (από Απρίλιο 2026 είναι **23.9.0**) και ενημερώνει το `.csproj`. Μετά από αυτό, προσθέστε τη δήλωση `using` στην κορυφή του αρχείου σας:

```csharp
using Aspose.OCR;
```

> **Pro tip:** Αν χρησιμοποιείτε Visual Studio, η διεπαφή του NuGet Package Manager λειτουργεί εξίσου—απλώς ψάξτε για *Aspose.OCR*.

## Βήμα 2: Φόρτωση της Εικόνας που Θέλετε να Αναγνωρίσετε

Τώρα πρέπει να πείτε στη μηχανή OCR ποια εικόνα θα διαβάσει. Το Aspose παρέχει τη βολική μέθοδο `OcrImage.FromFile` που υποστηρίζει τις περισσότερες κοινές μορφές.

```csharp
// Step 2: Load the image you want to recognize
var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.jpg");
```

Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή ή κρατήστε την εικόνα δίπλα στο εκτελέσιμο και χρησιμοποιήστε σχετική διαδρομή. Αν το αρχείο δεν υπάρχει, η μέθοδος ρίχνει `FileNotFoundException`, το οποίο μπορείτε να πιάσετε αργότερα.

## Βήμα 3: Δημιουργία της Μηχανής OCR (Platform‑Aware)

Το Aspose.OCR επιλέγει αυτόματα την καλύτερη υποκείμενη μηχανή για το λειτουργικό σύστημα που τρέχετε (Windows, Linux, macOS). Η δημιουργία της μέσα σε μπλοκ `using` εγγυάται σωστή αποδέσμευση πόρων.

```csharp
// Step 3: Create the OCR engine (auto‑selects best engine for the platform)
using var ocrEngine = new OcrEngine();
```

Γιατί το `using`; Η μηχανή κρατά εγγενείς πόρους (όπως unmanaged memory) που πρέπει να απελευθερωθούν. Η παράλειψη της αποδέσμευσης μπορεί να οδηγήσει σε διαρροές μνήμης, ειδικά όταν επεξεργάζεστε πολλές εικόνες σε βρόχο.

## Βήμα 4: (Προαιρετικό) Ορισμός Γλώσσας – Προεπιλογή η Αγγλική

Αν η εικόνα σας περιέχει αγγλικό κείμενο, μπορείτε να παραλείψετε αυτό το βήμα επειδή το `OcrLanguage.English` είναι η προεπιλογή. Για άλλες γλώσσες, απλώς αντιστοιχίστε την κατάλληλη τιμή enum.

```csharp
// Step 4: (Optional) Specify the language – English is the default
ocrEngine.Language = OcrLanguage.English;
```

> **Did you know?** Το Aspose.OCR υποστηρίζει πάνω από 30 γλώσσες, συμπεριλαμβανομένων των Αραβικών, Κινέζικων και Ρωσικών. Η αλλαγή γλώσσας είναι τόσο απλή όσο η αλλαγή του enum.

## Βήμα 5: Εκτέλεση της Διαδικασίας Αναγνώρισης

Καλώντας το `Recognize` γίνεται η βαριά δουλειά—ανάλυση pixel, διαχωρισμός χαρακτήρων και αναζήτηση σε λεξικό εκτελούνται στο παρασκήνιο.

```csharp
// Step 5: Run the recognition process on the loaded image
var ocrResult = ocrEngine.Recognize(ocrImage);
```

Αν η μηχανή δεν βρει κείμενο, το `ocrResult.Text` θα είναι κενή συμβολοσειρά. Μπορείτε να ελέγξετε το `ocrResult.HasText` (Boolean) πριν προχωρήσετε.

## Βήμα 6: Ανάκτηση και Εμφάνιση του Αποτελέσματος Καθαρής Συμβολοσειράς

Τέλος, εξάγετε τη συμβολοσειρά και γράψτε την στην κονσόλα. Εδώ **μετατρέπετε εικόνα σε κείμενο**.

```csharp
// Step 6: Retrieve the plain‑text result and display it
string recognizedText = ocrResult.Text;
Console.WriteLine("Recognized text:");
Console.WriteLine(recognizedText);
```

Η έξοδος θα μοιάζει κάπως έτσι:

```
Recognized text:
Invoice #12345
Date: 04/15/2026
Total: $256.78
```

Αν χρειάζεστε το κείμενο για περαιτέρω επεξεργασία (π.χ. αποθήκευση σε αρχείο, εισαγωγή σε βάση δεδομένων ή εκτέλεση regex), το έχετε ήδη στη μεταβλητή `recognizedText`.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το ολοκληρωμένο πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε μια νέα εφαρμογή κονσόλας (`dotnet new console`). Περιλαμβάνει διαχείριση σφαλμάτων για τις πιο κοινές παγίδες.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load the image you want to recognize
            var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.jpg");

            // 2️⃣ Create the OCR engine (auto‑selects best engine for the platform)
            using var ocrEngine = new OcrEngine();

            // 3️⃣ (Optional) Set language – English is default
            ocrEngine.Language = OcrLanguage.English;

            // 4️⃣ Run the recognition process
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // 5️⃣ Check if any text was found
            if (!ocrResult.HasText || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be extracted from the image.");
                return;
            }

            // 6️⃣ Retrieve and display the plain‑text result
            string recognizedText = ocrResult.Text;
            Console.WriteLine("Recognized text:");
            Console.WriteLine(recognizedText);
        }
        catch (FileNotFoundException)
        {
            Console.WriteLine("The specified image file was not found. Double‑check the path.");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"An unexpected error occurred: {ex.Message}");
        }
    }
}
```

> **Expected output:** Η κονσόλα εκτυπώνει τους ακριβείς χαρακτήρες που ανίχνευσε η μηχανή OCR. Αν η πηγή εικόνας είναι καθαρή και υψηλής ανάλυσης, η ακρίβεια συνήθως υπερβαίνει το 95 %.

## Διαχείριση Συνηθισμένων Edge Cases

### 1️⃣ Εικόνες με Πολλαπλές Γλώσσες  
Αν έχετε διγλωσσική απόδειξη, ορίστε `ocrEngine.Language` σε `OcrLanguage.Multilingual`. Η μηχανή θα προσπαθήσει να εντοπίσει αυτόματα κάθε γλώσσα.

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

### 2️⃣ Χαμηλής Ανάλυσης ή Κακοστραμμένες Εικόνες  
Προεπεξεργαστείτε την εικόνα (περιστροφή, αλλαγή μεγέθους, αύξηση αντίθεσης) πριν τη δώσετε στο Aspose. Η βιβλιοθήκη εκθέτει μεθόδους `OcrImage` όπως `Resize` και `Rotate`.

```csharp
ocrImage = ocrImage.Rotate(0.0); // placeholder – replace with actual angle if needed
```

### 3️⃣ Μεγάλες Παρτίδες  
Όταν επεξεργάζεστε δεκάδες αρχεία, επαναχρησιμοποιήστε την ίδια παρουσία `OcrEngine` αντί να δημιουργείτε νέα σε κάθε βρόχο. Απλώς θυμηθείτε να την αποδεσμεύσετε μετά το τέλος της παρτίδας.

```csharp
using var batchEngine = new OcrEngine();
foreach (var file in Directory.GetFiles(@"images", "*.jpg"))
{
    var img = OcrImage.FromFile(file);
    var result = batchEngine.Recognize(img);
    // handle result…
}
```

### 4️⃣ Περιορισμοί Μνήμης σε Linux Containers  
Αν τρέχετε μέσα σε Docker container με περιορισμένη RAM, ορίστε `ocrEngine.MaxMemoryUsage` (αν το API παρέχει τέτοιο property) για να αποφύγετε καταρρεύσεις OOM.

## Pro Tips & Gotchas

- **File Encoding:** Η επιστρεφόμενη συμβολοσειρά είναι UTF‑16 (`string` στο .NET). Αν χρειάζεστε UTF‑8 για εγγραφή σε αρχείο, χρησιμοποιήστε `Encoding.UTF8.GetBytes(recognizedText)`.
- **Performance:** Για μία εικόνα, το κόστος αρχικοποίησης της μηχανής είναι αμελητέο. Για μαζικές εργασίες, αρχικοποιήστε μία φορά (δείτε το παράδειγμα batch) για να μειώσετε τον χρόνο επεξεργασίας κατά ~30 %.
- **Debugging:** Αν το αποτέλεσμα OCR φαίνεται παραμορφωμένο, εξετάστε το `ocrResult.Words` (συλλογή αντικειμένων λέξεων) για να δείτε τα confidence scores. Χαμηλή εμπιστοσύνη συχνά σημαίνει θολή εικόνα.
- **License:** Το Aspose.OCR λειτουργεί σε λειτουργία αξιολόγησης χωρίς άδεια, αλλά προσθέτει υδατογράφημα στο εξαγόμενο κείμενο. Καταχωρίστε αρχείο άδειας (`Aspose.OCR.lic`) για παραγωγική χρήση.

## Visual Overview

![how to perform OCR example in C#](ocr-example.png "how to perform OCR example in C#")

*The screenshot shows the complete console output after running the sample code.*

## Συμπέρασμα

Τώρα έχετε μια σταθερή κατανόηση του **πώς να εκτελέσετε OCR** σε C# χρησιμοποιώντας το Aspose.OCR, και μπορείτε με σιγουριά **να αναγνωρίζετε κείμενο από εικόνα**, **να εξάγετε κείμενο από jpg**, και **να μετατρέπετε εικόνα σε κείμενο** για οποιαδήποτε επόμενη επεξεργασία. Το παράδειγμα καλύπτει τα βασικά βήματα, εξηγεί γιατί κάθε μέρος είναι σημαντικό, και δίνει ενδείξεις για προχωρημένα σενάρια όπως υποστήριξη πολλαπλών γλωσσών και επεξεργασία παρτίδων.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να αντικαταστήσετε το JPEG με PNG, πειραματιστείτε με το `OcrLanguage.Multilingual`, ή διοχετεύστε το εξαγόμενο κείμενο σε pipeline επεξεργασίας φυσικής γλώσσας. Οι δυνατότητες είναι απεριόριστες όταν μπορείτε να μετατρέψετε εικόνες σε αναζητήσιμες, επεξεργάσιμες συμβολοσειρές.

Έχετε ερωτήσεις ή αντιμετωπίσατε κάποιο πρόβλημα; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}