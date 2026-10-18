---
category: general
date: 2026-02-20
description: Προεπεξεργασία OCR εικόνας με το Aspose.OCR σε C#. Μάθετε πώς να εφαρμόζετε
  φίλτρο διαμέσου, να μειώνετε τον θόρυβο της εικόνας και να εξάγετε κείμενο από την
  εικόνα αποδοτικά.
draft: false
keywords:
- preprocess image OCR
- apply median filter
- extract text image
- reduce image noise
- c# ocr example
language: el
og_description: Προεπεξεργασία OCR εικόνας με το Aspose.OCR. Αυτό το σεμινάριο δείχνει
  πώς να εφαρμόσετε φίλτρο διαμέσου, να μειώσετε τον θόρυβο της εικόνας και να εξάγετε
  κείμενο από την εικόνα χρησιμοποιώντας C#.
og_title: Προεπεξεργασία OCR εικόνας σε C# – Πλήρης Οδηγός
tags:
- OCR
- C#
- Image Processing
title: Προεπεξεργασία OCR εικόνας σε C# – Πλήρης οδηγός βήμα‑προς‑βήμα
url: /el/net/ocr-optimization/preprocess-image-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προεπεξεργασία OCR Εικόνας σε C# – Πλήρης Οδηγός Βήμα‑βήμα

Σας έχει συμβεί ποτέ να χρειάζεται να **προεπεξεργαστείτε OCR εικόνας** επειδή οι σαρωμένες φωτογραφίες σας επιστρέφουν ακατάληπτο κείμενο; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα—π.χ. αποδείξεις, ταυτότητες ή χειρόγραφα σημειώματα—η ακατέργαστη εικόνα σπάνια είναι έτοιμη για άμεση αναγνώριση. Το καλό νέο; Μερικά απλά βήματα προεπεξεργασίας μπορούν να αυξήσουν δραματικά την ακρίβεια, και μπορείτε να τα κάνετε όλα σε C# με το Aspose.OCR.

Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό παράδειγμα που δείχνει πώς να **εφαρμόσετε median filter**, **μειώσετε το θόρυβο της εικόνας**, και τελικά **εξάγετε κείμενο από την εικόνα** με καθαρό, αναγνώσιμο αποτέλεσμα. Στο τέλος θα έχετε μια πλήρως εκτελέσιμη εφαρμογή κονσόλας C# που μπορείτε να ενσωματώσετε σε οποιαδήποτε λύση .NET. Χωρίς ασαφείς αναφορές, μόνο ο κώδικας που χρειάζεστε και το «γιατί» πίσω από κάθε γραμμή.

---

## Τι Θα Χρειαστείτε

- **Aspose.OCR for .NET** (τελευταία έκδοση τη στιγμή της συγγραφής, 23.12). Μπορείτε να το αποκτήσετε μέσω NuGet: `Install-Package Aspose.OCR`.
- .NET 6.0 ή νεότερο (το παράδειγμα χρησιμοποιεί εφαρμογή κονσόλας, αλλά η ίδια λογική λειτουργεί σε ASP.NET, WPF κ.λπ.).
- Ένα δείγμα εικόνας που χρειάζεται καθαρισμό—π.χ. `skewed_photo.jpg`.  
- Μια μέτρια εμπειρία με C#· οι έννοιες είναι απλές ακόμη και για junior developers.

> **Pro tip:** Αν εργάζεστε σε εταιρικό υπολογιστή, βεβαιωθείτε ότι το NuGet feed σας είναι ρυθμισμένο ώστε να επιτρέπει εξωτερικά πακέτα, διαφορετικά η εγκατάσταση θα αποτύχει.

---

## Βήμα 1 – Δημιουργία του Αντικειμένου OCR Engine  

