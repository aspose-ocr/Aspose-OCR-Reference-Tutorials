---
category: general
date: 2026-04-01
description: Προεπεξεργασία εικόνας για OCR ώστε να βελτιωθεί η ακρίβεια του OCR.
  Μάθετε πώς να εφαρμόζετε αυτόματη διόρθωση κλίσης, αποθορυβοποίηση και μετατροπή
  σε ασπρόμαυρο χρησιμοποιώντας το Aspose.OCR.
draft: false
keywords:
- preprocess image for OCR
- improve OCR accuracy
- black and white OCR
- Aspose OCR preprocessing
- image deskew C#
- OCR noise reduction
language: el
og_description: Προεπεξεργασία εικόνας για OCR ώστε να βελτιωθεί η ακρίβεια του OCR.
  Αυτός ο οδηγός βήμα‑βήμα δείχνει την αυτόματη ευθυγράμμιση, την αφαίρεση θορύβου
  και τη μετατροπή σε ασπρόμαυρο σε C#.
og_title: Προεπεξεργασία εικόνας για OCR – Βελτιώστε την ακρίβεια με το Aspose.OCR
tags:
- OCR
- C#
- Image Processing
title: Προεπεξεργασία εικόνας για OCR – Αυξήστε την ακρίβεια με το Aspose.OCR
url: /el/net/ocr-optimization/preprocess-image-for-ocr-boost-accuracy-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προεπεξεργασία Εικόνας για OCR – Βελτιώστε την Ακρίβεια με το Aspose.OCR

Έχετε αναρωτηθεί ποτέ γιατί τα αποτελέσματα του OCR σας μοιάζουν με ακατάστατο μπερδεμένο κείμενο, παρόλο που η πηγή εικόνας φαίνεται εντάξει; Πιθανότατα λείπει ένα κρίσιμο βήμα: **preprocess image for OCR**.  
Σε αυτό το tutorial θα δούμε ακριβώς πώς να καθαρίσουμε μια λοξή, θορυβώδη εικόνα ώστε η μηχανή να την διαβάσει σαν επαγγελματίας. Στο τέλος θα δείτε μια αξιοσημείωτη βελτίωση στην **improve OCR accuracy** και θα εξοικειωθείτε με την τεχνική **black and white OCR** που το Aspose.OCR καθιστά εύκολη.

## Τι Θα Μάθετε

Θα καλύψουμε τα πάντα, από την εγκατάσταση του πακέτου Aspose.OCR NuGet μέχρι τη ρύθμιση του `PreprocessOptions` που εκτελεί auto‑deskew, denoise και binarize την εικόνα σας. Θα λάβετε επίσης πρακτικές συμβουλές για τη διαχείριση ακραίων περιπτώσεων — όπως έντονη περιστροφή ή σαρώσεις χαμηλής αντίθεσης — ώστε να διατηρείτε την ποιότητα αναγνώρισης υψηλή, ό,τι και να συμβαίνει. Δεν απαιτούνται εξωτερικά έγγραφα· η ολοκληρωμένη λύση βρίσκεται εδώ.

### Προαπαιτούμενα

- .NET 6.0 ή νεότερο (το παράδειγμα μεταγλωττίζεται με .NET 6, αλλά παλαιότερες εκδόσεις λειτουργούν επίσης)
- Βασική εξοικείωση με C# και Visual Studio (ή οποιοδήποτε IDE προτιμάτε)
- Ένα αρχείο εικόνας που είναι λοξό ή θορυβώδες (θα το ονομάσουμε `skewed_noisy.jpg`)

Αν έχετε τσεκάρει όλα αυτά, ας βουτήξουμε.

## Προεπεξεργασία Εικόνας για OCR – Γιατί η Προεπεξεργασία Σημαίνει

Σκεφτείτε μια μηχανή OCR ως έναν απαιτητικό αναγνώστη: αν η σελίδα είναι λοξή, λεκιασμένη ή πολύ γκρι, θα δυσκολευτεί να διαβάσει τις λέξεις. Η προεπεξεργασία αντιμετωπίζει τρεις κοινούς εχθρούς:

1. **Rotation** – Το Auto‑deskew ευθυγραμμίζει τη σελίδα ώστε οι γραμμές να είναι οριζόντιες.  
2. **Noise** – Το Denoising αφαιρεί τυχαία pixel που διαφορετικά μοιάζουν με τυχαίους χαρακτήρες.  
3. **Contrast** – Η Binarizing (μετατροπή σε μαύρο‑άσπρο) παρέχει στη μηχανή καθαρό διαχωρισμό προσκηνίου/υπόβαθρου.

Μαζί αποτελούν τη ραχοκοκαλιά κάθε ροής εργασίας που θέλει να **improve OCR accuracy**.

