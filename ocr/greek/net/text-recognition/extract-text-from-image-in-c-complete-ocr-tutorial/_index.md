---
category: general
date: 2026-06-06
description: Εξάγετε κείμενο από εικόνα χρησιμοποιώντας C# OCR. Μάθετε πώς να φορτώνετε
  εικόνα για OCR, να αναγνωρίζετε σαρωμένο έγγραφο και να λαμβάνετε ακριβή αποτελέσματα
  σε λίγα λεπτά.
draft: false
keywords:
- extract text from image
- load image for OCR
- recognize scanned document
- c# OCR tutorial
language: el
og_description: Εξαγωγή κειμένου από εικόνα με C#. Αυτό το σεμινάριο δείχνει πώς να
  φορτώσετε εικόνα για OCR, να αναγνωρίσετε σαρωμένο έγγραφο και να κατακτήσετε ένα
  σεμινάριο OCR σε C# βήμα‑βήμα.
og_title: Εξαγωγή κειμένου από εικόνα σε C# – Πλήρης οδηγός OCR
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from image using C# OCR. Learn how to load image for OCR,
    recognize scanned document, and get accurate results in minutes.
  headline: Extract Text from Image in C# – Complete OCR Tutorial
  type: TechArticle
- description: Extract text from image using C# OCR. Learn how to load image for OCR,
    recognize scanned document, and get accurate results in minutes.
  name: Extract Text from Image in C# – Complete OCR Tutorial
  steps:
  - name: Save the code as `Program.cs` inside a new console project.
    text: Save the code as `Program.cs` inside a new console project.
  - name: Open a terminal at the project root.
    text: Open a terminal at the project root.
  - name: Run `dotnet add package Aspose.OCR` (if you haven’t already).
    text: Run `dotnet add package Aspose.OCR` (if you haven’t already).
  - name: 'Build and execute:'
    text: 'Build and execute:'
  type: HowTo
- questions:
  - answer: Yes—most OCR libraries let you load a PDF page as an image stream or expose
      a `PdfDocument` API. Convert each page to an image first, then follow the same
      steps.
    question: Can I process PDFs directly?
  - answer: The `ImageStream.FromFile` method supports JPEG, PNG, BMP, and TIFF out
      of the box. No extra conversion required.
    question: What if my image is in PNG format?
  - answer: Handwriting is a tougher nut to crack. Look for a library that offers
      a “handwriting” model, or pre‑process the image with binarization and noise
      removal before feeding it to the engine.
    question: How do I improve accuracy for handwritten notes?
  - answer: 'Absolutely. Most engines expose a `Rect` or `Region` property where you
      can limit OCR to a bounding box—great for forms with fixed fields. --- ## Next
      Steps & Related Topics Now that you’ve mastered the basics of **extract text
      from image** with a **c# OCR tutorial**, consider exploring: - **Batch p'
    question: Is there a way to extract text in a specific region?
  type: FAQPage
tags:
- OCR
- C#
- Image Processing
title: Εξαγωγή κειμένου από εικόνα σε C# – Πλήρης οδηγός OCR
url: /el/net/text-recognition/extract-text-from-image-in-c-complete-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα σε C# – Πλήρης Οδηγός OCR

Έχετε αναρωτηθεί ποτέ πώς να **εξάγετε κείμενο από εικόνα** χρησιμοποιώντας μόνο λίγες γραμμές C#; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν δυσκολίες όταν πρέπει να αποσπάσουν λέξεις από ένα θορυβώδες, λοξάτο σκανάρισμα, και τα συνηθισμένα κόλπα «αντιγραφή‑επικόλληση» δεν αρκούν.  

Σε αυτόν τον οδηγό θα περάσουμε από ένα πρακτικό **c# OCR tutorial** που δείχνει πώς να **φορτώνετε εικόνα για OCR**, να ενεργοποιήσετε έξυπνη προεπεξεργασία και, τέλος, να **αναγνωρίσετε το περιεχόμενο του σαρωμένου εγγράφου** με κρυστάλλινη ακρίβεια. Στο τέλος θα έχετε ένα εκτελέσιμο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

## Τι Καλύπτει Αυτός ο Οδηγός

