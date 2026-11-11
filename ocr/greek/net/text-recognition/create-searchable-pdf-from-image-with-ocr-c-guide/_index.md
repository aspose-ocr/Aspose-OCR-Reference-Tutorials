---
category: general
date: 2026-03-18
description: Δημιουργήστε PDF με δυνατότητα αναζήτησης χρησιμοποιώντας το Aspose OCR
  σε C#. Μετατρέψτε την εικόνα σε PDF, προσθέστε στρώση κειμένου OCR και γράψτε τα
  bytes του PDF σε αρχείο σε λίγα εύκολα βήματα.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- add ocr text layer
- write pdf bytes to file
language: el
og_description: Δημιουργήστε γρήγορα PDF με δυνατότητα αναζήτησης χρησιμοποιώντας
  το Aspose OCR σε C#. Μάθετε πώς να μετατρέπετε εικόνα σε PDF, να προσθέτετε στρώση
  κειμένου OCR και να γράφετε τα bytes του PDF σε αρχείο.
og_title: Δημιουργία PDF με δυνατότητα αναζήτησης από εικόνα – Γρήγορος οδηγός OCR
  σε C#
tags:
- OCR
- PDF
- C#
- Aspose
title: Δημιουργία PDF με δυνατότητα αναζήτησης από εικόνα με OCR – Οδηγός C#
url: /el/net/text-recognition/create-searchable-pdf-from-image-with-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία αναζητήσιμου PDF από εικόνα με OCR – Οδηγός C#

Έχετε ποτέ χρειαστεί να **δημιουργήσετε αναζητήσιμο PDF** από μια σαρωμένη εικόνα; Με το Aspose OCR μπορείτε να το κάνετε σε λίγες γραμμές, χωρίς βαριές βιβλιοθήκες. Σε αυτό το tutorial θα **μετατρέψουμε την εικόνα σε PDF**, θα προσθέσουμε μια **στρώση κειμένου OCR** από πάνω, και τελικά θα **γράψουμε τα bytes του PDF σε αρχείο** ώστε να έχετε ένα έγγραφο PDF/A‑2b συμβατό με πρότυπα που οι χρήστες σας μπορούν πραγματικά να αναζητήσουν.

Αν αναρωτιέστε γιατί να ασχοληθείτε με ένα αναζητήσιμο PDF αντί για ένα αρχείο μόνο με εικόνα, σκεφτείτε την εμπειρία του χρήστη: ένα αναζητήσιμο PDF επιτρέπει στους ανθρώπους να αντιγράφουν, να επιλέγουν και να ευρετηριάζουν το κείμενο—ιδανικό για αρχεία, νομικά έγγραφα ή οποιαδήποτε ροή εργασίας που χρειάζεται εξαγωγή κειμένου αργότερα. Ας ξεκινήσουμε.

## Τι θα χρειαστείτε

- .NET 6 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+)
- Ένα πακέτο NuGet Aspose.OCR (`Aspose.OCR` έκδοση 23.10 ή νεότερη)
- Μια raster εικόνα (`.png`, `.jpg`, κλπ.) που θέλετε να μετατρέψετε σε αναζητήσιμο PDF
- Μια βασική γνώση C#—τίποτα περίπλοκο, μόνο τα θεμέλια

Αυτό είναι όλο. Χωρίς εξωτερικά εργαλεία, χωρίς επιπλέον μετατροπείς. Όλη η βαριά δουλειά γίνεται από τη μηχανή OCR της Aspose.

## Δημιουργία Αναζητήσιμου PDF – Επισκόπηση

Πριν βουτήξουμε στον κώδικα, ας περιγράψουμε τη διαδικασία:

1. **Δημιουργία** της μηχανής OCR – αυτό το αντικείμενο ξέρει πώς να διαβάζει κείμενο από εικόνες.  
2. **Φόρτωση** της πηγαίας εικόνας – θα περάσουμε ένα `ImageStream` στη μηχανή.  
3. **Διαμόρφωση** των επιλογών αποθήκευσης PDF/A‑2b – αυτό λέει στην Aspose να ενσωματώσει το αναγνωρισμένο κείμενο ως κρυφή στρώση.  
4. **Εκτέλεση** του OCR και **σύλληψη** των παραγόμενων bytes PDF.  
5. **Γραφή** αυτών των bytes στο δίσκο, παράγοντας το τελικό αναζητήσιμο αρχείο PDF.

