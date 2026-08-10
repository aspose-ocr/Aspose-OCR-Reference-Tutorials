---
category: general
date: 2026-02-24
description: c# OCR tutorial που δείχνει πώς να εξάγετε κείμενο από εικόνα χρησιμοποιώντας
  το Aspose OCR – ένας πλήρης, βήμα‑βήμα οδηγός για προγραμματιστές .NET.
draft: false
keywords:
- c# ocr tutorial
- how to extract text from image
- Aspose OCR C#
- OCR region of interest
- image text extraction C#
language: el
og_description: c# OCR tutorial που δείχνει πώς να εξάγετε κείμενο από εικόνα χρησιμοποιώντας
  το Aspose OCR – ένας πλήρης, βήμα‑βήμα οδηγός για προγραμματιστές .NET.
og_title: 'c# OCR tutorial: Εξαγωγή κειμένου από εικόνες με Aspose OCR'
tags:
- C#
- OCR
- Aspose
- Image Processing
title: 'c# OCR tutorial: Εξαγωγή κειμένου από εικόνες με το Aspose OCR'
url: /el/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Εξαγωγή Κειμένου από Εικόνες Χρησιμοποιώντας το Aspose OCR

Αναρωτηθήκατε ποτέ πώς να εξάγετε κείμενο από αρχεία εικόνας σε μια εφαρμογή C#; Δεν είστε ο μόνος. Σε πολλά πραγματικά έργα—σκεφτείτε σαρωτές διαβατηρίων, επεξεργαστές τιμολογίων ή ακόμη και απλούς αναγνώστες αποδείξεων—η λήψη αξιόπιστων αποτελεσμάτων OCR αποτελεί καθημερινό εμπόδιο.  

Αυτό το **c# ocr tutorial** σας καθοδηγεί μέσα από μια πρακτική λύση με το Aspose OCR, δείχνοντας ακριβώς **πώς να εξάγετε κείμενο από εικόνα** αρχεία, να περιορίσετε τη σάρωση σε μια περιοχή ενδιαφέροντος και να εμφανίσετε το αποτέλεσμα—όλα σε λίγες γραμμές κώδικα.  

Θα καλύψουμε όλα όσα χρειάζεστε: το πακέτο NuGet, τις απαιτούμενες δηλώσεις `using`, τη ρύθμιση ROI, τη διαμόρφωση επιλογών και έναν γρήγορο έλεγχο ορθότητας του αποτελέσματος. Στο τέλος, θα έχετε μια εκτελέσιμη εφαρμογή console που εξάγει το όνομα από μια σάρωση διαβατηρίου (ή οποιαδήποτε άλλη εικόνα που θα επιλέξετε). Χωρίς περιττές πληροφορίες, μόνο μια σαφής, πλήρης απάντηση που μπορείτε να αντιγράψετε‑επικολλήσετε και να εκτελέσετε.

## Προαπαιτούμενα

- .NET 6+ SDK (ή .NET Framework 4.7+ αν προτιμάτε το παλαιότερο runtime)
- Visual Studio 2022 ή οποιονδήποτε επεξεργαστή που υποστηρίζει C#
- Πρόσβαση στο Internet για λήψη του πακέτου NuGet **Aspose.OCR**
- Ένα αρχείο εικόνας (π.χ., `passport_scan.png`) που περιέχει αναγνώσιμο κείμενο

> **Pro tip:** Αν πειραματίζεστε τοπικά, τοποθετήστε ένα μικρό PNG ή JPEG σε έναν φάκελο που ονομάζεται `Images` μέσα στο έργο σας – διατηρεί το μονοπάτι σύντομο και τον κώδικα τακτοποιημένο.

## Βήμα 1: Εγκατάσταση Aspose OCR και Προσθήκη Namespaces

Πρώτα απ' όλα, χρειαζόμαστε τη βιβλιοθήκη OCR. Ανοίξτε το τερματικό σας (ή το Package Manager Console) και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Μόλις εγκατασταθεί το πακέτο, προσθέστε τις απαιτούμενες δηλώσεις `using` στην αρχή του αρχείου `Program.cs`:

```csharp
using Aspose.OCR;          // Core OCR engine
using System.Drawing;     // Rectangle struct for ROI
```

Αυτές οι δύο γραμμές σας δίνουν πρόσβαση στο `OcrEngine`, `OcrOptions` και τον τύπο `Rectangle` που θα χρησιμοποιήσουμε για να περιορίσουμε την περιοχή σάρωσης.

## Βήμα 2: Δημιουργία Παραδείγματος OCR Engine