- Εγκατάσταση του πακέτου NuGet Aspose.OCR (ή συμβατού)  
- Δημιουργία και ρύθμιση μιας παρουσίας μηχανής OCR  
- **Φόρτωση εικόνας για OCR** – διαχείριση διαδρομών αρχείων, ροών και κοινών παγίδων  
- Ενεργοποίηση αυτόματης προεπεξεργασίας για διόρθωση κλίσης, μείωση θορύβου και προβλήματα αντίθεσης  
- **Αναγνώριση σαρωμένου εγγράφου** – λήψη του αποτελέσματος ως απλό κείμενο  
- Πλήρης πηγαίος κώδικας που μπορείτε να αντιγράψετε‑επικολλήσετε και να τρέξετε αμέσως  

Δεν απαιτείται προηγούμενη εμπειρία OCR· αρκεί μια βασική κατανόηση του C# και του Visual Studio (ή του αγαπημένου σας IDE).  

> **Γιατί να σας ενδιαφέρει;** Η αυτοματοποίηση της εξαγωγής κειμένου ανοίγει δρόμους για επεξεργασία τιμολογίων, αναζητήσιμα PDF, μείωση της εισαγωγής δεδομένων και ακόμη σύνολα δεδομένων έτοιμα για AI.  

![εξαγωγή κειμένου από εικόνα χρησιμοποιώντας C# OCR](/images/extract-text-from-image-csharp.png "εξαγωγή κειμένου από εικόνα")

## Προαπαιτούμενα

- .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.8)  
- Visual Studio 2022 (η έκδοση Community είναι εντάξει)  
- Πακέτο NuGet `Aspose.OCR` (ή οποιαδήποτε βιβλιοθήκη που εκθέτει `OcrEngine`, `OcrResult`, κ.λπ.)  

Αν δεν έχετε εγκαταστήσει ακόμη το πακέτο, εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Αυτή η εντολή κατεβάζει όλα τα εγγενή δυαδικά αρχεία που χρειάζεστε για υψηλής απόδοσης OCR.

---

## Βήμα 1: Δημιουργία Παρουσίας Μηχανής OCR

Το πρώτο πράγμα που κάνετε είναι να εκκινήσετε τη μηχανή που θα κάνει το βάρος. Σκεφτείτε το `OcrEngine` ως τον εγκέφαλο πίσω από τη λειτουργία—μόλις είναι ζωντανό, μπορείτε να του δώσετε εικόνες και να ζητήσετε κείμενο.

```csharp
using Aspose.OCR;          // Namespace for OCR classes
using Aspose.OCR.Image;    // For ImageStream helper

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **Συμβουλή:** Κρατήστε τη μηχανή ως singleton αν επεξεργάζεστε πολλές εικόνες σε παρτίδα· επαναχρησιμοποιεί εσωτερικούς πόρους και επιταχύνει τη διαδικασία.

## Βήμα 2: Ενεργοποίηση Αυτόματης Προεπεξεργασίας

Οι πραγματικές σαρώσεις σπάνια είναι τέλειες. Έρχονται λοξά, θορυβώδεις ή με χαμηλή αντίθεση. Η ενεργοποίηση του `AutoPreprocess` λέει στη μηχανή να διορθώνει αυτόματα την κλίση, να αφαιρεί θόρυβο και να ρυθμίζει την αντίθεση πριν ακόμη κοιτάξει τους χαρακτήρες.

```csharp
// Step 2: Enable automatic preprocessing (deskew, denoise, contrast adjustment)
ocrEngine.Config.AutoPreprocess = true;
```

Γιατί είναι σημαντικό; Χωρίς προεπεξεργασία, η μηχανή OCR μπορεί να διαβάσει το “8” ως “B” ή να χάσει εντελώς μια γραμμή. Το αυτόματο βήμα σας σώζει από το να γράψετε προσαρμοσμένο κώδικα καθαρισμού εικόνας.

## Βήμα 3: Ορισμός Γλώσσας Αναγνώρισης

Οι περισσότερες βιβλιοθήκες OCR έρχονται με πακέτα γλωσσών. Εδώ ορίζουμε τα Αγγλικά, αλλά μπορείτε να αλλάξετε σε `OcrLanguage.French`, `OcrLanguage.Spanish`, κ.λπ., ανάλογα με το έγγραφό σας.

```csharp
// Step 3: Set the language for recognition
ocrEngine.Language = OcrLanguage.English;
```

Αν το σαρωμένο έγγραφο περιέχει μιξά γλώσσες, μπορείτε είτε να τρέξετε τη μηχανή δύο φορές είτε να χρησιμοποιήσετε ένα πολυγλωσσικό μοντέλο—κάτι που θα εξερευνήσετε αργότερα.

## Βήμα 4: Φόρτωση Εικόνας για OCR

Τώρα **φορτώνουμε εικόνα για OCR**. Η βοηθητική μέθοδος `ImageStream.FromFile` διαβάζει το αρχείο σε μορφή που καταλαβαίνει η μηχανή. Βεβαιωθείτε ότι η διαδρομή δείχνει σε πραγματικό αρχείο· οι σχετικές διαδρομές λειτουργούν όταν τρέχετε από το φάκελο του έργου.

```csharp
// Step 4: Load the image to be processed
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **Κοινό λάθος:** Χρήση διαδρομής με κενά χωρίς εισαγωγικά μπορεί να προκαλέσει `FileNotFoundException`. Πάντα ελέγχετε με `File.Exists` ότι το αρχείο υπάρχει πριν το περάσετε στη μηχανή.