Κάθε ένα από αυτά τα βήματα αντιστοιχεί άμεσα σε μία ή δύο γραμμές C#, κάνοντας όλη τη ροή εργασίας να μοιάζει με ένα μικρό script αντί για ένα τεράστιο έργο.

## Βήμα 1: Μετατροπή Εικόνας σε PDF – Φόρτωση της Εικόνας

Πρώτα απ' όλα: πρέπει να δώσουμε στη μηχανή OCR κάτι για ανάγνωση. Η βοηθητική μέθοδος `ImageStream.FromFile` φορτώνει το αρχείο σε ένα stream που η Aspose μπορεί να επεξεργαστεί.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

// 1️⃣ Load the source image you want to turn into a searchable PDF
ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");
```

> **Pro tip:** Κρατήστε την ανάλυση της εικόνας σας τουλάχιστον 300 dpi· η ακρίβεια του OCR μειώνεται δραματικά σε χαμηλής ανάλυσης σάρωση.

## Βήμα 2: Αναγνώριση Κειμένου από την Εικόνα και Προσθήκη Στρώσης Κειμένου OCR

Τώρα δημιουργούμε τη μηχανή OCR και της λέμε να αναγνωρίσει το κείμενο. Η μαγεία συμβαίνει όταν συνδυάζουμε το αποτέλεσμα αναγνώρισης με `PdfSaveOptions` που έχουν `IncludeTextLayer = true`. Αυτή η σημαία αναγκάζει την Aspose να ενσωματώσει τους εξαγόμενους χαρακτήρες ως αόρατη στρώση κειμένου, κάτι που κάνει το PDF αναζητήσιμο.

```csharp
// 2️⃣ Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// 3️⃣ Set up PDF/A‑2b save options – includes the hidden text layer
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
{
    PdfCompliance = PdfCompliance.PdfA2b, // ensures PDF/A‑2b compliance
    IncludeTextLayer = true               // this is the key for searchable PDFs
};
```

Γιατί PDF/A‑2b; Είναι ένα πρότυπο ISO για αρχειοθέτηση που εγγυάται μακροπρόθεσμη διατήρηση και, σημαντικό για εμάς, εξαναγκάζει το PDF να περιέχει μια αναζητήσιμη στρώση κειμένου. Αν δεν χρειάζεστε συμμόρφωση με πρότυπο αρχειοθέτησης, μπορείτε να παραλείψετε το `PdfCompliance` εντελώς, αλλά η διατήρησή του δεν σας κοστίζει τίποτα.

## Βήμα 3: Γραφή Bytes PDF σε Αρχείο – Αποθήκευση του Αποτελέσματος

Με τη μηχανή έτοιμη και τις επιλογές ορισμένες, εκτελούμε την αναγνώριση και ζητάμε αμέσως από την Aspose να μας δώσει το PDF ως `byte[]`. Στη συνέχεια αποθηκεύουμε αυτά τα bytes στο δίσκο χρησιμοποιώντας `File.WriteAllBytes`. Απλό, αλλά ισχυρό.

```csharp
// 4️⃣ Perform OCR on the image and get the PDF bytes
byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

// 5️⃣ Write the PDF/A‑2b file to the output location
System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
Console.WriteLine("PDF/A‑2b file created – you now have a searchable PDF!");
```

Η γραμμή `Console.WriteLine` είναι προαιρετική, αλλά σας δίνει άμεση ανάδραση όταν τρέχετε το πρόγραμμα από ένα τερματικό.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας τα πάντα, εδώ είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αντιγράψτε‑και‑επικολλήστε το σε ένα νέο έργο console, αντικαταστήστε το `YOUR_DIRECTORY` με μια πραγματική διαδρομή, και πατήστε **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

class PdfA2bDemo
{
    static void Main()
    {
        // Step 1: Load the source image
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");

        // Step 2: Create OCR engine and configure PDF/A‑2b options
        OcrEngine ocrEngine = new OcrEngine();
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
        {
            PdfCompliance = PdfCompliance.PdfA2b,
            IncludeTextLayer = true
        };

        // Step 3: Recognize and save as PDF bytes
        byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

        // Step 4: Write the bytes to a searchable PDF file
        System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
        Console.WriteLine("PDF/A‑2b file created.");
    }
}
```

