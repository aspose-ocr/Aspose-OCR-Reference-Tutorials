---
category: general
date: 2026-02-09
description: Μάθετε πώς να αναγνωρίζετε κείμενο από εικόνα και να εξάγετε απλό κείμενο
  χρησιμοποιώντας προσαρμοσμένο λεξικό σε C#. Περιλαμβάνει κώδικα βήμα‑βήμα και συμβουλές.
draft: false
keywords:
- recognize text from image
- extract plain text
- read dictionary file
- how to extract text
- how to add custom dictionary
language: el
og_description: Αναγνωρίστε κείμενο από εικόνα σε C# με το Aspose OCR. Ακολουθήστε
  αυτόν τον οδηγό για να εξάγετε απλό κείμενο και να προσθέσετε ένα προσαρμοσμένο
  λεξικό για καλύτερη ακρίβεια.
og_title: Αναγνώριση κειμένου από εικόνα – Πλήρης οδηγός C#
tags:
- OCR
- C#
- Aspose
title: Αναγνώριση κειμένου από εικόνα με το Aspose OCR – Πλήρης οδηγός C#
url: /el/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση κειμένου από εικόνα – Πλήρες Tutorial C#

Έχετε χρειαστεί ποτέ να **αναγνωρίσετε κείμενο από εικόνα** αλλά τα αποτελέσματα να λείπουν λέξεις ειδικές για το πεδίο σας; Δεν είστε μόνοι. Σε πολλά έργα—σάρωση τιμολογίων, ανάγνωση καρτών, ή απλώς εξαγωγή λεζάντων από screenshots—η προεπιλεγμένη μηχανή OCR δεν είναι αρκετά έξυπνη για το λεξιλόγιό σας.  

Τα καλά νέα; Φορτώνοντας ένα **προσαρμοσμένο λεξικό** μπορείτε να βελτιώσετε δραστικά την ακρίβεια και, φυσικά, **να εξάγετε καθαρό κείμενο** σε ένα βήμα. Σε αυτό το tutorial θα περάσουμε από τη διαδικασία από το διάβασμα ενός αρχείου λεξικού μέχρι την εκτύπωση του αποτελέσματος OCR, χρησιμοποιώντας το Aspose.OCR σε C#.  

Θα απαντήσουμε επίσης στην ερώτηση “**πώς να προσθέσετε προσαρμοσμένο λεξικό**”, θα σας δείξουμε **πώς να εξάγετε κείμενο** αποδοτικά, και θα επισημάνουμε κοινά λάθη ώστε να μην χάσετε άλλη ώρα ρυθμίζοντας ρυθμίσεις.

## Τι Θα Χρειαστείτε

- **.NET 6+** (οποιαδήποτε πρόσφατη έκδοση runtime)
- **Aspose.OCR for .NET** πακέτο NuGet  
  ```bash
  dotnet add package Aspose.OCR
  ```
- Ένα **αρχείο κειμένου** (`custom_dictionary.txt`) που περιέχει μία λέξη ανά γραμμή – αυτές είναι οι όροι που αναμένετε να εμφανιστούν.
- Μια **εικόνα** (`input_image.png`) που περιέχει το κείμενο που θέλετε να αναγνωρίσετε.

Καμία πρόσθετη βιβλιοθήκη, καμία εξωτερική υπηρεσία. Απλώς καθαρό C# και Aspose.

## Βήμα 1: Αρχικοποίηση του OCR Engine – Αναγνώριση Κειμένου από Εικόνα

Το πρώτο που κάνετε είναι να δημιουργήσετε ένα `OcrEngine`. Αυτό το αντικείμενο κρατά όλες τις επιλογές διαμόρφωσης, συμπεριλαμβανομένου του προσαρμοσμένου λεξικού που θα ενσωματώσουμε αργότερα.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

