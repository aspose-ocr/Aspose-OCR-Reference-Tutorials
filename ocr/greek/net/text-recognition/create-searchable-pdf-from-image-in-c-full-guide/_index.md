---
category: general
date: 2026-03-21
description: Δημιουργήστε αναζητήσιμο PDF από σαρωμένες εικόνες σε C#. Μάθετε πώς
  να μετατρέψετε εικόνα σε PDF, να εξάγετε κείμενο από τη σάρωση και να εκτελέσετε
  OCR στην εικόνα χρησιμοποιώντας το Aspose OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from scan
- convert scanned document
- perform ocr on image
language: el
og_description: Δημιουργήστε αναζητήσιμο PDF από σαρωμένες εικόνες σε C#. Μάθετε βήμα‑βήμα
  πώς να μετατρέψετε την εικόνα σε PDF, να εξάγετε κείμενο από τη σάρωση και να εκτελέσετε
  OCR στην εικόνα.
og_title: Δημιουργία Αναζητήσιμου PDF από Εικόνα σε C# – Πλήρης Οδηγός
tags:
- OCR
- C#
- PDF
- Aspose
title: Δημιουργία Αναζητήσιμου PDF από Εικόνα σε C# – Πλήρης Οδηγός
url: /el/net/text-recognition/create-searchable-pdf-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF από Εικόνα σε C# – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **δημιουργήσετε αναζητήσιμο PDF** από μια σειρά σαρωμένων εικόνων; Δεν είστε μόνοι—νομικές ομάδες, λογιστές και προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν προσπαθούν να μετατρέψουν τα έντυπα συμβόλαια σε κάτι που μπορείτε να ψάξετε με Ctrl‑F.  

Σε αυτό το σεμινάριο, θα μάθετε πώς να **μετατρέψετε εικόνα σε PDF**, **εξάγετε κείμενο από σάρωση**, και **εκτελέσετε OCR σε εικόνα** χρησιμοποιώντας τη βιβλιοθήκη Aspose OCR. Στο τέλος, θα έχετε ένα έτοιμο προς χρήση απόσπασμα κώδικα C# που δημιουργεί ένα αναζητήσιμο PDF με λίγες μόνο γραμμές κώδικα.

## Τι Καλύπτει Αυτός ο Οδηγός

* Ρύθμιση του πακέτου NuGet Aspose OCR.  
* Φόρτωση μιας σαρωμένης PNG ή JPEG σε ένα `OcrEngine`.  
* Μετατροπή αυτής της εικόνας σε αναζητήσιμο PDF με μία κλήση μεθόδου.  
* Αποθήκευση του αποτελέσματος και επαλήθευση ότι το επίπεδο κειμένου λειτουργεί πραγματικά.  

Καμία ασαφής αναφορά σε εξωτερικά έγγραφα—όλα όσα χρειάζεστε είναι εδώ. Μια βασική κατανόηση του C# και του .NET Core/Framework είναι αρκετή· αν έχετε γράψει ένα “Hello World” πριν, θα τα καταφέρετε.

---

## Προαπαιτούμενα

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0+ (or .NET Framework 4.7.2+) | Το Aspose OCR υποστηρίζει και τα δύο, αλλά η πιο πρόσφατη εκτέλεση προσφέρει καλύτερη απόδοση. |
| Visual Studio 2022 or VS Code | Ένα IDE καθιστά πιο εύκολη τη διαχείριση των πακέτων NuGet και την εκτέλεση της επίδειξης. |
| Aspose.OCR NuGet package (`Aspose.OCR` v23.12 or later) | Αυτή η βιβλιοθήκη παρέχει την κλάση `OcrEngine` που θα χρησιμοποιήσουμε. |
| A scanned image (`contract_scan.png` in this example) | Το αρχείο προέλευσης που θέλετε να μετατρέψετε σε αναζητήσιμο PDF. |