Το πρώτο που κάνετε είναι να δημιουργήσετε ένα `OcrEngine`. Αυτό το αντικείμενο κρατά τις ρυθμίσεις αναγνώρισης και θα επεξεργαστεί αργότερα το προεπεξεργασμένο bitmap.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;   // For Image handling
using System;

class PreprocessExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is the core component that will read text.
        OcrEngine ocrEngine = new OcrEngine();

        // ... we’ll continue with loading and preprocessing the image below.
```

**Γιατί;**  
Η δημιουργία του engine μία φορά και η επαναχρησιμοποίησή του για πολλαπλές εικόνες μειώνει το κόστος. Επιτρέπει επίσης την αλλαγή γλώσσας ή λειτουργιών αναγνώρισης αργότερα χωρίς να χρειάζεται να ξαναχτίσετε ολόκληρη τη ροή.

---

## Βήμα 2 – Φόρτωση της Πηγαίας Εικόνας  

Χρειάζεστε ένα αντικείμενο `System.Drawing.Image` που δείχνει στο ακατέργαστο αρχείο σας. Σε πραγματικό έργο ίσως δεχόσαστε ένα stream, αλλά για σαφήνεια θα διαβάσουμε από δίσκο.

```csharp
        // Load the image that requires preprocessing.
        Image sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_photo.jpg");
```

> **Σημείωση:** Αντικαταστήστε το `YOUR_DIRECTORY` με το πραγματικό μονοπάτι του φακέλου. Αν το αρχείο δεν βρεθεί, θα εξαχθεί `FileNotFoundException`—πιάστε το αν θέλετε πιο ευγενική διαχείριση σφαλμάτων.

---

## Βήμα 3 – Διόρθωση Στρέψης και Περιστροφή της Εικόνας  

Οι περισσότερες σαρωμένες εγγραφές είναι ελαφρώς κεκλιμένες. Το φίλτρο `DeskewAndRotate` ανιχνεύει αυτόματα τη γωνία κλίσης και περιστρέφει την εικόνα σε όρθια θέση.

```csharp
        // Correct orientation – crucial for accurate OCR.
        Image processedImage = sourceImage.Apply(Preprocess.DeskewAndRotate());
```

**Γιατί έχει σημασία;**  
Οι μηχανές OCR υποθέτουν ότι οι γραμμές κειμένου είναι οριζόντιες. Ακόμη και μια κλίση 2 μποίρει να μειώσει την ακρίβεια αναγνώρισης κατά 15‑20 %. Η διόρθωση κλίσης είναι ο πιο οικονομικός τρόπος για μεγάλο κέρδος.

---

## Βήμα 4 – Εφαρμογή Median Filter για Μείωση Θορύβου Εικόνας  

Ο θόρυβος εμφανίζεται ως στίγματα ή τυχαία pixel, ειδικά σε φωτογραφίες χαμηλού φωτισμού. Ένα median filter εξομαλύνει αυτά τα στίγματα ενώ διατηρεί τις άκρες, κάτι που χρειαζόμαστε πριν το OCR.

```csharp
        // Reduce noise – radius of 2 is a good balance for most photos.
        processedImage = processedImage.Apply(Preprocess.MedianFilter(radius: 2));
```

**Γιατί median filter;**  
Σε αντίθεση με ένα mean (μέσο) φίλτρο, το median filter αντικαθιστά κάθε pixel με τη μεσαία τιμή της γειτονιάς του. Αυτό σημαίνει ότι ο απομονωμένος θόρυβος εξαλείφεται χωρίς να θολώνουν τα στίγματα του κειμένου—μια κλασική τεχνική για **reduce image noise**.

---

## Βήμα 5 – Ενίσχυση Αντίθεσης με Stretching  

Μετά την αφαίρεση θορύβου, το επόμενο βήμα είναι να ενισχύσετε τη διαφορά μεταξύ κειμένου και φόντου. Η διάταση αντίθεσης (contrast stretching) διασπείρει τις εντάσεις pixel σε όλο το εύρος 0‑255.

```csharp
        // Stretch contrast to make dark text pop against a light background.
        processedImage = processedImage.Apply(Preprocess.ContrastStretch());
