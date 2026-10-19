---
category: general
date: 2026-05-21
description: Δημιουργήστε αναζητήσιμο PDF χρησιμοποιώντας το Aspose OCR ενώ βελτιώνετε
  την ακρίβεια του OCR και μαθαίνετε πώς να φορτώνετε εικόνα για OCR σε C#. Βήμα‑βήμα
  οδηγός.
draft: false
keywords:
- create searchable PDF
- improve OCR accuracy
- load image for OCR
- Aspose OCR C#
- PDF output with OCR
language: el
og_description: Δημιουργήστε PDF με δυνατότητα αναζήτησης χρησιμοποιώντας το Aspose
  OCR. Μάθετε πώς να βελτιώσετε την ακρίβεια του OCR και να φορτώσετε εικόνα για OCR
  σε ένα ενιαίο, εκτελέσιμο παράδειγμα.
og_title: Δημιουργήστε Αναζητήσιμο PDF με Aspose OCR – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Create searchable PDF using Aspose OCR while you improve OCR accuracy
    and learn how to load image for OCR in C#. Step‑by‑step tutorial.
  headline: Create Searchable PDF with Aspose OCR – Complete Programming Guide
  type: TechArticle
tags:
- OCR
- Aspose
- PDF
- C#
title: Δημιουργία Αναζητήσιμου PDF με Aspose OCR – Πλήρης Οδηγός Προγραμματισμού
url: /el/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF με Aspose OCR – Πλήρης Οδηγός Προγραμματισμού

Κάποτε χρειάστηκε να **δημιουργήσετε αναζητήσιμο PDF** από μια σαρωμένη εικόνα αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν αρχίζουν έργα OCR. Τα καλά νέα είναι ότι το Aspose OCR κάνει όλη τη διαδικασία—φόρτωση της εικόνας, βελτιστοποίηση της εικόνας για καλύτερα αποτελέσματα, και τελικά αποθήκευση ενός αναζητήσιμου PDF—πολύ απλή.

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από ένα πλήρες, ολοκληρωμένο παράδειγμα που όχι μόνο δείχνει πώς να **δημιουργήσετε αναζητήσιμο PDF**, αλλά επίσης δείχνει πώς να **βελτιώσετε την ακρίβεια του OCR** και τον σωστό τρόπο **φόρτωσης εικόνας για OCR**. Στο τέλος θα έχετε μια έτοιμη εφαρμογή κονσόλας C# που παράγει ένα αναζητήσιμο PDF με την αρχική εικόνα ενσωματωμένη.

## Τι Θα Μάθετε

- Ρύθμιση του Aspose OCR (συμπεριλαμβανομένης της προαιρετικής επιτάχυνσης GPU)  
- Διαμόρφωση της μηχανής για γαλλικά (ή οποιαδήποτε γλώσσα) ώστε να **βελτιώσετε την ακρίβεια του OCR**  
- Σωστή **φόρτωση εικόνας για OCR** χρησιμοποιώντας `ImageStream`  
- Δημιουργία αλυσίδας φίλτρων για καθαρισμό της εικόνας πριν την αναγνώριση  
- Αποθήκευση του αποτελέσματος ως αναζητήσιμο PDF με την πηγαία εικόνα ενσωματωμένη  

Δεν απαιτούνται εξωτερικές εξαρτήσεις εκτός από το Aspose OCR, και ο κώδικας λειτουργεί σε .NET 6+ (ή .NET Framework 4.6+). Ας ξεκινήσουμε.

---

![Δείγμα αναζητήσιμου PDF που δημιουργήθηκε από το Aspose OCR – παράδειγμα δημιουργίας αναζητήσιμου PDF](images/searchable-pdf-sample.png "παράδειγμα δημιουργίας αναζητήσιμου PDF")

## Βήμα 1: Δημιουργία Αναζητήσιμου PDF – Ενεργοποίηση GPU & Ορισμός Διαδρομής Πόρων  

Αν διαθέτετε συμβατό GPU, η ενεργοποίησή του μπορεί να επιταχύνει δραματικά την αναγνώριση. Ακόμη και αν το παραλείψετε, ο υπόλοιπος κώδικας λειτουργεί κανονικά.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;          // optional GPU support
using Aspose.OCR.Pdf;          // PDF output
using Aspose.OCR.Filters;     // pre‑processing filters

// Enable GPU acceleration (optional)
OcrEngine.EnableGpu(true);

