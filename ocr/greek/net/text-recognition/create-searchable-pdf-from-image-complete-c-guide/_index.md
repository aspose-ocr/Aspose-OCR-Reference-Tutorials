---
category: general
date: 2026-03-23
description: Δημιουργήστε αναζητήσιμο PDF από εικόνα χρησιμοποιώντας το Aspose OCR.
  Μάθετε πώς να μετατρέψετε TIFF σε PDF με υψηλή συμπίεση και να αναγνωρίσετε το κείμενο
  της εικόνας σε λίγα λεπτά.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- high compression pdf
- recognize image text
- searchable pdf from image
language: el
og_description: Δημιουργήστε PDF με δυνατότητα αναζήτησης από εικόνα με το Aspose
  OCR. Αυτό το σεμινάριο δείχνει πώς να μετατρέψετε TIFF σε PDF, να προσθέσετε ένα
  επίπεδο αναζητήσιμου κειμένου και να εφαρμόσετε υψηλή συμπίεση.
og_title: Δημιουργία Αναζητήσιμου PDF από Εικόνα – Πλήρης Οδηγός C#
tags:
- Aspose OCR
- C#
- PDF generation
title: Δημιουργία Αναζητήσιμου PDF από Εικόνα – Πλήρης Οδηγός C#
url: /el/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF από Εικόνα – Πλήρης Οδηγός C#

Έχετε χρειαστεί ποτέ να **create searchable pdf** από ένα σαρωμένο έγγραφο αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε ο μόνος—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν μετατρέπουν σαρώσεις TIFF σε αναζητήσιμα PDF. Τα καλά νέα; Με το Aspose OCR μπορείτε να **convert tiff to pdf**, να προσθέσετε ένα κρυφό στρώμα κειμένου από πάνω, και ακόμη να μειώσετε το μέγεθος του αρχείου με επιλογές **high compression pdf**, όλα σε λίγες γραμμές C#.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: από την εγκατάσταση των σωστών πακέτων NuGet, τη φόρτωση μιας εικόνας TIFF, την αναγνώριση του κειμένου της, και τέλος την εξαγωγή ενός αναζητήσιμου PDF. Στο τέλος θα έχετε μια εκτελέσιμη εφαρμογή console που **recognize image text** και παράγει ένα συμπαγές, αναζητήσιμο PDF έτοιμο για ευρετηρίαση. Χωρίς επιπλέον εργαλεία, χωρίς χειροκίνητα βήματα OCR—απλός κώδικας και λίγη εξήγηση.

## Προαπαιτούμενα & Τι Θα Χρειαστείτε

- **.NET 6+** (ή .NET Framework 4.6+). Το API λειτουργεί και στα δύο, αλλά το .NET 6 παρέχει τις τελευταίες βελτιώσεις χρόνου εκτέλεσης.  
- **Visual Studio 2022** ή οποιοδήποτε IDE προτιμάτε.  
- Πακέτα NuGet **Aspose.OCR** και **Aspose.OCR.Gpu** (το πακέτο GPU είναι προαιρετικό αλλά επιταχύνει την αναγνώριση σε υποστηριζόμενο υλικό).  
- Ένα δείγμα αρχείου TIFF (π.χ., `invoice.tif`) τοποθετημένο σε φάκελο που ελέγχετε.  

Αν έχετε ήδη αυτά τα στοιχεία, υπέροχα—προχωρήστε. Αν όχι, το βήμα εγκατάστασης παρακάτω θα καλύψει τα πάντα.

## Βήμα 1: Εγκατάσταση Πακέτων Aspose OCR

Για αρχή, ανοίξτε το φάκελο του έργου σας σε ένα τερματικό και εκτελέστε:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Αυτές οι εντολές φέρνουν τόσο τη βασική μηχανή OCR όσο και τη βιβλιοθήκη επιτάχυνσης GPU. Η δεύτερη δεν είναι υποχρεωτική· η μηχανή θα επιστρέψει σε λειτουργία CPU εάν δεν βρει συμβατό GPU.

> **Pro tip:** Όταν στοχεύετε σε περιβάλλον παραγωγής, κλειδώστε τις εκδόσεις των πακέτων στο `csproj` σας για να αποφύγετε απροσδόκητες αλλαγές που σπάζουν.

## Βήμα 2: Δημιουργία Σκελετού Έργου

Δημιουργήστε μια νέα εφαρμογή console (αν δεν έχετε ήδη μία):

```bash
dotnet new console -n PdfExportDemo
cd PdfExportDemo
```

Αντικαταστήστε το αυτόματα δημιουργημένο `Program.cs` με τον πλήρη κώδικα που θα εμφανιστεί αργότερα. Το πρόγραμμα θα:

1. Αρχικοποιήσει ένα `OcrEngine` με υποστήριξη GPU.  
2. Φορτώσει την εικόνα TIFF.  
3. Εκτελέσει OCR και τερματίσει ομαλά σε περίπτωση αποτυχίας.  
4. Ρυθμίσει **PdfExportOptions** για ένα αναζητήσιμο στρώμα και **high compression**.  
5. Γράψει το αρχείο εξόδου.

## Βήμα 3: Γράψτε τον Πλήρη Κώδικα (Πλήρες Παράδειγμα)

Παρακάτω είναι το *ολόκληρο* αρχείο πηγαίου κώδικα. Αντιγράψτε‑το στο `Program.cs`. Τα σχόλια εξηγούν το “γιατί” πίσω από κάθε γραμμή, όχι μόνο το “τι”.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;

class PdfExport
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Initialise OCR engine with GPU acceleration.
        //    GpuMode.Enabled tells Aspose to use the GPU if one is present.
        //    If no compatible GPU exists, the engine automatically falls back
        //    to CPU mode—no extra code required.
        // ------------------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine(GpuMode.Enabled))
        {
            // ------------------------------------------------------------
            // 2️⃣ Load the source image.
            //    ImageStream.FromFile supports many formats; here we use TIFF.
            // ------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\invoice.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // ------------------------------------------------------------
            // 3️⃣ Perform OCR recognition.
            //    Recognize() returns false if the engine cannot read the image.
            //    Exiting early prevents us from creating an empty PDF.
            // ------------------------------------------------------------
            if (!ocrEngine.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return;
            }

            // ------------------------------------------------------------
            // 4️⃣ Configure PDF export options.
            //    IncludeTextLayer = true adds an invisible, searchable text layer.
            //    CompressionLevel = High reduces file size dramatically.
            // ------------------------------------------------------------
            PdfExportOptions pdfExportOptions = new PdfExportOptions
            {
                IncludeTextLayer = true,
                CompressionLevel = PdfCompression.High
            };

            // ------------------------------------------------------------
            // 5️⃣ Save the searchable PDF.
            //    The output will be a compact, searchable PDF ready for indexing.
            // ------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\invoice.pdf";
            ocrEngine.Save(outputPath, pdfExportOptions);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");
        }
    }
}
```

### Γιατί Λειτουργεί Αυτό

- **GPU acceleration** μπορεί να μειώσει το χρόνο αναγνώρισης από δευτερόλεπτα σε χιλιοστά του δευτερολέπτου σε σύγχρονες κάρτες—χρήσιμο για μαζική επεξεργασία.  
- **IncludeTextLayer** ενσωματώνει το κείμενο που προέρχεται από OCR αόρατα, επιτρέποντας στους προβολείς PDF να αναζητούν το έγγραφο χωρίς να αλλάζουν την οπτική του εμφάνιση.  
- **High compression** χρησιμοποιεί συμπίεση Flate (ZIP) στο ρεύμα εικόνας, η οποία είναι χωρίς απώλειες αλλά μειώνει το μέγεθος του αρχείου δραματικά—ιδανικό για αρχειοθέτηση χιλιάδων τιμολογίων.

## Βήμα 4: Εκτελέστε την Εφαρμογή και Επαληθεύστε το Αποτέλεσμα

Ανοίξτε ένα τερματικό μέσα στο φάκελο του έργου και εκτελέστε:

```bash
dotnet run
```

```
Searchable PDF saved to: YOUR_DIRECTORY\invoice.pdf
```

Ανοίξτε το `invoice.pdf` σε οποιονδήποτε αναγνώστη PDF (Adobe Acrobat, Edge ή ακόμη και σε πρόγραμμα περιήγησης). Δοκιμάστε να αναζητήσετε μια λέξη που ξέρετε ότι εμφανίζεται στο αρχικό TIFF—π.χ., “Total”. Ο προβολέας θα πρέπει να επισημάνει τη λέξη παρόλο που είναι μέρος της εικόνας. Αυτό είναι το χαρακτηριστικό ενός **searchable pdf**.

### Αναμενόμενο Μέγεθος Αρχείου

Ένα τυπικό σαρωμένο τιμολόγιο (≈300 KB TIFF) συχνά μειώνεται σε **~80 KB** μετά την εφαρμογή του `PdfCompression.High`. Το ακριβές μέγεθος εξαρτάται από την πολυπλοκότητα της εικόνας, αλλά θα παρατηρήσετε σαφής μείωση.

## Βήμα 5: Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις

| Situation | What to Adjust | Why |
|-----------|----------------|-----|
| **Δεν υπάρχει GPU** | Αλλάξτε το `new OcrEngine(GpuMode.Enabled)` σε `new OcrEngine(GpuMode.Disabled)` | Αποτρέπει τη μηχανή από το να προσπαθήσει αρχικοποίηση GPU, κάτι που μπορεί να προκαλέσει μικρή καθυστέρηση. |
| **Πολλές σελίδες (multi‑page TIFF)** | Ορίστε `ocrEngine.Image = ImageStream.FromFile("multi.tif", PageRange.All);` | Φορτώνει όλα τα πλαίσια· το Aspose θα επεξεργαστεί κάθε σελίδα και θα δημιουργήσει ένα PDF πολλαπλών σελίδων. |
| **Απαιτείται γλώσσα OCR διαφορετική από τα Αγγλικά** | `ocrEngine.Language = Language.French;` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) | Βελτιώνει την ακρίβεια για έγγραφα μη‑Αγγλικής γλώσσας. |
| **Θέλετε ορατό επικάλυμμα κειμένου αντί για κρυφό στρώμα** | `pdfExportOptions.IncludeTextLayer = false;` και προσθέστε χειροκίνητα αντικείμενα `TextFragment`. | Χρήσιμο όταν θέλετε το κείμενο OCR να εμφανίζεται ως επιλέξιμο κείμενο πάνω από την εικόνα. |
| **Πολύ μικρά PDFs** | Συνδυάστε το `PdfCompression.High` με `ImageResolution = 150` DPI πριν την αναγνώριση. | Χαμηλότερο DPI μειώνει τα δεδομένα εικόνας, μειώνοντας περαιτέρω το PDF με κόστος τη οπτική ποιότητα. |

> **Note:** Πάντα δοκιμάζετε τις ακραίες περιπτώσεις σε ένα μικρό δείγμα πριν την κλιμάκωση στην παραγωγή. Η ακρίβεια του OCR μπορεί να διαφέρει ανάλογα με την ποιότητα της εικόνας, το θόρυβο και τη γλώσσα.

## Βήμα 6: Συμβουλές για Υλοποιήσεις Έτοιμες για Παραγωγή

1. **Error Logging** – Αντικαταστήστε το `Console.WriteLine` με ένα κατάλληλο πλαίσιο καταγραφής (Serilog, NLog) για ευκολότερη διάγνωση.  
2. **Batch Processing** – Τυλίξτε τη βασική λογική σε μια μέθοδο που δέχεται διαδρομές εισόδου/εξόδου, και στη συνέχεια επαναλάβετε πάνω σε έναν φάκελο αρχείων TIFF.  
3. **Async I/O** – Αν και το Aspose OCR είναι συγχρονικό, η φόρτωση και αποθήκευση αρχείων μπορεί να γίνει ασύγχρονα για να διατηρούνται τα νήματα UI ανταποκρινόμενα.  
4. **Security** – Εάν εκθέτετε αυτή τη λειτουργία μέσω web API, επικυρώστε τις διαδρομές αρχείων και περιορίστε τα μεγέθη αρχείων για να αποτρέψετε κακή χρήση.  
5. **Version Pinning** – Χρησιμοποιήστε ακριβείς αριθμούς εκδόσεων (`<PackageReference Include="Aspose.OCR" Version="23.12.0" />`) για να εγγυηθείτε συνεπή συμπεριφορά σε όλες τις κατασκευές.

## Συμπέρασμα

Μόλις δημιουργήσαμε μια **complete, end‑to‑end solution** που **create searchable pdf** αρχεία από σαρωμένες εικόνες, **convert tiff to pdf**, και το κάνει με ρυθμίσεις **high compression pdf** ενώ **recognize image text** με ακρίβεια. Το αποτέλεσμα **searchable pdf from image** είναι ελαφρύ, αναζητήσιμο, και έτοιμο για επόμενες ροές εργασίας όπως ευρετηρίαση, αρχειοθέτηση ή e‑discovery.

Έχετε μια δέσμη τιμολογίων; Ενσωματώστε τη μέθοδο σε έναν βρόχο, δείξτε την σε έναν φάκελο, και αφήστε το Aspose OCR να κάνει το σκληρό έργο. Θέλετε να πειραματιστείτε με διαφορετικά επίπεδα συμπίεσης ή πακέτα γλωσσών; Ο κώδικας είναι αρκετά modular ώστε να αλλάξετε αυτές τις επιλογές σε δευτερόλεπτα.

---

*Ready to level up?* Δοκιμάστε να προσθέσετε υδατογράφημα, να ενσωματώσετε μεταδεδομένα, ή ακόμη και να συνδέσετε πολλαπλά OCR‑επεξεργασμένα PDFs. Η σουίτα Aspose προσφέρει πολλές επεκτάσεις—εξερευνήστε τα έγγραφα και διατηρήστε το ρυθμό. Καλή προγραμματιστική!

![Δημιουργία αναζητήσιμου PDF από παράδειγμα screenshot](https://example.com/images/create-searchable-pdf.png "παράδειγμα δημιουργίας αναζητήσιμου pdf")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}