class CustomDictionaryDemo
{
    static void Main()
    {
        // Initialise the OCR engine – this is where recognition starts
        OcrEngine ocrEngine = new OcrEngine();
```

> **Γιατί είναι σημαντικό:**  
> Χωρίς ένα στιγμιότυπο του engine δεν υπάρχει πλαίσιο για ρυθμίσεις όπως γλώσσα, DPI ή προσαρμοσμένες λίστες λέξεων. Σκεφτείτε το `OcrEngine` ως τον εγκέφαλο που αργότερα θα **αναγνωρίσει κείμενο από εικόνα**.

## Βήμα 2: Ανάγνωση του Αρχείου Λεξικού – Πώς να Προσθέσετε Προσαρμοσμένο Λεξικό

Στη συνέχεια, πρέπει να **διαβάσουμε το περιεχόμενο του αρχείου λεξικού** σε ένα `HashSet<string>`. Ένα hash set παρέχει αναζήτηση O(1), ιδανική για τους εσωτερικούς ελέγχους του engine.

```csharp
        // Load a custom dictionary from a plain‑text file
        // Each line in the file should contain a single word
        HashSet<string> customDictionary = new HashSet<string>(
            File.ReadAllLines(@"YOUR_DIRECTORY/custom_dictionary.txt"));
        
        // Attach the dictionary to the OCR configuration
        ocrEngine.Configuration.CustomDictionary = customDictionary;
```

> **Συμβουλή επαγγελματία:**  
> Κρατήστε το αρχείο λεξικού κωδικοποιημένο σε UTF‑8 και αποφύγετε κενές γραμμές· αυτές θα θεωρηθούν κενές συμβολοσειρές και μπορεί να μπερδέψουν το engine.

## Βήμα 3: Φόρτωση της Εικόνας – Πώς να Εξάγετε Κείμενο

Τώρα τροφοδοτούμε την εικόνα που θέλουμε να επεξεργαστούμε. Το Aspose χρησιμοποιεί `ImageStream` για να αφαιρέσει την άμεση διαχείριση αρχείων.

```csharp
        // Load the image that contains the text you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/input_image.png");
```

> **Περίπτωση άκρης:**  
> Αν η εικόνα σας είναι μεγαλύτερη από 2000 × 2000 pixels, σκεφτείτε να τη μειώσετε πρώτα. Πολύ μεγάλες εικόνες μπορούν να επιβραδύνουν την αναγνώριση χωρίς να βελτιώνουν την ακρίβεια.

## Βήμα 4: Εκτέλεση της Διαδικασίας OCR – Εξαγωγή Καθαρού Κειμένου

Με όλα έτοιμα, καλέστε `Recognize`. Η μέθοδος επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει τόσο το ακατέργαστο όσο και το καθαρισμένο κείμενο.

```csharp
        // Run OCR – this is where the engine actually recognises text from image
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Display the extracted plain text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.PlainText);
    }
}
```

> **Τι θα δείτε:**  
> Η κονσόλα εκτυπώνει μια καθαρή, διατηρώντας τις αλλαγές γραμμής, έκδοση του κειμένου. Αν το προσαρμοσμένο λεξικό σας περιέχει τις λέξεις “Aspose” και “OCR”, αυτές θα εμφανιστούν ακριβώς όπως τις ορίσατε, ακόμη και αν η εικόνα είναι ελαφρώς θορυβώδης.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το **πλήρες, έτοιμο για αντιγραφή** πρόγραμμα. Αντικαταστήστε το `YOUR_DIRECTORY` με τη διαδρομή του φακέλου όπου αποθηκεύσατε το λεξικό και την εικόνα.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

class CustomDictionaryDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load a custom dictionary and assign it to the engine configuration
        HashSet<string> customDictionary = new HashSet<string>(
            File.ReadAllLines(@"YOUR_DIRECTORY/custom_dictionary.txt"));
        ocrEngine.Configuration.CustomDictionary = customDictionary;

        // Step 3: Load the image that contains the text to be recognized
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/input_image.png");

        // Step 4: Run the OCR process on the image
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 5: Display the extracted plain text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.PlainText);
    }
}
```

**Αναμενόμενη έξοδος** (υποθέτοντας ότι η εικόνα περιέχει το κείμενο “Welcome to Aspose OCR Demo”)  

```
=== Extracted Text ===
Welcome to Aspose OCR Demo
```

Αν το “Aspose” ήταν στο προσαρμοσμένο λεξικό σας, η ορθογραφία θα είναι τέλεια ακόμη και αν η εικόνα είχε ελαφρύ θόλωση.

## Συχνές Ερωτήσεις

