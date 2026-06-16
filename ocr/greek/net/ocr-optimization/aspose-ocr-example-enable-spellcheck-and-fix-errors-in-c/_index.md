---
category: general
date: 2026-03-07
description: Παράδειγμα Aspose OCR που δείχνει πώς να ενεργοποιήσετε τον ορθογραφικό
  έλεγχο, να προσθέσετε προσαρμοσμένο λεξικό, να φορτώσετε OCR εικόνας και να διορθώσετε
  γρήγορα τα σφάλματα OCR.
draft: false
keywords:
- aspose ocr example
- how to enable spellcheck
- how to add dictionary
- load image ocr
- how to fix ocr errors
language: el
og_description: Παράδειγμα Aspose OCR που σας καθοδηγεί στη ενεργοποίηση του ελέγχου
  ορθογραφίας, στην προσθήκη προσαρμοσμένου λεξικού, στη φόρτωση εικόνας για OCR και
  στη διόρθωση κοινών σφαλμάτων OCR.
og_title: Παράδειγμα Aspose OCR – Ενεργοποίηση ορθογραφικού ελέγχου & Διόρθωση σφαλμάτων
tags:
- Aspose
- OCR
- C#
- SpellCheck
title: Παράδειγμα Aspose OCR – Ενεργοποίηση ορθογραφικού ελέγχου και διόρθωση σφαλμάτων
  σε C#
url: /el/net/ocr-optimization/aspose-ocr-example-enable-spellcheck-and-fix-errors-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Παράδειγμα Aspose OCR – Ενεργοποίηση Ορθογραφικού Ελέγχου και Διόρθωση Σφαλμάτων σε C#

Έχετε ποτέ χρειαστεί ένα **Aspose OCR example** που όχι μόνο διαβάζει κείμενο από μια εικόνα αλλά και καθαρίζει αυτά τα επίμονα ορθογραφικά λάθη; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα η ακατέργαστη έξοδος OCR είναι γεμάτη τυπογραφικά λάθη, ειδικά όταν η πηγή εικόνας περιέχει γραμματοσειρές χαμηλής αντίθεσης ή χειρόγραφες σημειώσεις.  

Τα καλά νέα; Με το Aspose.OCR μπορείτε να **ενεργοποιήσετε τον ορθογραφικό έλεγχο**, να ενσωματώσετε το δικό σας λεξικό και να λάβετε μια επεξεργασμένη συμβολοσειρά σε λίγες μόνο γραμμές κώδικα. Παρακάτω θα δείτε ακριβώς **πώς να ενεργοποιήσετε τον ορθογραφικό έλεγχο**, **πώς να προσθέσετε ένα λεξικό**, και **πώς να φορτώσετε εικόνα OCR** ώστε τελικά να **διορθώσετε τα σφάλματα OCR** χωρίς να τσακίζετε τα μαλλιά σας.

Σε αυτό το tutorial θα καλύψουμε όλα όσα χρειάζεστε — από την εγκατάσταση του NuGet μέχρι ένα πλήρες, εκτελέσιμο πρόγραμμα που εκτυπώνει διορθωμένο κείμενο. Στο τέλος θα έχετε ένα στιβαρό **Aspose OCR example** που μπορείτε να ενσωματώσετε απευθείας σε οποιοδήποτε έργο .NET.

## Προαπαιτούμενα

- .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework)
- Visual Studio 2022 ή οποιοδήποτε IDE συμβατό με C#
- Ένα αρχείο εικόνας (`typed_text.png`) που περιέχει καθαρό, τυπωμένο αγγλικό κείμενο
- Πρόσβαση στο Internet για λήψη του πακέτου NuGet Aspose.OCR

Δεν απαιτούνται άλλες βιβλιοθήκες τρίτων.

---

## Βήμα 1 – Εγκατάσταση του πακέτου NuGet Aspose.OCR (Φόρτωση εικόνας OCR)

Πριν γράψουμε οποιονδήποτε κώδικα, χρειαζόμαστε τη βιβλιοθήκη που τροφοδοτεί τη μηχανή OCR.

```bash
dotnet add package Aspose.OCR
```

> **Συμβουλή:** Αν χρησιμοποιείτε Visual Studio, κάντε δεξί κλικ στο έργο → *Manage NuGet Packages* → αναζητήστε το **Aspose.OCR** και πατήστε *Install*.  

Η εγκατάσταση του πακέτου σας δίνει πρόσβαση στα `OcrEngine`, `ImageStream` και στα ενσωματωμένα εργαλεία ορθογραφικού ελέγχου που θα χρησιμοποιήσουμε αργότερα. Μόλις το πακέτο είναι στη θέση του, είστε έτοιμοι να **φορτώσετε εικόνα OCR**.

