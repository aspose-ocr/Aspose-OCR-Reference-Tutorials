---
category: general
date: 2026-02-16
description: Δημιουργήστε PDF με δυνατότητα αναζήτησης από εικόνα TIFF χρησιμοποιώντας
  το Aspose OCR. Μάθετε πώς να μετατρέψετε TIFF σε PDF, να κάνετε OCR σε εικόνα σε
  PDF και να αναγνωρίσετε κείμενο από εικόνα σε C#.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- ocr image to pdf
- recognize text from image
- convert scanned image pdf
language: el
og_description: Δημιουργήστε γρήγορα PDF με δυνατότητα αναζήτησης. Αυτό το σεμινάριο
  δείχνει πώς να μετατρέψετε TIFF σε PDF, να κάνετε OCR εικόνας σε PDF και να αναγνωρίσετε
  κείμενο από εικόνα με το Aspose OCR.
og_title: Δημιουργία Αναζητήσιμου PDF από TIFF – Οδηγός Aspose OCR
tags:
- Aspose OCR
- C#
- PDF/A
- Document Processing
title: Δημιουργία Αναζητήσιμου PDF από TIFF – Οδηγός Βήμα‑βήμα για το Aspose OCR
url: /el/net/text-recognition/create-searchable-pdf-from-tiff-aspose-ocr-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF από TIFF – Οδηγός Βήμα‑βήμα με Aspose OCR

Έχετε ποτέ χρειαστεί να **δημιουργήσετε αναζητήσιμο PDF** από ένα σαρωμένο TIFF αλλά δεν ήξερες ποια βιβλιοθήκη θα κάνει τη βαριά δουλειά; Δεν είστε μόνοι. Σε πολλά έργα αυτοματοποίησης γραφείου καταλήγουμε με ένα σωρό αρχείων TIFF που μοιάζουν με εικόνες, όχι κείμενο. Τα καλά νέα; Με το Aspose OCR μπορείτε να **μετατρέψετε tiff σε pdf**, να εκτελέσετε OCR στην εικόνα και να καταλήξετε με ένα PDF/A‑2b που είναι πλήρως αναζητήσιμο.

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα ένα πλήρες, εκτελέσιμο παράδειγμα C# που δείχνει ακριβώς πώς να **δημιουργήσετε αναζητήσιμο PDF** αρχεία, γιατί κάθε βήμα είναι σημαντικό και ποια παγίδες πρέπει να προσέξετε. Στο τέλος θα μπορείτε να **αναγνωρίσετε κείμενο από εικόνα** αρχεία, **OCR εικόνα σε pdf**, και ακόμη **μετατρέψετε σαρωμένα pdf εικόνας** έγγραφα που πληρούν τα πρότυπα αρχειοθέτησης.

## Τι Θα Μάθετε

- Πώς να εγκαταστήσετε και να αναφέρετε το πακέτο NuGet Aspose OCR.  
- Ο ακριβής κώδικας που απαιτείται για **δημιουργία αναζητήσιμου PDF** από αρχείο TIFF.  
- Γιατί η φόρτωση του σωστού μοντέλου γλώσσας είναι κρίσιμη για ακριβές OCR.  
- Συμβουλές για διαχείριση μεγάλων σκαναρισμάτων, πολυ‑σελίδων TIFF και συμμόρφωση με PDF/A.  
- Πού βρίσκεται το παραγόμενο αρχείο και πώς να επαληθεύσετε ότι το κείμενο είναι αναζητήσιμο.

### Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| .NET 6.0 ή νεότερο (οποιοδήποτε πρόσφατο runtime .NET) | Το Aspose OCR παρέχει δυαδικά αρχεία για .NET Standard 2.0+, που τρέχουν παντού από .NET Core έως .NET Framework. |
| Visual Studio 2022 (ή VS Code με επέκταση C#) | Σας παρέχει IntelliSense και εύκολη διαχείριση NuGet. |
| Ένα ενεργό άδεια Aspose OCR (ή ένα δωρεάν κλειδί αξιολόγησης) | Η δωρεάν δοκιμή περιορίζει τον αριθμό σελίδων· μια άδεια αφαιρεί το υδατογράφημα και ενεργοποιεί την έξοδο PDF/A‑2b. |
| Ένα αρχείο TIFF που θέλετε να επεξεργαστείτε (π.χ., `input.tif`) | Αυτή είναι η εικόνα προέλευσης που θα μετατρέψουμε σε **αναζητήσιμο PDF**. |

> **Συμβουλή:** Αν εργάζεστε με πολυ‑σελίδες TIFF, το Aspose OCR θα αντιμετωπίσει κάθε σελίδα ως ξεχωριστή εικόνα αυτόματα—χωρίς επιπλέον κώδικα.

## Βήμα 1: Εγκατάσταση του Πακέτου NuGet Aspose OCR

Πρώτα, προσθέστε τη βιβλιοθήκη στο έργο σας. Ανοίξτε το Package Manager Console και εκτελέστε:

```powershell
Install-Package Aspose.OCR
```

Ή, αν προτιμάτε το GUI, αναζητήστε “Aspose.OCR” στο **NuGet Package Manager** και κάντε κλικ στο **Install**. Αυτό θα κατεβάσει όλα τα απαιτούμενα DLL, συμπεριλαμβανομένων των μοντέλων γλώσσας που θα χρειαστούμε αργότερα.

> **Γιατί αυτό το βήμα;** Χωρίς το πακέτο η κλάση `OcrEngine` δεν υπάρχει, και θα λάβετε σφάλματα κατά τη μεταγλώττιση. Η προσέγγιση μέσω NuGet εγγυάται ότι έχετε τη σωστή έκδοση (προς το παρόν 23.12) και κατεβάζει αυτόματα τυχόν εξαρτήσεις.

## Βήμα 2: Αρχικοποίηση του OCR Engine

Δημιουργώντας μια παρουσία του engine είναι η πρώτη πραγματική γραμμή κώδικα που θα γράψετε. Σκεφτείτε το `OcrEngine` ως τον εγκέφαλο που κάνει όλη τη βαριά δουλειά.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine – this object will manage the entire pipeline
OcrEngine ocrEngine = new OcrEngine();
```

> **Τι συμβαίνει;** Ο κατασκευαστής ρυθμίζει εσωτερικές μνήμες και προετοιμάζει το engine για φόρτωση μοντέλου γλώσσας. Αν το παραλείψετε, κλήσεις όπως `LoadLanguage` θα ρίξουν `NullReferenceException`.

## Βήμα 3: Φόρτωση του Αγγλικού Μοντέλου Γλώσσας (ή οποιουδήποτε άλλου)

Η ακρίβεια του OCR εξαρτάται από το μοντέλο γλώσσας που φορτώνετε. Για τα περισσότερα δυτικά έγγραφα η Αγγλική είναι επαρκής, αλλά το Aspose υποστηρίζει δεκάδες γλώσσες.

```csharp
// Load English language data – essential for recognizing Latin characters
ocrEngine.LoadLanguage(LanguageModel.English);
```

> **Γιατί να φορτώσετε μοντέλο;** Το engine χρειάζεται μια στατιστική αναπαράσταση των σχημάτων χαρακτήρων. Χωρίς αυτό θα πάρετε ακατανόητο κείμενο ή κενό αποτέλεσμα. Αν χρειάζεστε **αναγνώριση κειμένου από εικόνα** στα Γαλλικά, αντικαταστήστε το `LanguageModel.English` με `LanguageModel.French`.

## Βήμα 4: Παροχή της Εικόνας TIFF και Δημιουργία PDF/A‑2b

Τώρα δείχνουμε το engine στο αρχείο προέλευσης. Η βοηθητική μέθοδος `ImageStream.FromFile` διαβάζει το TIFF (μονή ή πολλαπλή σελίδα) στη μνήμη.

```csharp
// Step 4: Assign the TIFF image to the engine
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.tif");

// Run OCR and produce a PDF/A‑2b document – this is the searchable PDF we want
PdfAResult searchablePdf = ocrEngine.RecognizePdfA(PdfAStandard.PdfA2b);
```

> **Τι κάνει αυτό;** Η `RecognizePdfA` εκτελεί τρεις ενέργειες στο παρασκήνιο:  
> 1️⃣ Εκτελεί OCR σε κάθε σελίδα του TIFF.  
> 2️⃣ Ενσωματώνει το αναγνωρισμένο κείμενο ως αόρατο στρώμα.  
> 3️⃣ Συσκευάζει τα πάντα σε ένα κοντέινερ PDF/A‑2b, το οποίο είναι το πρότυπο ISO για μακροπρόθεσμη διατήρηση.  

Αν χρειάζεστε μόνο ένα απλό PDF (χωρίς συμμόρφωση με αρχειοθέτηση), μπορείτε να καλέσετε `ocrEngine.RecognizePdf()` αντί αυτού. Αλλά για τα περισσότερα επιχειρηματικά σενάρια, το PDF/A‑2b είναι η πιο ασφαλής επιλογή.

## Βήμα 5: Αποθήκευση του Αναζητήσιμου PDF στο Δίσκο

Τέλος, γράψτε το αποτέλεσμα σε αρχείο. Η μέθοδος `Save` παίρνει μια διαδρομή και διαχειρίζεται όλο το I/O.

```csharp
// Save the generated searchable PDF to your output folder
searchablePdf.Save("YOUR_DIRECTORY/output.pdf");
```

Όταν ανοίξετε το `output.pdf` στο Adobe Reader, θα πρέπει να μπορείτε να πληκτρολογήσετε μια λέξη στο πεδίο αναζήτησης και να τη βρείτε αμέσως—παρόλο που το αρχικό αρχείο ήταν μόνο μια εικόνα. Αυτή είναι η μαγεία των ροών εργασίας **δημιουργίας αναζητήσιμου PDF**.

## Μετατροπή TIFF σε PDF – Σύντομη Ανασκόπηση

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα που ενώνει όλα τα παραπάνω. Μπορείτε να το αντιγράψετε‑και‑επικολλήσετε σε μια εφαρμογή κονσόλας και να πατήσετε **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the desired language model (English in this case)
        ocrEngine.LoadLanguage(LanguageModel.English);

        // 3️⃣ Point the engine at the TIFF you want to convert
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.tif");

        // 4️⃣ Recognize the image and produce a PDF/A‑2b (searchable PDF)
        PdfAResult searchablePdf = ocrEngine.RecognizePdfA(PdfAStandard.PdfA2b);

        // 5️⃣ Persist the result to disk
        searchablePdf.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("✅ Searchable PDF created successfully!");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Το `output.pdf` εμφανίζεται στο `YOUR_DIRECTORY`. Ανοίξτε το, επιλέξτε το εργαλείο κειμένου, και θα δείτε επιλέξιμο, αναζητήσιμο κείμενο επικάλυψη πάνω στην αρχική ραστερ εικόνα.

## OCR Εικόνας σε PDF – Διαχείριση Ακραίων Περιπτώσεων

### Πολυ‑σελίδες TIFF

Αν το αρχείο προέλευσης περιέχει περισσότερες από μία σελίδες, το Aspose OCR επεξεργάζεται αυτόματα κάθε σελίδα και προσθέτει την αντίστοιχη σελίδα στο PDF. Δεν απαιτείται επιπλέον βρόχος.

### Μεγάλα Αρχεία & Διαχείριση Μνήμης

Για σκαναρίσματα σε κλίμακα gigabyte, σκεφτείτε την ενεργοποίηση του **λειτουργίας streaming**:

```csharp
ocrEngine.Image = ImageStream.FromFile("large.tif", useMemoryCache: false);
```

Αυτό λέει στο engine να διαβάζει τμήματα από το δίσκο αντί να φορτώνει ολόκληρη την εικόνα στη RAM—ιδανικό για εργασίες παρτίδας σε διακομιστή.

### Διαφορετικές Μορφές Εξόδου

Μερικές φορές δεν χρειάζεστε PDF/A‑2b αλλά απλό PDF. Αλλάξτε την κλήση:

```csharp
PdfResult plainPdf = ocrEngine.RecognizePdf();
plainPdf.Save("plain.pdf");
```

Ή, αν θέλετε μόνο το ακατέργαστο κείμενο (χωρίς PDF), χρησιμοποιήστε:

```csharp
string extractedText = ocrEngine.RecognizeText();
System.IO.File.WriteAllText("text.txt", extractedText);
```

Αυτές οι παραλλαγές αντιμετωπίζουν το σενάριο **μετατροπής σαρωμένης εικόνας pdf** όπου τα επόμενα συστήματα δέχονται μόνο απλά PDF.

## Συμβουλές για Αξιόπιστο OCR

- **Το DPI μετράει:** Σκαναρίσματα στα 300 DPI ή υψηλότερα δίνουν τα καλύτερα ποσοστά αναγνώρισης. Κάτω από 200 DPI θα παρατηρήσετε πτώση στην ακρίβεια.  
- **Προεπεξεργασία:** Αν το TIFF είναι θορυβώδες, εκτελέστε το μέσω `ocrEngine.Image = ImageProcessor.Deskew(...).Apply(ocrEngine.Image);` πριν την αναγνώριση.  
- **Άδεια:** Θυμηθείτε να ορίσετε την άδειά σας νωρίς στην εφαρμογή (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`). Χωρίς αυτή, η έξοδος θα περιέχει υδατογράφημα “Evaluation”.  
- **Επεξεργασία παρτίδας:** Τυλίξτε τη βασική λογική σε βρόχο `foreach` πάνω σε φάκελο με TIFF για **μετατροπή tiff σε pdf** μαζικά.