![preprocess image for OCR example](https://example.com/ocr-preprocess.png "preprocess image for OCR example")

*(Alt text: “παράδειγμα προεπεξεργασίας εικόνας για OCR που δείχνει πριν και μετά τη δυαδικοποίηση”)*

## Βήμα 1: Εγκατάσταση Aspose.OCR

Πρώτα απ' όλα—πάρτε τη βιβλιοθήκη. Ανοίξτε το τερματικό (ή το Package Manager Console) και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Ή, αν προτιμάτε το UI του Visual Studio, κάντε δεξί‑κλικ στο **Dependencies → Manage NuGet Packages**, ψάξτε για **Aspose.OCR**, και κάντε κλικ στο **Install**. Το πακέτο περιλαμβάνει όλα όσα χρειάζεστε, συμπεριλαμβανομένου του χώρου ονομάτων `Filters` που χρησιμοποιείται για προεπεξεργασία.

## Βήμα 2: Δημιουργία του OCR Engine

Τώρα που η βιβλιοθήκη είναι στη θέση της, μπορούμε να δημιουργήσουμε μια παρουσία του `OcrEngine`. Αυτό το αντικείμενο είναι το σημείο εισόδου για όλη τη δουλειά αναγνώρισης.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Step 2: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // The rest of the steps follow...
    }
}
```

Γιατί δημιουργούμε πρώτα τη μηχανή; Η μηχανή κρατά τις παγκόσμιες ρυθμίσεις (γλώσσα, περιοχή κ.λπ.) και, κυρίως, τις `PreprocessOptions` που θα ρυθμίσουμε στη συνέχεια.

## Βήμα 3: Ρύθμιση των Preprocess Options

Εδώ συμβαίνει η μαγεία. Θα ενεργοποιήσουμε τρία flags:

- `AutoDeskew` – Ανιχνεύει και διορθώνει αυτόματα τη περιστροφή.
- `DenoiseLevel = DenoiseLevel.Medium` – Βρίσκει μια ισορροπία μεταξύ καθαρισμού θορύβου και διατήρησης λεπτομερειών.
- `Binarize` – Εξαναγκάζει έξοδο μαύρο‑άσπρου, την κλασική προσέγγιση **black and white OCR**.

```csharp
// Step 3: Set up preprocessing to clean the image
PreprocessOptions preprocessOptions = new PreprocessOptions
{
    AutoDeskew = true,                     // Correct rotation automatically
    DenoiseLevel = DenoiseLevel.Medium,   // Reduce noise while preserving details
    Binarize = true                        // Convert to black‑and‑white for better recognition
};

// Attach options to the engine
ocrEngine.PreprocessOptions = preprocessOptions;
```

**Γιατί αυτές οι ρυθμίσεις;** Το Auto‑deskew αντιμετωπίζει τις πιο κοινές κλίσεις (μέχρι ~15°). Η μέτρια αποθόρυβωση λειτουργεί για τυπικά σαρωμένα έγγραφα· μπορείτε να την αυξήσετε σε `High` για πολύ θορυβώδεις σαρώσεις, αλλά προσέξτε να μην χάσετε μικρούς χαρακτήρες. Η δυαδικοποίηση είναι η βάση του **black and white OCR** — αφαιρεί ήπιες γκρι κλίμακες που μπερδεύουν τον αναγνώστη.

## Βήμα 4: Εκτέλεση Αναγνώρισης σε Θορυβώδη Εικόνα

Με τη μηχανή έτοιμη, δώστε της τη διαδρομή προς την προβληματική εικόνα. Η μέθοδος `Recognize` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το εξαγόμενο κείμενο και τις βαθμολογίες εμπιστοσύνης.

```csharp
// Step 4: Recognize text from a skewed and noisy image
// Replace the path with your actual image location
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/skewed_noisy.jpg");

// Output the raw text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

Αν όλα πάνε ομαλά, θα δείτε ένα καθαρό μπλοκ κειμένου στην κονσόλα. Η μηχανή εκθέτει επίσης το `ocrResult.Confidence` αν χρειάζεστε αριθμητικό μέτρο για **improve OCR accuracy**.

## Βήμα 5: Επαλήθευση του Αποτελέσματος και Λεπτομερής Ρύθμιση για Καλύτερη Ακρίβεια

Το να βλέπετε το αποτέλεσμα είναι υπέροχο, αλλά μπορεί να παρατηρήσετε ακόμη μερικά λάθη ανάγνωσης — ειδικά με ασυνήθιστα fonts. Εδώ είναι μερικοί γρήγοροι έλεγχοι:

1. **Inspect Confidence** – Τιμές κάτω από 0.7 συχνά υποδεικνύουν προβληματική περιοχή. Μπορείτε να τις καταγράψετε και να αποφασίσετε αν θα επεξεργαστείτε ξανά με υψηλότερο `DenoiseLevel`.
2. **Adjust Binarization Threshold** – Το Aspose σας επιτρέπει να περάσετε ένα προσαρμοσμένο όριο μέσω του `PreprocessOptions.BinarizationThreshold`. Χαμηλότεροι αριθμοί διατηρούν περισσότερο γκρι, υψηλότεροι αριθμοί επιβάλλουν πιο αυστηρό μαύρο‑άσπρο.
3. **Crop or Resize** – Αν η εικόνα είναι τεράστια, μειώστε την σε ~150 DPI πριν τη δώσετε στη μηχανή· αυτό επιταχύνει την επεξεργασία και μπορεί πραγματικά να αυξήσει την ακρίβεια.

