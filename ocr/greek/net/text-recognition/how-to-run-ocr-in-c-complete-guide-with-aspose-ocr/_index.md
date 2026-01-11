---
category: general
date: 2026-01-10
description: Πώς να εκτελέσετε OCR σε μια εικόνα χρησιμοποιώντας το Aspose OCR σε
  C#. Μάθετε πώς να εξάγετε κείμενο από εικόνα, να εκτελέσετε OCR σε εικόνα και να
  φορτώσετε εικόνα για OCR με επιτάχυνση GPU.
draft: false
keywords:
- how to run OCR
- extract text from image
- run OCR on image
- load image for OCR
- Aspose OCR tutorial
language: el
og_description: Πώς να εκτελέσετε OCR σε μια εικόνα χρησιμοποιώντας το Aspose OCR.
  Αυτό το σεμινάριο δείχνει πώς να εξάγετε κείμενο από εικόνα, να εκτελέσετε OCR στην
  εικόνα και να φορτώσετε την εικόνα για OCR αποδοτικά.
og_title: Πώς να εκτελέσετε OCR σε C# – Πλήρης οδηγός βήμα‑βήμα
tags:
- OCR
- C#
- Aspose
title: Πώς να Εκτελέσετε OCR σε C# – Πλήρης Οδηγός με το Aspose OCR
url: /el/net/text-recognition/how-to-run-ocr-in-c-complete-guide-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε C# – Πλήρης Οδηγός με το Aspose OCR

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε μια φωτογραφία και να εξάγετε το κείμενο χωρίς να τσακίζετε τα μαλλιά σας; Δεν είστε ο μόνος. Είτε ψηφιοποιείτε τιμολόγια, σκανάρετε αποδείξεις, είτε απλώς προσπαθείτε να δημιουργήσετε ένα αναζητήσιμο PDF, η δυνατότητα εξαγωγής κειμένου από εικόνα είναι καθημερινή ανάγκη για πολλούς προγραμματιστές.  

Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό, ολοκληρωμένο παράδειγμα που δείχνει **πώς να εκτελέσετε OCR σε αρχεία εικόνας** χρησιμοποιώντας τη βιβλιοθήκη Aspose OCR, με πλήρη επιτάχυνση GPU για ταχύτητα. Στο τέλος θα γνωρίζετε ακριβώς πώς να φορτώσετε εικόνα για OCR, να ρυθμίσετε τη χρήση μνήμης και να λάβετε καθαρά αποτελέσματα απλού κειμένου — όλα σε λίγα λεπτά κώδικα.

## Τι Θα Μάθετε

- Πώς να αρχικοποιήσετε τη μηχανή Aspose OCR σε C#  
- Πώς να **φορτώσετε εικόνα για OCR** από δίσκο ή ροή  
- Πώς να ενεργοποιήσετε την επιτάχυνση GPU και να περιορίσετε τη μνήμη GPU  
- Πώς να **εξάγετε κείμενο από εικόνα** και να επαληθεύσετε το αποτέλεσμα  
- Συνηθισμένα προβλήματα (έλλειψη μονάδας GPU, περιορισμοί μνήμης) και γρήγορες λύσεις  

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose OCR· αρκεί ένα λειτουργικό περιβάλλον .NET και μια δείγμα εικόνας.

---

## Πώς να Εκτελέσετε OCR σε Εικόνα με το Aspose OCR

Το πρώτο που χρειάζεστε είναι ένα σαφές, εκτελέσιμο απόσπασμα κώδικα που κάνει όλη τη δουλειά. Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε, επικολλήσετε και να τρέξετε αμέσως.

