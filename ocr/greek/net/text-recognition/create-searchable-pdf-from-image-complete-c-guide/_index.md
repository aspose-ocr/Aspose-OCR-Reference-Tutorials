---
category: general
date: 2026-02-13
description: Δημιουργήστε PDF με δυνατότητα αναζήτησης από εικόνα χρησιμοποιώντας
  το Aspose.OCR. Μάθετε πώς να μετατρέπετε εικόνα σε PDF, να εξάγετε κείμενο από την
  εικόνα, να ενσωματώνετε γραμματοσειρές στο PDF και να αναγνωρίζετε κείμενο από PNG.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- embed fonts in pdf
- recognize text from png
language: el
og_description: Δημιουργήστε αναζητήσιμο PDF από εικόνα με το Aspose.OCR. Αυτός ο
  οδηγός δείχνει πώς να μετατρέψετε την εικόνα σε PDF, να ενσωματώσετε γραμματοσειρές
  και να εξάγετε κείμενο από PNG με ευκολία.
og_title: Δημιουργία Αναζητήσιμου PDF από Εικόνα – Βήμα‑βήμα Οδηγός C#
tags:
- C#
- OCR
- Aspose
- PDF generation
title: Δημιουργία Αναζητήσιμου PDF από Εικόνα – Πλήρης Οδηγός C#
url: /el/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF από Εικόνα – Πλήρης Οδηγός C#

Έχετε ποτέ χρειαστεί να **δημιουργήσετε αναζητήσιμο PDF** από ένα σκαναρισμένο PNG αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι. Σε πολλά έργα—σκεφτείτε την ψηφιοποίηση τιμολογίων ή την αρχειοθέτηση παλιών εγχειριδίων—η δυνατότητα να μετατρέψετε μια εικόνα σε PDF που μπορείτε πραγματικά να αναζητήσετε είναι ένας καθοριστικός παράγοντας.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τις ακριβείς ενέργειες για **μετατροπή εικόνας σε PDF**, **εξαγωγή κειμένου από εικόνα**, ενσωμάτωση των απαραίτητων γραμματοσειρών, και τελικά τη δημιουργία ενός πλήρως αναζητήσιμου αρχείου PDF. Χωρίς ασαφείς αναφορές, μόνο ένα ολοκληρωμένο, εκτελέσιμο παράδειγμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο Visual Studio σήμερα.

> **Τι θα πάρετε:** μια εφαρμογή C# console που διαβάζει το `input.png`, εκτελεί OCR, ενσωματώνει γραμματοσειρές, διατηρεί την αρχική raster εικόνα ως φόντο, και γράφει το `output.pdf`. Στο τέλος θα καταλάβετε *γιατί* κάθε γραμμή είναι σημαντική και πώς να την προσαρμόσετε στις δικές σας ανάγκες.

---

## Προαπαιτούμενα

- .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+).  
- Aspose.OCR for .NET – μπορείτε να το κατεβάσετε από το NuGet (`Install-Package Aspose.OCR`).  
- Ένα δείγμα εικόνας PNG (`input.png`) τοποθετημένο σε φάκελο που ελέγχετε.  
- Βασική εξοικείωση με έργα C# console (αν δεν έχετε δημιουργήσει ποτέ ένα, ανοίξτε το Visual Studio → **Create a new project** → **Console App** → **C#**).

> **Συμβουλή:** Η Aspose προσφέρει δωρεάν δοκιμαστική άδεια· απλώς τοποθετήστε το αρχείο `.lic` δίπλα στο εκτελέσιμο σας και η βιβλιοθήκη θα λειτουργεί χωρίς υδατογράφημα.

---

## Βήμα 1: Ρύθμιση του OCR Engine – Αναγνώριση Κειμένου από PNG

Το πρώτο που χρειαζόμαστε είναι ένας OCR engine που μπορεί πραγματικά να διαβάσει τους χαρακτήρες σε ένα αρχείο PNG. Η Aspose.OCR το κάνει εύκολο.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

// Initialize the OCR engine with English language support
OcrEngine ocrEngine = new OcrEngine
{
    // Primary language – you can add more if needed
    Language = OcrLanguage.English
};
```

**Γιατί είναι σημαντικό:**  
Η ρύθμιση του `Language` λέει στον engine ποιο σύνολο χαρακτήρων να περιμένει. Αν το παραλείψετε, ο engine χρησιμοποιεί μια γενική λειτουργία που μπορεί να ερμηνεύσει λανθασμένα χαρακτήρες με τόνους ή αριθμούς. Για πολυγλωσσικά έγγραφα, μπορείτε να περάσετε λίστα χωρισμένη με κόμμα όπως `OcrLanguage.English | OcrLanguage.French`.

---

## Βήμα 2: Φόρτωση και Αναγνώριση της Εικόνας – Εξαγωγή Κειμένου από Εικόνα

Τώρα που ο engine είναι έτοιμος, του δίνουμε το PNG που θέλουμε να επεξεργαστούμε.

```csharp
// Path to the source image; adjust as needed
string inputPath = @"YOUR_DIRECTORY/input.png";

