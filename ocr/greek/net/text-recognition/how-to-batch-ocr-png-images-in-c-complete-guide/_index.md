---
category: general
date: 2026-03-17
description: Πώς να κάνετε μαζική OCR εικόνων PNG σε C# γρήγορα. Μάθετε να εξάγετε
  κείμενο από αρχεία PNG, να μετατρέπετε PNG σε κείμενο και να διαβάζετε εικόνες από
  φάκελο με ένα απλό script.
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: el
og_description: Πώς να κάνετε ομαδική OCR εικόνων PNG σε C# με βήμα‑βήμα κώδικα. Εξάγετε
  κείμενο από αρχεία PNG, μετατρέψτε PNG σε κείμενο και διαβάστε εικόνες από φάκελο
  χωρίς κόπο.
og_title: Πώς να εκτελέσετε ομαδική OCR σε εικόνες PNG με C# – Πλήρης οδηγός
tags:
- OCR
- C#
- Image Processing
title: Πώς να κάνετε ομαδική OCR εικόνων PNG σε C# – Πλήρης οδηγός
url: /el/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εκτελέσετε Batch OCR σε εικόνες PNG σε C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε batch OCR** σε έναν φάκελο γεμάτο στιγμιότυπα οθόνης χωρίς να ανοίγετε κάθε αρχείο χειροκίνητα; Δεν είστε ο μόνος—οι προγραμματιστές ρωτούν συνεχώς πώς να κάνουν batch OCR μεγάλων συλλογών PNG, ειδικά όταν ο στόχος είναι η εξαγωγή κειμένου από αρχεία PNG για ανάλυση downstream.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα ένα έτοιμο προς εκτέλεση παράδειγμα C# που **εξάγει κείμενο PNG** αρχεία, **μετατρέπει PNG σε κείμενο**, και σας δείχνει τον καλύτερο τρόπο για **ανάγνωση εικόνων από φάκελο**. Στο τέλος θα έχετε ένα ενιαίο script που δημιουργεί ένα `.txt` δίπλα σε κάθε εικόνα, εξοικονομώντας σας ώρες χειροκίνητης αντιγραφής‑επικόλλησης.

## Τι Θα Επιτύχετε

- Αρχικοποιήστε μια μηχανή OCR μία φορά και επαναχρησιμοποιήστε την για ολόκληρο το batch.  
- Σαρώστε κάθε `*.png` σε έναν δεδομένο φάκελο χωρίς να γράψετε βρόχο εσείς.  
- Γράψτε κάθε αποτέλεσμα OCR σε δικό του αρχείο κειμένου, διατηρώντας το αρχικό όνομα αρχείου.  
- Διαχειριστείτε κοινές περιπτώσεις άκρων όπως κενά φακέλους ή αρχεία που δεν είναι εικόνες με χάρη.

### Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Core και .NET Framework).  
- Μια βιβλιοθήκη OCR που εκθέτει τύπους `OcrEngine`, `ImageStream` και `OcrResult` (για παράδειγμα, το φανταστικό SDK **FastOCR** που χρησιμοποιείται στα αποσπάσματα).  
- Βασικές γνώσεις C#—δεν απαιτούνται προχωρημένα patterns.

---

## Πώς να κάνετε Batch OCR σε εικόνες PNG – Επισκόπηση

Παρακάτω βρίσκεται το **πλήρες, εκτελέσιμο πρόγραμμα**. Μπορείτε να το αντιγράψετε‑επικολλήσετε σε ένα νέο κονσόλα project, να αντικαταστήσετε τις διαδρομές placeholder, και να πατήσετε **F5**.

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **Αναμενόμενο αποτέλεσμα:** Για κάθε `image01.png` θα βρείτε ένα `image01.txt` που περιέχει τους αναγνωρισμένους χαρακτήρες. Η κονσόλα θα εμφανίζει κάθε αρχείο καθώς γράφεται.

![Διάγραμμα για batch OCR](how-to-batch-ocr-diagram.png "Διάγραμμα που απεικονίζει πώς να κάνετε batch OCR σε εικόνες PNG χρησιμοποιώντας C#")

---