## Συχνές Ερωτήσεις

**Ε: Λειτουργεί αυτό σε Linux;**  
Α: Απόλυτα. Το Aspose OCR στοχεύει στο .NET Standard, έτσι μπορείτε να εκτελέσετε το ίδιο δυαδικό αρχείο σε Windows, Linux ή macOS με το runtime .NET 6.

**Ε: Τι γίνεται αν χρειαστώ αναγνώριση γλώσσας διαφορετικής από τα Αγγλικά;**  
Α: Απλώς αντικαταστήστε το `LanguageModel.English` με το κατάλληλο enum, π.χ., `LanguageModel.Spanish`. Μπορείτε επίσης να φορτώσετε πολλαπλές γλώσσες ταυτόχρονα για έγγραφα με μεικτές γλώσσες.

**Ε: Μπορώ να ενσωματώσω προσαρμοσμένη γραμματοσειρά στο PDF/A;**  
Α: Ναι. Χρησιμοποιήστε `ocrEngine.Options.PdfOptions.Font = PdfFont.CreateFont("path/to/font.ttf");` πριν καλέσετε το `RecognizePdfA`.

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για **δημιουργία αναζητήσιμου PDF** αρχείων από εικόνες TIFF χρησιμοποιώντας το Aspose OCR. Από την εγκατάσταση του πακέτου NuGet, τη φόρτωση του σωστού μοντέλου γλώσσας, μέχρι τη δημιουργία PDF/A‑

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}