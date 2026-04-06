---
category: general
date: 2026-04-06
description: Μάθετε πώς να εκτελείτε OCR σε αρχεία εικόνας, να εξάγετε κείμενο από
  TIF, να φορτώνετε εικόνα για OCR και να μετατρέπετε το αποτέλεσμα σε EPUB χρησιμοποιώντας
  το Aspose OCR σε C#.
draft: false
keywords:
- perform OCR on image
- convert image to EPUB
- how to generate EPUB
- extract text from TIF
- load image for OCR
language: el
og_description: Κάντε OCR σε εικόνα με C#, εξάγετε κείμενο από TIF, φορτώστε την εικόνα
  για OCR και μετατρέψτε το αποτέλεσμα σε EPUB. Οδηγός βήμα‑προς‑βήμα με πλήρη κώδικα.
og_title: Εκτέλεση OCR σε εικόνα → EPUB – Πλήρης οδηγός C#
tags:
- C#
- Aspose OCR
- EPUB conversion
- Image processing
title: Εκτελέστε OCR σε εικόνα και μετατρέψτε σε EPUB – Πλήρης οδηγός C#
url: /el/net/text-recognition/perform-ocr-on-image-and-convert-to-epub-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε Εικόνα και Μετατροπή σε EPUB – Πλήρης Οδηγός C#

Έχετε χρειαστεί ποτέ να **εκτελέσετε OCR σε εικόνα** αρχεία αλλά δεν ήσασταν σίγουροι πώς να μετατρέψετε το κείμενο σε μορφή αναγνώσιμου e‑book; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν έχουν μια σαρωμένη σελίδα (συχνά .TIF) και θέλουν να τη μετατρέψουν σε καθαρό EPUB χωρίς να αντιγράψουν και να επικολλήσουν χειροκίνητα.  

Σε αυτόν τον οδηγό θα περάσουμε από όλη τη διαδικασία: **φόρτωση εικόνας για OCR**, εξαγωγή του κειμένου και τέλος **μετατροπή εικόνας σε EPUB** χρησιμοποιώντας τη βιβλιοθήκη Aspose OCR. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που μπορεί να πάρει μια σαρωμένη σελίδα και να δημιουργήσει ένα τέλεια δομημένο αρχείο EPUB—χωρίς επιπλέον εργαλεία.

## Τι Θα Μάθετε

- Πώς να **φορτώνετε εικόνα για OCR** σε C# (συμπεριλαμβανομένου του χειρισμού μεγάλων αρχείων TIF).  
- Τα ακριβή βήματα για **εκτέλεση OCR σε εικόνα** με Aspose OCR και γιατί κάθε κλήση είναι σημαντική.  
- Τεχνικές για **εξαγωγή κειμένου από TIF** και καθαρισμό του για έκδοση e‑book.  
- Ο πιο απλός τρόπος για **μετατροπή εικόνας σε EPUB** και ποιες επιλογές έχετε για προσαρμογή.  
- Κοινά προβλήματα—όπως η πίεση μνήμης σε μεγάλες σαρώσεις—και γρήγορες λύσεις.

### Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|-------------|----------------|
| .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.8) | Παρέχει το runtime για τη σύνταξη C# 10 που χρησιμοποιείται παρακάτω. |
| Πακέτο NuGet Aspose.OCR (`Aspose.OCR` και `Aspose.OCR.Export`) | Η μηχανή που αναγνωρίζει χαρακτήρες και γράφει EPUB. |
| Μία εικόνα TIF (`book_page.tif`) που θέλετε να επεξεργαστείτε | Το παράδειγμά μας χρησιμοποιεί μια σάρωση μίας σελίδας, αλλά η ίδια λογική λειτουργεί για πολυ-σελίδες TIFF. |
| Visual Studio 2022 (ή οποιοδήποτε IDE προτιμάτε) | Κάνει το debugging και τη διαχείριση πακέτων απλό. |

Αν τα έχετε ήδη, πάρτε ένα φλιτζάνι καφέ και ας ξεκινήσουμε.

