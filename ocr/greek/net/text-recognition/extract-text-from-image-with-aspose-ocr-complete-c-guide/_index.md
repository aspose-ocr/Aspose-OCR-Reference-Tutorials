---
category: general
date: 2026-01-04
description: Εξάγετε κείμενο από εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να φορτώνετε εικόνα για OCR και να ορίζετε τη γλώσσα OCR για επεξεργασία εκτός
  σύνδεσης.
draft: false
keywords:
- extract text from image
- load image for ocr
- set ocr language
- offline ocr csharp
- aspose ocr tutorial
language: el
og_description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Αυτός
  ο οδηγός δείχνει πώς να φορτώσετε εικόνα για OCR και να ορίσετε τη γλώσσα OCR για
  αξιόπιστη επεξεργασία εκτός σύνδεσης.
og_title: Εξαγωγή κειμένου από εικόνα με Aspose OCR – Πλήρης οδηγός C#
tags:
- C#
- OCR
- Aspose
title: Εξαγωγή κειμένου από εικόνα με Aspose OCR – Πλήρης οδηγός C#
url: /el/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Πλήρης Οδηγός C#

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από εικόνα** αλλά να κολλήσατε στο ερώτημα «πώς θα πάρω πραγματικά τα pixel στον κώδικα;»; Δεν είστε οι μόνοι. Σε πολλές πραγματικές εφαρμογές — σκεφτείτε σαρωτές αποδείξεων, επαλήθευση ταυτοτήτων ή απλώς την ψηφιοποίηση χειρόγραφων σημειώσεων — η αξιόπιστη λειτουργία OCR είναι κρίσιμη.

Το θέμα είναι: το Aspose OCR σας επιτρέπει να **φορτώνετε εικόνα για OCR** και να **ορίζετε τη γλώσσα OCR** χωρίς να χρειάζεται σύνδεση στο διαδίκτυο. Σε αυτό το tutorial θα περάσουμε από ένα πλήρως εκτελέσιμο παράδειγμα C# που δείχνει ακριβώς πώς γίνεται αυτό, μαζί με μια σειρά από συμβουλές που θα θέλατε να γνωρίζατε νωρίτερα.

> **Τι θα αποκομίσετε**  
> • Ένα πλήρες πρόγραμμα, έτοιμο για αντιγραφή‑και‑επικόλληση, που εξάγει κείμενο από εικόνα.  
> • Κατανόηση του γιατί πρέπει να δείχνετε στη μηχανή ένα τοπικό πακέτο γλώσσας.  
> • Πρακτικές συμβουλές για τη διαχείριση ειδικών περιπτώσεων (ελλιπή πόροι, λανθασμένες διαδρομές αρχείων κ.λπ.).

---

## Τι Θα Χρειαστείτε

- **.NET 6+** (ο κώδικας μεταγλωττίζεται και σε .NET Framework, αλλά το .NET 6 είναι το ιδανικό).  
- **Aspose.OCR for .NET** πακέτο NuGet (`Install-Package Aspose.OCR`).  
- Τοπικός φάκελος γλώσσας OCR (στο παράδειγμα θα χρησιμοποιήσουμε το πακέτο Tamil).  
- Ένα αρχείο εικόνας που θέλετε να επεξεργαστείτε (π.χ., `tamil_note.jpg`).  

Δεν απαιτείται σύνδεση στο διαδίκτυο μόλις τα γλωσσικά αρχεία είναι αποθηκευμένα στον δίσκο, κάτι που καθιστά αυτή την προσέγγιση ιδανική για περιβάλλοντα εκτός σύνδεσης ή ασφαλή.

---

## Βήμα 1: Εξαγωγή Κειμένου από Εικόνα – Προετοιμασία Πόρων

Πρώτα, πρέπει να πούμε στο Aspose OCR πού βρίσκονται τα αρχεία γλώσσας. Αν δεν έχετε κατεβάσει ακόμη το πακέτο Tamil, κατεβάστε το από την ιστοσελίδα της Aspose και τοποθετήστε το σε φάκελο **Resources** δίπλα στο εκτελέσιμο σας.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

// Define the path to the local OCR language resources
string resourcesPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "Resources");