Η μηχανή είναι η καρδιά της διαδικασίας. Σκεφτείτε την ως το «εγκέφαλο» που διαβάζει εικονοστοιχεία και τα μετατρέπει σε χαρακτήρες. Η αρχικοποίησή της είναι απλή:

```csharp
// Step 2: Instantiate the OCR engine – this object does the heavy lifting.
OcrEngine ocrEngine = new OcrEngine();
```

> **Γιατί αυτό είναι σημαντικό:** Ένα μόνο `OcrEngine` μπορεί να επαναχρησιμοποιηθεί για πολλαπλές εικόνες, κάτι που εξοικονομεί μνήμη και αποτρέπει επαναλαμβανόμενους ελέγχους άδειας.

## Βήμα 3: Ορισμός Περιοχής Ενδιαφέροντος (ROI)

Η σάρωση ολόκληρης μιας υψηλής ανάλυσης εικόνας μπορεί να είναι σπατάλη, ειδικά όταν γνωρίζετε ακριβώς πού βρίσκεται το κείμενο (π.χ., το πεδίο ονόματος σε ένα διαβατήριο). Καθορίζοντας μια **περιοχή ενδιαφέροντος**, λέτε στη μηχανή να αγνοήσει ό,τι βρίσκεται εκτός του ορθογωνίου.

```csharp
// Step 3: Set the ROI – adjust X, Y, Width, Height to match your image layout.
Rectangle regionOfInterest = new Rectangle(150, 300, 800, 200);
```

- **X** και **Y** αντιπροσωπεύουν την επάνω‑αριστερή γωνία του ορθογωνίου.
- **Width** και **Height** ορίζουν το μέγεθος του κουτιού.

Αν δεν είστε σίγουροι για τους ακριβείς αριθμούς, ένας γρήγορος οπτικός έλεγχος με οποιονδήποτε επεξεργαστή εικόνας (όπως το Paint.NET) θα σας βοηθήσει να εντοπίσετε τις συντεταγμένες.

## Βήμα 4: Διαμόρφωση OCR Options και Σύνδεση του ROI

Τώρα συνδέουμε το ROI με ένα αντικείμενο `OcrOptions`. Αυτό το αντικείμενο σας επιτρέπει επίσης να ρυθμίσετε τη γλώσσα, την ταχύτητα ανίχνευσης και άλλα, αλλά για αυτό το tutorial θα το κρατήσουμε στο ελάχιστο.

```csharp
// Step 4: Prepare OCR options and assign the ROI we just defined.
OcrOptions ocrOptions = new OcrOptions { Roi = regionOfInterest };
```

> **Ακραία περίπτωση:** Αν παραλείψετε το ROI, το Aspose OCR θα σαρώσει ολόκληρη την εικόνα, κάτι που μπορεί να αυξήσει τον χρόνο επεξεργασίας και να παράγει επιπλέον θόρυβο στο αποτέλεσμα.

## Βήμα 5: Εκτέλεση του OCR Engine στην Εικόνα Σας

Με όλα συνδεδεμένα, ήρθε η ώρα να αναγνωρίσετε πραγματικά το κείμενο. Παρέχετε τη διαδρομή στην εικόνα σας και τις επιλογές που μόλις δημιουργήσαμε.

```csharp
// Step 5: Perform OCR on the target image using the configured options.
OcrResult ocrResult = ocrEngine.RecognizeImage(
    "Images/passport_scan.png", // Adjust this path to your file location
    ocrOptions);
```

Η μέθοδος επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το εξαγόμενο κείμενο, τους δείκτες εμπιστοσύνης και ακόμη και τα πλαίσια οριοθέτησης για κάθε λέξη (αν τα χρειαστείτε αργότερα).

## Βήμα 6: Εμφάνιση του Εξαγόμενου Κειμένου

Τέλος, εμφανίστε το αποτέλεσμα. Σε μια πραγματική εφαρμογή μπορεί να το αποθηκεύσετε σε βάση δεδομένων, αλλά για αυτό το tutorial μια απλή έξοδος στην κονσόλα αρκεί.

```csharp
// Step 6: Show the extracted text in the console.
Console.WriteLine("Extracted name: " + ocrResult.Text);
```

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε κάτι όπως:

```
Extracted name: JOHN DOE
```

Αν η έξοδος είναι κενή ή ακατανόητη, ελέγξτε ξανά τις συντεταγμένες ROI και βεβαιωθείτε ότι η πηγή εικόνας είναι καθαρή (υψηλή αντίθεση, ελάχιστη θολότητα).

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται ολόκληρο το αρχείο `Program.cs` έτοιμο για μεταγλώττιση. Αποθηκεύστε το σε ένα έργο console, τοποθετήστε την εικόνα σας στον φάκελο `Images` και πατήστε **F5**.