// Tell Aspose where to find language data files (offline mode)
OcrEngine.SetResourcesPath(@"YOUR_DIRECTORY/Resources");
```

**Γιατί είναι σημαντικό:** Η επιτάχυνση GPU μειώνει την καθυστέρηση σε μεγάλα παρτίδες, και ο ορισμός της διαδρομής πόρων εξασφαλίζει ότι η μηχανή μπορεί να λειτουργήσει χωρίς σύνδεση στο διαδίκτυο—ιδανικό για CI pipelines ή περιβάλλοντα χωρίς πρόσβαση στο διαδίκτυο.

> **Συμβουλή επαγγελματία:** Αν τρέχετε σε διακομιστή χωρίς οθόνη, βεβαιωθείτε ότι οι οδηγοί CUDA ταιριάζουν με την έκδοση που περιλαμβάνεται στο Aspose OCR· μη συμβατές εκδόσεις μπορούν να προκαλέσουν σιωπηλές αποτυχίες.

## Βήμα 2: Βελτίωση Ακρίβειας OCR – Επιλογή της Σωστής Γλώσσας  

Η επιλογή του σωστού μοντέλου γλώσσας είναι γρήγορη βελτίωση στην ακρίβεια. Εδώ επιλέγουμε γαλλικά, αλλά μπορείτε να αντικαταστήσετε το `OcrLanguage.French` με οποιαδήποτε υποστηριζόμενη γλώσσα.

```csharp
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.French   // improves OCR accuracy for French documents
};
```

**Γιατί είναι σημαντικό:** Τα λεξικά ειδικά για κάθε γλώσσα βοηθούν τη μηχανή να επιλύει αμφίσημους χαρακτήρες (π.χ., “œ” vs “oe”). Αν παραλείψετε αυτό το βήμα, η μηχανή προεπιλέγει τα αγγλικά, κάτι που μπορεί να μειώσει δραστικά την **βελτίωση της ακρίβειας του OCR** για κείμενα μη‑αγγλικής γλώσσας.

## Βήμα 3: Φόρτωση Εικόνας για OCR – Χρήση ImageStream  

Τώρα **φορτώνουμε εικόνα για OCR**. Η βοηθητική μέθοδος `ImageStream.FromFile` αφαιρεί την ανάγκη χειρισμού ακατέργαστων bitmap και λειτουργεί με τις πιο κοινές μορφές (JPG, PNG, TIFF).

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");
```

**Γιατί είναι σημαντικό:** Η φόρτωση της εικόνας με αυτόν τον τρόπο εγγυάται ότι το Aspose λαμβάνει την εικόνα σε μορφή που μπορεί να επεξεργαστεί αποδοτικά. Αν προσπαθήσετε να περάσετε ένα ακατέργαστο `Bitmap` απευθείας, μπορεί να αντιμετωπίσετε προβλήματα διαχείρισης μνήμης σε μεγάλα αρχεία.

## Βήμα 4: Δημιουργία Αλυσίδας Φίλτρων Εικόνας για Αύξηση Ακρίβειας  

Μια καθαρή εικόνα είναι το ήμισυ της μάχης. Η αλυσίδα παρακάτω διορθώνει την κλίση της εικόνας και αφαιρεί τον θόρυβο φόντου—δύο κλασικοί εχθροί που υποβαθμίζουν την **βελτίωση της ακρίβειας του OCR**.

```csharp
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter());   // corrects rotation
filterPipeline.Add(new DenoiseFilter()); // reduces grainy artifacts

// Apply the pipeline and replace the original image
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);
```

**Γιατί είναι σημαντικό:** Η διόρθωση κλίσης εξασφαλίζει ότι οι γραμμές κειμένου είναι οριζόντιες, ενώ η αφαίρεση θορύβου μειώνει τα ψευδή σχήματα χαρακτήρων. Μπορείτε να προσθέσετε περισσότερα φίλτρα (π.χ., `ContrastFilter`) αν οι σάρωσες σας είναι ιδιαίτερα κακής ποιότητας.

## Βήμα 5: Εκτέλεση Αναγνώρισης OCR  

Με την εικόνα προεπεξεργασμένη, αφήνουμε τελικά τη μηχανή να κάνει τη μαγεία της.

```csharp
ocrEngine.Recognize();
```

Αυτή η μοναδική γραμμή ενεργοποιεί το μοντέλο deep‑learning πίσω από το Aspose OCR. Συμπληρώνει το `ocrEngine.Text` με απλό κείμενο και προετοιμάζει επίσης την έξοδο PDF.

> **Τι γίνεται αν το κείμενο φαίνεται παραμορφωμένο;** Ελέγξτε ξανά τη ρύθμιση γλώσσας από το Βήμα 2 και σκεφτείτε να προσθέσετε ένα `BinarizeFilter` στην αλυσίδα φίλτρων.

## Βήμα 6: Αποθήκευση του Αποτελέσματος ως Αναζητήσιμο PDF  