## Βήμα 2 – Δημιουργία του αντικειμένου OCR Engine

Η δημιουργία της μηχανής είναι το πρώτο συγκεκριμένο βήμα σε οποιοδήποτε **Aspose OCR example**. Σκεφτείτε το `OcrEngine` ως τον εγκέφαλο που θα αναλύσει το bitmap και θα εξάγει κείμενο.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Step 2: Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

Ο κατασκευαστής `OcrEngine` δεν απαιτεί παραμέτρους, κάτι που το καθιστά απλό και καθαρό για γρήγορα πρωτότυπα.

## Βήμα 3 – Πώς να ενεργοποιήσετε τον ορθογραφικό έλεγχο (και γιατί είναι σημαντικό)

Η ακατέργαστη έξοδος OCR συχνά περιέχει λανθασμένα αναγνωρισμένες λέξεις όπως “teh” αντί για “the”. Η ενεργοποίηση του ενσωματωμένου ορθογραφικού ελεγκτή επιτρέπει στο Aspose να αντικαθιστά αυτόματα αυτά τα σφάλματα με την πιο πιθανή σωστή ορθογραφία.

```csharp
// Step 3: Turn on spell checking and set the language to English
ocrEngine.Settings.SpellCheck.Enabled = true;
ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;
```

> **Γιατί να ενεργοποιήσετε τον ορθογραφικό έλεγχο;**  
> - **Ακρίβεια:** Ένας ορθογραφικός έλεγχος μετά την επεξεργασία μπορεί να αυξήσει την συνολική ακρίβεια κειμένου κατά 10‑15 % για έντυπα έγγραφα.  
> - **Εμπειρία χρήστη:** Καθαρό κείμενο σημαίνει λιγότερη επεξεργασία στο downstream όταν τροφοδοτείτε το αποτέλεσμα σε ευρετήρια αναζήτησης ή pipelines ανάλυσης.

## Βήμα 4 – Πώς να προσθέσετε ένα λεξικό (προσαρμοσμένες λέξεις)

Μερικές φορές το προεπιλεγμένο λεξικό δεν γνωρίζει τα ονόματα των εμπορικών σημάτων, τους κωδικούς προϊόντων ή το ειδικό λεξιλόγιο του τομέα σας. Εκεί έρχεται σε εφαρμογή το **πώς να προσθέσετε λεξικό**.

```csharp
// Step 4: Add custom words that the spell checker should accept
ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
{
    "AsposeOCR",   // our library name
    "OCRify",      // a fictional product
    "CSharpify"    // another custom term
});
```

Μπορείτε να δώσετε έναν πίνακα, μια λίστα ή ακόμη και να διαβάσετε από αρχείο εάν έχετε μεγάλο προσαρμοσμένο λεξιλόγιο. Ο ορθογραφικός ελεγκτής θα θεωρεί τώρα αυτές τις καταχωρήσεις έγκυρες, αποτρέποντας λανθασμένες διορθώσεις.

## Βήμα 5 – Φόρτωση της εικόνας για OCR (Φόρτωση εικόνας OCR)

Τώρα που η μηχανή είναι ρυθμισμένη, πρέπει να την κατευθύνουμε προς την εικόνα που θέλουμε να διαβάσουμε. Η βοηθητική μέθοδος `ImageStream.FromFile` αφαιρεί τις λεπτομέρειες ανάγνωσης αρχείου.

```csharp
// Step 5: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");
```

> **Συμβουλή:** Εάν η εικόνα σας βρίσκεται σε υποφάκελο του έργου, ορίστε την ιδιότητα *Copy to Output Directory* σε *Copy always* ώστε η διαδρομή να λυθεί κατά την εκτέλεση.

## Βήμα 6 – Εκτέλεση αναγνώρισης και διόρθωση σφαλμάτων OCR

Με όλα ρυθμισμένα, μια ενιαία κλήση στο `Recognize()` εκτελεί τη διαδικασία OCR, εφαρμόζει τον ορθογραφικό έλεγχο και αποθηκεύει το καθαρισμένο αποτέλεσμα στο `ocrEngine.Text`.

```csharp
// Step 6: Run OCR and let the spell checker clean the output
ocrEngine.Recognize();

// Step 7: Output the corrected text to the console
Console.WriteLine("Corrected text:");
Console.WriteLine(ocrEngine.Text);
```

### Αναμενόμενη έξοδος