## Εξήγηση Βήμα‑βήμα

### 1. Αρχικοποίηση της Μηχανής OCR – η Καρδιά της Διαδικασίας  

Η γραμμή `var ocrEngine = new OcrEngine();` δημιουργεί μια μοναδική παρουσία της μηχανής που θα επαναχρησιμοποιηθεί για ολόκληρο το batch. Η επαναχρησιμοποίηση της μηχανής είναι **καίρια** επειδή οι περισσότερες βιβλιοθήκες OCR εκχωρούν βαριά πόρους (όπως μοντέλα γλώσσας) κατά την κατασκευή. Η αρχικοποίηση μία φορά βελτιώνει δραματικά την απόδοση—ιδιαίτερα όταν έχετε δεκάδες ή εκατοντάδες PNG.

> **Συμβουλή:** Αν χρειάζεστε γλώσσα διαφορετική από τα Αγγλικά, ορίστε `ocrEngine.Config.Language = Language.Spanish;` (ή οποιοδήποτε υποστηριζόμενο enum).  

### 2. Ανάγνωση Εικόνων από Φάκελο – εντοπισμός κάθε PNG  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` κάνει ακριβώς αυτό που υπόσχεται η δευτερεύουσα λέξη-κλειδί *read images from directory*. Επιστρέφει έναν πίνακα από απόλυτες διαδρομές, τις οποίες αργότερα τροφοδοτούμε στη μηχανή OCR.  

> **Γιατί να μην χρησιμοποιήσετε `SearchOption.AllDirectories`;** Αν οι εικόνες σας είναι ενσωματωμένες σε υποφακέλους, μπορείτε να μεταβείτε σε `GetFiles(path, "*.png", SearchOption.AllDirectories)`. Απλώς θυμηθείτε ότι οι πιο βαθιές σάρωση μπορεί να φέρει ανεπιθύμητα αρχεία, οπότε φιλτράρετε αναλόγως.

### 3. Μετατροπή Διαδρομών Αρχείων σε Αντικείμενα ImageStream  

Οι περισσότερες SDK OCR αναμένουν ένα stream αντί για μια ακατέργαστη διαδρομή. Η έκφραση LINQ `Select(path => ImageStream.FromFile(path)).ToList()` δημιουργεί μια **λίστα από streams** που ο batch recognizer μπορεί να καταναλώσει σε μία κλήση. Αυτό το βήμα εξασφαλίζει επίσης ότι τα handles αρχείων ανοίγονται μόνο μία φορά, μειώνοντας το I/O overhead.

> **Περιπτωση άκρου:** Αν ένα αρχείο είναι κατεστραμμένο, το `ImageStream.FromFile` μπορεί να ρίξει εξαίρεση. Τυλίξτε τη μετατροπή σε `try/catch` αν χρειάζεστε ανθεκτικότητα.

### 4. Αναγνώριση Κειμένου σε Ολόκληρο το Batch  

`ocrEngine.RecognizeBatch(imageStreams)` είναι το ιδανικό σημείο για *how to batch OCR*. Αντί να κάνετε βρόχο πάνω σε κάθε εικόνα και να καλέσετε τη μέθοδο single‑image, δίνουμε ολόκληρη τη συλλογή στη μηχανή. Εσωτερικά η βιβλιοθήκη μπορεί να παραλληλοποιήσει την εργασία, δίνοντάς σας επιπλέον ταχύτητα σε πολυπύρηνες μηχανές.

> **Συμβουλή:** Αν η βιβλιοθήκη OCR σας δεν εκθέτει μέθοδο batch, μπορείτε ακόμη να πετύχετε παρόμοια απόδοση χρησιμοποιώντας `Parallel.ForEach` γύρω από την κλήση single‑image `Recognize`.

### 5. Γράψιμο Κάθε Αποτελέσματος OCR – μετατροπή PNG σε κείμενο  

