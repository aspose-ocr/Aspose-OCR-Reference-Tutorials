---
category: general
date: 2026-03-28
description: Μάθετε πώς να εξάγετε κείμενο από εικόνα σε C# ενώ φορτώνετε αρχείο εικόνας
  σε C# και ορίζετε τη γλώσσα OCR για επεξεργασία εκτός σύνδεσης. Δεν χρειάζεται internet.
draft: false
keywords:
- extract text from image
- load image file c#
- set ocr language
language: el
og_description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας τη λειτουργία offline
  του Aspose OCR. Οδηγός βήμα‑προς‑βήμα για τη φόρτωση αρχείου εικόνας σε C# και τον
  καθορισμό της γλώσσας OCR χωρίς κλήσεις δικτύου.
og_title: Εξαγωγή κειμένου από εικόνα σε C# – Πλήρης εκτός σύνδεσης οδηγός OCR
tags:
- OCR
- C#
- Aspose
title: Εξαγωγή κειμένου από εικόνα σε C# – Οδηγός OCR εκτός σύνδεσης
url: /el/net/text-recognition/extract-text-from-image-in-c-offline-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα σε C# – Οδηγός Offline OCR

Κάποτε χρειάστηκε να **εξάγετε κείμενο από εικόνα** αλλά σας ενοχλεί η ιδέα να στέλνετε αρχεία μέσω του διαδικτύου; Δεν είστε μόνοι. Σε πολλές ρυθμιζόμενες βιομηχανίες, τα δεδομένα δεν μπορούν να φύγουν από τα εγκαταστάσεις, οπότε μια λύση offline OCR γίνεται απαραίτητη. Αυτό το tutorial δείχνει ακριβώς πώς να εξάγετε κείμενο από εικόνα σε C# χρησιμοποιώντας το Aspose OCR σε offline λειτουργία—χωρίς κλήσεις δικτύου, μόνο καθαρή τοπική επεξεργασία.

Θα περάσουμε από τη φόρτωση ενός αρχείου εικόνας με κώδικα C#, τη διαμόρφωση του μοντέλου γλώσσας και, τέλος, την ανάκτηση του αναγνωρισμένου κειμένου από την εικόνα. Στο τέλος, θα έχετε μια έτοιμη για εκτέλεση εφαρμογή console που εξάγει κείμενο από εικόνα χωρίς ποτέ να αγγίξει το cloud. Χωρίς περιττά πρόσθετα, μόνο μια πρακτική, ολοκληρωμένη λύση που μπορείτε να ενσωματώσετε στα δικά σας έργα.

## Τι Θα Χρειαστείτε

- **.NET 6 ή νεότερο** (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework)
- **Aspose.OCR for .NET** πακέτο NuGet (έκδοση 23.6 ή νεότερη)
- Ένα δείγμα εικόνας (PNG, JPG ή TIFF) που περιέχει καθαρό, ευανάγνωστο κείμενο
- Visual Studio, Rider ή οποιονδήποτε επεξεργαστή C# προτιμάτε

Αυτό είναι όλο—χωρίς επιπλέον υπηρεσίες, χωρίς κλειδιά API. Αν έχετε ήδη περιβάλλον ανάπτυξης C#, είστε έτοιμοι.

## Βήμα 1 – Δημιουργία του OCR Engine και Ενεργοποίηση Offline Mode  