### Αναμενόμενο Αποτέλεσμα

- Ένα αρχείο με όνομα `output.pdf` εμφανίζεται στον φάκελο που καθορίσατε.  
- Ανοίξτε το σε Adobe Acrobat Reader ή οποιονδήποτε PDF viewer και δοκιμάστε να επιλέξετε κείμενο—αν μπορείτε να αντιγράψετε λέξεις, έχετε δημιουργήσει επιτυχώς **αναζητήσιμο PDF**.  
- Το έγγραφο θα περάσει επίσης τα εργαλεία επικύρωσης PDF/A‑2b επειδή χρησιμοποιήσαμε τη σωστή σημαία συμμόρφωσης.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

**Τι γίνεται αν η εικόνα μου περιέχει πολλαπλές σελίδες;**  
Τυλίξτε κάθε σελίδα σε ένα δικό της `ImageStream` και τροφοδοτήστε τα διαδοχικά στη `OcrEngine`. Η Aspose θα συνενώσει αυτόματα τις σελίδες σε ένα ενιαίο PDF.

**Μπορώ να αλλάξω τη γλώσσα του OCR;**  
Απολύτως. Ορίστε `ocrEngine.Language = Language.English;` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) πριν καλέσετε το `Recognize`.

**Τι γίνεται με τη χρήση μνήμης για τεράστια αρχεία;**  
Αν επεξεργάζεστε σάρωση σε κλίμακα gigabyte, σκεφτείτε να κάνετε streaming του αποτελέσματος απευθείας σε ένα `FileStream` αντί να κρατάτε ολόκληρο το `byte[]` στη μνήμη:

```csharp
using (var file = new FileStream("output.pdf", FileMode.Create))
{
    ocrEngine.Recognize(image).Save(pdfSaveOptions, file);
}
```

**Χρειάζομαι άδεια;**  
Η Aspose προσφέρει δωρεάν δοκιμή χωρίς υδατογράφημα. Για παραγωγική χρήση, αγοράστε άδεια ώστε να αφαιρεθεί το banner αξιολόγησης και να ξεκλειδωθούν όλες οι λειτουργίες.

## Συμβουλές για Καλύτερη Ακρίβεια OCR

- **Προ‑επεξεργασία** της εικόνας: ευθυγράμμιση, απομάκρυνση θορύβου και αύξηση αντίθεσης.  
- **Χρήση μορφών χωρίς απώλειες** όπως PNG· τα σφάλματα συμπίεσης JPEG μπορούν να μπερδέψουν τη μηχανή.  
- **Αποφυγή χρωματιστών υποβάθρων**· ένα καθαρό λευκό υπόβαθρο δίνει τα καλύτερα αποτελέσματα.

## Επόμενα Βήματα

Τώρα που μπορείτε να **δημιουργήσετε αναζητήσιμο PDF**, ίσως θέλετε να:

- **Επεξεργαστείτε μαζικά** έναν φάκελο εικόνων χρησιμοποιώντας `Directory.GetFiles`.  
- **Εξάγετε το κρυφό κείμενο** αργότερα με τα API του `PdfDocument` για ευρετηρίαση.  
- **Συνδυάστε OCR με ψηφιακές υπογραφές** για δημιουργία αρχείων που αποδεικνύουν μη παραβίαση.  

Όλα αυτά βασίζονται στο ίδιο βασικό μοτίβο που καλύψαμε: φόρτωση, αναγνώριση, διαμόρφωση, αποθήκευση.

---

*Έτοιμοι να μετατρέψετε τα σαρωμένα αρχεία σας σε αναζητήσιμα PDF; Πάρτε τον κώδικα, δείξτε του τις εικόνες σας, και αφήστε το Aspose να κάνει τη βαριά δουλειά. Καλή προγραμματιστική!*

![Παράδειγμα δημιουργίας αναζητήσιμου PDF](/images/create-searchable-pdf.png "Εικονογράφηση ενός αναζητήσιμου PDF που δημιουργήθηκε από μια εικόνα")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}