// Ensure the folder exists – a simple guard against a common pitfall
if (!Directory.Exists(resourcesPath))
{
    Console.WriteLine($"Resources folder not found at {resourcesPath}");
    return;
}
```

**Γιατί είναι σημαντικό:** Ορίζοντας το `ResourcesPath` βάζουμε τη μηχανή σε **λειτουργία εκτός σύνδεσης**. Αυτό εξαλείφει τυχόν ανεπιθύμητες κλήσεις δικτύου και εγγυάται συνεπή αποτελέσματα σε όλες τις εγκαταστάσεις.

---

## Βήμα 2: Φόρτωση Εικόνας για OCR

Τώρα που η μηχανή ξέρει πού να ψάξει για τα γλωσσικά δεδομένα, πρέπει να της δώσουμε την εικόνα που θέλουμε να διαβάσει. Εδώ ξεχωρίζει το βήμα **load image for OCR** — το Aspose δέχεται ευρύ φάσμα μορφών (JPG, PNG, BMP, TIFF, κ.λπ.).

```csharp
// Create and configure the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Config =
    {
        ResourcesPath = resourcesPath,      // Force offline mode
        AutoDownloadResources = false,     // Disable on‑demand download
        Language = Language.Tamil          // Set OCR language (see next step)
    }
};

// Load the image you want to recognize
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "tamil_note.jpg");

// Defensive check – helps you avoid the dreaded FileNotFoundException
if (!File.Exists(imagePath))
{
    Console.WriteLine($"Image not found at {imagePath}");
    return;
}

ocrEngine.LoadImage(imagePath);
```

**Συμβουλή επαγγελματία:** Τυλίξτε την κλήση `LoadImage` σε μπλοκ try‑catch αν η εφαρμογή σας επεξεργάζεται αρχεία που παρέχονται από χρήστες. Έτσι μπορείτε να εμφανίσετε φιλικό μήνυμα σφάλματος αντί για στοίβα εντολών.

---

## Βήμα 3: Ορισμός Γλώσσας OCR – Επιλέξτε το Σωστό Πακέτο

Αν παραλείψετε αυτό το βήμα, το Aspose προεπιλογή είναι τα Αγγλικά, κάτι που θα παράγει ακαταλαβίστικο κείμενο όταν η πηγαία γλώσσα είναι Tamil, Arabic ή οποιοδήποτε άλλο σύστημα γραφής. Η ρύθμιση της γλώσσας είναι τόσο απλή όσο η ανάθεση μιας τιμής enum, αλλά μπορείτε επίσης να περάσετε έναν προσαρμοσμένο κωδικό ISO‑639‑2 αν έχετε προσθέσει τρίτο πακέτο.

```csharp
// The language was already set in the config above, but you can change it at runtime:
ocrEngine.Config.Language = Language.Tamil; // Options: English, Arabic, ChineseSimplified, etc.
```

**Γιατί να σας ενδιαφέρει:** Η ακρίβεια του OCR εξαρτάται από μοντέλα χαρακτήρων ειδικά για κάθε γλώσσα. Η χρήση του σωστού πακέτου μπορεί να αυξήσει τα ποσοστά αναγνώρισης από 60 % σε πάνω από 95 % για πολλές γραφές.

---

## Βήμα 4: Εκτέλεση Αναγνώρισης και Λήψη Αποτελεσμάτων

Με όλα τα στοιχεία στη θέση τους — πόροι, εικόνα, γλώσσα — είμαστε έτοιμοι να εξάγουμε το κείμενο. Η μέθοδος `Recognize` κάνει όλη τη βαριά δουλειά και επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει τη ακατέργαστη συμβολοσειρά, βαθμούς εμπιστοσύνης και ακόμη και τα πλαίσια περιορισμού αν τα χρειάζεστε αργότερα.

```csharp
// Perform the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();