![Διάγραμμα ροής που δείχνει πώς να εκτελέσετε OCR σε εικόνα, να εξαγάγετε κείμενο και να δημιουργήσετε αρχείο EPUB](perform-ocr-on-image-workflow.png "εκτέλεση OCR σε εικόνα workflow")

## Βήμα 1: Φόρτωση Εικόνας για OCR

Πριν η μηχανή μπορέσει να αναγνωρίσει οτιδήποτε, χρειάζεται μια έγκυρη παρουσία `System.Drawing.Image`. Η μέθοδος `Image.FromFile` λειτουργεί για τις περισσότερες μορφές raster, αλλά με TIF μπορεί να αντιμετωπίσετε προβλήματα πολλαπλών πλαισίων. Η περιτύλιξη της κλήσης σε ένα μπλοκ `using` εγγυάται ότι το χειριστήριο του αρχείου απελευθερώνεται άμεσα—σημαντικό όταν επεξεργάζεστε δεκάδες σελίδες σε παρτίδα.

```csharp
using System.Drawing;

// Path to your source scan – change this to your actual file location
string sourcePath = @"C:\Scans\book_page.tif";

// Load the image safely
using (Image sourceImage = Image.FromFile(sourcePath))
{
    // The image is now ready for OCR
    // (We’ll hand it off to the engine in the next step)
}
```

**Γιατί είναι σημαντικό:**  
- **Ασφάλεια μνήμης:** το `using` εξασφαλίζει ότι οι πόροι GDI+ απελευθερώνονται, αποτρέποντας διαρροές που μπορούν να καταρρεύσουν υπηρεσίες μεγάλης διάρκειας.  
- **Ευελιξία μορφής:** το `Image.FromFile` ανιχνεύει αυτόματα TIFF, PNG, JPEG κ.λπ., έτσι δεν χρειάζεστε ξεχωριστούς φορτωτές για κάθε τύπο αρχείου.

> **Συμβουλή:** Αν αντιμετωπίσετε σφάλματα “parameter is not valid” σε ορισμένα TIFF, σκεφτείτε να χρησιμοποιήσετε `Image.FromStream` με ένα `FileStream` ανοιγμένο σε λειτουργία μόνο για ανάγνωση. Παρακάμπτει κάποιες ιδιαιτερότητες του GDI+.

## Βήμα 2: Εκτέλεση OCR σε Εικόνα

Τώρα που η εικόνα είναι στη μνήμη, δημιουργούμε την μηχανή Aspose OCR. Η κλάση `OcrEngine` είναι ελαφριά· μπορείτε να επαναχρησιμοποιήσετε ένα μόνο αντικείμενο για πολλές σελίδες, μειώνοντας το φορτίο.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

// Create the OCR engine – you can pass a license object here if you have one
OcrEngine ocrEngine = new OcrEngine();

// Inside the using block from Step 1
using (Image sourceImage = Image.FromFile(sourcePath))
{
    // Run the recognition process
    OcrResult ocrResult = ocrEngine.Recognize(sourceImage);

    // The Result property holds the extracted plain text
    string extractedText = ocrResult.Text;

    // Optional: Write the raw text to console for quick verification
    Console.WriteLine("=== Extracted Text ===");
    Console.WriteLine(extractedText);
}
```

**Γιατί είναι σημαντικό:**  
- Το `Recognize` κάνει όλη τη βαριά δουλειά (δυαδικοποίηση, ανάλυση διάταξης, ταξινόμηση χαρακτήρων).  
- Το επιστρεφόμενο `OcrResult` σας παρέχει τόσο το απλό κείμενο όσο και, αν χρειαστεί, τις συντεταγμένες κάθε λέξης—χρήσιμο για μεταγενέστερη επεξεργασία.  

### Περιπτώσεις Άκρων & Ρυθμίσεις

| Κατάσταση | Προτεινόμενη ρύθμιση |
|-----------|-----------------|
| Σαρώσεις χαμηλής αντίθεσης | Ορίστε `ocrEngine.Settings.ImagePreprocessing` σε `ImagePreprocessingMode.Auto` για καλύτερη δυαδικοποίηση. |
| Έγγραφα πολλαπλών γλωσσών | Χρησιμοποιήστε `ocrEngine.Settings.Language = Language.English | Language.French;` για ενεργοποίηση ανάμειξης γλωσσών. |
| Τεράστιο TIFF ( > 200 MB ) | Επεξεργαστείτε σελίδα-προς-σελίδα χρησιμοποιώντας `Image.GetFrameCount` και `SelectActiveFrame` για χαμηλή χρήση μνήμης. |

## Βήμα 3: Μετατροπή Εικόνας σε EPUB

Με το ακατέργαστο κείμενο στα χέρια, το επόμενο βήμα είναι να το συσκευάσετε σε ένα EPUB. Η Aspose OCR παρέχει ένα βολικό βοηθό `EpupExport` (ναι, η βιβλιοθήκη το γράφει “Epup”, αλλά το αποτέλεσμα είναι ένα τυπικό `.epub`). Μπορείτε να του δώσετε το `OcrResult` απευθείας· η βιβλιοθήκη θα δημιουργήσει ένα EPUB μονο-κεφαλαίου που περιέχει το αναγνωρισμένο κείμενο.

```csharp
// Destination path for the EPUB file
string epubPath = @"C:\Outputs\book_page.epub";