```csharp
using Aspose.OCR;
using System.Drawing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create an OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Step 2: Define the region of interest (ROI) where the text is expected
            // (x, y, width, height) – adjust these values for your own image
            Rectangle regionOfInterest = new Rectangle(150, 300, 800, 200);

            // Step 3: Prepare OCR options and assign the ROI
            OcrOptions ocrOptions = new OcrOptions { Roi = regionOfInterest };

            // Step 4: Perform OCR on the target image using the configured options
            OcrResult ocrResult = ocrEngine.RecognizeImage(
                "Images/passport_scan.png",
                ocrOptions);

            // Step 5: Display the extracted text
            Console.WriteLine("Extracted name: " + ocrResult.Text);
        }
    }
}
```

> **Αναμενόμενη έξοδος:**  
> `Extracted name: JOHN DOE` (ή όποιο κείμενο βρίσκεται στην καθορισμένη ROI).

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν η εικόνα μου είναι σε διαφορετική μορφή;

Το Aspose OCR υποστηρίζει PNG, JPEG, BMP, TIFF και ακόμη PDF. Απλώς αλλάξτε την επέκταση του αρχείου στη διαδρομή· η μηχανή ανιχνεύει αυτόματα τη μορφή.

### Μπορώ να επεξεργαστώ πολλαπλές εικόνες σε βρόχο;

Απολύτως. Το `OcrEngine` μπορεί να επαναχρησιμοποιηθεί:

```csharp
foreach (var file in Directory.GetFiles("Images", "*.png"))
{
    var result = ocrEngine.RecognizeImage(file, ocrOptions);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text}");
}
```

### Πώς μπορώ να βελτιώσω την ακρίβεια για μη‑λατινικά σενάρια;

Ορίστε την ιδιότητα γλώσσας στο `OcrOptions`:

```csharp
ocrOptions.Language = Language.English; // or Language.Russian, Language.ChineseSimplified, etc.
```

### Τι γίνεται αν το ROI είναι λανθασμένο και χάσω το κείμενο;

Μπορείτε είτε να μεγαλώσετε το ορθογώνιο είτε να παραλείψετε εντελώς το ROI ώστε η μηχανή να σαρώσει ολόκληρη την εικόνα. Λάβετε υπόψη ότι η σάρωση ολόκληρης της εικόνας μπορεί να αυξήσει τον χρόνο επεξεργασίας.

## Επαγγελματικές Συμβουλές για Ομαλή Εμπειρία

- **Cache the engine:** Η δημιουργία νέου `OcrEngine` για κάθε εικόνα προσθέτει επιβάρυνση. Διατηρήστε ένα μόνο παράδειγμα ενεργό όσο τρέχει η εφαρμογή σας.
- **Pre‑process the image:** Απλά βήματα όπως η μετατροπή σε κλίμακα του γκρι ή η αύξηση της αντίθεσης μπορούν να βελτιώσουν δραματικά τα ποσοστά αναγνώρισης.
- **Handle null results:** Πάντα ελέγξτε `ocrResult?.Text` πριν το χρησιμοποιήσετε για να αποφύγετε `NullReferenceException`.
- **License matters:** Η δωρεάν έκδοση προσθέτει υδατογράφημα μετά τους πρώτους 200 χαρακτήρες. Καταχωρίστε δοκιμαστική ή εμπορική άδεια αν χρειάζεστε έξοδο παραγωγικής ποιότητας.

## Επόμενα Βήματα

Τώρα που έχετε κατακτήσει τα βασικά του **c# ocr tutorial**, σκεφτείτε να εξερευνήσετε:

- **How to extract text from image** σε μαζική επεξεργασία (batch processing)
- Χρήση του **Aspose OCR** για ανίχνευση πινάκων ή δομημένων δεδομένων
- Ενσωμάτωση του αποτελέσματος OCR με βάση δεδομένων ή web API
- Συνδυασμός OCR με βιβλιοθήκες **image pre‑processing** όπως το `OpenCvSharp`

Κάθε ένα από αυτά τα θέματα βασίζεται στο θεμέλιο που δημιουργήσατε, επιτρέποντάς σας να μετατρέψετε ακατέργαστες σαρώσεις σε αναζητήσιμα, επεξεργάσιμα δεδομένα.

---

*Έτοιμοι να το θέσετε σε παραγωγή; Κατεβάστε τον πλήρη κώδικα από το αποθετήριο μου στο GitHub, προσαρμόστε το ROI για τα δικά σας έγγραφα, και δείτε το κείμενο να εμφανίζεται σαν μαγεία.*  

Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}