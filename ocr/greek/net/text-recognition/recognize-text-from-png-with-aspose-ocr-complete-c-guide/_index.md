---
category: general
date: 2026-05-28
description: Αναγνώριση κειμένου από PNG χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να εξάγετε κείμενο από σαρωμένες σελίδες και να εκτελείτε OCR σε εικόνες αποδοτικά.
draft: false
keywords:
- recognize text from png
- extract text from scanned pages
- perform ocr on images
- Aspose OCR C#
- OCR image processing
language: el
og_description: Αναγνώριση κειμένου από PNG χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να εξάγετε κείμενο από σαρωμένες σελίδες και να εκτελείτε OCR σε εικόνες σε
  λίγα λεπτά.
og_title: Αναγνώριση κειμένου από PNG με το Aspose OCR – Πλήρης Οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: recognize text from png using Aspose OCR in C#. Learn how to extract
    text from scanned pages and perform OCR on images efficiently.
  headline: recognize text from png with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: recognize text from png using Aspose OCR in C#. Learn how to extract
    text from scanned pages and perform OCR on images efficiently.
  name: recognize text from png with Aspose OCR – Complete C# Guide
  steps:
  - name: '**Engine initialization** – The `OcrEngine` class is the entry point; it
      holds all configuration and state.'
    text: '**Engine initialization** – The `OcrEngine` class is the entry point; it
      holds all configuration and state.'
  - name: '**Evaluation‑mode guard** – If you’re using a trial license, Aspose caps
      the number of pages you can process. Setting `MaxPagesInEvaluation` prevents
      the library from throwing a *LicenseException* halfway through.'
    text: '**Evaluation‑mode guard** – If you’re using a trial license, Aspose caps
      the number of pages you can process. Setting `MaxPagesInEvaluation` prevents
      the library from throwing a *LicenseException* halfway through.'
  - name: '**Image loading** – `ImageStream.FromFile` abstracts away the `System.Drawing`
      dependency, letting you feed any supported format (PNG, JPEG, BMP) directly.'
    text: '**Image loading** – `ImageStream.FromFile` abstracts away the `System.Drawing`
      dependency, letting you feed any supported format (PNG, JPEG, BMP) directly.'
  - name: '**Recognition loop** – By iterating, you can **perform OCR on images**
      in bulk, which is exactly what most real‑world scanning pipelines need.'
    text: '**Recognition loop** – By iterating, you can **perform OCR on images**
      in bulk, which is exactly what most real‑world scanning pipelines need.'
  - name: '**Disposal** – The engine holds unmanaged resources; disposing releases
      memory promptly, especially important when processing many high‑resolution PNGs.'
    text: '**Disposal** – The engine holds unmanaged resources; disposing releases
      memory promptly, especially important when processing many high‑resolution PNGs.'
  - name: Install the NuGet package.
    text: Install the NuGet package.
  - name: Initialise `OcrEngine`.
    text: Initialise `OcrEngine`.
  - name: (Optional) Set a page limit for evaluation mode.
    text: (Optional) Set a page limit for evaluation mode.
  - name: Load each PNG with `ImageStream.FromFile`.
    text: Load each PNG with `ImageStream.FromFile`.
  - name: Call `Recognize()` and output the result.
    text: Call `Recognize()` and output the result.
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: Αναγνώριση κειμένου από PNG με το Aspose OCR – Πλήρης Οδηγός C#
url: /el/net/text-recognition/recognize-text-from-png-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από PNG με Aspose OCR – Πλήρης Οδηγός C#

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε κείμενο από png** αρχεία σε μια εφαρμογή .NET; Με το Aspose OCR μπορείτε γρήγορα να **εξάγετε κείμενο από σαρωμένες σελίδες** και **εκτελέσετε OCR σε εικόνες** χωρίς να ασχοληθείτε με χαμηλού επιπέδου επεξεργασία εικόνας. Σε αυτό το σεμινάριο θα περάσουμε από ένα έτοιμο προς εκτέλεση παράδειγμα C#, θα εξηγήσουμε γιατί κάθε γραμμή είναι σημαντική και θα σας δείξουμε πώς να το προσαρμόσετε σε πραγματικά έργα.