Αν λείπει κάποιο από αυτά, απλώς ανοίξτε το τερματικό σας και εκτελέστε:

```bash
dotnet add package Aspose.OCR --version 23.12
```

Αυτή η εντολή ενσωματώνει όλα όσα χρειάζεστε.

---

## Βήμα 1: Αρχικοποίηση του OCR Engine – Δημιουργία Πυρήνα Αναζητήσιμου PDF

Το πρώτο που κάνουμε είναι να δημιουργήσουμε μια παρουσία του `OcrEngine`. Σκεφτείτε το ως τον εγκέφαλο που θα διαβάσει τα pixel και θα παράγει κείμενο.

```csharp
using System;
using System.Drawing;               // For Image handling
using Aspose.OCR;                  // Core OCR namespace
using Aspose.OCR.Output;           // PDFResult lives here

class Program
{
    static void Main()
    {
        // Step 1: Create the OCR engine
        var ocrEngine = new OcrEngine();

        // The rest of the steps follow...
```

**Γιατί είναι σημαντικό:**  
Η δημιουργία του engine μία φορά και η επαναχρησιμοποίησή του για πολλαπλές εικόνες είναι πιο αποδοτική από το να το δημιουργείτε μέσα σε βρόχο. Το engine διατηρεί εσωτερικούς πόρους (όπως πακέτα γλώσσας) που δεν θέλετε να φορτώνετε ξανά κάθε φορά.

---

## Βήμα 2: Φόρτωση της Πηγαίας Εικόνας – Μετατροπή Εικόνας σε PDF

Στη συνέχεια, κατευθύνουμε το engine στο αρχείο που θέλουμε να επεξεργαστούμε. Το Aspose OCR δέχεται οποιοδήποτε `System.Drawing.Image`, έτσι PNG, JPEG, BMP, ακόμη και TIFF λειτουργούν.

```csharp
        // Step 2: Load the scanned image
        string inputPath = @"YOUR_DIRECTORY/contract_scan.png";
        ocrEngine.Image = Image.FromFile(inputPath);
```

**Συμβουλή:** Αν η εικόνα σας είναι τεράστια (πάνω από 10 MP), σκεφτείτε να τη μειώσετε πρώτα για να διατηρήσετε τη χρήση μνήμης λογική. Η ποιότητα του OCR συνήθως παραμένει καλή στα 300 DPI.

```csharp
        // Optional: downscale large images (maintains aspect ratio)
        // ocrEngine.Image = ImageHelper.Resize(ocrEngine.Image, 2000, 2000);
```

---

## Βήμα 3: Εκτέλεση OCR και Δημιουργία Αναζητήσιμου PDF – Εξαγωγή Κειμένου από Σάρωση

Τώρα συμβαίνει η μαγεία. Η μέθοδος `RecognizePdf()` κάνει δύο πράγματα ταυτόχρονα: εκτελεί OCR στην εικόνα **και** ενσωματώνει το προκύπτον στρώμα κειμένου σε ένα PDF container.

```csharp
        // Step 3: Run OCR and get a searchable PDF result
        PdfResult searchablePdf = ocrEngine.RecognizePdf();
```

**Τι περιέχει το `PdfResult`?**  
Είναι ένας ελαφρύς wrapper που κρατά τα bytes του PDF στη μνήμη. Μπορείτε να το ρέετε απευθείας σε μια απάντηση σε web API, ή—όπως θα κάνουμε στη συνέχεια—να το αποθηκεύσετε στο δίσκο.

---

## Βήμα 4: Αποθήκευση του PDF στο Δίσκο – Μετατροπή Σαρωμένου Εγγράφου σε Αναζητήσιμο PDF

Τέλος, γράψτε τα bytes του PDF σε ένα αρχείο. Η επέκταση αρχείου `.pdf` ενημερώνει οποιονδήποτε προβολέα PDF ότι το έγγραφο είναι αναζητήσιμο.

