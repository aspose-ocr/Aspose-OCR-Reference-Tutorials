---
category: general
date: 2026-02-17
description: Μάθετε πώς να εκτελείτε OCR σε εικόνα και να εξάγετε κείμενο από εικόνα
  χρησιμοποιώντας το Aspose OCR σε C#. Περιλαμβάνει τη φόρτωση αρχείου εικόνας, τη
  μετατροπή της εικόνας σε κείμενο και τη ρύθμιση της γλώσσας OCR.
draft: false
keywords:
- perform OCR on image
- extract text from image
- convert image to text
- load image file c#
- setup OCR language
language: el
og_description: Εκτελέστε OCR σε εικόνα σε C# και εξάγετε κείμενο από την εικόνα με
  το Aspose OCR. Οδηγός βήμα-προς-βήμα που καλύπτει τη φόρτωση του αρχείου εικόνας,
  τη ρύθμιση της γλώσσας OCR και τη μετατροπή της εικόνας σε κείμενο.
og_title: Εκτέλεση OCR σε εικόνα με C# – Πλήρης οδηγός Aspose OCR
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Εκτέλεση OCR σε εικόνα με C# – Πλήρης οδηγός Aspose OCR
url: /el/net/text-recognition/perform-ocr-on-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε εικόνα σε C# – Πλήρης Οδηγός Aspose OCR

Κάποτε χρειάστηκε να **perform OCR on image** αρχεία αλλά δεν ήξερες ποια βιβλιοθήκη να επιλέξεις για ένα έργο C#; Δεν είσαι μόνος. Σε πολλές πραγματικές εφαρμογές — σκεφτείτε σαρωτές αποδείξεων, αναγνώστες πολυγλωσσικών πινακίδων ή ψηφιοποίηση αρχείων — η δυνατότητα **extract text from image** γρήγορα είναι καθοριστική.

Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό παράδειγμα που δείχνει ακριβώς πώς να **perform OCR on image** χρησιμοποιώντας τη βιβλιοθήκη Aspose OCR, πώς να **load image file C#** κώδικα, και τα βήματα για **setup OCR language** για κείμενο Tamil. Στο τέλος θα μπορείτε να **convert image to text** με λίγες μόνο γραμμές κώδικα.

## Τι Θα Μάθετε

- Πώς να εγκαταστήσετε και να αναφέρετε το Aspose OCR σε ένα .NET project.  
- Τον ακριβή κώδικα που χρειάζεται για **load image file C#** και την παροχή του στην μηχανή OCR.  
- Πώς να **setup OCR language** (Tamil σε αυτήν την περίπτωση) ώστε η μηχανή να γνωρίζει ποιοι χαρακτήρες να περιμένει.  
- Πώς να **extract text from image** και να τον εμφανίσετε, παρέχοντάς σας ένα έτοιμο string για περαιτέρω επεξεργασία.  