Αν αναρωτιέστε αν λειτουργεί σε σαρώσεις πολλαπλών σελίδων, αν μπορείτε να περιορίσετε τη λειτουργία αξιολόγησης ή πώς να διαχειριστείτε τεράστια αρχεία εικόνας—μείνετε συντονισμένοι. Στο τέλος θα έχετε ένα σταθερό, έτοιμο για παραγωγή απόσπασμα κώδικα που μπορείτε να αντιγράψετε‑επικολλήσετε στη δική σας λύση.

---

## Τι Θα Χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα παρακάτω:

| Prerequisite | Why it matters |
|--------------|----------------|
| **.NET 6.0 or later** (or .NET Framework 4.6+) | Το Aspose.OCR στοχεύει σε σύγχρονα runtime και παρέχει τις τελευταίες βελτιώσεις απόδοσης. |
| **Visual Studio 2022** (or any IDE you like) | Ένας άνετος επεξεργαστής καθιστά πιο εύκολη τη δοκιμή του κώδικα. |
| **Aspose.OCR NuGet package** | Αυτή είναι η βιβλιοθήκη που πραγματικά κάνει τη βαριά δουλειά. |
| A folder with a handful of **PNG images** you want to read | Το σεμινάριο υποθέτει αρχεία με ονόματα `page1.png`, `page2.png`, … |

Αν κάποιο από αυτά σας είναι άγνωστο, απλώς εγκαταστήστε το πακέτο NuGet και δημιουργήστε ένα απλό έργο κονσόλας—χωρίς επιπλέον ρυθμίσεις.

---

## Βήμα 1: Εγκατάσταση Aspose.OCR μέσω NuGet

Ανοίξτε το τερματικό σας (ή το Package Manager Console) και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Ή, αν προτιμάτε το UI, κάντε δεξί κλικ στο **Dependencies → Manage NuGet Packages**, αναζητήστε το *Aspose.OCR* και κάντε κλικ στο **Install**. Αυτό θα φέρει όλα όσα χρειάζεστε, συμπεριλαμβανομένης της βοηθητικής κλάσης `ImageStream` που χρησιμοποιείται αργότερα.

> **Συμβουλή:** Χρησιμοποιήστε την πιο πρόσφατη σταθερή έκδοση (ως Μάιος 2026 είναι η 23.10). Οι νέες εκδόσεις συχνά περιλαμβάνουν διορθώσεις σφαλμάτων για δύσκολες μορφές εικόνας.

---

## Βήμα 2: Δημιουργία Ελάχιστης Εφαρμογής Κονσόλας