```csharp
        // Step 4: Save the searchable PDF
        string outputPath = @"YOUR_DIRECTORY/contract_searchable.pdf";
        searchablePdf.Save(outputPath);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

Εκτελέστε το πρόγραμμα (`dotnet run`) και ανοίξτε το `contract_searchable.pdf` στο Adobe Reader. Προσπαθήστε να επιλέξετε κάποιο κείμενο και να το αντιγράψετε—θα δείτε το κρυφό στρώμα να λειτουργεί.

---

## Επαλήθευση του Αποτελέσματος – Λειτουργεί Πραγματικά το OCR;

Μια γρήγορη έλεγχος λογικής σας εξοικονομεί ώρες αργότερα. Ανοίξτε το PDF, πατήστε **Ctrl + F**, και αναζητήστε μια λέξη που ξέρετε ότι εμφανίζεται στην αρχική σάρωση (π.χ., “Agreement”). Αν η αναζήτηση τη βρει, έχετε δημιουργήσει επιτυχώς **αναζητήσιμο PDF**.

Αν το κείμενο δεν είναι επιλέξιμο, ελέγξτε ξανά:

* Την ποιότητα της εικόνας (θολές σαρώσεις παράγουν κακή OCR).  
* Ότι χρησιμοποιήσατε `RecognizePdf()` και όχι μόνο `Recognize()` (το δεύτερο επιστρέφει μόνο απλό κείμενο).  
* Ότι έχει οριστεί η σωστή γλώσσα—`ocrEngine.Language = Language.English;` μπορεί να βελτιώσει την ακρίβεια.

---

## Διαχείριση Πολλών Σελίδων – Μετατροπή Σαρωμένου Εγγράφου με Πολλές Εικόνες

Συχνά ένα συμβόλαιο εκτείνεται σε πολλές σελίδες. Αντί να επεξεργάζεστε κάθε εικόνα ξεχωριστά, μπορείτε να κάνετε βρόχο σε έναν φάκελο και να συγχωνεύσετε τα αποτελέσματα:

```csharp
        var pdfPages = new System.Collections.Generic.List<PdfResult>();

        foreach (var file in System.IO.Directory.GetFiles(@"YOUR_DIRECTORY/Scans", "*.png"))
        {
            ocrEngine.Image = Image.FromFile(file);
            pdfPages.Add(ocrEngine.RecognizePdf());
        }

        // Merge all pages into one PDF
        var mergedPdf = PdfResult.Merge(pdfPages);
        mergedPdf.Save(@"YOUR_DIRECTORY/contract_full_searchable.pdf");
