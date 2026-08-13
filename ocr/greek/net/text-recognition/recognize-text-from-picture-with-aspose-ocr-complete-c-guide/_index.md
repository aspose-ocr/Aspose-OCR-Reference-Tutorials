---
category: general
date: 2026-03-05
description: Μάθετε πώς να αναγνωρίζετε κείμενο από εικόνα χρησιμοποιώντας το Aspose
  OCR σε C#. Περιλαμβάνει βήματα για την εξαγωγή κειμένου από JPEG, τη μετατροπή της
  εικόνας σε κείμενο και τη φόρτωση της εικόνας για OCR.
draft: false
keywords:
- recognize text from picture
- extract text from jpeg
- convert image to text
- load image for ocr
- recognize hindi text image
language: el
og_description: Αναγνώριση κειμένου από εικόνα σε C# χρησιμοποιώντας Aspose OCR. Οδηγός
  βήμα‑βήμα για την εξαγωγή κειμένου από JPEG, τη μετατροπή εικόνας σε κείμενο και
  τη φόρτωση εικόνας για OCR.
og_title: αναγνώριση κειμένου από εικόνα – Πλήρης οδηγός Aspose OCR σε C#
tags:
- OCR
- C#
- Aspose
title: Αναγνώριση κειμένου από εικόνα με Aspose OCR – Πλήρης οδηγός C#
url: /el/net/text-recognition/recognize-text-from-picture-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση κειμένου από εικόνα – Πλήρης Οδηγός C# Aspose OCR

Έχετε ποτέ χρειαστεί να αναγνωρίσετε κείμενο από εικόνα αλλά δεν ξέρατε ποια βιβλιοθήκη θα κάνει πραγματικά τη σκληρή δουλειά; Δεν είστε μόνοι. Σε πολλές πραγματικές εφαρμογές—σκεφτείτε σαρωτές τιμολογίων, αναγνώστες αποδείξεων ή εργαλεία μετάφρασης πολυγλωσσικών πινακίδων—η δυνατότητα εξαγωγής χαρακτήρων από ένα JPEG ή PNG είναι απολύτως κρίσιμη.

Σε αυτόν τον οδηγό θα σας δείξουμε **ακριβώς** πώς να αναγνωρίσετε κείμενο από εικόνα με το Aspose OCR για .NET. Στο τέλος θα μπορείτε να εξάγετε κείμενο από αρχεία jpeg, να μετατρέψετε εικόνα σε κείμενο και ακόμη να αναγνωρίσετε εικόνα με κείμενο στα Χίντι με λίγες γραμμές κώδικα. Χωρίς ασαφείς αναφορές, μόνο ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο Visual Studio τώρα.

## Τι Θα Μάθετε

- Πώς να **φορτώσετε εικόνα για OCR** χρησιμοποιώντας ένα stream που λειτουργεί με οποιονδήποτε τύπο αρχείου.  
- Η διαφορά μεταξύ **εξαγωγής κειμένου από jpeg** και γενικής μετατροπής εικόνας, και γιατί η βιβλιοθήκη διαχειρίζεται και τα δύο αδιάλειπτα.  
- Πώς να **μετατρέψετε εικόνα σε κείμενο** με μία κλήση μεθόδου, και στη συνέχεια να εμφανίσετε το αποτέλεσμα.  
- Συγκεκριμένα βήματα για **αναγνώριση εικόνας με κείμενο στα Χίντι**—συμπεριλαμβανομένης της αυτόματης λήψης δεδομένων γλώσσας.  
- Συνηθισμένα προβλήματα (τοποθέτηση άδειας, διαρροές μνήμης) και επαγγελματικές συμβουλές που σας εξοικονομούν χρόνο εντοπισμού σφαλμάτων.

> **Προαπαιτούμενα** – .NET 6+ (ή .NET Framework 4.7.2), Visual Studio 2022, και αρχείο άδειας Aspose OCR (`Aspose.OCR.lic`). Αν δεν έχετε ακόμη άδεια, μπορείτε να ζητήσετε ένα δωρεάν προσωρινό κλειδί από τον ιστότοπο της Aspose.

---

## Βήμα 1 – Αναγνώριση κειμένου από εικόνα: Αρχικοποίηση του OCR Engine

Πριν μπορέσουμε να κάνουμε οτιδήποτε, χρειαζόμαστε μια παρουσία `OcrEngine` και μια έγκυρη άδεια. Η μηχανή είναι το κεντρικό αντικείμενο που συντονίζει την ανάλυση εικόνας, την ανίχνευση γλώσσας και την εξαγωγή κειμένου.

```csharp
using Aspose.OCR;          // Core OCR namespace
using System;              // For Console
using Aspose.OCR.Models;   // For language enums

// Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Apply your license – replace the path with the actual location of Aspose.OCR.lic
ocrEngine.SetLicense("Aspose.OCR.lic");

// Optional: Verify that the license was applied (helps during debugging)
if (ocrEngine.IsLicensed)
    Console.WriteLine("License applied successfully.");
else
    Console.WriteLine("Warning: Running in evaluation mode.");
```

