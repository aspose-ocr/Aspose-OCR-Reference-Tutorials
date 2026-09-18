---
category: general
date: 2026-01-10
description: Πώς να διορθώσετε την κλίση μιας εικόνας και να βελτιώσετε τα αποτελέσματα
  OCR με το Aspose.OCR. Μάθετε πώς να προεπεξεργάζεστε την εικόνα για OCR, να αφαιρείτε
  τον θόρυβο από τη σάρωση και να αναγνωρίζετε κείμενο από τη σάρωση.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from scan
- how to use ocr
- remove noise from scan
language: el
og_description: Πώς να διορθώσετε την κλίση μιας εικόνας και να βελτιώσετε την ακρίβεια
  του OCR. Αυτός ο οδηγός δείχνει πώς να προεπεξεργαστείτε την εικόνα για OCR, να
  αφαιρέσετε τον θόρυβο από τη σάρωση και να αναγνωρίσετε το κείμενο από τη σάρωση
  χρησιμοποιώντας το Aspose.OCR.
og_title: Πώς να διορθώσετε την κλίση εικόνας σε C# – Πλήρης οδηγός προεπεξεργασίας
  OCR
tags:
- OCR
- C#
- Image Processing
title: Πώς να διορθώσετε την κλίση εικόνας σε C# – Πλήρης οδηγός προεπεξεργασίας OCR
url: /el/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να διορθώσετε την κλίση εικόνας σε C# – Ολοκληρωμένος Οδηγός Προεπεξεργασίας OCR

Έχετε αναρωτηθεί ποτέ **πώς να διορθώσετε την κλίση εικόνας** πριν τη δώσετε σε μια μηχανή OCR; Δεν είστε οι μόνοι. Τα σαρωμένα έγγραφα είναι συχνά κεκλιμένα, θορυβώδη ή χαμηλής αντίθεσης, και αυτό επηρεάζει οποιαδήποτε προσπάθεια αναγνώρισης κειμένου.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που **προετοιμάζει την εικόνα για OCR**, αφαιρεί τον θόρυβο από το σκαν, και τελικά **αναγνωρίζει κείμενο από το σκαν** χρησιμοποιώντας τη βιβλιοθήκη Aspose.OCR. Στο τέλος θα έχετε μια σαφή εικόνα για **πώς να χρησιμοποιήσετε OCR** σε C# κρατώντας τον κώδικα σύντομο και ευανάγνωστο.

> **Pro tip:** Ακόμη και μια μικρή περιστροφή (5‑10°) μπορεί να μειώσει την ακρίβεια του OCR κατά 30 % ή περισσότερο. Η διόρθωση κλίσης είναι το πρώτο βήμα που δεν πρέπει ποτέ να παραλείψετε.

---

## Τι θα χρειαστείτε

- **.NET 6+** (ο κώδικας λειτουργεί και σε .NET Framework, αλλά το .NET 6 είναι το τρέχον LTS)
- **Aspose.OCR for .NET** – μπορείτε να το αποκτήσετε από το NuGet (`Install-Package Aspose.OCR`)
- Ένα δείγμα αρχείου TIFF/PNG/JPEG που είναι περιστραμμένο ή θορυβώδες (θα χρησιμοποιήσουμε το `noisy_rotated.tif` στο παράδειγμα)
- Οποιοδήποτε IDE προτιμάτε – Visual Studio, Rider ή VS Code αρκούν

Αυτό είναι όλο. Χωρίς πρόσθετες βιβλιοθήκες, χωρίς εξωτερικές υπηρεσίες.

---

## Βήμα 1 – Φόρτωση της Πηγαίας Εικόνας (Γιατί είναι Σημαντικό)

Πριν μπορέσουμε να **διορθώσουμε την κλίση εικόνας**, πρέπει να τη διαβάσουμε σε ένα Aspose `ImageStream`. Αυτό το αντικείμενο αφαιρεί την πολυπλοκότητα του I/O αρχείων και παρέχει στη μηχανή OCR μια συνεπή διεπαφή.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the original scan – replace the path with your own file
var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");