```

**Γιατί stretch;**  
Οι μηχανές OCR βασίζονται σε σαφή διαχωρισμό προσκηνίου‑υπόβαθρου. Αν η εικόνα είναι ξεθωριασμένη, η μηχανή μπορεί να θεωρήσει το κείμενο ως φόντο. Η διάταση αντίθεσης διορθώνει αυτό το πρόβλημα χωρίς να απαιτείται χειροκίνητη κατωφλίωση.

---

## Βήμα 6 – Εκτέλεση OCR στην Προεπεξεργασμένη Εικόνα  

Τώρα που η εικόνα είναι ευθεία, καθαρή και υψηλής αντίθεσης, την παραδίδουμε στον OCR engine.

```csharp
        // Recognize the text from the cleaned image.
        string extractedText = ocrEngine.Recognize(processedImage);
```

**Τι λαμβάνετε:**  
Το `extractedText` περιέχει το ακατέργαστο Unicode string που ανίχνευσε το Aspose.OCR. Μπορείτε να το επεξεργαστείτε περαιτέρω (trim, regex κ.λπ.) αν χρειάζεται.

---

## Βήμα 7 – Εξαγωγή του Αναγνωρισμένου Κειμένου  

Τέλος, γράψτε το αποτέλεσμα στην κονσόλα ή σε αρχείο—ό,τι ταιριάζει στη ροή εργασίας σας.

```csharp
        // Show the result in the console.
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Αν το `skewed_photo.jpg` περιέχει τη φράση “Hello World”, θα δείτε κάτι όπως:

```
=== Extracted Text ===
Hello World
```

Αν η εικόνα παραμένει θορυβώδης, μπορεί να παρατηρήσετε ακατάληπτους χαρακτήρες—επιστρέψτε στο Βήμα 4 και αυξήστε την ακτίνα του median filter, ή πειραματιστείτε με πρόσθετα φίλτρα όπως `GaussianBlur`.

---

## Πλήρες Παράδειγμα (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι ολόκληρο το πρόγραμμα, έτοιμο για μεταγλώττιση. Δεν λείπουν κομμάτια—απλώς αντικαταστήστε τη διαδρομή του αρχείου.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;
using System;

class PreprocessExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image that needs preprocessing
        Image sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_photo.jpg");

        // Step 3: Deskew and rotate the image to correct orientation
        Image processedImage = sourceImage.Apply(Preprocess.DeskewAndRotate());

        // Step 4: Reduce noise with a median filter (radius = 2)
        processedImage = processedImage.Apply(Preprocess.MedianFilter(radius: 2));

        // Step 5: Enhance contrast using contrast stretching
        processedImage = processedImage.Apply(Preprocess.ContrastStretch());

        // Step 6: Perform OCR on the preprocessed image
        string extractedText = ocrEngine.Recognize(processedImage);

        // Step 7: Output the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

> **Συμβουλή για ειδικές περιπτώσεις:** Αν η εικόνα σας περιέχει χρωματιστό κείμενο πάνω σε χρωματιστό φόντο, σκεφτείτε να τη μετατρέψετε σε grayscale πριν εφαρμόσετε `ContrastStretch`. Μπορείτε να το κάνετε με `Preprocess.Grayscale()` στην αλυσίδα.

---

## Συχνές Ερωτήσεις & Παραλλαγές  

### Τι γίνεται αν η εικόνα είναι ανάποδα;  
`DeskewAndRotate` ανιχνεύει αυτόματα περιστροφές 180 μοίρες, αλλά μπορείτε να εξαναγκάσετε περιστροφή με `Preprocess.Rotate(angle: 180)` πριν από το deskew.

