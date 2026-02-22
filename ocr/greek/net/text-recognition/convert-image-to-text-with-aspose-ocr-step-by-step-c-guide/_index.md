---
category: general
date: 2026-02-22
description: Μετατρέψτε εικόνα σε κείμενο χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να καταχωρίσετε ένα γλωσσικό μοντέλο, να φορτώσετε εικόνα για OCR και να εξάγετε
  κείμενο από την εικόνα, συμπεριλαμβανομένης της υποστήριξης κυριλλικών.
draft: false
keywords:
- convert image to text
- extract text from image
- how to register module
- load image for ocr
- how to recognize cyrillic
language: el
og_description: Μετατρέψτε την εικόνα σε κείμενο άμεσα. Αυτός ο οδηγός δείχνει πώς
  να εγγράψετε το module, να φορτώσετε την εικόνα για OCR και να εξάγετε το κείμενο
  από την εικόνα, συμπεριλαμβανομένης της αναγνώρισης κυριλλικών.
og_title: Μετατροπή εικόνας σε κείμενο με Aspose OCR – Πλήρης οδηγός C#
tags:
- Aspose OCR
- C#
- Image Processing
title: Μετατροπή εικόνας σε κείμενο με Aspose OCR – Οδηγός βήμα‑προς‑βήμα C#
url: /el/net/text-recognition/convert-image-to-text-with-aspose-ocr-step-by-step-c-guide/
---

Pro tip" etc.

Let's produce the translated content.

Need to keep the shortcodes exactly as they appear.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή Εικόνας σε Κείμενο με Aspose OCR – Οδηγός Βήμα‑βήμα C#

Έχετε χρειαστεί ποτέ να **μετατρέψετε εικόνα σε κείμενο** αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν δυσκολίες όταν η εικόνα περιέχει μη‑λατινικούς χαρακτήρες όπως κυριλλικούς. Σε αυτό το tutorial θα περάσουμε από μια πλήρη, έτοιμη προς εκτέλεση λύση που δείχνει πώς να καταχωρίσετε ένα γλωσσικό module, να φορτώσετε μια εικόνα για OCR και, τέλος, να εξάγετε κείμενο από την εικόνα χρησιμοποιώντας το Aspose OCR για .NET.

Θα καλύψουμε τα πάντα, από την εγκατάσταση του πακέτου NuGet μέχρι τη διαχείριση περιπτώσεων όπως η έλλειψη αρχείων γλώσσας. Στο τέλος αυτού του οδηγού θα μπορείτε να **μετατρέψετε εικόνα σε κείμενο** με λίγες μόνο γραμμές C# και θα κατανοήσετε *γιατί* κάθε βήμα είναι σημαντικό.

## Τι Θα Μάθετε

- Πώς να **καταχωρίσετε το κυριλλικό γλωσσικό module** ώστε η μηχανή OCR να καταλαβαίνει το αλφάβητο.  
- Τον σωστό τρόπο **φόρτωσης εικόνας για OCR** με τη μέθοδο `Image.Load` του Aspose.  
- Πώς να ρυθμίσετε τη μηχανή ώστε **να αναγνωρίζει κυριλλικά** και στη συνέχεια **να εξάγει κείμενο από την εικόνα**.  
- Συμβουλές για την αντιμετώπιση κοινών προβλημάτων όπως κατεστραμμένα zip modules ή μη υποστηριζόμενες μορφές εικόνας.  

### Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+).  
- Visual Studio 2022 (ή οποιοδήποτε IDE που υποστηρίζει C#).  
- Πακέτο NuGet Aspose.OCR (`Install-Package Aspose.OCR`).  
- Ένα zip αρχείο γλώσσας κυριλλικών (`cyrillic.zip`) και ένα δείγμα εικόνας (`cyrillic_sample.jpg`).  

> **Pro tip:** Κρατήστε τα γλωσσικά modules σε έναν αφιερωμένο φάκελο (π.χ., `./ocr-modules/`) για να αποφύγετε σφάλματα σχετιζόμενα με διαδρομές.

---

## Βήμα 1: Πώς να Καταχωρίσετε το Module – Προσθήκη Υποστήριξης Κυριλλικών

Πριν η μηχανή OCR μπορέσει να διαβάσει κυριλλικούς χαρακτήρες, πρέπει να της πείτε πού βρίσκονται τα δεδομένα γλώσσας. Αυτό είναι το **πώς να καταχωρίσετε το module** μέρος της διαδικασίας.

```csharp
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to the Cyrillic language module (ZIP file)
string languageModulePath = Path.Combine("ocr-modules", "cyrillic.zip");

// Read the ZIP file into a byte array
byte[] moduleBytes = File.ReadAllBytes(languageModulePath);

// Register the module with the OCR engine
OcrEngine.RegisterLanguageModule(Language.Cyrillic, moduleBytes);
```

**Γιατί να καταχωρίσετε;**  
Το Aspose OCR παρέχει ένα προεπιλεγμένο σύνολο λατινικών γλωσσών για να διατηρεί τη βιβλιοθήκη ελαφριά. Καταχωρίζοντας το κυριλλικό module επεκτείνετε το λεξικό της μηχανής, επιτρέποντάς της να αντιστοιχίσει σωστά τα γλύφους σε χαρακτήρες Unicode. Η παράλειψη αυτού του βήματος κάνει τη μηχανή να προσπαθεί να μαντέψει, με αποτέλεσμα ακατάληπτο κείμενο.

> **Κοινό λάθος:** Χρήση σχετικής διαδρομής που δείχνει σε λάθος φάκελο. Πάντα να δημιουργείτε τη διαδρομή με `Path.Combine` ή να την επαληθεύετε με `File.Exists` πριν καλέσετε `RegisterLanguageModule`.

---

## Βήμα 2: Φόρτωση Εικόνας για OCR – Προετοιμασία Εισόδου

Τώρα που η γλώσσα είναι έτοιμη, πρέπει να φέρουμε την εικόνα στη μνήμη. Αυτό είναι το **βήμα φόρτωσης εικόνας για OCR**.

```csharp
using Aspose.OCR;

// Ensure the image exists
string imagePath = Path.Combine("ocr-images", "cyrillic_sample.jpg");
if (!File.Exists(imagePath))
{
    Console.WriteLine($"Image not found: {imagePath}");
    return;
}

// Load the image – Aspose automatically detects format (JPEG, PNG, BMP, etc.)
Image inputImage = Image.Load(imagePath);
```

**Γιατί να φορτώνετε με αυτόν τον τρόπο;**  
`Image.Load` αφαιρεί την ανίχνευση μορφής και τη μετατροπή χρωματικού χώρου, παρέχοντάς σας ένα συνεπές αντικείμενο `Image` ανεξάρτητα από τον τύπο του αρχείου προέλευσης. Αυτό μειώνει τις πιθανότητες σφαλμάτων *Unsupported format* που συχνά απογοητεύουν νέους χρήστες OCR.

> **Συμβουλή:** Αν χρειάζεται να προεπεξεργαστείτε την εικόνα (π.χ., ευθυγράμμιση ή δυαδικοποίηση), κάντε το *πριν* καλέσετε `Recognize`. Το Aspose παρέχει βοηθητικά εργαλεία `ImageProcessor` για αυτό.

---

## Βήμα 3: Ορισμός Γλώσσας & Μετατροπή Εικόνας σε Κείμενο

Με το module καταχωρημένο και την εικόνα φορτωμένη, μπορούμε τελικά να **μετατρέψουμε εικόνα σε κείμενο**. Αυτό το βήμα απαντά επίσης στο **πώς να αναγνωρίζετε κυριλλικά**.

```csharp
// Create an OCR engine instance and set its language to Cyrillic
var ocrEngine = new OcrEngine
{
    Language = Language.Cyrillic,
    // Optional: increase accuracy for noisy images
    // Settings = new OcrEngineSettings { EnableNoiseRemoval = true }
};

// Run the recognition process
OcrResult ocrResult = ocrEngine.Recognize(inputImage);
```

**Γιατί να ορίσετε ρητά τη γλώσσα;**  
Ακόμη και μετά την καταχώρηση, η μηχανή προεπιλέγει τα Αγγλικά. Η καθορισμένη τιμή `Language.Cyrillic` κατευθύνει τη μηχανή να χρησιμοποιήσει το νεοκαταχωρημένο λεξικό, βελτιώνοντας δραστικά την ακρίβεια για σλαβικές γραφές.

> **Ακραία περίπτωση:** Αν προσπαθήσετε να αναγνωρίσετε μια εικόνα χωρίς να ορίσετε τη γλώσσα, το Aspose θα επιστρέψει Λατινικά, παράγοντας ακατανόητους χαρακτήρες για κυριλλικό κείμενο.

---

## Βήμα 4: Εξαγωγή Κειμένου από την Εικόνα – Λήψη Αποτελέσματος

Το αντικείμενο `OcrResult` περιέχει το ακατέργαστο κείμενο, τις βαθμολογίες εμπιστοσύνης και τα δεδομένα θέσης. Για τις περισσότερες περιπτώσεις χρειάζεστε μόνο το απλό κείμενο.

```csharp
// Display the recognized text in the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);

// Optional: check confidence (0‑100)
// Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
```

**Γιατί να ελέγχετε την εμπιστοσύνη;**  
Η βαθμολογία εμπιστοσύνης δείχνει πόσο αξιόπιστο είναι το αποτέλεσμα OCR. Τιμές πάνω από 80% θεωρούνται γενικά ασφαλείς για επεξεργασία, ενώ χαμηλότερες μπορεί να απαιτούν χειροκίνητη επανεξέταση ή προεπεξεργασία εικόνας.

> **Τι γίνεται αν το αποτέλεσμα είναι κενό;**  
Συνηθισμένοι λόγοι περιλαμβάνουν λανθασμένο γλωσσικό module, κατεστραμμένη εικόνα ή εικόνα με πολύ χαμηλή αντίθεση. Δοκιμάστε να αυξήσετε την αντίθεση ή να χρησιμοποιήσετε `ImageProcessor.AdjustContrast` πριν την αναγνώριση.

---

## Πλήρες Παράδειγμα Λειτουργικού Κώδικα

Παρακάτω βρίσκεται το πλήρες, έτοιμο για αντιγραφή‑και‑επικόλληση πρόγραμμα που ενώνει όλα τα βήματα. Αποθηκεύστε το ως `Program.cs` και τρέξτε το από τη ρίζα του έργου σας.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Register the Cyrillic language module
        // -------------------------------------------------
        string languageModulePath = Path.Combine("ocr-modules", "cyrillic.zip");
        if (!File.Exists(languageModulePath))
        {
            Console.WriteLine($"Language module not found: {languageModulePath}");
            return;
        }
        OcrEngine.RegisterLanguageModule(Language.Cyrillic, File.ReadAllBytes(languageModulePath));

        // -------------------------------------------------
        // Step 2: Load the image you want to convert
        // -------------------------------------------------
        string imagePath = Path.Combine("ocr-images", "cyrillic_sample.jpg");
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }
        Image inputImage = Image.Load(imagePath);

        // -------------------------------------------------
        // Step 3: Create OCR engine and set language
        // -------------------------------------------------
        var ocrEngine = new OcrEngine { Language = Language.Cyrillic };

        // -------------------------------------------------
        // Step 4: Recognize and extract text
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 5: Output the result
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Αναμενόμενο Αποτέλεσμα**