```csharp
// ------------------------------------------------------------
// Complete C# program: How to Run OCR with Aspose OCR
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Config;
using System.Drawing;          // For Image handling (optional)

// 1️⃣ Initialize the OCR engine
var ocrEngine = new OcrEngine();

// 2️⃣ Enable GPU acceleration (requires the Aspose OCR GPU module)
//    This speeds up recognition dramatically on supported hardware.
ocrEngine.Config.EnableGpuAcceleration = true;

// 3️⃣ (Optional) Limit GPU memory usage to 1024 MB to avoid OOM errors
ocrEngine.Config.GpuMemoryLimit = 1024;

// 4️⃣ Load the image you want to process
//    Replace the path with your own image file.
string imagePath = "YOUR_DIRECTORY/sample_skewed.jpg";
ocrEngine.Image = ImageStream.FromFile(imagePath);

// 5️⃣ Run the OCR recognition
ocrEngine.Recognize();

// 6️⃣ Retrieve the plain‑text result and display it
string recognizedText = ocrEngine.Text;
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

**Αναμενόμενο αποτέλεσμα** (υποθέτοντας ότι η δείγμα εικόνας περιέχει τη φράση “Hello World”):

```
=== OCR Result ===
Hello World
```

> **Συμβουλή:** Αν δεν βλέπετε κανένα κείμενο, ελέγξτε ξανά ότι η μονάδα GPU είναι εγκατεστημένη και ότι η διαδρομή της εικόνας είναι σωστή. Η μέθοδος `ImageStream.FromFile` ρίχνει μια σαφή εξαίρεση αν το αρχείο δεν βρεθεί.

---

## Εξαγωγή Κειμένου από Εικόνα Χρησιμοποιώντας Επιτάχυνση GPU

Γιατί να ασχοληθούμε με το GPU; Το OCR μόνο με CPU λειτουργεί, αλλά μπορεί να είναι εξαιρετικά αργό σε μεγάλες ή υψηλής ανάλυσης εικόνες. Η ενεργοποίηση της επιτάχυνσης GPU (βήμα 2 παραπάνω) μεταβιβάζει το βαρέως φορτίου στην κάρτα γραφικών σας, η οποία μπορεί να επεξεργαστεί χιλιάδες εικονοστοιχεία ανά δευτερόλεπτο.

### Πότε να Χρησιμοποιήσετε GPU

- **Επεξεργασία παρτίδας** – σάρωση δεκάδων τιμολογίων σε μία φορά.  
- **Σάρωση υψηλής ανάλυσης** – οτιδήποτε πάνω από 300 dpi.  
- **Εφαρμογές σε πραγματικό χρόνο** – όπως ένας κινητός σαρωτής που χρειάζεται άμεση ανάδραση.

Αν το περιβάλλον σας δεν διαθέτει συμβατό GPU, απλώς ορίστε `EnableGpuAcceleration = false;` και η μηχανή θα επιστρέψει αυτόματα σε λειτουργία CPU.

---

## Εκτέλεση OCR σε Εικόνα – Φόρτωση της Εικόνας Σωστά

Η φόρτωση της εικόνας είναι το βήμα **load image for OCR** που συχνά προκαλεί προβλήματα. Το Aspose OCR αναμένει ένα `ImageStream`, το οποίο μπορεί να δημιουργηθεί από αρχείο, ροή μνήμης ή ακόμη και URL. Εδώ είναι μερικές παραλλαγές:

```csharp
// Load from file (as shown earlier)
ocrEngine.Image = ImageStream.FromFile("path/to/file.jpg");

// Load from a byte array (useful for web uploads)
byte[] imageBytes = File.ReadAllBytes("uploaded_image.png");
ocrEngine.Image = ImageStream.FromBytes(imageBytes);

