---
category: general
date: 2026-03-18
description: Πώς να κάνετε OCR PDF σε C# – μάθετε να μετατρέπετε σαρωμένα PDF, να
  δημιουργείτε PDF με δυνατότητα αναζήτησης, να προσθέτετε υδατογράφημα σε PDF και
  να εξάγετε κείμενο από PDF με μια απλή ροή εργασίας OcrEngine.
draft: false
keywords:
- how to ocr pdf
- convert scanned pdf
- create searchable pdf
- add watermark pdf
- extract text from pdf
language: el
og_description: Πώς να κάνετε OCR σε PDF με C#; Αυτός ο οδηγός σας δείχνει πώς να
  μετατρέψετε σαρωμένο PDF, να δημιουργήσετε PDF με δυνατότητα αναζήτησης, να προσθέσετε
  υδατογράφημα σε PDF και να εξάγετε κείμενο από PDF χρησιμοποιώντας το OcrEngine.
og_title: Πώς να κάνετε OCR PDF σε C# – Γρήγορος και Πλήρης Οδηγός
tags:
- OCR
- PDF
- C#
- Document Processing
title: Πώς να κάνετε OCR PDF σε C# – Μετατροπή σαρωμένων PDF
url: /el/python-java/general/how-to-ocr-pdf-in-c-convert-scanned-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε OCR PDF σε C# – Μετατροπή Σαρωμένων PDF

Έχετε ποτέ χρειαστεί να **how to OCR PDF** αλλά να κολλήσετε σε ένα σαρωμένο αρχείο που δεν συνεργάζεται; Δεν είστε οι μόνοι. Σε πολλά πραγματικά έργα—σκεφτείτε την ψηφιοποίηση τιμολογίων ή την αρχειοθέτηση ιστορικών αναφορών—τέλος πάντων έχετε ένα σωρό εικόνων μέσα σε ένα PDF, και ο μόνος τρόπος να τα κάνετε αναζητήσιμα είναι να τρέξετε OCR πάνω τους.  

Τα καλά νέα; Με μερικές μόνο γραμμές C# μπορείτε να **convert scanned PDF** σε ένα **create searchable PDF**, να προσθέσετε ένα διακριτικό υδατογράφημα, και ακόμη να εξάγετε το ακατέργαστο κείμενο για περαιτέρω επεξεργασία. Παρακάτω θα δείτε ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που κάνει ακριβώς αυτό.

## Τι καλύπτει αυτό το tutorial

* Πώς να **how to OCR PDF** χρησιμοποιώντας την κλάση `OcrEngine`.  
* Μετατροπή ενός σαρωμένου PDF σε **create searchable PDF**.  
* Προσθήκη υδατογραφήματος στην πρώτη σελίδα (**add watermark pdf**).  
* Ανάκτηση αλφαριθμητικών συμβολοσειρών από το αποτέλεσμα (**extract text from pdf**).  
* Συνηθισμένα προβλήματα—όπως η διαχείριση εγγράφων πολλαπλών σελίδων ή η αντιμετώπιση σαρωμάτων χαμηλής ανάλυσης.

Χωρίς εξωτερικούς συνδέσμους τεκμηρίωσης, χωρίς ημιτελή αποσπάσματα. Ό,τι χρειάζεστε είναι εδώ.

## Προαπαιτούμενα

* .NET 6.0 ή νεότερο (ο κώδικας μεταγλωττίζεται και με .NET 5).  
* Μια αναφορά στη βιβλιοθήκη OCR που παρέχει `OcrEngine` και `ImageFormats` (π.χ., `Aspose.OCR` ή παρόμοιο πακέτο).  
* Ένα αρχείο PDF εισόδου με όνομα `input.pdf` τοποθετημένο σε φάκελο που ελέγχετε.  
* Βασική εξοικείωση με εφαρμογές κονσόλας C#.

Αν τα έχετε ήδη, υπέροχα—ας προχωρήσουμε.

## Βήμα 1: Ρύθμιση του έργου και εισαγωγή εξαρτήσεων

Δημιουργήστε ένα νέο έργο κονσόλας και προσθέστε το πακέτο OCR μέσω NuGet:

```bash
dotnet new console -n OcrPdfDemo
cd OcrPdfDemo
dotnet add package Aspose.OCR
```

Τώρα ανοίξτε το `Program.cs`. Στην κορυφή, εισάγετε τα namespaces που θα χρειαστείτε:

```csharp
using System;
using Aspose.OCR;          // OcrEngine lives here
using Aspose.OCR.Image;   // ImageFormats enum
```

*Γιατί είναι σημαντικό*: Η εισαγωγή των σωστών namespaces επιτρέπει στον μεταγλωττιστή να εντοπίσει το `OcrEngine`. Η παράλειψη αυτού του βήματος θα προκαλέσει σφάλμα `CS0246` και θα διακόψει τη δημιουργία.