```csharp
// Example: Increase denoise for a very dirty scan
ocrEngine.PreprocessOptions.DenoiseLevel = DenoiseLevel.High;

// Re‑run recognition
var refinedResult = ocrEngine.Recognize("YOUR_DIRECTORY/very_dirty.jpg");
Console.WriteLine(refinedResult.Text);
```

## Bonus: Χρήση Black and White OCR για Ακόμη Καλύτερα Αποτελέσματα

Μερικές φορές θα ακούσετε προγραμματιστές να λένε «απλώς μείνετε στο grayscale» — αλλά η προσέγγιση **black and white OCR** συχνά την ξεπερνά, ειδικά όταν το υλικό προέλευσης έχει άνιση φωτισμό. Εξαναγκάζοντας μια δυαδική εικόνα, αφαιρείτε ήπιες σκιές που η μηχανή μπορεί να παρερμηνεύσει ως χαρακτήρες.

Αν θέλετε να πειραματιστείτε περισσότερο, μπορείτε να δημιουργήσετε τη δυαδική εικόνα μόνοι σας και να τη δώσετε στη μηχανή:

```csharp
// Generate a binary bitmap manually (optional)
Bitmap binaryBitmap = ocrEngine.PreprocessOptions.ApplyFilters(
    Image.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg")
);

// Pass the bitmap directly
var bitmapResult = ocrEngine.Recognize(binaryBitmap);
Console.WriteLine(bitmapResult.Text);
```

Αυτό σας δίνει πλήρη έλεγχο πάνω στη διαδικασία προεπεξεργασίας, κάτι που μπορεί να φανεί χρήσιμο όταν χρειάζεται να ενσωματώσετε προσαρμοσμένα φίλτρα ή βιβλιοθήκες εικόνας τρίτων.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας τα πάντα, εδώ είναι μια έτοιμη για εκτέλεση εφαρμογή console που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο έργο C#.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing (auto‑deskew, denoise, binarize)
        PreprocessOptions preprocessOptions = new PreprocessOptions
        {
            AutoDeskew = true,
            DenoiseLevel = DenoiseLevel.Medium,
            Binarize = true
        };
        ocrEngine.PreprocessOptions = preprocessOptions;

        // 3️⃣ Recognize the image (replace with your file path)
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 4️⃣ Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);

        // 5️⃣ Optional: tweak settings if confidence is low
        if (ocrResult.Confidence < 0.7)
        {
            Console.WriteLine("\nLow confidence detected – increasing denoise level.");
            ocrEngine.PreprocessOptions.DenoiseLevel = DenoiseLevel.High;
            var retryResult = ocrEngine.Recognize("YOUR_DIRECTORY/skewed_noisy.jpg");
            Console.WriteLine("=== Refined Output ===");
            Console.WriteLine(retryResult.Text);
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα στην κονσόλα**

```
=== OCR Output ===
The quick brown fox jumps over the lazy dog.

=== Refined Output ===
The quick brown fox jumps over the lazy dog.
```

*Το πραγματικό σας κείμενο θα διαφέρει, φυσικά, αλλά θα πρέπει να παρατηρήσετε την ίδια καθαρή μορφοποίηση.*

## Συμπέρασμα

Μόλις σας δείξαμε πώς να **preprocess image for OCR** χρησιμοποιώντας το Aspose.OCR, και γιατί κάθε βήμα — auto‑deskew, denoise και μετατροπή σε μαύρο‑άσπρο — παίζει καθοριστικό ρόλο στην **improve OCR accuracy**. Ακολουθώντας τον παραπάνω κώδικα, θα έχετε αξιόπιστα αποτελέσματα σε θορυβώδεις, λοξές σαρώσεις χωρίς να ψάχνετε στην τεκμηρίωση.

Τι ακολουθεί; Δοκιμάστε να συνδυάσετε αυτή τη ροή εργασίας με ρυθμίσεις ειδικές για γλώσσες (π.χ., `ocrEngine.Language = Language.English`) ή δώστε το καθαρισμένο bitmap σε ένα downstream μοντέλο NLP. Μπορείτε επίσης να πειραματιστείτε με το `BinarizationThreshold` για να ρυθμίσετε λεπτομερώς το αποτέλεσμα **black and white OCR** για αποδείξεις χαμηλής αντίθεσης ή χειρόγραφες σημειώσεις.

Μη διστάσετε να αφήσετε ένα σχόλιο αν αντιμετωπίσετε προβλήματα, ή να μοιραστείτε τα δικά σας κόλπα για να εξάγετε επιπλέον ακρίβεια από το OCR. Καλό κώδικα, και εύχομαι το κείμενό σας να είναι πάντα αναγνώσιμο!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}