```
=== OCR Result ===
Привет мир! Это пример текста на кириллице.
```

Αν δείτε ακατανόητο κείμενο αντί για κυριλλικά, ελέγξτε ξανά ότι το αρχείο `cyrillic.zip` ταιριάζει με την έκδοση του Aspose OCR που έχετε εγκαταστήσει και ότι η εικόνα είναι αρκετά καθαρή για αναγνώριση.

---

## Συχνές Ερωτήσεις (FAQ)

**Ε: Μπορώ να χρησιμοποιήσω αυτή τη μέθοδο για άλλες γλώσσες;**  
Α: Φυσικά. Αντικαταστήστε το `Language.Cyrillic` με το αντίστοιχο enum (π.χ., `Language.Arabic`) και καταχωρίστε το αντίστοιχο ZIP αρχείο.

**Ε: Ποιες μορφές εικόνας υποστηρίζονται;**  
Α: JPEG, PNG, BMP, TIFF και GIF υποστηρίζονται εγγενώς από το `Image.Load`. Για PDF χρειάζεστε το Aspose.PDF, έπειτα μετατρέψτε τις σελίδες σε εικόνες πριν το OCR.

**Ε: Πώς μπορώ να βελτιώσω την ακρίβεια σε χαμηλής ποιότητας σκαναρίσματα;**  
Α: Προεπεξεργαστείτε την εικόνα—εφαρμόστε δυαδικοποίηση, ευθυγράμμιση ή αφαίρεση θορύβου χρησιμοποιώντας `ImageProcessor`. Επίσης, αυξήστε ρυθμίσεις του `OcrEngineSettings` όπως `EnableNoiseRemoval` και `EnableTextSegmentation`.

**Ε: Υπάρχει τρόπος να λάβω το πλαίσιο (bounding box) κάθε λέξης;**  
Α: Ναι. Το `OcrResult` περιέχει τη συλλογή `Regions` όπου κάθε περιοχή έχει δεδομένα `Location`. Επανάληψη μέσω `ocrResult.Regions` θα σας δώσει τις συντεταγμένες.

---

## Συμπέρασμα

Σας δείξαμε πώς να **μετατρέψετε εικόνα σε κείμενο** με το Aspose OCR, καλύπτοντας όλα από το **πώς να καταχωρίσετε το module** μέχρι το **φόρτωση εικόνας για OCR** και τελικά την **εξαγωγή κειμένου από την εικόνα** ενώ **αναγνωρίζετε κυριλλικά**. Ο πλήρης κώδικας παραπάνω είναι έτοιμος για εκτέλεση, και οι εξηγήσεις σας δίνουν το *γιατί* πίσω από κάθε γραμμή—ώστε να προσαρμόσετε τη λύση σε άλλες γλώσσες ή πιο σύνθετες ροές εργασίας.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε τη μετατροπή πολυσελίδων PDF, ενσωματώστε το αποτέλεσμα OCR σε ευρετήριο αναζήτησης ή συνδυάστε το με τις Azure Cognitive Services για ανίχνευση γλώσσας. Ο ουρανός είναι το όριο μόλις κυριαρχήσετε τα βασικά της μετατροπής εικόνας‑σε‑κείμενο.

---

![convert image to text example](image-placeholder.png "μετατροπή εικόνας σε κείμενο")

*Καλό προγραμματισμό! Αν αντιμετωπίσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω και θα τα λύσουμε μαζί.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}