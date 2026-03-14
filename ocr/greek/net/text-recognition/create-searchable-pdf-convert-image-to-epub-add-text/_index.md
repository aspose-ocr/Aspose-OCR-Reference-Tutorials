---
category: general
date: 2026-03-13
description: Δημιουργήστε αναζητήσιμο PDF από οποιαδήποτε εικόνα χρησιμοποιώντας το
  Aspose OCR. Μάθετε πώς να μετατρέψετε την εικόνα σε EPUB, να προσθέσετε αναζητήσιμο
  κείμενο και να δημιουργήσετε αναζητήσιμο PDF σε C#.
draft: false
keywords:
- create searchable pdf
- convert image to epub
- ocr image to pdf
- add searchable text
- generate searchable pdf
language: el
og_description: Δημιουργήστε αναζητήσιμο PDF από οποιαδήποτε εικόνα χρησιμοποιώντας
  το Aspose OCR. Αυτός ο οδηγός δείχνει πώς να μετατρέψετε την εικόνα σε EPUB, να
  προσθέσετε αναζητήσιμο κείμενο και να δημιουργήσετε αναζητήσιμο PDF σε C#.
og_title: Δημιουργία PDF με δυνατότητα αναζήτησης – Μετατροπή εικόνας σε EPUB & Προσθήκη
  κειμένου
tags:
- Aspose OCR
- C#
- PDF
- EPUB
title: Δημιουργία Αναζητήσιμου PDF – Μετατροπή Εικόνας σε EPUB & Προσθήκη Κειμένου
url: /el/net/text-recognition/create-searchable-pdf-convert-image-to-epub-add-text/
---

.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF – Μετατροπή Εικόνας σε EPUB & Προσθήκη Κειμένου

Θέλετε να **δημιουργήσετε αναζητήσιμο PDF** από μια σαρωμένη απόδειξη ή οποιαδήποτε εικόνα; Σε αυτό το tutorial θα σας δείξουμε πώς να δημιουργήσετε αναζητήσιμο PDF χρησιμοποιώντας το Aspose OCR, ενώ ταυτόχρονα **μετατρέπετε την εικόνα σε EPUB** και **προσθέτετε στρώματα αναζητήσιμου κειμένου**—όλα σε ένα μόνο έργο C#.  

Αν έχετε αντιμετωπίσει ποτέ PDFs που φαίνονται ωραία αλλά δεν μπορούν να αναζητηθούν, δεν είστε μόνοι. Τα καλά νέα είναι ότι ένα κρυφό στρώμα κειμένου μπορεί να μετατρέψει μια επίπεδη εικόνα σε πλήρως αναζητήσιμο έγγραφο, και το Aspose το κάνει σχεδόν αβλαβές.

## Τι Θα Μάθετε

* Πώς να αρχικοποιήσετε τη μηχανή Aspose OCR και να ορίσετε τη γλώσσα.  
* Τα ακριβή βήματα για **μετατροπή εικόνας σε EPUB** για διανομή e‑book.  
* Πώς να διαμορφώσετε τον PDF writer ώστε η έξοδος να περιέχει ένα κρυφό, αναζητήσιμο στρώμα κειμένου.  
* Συμβουλές για τη διαχείριση ειδικών περιπτώσεων όπως αποδείξεις πολλαπλών σελίδων ή μη‑αγγλικές γλώσσες.  

Το μόνο που χρειάζεστε εκ των προτέρων είναι ένα .NET περιβάλλον ανάπτυξης (Visual Studio 2022 ή νεότερο) και ένα πακέτο Aspose OCR NuGet. Χωρίς εξωτερικές υπηρεσίες, χωρίς περίπλοκα αρχεία ρυθμίσεων—απλός C# κώδικας που μπορείτε να αντιγράψετε‑επικολλήσετε και να εκτελέσετε.

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντική |
|----------|-----------------------|
| .NET 6.0+ | Το Aspose OCR στοχεύει στο .NET Standard 2.0+, οπότε το .NET 6 προσφέρει τις τελευταίες βελτιώσεις runtime. |
| Πακέτο Aspose.OCR NuGet | Παρέχει τις κλάσεις `OcrEngine`, `EpubWriter` και `PdfWriter` που χρησιμοποιούνται στον κώδικα. |
| Αρχείο εικόνας (π.χ., `receipt.jpg`) | Η πηγή πάνω στην οποία θα τρέξετε OCR. Οποιαδήποτε raster εικόνα (PNG, JPEG, BMP) λειτουργεί. |
| Βασικές γνώσεις C# | Θα διαβάζετε και θα προσαρμόζετε αποσπάσματα κώδικα, όχι να μάθετε τη γλώσσα από το μηδέν. |

Μπορείτε να εγκαταστήσετε το πακέτο με την ακόλουθη εντολή:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Αν χρησιμοποιείτε Visual Studio, η διεπαφή του NuGet Package Manager κάνει το ίδιο—απλώς ψάξτε για “Aspose.OCR”.

## Βήμα 1 – Δημιουργία Αναζητήσιμου PDF με Aspose OCR