## Βήμα 5: Εκτέλεση της Αναγνώρισης OCR

Με όλα ρυθμισμένα, τελικά **αναγνωρίζουμε το περιεχόμενο του σαρωμένου εγγράφου**. Η μέθοδος `Recognize` κάνει το βάρος και επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το εξαγόμενο κείμενο και τις βαθμολογίες εμπιστοσύνης.

```csharp
// Step 5: Perform OCR recognition
OcrResult ocrResult = ocrEngine.Recognize();
```

Αν χρειάζεστε το επίπεδο εμπιστοσύνης για κάθε γραμμή, μπορείτε να ελέγξετε το `ocrResult.Confidence` (float μεταξύ 0 και 1). Χαμηλή εμπιστοσύνη; Σκεφτείτε να ρυθμίσετε τις παραμέτρους προεπεξεργασίας ή να δώσετε εικόνα υψηλότερης ανάλυσης.

## Βήμα 6: Έξοδος του Αναγνωρισμένου Κειμένου

Ο πιο απλός τρόπος για να επαληθεύσετε την επιτυχία είναι να εκτυπώσετε το κείμενο στην κονσόλα. Σε πραγματική εφαρμογή πιθανότατα θα το γράψετε σε αρχείο, βάση δεδομένων ή θα το στείλετε σε άλλη υπηρεσία.

```csharp
// Step 6: Output the recognized text
Console.WriteLine(ocrResult.Text);
```

Η εκτέλεση του προγράμματος θα πρέπει να εμφανίσει κάτι σαν:

```
The quick brown fox jumps over the lazy dog.
```

Ακόμα κι αν η αρχική εικόνα ήταν ελαφρώς λοξά ή θορυβώδης, η αυτόματη προεπεξεργασία θα την έχει καθαρίσει αρκετά για καθαρό αποτέλεσμα.

---