// Perform OCR – this populates the engine's internal text representation
ocrEngine.RecognizeImage(inputPath);
```

**Τι συμβαίνει στο παρασκήνιο;**  
Η `RecognizeImage` σαρώνει το bitmap, εντοπίζει μπλοκ κειμένου και αποθηκεύει το αποτέλεσμα στο `ocrEngine`. Μπορείτε αργότερα να προσπελάσετε το `ocrEngine.Text` αν χρειάζεστε μόνο το ακατέργαστο κείμενο, αλλά για ένα αναζητήσιμο PDF θα αφήσουμε την Aspose να διαχειριστεί τη μετατροπή απευθείας.

> **Ακραία περίπτωση:** Αν το PNG σας είναι τεράστιο (πάνω από 10 MB) μπορεί να ξεμείνετε από μνήμη. Σε αυτήν την περίπτωση, εξετάστε το ενδεχόμενο αλλαγής μεγέθους της εικόνας πρώτα ή τη χρήση του `OcrEngine.RecognizeImage(Stream)` για ροή δεδομένων.

---

## Βήμα 3: Ρύθμιση Επιλογών Εξαγωγής PDF – Ενσωμάτωση Γραμματοσειρών στο PDF

Ένα αναζητήσιμο PDF δεν είναι χρήσιμο αν οι γραμματοσειρές δεν είναι ενσωματωμένες· το έγγραφο θα εμφανίζεται σπασμένο σε μηχανήματα που δεν διαθέτουν τις απαιτούμενες γραμματοσειρές. Η Aspose μας επιτρέπει να το ελέγξουμε με ένα απλό αντικείμενο επιλογών.

```csharp
// Define how the searchable PDF should be built
SearchablePdfOptions pdfOptions = new SearchablePdfOptions
{
    // Guarantees the PDF renders correctly everywhere
    EmbedFonts = true,

    // Keeps the original raster image as a visual background
    KeepOriginalImage = true
};
```

**Γιατί να ενσωματώσετε γραμματοσειρές;**  
Όταν το `EmbedFonts` είναι `true`, το PDF περιέχει τα δεδομένα της γραμματοσειράς μέσα στο αρχείο. Αυτό εξασφαλίζει ότι οποιοσδήποτε προβολέας—Chrome, Adobe Reader ή μια κινητή εφαρμογή—θα εμφανίσει το κείμενο ακριβώς όπως προορίζεται, ακόμη και αν το σύστημα-στόχος δεν διαθέτει τη γραμματοσειρά.

**Πότε θα θέλατε να θέσετε το `KeepOriginalImage` σε `false`;**  
Αν χρειάζεστε μόνο το εξαγόμενο κείμενο και θέλετε μικρότερο αρχείο, η απενεργοποίηση αυτή αφαιρεί την εικόνα φόντου, αφήνοντας ένα «καθαρό» PDF μόνο με κείμενο.

---

## Βήμα 4: Εξαγωγή σε Αναζητήσιμο PDF – Μετατροπή Εικόνας σε PDF

Με τα αποτελέσματα OCR και τις επιλογές PDF έτοιμες, το τελευταίο βήμα είναι μια εντολή που γράφει το αναζητήσιμο PDF στο δίσκο.

```csharp
// Destination path for the generated PDF
string outputPath = @"YOUR_DIRECTORY/output.pdf";

// Export the OCR result as a searchable PDF
ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created.");
```

**Τι θα δείτε:**  
Ανοίγοντας το `output.pdf` σε οποιονδήποτε προβολέα, μπορείτε να επιλέξετε κείμενο, να το αντιγράψετε και ακόμη να κάνετε αναζήτηση (`Ctrl + F`) για να εντοπίσετε λέξεις που αρχικά υπήρχαν μόνο ως pixel στο PNG.

---

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να μεταγλωττίσετε και να τρέξετε αμέσως. Αντικαταστήστε το `YOUR_DIRECTORY` με το φάκελο που περιέχει το `input.png`.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine – set language to English
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // 2️⃣ Recognize text from the PNG image
        string inputPath = @"YOUR_DIRECTORY/input.png";
        ocrEngine.RecognizeImage(inputPath);

        // 3️⃣ Prepare PDF options – embed fonts & keep raster background
        SearchablePdfOptions pdfOptions = new SearchablePdfOptions
        {
            EmbedFonts = true,
            KeepOriginalImage = true
        };

        // 4️⃣ Export to a searchable PDF file
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

        // 5️⃣ Notify the user
        Console.WriteLine("Searchable PDF created.");
    }
}
```