Το πρώτο που πρέπει να κάνετε είναι να δημιουργήσετε ένα αντικείμενο `OcrEngine` και να ενεργοποιήσετε τη σημαία `OfflineMode`. Αυτό λέει στο Aspose OCR να βασίζεται αποκλειστικά στα language packs που συνοδεύουν τη βιβλιοθήκη.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class OfflineModeTutorial
{
    static void Main()
    {
        // Initialize the OCR engine and force offline processing
        var ocrEngine = new OcrEngine
        {
            OfflineMode = true   // <-- crucial for on‑premise scenarios
        };
```

**Γιατί είναι σημαντικό:**  
Όταν το `OfflineMode` είναι `true`, η μηχανή δεν θα προσπαθήσει να κατεβάσει δεδομένα γλώσσας ή να στείλει τηλεμετρία. Αυτό εγγυάται τη συμμόρφωση με αυστηρές πολιτικές ιδιωτικότητας δεδομένων.

## Βήμα 2 – Φόρτωση Αρχείου Εικόνας σε Στυλ C#  

Τώρα που η μηχανή είναι έτοιμη, πρέπει να της δώσουμε μια εικόνα. Η φόρτωση ενός αρχείου εικόνας σε C# είναι παιχνιδάκι με τη μέθοδο `System.Drawing.Image.FromFile`. Απλώς βεβαιωθείτε ότι η διαδρομή δείχνει σε πραγματικό αρχείο στο δίσκο.

```csharp
        // Step 2: Load the image you want to process
        string imagePath = "YOUR_DIRECTORY/offline_test.png";
        ocrEngine.Image = Image.FromFile(imagePath);
```

> **Pro tip:** Αν στοχεύετε .NET Core σε Linux, προσθέστε το πακέτο `System.Drawing.Common` και ορίστε το `LD_LIBRARY_PATH` ώστε να δείχνει στο `libgdiplus`. Διαφορετικά θα εμφανιστεί εξαίρεση χρόνου εκτέλεσης.

**Προειδοποίηση για edge case:**  
Μια κενή ή κατεστραμμένη εικόνα θα προκαλέσει `FileNotFoundException` ή `ArgumentException`. Τυλίξτε τον κώδικα φόρτωσης σε block try‑catch αν αναμένετε ασταθή είσοδο.

## Βήμα 3 – Ορισμός OCR Γλώσσας Πριν από την Αναγνώριση  

Το Aspose OCR συνοδεύεται από αρκετά language packs, αλλά πρέπει να πείτε στη μηχανή ποια(ες) να χρησιμοποιήσει. Εδώ **ορίζουμε την OCR γλώσσα** για τη συνεδρία.

```csharp
        // Step 3: Specify the language model(s) that are available locally
        ocrEngine.Language = new[] { "English" }; // you can add more, e.g., "French", "Spanish"
```

**Γιατί πρέπει να ορίσετε τη γλώσσα:**  
Ο περιορισμός της μηχανής στις γλώσσες που πραγματικά χρειάζεστε επιταχύνει την αναγνώριση και μειώνει το αποτύπωμα μνήμης. Αν παραλείψετε αυτό το βήμα, η μηχανή θα προσπαθήσει να μαντέψει, κάτι που μπορεί να είναι πιο αργό και λιγότερο ακριβές.

## Βήμα 4 – Εκτέλεση της Λειτουργίας OCR  

Με όλα ρυθμισμένα, η πραγματική εξαγωγή κειμένου είναι μια μόνο κλήση μεθόδου. Η μέθοδος `Recognize` επιστρέφει το αναγνωρισμένο string.

```csharp
        // Step 4: Perform the OCR operation
        string recognizedText = ocrEngine.Recognize();

        // Step 5: Output the recognized text to the console
        Console.WriteLine(recognizedText);
    }
}
```

**Τι θα δείτε:**  
Αν η εικόνα περιέχει τη φράση “Hello World”, η κονσόλα θα εκτυπώσει:

```
Hello World
```

Αν η εικόνα έχει πολλαπλές γραμμές, κάθε γραμμή θα χωρίζεται με χαρακτήρα νέας γραμμής (`\n`). Μπορείτε να επεξεργαστείτε περαιτέρω το string—να αφαιρέσετε λευκούς χαρακτήρες, να το χωρίσετε σε λέξεις ή να το περάσετε σε μια downstream NLP pipeline.

## Πλήρες Παράδειγμα Λειτουργίας  

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο project console. Θυμηθείτε να αντικαταστήσετε το `YOUR_DIRECTORY/offline_test.png` με την πραγματική διαδρομή της εικόνας δοκιμής σας.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class OfflineModeTutorial
{
    static void Main()
    {
        // 1️⃣ Create OCR engine and enable offline mode
        var ocrEngine = new OcrEngine
        {
            OfflineMode = true
        };

        // 2️⃣ Load image file C# style
        string imagePath = "YOUR_DIRECTORY/offline_test.png";
        ocrEngine.Image = Image.FromFile(imagePath);

        // 3️⃣ Set OCR language (English only in this demo)
        ocrEngine.Language = new[] { "English" };

        // 4️⃣ Run OCR and capture the result
        string recognizedText = ocrEngine.Recognize();

        // 5️⃣ Show the output
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

Τρέξτε το πρόγραμμα (`dotnet run` από το τερματικό ή πατήστε F5 στο Visual Studio) και παρακολουθήστε την έξοδο της κονσόλας. Αν όλα είναι σωστά συνδεδεμένα, μόλις **εξάγετε κείμενο από εικόνα** χωρίς ποτέ να φύγετε από το μηχάνημά σας.

![Extract text from image using Aspose OCR offline mode](extract-text-image.png)

*Image alt text: “extract text from image using Aspose OCR offline mode”*  

## Συχνές Ερωτήσεις & Παγίδες  

- **Τι γίνεται αν χρειαστώ να αναγνωρίσω μια γλώσσα που δεν περιλαμβάνεται;**  
  Το Aspose OCR παρέχει επιπλέον language packs που μπορείτε να κατεβάσετε από το portal της Aspose. Τοποθετήστε το αρχείο `.dat` στον ίδιο φάκελο με το εκτελέσιμο σας και προσθέστε το όνομά του στον πίνακα `Language`.

- **Μπορώ να επεξεργαστώ PDFs αντί για PNGs;**  
  Ναι. Μετατρέψτε κάθε σελίδα PDF σε εικόνα πρώτα (π.χ., χρησιμοποιώντας το `Aspose.PDF`) και μετά περάστε το bitmap στη μηχανή OCR. Η ροή εργασίας παραμένει η ίδια.

- **Η μηχανή είναι thread‑safe;**  
  Ένα μόνο αντικείμενο `OcrEngine` δεν πρέπει να μοιράζεται μεταξύ νημάτων. Δημιουργήστε μια νέα μηχανή ανά αίτημα αν χτίζετε web service.

- **Συμβουλή απόδοσης:**  
  Για επεξεργασία παρτίδας, επαναχρησιμοποιήστε την ίδια μηχανή αλλά καλέστε `ocrEngine.Reset()` μεταξύ εικόνων. Αυτό αποφεύγει το κόστος επανεκκίνησης των δεδομένων γλώσσας.

## Επόμενα Βήματα  

Τώρα που μπορείτε να **εξάγετε κείμενο από εικόνα**, σκεφτείτε τις παρακάτω ιδέες επέκτασης:

1. **Διατήρηση αποτελεσμάτων** – γράψτε το αναγνωρισμένο κείμενο σε βάση δεδομένων ή αρχείο JSON.  
2. **Συνδυασμός με AI** – περάστε το αποτέλεσμα στις Azure Cognitive Services για ανάλυση συναισθήματος.  
3. **Λειτουργία παρτίδας** – κάντε βρόχο σε φάκελο εικόνων, συσσωρεύστε τα αποτελέσματα και δημιουργήστε μια αναφορά σύνοψης.  

Κάθε μία από αυτές τις επεκτάσεις θα περιλαμβάνει επίσης τη φόρτωση αρχείων εικόνας σε C# και πιθανώς τον ορισμό OCR γλώσσας για κάθε παρτίδα, αλλά το βασικό μοτίβο παραμένει αμετάβλητο.

---

### TL;DR  

- Χρησιμοποιήστε το `OfflineMode` του Aspose OCR για επεξεργασία on‑premise.  
- Φορτώστε την εικόνα με `Image.FromFile` (**load image file C#**).  
- Ορίστε τη γλώσσα με `ocrEngine.Language` (**set OCR language**).  
- Καλέστε `Recognize()` και έχετε επιτυχώς **εξάγει κείμενο από εικόνα**.

Δοκιμάστε το, τροποποιήστε τον πίνακα γλωσσών και δείτε πόσο γρήγορα μπορείτε να μετατρέψετε σαρωμένα έγγραφα σε αναζητήσιμο κείμενο. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}