// Inside the same using block after OCR
using (Image sourceImage = Image.FromFile(sourcePath))
{
    OcrResult ocrResult = ocrEngine.Recognize(sourceImage);

    // Export to EPUB – this writes the file to disk
    EpupExport.ToEpup(ocrResult, epubPath);

    Console.WriteLine($"EPUB created at: {epubPath}");
}
```

**Γιατί είναι σημαντικό:**  
- Ο βοηθός αναλαμβάνει τη συσκευασία του EPUB (manifest, spine, metadata) ώστε να μην χρειάζεται να δημιουργήσετε χειροκίνητα τη δομή XML.  
- Σεβεται τη αρχική σειρά ανάγνωσης που εντόπισε η μηχανή OCR, πράγμα που σημαίνει ότι οι τίτλοι και οι παράγραφοι παραμένουν στη σωστή ακολουθία.

### Προσαρμογή του EPUB

Αν χρειάζεστε εικόνα εξώφυλλου, προσαρμοσμένα μεταδεδομένα ή πολλαπλά κεφάλαια, μπορείτε να δημιουργήσετε ένα `EpubDocument` χειροκίνητα:

```csharp
using Aspose.OCR.Export.Epub;

// Create a new EPUB document
EpubDocument epubDoc = new EpubDocument();

// Add a title metadata entry
epubDoc.Metadata.Title = "Scanned Book – Chapter 1";

// Optionally add a cover (must be a JPEG or PNG)
epubDoc.CoverImage = Image.FromFile(@"C:\Assets\cover.jpg");

// Insert the OCR text as a chapter
epubDoc.AddChapter("Chapter 1", ocrResult.Text);