Το τελικό βήμα είναι η αποθήκευση ενός **αναζητήσιμου PDF** όπου το εξαγόμενο κείμενο βρίσκεται πίσω από την αρχική εικόνα—ακριβώς αυτό που χρειάζεστε για νομικά έγγραφα ή αρχειοθέτηση.

```csharp
ocrEngine.Save(@"YOUR_DIRECTORY/output.pdf",
    new PdfSaveOptions { EmbedOriginalImage = true });
```

**Γιατί είναι σημαντικό:** `EmbedOriginalImage = true` διατηρεί την οπτική πιστότητα της σάρωσης ενώ επιτρέπει την αναζήτηση κειμένου. Αν το ορίσετε σε `false`, το PDF θα περιέχει μόνο το εξαγόμενο κείμενο, κάτι που μπορεί να είναι χρήσιμο για ελαφριές αρχειοθήκες.

### Προαιρετικό: Εκτύπωση Αναγνωρισμένου Κειμένου & JSON  

Αν θέλετε να εξετάσετε την ακατέργαστη έξοδο, αυτές οι γραμμές εκτυπώνουν το απλό κείμενο και ένα δομημένο JSON payload.

```csharp
Console.WriteLine(ocrEngine.Text);               // plain text
Console.WriteLine(ocrEngine.GetResultAsJson());  // JSON with layout info
```

**Αναμενόμενη έξοδος:** Μετά την εκτέλεση του προγράμματος, θα δείτε τις γαλλικές προτάσεις να εμφανίζονται στην κονσόλα, ακολουθούμενες από ένα αντικείμενο JSON που περιέχει τα πλαίσια οριοθέτησης, τις βαθμολογίες εμπιστοσύνης και τα μεταδεδομένα γλώσσας.

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;          // optional GPU support
using Aspose.OCR.Pdf;          // PDF output
using Aspose.OCR.Filters;     // pre‑processing filters

// 1️⃣ Enable GPU (optional) and set resources path
OcrEngine.EnableGpu(true);
OcrEngine.SetResourcesPath(@"YOUR_DIRECTORY/Resources");

// 2️⃣ Create and configure the OCR engine (improve OCR accuracy)
var ocrEngine = new OcrEngine { Language = OcrLanguage.French };

// 3️⃣ Load the source image (load image for OCR)
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");

// 4️⃣ Build filter pipeline (deskew + denoise)
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter());
filterPipeline.Add(new DenoiseFilter());
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);

// 5️⃣ Recognize text
ocrEngine.Recognize();

// 6️⃣ Save as searchable PDF (create searchable PDF)
ocrEngine.Save(@"YOUR_DIRECTORY/output.pdf",
    new PdfSaveOptions { EmbedOriginalImage = true });

// Optional: output text and JSON
Console.WriteLine(ocrEngine.Text);
Console.WriteLine(ocrEngine.GetResultAsJson());
```

Τρέξτε το πρόγραμμα, ορίστε το `YOUR_DIRECTORY` σε έναν φάκελο που περιέχει το `input.jpg` και τους πόρους του Aspose OCR, και θα λάβετε το `output.pdf` ακριβώς δίπλα του.

---

## Συμπέρασμα

Τώρα έχετε μια σταθερή, έτοιμη για παραγωγή συνταγή για **δημιουργία αναζητήσιμου PDF** με το Aspose OCR, ενώ ταυτόχρονα μάθατε πώς να **βελτιώσετε την ακρίβεια του OCR** και να **φορτώνετε σωστά εικόνα για OCR**. Η αλυσίδα—GPU (προαιρετικό) → επιλογή γλώσσας → φόρτωση εικόνας → αλυσίδα φίλτρων → αναγνώριση → αποθήκευση PDF—καλύπτει κάθε κρίσιμο βήμα, ώστε να την προσαρμόσετε σε άλλες γλώσσες, μεγαλύτερες παρτίδες ή διαφορετικές μορφές εξόδου.

Τι ακολουθεί; Δοκιμάστε να αντικαταστήσετε το `PdfSaveOptions` με `DocxSaveOptions` για δημιουργία αναζητήσιμων εγγράφων Word, πειραματιστείτε με επιπλέον φίλτρα όπως το `ContrastFilter`, ή ενσωματώστε αυτόν τον κώδικα σε ένα ASP.NET Core API για δημιουργία PDF «on‑the‑fly». Οι δυνατότητες είναι απεριόριστες, και με τη βάση που θέσατε εδώ, είστε έτοιμοι να αντιμετωπίσετε οποιαδήποτε πρόκληση σχετική με OCR.

Έχετε ερωτήσεις ή αντιμετωπίζετε κάποιο πρόβλημα; Αφήστε ένα σχόλιο, και καλή προγραμματιστική δουλειά!

## Σχετικά Μαθήματα

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}