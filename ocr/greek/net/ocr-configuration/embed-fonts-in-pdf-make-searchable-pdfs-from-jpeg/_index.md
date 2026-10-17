---
category: general
date: 2026-03-05
description: Ενσωμάτωση γραμματοσειρών σε PDF κατά τη μετατροπή JPEG σε PDF με δυνατότητα
  αναζήτησης χρησιμοποιώντας το Aspose OCR. Μάθετε πώς να αναγνωρίζετε κείμενο από
  JPEG και να ενσωματώνετε γραμματοσειρές για συμμόρφωση με PDF/A‑2b.
draft: false
keywords:
- embed fonts in pdf
- recognize text from jpeg
- how to create searchable pdf
- convert image to searchable pdf
- perform ocr on image
language: el
og_description: Ενσωματώστε γραμματοσειρές σε PDF ενώ μετατρέπετε ένα JPEG σε PDF
  με δυνατότητα αναζήτησης. Αυτός ο οδηγός βήμα‑βήμα δείχνει πώς να αναγνωρίζετε κείμενο
  από JPEG και να δημιουργείτε αρχεία συμβατά με PDF/A‑2b.
og_title: Ενσωμάτωση γραμματοσειρών σε PDF – Δημιουργία αναζητήσιμων PDF από JPEG
tags:
- Aspose OCR
- PDF generation
- C#
- .NET
title: Ενσωμάτωση γραμματοσειρών σε PDF – Δημιουργία αναζητήσιμων PDF από JPEG
url: /el/net/ocr-configuration/embed-fonts-in-pdf-make-searchable-pdfs-from-jpeg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ενσωμάτωση γραμματοσειρών σε PDF – Δημιουργία αναζητήσιμων PDF από JPEG

Έχετε χρειαστεί ποτέ να **ενσωματώσετε γραμματοσειρές σε PDF** αρχεία που δημιουργήθηκαν από σαρωμένες εικόνες; Δεν είστε μόνοι. Οι περισσότεροι προγραμματιστές αντιμετωπίζουν το πρόβλημα όπου το παραγόμενο PDF φαίνεται εντάξει στον υπολογιστή τους, αλλά εμφανίζει ελλιπές κείμενο όταν ανοίγεται αλλού επειδή οι γραμματοσειρές δεν ενσωματώθηκαν.  

Τα καλά νέα; Με το Aspose OCR μπορείτε να **αναγνωρίσετε κείμενο από JPEG**, να ενσωματώσετε τις απαραίτητες γραμματοσειρές και να δημιουργήσετε ένα πλήρως αναζητήσιμο έγγραφο PDF/A‑2b με λίγες μόνο γραμμές C#. Σε αυτό το tutorial θα περάσουμε από κάθε βήμα — γιατί κάθε ρύθμιση είναι σημαντική, πώς να αποφύγετε κοινά προβλήματα και πώς θα πρέπει να φαίνεται το τελικό PDF.

Στο τέλος αυτού του οδηγού θα μπορείτε να **μετατρέψετε εικόνα σε αναζητήσιμο PDF**, να ενσωματώσετε σωστά τις γραμματοσειρές και να καταλάβετε πώς να **εκτελέσετε OCR σε αρχεία εικόνας** προγραμματιστικά.

## Τι Θα Χρειαστεί