**Αναμενόμενη έξοδος στην κονσόλα:**

```
Searchable PDF created.
```

Ανοίξτε το `output.pdf` και δοκιμάστε να αναζητήσετε μια λέξη που γνωρίζετε ότι εμφανίζεται στο `input.png`. Αν επισημανθεί, έχετε δημιουργήσει επιτυχώς **αναζητήσιμο PDF** από μια εικόνα.

---

## Συχνές Ερωτήσεις & Επαγγελματικές Συμβουλές

### “Μπορώ να επεξεργαστώ πολλαπλές εικόνες σε μία εκτέλεση;”

Απολύτως. Τυλίξτε τη λογική αναγνώρισης και εξαγωγής μέσα σε βρόχο, ίσως χρησιμοποιώντας `Directory.GetFiles(..., "*.png")`. Θυμηθείτε να δώσετε σε κάθε PDF μοναδικό όνομα, π.χ. `Path.GetFileNameWithoutExtension(img) + ".pdf"`.

### “Τι γίνεται αν το έγγραφό μου περιέχει κείμενο στα Αγγλικά και στα Ισπανικά;”

Ορίστε την ιδιότητα γλώσσας σε συνδυασμένη σημαία:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

Η Aspose θα προσπαθήσει τότε να εντοπίσει χαρακτήρες και από τα δύο αλφάβητα.

### “Το αρχείο PDF είναι τεράστιο—πώς μπορώ να το μειώσω;”

Δύο γρήγορα κόλπα:

1. Ορίστε `pdfOptions.KeepOriginalImage = false` για να αφαιρέσετε το raster φόντο.  
2. Χρησιμοποιήστε `pdfOptions.ImageCompression = ImageCompression.Jpeg;` (θα χρειαστεί να προσθέσετε αυτήν την ιδιότητα) για να συμπιέσετε την ενσωματωμένη εικόνα.

### “Χρειάζομαι άδεια για παραγωγική χρήση;”

Η δοκιμαστική άδεια λειτουργεί καλά για δοκιμές, αλλά για εμπορική ανάπτυξη πρέπει να αγοράσετε άδεια και να την καταχωρίσετε νωρίς στην εφαρμογή σας:

```csharp
Aspose.OCR.License license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

---

## Επέκταση της Λύσης

Τώρα που ξέρετε πώς να **δημιουργήσετε αναζητήσιμο PDF**, ίσως θέλετε να:

- **Προσθέσετε υδατογράφημα** – χρησιμοποιήστε το `PdfDocument` από την Aspose.PDF για να επικάψετε κείμενο μετά το OCR.  
- **Επεξεργασία πολλαπλών PDF** – συνδυάστε πολλά αναζητήσιμα PDF σε ένα χρησιμοποιώντας το `PdfFileEditor`.  
- **Ενσωμάτωση με Azure Blob Storage** – διαβάστε/γράψτε τα ρεύματα εικόνας και PDF απευθείας από το cloud, εξαλείφοντας την τοπική I/O.

Κάθε μία από αυτές τις επεκτάσεις ακολουθεί το ίδιο μοτίβο: λάβετε το αποτέλεσμα OCR, ρυθμίστε την επόμενη βιβλιοθήκη, και αλυσίδωσε τις λειτουργίες.

---

## Συμπέρασμα

Μόλις μάθατε πώς να **δημιουργήσετε αναζητήσιμο PDF** από μια εικόνα PNG χρησιμοποιώντας την Aspose.OCR σε C#. Αρχικοποιώντας τον OCR engine, αναγνωρίζοντας το κείμενο, ρυθμίζοντας το `SearchablePdfOptions` για **ενσωμάτωση γραμματοσειρών στο PDF**, και εξάγοντας, λαμβάνετε ένα αρχείο που είναι τόσο οπτικά πανομοιότυπο με το πρωτότυπο όσο και πλήρως αναζητήσιμο.  

Από εδώ, πειραματιστείτε με μαζικές μετατροπές, διαφορετικές γλώσσες ή πιο σφιχτή συμπίεση—ό,τι ταιριάζει στη ροή εργασίας σας. Αν αντιμετωπίσετε δυσκολίες, τα φόρουμ της Aspose και η τεκμηρίωση API είναι αξιόπιστες πηγές, αλλά τα βασικά βήματα παραπάνω καλύπτουν το 90 % των τυπικών περιπτώσεων.

Καλή κωδικοποίηση, και εύχομαι τα PDF σας να είναι πάντα αναζητήσιμα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}