## Βήμα 2: Αρχικοποίηση της μηχανής OCR

Η μηχανή είναι η καρδιά της διαδικασίας. Την δημιουργείτε μία φορά και την επαναχρησιμοποιείτε για κάθε σελίδα.

```csharp
// Step 2: Initialize the OCR engine
OcrEngine engine = new OcrEngine();
```

*Συμβουλή*: Αν σκοπεύετε να επεξεργαστείτε πολλά PDF διαδοχικά, σκεφτείτε να επαναχρησιμοποιήσετε την ίδια παρουσία `engine` για να αποφύγετε επαναλαμβανόμενους ελέγχους άδειας.

## Βήμα 3: Φόρτωση του πηγαίου PDF

Ενημερώστε τη μηχανή ποιο αρχείο θα επεξεργαστεί. Η μέθοδος `SetImageFromFile` δέχεται οποιαδήποτε πηγή εικόνας‑ή‑PDF.

```csharp
// Step 3: Load the scanned PDF you want to OCR
engine.SetImageFromFile(@"YOUR_DIRECTORY\input.pdf");
```

> **Γιατί αυτό το βήμα είναι κρίσιμο** – Η μηχανή χρειάζεται μια bitmap αναπαράσταση κάθε σελίδας. Όταν της δίνετε ένα PDF, εσωτερικά rasterizes κάθε σελίδα με βάση το προεπιλεγμένο DPI (συνήθως 300). Αν το πηγαίο PDF είναι ήδη κειμενικό, η μηχανή θα το περάσει απλά αμετάβλητο, εξοικονομώντας χρόνο.

## Βήμα 4: Εκτέλεση της αναγνώρισης OCR

Τώρα γίνεται η βαριά δουλειά. Η μέθοδος `Recognize` σαρώει κάθε σελίδα, εξάγει γλύφους και δημιουργεί ένα αναζητήσιμο στρώμα.

```csharp
// Step 4: Perform OCR on the loaded document
engine.Recognize();
```

*Συχνή ερώτηση*: *Τι γίνεται αν το PDF έχει 50 σελίδες;*  
Η `Recognize` επεξεργάζεται ολόκληρο το έγγραφο εξ ορισμού. Για περιβάλλοντα με περιορισμένη μνήμη μπορείτε να ορίσετε `engine.PageIndex` και `engine.PageCount` για επεξεργασία σελίδα‑με‑σελίδα.

## Βήμα 5: Αποθήκευση του αναζητήσιμου PDF (Υδατογράφημα στη Σελίδα 1)

Θα αποθηκεύσουμε το αποτέλεσμα ως PDF. Η πρώτη σελίδα θα λάβει αυτόματα ένα υδατογράφημα επειδή η βιβλιοθήκη OCR προσθέτει προεπιλεγμένα μια επικάλυψη «Generated by Aspose.OCR». Αν χρειάζεστε προσαρμοσμένο υδατογράφημα, μπορείτε να τροποποιήσετε την ιδιότητα `engine.Watermark` πριν την αποθήκευση.

```csharp
// Step 5: Save the OCR‑processed PDF with a watermark on page 1
engine.Save(@"YOUR_DIRECTORY\output.pdf", ImageFormats.Pdf);
```

Μετά από αυτήν την κλήση θα έχετε ένα **create searchable PDF** όπου μπορείτε να επιλέξετε, να αντιγράψετε και να αναζητήσετε το κείμενο όπως σε οποιοδήποτε εγγενές PDF.

## Βήμα 6: Εξαγωγή απλού κειμένου (Προαιρετικό αλλά χρήσιμο)

Αν θέλετε επίσης να **extract text from pdf** για ευρετηρίαση ή περαιτέρω ανάλυση, η μηχανή σας δίνει πρόσβαση στην ακατέργαστη συμβολοσειρά.

```csharp
// Step 6: Pull the recognized text into a string
string extractedText = engine.Text;
Console.WriteLine("=== Extracted Text Start ===");
Console.WriteLine(extractedText);
Console.WriteLine("=== Extracted Text End ===");
```