Υποθέτοντας ότι το `typed_text.png` περιέχει την πρόταση `The quick brown fox jumps over teh lazy dog`, η κονσόλα θα εμφανίσει:

```
Corrected text:
The quick brown fox jumps over the lazy dog
```

Παρατηρήστε πώς το “teh” διορθώθηκε αυτόματα σε “the”. Εάν είχατε προσθέσει το “OCRify” στο προσαρμοσμένο λεξικό και η εικόνα περιείχε αυτή τη λέξη, η μηχανή θα την άφηνε αμετάβλητη.

---

## Πλήρες λειτουργικό παράδειγμα (Έτοιμο για αντιγραφή‑επικόλληση)

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να ενσωματώσετε σε ένα νέο έργο κονσόλας. Περιλαμβάνει όλα τα παραπάνω βήματα, συν λίγα σχόλια για σαφήνεια.

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

Αποθηκεύστε το ως `Program.cs`, εκτελέστε `dotnet run`, και θα πρέπει να δείτε την διορθωμένη πρόταση να εκτυπώνεται στην κονσόλα.

---

## Συχνές ερωτήσεις & Ακραίες περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **Τι γίνεται αν η εικόνα είναι PDF πολλαπλών σελίδων;** | Το Aspose.OCR μπορεί να διαχειριστεί σελίδες PDF ως εικόνες. Χρησιμοποιήστε `ocrEngine.Image = ImageStream.FromPdf("file.pdf", pageNumber: 1);` και επαναλάβετε τη διαδικασία για κάθε σελίδα. |
| **Μπορώ να αλλάξω τη γλώσσα σε κάτι διαφορετικό από τα Αγγλικά;** | Απόλυτα. Ορίστε `ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.French;` (ή οποιαδήποτε υποστηριζόμενη γλώσσα). |
| **Το προσαρμοσμένο λεξικό μου είναι τεράστιο — θα επηρεάσει την απόδοση;** | Η προσθήκη χιλιάδων λέξεων προκαλεί ένα μικρό αρχικό κόστος, αλλά η αναζήτηση είναι O(1) χάρη σε ένα hash‑set στο παρασκήνιο. Για τεράστια λεξιλόγια, σκεφτείτε να τα φορτώνετε μία φορά κατά την εκκίνηση της εφαρμογής. |
| **Τι γίνεται αν η μηχανή OCR ρίξει εξαίρεση σε κατεστραμμένη εικόνα;** | Τυλίξτε το `Recognize()` σε μπλοκ try‑catch και ελέγξτε το `ocrEngine.LastError`. Μπορείτε επίσης να προελέγξετε τις διαστάσεις της εικόνας με `ocrEngine.Image.Width` και `Height`. |
| **Χρειάζομαι άδεια για παραγωγική χρήση;** | Η δωρεάν αξιολόγηση λειτουργεί για δοκιμές, αλλά μια εμπορική άδεια αφαιρεί το υδατογράφημα αξιολόγησης και ξεκλειδώνει πλήρη απόδοση. |

## Συμπέρασμα

Τώρα έχετε ένα **πλήρες Aspose OCR example** που δείχνει **πώς να ενεργοποιήσετε τον ορθογραφικό έλεγχο**, **πώς να προσθέσετε ένα λεξικό**, **να φορτώσετε εικόνα OCR**, και **πώς να διορθώσετε σφάλματα OCR** με έναν καθαρό, έτοιμο για παραγωγή τρόπο. Με τη ρύθμιση του ορθογραφικού ελεγκτή και την παροχή μιας προσαρμοσμένης λίστας λέξεων, βελτιώνετε δραματικά την ποιότητα του εξαγόμενου κειμένου χωρίς να γράψετε λογική post‑processing.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αλλάξετε τη γλώσσα στα Ισπανικά, να τροφοδοτήσετε ένα PDF πολλαπλών σελίδων, ή να ενσωματώσετε το αποτέλεσμα σε ένα αναζητήσιμο ευρετήριο Azure Cognitive Search. Το ίδιο μοτίβο ισχύει — απλώς προσαρμόστε τη σημαία γλώσσας και ίσως επεκτείνετε το προσαρμοσμένο λεξικό.

Αν βρήκατε αυτόν τον οδηγό χρήσιμο, δώστε του ένα αστέρι στο GitHub, μοιραστείτε το με συναδέλφους, ή αφήστε ένα σχόλιο παρακάτω. Καλή προγραμματιστική, και εύχομαι τα αποτελέσματα OCR σας να είναι πάντα χωρίς σφάλματα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}