**Γιατί είναι σημαντικό:** Χωρίς σωστή άδεια η μηχανή επιστρέφει σε δοκιμαστική έκδοση 30 ημερών που προσθέτει υδατογράφημα στο αποτέλεσμα και περιορίζει την ακρίβεια. Η άμεση εφαρμογή της άδειας αποφεύγει επίσης μια σιωπηλή ποινή απόδοσης αργότερα.

---

## Βήμα 2 – Φόρτωση εικόνας για OCR (εξαγωγή κειμένου από jpeg ή PNG)

Τώρα πρέπει να τροφοδοτήσουμε τη μηχανή με μια εικόνα. Το Aspose OCR λειτουργεί με streams, πράγμα που σημαίνει ότι μπορείτε να φορτώσετε ένα αρχείο από δίσκο, από απάντηση δικτύου ή ακόμη και από bitmap στη μνήμη. Εδώ είναι η πιο απλή περίπτωση—ανάγνωση ενός JPEG από το φάκελο του έργου σας.

```csharp
// Path to the picture you want to process
string imagePath = @"YOUR_DIRECTORY\hindi_sample.jpg";

// Open a stream that the OCR engine can consume
using (var imageStream = ImageStream.FromFile(imagePath))
{
    // Assign the stream to the engine
    ocrEngine.Image = imageStream;

    Console.WriteLine($"Loaded image: {imagePath}");
    // The using block ensures the stream is disposed automatically.
}
```

> **Συμβουλή:** Αν σκοπεύετε να επεξεργάζεστε πολλές εικόνες σε βρόχο, κρατήστε τη παρουσία `OcrEngine` ενεργή και αντικαταστήστε μόνο το `ocrEngine.Image` σε κάθε επανάληψη. Αυτό επαναχρησιμοποιεί εσωτερικά buffers και επιταχύνει την επεξεργασία παρτίδας.

---

## Βήμα 3 – Επιλογή γλώσσας Χίντι (αναγνώριση εικόνας με κείμενο στα Χίντι)

Το Aspose OCR υποστηρίζει πάνω από 130 γλώσσες και θα κατεβάσει το απαιτούμενο πακέτο γλώσσας την πρώτη φορά που το ζητήσετε. Επειδή το δείγμα μας περιέχει γραφή Devanagari, ορίζουμε τη γλώσσα σε Χίντι.

```csharp
// Tell the engine which language to look for
ocrEngine.Language = OcrLanguage.Hindi;   // Supports 130+ languages

Console.WriteLine("Language set to Hindi. If the data isn’t cached, it will be downloaded now.");
```