Δημιουργήστε ένα νέο έργο κονσόλας αν δεν το έχετε κάνει ήδη:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Αντικαταστήστε το περιεχόμενο του `Program.cs` με το πλήρες παράδειγμα παρακάτω. Παρατηρήστε πώς διατηρούμε τον κώδικα **αυτο‑συνεπή**—χωρίς εξωτερικά αρχεία ρυθμίσεων, χωρίς κρυφή μαγεία.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine
            // -------------------------------------------------
            var engine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣  Optional: limit pages when running in evaluation mode
            // -------------------------------------------------
            // Evaluation licenses only allow a few pages; set this to avoid runtime errors.
            engine.Configuration.MaxPagesInEvaluation = 5;

            // -------------------------------------------------
            // 3️⃣  Define where your PNG files live
            // -------------------------------------------------
            string basePath = @"YOUR_DIRECTORY"; // <-- change this to your real folder

            // -------------------------------------------------
            // 4️⃣  Loop through the images you want to process
            // -------------------------------------------------
            for (int i = 0; i < 5; i++) // adjust the loop count to match your file count
            {
                // Load the current page image
                engine.Image = ImageStream.FromFile($"{basePath}/page{i + 1}.png");

                // -------------------------------------------------
                // 5️⃣  Perform OCR and display the result
                // -------------------------------------------------
                Console.WriteLine($"--- Page {i + 1} ---");
                string recognizedText = engine.Recognize();

                // Show the extracted text; you could also write it to a file.
                Console.WriteLine(recognizedText);
                Console.WriteLine(); // blank line for readability
            }

            // -------------------------------------------------
            // 6️⃣  Clean up (optional but good practice)
            // -------------------------------------------------
            engine.Dispose();
        }
    }
}
```

### Γιατί Λειτουργεί Αυτή η Δομή

1. **Engine initialization** – Η κλάση `OcrEngine` είναι το σημείο εισόδου· διατηρεί όλες τις ρυθμίσεις και την κατάσταση.  
2. **Evaluation‑mode guard** – Αν χρησιμοποιείτε δοκιμαστική άδεια, το Aspose περιορίζει τον αριθμό των σελίδων που μπορείτε να επεξεργαστείτε. Ορίζοντας `MaxPagesInEvaluation` αποτρέπει τη βιβλιοθήκη από το να ρίξει *LicenseException* στα μισά.  
3. **Image loading** – Η μέθοδος `ImageStream.FromFile` αφαιρεί την εξάρτηση από το `System.Drawing`, επιτρέποντάς σας να τροφοδοτήσετε άμεσα οποιαδήποτε υποστηριζόμενη μορφή (PNG, JPEG, BMP).  
4. **Recognition loop** – Με την επανάληψη, μπορείτε να **εκτελέσετε OCR σε εικόνες** μαζικά, κάτι που είναι ακριβώς αυτό που χρειάζονται οι περισσότερες πραγματικές γραμμές σάρωσης.  
5. **Disposal** – Η μηχανή διατηρεί μη διαχειριζόμενους πόρους· η απελευθέρωση (dispose) απελευθερώνει τη μνήμη άμεσα, κάτι ιδιαίτερα σημαντικό όταν επεξεργάζεστε πολλές PNG υψηλής ανάλυσης.

---

## Βήμα 3: Εκτέλεση της Εφαρμογής και Επαλήθευση του Αποτελέσματος

Δομήστε (build) και εκτελέστε:

```bash
dotnet run
```

Υποθέτοντας ότι τοποθετήσατε πέντε αρχεία PNG με ονόματα `page1.png` … `page5.png` στο φάκελο που καθορίσατε, θα πρέπει να δείτε κάτι όπως:

```
--- Page 1 ---
Invoice #12345
Date: 2026-05-01
Total: $1,250.00

--- Page 2 ---
Thank you for your purchase!
...