Το πρώτο που χρειάζεται είναι ένα αντικείμενο `OcrEngine` που ξέρει ποια γλώσσα θα αναγνωρίσει. Η αγγλική είναι η προεπιλογή, αλλά μπορείτε να την αλλάξετε σε γαλλικά, γερμανικά κ.λπ., ορίζοντας `ocrEngine.Language`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialise the OCR engine and set the language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English          // Change this if your document isn’t English
};
```

Γιατί να αρχικοποιήσετε τη μηχανή πρώτα; Η μηχανή κρατά το μοντέλο αναγνώρισης στη μνήμη, οπότε η δημιουργία της μία φορά και η επαναχρησιμοποίησή της σε πολλές εικόνες εξοικονομεί CPU και RAM. Σε μεγαλύτερες παρτίδες, θα κρατάτε το ίδιο αντικείμενο ζωντανό για όλη τη διάρκεια της εκτέλεσης.

## Βήμα 2 – Φόρτωση Εικόνας και Εκτέλεση OCR

Στη συνέχεια κατευθύνουμε τη μηχανή στο αρχείο που θέλουμε να επεξεργαστούμε. Η μέθοδος `ImageStream.FromFile` διαβάζει την εικόνα σε μορφή που καταλαβαίνει η μηχανή OCR.

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Run the recognition engine – this populates the internal text buffer
ocrEngine.Recognize();
```

> **Τι γίνεται αν η εικόνα είναι πολλαπλών σελίδων;**  
> Το Aspose OCR μπορεί να διαχειριστεί TIFF πολλαπλών σελίδων αμέσως. Απλώς περάστε τη διαδρομή του αρχείου TIFF· η μηχανή θα επεξεργαστεί αυτόματα κάθε σελίδα.

## Βήμα 3 – Μετατροπή Εικόνας σε EPUB

Αν χρειάζεστε επίσης μια έκδοση e‑book του σαρωμένου εγγράφου, το Aspose το κάνει με μία γραμμή κώδικα. Η `EpubWriter` χρησιμοποιεί το ίδιο αντικείμενο `OcrEngine`, πράγμα που σημαίνει ότι τα αποτελέσματα OCR επαναχρησιμοποιούνται χωρίς επιπλέον επεξεργασία.

```csharp
// Export the recognised content to an ePub file
EpubWriter epubWriter = new EpubWriter();
epubWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt.epub");
```

Γιατί εξαγωγή σε EPUB; Το EPUB είναι μορφή επαναρροής—ιδανική για κινητές συσκευές. Το κείμενο OCR γίνεται επιλέξιμο, ενώ η αρχική εικόνα παραμένει ως φόντο, διατηρώντας την εμφάνιση της αρχικής σάρωσης.

## Βήμα 4 – Προσθήκη Αναζητήσιμου Στρώματος Κειμένου στο PDF

Τώρα έρχεται το τμήμα που **δημιουργεί πραγματικά αναζητήσιμο PDF**. Ενεργοποιώντας το `AddSearchableTextLayer`, ο PDF writer ενσωματώνει ένα αόρατο στρώμα κειμένου που αντικατοπτρίζει την έξοδο OCR. Οι χρήστες μπορούν να αναζητήσουν, να αντιγράψουν ή να επισημάνουν κείμενο όπως σε ένα φυσικό PDF.

```csharp
// Configure PDF writer to include a hidden searchable text layer
PdfWriter pdfWriter = new PdfWriter
{
    AddSearchableTextLayer = true   // Enables the hidden text layer for searchability
};

// Save the OCR result as a searchable PDF
pdfWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt_searchable.pdf");
```

> **Κοινό λάθος:** Η παράλειψη του `AddSearchableTextLayer` οδηγεί σε PDF που φαίνεται ίδιο αλλά δεν περιέχει αναζητήσιμο κείμενο. Ελέγχετε πάντα αυτή τη σημαία όταν χρειάζεστε αναζητήσιμο έγγραφο.

## Βήμα 5 – Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι μια αυτόνομη εφαρμογή κονσόλας που μπορείτε να τοποθετήσετε σε ένα νέο .NET project και να τρέξετε αμέσως.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace OcrToPdfAndEpub
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the source image
            string imagePath = "YOUR_DIRECTORY/receipt.jpg";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            ocrEngine.Recognize();

            // 4️⃣ Convert to EPUB (optional but handy)
            EpubWriter epubWriter = new EpubWriter();
            string epubPath = "YOUR_DIRECTORY/receipt.epub";
            epubWriter.Save(ocrEngine, epubPath);
            Console.WriteLine($"EPUB saved to {epubPath}");

            // 5️⃣ Create searchable PDF
            PdfWriter pdfWriter = new PdfWriter
            {
                AddSearchableTextLayer = true
            };
            string pdfPath = "YOUR_DIRECTORY/receipt_searchable.pdf";
            pdfWriter.Save(ocrEngine, pdfPath);
            Console.WriteLine($"Searchable PDF saved to {pdfPath}");
        }
    }
}
```

### Αναμενόμενη Έξοδος

* `receipt.epub` – ένα αρχείο EPUB που μπορείτε να ανοίξετε στο Calibre, Apple Books ή οποιονδήποτε e‑reader.  
* `receipt_searchable.pdf` – ένα PDF όπου μπορείτε να πατήσετε **Ctrl + F** και να βρείτε οποιαδήποτε λέξη εμφανίστηκε στην αρχική εικόνα.

Αν ανοίξετε το PDF στο Adobe Acrobat και δείτε **File → Properties → Description**, θα δείτε ένα κρυφό ρεύμα κειμένου στην καρτέλα **Fonts**, επιβεβαιώνοντας ότι το αναζητήσιμο στρώμα υπάρχει.

## Συχνές Ερωτήσεις & Ειδικές Περιπτώσεις

**Ε: Λειτουργεί αυτό με μη‑αγγλικές γλώσσες;**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}