- **Aspose.OCR for .NET** (τελευταία έκδοση, π.χ., 23.10) – η βιβλιοθήκη που κάνει τη βαριά δουλειά.
- Ένα έγκυρο **αρχείο άδειας Aspose OCR** (`Aspose.OCR.lic`). Η δωρεάν δοκιμή λειτουργεί, αλλά μια άδεια έκδοση αφαιρεί τα υδατογραφήματα αξιολόγησης.
- Μια εικόνα JPEG (`input.jpg`) που περιέχει τυπωμένο ή πληκτρολογημένο κείμενο.
- Ένα περιβάλλον ανάπτυξης .NET (Visual Studio, Rider ή VS Code με την επέκταση C#).

Δεν απαιτούνται επιπλέον πακέτα NuGet· η μηχανή OCR περιλαμβάνει ήδη τα εργαλεία δημιουργίας PDF.

## Βήμα 1: Ρύθμιση της Μηχανής OCR και Εφαρμογή της Άδειας *(Ενσωμάτωση γραμματοσειρών σε PDF)*

Πριν μπορέσετε να εκτελέσετε οποιαδήποτε αναγνώριση, πρέπει να δημιουργήσετε μια παρουσία `OcrEngine` και να της υποδείξετε ποια άδεια θα χρησιμοποιήσει. Η παράλειψη του βήματος άδειας θα κάνει τη μηχανή να λειτουργεί σε λειτουργία αξιολόγησης, η οποία προσθέτει ένα λογότυπο “Powered by Aspose” σε κάθε σελίδα.

```csharp
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;
using Aspose.OCR.Saving;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Apply your license – replace the path with the actual location of your .lic file
ocrEngine.SetLicense("Aspose.OCR.lic");
```

**Γιατί είναι σημαντικό:** Η άδεια δεν αφαιρεί μόνο τα υδατογραφήματα, αλλά επίσης ξεκλειδώνει τις επιλογές συμμόρφωσης PDF/A που θα χρειαστούμε αργότερα για την ενσωμάτωση γραμματοσειρών.

## Βήμα 2: Φόρτωση της Εικόνας JPEG που Θέλετε να Επεξεργαστείτε *(Αναγνώριση Κειμένου από JPEG)*

Η μηχανή OCR λειτουργεί με μια ιδιότητα `Image` που δέχεται ένα `ImageStream`. Κατευθύνετέ την προς το JPEG που θέλετε να μετατρέψετε.

```csharp
// Load the source JPEG image
ocrEngine.Image = ImageStream.FromFile(@"C:\MyImages\input.jpg");
```

**Συμβουλή:** Αν η εικόνα σας βρίσκεται σε ροή (π.χ., ανεβάστηκε μέσω API), μπορείτε να χρησιμοποιήσετε `ImageStream.FromStream(yourStream)` αντί για `FromFile`.

## Βήμα 3: Διαμόρφωση Επιλογών Αποθήκευσης PDF για Αναζητήσιμο PDF

Αυτή είναι η καρδιά της απαίτησης “ενσωμάτωση γραμματοσειρών σε PDF”. Θα χρησιμοποιήσουμε το `PdfSaveOptions` για να:

1. Στοχεύσουμε στο **PDF/A‑2b** (ένα ευρέως αποδεκτό πρότυπο αρχειοθέτησης).
2. **Ενσωματώσουμε όλες τις χρησιμοποιημένες γραμματοσειρές** ώστε το PDF να εμφανίζεται το ίδιο παντού.
3. Εφαρμόσουμε **συμπίεση Flate χωρίς απώλειες** για να διατηρήσουμε λογικό μέγεθος αρχείου.
4. Διατηρήσουμε το αρχικό JPEG ως στρώμα φόντου, το οποίο διατηρεί την οπτική πιστότητα.

```csharp
// Set up PDF export options
var pdfSaveOptions = new PdfSaveOptions
{
    // Produce a PDF/A‑2b compliant document
    PdfAStandard = PdfAStandard.PdfA2b,

    // Ensure every font used by the OCR text is embedded
    EmbedFonts = true,

    // Use lossless compression for the text and graphics streams
    Compression = PdfCompression.Flate,

    // Keep the original image behind the OCR layer (makes the PDF searchable)
    RenderOriginalImage = true
};
```

**Γιατί αυτές οι ρυθμίσεις;**  
- **PdfAStandard.PdfA2b** εγγυάται μακροπρόθεσμη διατήρηση και επιβάλλει την ενσωμάτωση των γραμματοσειρών.  
- **EmbedFonts = true** είναι η ρητή σημαία που ικανοποιεί τον κύριο στόχο της λέξης-κλειδί.  
- **Compression.Flate** μειώνει το μέγεθος χωρίς να θυσιάζει την ποιότητα.  
- **RenderOriginalImage** διατηρεί την οπτική εμφάνιση της σαρωμένης σελίδας ενώ το κρυφό στρώμα OCR παρέχει αναζητήσιμο κείμενο.

## Βήμα 4: Εκτέλεση Αναγνώρισης OCR στην Εικόνα *(Εκτέλεση OCR σε Εικόνα)*

Με όλα έτοιμα, ενεργοποιήστε την αναγνώριση. Η μηχανή θα αναλύσει το JPEG, θα εξάγει χαρακτήρες και εσωτερικά θα δημιουργήσει ένα στρώμα κειμένου.

```csharp
// Execute OCR – this populates the internal text layer
ocrEngine.Recognize();
```

**Συχνή ερώτηση:** *Πρέπει να καθορίσω γλώσσα ή λεξικό;*  
Αν το έγγραφό σας δεν είναι στα Αγγλικά, ορίστε `ocrEngine.Language = OcrLanguage.French;` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) πριν καλέσετε το `Recognize()`. Η προεπιλογή είναι τα Αγγλικά.