// Quick sanity check – make sure the image loaded
if (sourceImage == null)
{
    Console.WriteLine("Failed to load the image. Check the path and file permissions.");
    return;
}
```

*Γιατί να φορτώσουμε πρώτα;* Επειδή όλα τα επόμενα φίλτρα λειτουργούν πάνω σε μια εικόνα στη μνήμη. Αν το αρχείο δεν μπορεί να διαβαστεί, ολόκληρη η αλυσίδα καταρρέει.

---

## Βήμα 2 – Δημιουργία Σειράς Προεπεξεργασίας (Διόρθωση Κλίσης + Αφαίρεση Θορύβου + Αντίθεση)

Μια αξιόπιστη ροή εργασίας OCR συνήθως συνδέει πολλά φίλτρα. Εδώ είναι που **προετοιμάζουμε την εικόνα για OCR** και, πιο σημαντικό, **πώς να διορθώσετε την κλίση εικόνας** αυτόματα.

```csharp
// Create a pipeline that will run three filters in order
var preprocessPipeline = new PreprocessPipeline()
{
    // 1️⃣ DeskewFilter – detects rotation up to 30° and corrects it
    new DeskewFilter { MaxAngle = 30 },

    // 2️⃣ DenoiseFilter – smooths out speckles while keeping edges
    new DenoiseFilter { Strength = 0.8 },

    // 3️⃣ ContrastBoostFilter – makes faint characters pop
    new ContrastBoostFilter { Level = 1.3 }
};
```

**Γιατί αυτά τα τρία;**  
- **DeskewFilter** λύνει το πρόβλημα «πώς να διορθώσετε την κλίση εικόνας» αυτόματα· δεν χρειάζεται να μαντέψετε τη γωνία.  
- **DenoiseFilter** αντιμετωπίζει την απαίτηση «αφαίρεση θορύβου από το σκαν», που αλλιώς δημιουργεί φανταστικούς χαρακτήρες.  
- **ContrastBoostFilter** βοηθά τη μηχανή OCR να διακρίνει το σκοτεινό κείμενο από το φωτεινό φόντο, ένα κλασικό ζήτημα όταν *προετοιμάζετε την εικόνα για OCR*.

---

## Βήμα 3 – Εφαρμογή της Σειράς (Δείτε τη Μεταμόρφωση)

Τώρα τρέχουμε τα φίλτρα. Η επιστρεφόμενη `processedImage` είναι αυτή που θα δώσουμε στη μηχανή OCR.

```csharp
// Apply all filters – the result is a cleaned‑up bitmap
var processedImage = preprocessPipeline.Apply(sourceImage);

// Optional: Save the cleaned image for visual verification
processedImage.Save("cleaned_output.tif");
Console.WriteLine("Image preprocessing complete – cleaned_output.tif saved.");
```

Αν ανοίξετε το `cleaned_output.tif`, θα παρατηρήσετε ότι το κείμενο είναι ευθεία, λιγότερο σπόρια και με υψηλότερη αντίθεση. Αυτός ο οπτικός έλεγχος είναι χρήσιμος όταν *αφαιρείτε θόρυβο από το σκαν* και θέλετε να επιβεβαιώσετε ότι η διόρθωση κλίσης λειτούργησε.

---

## Βήμα 4 – Δημιουργία και Διαμόρφωση της Μηχανής OCR (Πώς να Χρησιμοποιήσετε OCR)

Με μια καθαρή εικόνα στα χέρια, δημιουργούμε το `OcrEngine`. Αυτό είναι ο πυρήνας του **πώς να χρησιμοποιήσετε OCR** με την Aspose.

```csharp
// Initialize the OCR engine
var ocrEngine = new OcrEngine
{
    // Assign the pre‑processed image
    Image = processedImage,

    // Optional: Set language (English is default)
    // Language = Language.English,
    
    // Enable automatic page segmentation (helps with multi‑column scans)
    AutoPageSegmentation = true
};
```

*Γιατί ορίζουμε το `AutoPageSegmentation`;* Επειδή πολλά σκαν περιέχουν πίνακες ή πολλαπλές στήλες. Η ενεργοποίηση του επιτρέπει στη μηχανή να χωρίσει τη σελίδα έξυπνα, βελτιώνοντας το τελικό αποτέλεσμα **αναγνώρισης κειμένου από το σκαν**.

---

## Βήμα 5 – Εκτέλεση της Διαδικασίας Αναγνώρισης (Τέλος, Αναγνώριση Κειμένου)

Τώρα η στιγμή της αλήθειας: ζητάμε από τη μηχανή να διαβάσει το κείμενο.

```csharp
// Kick off the OCR process
ocrEngine.Recognize();

// Retrieve the plain‑text result
string recognizedText = ocrEngine.Text;

// Show the output in the console
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

Αν όλα πήγαν ομαλά, θα δείτε ένα καθαρό μπλοκ κειμένου που ταιριάζει με το αρχικό έγγραφο. Αυτό είναι το αποτέλεσμα της σωστής **διόρθωσης κλίσης εικόνας**, της **αφαίρεσης θορύβου** και της **προετοιμασίας εικόνας για OCR**.

---