### Πώς να **διαβάσετε αρχείο λεξικού** με διαφορετικές κωδικοποιήσεις;
Χρησιμοποιήστε `File.ReadAllLines(path, Encoding.UTF8)` (ή `Encoding.Unicode`) ώστε να ταιριάζει η κωδικοποίηση του αρχείου. Αυτό αποτρέπει κρυφούς χαρακτήρες να μπει στο `HashSet`.

### Τι γίνεται αν το αποτέλεσμα OCR εξακολουθεί να λείπει λέξη από το λεξικό μου;
Βεβαιωθείτε ότι το κεφαλαίο/μικρό γράμμα ταιριάζει με την καταχώρηση στο λεξικό, ή ορίστε `ocrEngine.Configuration.IgnoreCase = true`. Επίσης, ελέγξτε ότι η ανάλυση της εικόνας είναι τουλάχιστον 300 dpi για βέλτιστα αποτελέσματα.

### Μπορώ να **εξάγω καθαρό κείμενο** από PDF αντί για εικόνα;
Ναι—το Aspose.PDF μπορεί να αποδώσει κάθε σελίδα σε εικόνα, έπειτα να τροφοδοτήσει αυτές τις εικόνες στην ίδια διαδικασία OCR. Η ροή εργασίας είναι ταυτόσημη· απλώς προσθέτετε ένα βήμα μετατροπής PDF‑σε‑εικόνα.

### Υπάρχει τρόπος **πώς να προσθέσετε προσαρμοσμένο λεξικό** κατά το runtime για πολλές γλώσσες;
Απολύτως. Δημιουργήστε ένα ξεχωριστό `HashSet<string>` ανά γλώσσα και αλλάξτε το `ocrEngine.Configuration.CustomDictionary` πριν από κάθε κλήση `Recognize`.

## Συμβουλές & Τεχνάσματα για Καλύτερη Ακρίβεια

- **Προεπεξεργασία της εικόνας**: Μετατρέψτε σε γκρι, αυξήστε την αντίθεση ή εφαρμόστε ελαφρύ Gaussian blur για αφαίρεση σπινθηρισμών.
- **Επεξεργασία σε παρτίδες**: Αν έχετε δεκάδες εικόνες, επαναχρησιμοποιήστε το ίδιο στιγμιότυπο `OcrEngine`; η επανεκκίνηση κάθε φορά προσθέτει περιττό κόστος.
- **Καταγραφή των ακατέργαστων δεδομένων OCR**: `ocrResult.TextLines` παρέχει βαθμολογίες εμπιστοσύνης ανά γραμμή, χρήσιμες για μετα-επεξεργασία ή σηματοδότηση αποτελεσμάτων χαμηλής εμπιστοσύνης.

## Επόμενα Βήματα

Τώρα που ξέρετε **πώς να εξάγετε κείμενο** και **πώς να προσθέσετε προσαρμοσμένο λεξικό**, σκεφτείτε τα παρακάτω θέματα:

1. **Ενσωμάτωση με ASP.NET Core** – εκθέστε ένα API endpoint που δέχεται εικόνα και επιστρέφει αποτελέσματα OCR σε μορφή JSON.  
2. **Συνδυασμός με Entity Framework** – αποθηκεύστε το εξαγόμενο καθαρό κείμενο απευθείας σε βάση δεδομένων για αναζητήσιμα αρχεία.  
3. **Εξερεύνηση ανίχνευσης γλώσσας** – εναλλάξτε λεξικά αυτόματα βάσει κωδικών ανιχνευόμενης γλώσσας.

Κάθε ένα από αυτά χτίζει πάνω στο θεμέλιο που θέσαμε σε αυτόν τον οδηγό, επιτρέποντάς σας να μετατρέψετε ένα απλό **αναγνώριση κειμένου από εικόνα** snippet σε υπηρεσία έτοιμη για παραγωγή.

---

*Καλή προγραμματιστική! Αν αντιμετωπίσετε κάποιο πρόβλημα, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την τεκμηρίωση του Aspose.OCR για πιο προχωρημένες επιλογές διαμόρφωσης. Θυμηθείτε, ένα καλά σχεδιασμένο προσαρμοσμένο λεξικό είναι συχνά το μυστικό συστατικό που μετατρέπει ένα μέτριο OCR σε εξαιρετικά ακριβή εξαγωγή κειμένου.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}