## Βήμα 5: Αποθήκευση του Αποτελέσματος ως Αναζητήσιμο PDF με Ενσωματωμένες Γραμματοσειρές

Τέλος, γράψτε το αποτέλεσμα στο δίσκο. Η μέθοδος `Save` δέχεται τη διαδρομή προορισμού και τις `PdfSaveOptions` που ορίσαμε νωρίτερα.

```csharp
// Save the searchable PDF with embedded fonts
ocrEngine.Save(@"C:\MyImages\output.pdf", pdfSaveOptions);
```

Όταν ανοίξετε το `output.pdf` στο Adobe Acrobat ή σε οποιονδήποτε προβολέα PDF, θα πρέπει να μπορείτε να:

- **Αναζητήσετε** οποιαδήποτε λέξη εμφανίστηκε στο αρχικό JPEG.
- Δείτε **χωρίς προειδοποιήσεις ελλιπών γραμματοσειρών** (thanks to `EmbedFonts = true`).
- Επαληθεύσετε ότι το αρχείο συμμορφώνεται με **PDF/A‑2b** (Αρχείο → Ιδιότητες → PDF/A).

## Πλήρες Παράδειγμα Λειτουργίας

Ακολουθεί το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αντιγράψτε‑και‑επικολλήστε το σε ένα νέο έργο Console App, προσαρμόστε τις διαδρομές αρχείων και πατήστε **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;
using Aspose.OCR.Saving;

namespace ImageToSearchablePdf
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine and apply license
            var ocrEngine = new OcrEngine();
            ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

            // 2️⃣ Load JPEG image
            ocrEngine.Image = ImageStream.FromFile(@"C:\MyImages\input.jpg");

            // 3️⃣ Configure PDF save options (embed fonts, PDF/A‑2b, etc.)
            var pdfSaveOptions = new PdfSaveOptions
            {
                PdfAStandard = PdfAStandard.PdfA2b,
                EmbedFonts = true,
                Compression = PdfCompression.Flate,
                RenderOriginalImage = true
            };

            // 4️⃣ Run OCR recognition
            ocrEngine.Recognize();

            // 5️⃣ Save searchable PDF with embedded fonts
            string outputPath = @"C:\MyImages\output.pdf";
            ocrEngine.Save(outputPath, pdfSaveOptions);

            Console.WriteLine($"✅ PDF created at: {outputPath}");
            Console.WriteLine("Open it in any PDF viewer and try searching for words from the original JPEG.");
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:**  
Η κονσόλα εκτυπώνει ένα μήνυμα επιτυχίας και το `output.pdf` εμφανίζεται στον φάκελο προορισμού. Ανοίγοντας το PDF και χρησιμοποιώντας το πεδίο αναζήτησης του προβολέα θα πρέπει να εντοπίζει οποιαδήποτε λέξη υπήρχε στο `input.jpg`.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### 1. “Τι γίνεται αν το JPEG μου είναι multi‑page TIFF;”

Το Aspose OCR αντιμετωπίζει κάθε σελίδα ξεχωριστά. Μετατρέψτε το TIFF σε σειρά JPEG (ή χρησιμοποιήστε `ImageStream.FromFile` σε κάθε σελίδα) και επαναλάβετε τη διαδικασία OCR, προσθέτοντας κάθε αποτέλεσμα στο ίδιο PDF χρησιμοποιώντας ξανά την ίδια παρουσία `OcrEngine`.

### 2. “Μπορώ να ελέγξω το DPI ή την προεπεξεργασία της εικόνας;”

Ναι. Πριν καλέσετε το `Recognize()`, μπορείτε να προσαρμόσετε την ανάλυση της εικόνας:

```csharp
ocrEngine.Image.DpiX = 300;
ocrEngine.Image.DpiY = 300;
ocrEngine.Image.AutoRotate = true; // auto‑rotate for landscape scans
```