## Πλήρης Πηγαίος Κώδικας – Ένα Παράδειγμα Έτοιμο για Εκτέλεση

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε σε ένα νέο έργο κονσόλας (`dotnet new console`). Περιλαμβάνει όλα τα παραπάνω βήματα, συν ένα μικρό κομμάτι διαχείρισης σφαλμάτων για να κάνει τον οδηγό πιο ανθεκτικό.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace ExtractTextFromImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Validate input argument
            if (args.Length == 0)
            {
                Console.WriteLine("Usage: dotnet run <image-path>");
                return;
            }

            string imagePath = args[0];

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found at '{imagePath}'");
                return;
            }

            try
            {
                // Step 1: Create OCR engine
                OcrEngine ocrEngine = new OcrEngine();

                // Step 2: Enable auto‑preprocess (deskew, denoise, contrast)
                ocrEngine.Config.AutoPreprocess = true;

                // Step 3: Choose language (English in this case)
                ocrEngine.Language = OcrLanguage.English;

                // Step 4: Load image for OCR
                ocrEngine.Image = ImageStream.FromFile(imagePath);

                // Step 5: Recognize scanned document
                OcrResult result = ocrEngine.Recognize();

                // Step 6: Output the extracted text
                Console.WriteLine("\n--- Extracted Text ---\n");
                Console.WriteLine(result.Text);
                Console.WriteLine("\n--- End of Output ---\n");

                // Optional: Show confidence if you need it
                Console.WriteLine($"Overall confidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Πώς να Εκτελέσετε

1. Αποθηκεύστε τον κώδικα ως `Program.cs` μέσα σε ένα νέο έργο κονσόλας.  
2. Ανοίξτε ένα τερματικό στη ρίζα του έργου.  
3. Εκτελέστε `dotnet add package Aspose.OCR` (αν δεν το έχετε κάνει ήδη).  
4. Κατασκευάστε και τρέξτε:  

   ```bash
   dotnet run "C:\Images\invoice_scanned.jpg"
   ```

Θα πρέπει να δείτε το εξαγόμενο κείμενο στην κονσόλα, μαζί με ένα συνολικό ποσοστό εμπιστοσύνης.

---

## Συχνές Ερωτήσεις (FAQs)

**Ε: Μπορώ να επεξεργαστώ PDF απευθείας;**  
Α: Ναι—οι περισσότερες βιβλιοθήκες OCR σας επιτρέπουν να φορτώσετε μια σελίδα PDF ως ροή εικόνας ή να χρησιμοποιήσετε ένα API `PdfDocument`. Μετατρέψτε κάθε σελίδα σε εικόνα πρώτα, μετά ακολουθήστε τα ίδια βήματα.

**Ε: Τι γίνεται αν η εικόνα μου είναι σε μορφή PNG;**  
Α: Η μέθοδος `ImageStream.FromFile` υποστηρίζει JPEG, PNG, BMP και TIFF από προεπιλογή. Δεν απαιτείται επιπλέον μετατροπή.

**Ε: Πώς βελτιώνω την ακρίβεια για χειρόγραφες σημειώσεις;**  
Α: Η χειρόγραφη γραφή είναι πιο δύσκολη. Αναζητήστε μια βιβλιοθήκη που προσφέρει μοντέλο “handwriting”, ή προεπεξεργαστείτε την εικόνα με δυαδικοποίηση και αφαίρεση θορύβου πριν τη δώσετε στη μηχανή.

**Ε: Υπάρχει τρόπος να εξάγω κείμενο από συγκεκριμένη περιοχή;**  
Α: Σίγουρα. Οι περισσότερες μηχανές εκθέτουν μια ιδιότητα `Rect` ή `Region` όπου μπορείτε να περιορίσετε το OCR σε ένα πλαίσιο—ιδανικό για φόρμες με σταθερά πεδία.

---

## Επόμενα Βήματα & Σχετικά Θέματα

Τώρα που έχετε κατακτήσει τα βασικά της **εξαγωγής κειμένου από εικόνα** με ένα **c# OCR tutorial**, σκεφτείτε να εξερευνήσετε:

- **Επεξεργασία παρτίδας** – βρόχος πάνω από έναν φάκελο εικόνων και εγγραφή κάθε αποτελέσματος σε αρχείο CSV.  
- **Δημιουργία PDF** – συνδυάστε το εξαγόμενο κείμενο με μια βιβλιοθήκη PDF για δημιουργία αναζητήσιμων PDF.  
- **Μετα‑επεξεργασία με μηχανική μάθηση** – χρησιμοποιήστε ελεγκτές ορθογραφίας ή μοντέλα γλώσσας για να καθαρίσετε τα σφάλματα OCR.  

Κάθε ένα από αυτά βασίζεται στις βασικές έννοιες που καλύψαμε: φόρτωση εικόνας για OCR, ρύθμιση της μηχανής και αναγνώριση σαρωμένου εγγράφου.

---

## Συμπέρασμα

Διανύσαμε έναν πλήρη, από‑αρχή‑μέχρι‑τέλος παράδειγμα που δείχνει πώς να **εξάγετε κείμενο από εικόνα** σε C#. Από τη δημιουργία του `OcrEngine` μέχρι την έξοδο του τελικού κειμένου, κάθε γραμμή κώδικα εξηγείται και είναι έτοιμη για εκτέλεση.  

Ακολουθώντας τα βήματα, θα μπορείτε να μετατρέψετε θορυβώδεις σαρώσεις, αποδείξεις ή χειρόγραφες σημειώσεις σε αναζητήσιμο, επεξεργάσιμο κείμενο σε δευτερόλεπτα. Συνεχίστε να πειραματίζεστε—προσαρμόστε τις σημαίες προεπεξεργασίας, αλλάξτε γλώσσες ή επεξεργαστείτε παρτίδες αρχείων. Ο κόσμος της αυτοματοποιημένης επεξεργασίας εγγράφων είναι δικός σας για εξερεύνηση.

Έχετε περισσότερες ερωτήσεις ή ένα ενδιαφέρον σενάριο χρήσης; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}