Ο τελικός βρόχος `for` γράφει το `ocrResults[i].Text` σε ένα αρχείο `.txt` του οποίου το όνομα αντικατοπτρίζει το αρχικό PNG. Αυτό είναι ακριβώς αυτό που περιγράφει η δευτερεύουσα λέξη-κλειδί *convert PNG to text*. Η κλήση `Path.Combine` εγγυάται ότι ο φάκελος εξόδου υπάρχει και αποτρέπει σφάλματα διαπέρασης διαδρομής.

> **Κοινό λάθος:** Η παράλειψη δημιουργίας του φακέλου εξόδου πρώτα θα προκαλέσει `DirectoryNotFoundException`. Η γραμμή `Directory.CreateDirectory(outputFolder);` το λύνει προληπτικά.

## Διαχείριση Πραγματικών Παραλλαγών

| Situation | What to Change | Why |
|-----------|----------------|-----|
| **Κενός φάκελος εισόδου** | Διατηρήστε το αρχικό guard `if (imagePaths.Length == 0)` | Αποτρέπει μια περιττή κλήση OCR και παρέχει φιλικό μήνυμα |
| **Ανάμεικτοι τύποι αρχείων** | Χρησιμοποιήστε `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` | Εγγυάται ότι επεξεργάζεστε μόνο PNG, ικανοποιώντας το *extract text png* χωρίς σφάλματα |
| **Μεγάλες εικόνες ( > 5 MB )** | Μειώστε την ανάλυση πριν την τροφοδοσία στο OCR: `ImageStream.FromFile(path).Resize(1920, 1080)` (αν υποστηρίζεται από το API) | Μειώνει την πίεση μνήμης και συχνά βελτιώνει την ακρίβεια αναγνώρισης |
| **Διαφορετική γλώσσα OCR** | Ορίστε `ocrEngine.Config.Language = Language.French;` | Ευθυγραμμίζει τη μηχανή με τη γλώσσα των πηγαίων εικόνων |

## Συχνές Ερωτήσεις (FAQ)

**Q: Λειτουργεί αυτό με αρχεία JPEG ή TIFF;**  
A: Η βασική λογική παραμένει η ίδια· απλώς αλλάξτε το μοτίβο αναζήτησης σε `"*.jpg"` ή `"*.tif"` και βεβαιωθείτε ότι η βιβλιοθήκη OCR μπορεί να αποκωδικοποιήσει αυτές τις μορφές.

**Q: Πώς μπορώ να επεξεργαστώ χιλιάδες εικόνες χωρίς να εξαντλήσω τη μνήμη;**  
A: Αντικαταστήστε την κλήση batch με μια προσέγγιση streaming—επεξεργαστείτε ένα τμήμα, π.χ. 50 εικόνες τη φορά, και μετά απελευθερώστε τα streams πριν φορτώσετε το επόμενο τμήμα.

**Q: Χρειάζομαι το σκορ εμπιστοσύνης OCR. Πού το βρίσκω;**  
A: Τα περισσότερα αντικείμενα `OcrResult` εκθέτουν μια ιδιότητα `Confidence`. Μπορείτε να επεκτείνετε το βήμα εγγραφής:

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

## Συμπέρασμα

Μόλις καλύψαμε **πώς να κάνετε batch OCR** σε εικόνες PNG σε C# από την αρχή μέχρι το τέλος. Αρχικοποιώντας μια μοναδική μηχανή, διαβάζοντας εικόνες από φάκελο, μετατρέποντάς τες σε streams, αναγνωρίζοντας ολόκληρο το batch, και τελικά γράφοντας κάθε αποτέλεσμα σε αρχείο κειμένου, έχετε τώρα ένα σταθερό, έτοιμο για παραγωγή πρότυπο για εργασίες **extract text PNG**, **convert PNG to text**, και **read images from directory**.

Τι ακολουθεί; Δοκιμάστε να αλλάξετε τον πάροχο OCR, προσθέστε πολυνηματική επεξεργασία (π.χ., ορθογραφικό έλεγχο), ή τροφοδοτήστε τα αρχεία `.txt` σε έναν δείκτη αναζήτησης. Ο ουρανός είναι το όριο μόλις κυριαρχήσετε τη ροή εργασίας batch.

Έχετε μια παραλλαγή που θέλετε να μοιραστείτε; Αφήστε ένα σχόλιο, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}