Υψηλότερο DPI συχνά προσφέρει καλύτερη ακρίβεια αναγνώρισης, ειδικά για μικρές γραμματοσειρές.

### 3. “Το PDF μου εξακολουθεί να εμφανίζει ελλιπείς γραμματοσειρές στο Adobe Reader—τι συμβαίνει;”

Βεβαιωθείτε ότι στοχεύετε στο **PDF/A‑2b** και ότι το `EmbedFonts` είναι ορισμένο σε `true`. Αν αλλάξατε χειροκίνητα το `PdfAStandard` σε `None`, το βήμα επικύρωσης PDF/A παραλείπεται και ορισμένες γραμματοσειρές μπορεί να παραμείνουν μη ενσωματωμένες.

### 4. “Είναι το στρώμα OCR αναζητήσιμο σε κινητές συσκευές;”

Απολύτως. Το κρυφό στρώμα κειμένου είναι μέρος του προτύπου PDF, έτσι οποιοσδήποτε προβολέας PDF που υποστηρίζει εξαγωγή κειμένου (συμπεριλαμβανομένων των iOS Files, Android PDF Viewer κ.λπ.) θα επιτρέπει την αναζήτηση.

### 5. “Πώς να διαχειριστώ γλώσσες από δεξιά προς αριστερά όπως η Αραβική;”

Ορίστε τη γλώσσα πριν από την αναγνώριση:

```csharp
ocrEngine.Language = OcrLanguage.Arabic;
ocrEngine.Recognize();
```

Το Aspose OCR αλλάζει αυτόματα την κατεύθυνση του κειμένου και ενσωματώνει τις κατάλληλες γραμματοσειρές όταν το `EmbedFonts` είναι true.

## Επαγγελματικές Συμβουλές & Συχνά Παγίδες

- **Συμβουλή pro:** Αν οι πηγαίες εικόνες σας είναι έγχρωμες φωτογραφίες, σκεφτείτε να τις μετατρέψετε πρώτα σε γκρι κλίμακα (`ocrEngine.Image.ConvertToGrayscale();`). Αυτό μειώνει το μέγεθος του αρχείου χωρίς να επηρεάζει την ακρίβεια του OCR.
- **Προσοχή:** Η χρήση της δωρεάν άδειας δοκιμής με μια **μεγάλη** εικόνα μπορεί να κάνει τη μηχανή να κόβει το κείμενο OCR. Αναβαθμίστε σε πλήρη άδεια για παραγωγικά φορτία εργασίας.
- **Συμβουλή απόδοσης:** Η επαναχρησιμοποίηση της ίδιας παρουσία `OcrEngine` σε πολλές εικόνες αποφεύγει το κόστος φόρτωσης των DLL του OCR επανειλημμένα.
- **Σημείωση ασφαλείας:** Τα αρχεία PDF/A‑2b είναι **μόνο‑ανάγνωση** από τη φύση τους, κάτι που βοηθά στην αποφυγή τυχαίας ένεσης σεναρίων — ένα ωραίο πλεονέκτημα για περιβάλλοντα με αυστηρή συμμόρφωση.

## Συμπέρασμα

Συζητήσαμε ολόκληρη τη διαδικασία για **ενσωμάτωση γραμματοσειρών σε PDF** ενώ **αναγνωρίζετε κείμενο από JPEG** και παράγετε ένα **αναζητήσιμο PDF** που πληροί τα πρότυπα PDF/A‑2b. Η διαδικασία συνοψίζεται σε:

1. Αρχικοποιήστε το `OcrEngine` και εφαρμόστε την άδειά σας.  
2. Φορτώστε την εικόνα JPEG.  
3. Διαμορφώστε τις `PdfSaveOptions` (ενσωμάτωση γραμματοσειρών, PDF/A‑2b, συμπίεση).  
4. Εκτελέστε το `Recognize()`.  
5. Αποθηκεύστε με τις ρυθμισμένες επιλογές.

Τώρα μπορείτε να ενσωματώσετε αυτή τη ροή σε web services, desktop utilities ή batch jobs που χρειάζονται **μετατροπή εικόνας σε αναζητήσιμο PDF** σε πραγματικό χρόνο. Στη συνέχεια, μπορείτε να εξερευνήσετε **πώς να δημιουργήσετε αναζητήσιμο PDF** από πολυσελιδικά PDF ή PDF που δημιουργούνται

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}