```

Αν λάβετε μια κενή συμβολοσειρά, ελέγξτε ξανά ότι οι εικόνες περιέχουν **αναγνώσιμο κείμενο** (καλό αντίθεση, όχι φωτογραφία θολής πινακίδας). Το Aspose OCR λειτουργεί καλύτερα με σαρώσεις υψηλής ποιότητας—σκεφτείτε 300 dpi ή περισσότερο.

> **Image example**  
> ![παράδειγμα εξόδου αναγνώρισης κειμένου από png](https://example.com/ocr-output.png "αναγνώριση κειμένου από png – έξοδος κονσόλας")

---

## Βήμα 4: Συνηθισμένα Προβλήματα Κατά την **εξαγωγή κειμένου από σαρωμένες σελίδες**

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Κενή έξοδος | Η εικόνα έχει χαμηλή αντίθεση ή είναι θορυβώδης | Προεπεξεργασία με Aspose.Imaging (δυαδικοποίηση, διόρθωση κλίσης). |
| Παραμορφωμένοι χαρακτήρες | Η γλώσσα δεν έχει οριστεί (η προεπιλογή είναι Αγγλικά) | `engine.Configuration.Language = Language.English;` ή ορίστε σε `Language.French`, κλπ. |
| Exception *“File not found”* | Λάθος διαδρομή φακέλου ή λείπει η επέκταση αρχείου | Χρησιμοποιήστε `Path.Combine(basePath, $"page{i+1}.png")` για ασφάλεια. |
| Σφάλμα άδειας μετά από λίγες σελίδες | Χρήση δοκιμαστικής άδειας χωρίς `MaxPagesInEvaluation` | Αγοράστε άδεια ή διατηρήστε τη γραμμή `MaxPagesInEvaluation`. |

Αυτές οι συμβουλές διατηρούν την ροή εργασίας **εξαγωγής κειμένου από σαρωμένες σελίδες** ομαλή, ακόμη και όταν το υλικό προέλευσης δεν είναι τέλειο.

---

## Βήμα 5: Προχωρημένα – Κλιμάκωση σε Εκατοντάδες Εικόνες

Αν χρειάζεστε να **εκτελέσετε OCR σε εικόνες** αποθηκευμένες σε βάση δεδομένων ή σε cloud bucket, αντικαταστήστε το βρόχο `for` με ένα `foreach` πάνω από μια συλλογή διαδρομών αρχείων:

```csharp
string[] pngFiles = Directory.GetFiles(basePath, "*.png");
foreach (var file in pngFiles)
{
    engine.Image = ImageStream.FromFile(file);
    Console.WriteLine($"--- {Path.GetFileName(file)} ---");
    Console.WriteLine(engine.Recognize());
}
```

Μπορείτε επίσης να ενεργοποιήσετε **πολλαπλή νηματοποίηση** (Aspose OCR είναι thread‑safe) για να επιταχύνετε την επεξεργασία σε πολυπύρηνες μηχανές:

```csharp
Parallel.ForEach(pngFiles, file =>
{
    var localEngine = new OcrEngine(); // each thread gets its own engine
    localEngine.Image = ImageStream.FromFile(file);
    string text = localEngine.Recognize();
    lock (Console.Out) // avoid garbled console output
    {
        Console.WriteLine($"--- {Path.GetFileName(file)} ---");
        Console.WriteLine(text);
    }
    localEngine.Dispose();
});
```

Θυμηθείτε να απελευθερώνετε (dispose) κάθε instance της μηχανής· διαφορετικά θα διαρρεύσει η εγγενής μνήμη.

---

## Βήμα 6: Πέρα από PNG – Άλλες Μορφές και PDF

Το Aspose OCR δεν περιορίζεται στα PNG. Μπορείτε να τροφοδοτήσετε JPEG, BMP, TIFF ή ακόμη και **σελίδες PDF** (μετατρέποντάς τες πρώτα σε εικόνες). Για PDF, συνδυάστε Aspose.PDF και Aspose.OCR:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Devices;

// Load PDF, render each page to a PNG stream, then OCR
Document pdf = new Document("sample.pdf");
for (int pageNum = 1; pageNum <= pdf.Pages.Count; pageNum++)
{
    using var imgStream = new MemoryStream();
    var rasterizer = new PngDevice();
    rasterizer.Process(pdf.Pages[pageNum], imgStream);
    imgStream.Position = 0;

    engine.Image = ImageStream.FromStream(imgStream);
    Console.WriteLine($"--- PDF Page {pageNum} ---");
    Console.WriteLine(engine.Recognize());
}
```

Αυτό το απόσπασμα δείχνει πώς μπορείτε να **εξάγετε κείμενο από σαρωμένες σελίδες** που έρχονται ως PDF—ένα κοινό σενάριο σε pipelines επεξεργασίας τιμολογίων.

---

## Ανασκόπηση & Επόμενα Βήματα

Καλύψαμε ολόκληρο τον κύκλο ζωής της **αναγνώρισης κειμένου από png** χρησιμοποιώντας Aspose OCR:

1. Εγκαταστήστε το πακέτο NuGet.  
2. Αρχικοποιήστε το `OcrEngine`.  
3. (Προαιρετικά) Ορίστε όριο σελίδων για τη λειτουργία αξιολόγησης.  
4. Φορτώστε κάθε PNG με `ImageStream.FromFile`.  
5. Καλέστε το `Recognize()` και εμφανίστε το αποτέλεσμα.

## Related Tutorials

- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Εξαγωγή κειμένου από εικόνα – Αναγνώριση γραμμής με Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)
- [Εξαγωγή κειμένου από εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}