```

**Γιατί να συγχωνεύσετε;**  
Ένα ενιαίο PDF είναι πιο εύκολο να μοιραστεί και να ευρετηριαστεί. Η βοηθητική λειτουργία `Merge` φροντίζει να ενώσει τις σελίδες διατηρώντας το στρώμα κειμένου κάθε σελίδας.

---

## Συνηθισμένα Προβλήματα & Συμβουλές – Εκτέλεση OCR σε Εικόνα σαν Επαγγελματίας

| Issue | Solution |
|-------|----------|
| **Χαμηλό DPI (κάτω από 150)** | Αναδειγματοληψία της εικόνας σε 300 DPI πριν το OCR. |
| **Λανθασμένη γλώσσα** | Ορίστε `ocrEngine.Language = Language.Spanish;` (ή οποιαδήποτε υποστηριζόμενη γλώσσα). |
| **Μεγάλο αποτύπωμα μνήμης** | Αποδεσμεύστε τα αντικείμενα `Image` μετά από κάθε επανάληψη: `ocrEngine.Image.Dispose();` |
| **Απουσία γραμματοσειρών στο PDF** | Το Aspose ενσωματώνει αυτόματα τις τυπικές γραμματοσειρές· για προσαρμοσμένες γραμματοσειρές, προσθέστε τις μέσω `PdfSaveOptions`. |

---

## Πλήρες Παράδειγμα Εργασίας – Όλος ο Κώδικας σε Ένα Σημείο

Παρακάτω είναι το πλήρες, έτοιμο για αντιγραφή πρόγραμμα που **δημιουργεί αναζητήσιμο PDF** από μία μόνο εικόνα. Δεν λείπουν κομμάτια.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Load image (replace with your actual path)
        string inputPath = @"YOUR_DIRECTORY/contract_scan.png";
        ocrEngine.Image = Image.FromFile(inputPath);

        // Optional: improve accuracy by setting language
        // ocrEngine.Language = Language.English;

        // Perform OCR and get searchable PDF
        PdfResult searchablePdf = ocrEngine.RecognizePdf();

        // Save PDF to disk
        string outputPath = @"YOUR_DIRECTORY/contract_searchable.pdf";
        searchablePdf.Save(outputPath);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

Εκτελέστε το, ανοίξτε το αποτέλεσμα, και μόλις **μετατρέψατε εικόνα σε PDF** διατηρώντας το αναζητήσιμο κείμενο—ακριβώς αυτό που απαιτεί η σύγχρονη ροή εργασίας εγγράφων.

---

## Επόμενα Βήματα – Επέκταση του OCR Pipeline σας

Τώρα που μπορείτε να **δημιουργήσετε αναζητήσιμο PDF**, σκεφτείτε αυτές τις βελτιώσεις:

* **Επεξεργασία σε παρτίδες** – Χρησιμοποιήστε το βρόχο πολλαπλών σελίδων παραπάνω για να διαχειριστείτε ολόκληρους φακέλους.  
* **Προσαρμοσμένες ρυθμίσεις OCR** – Ρυθμίστε `ocrEngine.RecognizeArea` για να εστιάσετε σε μια περιοχή, ή τροποποιήστε το `ocrEngine.PageSegmentationMode`.  
* **Ενσωμάτωση με web API** – Επιστρέψτε τα bytes του PDF απευθείας από ένα endpoint ASP.NET Core για μετατροπή σε πραγματικό χρόνο.  
* **Μετα-επεξεργασία** – Εκτελέστε ορθογραφικό έλεγχο ή φίλτρο regex στο εξαγόμενο κείμενο για μεγαλύτερη ακρίβεια.  

Κάθε ένα από αυτά τα θέματα περιλαμβάνει φυσικά **εξαγωγή κειμένου από σάρωση** ή **εκτέλεση OCR σε εικόνα**, έτσι ήδη χρησιμοποιείτε τις ίδιες λέξεις-κλειδιά που αγαπούν οι μηχανές αναζήτησης.

---

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να **δημιουργήσετε αναζητήσιμο PDF** από σαρωμένες εικόνες χρησιμοποιώντας το Aspose OCR σε C#. Από την αρχικοποίηση του engine, τη φόρτωση της εικόνας, την εκτέλεση OCR, μέχρι την αποθήκευση του τελικού αναζητήσιμου PDF, η διαδικασία είναι απλή και πλήρως αυτόνομη.  

Δοκιμάστε το με τα δικά σας συμβόλαια, τιμολόγια ή οποιοδήποτε σαρωμένο έγγραφο. Μόλις κυριαρχήσετε σε αυτή τη ροή, θα βρείτε εύκολο να **μετατρέψετε παρτίδες σαρωμένων εγγράφων**, **εξάγετε κείμενο από σάρωση**, και **εκτελέσετε OCR σε εικόνα** για οποιοδήποτε επόμενο έργο επεξεργασίας δεδομένων.  

Αν αντιμετωπίσετε κάποιο πρόβλημα ή έχετε ιδέες για περαιτέρω αυτοματοποίηση, αφήστε ένα σχόλιο παρακάτω. Καλή προγραμματιστική δουλειά, και απολαύστε τη μετατροπή των στοίβων χαρτιού σε αναζητήσιμα ψηφιακά περιουσιακά στοιχεία!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}