**Τι συμβαίνει στο παρασκήνιο;** Η βιβλιοθήκη ελέγχει έναν τοπικό φάκελο cache (`%AppData%\Aspose\OCR\`) για το μοντέλο Χίντι. Αν δεν υπάρχει, ένα μικρό αρχείο (~5 MB) λαμβάνεται από το CDN της Aspose. Η λήψη είναι διαφανής—δεν απαιτείται επιπλέον κώδικας.

---

## Βήμα 4 – Εκτέλεση της μετατροπής: μετατροπή εικόνας σε κείμενο

Με τη μηχανή έτοιμη και την εικόνα φορτωμένη, η πραγματική λειτουργία OCR είναι μια μόνο κλήση μεθόδου. Το αντικείμενο αποτελέσματος περιέχει το απλό κείμενο, τις βαθμολογίες εμπιστοσύνης και ακόμη συντεταγμένες περιοριστικού πλαισίου αν τα χρειαστείτε.

```csharp
// Run the recognition process
OcrResult ocrResult = ocrEngine.Recognize();

// The Text property holds the plain string
string extractedText = ocrResult.Text;

// Show the output in the console
Console.WriteLine("\n--- Recognized Text ---");
Console.WriteLine(extractedText);
Console.WriteLine("--- End of Output ---\n");
```

**Αναμενόμενο αποτέλεσμα** (υποθέτοντας ότι η δείγμα εικόνα περιέχει τη φράση “नमस्ते दुनिया”):

```
--- Recognized Text ---
नमस्ते दुनिया
--- End of Output ---
```

Αν η εικόνα είναι διαφορετικό JPEG, θα δείτε τους χαρακτήρες που κατάφερε να διαβάσει η μηχανή. Το `OcrResult` εκθέτει επίσης το `Confidence` (0‑100) για κάθε γραμμή αν χρειάζεστε φιλτράρισμα ποιότητας.

---

## Βήμα 5 – Εξαγωγή κειμένου από JPEG και διαχείριση ειδικών περιπτώσεων

Μια λύση έτοιμη για παραγωγή πρέπει να προβλέπει κοινά προβλήματα:

| Κατάσταση | Πώς να το αντιμετωπίσετε |
|-----------|--------------------------|
| **Κατεστραμμένο ή μη υποστηριζόμενο αρχείο** | Τυλίξτε το `Recognize()` σε `try/catch` και καταγράψτε το `OcrException`. |
| **Εικόνα χαμηλής ανάλυσης** | Προεπεξεργαστείτε με `ImageProcessor` για αύξηση DPI (π.χ., `ocrEngine.Image = ImageProcessor.IncreaseResolution(ocrEngine.Image, 300);`). |
| **Πολλαπλές γλώσσες σε μία εικόνα** | Ορίστε `ocrEngine.Language = OcrLanguage.Multilingual;` και προαιρετικά δώστε λίστα προτεραιότητας γλωσσών. |
| **Μεγάλη παρτίδα** | Επαναχρησιμοποιήστε την ίδια παρουσία `OcrEngine`, αντικαθιστώντας μόνο το `ocrEngine.Image` σε κάθε βρόχο. Αποδεσμεύστε τη μηχανή μετά την παρτίδα. |

Εδώ είναι ένας γρήγορος αμυντικός wrapper που μπορείτε να ενσωματώσετε στο έργο σας:

```csharp
static string RecognizePicture(string filePath, OcrLanguage lang = OcrLanguage.Hindi)
{
    try
    {
        using var stream = ImageStream.FromFile(filePath);
        OcrEngine engine = new OcrEngine();
        engine.SetLicense("Aspose.OCR.lic");
        engine.Language = lang;
        engine.Image = stream;

        var result = engine.Recognize();
        return result.Text;
    }
    catch (OcrException ex)
    {
        Console.Error.WriteLine($"OCR failed: {ex.Message}");
        return string.Empty;
    }
}
```

Κλήση του wrapper:

```csharp
string text = RecognizePicture(@"YOUR_DIRECTORY\hindi_sample.jpg");
Console.WriteLine(text);
```

Τώρα έχετε μια **επαναχρησιμοποιήσιμη** μέθοδο που **εξάγει κείμενο από jpeg**, **μετατρέπει εικόνα σε κείμενο**, και αντιμετωπίζει με χάρη τα σφάλματα.

---

## Bonus: Οπτικοποίηση του αποτελέσματος OCR (προαιρετικό)

Αν σας ενδιαφέρει πού τοποθετείται κάθε χαρακτήρας στην εικόνα, μπορείτε να σχεδιάσετε περιοριστικά πλαίσια χρησιμοποιώντας το `System.Drawing`. Αυτό δεν είναι απαραίτητο για βασική εξαγωγή κειμένου, αλλά είναι ένας ωραίος τρόπος να επαληθεύσετε ότι η μηχανή διαβάζει τη σωστή περιοχή.

```csharp
using System.Drawing; // Add System.Drawing.Common NuGet for .NET Core

// After recognition...
Bitmap bmp = new Bitmap(imagePath);
using (Graphics g = Graphics.FromImage(bmp))
{
    Pen pen = new Pen(Color.Red, 2);
    foreach (var line in ocrResult.Lines)
    {
        g.DrawRectangle(pen, line.Bounds);
    }
}

// Save a copy with overlays
bmp.Save("hindi_sample_annotated.png");
Console.WriteLine("Annotated image saved as hindi_sample_annotated.png");
```

Το παραγόμενο PNG θα εμφανίζει κόκκινες ορθογώνιες γύρω από κάθε ανιχνευμένη γραμμή—ιδανικό για εντοπισμό σφαλμάτων σε έγγραφα πολλαπλών γραμμών.

---

## Συμπέρασμα

Τώρα έχετε μια πλήρη, άκρη‑σε‑άκρη συνταγή για **αναγνώριση κειμένου από εικόνα** χρησιμοποιώντας το Aspose OCR σε C#. Καλύψαμε τα πάντα, από τη φόρτωση της εικόνας (ώστε να μπορείτε να **φορτώσετε εικόνα για OCR**) μέχρι την επιλογή του Χίντι ως γλώσσα-στόχο (άρα **αναγνώριση εικόνας με κείμενο στα Χίντι**), την πραγματική εκτέλεση της λειτουργίας **μετατροπή εικόνας σε κείμενο**, και τέλος την **εξαγωγή κειμένου από jpeg** με ανθεκτικό χειρισμό σφαλμάτων.

> **Επόμενα βήματα** – Δοκιμάστε να αντικαταστήσετε το `OcrLanguage.Hindi` με `OcrLanguage.Multilingual` για να διαχειριστείτε έγγραφα με μεικτές γραφές, ή ενσωματώστε τη μέθοδο σε ένα ASP.NET Core API ώστε οι χρήστες να μπορούν να ανεβάζουν εικόνες άμεσα. Μπορείτε επίσης να εξερευνήσετε τα μεταδεδομένα του `OcrResult` για να δημιουργήσετε αναζητήσιμα PDF ή να τροφοδοτήσετε το κείμενο σε υπηρεσία μετάφρασης.

Αν αντιμετωπίσετε οποιεσδήποτε ιδιαιτερότητες, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε τα φόρουμ του Aspose OCR. Καλή προγραμματιστική δουλειά, και εύχομαι οι εικόνες σας να είναι πάντα κρυστάλλινα καθαρές!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}