Η ιδιότητα `engine.Text` συνενώνει το κείμενο όλων των σελίδων, διατηρώντας τις αλλαγές γραμμής. Μπορείτε να το διαχωρίσετε με `\f` (form feed) αν χρειάζεστε λεπτομέρεια ανά σελίδα.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το πλήρες πρόγραμμα. Αντιγράψτε‑και‑επικολλήστε το στο `Program.cs`, αντικαταστήστε το `YOUR_DIRECTORY` με απόλυτη ή σχετική διαδρομή, και τρέξτε `dotnet run`.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine
            OcrEngine engine = new OcrEngine();

            // 2️⃣ Load the source PDF to be processed
            // Make sure the file exists; otherwise you'll get a FileNotFoundException.
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            engine.SetImageFromFile(inputPath);

            // 3️⃣ Perform OCR recognition on the loaded document
            engine.Recognize();

            // 4️⃣ Save the recognized document as a PDF (watermark appears on page 1)
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            engine.Save(outputPath, ImageFormats.Pdf);

            // 5️⃣ (Optional) Extract plain text for further use
            string extractedText = engine.Text;
            Console.WriteLine("=== Extracted Text Start ===");
            Console.WriteLine(extractedText);
            Console.WriteLine("=== Extracted Text End ===");

            Console.WriteLine($"OCR complete! Searchable PDF saved to: {outputPath}");
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Η εκτέλεση του προγράμματος εκτυπώνει το εξαγόμενο κείμενο στην κονσόλα και δημιουργεί το `output.pdf`. Ανοίξτε το PDF σε οποιονδήποτε προβολέα (Adobe Acrobat, Edge, κ.λπ.) και δοκιμάστε να αναζητήσετε μια λέξη που εμφανίστηκε στην αρχική σάρωση—θα δείτε ότι είναι πλέον αναζητήσιμο. Η πρώτη σελίδα εμφανίζει το προεπιλεγμένο υδατογράφημα, επιβεβαιώνοντας ότι το βήμα **add watermark pdf** ολοκληρώθηκε.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Question | Answer |
|----------|--------|
| **Τι γίνεται αν η σάρωση είναι χαμηλής ανάλυσης;** | Αυξήστε το DPI πριν την αναγνώριση: `engine.ImageInfo.DpiX = engine.ImageInfo.DpiY = 600;` Αυτό παρέχει στη μηχανή OCR περισσότερες λεπτομέρειες για επεξεργασία. |
| **Μπορώ να επιλέξω προσαρμοσμένο υδατογράφημα;** | Ναι. Ορίστε `engine.Watermark = "Confidential – Processed on " + DateTime.Now.ToShortDateString();` πριν το `Save`. |
| **Πώς να διαχειριστώ PDF με κωδικό πρόσβασης;** | Χρησιμοποιήστε `engine.LoadPassword = "yourPassword";` πριν το `SetImageFromFile`. |
| **Υπάρχει τρόπος να περιορίσω το OCR σε συγκεκριμένες σελίδες;** | Ορίστε `engine.PageIndex = 2;` και `engine.PageCount = 5;` για να επεξεργαστείτε μόνο τις σελίδες 3‑7. |
| **Τι γίνεται αν χρειάζεται να διατηρήσω τις αρχικές εικόνες ανέπαφες;** | Μετά το OCR μπορείτε να συγχωνεύσετε το αρχικό PDF με το στρώμα OCR χρησιμοποιώντας μια βιβλιοθήκη PDF (π.χ., `Aspose.PDF`) για να διατηρήσετε την πιστότητα των εικόνων. |

## Συμβουλές & Καλές Πρακτικές

* **Συμβουλή:** Εκτελέστε το OCR σε νήμα παρασκηνίου αν το ενσωματώνετε σε εφαρμογή UI—διαφορετικά η διεπαφή θα παγώσει.  
* **Προσοχή:** PDF με μεικτό raster και vector περιεχόμενο. Η μηχανή θα κάνει OCR μόνο στις raster σελίδες· το κείμενο vector παραμένει αυτόματα επιλέξιμο.  
* **Βελτίωση απόδοσης:** Κρατήστε στην μνήμη τα δεδομένα γλώσσας OCR (`engine.Language = OcrLanguage.English;`) για να αποφύγετε την επαναφόρτωση για κάθε έγγραφο.

## Συμπέρασμα

Τώρα έχετε μια πλήρη, ολοκληρωμένη λύση για **how to OCR PDF** σε C#. Αρχικοποιώντας το `OcrEngine`, φορτώνοντας ένα σαρωμένο αρχείο, αναγνωρίζοντας το κείμενο, αποθηκεύοντας ένα **create searchable pdf**, προσθέτοντας υδατογράφημα, και προαιρετικά **extracting text from pdf**, μπορείτε να μετατρέψετε οποιοδήποτε PDF βασισμένο σε εικόνα σε ένα αναζητήσιμο, ευρετηρίσιμο περιουσιακό στοιχείο.

Επόμενα βήματα; Δοκιμάστε να συνδέσετε αυτή τη ροή εργασίας με ένα σύστημα διαχείρισης εγγράφων, ή πειραματιστείτε με διαφορετικές γλώσσες (`engine.Language = OcrLanguage.French;`). Μπορείτε επίσης να εξερευνήσετε την επεξεργασία πολλαπλών αρχείων σε φάκελο—απλώς επαναλάβετε τα βήματα με μια νέα παρουσία `engine` κάθε φορά.

Καλή προγραμματιστική δουλειά, και εύχομαι τα PDF σας να είναι πάντα αναζητήσιμα! 

![Παράδειγμα OCR PDF που δείχνει αρχεία εισόδου και εξόδου](https://example.com/ocr-pdf-demo.png "πώς να κάνετε OCR PDF")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}