### Μπορώ να παραλείψω το median filter;  
Ναι, αλλά πιθανότατα θα δείτε μειωμένα οφέλη **reduce image noise**. Σε υψηλής ανάλυσης σκαναρίσματα το φίλτρο μπορεί να μην είναι απαραίτητο· σε φωτογραφίες χαμηλού φωτισμού, συνήθως είναι κρίσιμο.

### Πώς διαφέρει αυτό από ένα απλό `Apply(Preprocess.Binarize())`;  
Η δυαδικοποίηση μετατρέπει την εικόνα σε καθαρό μαύρο‑άσπρο, κάτι που μπορεί να είναι σκληρό για λεπτές γραμματοσειρές. Η προσέγγισή μας διατηρεί τις λεπτομέρειες του grayscale, έπειτα διαστέλλει την αντίθεση—συχνά αποδίδει καλύτερα για γραμματοσειρές διαφορετικού μεγέθους.

### Υπάρχει τρόπος να **εφαρμόσετε median filter** μόνο σε περιοχή ενδιαφέροντος;  
Το `Apply` του Aspose.OCR λειτουργεί σε ολόκληρο το bitmap, αλλά μπορείτε πρώτα να κόψετε την εικόνα (`sourceImage.Clone(new Rectangle(...), sourceImage.PixelFormat)`) και μετά να εφαρμόσετε το φίλτρο σε αυτό το υπο‑εικόνα.

---

## Επόμενα Βήματα – Πέρα από τη Βασική Προεπεξεργασία  

- **Language Packs:** Αν χρειάζεται να εξάγετε γαλλικούς ή ιαπωνικούς χαρακτήρες, φορτώστε το αντίστοιχο μοντέλο γλώσσας μέσω `ocrEngine.Language = Language.French;`.
- **Custom Thresholding:** Για εξαιρετικά χαμηλής αντίθεσης σκαναρίσματα, πειραματιστείτε με `Preprocess.AdaptiveThreshold()` μετά το median filter.
- **Batch Processing:** Τυλίξτε τα βήματα μέσα σε βρόχο `foreach (string file in Directory.GetFiles(...))` και γράψτε κάθε αποτέλεσμα σε αρχείο `.txt`.  
- **Performance Tuning:** Επαναχρησιμοποιήστε ένα μόνο αντικείμενο `OcrEngine` και προ-κατανείμετε ένα buffer `Bitmap` για να αποφύγετε ξαφνικές αυξήσεις GC όταν επεξεργάζεστε χιλιάδες εικόνες.

---

## Συμπέρασμα  

Δείξαμε πώς να **προεπεξεργαστείτε OCR εικόνας** σε C# από την αρχή μέχρι το τέλος: φόρτωση εικόνας, deskew, **apply median filter**, ενίσχυση αντίθεσης, και τελικά **extract text image** με το Aspose.OCR. Το πλήρες snippet κώδικα είναι έτοιμο να ενσωματωθεί σε οποιοδήποτε έργο, και οι εξηγήσεις παρέχουν το «γιατί» πίσω από κάθε μετασχηματισμό—ώστε να μπορείτε να ρυθμίσετε τις παραμέτρους για τις δικές σας περιπτώσεις.

Δοκιμάστε το με μερικές διαφορετικές φωτογραφίες, παίξτε με την ακτίνα του φίλτρου και παρακολουθήστε την ακρίβεια αναγνώρισης να ανεβαίνει. Όταν νιώσετε άνετα, εξερευνήστε τις πιο προχωρημένες βελτιώσεις που αναφέρθηκαν παραπάνω, και θα γίνετε το άτομο-αναφοράς για καθαρές pipelines OCR στην ομάδα σας.

Καλός κώδικας, και εύχομαι το OCR σας πάντα να διαβάζει καθαρά! 

![παράδειγμα προεπεξεργασίας OCR εικόνας](/images/preprocess-image-ocr.png "preprocess image OCR – πριν και μετά την επεξεργασία")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}