> **Prerequisite:** .NET 6.0 ή νεότερο, Visual Studio (ή οποιοδήποτε C# IDE), και ένα πακέτο Aspose OCR NuGet. Δεν απαιτείται προηγούμενη εμπειρία OCR.

![perform OCR on image example](https://example.com/placeholder-image.png "perform OCR on image example")

## Βήμα 1: Εγκατάσταση Πακέτου Aspose OCR NuGet

Πριν μπορέσετε να **perform OCR on image**, χρειάζεστε τη βιβλιοθήκη Aspose OCR στο project σας. Ανοίξτε το NuGet Package Manager και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

*Pro tip:* Αν χρησιμοποιείτε Visual Studio, κάντε δεξί‑κλικ στο project → **Manage NuGet Packages** → αναζητήστε **Aspose.OCR** και κάντε κλικ στο **Install**. Αυτό θα φέρει όλες τις απαιτούμενες εξαρτήσεις, ώστε να μην χρειαστεί να ψάχνετε για επιπλέον DLLs.

## Βήμα 2: Δημιουργία Αντικειμένου OCR Engine

Το πρώτο κομμάτι κώδικα δημιουργεί ένα αντικείμενο `OcrEngine`, το οποίο είναι το κεντρικό στοιχείο που θα **convert image to text**. Σκεφτείτε το ως τον εγκέφαλο που ερμηνεύει τα μοτίβα των pixel.

```csharp
using System;
using Aspose.OCR;

class TamilOcrDemo
{
    static void Main()
    {
        // Step 2: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

Γιατί δημιουργούμε την μηχανή εδώ; Επειδή κρατά ρυθμίσεις—όπως η γλώσσα—και διαχειρίζεται εσωτερικούς πόρους. Η επαναχρησιμοποίηση ενός μόνο instance για πολλές εικόνες μπορεί επίσης να βελτιώσει την απόδοση.

## Βήμα 3: **Setup OCR Language** για Tamil

Το Aspose OCR υποστηρίζει δεκάδες γλώσσες, αλλά πρέπει να του πείτε ποια να ψάξει. Αυτό είναι το βήμα **setup OCR language** που αυξάνει δραστικά την ακρίβεια για μη‑λατινικά αλφάβητα.

```csharp
        // Step 3: Configure the engine to recognize Tamil text
        ocrEngine.Settings.Language = Language.Tamil;
```

Αν χρειαστεί ποτέ να αλλάξετε σε άλλη γλώσσα (π.χ., Hindi ή English), απλώς αντικαταστήστε το `Language.Tamil` με την αντίστοιχη τιμή enum. Η βιβλιοθήκη προεπιλογή είναι η Αγγλική, οπότε η ρητή ρύθμιση απαιτείται μόνο για άλλες γλώσσες.

## Βήμα 4: **Load Image File C#** – Παροχή της Εικόνας στην Μηχανή

Τώρα φορτώνουμε πραγματικά την **load image file C#**. Η μέθοδος `ImageStream.FromFile` διαβάζει το αρχείο από το δίσκο και το προετοιμάζει για OCR.

```csharp
        // Step 4: Load the image containing Tamil characters
        string imagePath = @"YOUR_DIRECTORY/tamil_sign.jpg";
        ImageStream image = ImageStream.FromFile(imagePath);
```

> **Note:** Χρησιμοποιήστε απόλυτη διαδρομή ή βεβαιωθείτε ότι η εικόνα έχει αντιγραφεί στον φάκελο εξόδου (`Copy to Output Directory → Copy always`). Αν το αρχείο δεν βρεθεί, η μηχανή θα ρίξει `FileNotFoundException`.

## Βήμα 5: Εκτέλεση OCR και **Extract Text from Image**

Με τη μηχανή ρυθμισμένη και την εικόνα φορτωμένη, η τελική κλήση εκτελεί πραγματικά **perform OCR on image** και επιστρέφει ένα `OcrResult` που περιέχει το αναγνωρισμένο κείμενο.

```csharp
        // Step 5: Perform OCR on the image
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 6: Output the recognized text to the console
        Console.WriteLine("Recognized Tamil text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Η μέθοδος `Recognize` κάνει όλη τη βαριά δουλειά: προεπεξεργασία, τμηματοποίηση, ταξινόμηση χαρακτήρων και μετα‑επεξεργασία. Το αποτέλεσμα μπορεί να αποθηκευτεί, να σταλεί σε βάση δεδομένων ή να χρησιμοποιηθεί σε οποιαδήποτε λογική επεξεργασίας.

### Αναμενόμενη Έξοδος

Αν το `tamil_sign.jpg` περιέχει τη λέξη “தமிழ்”, θα δείτε κάτι όπως:

```
Recognized Tamil text:
தமிழ்
```

Αν η εικόνα είναι θολή ή ο φωτισμός είναι χαμηλός, μπορεί να εμφανιστούν ακατάλληλοι χαρακτήρες — γι' αυτό πάντα δοκιμάζετε με εικόνες υψηλής ποιότητας.

## Πλήρες, Εκτελέσιμο Παράδειγμα

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο console project. Περιλαμβάνει όλα τα παραπάνω βήματα σε ένα ενιαίο μπλοκ.

```csharp
using System;
using Aspose.OCR;

class TamilOcrDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Setup OCR language – Tamil in this case
        ocrEngine.Settings.Language = Language.Tamil;

        // Step 3: Load the image containing Tamil characters
        string imagePath = @"YOUR_DIRECTORY/tamil_sign.jpg";
        ImageStream image = ImageStream.FromFile(imagePath);

        // Step 4: Perform OCR on the image
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 5: Extract text from image and display it
        Console.WriteLine("Recognized Tamil text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Τρέξτε το πρόγραμμα (`dotnet run` ή πατήστε **F5** στο Visual Studio) και παρακολουθήστε την κονσόλα να εκτυπώνει το εξαγόμενο κείμενο Tamil. Αυτός είναι ολόκληρος ο κύκλος εργασίας **convert image to text** σε λιγότερο από 30 γραμμές κώδικα.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν χρειαστεί να επεξεργαστώ πολλαπλές εικόνες;

Δημιουργήστε ένα μόνο αντικείμενο `OcrEngine`, στη συνέχεια κάντε βρόχο πάνω σε μια λίστα διαδρομών αρχείων, καλώντας `Recognize` κάθε φορά. Η επαναχρησιμοποίηση της μηχανής μειώνει το φορτίο μνήμης.

```csharp
foreach (var path in imagePaths)
{
    var img = ImageStream.FromFile(path);
    var result = ocrEngine.Recognize(img);
    Console.WriteLine($"{path}: {result.Text}");
}
```

### Πώς μπορώ να βελτιώσω την ακρίβεια για θορυβώδεις εικόνες;

- Χρησιμοποιήστε τις επιλογές `ocrEngine.Settings.ImagePreprocessing` (π.χ., `AutoRotate`, `Deskew`).  
- Αυξήστε το DPI κατά τη λήψη της εικόνας (300 dpi ή περισσότερο είναι ιδανικό).  
- Μετατρέψτε την εικόνα σε κλίμακα του γκρι πριν τη δώσετε στη μηχανή.

### Μπορώ να **convert image to text** σε άλλες γλώσσες χωρίς αλλαγή κώδικα;

Ναι. Απλώς αντικαταστήστε το enum γλώσσας:

```csharp
ocrEngine.Settings.Language = Language.English; // or Language.Hindi, etc.
```

Το υπόλοιπο του pipeline παραμένει αμετάβλητο.

## Συμπέρασμα

Δείξαμε πώς να **perform OCR on image** χρησιμοποιώντας το Aspose OCR σε C#. Ακολουθώντας τα βήματα — εγκατάσταση του πακέτου NuGet, **setup OCR language**, **load image file C#**, και τέλος **extract text from image** — έχετε τώρα έναν αξιόπιστο, έτοιμο για παραγωγή τρόπο να **convert image to text**.

Από εδώ μπορείτε να εξερευνήσετε επεξεργασία παρτίδων, ενσωμάτωση του αποτελέσματος OCR με API μετάφρασης, ή αποθήκευση των αποτελεσμάτων σε μια αναζητήσιμη βάση δεδομένων. Ό,τι και αν είναι το επόμενο βήμα σας, το βασικό μοτίβο παραμένει το ίδιο: αρχικοποιήστε τη μηχανή, ρυθμίστε τη γλώσσα, δώστε της μια εικόνα, και διαβάστε το κείμενο.

Έχετε περισσότερες ερωτήσεις για OCR, πολυγλωσσική υποστήριξη ή βελτιστοποίηση απόδοσης; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική διασκέδαση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}