// Output the recognized text
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrResult.Text);
```

**Αναμενόμενο αποτέλεσμα:** Υποθέτοντας ότι το `tamil_note.jpg` περιέχει καθαρό χειρόγραφο Tamil, θα δείτε τους Unicode χαρακτήρες Tamil να εκτυπώνονται στην κονσόλα. Αν η εικόνα είναι θολή, το αποτέλεσμα μπορεί να περιλαμβάνει ερωτηματικά ή ακατανόητα σύμβολα — εδώ έρχεται χρήσιμη η προεπεξεργασία (απλοποίηση κλίσης, αφαίρεση θορύβου).

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται το ολοκληρωμένο πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα νέο έργο κονσόλας. Περιλαμβάνει όλες τις προστασίες που συζητήσαμε, ώστε να το τρέξετε αμέσως.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Define resources folder (offline OCR)
        // -------------------------------------------------
        string resourcesPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "Resources");
        if (!Directory.Exists(resourcesPath))
        {
            Console.WriteLine($"Resources folder not found at {resourcesPath}");
            return;
        }

        // -------------------------------------------------
        // Step 2: Configure OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            Config =
            {
                ResourcesPath = resourcesPath,
                AutoDownloadResources = false,
                Language = Language.Tamil // <-- set OCR language here
            }
        };

        // -------------------------------------------------
        // Step 3: Load the image you want to process
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "tamil_note.jpg");
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found at {imagePath}");
            return;
        }

        ocrEngine.LoadImage(imagePath);

        // -------------------------------------------------
        // Step 4: Run OCR and display the result
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize();

        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Εκτέλεση:**  
1. Τοποθετήστε το φάκελο `Resources` (που περιέχει τα αρχεία γλώσσας Tamil) δίπλα στο μεταγλωττισμένο `.exe`.  
2. Ρίξτε το `tamil_note.jpg` στον ίδιο φάκελο.  
3. Εκτελέστε `dotnet run` (ή τρέξτε το EXE).  

Θα πρέπει να δείτε το εξαγόμενο κείμενο Tamil να εμφανίζεται στην κονσόλα.

---

## Συχνές Ερωτήσεις & Ειδικές Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **Τι γίνεται αν πρέπει να επεξεργαστώ πολλαπλές εικόνες;** | Επαναχρησιμοποιήστε το ίδιο αντικείμενο `OcrEngine` — απλώς καλέστε ξανά το `LoadImage` πριν από κάθε `Recognize`. |
| **Μπορώ να αλλάξω τη γλώσσα εν κινήσει;** | Απολύτως. Ορίστε `ocrEngine.Config.Language = Language.English;` (ή οποιοδήποτε άλλο υποστηριζόμενο enum) πριν φορτώσετε την επόμενη εικόνα. |
| **Η εικόνα μου είναι σελίδα PDF — λειτουργεί αυτό;** | Όχι άμεσα. Μετατρέψτε τη σελίδα PDF σε εικόνα (π.χ., με Aspose.PDF) και μετά δώστε το bitmap στο `LoadImage`. |
| **Τι γίνεται αν λείπει το πακέτο γλώσσας;** | Η μηχανή θα ρίξει `FileNotFoundException`. Προστατέψτε το ελέγχοντας `Directory.Exists(resourcesPath)` (όπως φαίνεται). |
| **Μπορώ να λάβω βαθμούς εμπιστοσύνης;** | `ocrResult.Confidence` δίνει συνολικό σκορ· `ocrResult.Regions` περιέχει εμπιστοσύνη ανά χαρακτήρα αν χρειάζεστε λεπτομερή δεδομένα. |

---

## Συμβουλές Επαγγελματία για Παραγωγικό OCR

1. **Προεπεξεργασία εικόνων** — ευθυγράμμιση, αύξηση αντίθεσης και αφαίρεση θορύβου. Απλοί φίλτροι `System.Drawing` μπορούν να βελτιώσουν δραματικά την ακρίβεια.  
2. **Cache τη μηχανή** — η δημιουργία νέου `OcrEngine` για κάθε αίτηση είναι δαπανηρή. Διατηρήστε ένα singleton ανά γλώσσα σε υπηρεσία web.  
3. **Διαχείριση Unicode σωστά** — βεβαιωθείτε ότι η κονσόλα ή το UI σας χρησιμοποιεί UTF‑8· διαφορετικά οι μη‑λατινικοί χαρακτήρες θα εμφανίζονται ως “�”.  
4. **Καταγράψτε το ακατέργαστο αποτέλεσμα** — αποθηκεύστε το `ocrResult.Text` μαζί με την αρχική εικόνα για σκοπούς ελέγχου.  
5. **Ευγενική πτώση** — αν η εμπιστοσύνη πέσει κάτω από 0.6, σκεφτείτε να ζητήσετε από τον χρήστη νέα σάρωση ή να τρέξετε δεύτερη μηχανή OCR.

---

## Συμπέρασμα

Μόλις **εξάγαμε κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR, δείξαμε πώς να **φορτώσετε εικόνα για OCR** και παρουσιάσαμε τον σωστό τρόπο **ορισμού γλώσσας OCR** για αποτελέσματα εκτός σύνδεσης και υψηλής ακρίβειας. Το πλήρες, εκτελέσιμο παράδειγμα θα σας βάλει σε λειτουργία μέσα σε λίγα λεπτά, ενώ οι επιπλέον συμβουλές θα κρατήσουν την υλοποίησή σας ανθεκτική καθώς κλιμακώνετε.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αντικαταστήσετε το πακέτο Tamil με άλλη γλώσσα ή πειραματιστείτε με επεξεργασία παρτίδας πολλαπλών αρχείων ταυτόχρονα. Μπορείτε επίσης να εξερευνήσετε τα **εργαλεία προεπεξεργασίας εικόνας** της Aspose για να εξαγάγετε ακόμη μεγαλύτερη ακρίβεια από δύσκολες σάρωση.

Αν αντιμετωπίσετε πρόβλημα, αφήστε ένα σχόλιο παρακάτω — καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{</products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}