// Save the custom EPUB
epubDoc.Save(epubPath);
```

> **Σημείωση:** Η απλή κλήση `EpupExport.ToEpup` είναι ιδανική για γρήγορα σενάρια, ενώ η χειροκίνητη προσέγγιση ξεχωρίζει όταν χρειάζεστε πλήρη έλεγχο.

## Βήμα 4: Επαλήθευση του Αποτελέσματος

Μια γρήγορη έλεγχος λογικής εξοικονομεί ώρες debugging αργότερα. Ανοίξτε το παραγόμενο `.epub` σε οποιονδήποτε αναγνώστη (Calibre, Adobe Digital Editions ή ακόμη και σε web browser) και ψάξτε για:

1. Σωστή ροή κειμένου—χωρίς ελλιπείς λέξεις.  
2. Κατάλληλος τίτλος κεφαλαίου (αν έχετε ορίσει μεταδεδομένα).  
3. Προαιρετική εμφάνιση εικόνας εξώφυλλου.

Αν εντοπίσετε παραμορφωμένους χαρακτήρες, επανεξετάστε το **Βήμα 2** και πειραματιστείτε με τις `Settings` της μηχανής (π.χ., ενεργοποιήστε την ανίχνευση `Language` ή προσαρμόστε το `Resolution`).  

```csharp
// Quick verification snippet
if (File.Exists(epubPath))
{
    Console.WriteLine("✅ EPUB file exists and is ready for reading.");
}
else
{
    Console.WriteLine("❌ Something went wrong – the EPUB wasn't created.");
}
```

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα που ενώνει όλα τα παραπάνω. Επικολλήστε το σε ένα νέο console project, επαναφέρετε τα πακέτα NuGet Aspose OCR και πατήστε **F5**.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Export;
using Aspose.OCR.Export.Epub;   // Only needed for custom EPUB handling

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // Configuration – adjust these paths for your environment
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Scans\book_page.tif";
        string epubPath   = @"C:\Outputs\book_page.epub";

        // -----------------------------------------------------------------
        // Step 1: Load image for OCR (handles TIFF, JPEG, PNG, etc.)
        // -----------------------------------------------------------------
        using (Image sourceImage = Image.FromFile(sourcePath))
        {
            // -----------------------------------------------------------------
            // Step 2: Perform OCR on image
            // -----------------------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // Optional: tweak settings for low‑quality scans
            // ocrEngine.Settings.ImagePreprocessing = ImagePreprocessingMode.Auto;
            // ocrEngine.Settings.Language = Language.English;

            OcrResult ocrResult = ocrEngine.Recognize(sourceImage);

            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);

            // -----------------------------------------------------------------
            // Step 3: Convert image to EPUB (simple one‑chapter book)
            // -----------------------------------------------------------------
            EpupExport.ToEpup(ocrResult, epubPath);

            // For a richer EPUB, uncomment the block below:
            /*
            EpubDocument epubDoc = new EpubDocument();
            epubDoc.Metadata.Title = "Scanned Book – Chapter 1";
            epubDoc.AddChapter("Chapter 1", ocrResult.Text);
            // epubDoc.CoverImage = Image.FromFile(@"C:\Assets\cover.jpg");
            epubDoc.Save(epubPath);
            */

            // -----------------------------------------------------------------
            // Step 4: Verify output
            // -----------------------------------------------------------------
            if (System.IO.File.Exists(epubPath))
                Console.WriteLine($"✅ EPUB created successfully at: {epubPath}");
            else
                Console.WriteLine("❌ EPUB creation failed.");
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Η εκτέλεση του προγράμματος εκτυπώνει το αναγνωρισμένο κείμενο στην κονσόλα και δημιουργεί το `book_page.epub`. Ανοίγοντας το EPUB εμφανίζεται ένα ενιαίο κεφάλαιο που περιέχει το ακριβές κείμενο που είδατε στην έξοδο της κονσόλας. Δεν απαιτείται χειροκίνητη αντιγραφή‑επικόλληση.

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για **εκτέλεση OCR σε εικόνα** αρχεία, **εξαγωγή κειμένου από TIF**, και **μετατροπή εικόνας σε EPUB** χρησιμοποιώντας Aspose OCR σε C#. Η ροή εργασίας είναι απλή:

1. **Φορτώστε εικόνα για OCR** με ασφαλή μπλοκ `using`.  
2. **Εκτελέστε OCR σε εικόνα** μέσω `OcrEngine.Recognize`.  
3. **Μετατρέψτε το αποτέλεσμα σε EPUB** χρησιμοποιώντας `EpupExport.ToEpup` (ή ένα προσαρμοσμένο `EpubDocument`).  
4. **Επαληθεύστε** το αποτέλεσμα και προσαρμόστε τις ρυθμίσεις αν χρειάζεται.

Από εδώ μπορείτε να κλιμακώσετε τη λύση για μαζική επεξεργασία ολόκληρων βιβλίων, να προσθέσετε εξώφυλλο, να ενσωματώσετε γραμματοσειρές ή ακόμη και να το ενσωματώσετε σε web API. Τα δομικά στοιχεία είναι όλα στη θέση τους, και τώρα έχετε μια αξιόπιστη, αναφορά κατάλληλη για παραπομπές που μπορείτε να δείξετε σε βοηθούς AI.

**Τι θα ακολουθήσει;** Δοκιμάστε να προσθέσετε έναν βρόχο που διασχίζει έναν φάκελο με TIFF, συγκεντρώνει τα αποτελέσματα OCR σε πολλαπλά κεφάλαια EPUB, ή πειραματιστείτε

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}