// Load from a remote URL (requires internet)
ocrEngine.Image = ImageStream.FromUrl("https://example.com/image.tif");
```

**Ακραία περίπτωση:** Κάποιες εικόνες περιέχουν κανάλι άλφα (διαφάνεια) που μπερδεύει τη μηχανή OCR. Η αφαίρεση του άλφα είναι εύκολη:

```csharp
using (var bitmap = new Bitmap(imagePath))
{
    var nonAlpha = new Bitmap(bitmap.Width, bitmap.Height, System.Drawing.Imaging.PixelFormat.Format24bppRgb);
    using (var g = Graphics.FromImage(nonAlpha))
    {
        g.DrawImage(bitmap, 0, 0, bitmap.Width, bitmap.Height);
    }
    ocrEngine.Image = ImageStream.FromBitmap(nonAlpha);
}
```

Τώρα καλύψατε τους πιο συνηθισμένους τρόπους **load image for OCR**, διασφαλίζοντας ότι η μηχανή λαμβάνει πάντα ένα καθαρό, υποστηριζόμενο φορμάτ.

---

## Συμβουλές για Αποτελεσματική Φόρτωση Εικόνας για OCR

1. **Αλλαγή μεγέθους μεγάλων εικόνων** – το OCR δεν χρειάζεται φωτογραφία 4 K· η σμίκρυνση σε πλάτος ~1500 px επιταχύνει τη διαδικασία χωρίς να επηρεάζει την ακρίβεια.  
2. **Μετατροπή σε κλίμακα του γκρι** – μειώνει τον θόρυβο και μπορεί να βελτιώσει την αναγνώριση σε σάρωση χαμηλής αντίθεσης.  
3. **Προεπεξεργασία με ευθυγράμμιση** – αν η εικόνα σας είναι κεκλιμένη, η ενσωματωμένη ευθυγράμμιση του Aspose OCR μπορεί να ενεργοποιηθεί μέσω `ocrEngine.Config.EnableDeskew = true;`.  

Αυτές οι ρυθμίσεις είναι ιδιαίτερα χρήσιμες όταν **εξάγετε κείμενο από εικόνα** μαζικά.

---

## Συνηθισμένα Προβλήματα & Πώς να Τα Διορθώσετε

| Συμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| `System.DllNotFoundException: Aspose.OCR.Gpu.dll` | Η μονάδα GPU δεν είναι εγκατεστημένη | Εγκαταστήστε το πακέτο Aspose OCR GPU ή απενεργοποιήστε το GPU (`EnableGpuAcceleration = false`). |
| Κενό αποτέλεσμα | Λάθος διαδρομή εικόνας ή μη υποστηριζόμενο φορμάτ | Επαληθεύστε τη διαδρομή `ImageStream.FromFile`; δοκιμάστε να φορτώσετε από bytes για να διασφαλίσετε ότι το αρχείο διαβάζεται σωστά. |
| Σφάλμα έλλειψης μνήμης | Το όριο μνήμης GPU είναι πολύ χαμηλό για μεγάλη παρτίδα | Αυξήστε το `GpuMemoryLimit` (π.χ., 2048) ή επεξεργαστείτε τις εικόνες σε μικρότερα τμήματα. |
| Παραμορφωμένοι χαρακτήρες | Η εικόνα έχει πολύ θόρυβο ή χαμηλή αντίθεση | Προεπεξεργασία: δυαδικοποίηση, αποθόρυβο ή αύξηση DPI πριν το OCR. |

---

## Πλήρες Παράδειγμα Λειτουργίας – Συνδυάστε Όλα

Παρακάτω είναι μια συμπαγής εφαρμογή κονσόλας που ενσωματώνει τις καλύτερες πρακτικές που συζητήσαμε: επιτάχυνση GPU, περιορισμός μνήμης, προεπεξεργασία εικόνας και διαχείριση σφαλμάτων.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Config;

class Program
{
    static void Main()
    {
        try
        {
            // Initialize OCR engine
            var ocr = new OcrEngine();

            // Enable GPU (set false if no GPU)
            ocr.Config.EnableGpuAcceleration = true;
            ocr.Config.GpuMemoryLimit = 1024;          // 1 GB limit
            ocr.Config.EnableDeskew = true;            // Auto‑deskew

            // Load and optionally preprocess image
            string path = "YOUR_DIRECTORY/sample_skewed.jpg";
            using (var original = new Bitmap(path))
            {
                // Resize if too large
                const int maxWidth = 1500;
                Bitmap processed = original.Width > maxWidth
                    ? new Bitmap(original, new Size(maxWidth, original.Height * maxWidth / original.Width))
                    : new Bitmap(original);

                // Convert to grayscale (optional but often helpful)
                var gray = new Bitmap(processed.Width, processed.Height, System.Drawing.Imaging.PixelFormat.Format24bppRgb);
                using (var g = Graphics.FromImage(gray))
                {
                    var cm = new System.Drawing.Imaging.ColorMatrix(
                        new float[][]{
                            new float[]{0.3f,0.3f,0.3f,0,0},
                            new float[]{0.59f,0.59f,0.59f,0,0},
                            new float[]{0.11f,0.11f,0.11f,0,0},
                            new float[]{0,0,0,1,0},
                            new float[]{0,0,0,0,1}});
                    var ia = new System.Drawing.Imaging.ImageAttributes();
                    ia.SetColorMatrix(cm);
                    g.DrawImage(processed, new Rectangle(0,0,processed.Width,processed.Height),
                                0,0,processed.Width,processed.Height, GraphicsUnit.Pixel, ia);
                }

                // Feed the processed bitmap into OCR
                ocr.Image = ImageStream.FromBitmap(gray);
            }

            // Run recognition
            ocr.Recognize();

            // Output result
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocr.Text);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR: {ex.Message}");
        }
    }
}
```

Η εκτέλεση αυτού του προγράμματος εκτυπώνει το καθαρό κείμενο που εξήχθη από την εικόνα σας, δείχνοντας έναν αξιόπιστο τρόπο **εξαγωγής κειμένου από εικόνα** ακόμη και όταν η πηγή δεν είναι τέλεια.

---

## Συμπέρασμα

Καλύψαμε **πώς να εκτελέσετε OCR** σε εικόνα χρησιμοποιώντας το Aspose OCR, από την αρχικοποίηση της μηχανής μέχρι τη φόρτωση της εικόνας, την ενεργοποίηση της επιτάχυνσης GPU και τη διαχείριση ακραίων περιπτώσεων. Τώρα έχετε μια ισχυρή, αξιόπιστη αναφορά που μπορείτε να αντιγράψετε‑επικολλήσετε σε οποιοδήποτε έργο .NET και να ξεκινήσετε αμέσως **εξάγοντας κείμενο από εικόνα**.

Επόμενα βήματα; Δοκιμάστε να τροφοδοτήσετε σελίδες PDF, πειραματιστείτε με διαφορετικές γλώσσες (ορίστε `ocrEngine.Config.Language = "spa"` για Ισπανικά), ή ενσωματώστε αυτή τη ροή σε ένα web API που επεξεργάζεται ανεβάσματα σε πραγματικό χρόνο. Ο ουρανός είναι το όριο, και με τα εργαλεία που συζητήσαμε, είστε καλά εξοπλισμένοι για να αντιμετωπίσετε οποιαδήποτε πρόκληση OCR.

Καλή προγραμματιστική, και εύχομαι το κείμενό σας πάντα να είναι καθαρό και το OCR σας γρήγορο!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}