## Βήμα 6 – Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι το πλήρες πρόγραμμα, έτοιμο για μεταγλώττιση. Απλώς αντικαταστήστε τη διαδρομή του αρχείου και είστε έτοιμοι.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");
        if (sourceImage == null)
        {
            Console.WriteLine("Unable to load image. Check the path.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Build the preprocessing pipeline
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
        {
            new DeskewFilter { MaxAngle = 30 },          // how to deskew image
            new DenoiseFilter { Strength = 0.8 },       // remove noise from scan
            new ContrastBoostFilter { Level = 1.3 }      // improves OCR accuracy
        };

        // -------------------------------------------------
        // 3️⃣ Apply the pipeline
        // -------------------------------------------------
        var processedImage = preprocessPipeline.Apply(sourceImage);
        processedImage.Save("cleaned_output.tif");
        Console.WriteLine("Preprocessing finished – cleaned_output.tif saved.");

        // -------------------------------------------------
        // 4️⃣ Configure the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Image = processedImage,
            AutoPageSegmentation = true   // how to use OCR effectively
        };

        // -------------------------------------------------
        // 5️⃣ Recognize text from scan
        // -------------------------------------------------
        ocrEngine.Recognize();
        string result = ocrEngine.Text;

        Console.WriteLine("\n=== Recognized Text ===");
        Console.WriteLine(result);
    }
}
```

**Αναμενόμενο αποτέλεσμα** (κομμένο για συντομία):

```
=== Recognized Text ===
This is a sample scanned document.
It contains several lines of text,
and the OCR engine has correctly read them.
```

Αν το αποτέλεσμα φαίνεται παραμορφωμένο, ελέγξτε ξανά ότι η πηγή δεν είναι περιστραμμένη περισσότερο από 30°, ή αυξήστε το `DeskewFilter.MaxAngle`.

---

## Συχνές Ερωτήσεις (Ακραίες Περιπτώσεις & Παραλλαγές)

| Ερώτηση | Απάντηση |
|----------|--------|
| **Τι γίνεται αν το σκαν είναι περιστραμμένο 45°;** | Το `DeskewFilter` περιορίζεται στο `MaxAngle`. Αυξήστε το (π.χ., `MaxAngle = 60`) ή προ‑περιστρέψτε την εικόνα με μια βιβλιοθήκη γραφικών πριν τη δώσετε στη σειρά. |
| **Μπορώ να επεξεργαστώ PDF σελίδα‑με‑σελίδα;** | Ναι. Μετατρέψτε κάθε σελίδα PDF σε εικόνα (π.χ., χρησιμοποιώντας `Aspose.Pdf`) και τρέξτε την ίδια σειρά σε κάθε bitmap. |
| **Το έγγραφό μου είναι στα Γαλλικά – χρειάζεται κάτι άλλο;** | Ορίστε `ocrEngine.Language = Language.French;` ή φορτώστε ένα προσαρμοσμένο language pack. Τα υπόλοιπα της σειράς παραμένουν ίδια. |
| **Υπάρχει τρόπος να διατηρήσω την αρχική ανάλυση;** | Το `PreprocessPipeline` λειτουργεί στο αρχικό bitmap, διατηρώντας το DPI. Απλώς αποφύγετε το `ImageStream.Resize` εκτός αν χρειάζεται να μειώσετε το μέγεθος για απόδοση. |
| **Πώς επηρεάζει η ενίσχυση αντίθεσης τις έγχρωμες σαρώσεις;** | Το `ContrastBoostFilter` λειτουργεί σε κάθε κανάλι· είναι ασφαλές για γκρι κλίμακα ή έγχρωμες εικόνες, αλλά μπορείτε επίσης να μετατρέψετε σε γκρι με `new GrayscaleFilter()`. |

---

## Παράδειγμα Εικόνας (Οπτική Βοήθεια)

![how to deskew image example](/images/deskew-example.png)

*Η εικόνα δείχνει πριν/μετά από ένα σκαν 12° περιστρεφόμενο, θορυβώδες, που έχει διορθωθεί και καθαριστεί.*

---

## Συμπέρασμα

Καλύψαμε **πώς να διορθώσετε την κλίση εικόνας** χρησιμοποιώντας το Aspose.OCR, παρουσιάσαμε μια πλήρη **συνεχόμενη προετοιμασία εικόνας για OCR**, δείξαμε πώς να **αφαιρέσετε θόρυβο από το σκαν**, και τελικά **αναγνωρίσαμε κείμενο από το σκαν** με λίγες γραμμές C#. Συνδυάζοντας τα `DeskewFilter`, `DenoiseFilter` και `ContrastBoostFilter` λαμβάνετε ένα καθαρό bitmap που επιτρέπει στη μηχανή OCR να κάνει τη δουλειά της χωρίς να “πνίγεται” από εναπομεινάρια.  

Τι θα κάνετε στη συνέχεια; Δοκιμάστε διαφορετικές εντάσεις φίλτρων, προσθέστε ένα `BinarizationFilter` για καθαρό μαύρο‑άσπρο αποτέλεσμα, ή δώστε την καθαρή εικόνα σε μια επόμενη NLP αλυσίδα. Το ίδιο μοτίβο λειτουργεί για αποδείξεις, διαβατήρια και ιστορικά έγγραφα.

Έχετε περισσότερες ερωτήσεις για **πώς να χρησιμοποιήσετε OCR** σε άλλες γλώσσες ή πλατφόρμες; Αφήστε ένα σχόλιο, και καλή προγραμματιστική διασκέδαση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}