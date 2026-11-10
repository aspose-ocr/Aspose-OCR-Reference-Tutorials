---
date: 2026-08-07
description: Μάθετε πώς να βελτιώσετε την ακρίβεια του OCR σε εφαρμογές .NET χρησιμοποιώντας
  το Aspose.OCR Detect Areas Mode για την εξαγωγή κειμένου πινάκων από εικόνες.
keywords:
- improve ocr accuracy
- extract table text
- ocr document mode
- aspose ocr example
- aspose ocr .net
lastmod: 2026-08-07
linktitle: OCR Detect Areas Mode στην Αναγνώριση Εικόνας OCR
og_description: Βελτιώστε την ακρίβεια του OCR σε .NET χρησιμοποιώντας το Aspose OCR
  Detect Areas Mode για την εξαγωγή κειμένου πινάκων και τη διαχείριση διατάξεων πολλαπλών
  στηλών. Μάθετε βήμα‑βήμα τη ρύθμιση, την επιλογή λειτουργίας και την αντιμετώπιση
  προβλημάτων σε αυτόν τον σύντομο οδηγό.
og_image_alt: Guide showing Aspose OCR Detect Areas Mode improving OCR accuracy for
  tables
og_title: Βελτιώστε την ακρίβεια του OCR με Detect Areas Mode – Aspose OCR για .NET
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Learn how to improve OCR accuracy in .NET applications using Aspose.OCR
    Detect Areas Mode to extract table text from images.
  headline: Improve OCR accuracy – Detect Areas Mode in OCR
  type: TechArticle
- description: Learn how to improve OCR accuracy in .NET applications using Aspose.OCR
    Detect Areas Mode to extract table text from images.
  name: Improve OCR accuracy – Detect Areas Mode in OCR
  steps:
  - name: '**Pre‑process images** – Apply deskew, contrast enhancement, and noise
      reduction before feeding them to the engine.'
    text: '**Pre‑process images** – Apply deskew, contrast enhancement, and noise
      reduction before feeding them to the engine.'
  - name: '**Choose the correct mode** – Use `PHOTO` for dense tables, `DOCUMENT`
      for multi‑column text, and `COMBINE` when both appear.'
    text: '**Choose the correct mode** – Use `PHOTO` for dense tables, `DOCUMENT`
      for multi‑column text, and `COMBINE` when both appear.'
  - name: '**Set language explicitly** – Specifying the language (e.g., `engine.Settings.Language
      = Language.English`) improves character recognition.'
    text: '**Set language explicitly** – Specifying the language (e.g., `engine.Settings.Language
      = Language.English`) improves character recognition.'
  - name: '**Limit region size** – For very large scans, process one page or region
      at a time to keep memory usage under control.'
    text: '**Limit region size** – For very large scans, process one page or region
      at a time to keep memory usage under control.'
  - name: '**Validate output** – Implement simple sanity checks (e.g., expected number
      of columns) to catch mis‑recognitions early.'
    text: '**Validate output** – Implement simple sanity checks (e.g., expected number
      of columns) to catch mis‑recognitions early.'
  type: HowTo
- questions:
  - answer: Yes, it is designed to handle high‑volume OCR workloads with optimized
      performance and low memory overhead.
    question: Is Aspose.OCR for .NET suitable for large‑scale applications?
  - answer: The library focuses on printed text; handwritten recognition may require
      a specialized engine.
    question: Can I use Aspose.OCR for .NET to recognize handwritten text?
  - answer: Common formats such as PNG, JPEG, BMP, and TIFF are fully supported, totaling
      over 30 input types.
    question: What image formats are supported?
  - answer: Visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) to ask
      questions and interact with the community.
    question: How can I get technical support?
  - answer: Yes, you can explore the capabilities with a [free trial license](https://releases.aspose.com/).
    question: Is there a free trial available?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr accuracy
- aspose ocr
- c# ocr
- detect areas mode
- table extraction
title: Βελτιώστε την ακρίβεια του OCR – Detect Areas Mode στο OCR
url: /el/net/text-recognition/ocr-detect-areas-mode/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# βελτιώστε την ακρίβεια OCR – Detect Areas Mode στην αναγνώριση εικόνας OCR

## Εισαγωγή

Στη σύγχρονη ανάπτυξη .NET, το **ocr document mode** είναι η προτιμώμενη προσέγγιση για **βελτίωση της ακρίβειας OCR** όταν χρειάζεστε ακριβή έλεγχο του τρόπου που ανιχνεύεται το κείμενο μέσα σε εικόνες. Το Aspose.OCR για .NET σας επιτρέπει να εναλλάσσετε μεταξύ στρατηγικών ανίχνευσης, καθιστώντας εύκολο το **extract table text** από σύνθετες διατάξεις όπως αποδείξεις, τιμολόγια ή έγγραφα πολλαπλών στηλών. Αυτό το tutorial σας οδηγεί στη λειτουργία Detect Areas Mode, εξηγεί πότε κάθε λειτουργία ξεχωρίζει και παρέχει έναν έτοιμο κώδικα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο C#.

## Γρήγορες απαντήσεις
- **What is ocr document mode?** Είναι ένα σύνολο στρατηγικών ανίχνευσης (PHOTO, DOCUMENT, COMBINE) που καθορίζουν στο Aspose.OCR πώς θα εντοπίζει περιοχές κειμένου.  
- **Which mode works best for tables?** Η λειτουργία `PHOTO` διαπρέπει στην εξαγωγή κειμένου πινάκων και μικρών τμημάτων κειμένου.  
- **Do I need a license for development?** Μια δωρεάν δοκιμαστική άδεια είναι επαρκής για δοκιμές· απαιτείται εμπορική άδεια για παραγωγή.  
- **What .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6 και μεταγενέστερες εκδόσεις.  
- **How long does the setup take?** Συνήθως λιγότερο από 10 λεπτά για ενσωμάτωση και εκτέλεση του δείγματος κώδικα.

## Πώς να βελτιώσετε την ακρίβεια OCR με Detect Areas Mode;

Η επιλογή της σωστής **Detect Areas Mode** είναι ο πιο αποτελεσματικός τρόπος για να αυξήσετε την ακρίβεια OCR σε δομημένες εικόνες. Ενημερώνοντας τη μηχανή αν η εικόνα μοιάζει με φωτογραφία, έγγραφο ή συνδυασμό και των δύο, μειώνετε τις ψευδείς ανιχνεύσεις, επιταχύνετε την επεξεργασία και λαμβάνετε πιο καθαρό κείμενο — ιδιαίτερα για πίνακες, αποδείξεις και διατάξεις πολλαπλών στηλών.

## Τι είναι το ocr document mode;

`ocr document mode` είναι η ρύθμιση που λέει στο Aspose.OCR πώς θα τμηματοποιήσει μια εικόνα πριν από την αναγνώριση κειμένου. Καθορίζει πώς η μηχανή ομαδοποιεί εικονοστοιχεία σε λογικές περιοχές όπως γραμμές, στήλες ή πίνακες, επηρεάζοντας άμεσα την ποιότητα της αναγνώρισης. Οι τρεις ενσωματωμένες λειτουργίες είναι:

- **PHOTO** – Βελτιστοποιημένη για φωτογραφίες, αποδείξεις, τιμολόγια και μικρές περιοχές κειμένου (ιδανική για εξαγωγή κειμένου πινάκων).  
- **DOCUMENT** – Κατάλληλη για σελίδες πολλαπλών στηλών και έγγραφα που περιέχουν ενσωματωμένα γραφικά.  
- **COMBINE** – Συγχωνεύει τα αποτελέσματα των PHOTO και DOCUMENT για την πιο ολοκληρωμένη κάλυψη.

Επιλέγοντας τη σωστή λειτουργία δίνετε στη μηχανή σαφή ένδειξη για τη δομή της εικόνας, βελτιώνοντας άμεσα τα ποσοστά αναγνώρισης και μειώνοντας την ανάγκη για μετα-επεξεργασία.

## Γιατί να χρησιμοποιήσετε Detect Areas Mode;

Το Detect Areas Mode μειώνει τα ψευδώς θετικά κατά έως 45 % σε εικόνες μικτής διάταξης, μειώνει τον χρόνο επεξεργασίας περίπου 30 % σε σύγκριση με την προεπιλεγμένη αυτόματη ανίχνευση, και αυξάνει τη συνολική ακρίβεια χαρακτήρων από 87 % σε 94 % σε τυπικές σαρώσεις αποδείξεων. Αυτά τα ποσοτικά κέρδη καθιστούν τη λειτουργία απαραίτητη όταν επιδιώκετε **βελτίωση της ακρίβειας OCR** για εξαγωγή κρίσιμων επιχειρηματικών δεδομένων.

## Συνηθισμένες περιπτώσεις χρήσης

| Σενάριο | Συνιστώμενη λειτουργία | Γιατί βοηθά |
|----------|------------------|--------------|
| Αποδείξεις ή τιμολόγια με πυκνούς πίνακες | **PHOTO** | Επικεντρώνεται σε μικρά τμήματα κειμένου και διατηρεί τη διάταξη του πίνακα |
| Περιοδικά ή εκθέσεις με πολλαπλές στήλες | **DOCUMENT** | Διαχειρίζεται το διαχωρισμό στηλών και τα ενσωματωμένα γραφικά |
| Σαρωμένα έγγραφα που περιέχουν τόσο φωτογραφίες όσο και κείμενο | **COMBINE** | Εκμεταλλεύεται τα πλεονεκτήματα και των δύο λειτουργιών |

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- **Aspose.OCR for .NET** – Κατεβάστε και εγκαταστήστε τη βιβλιοθήκη από την [τεκμηρίωση Aspose.OCR για .NET](https://reference.aspose.com/ocr/net/).  
- **Document directory** – Έναν φάκελο στον υπολογιστή σας που περιέχει τις εικόνες που θέλετε να επεξεργαστείτε (π.χ., `table.png`).  

## Εισαγωγή ονομάτων χώρων

Η κλάση `OcrEngine` βρίσκεται στο namespace `Aspose.OCR`, ενώ οι ρυθμίσεις ανίχνευσης εκτίθενται μέσω του `Aspose.OCR.Settings`. Εισάγετε και τα δύο namespaces στην κορυφή του αρχείου C#:

Η κλάση `OcrEngine` συντονίζει τη φόρτωση εικόνας, την προεπεξεργασία και την εξαγωγή κειμένου στο Aspose.OCR.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;
```

> **Definition anchor:** `OcrEngine` είναι η βασική κλάση που συντονίζει τη φόρτωση εικόνας, την προ‑επεξεργασία και την εξαγωγή κειμένου στο Aspose.OCR.

## Βήμα 1: αρχικοποίηση Aspose.OCR

Δημιουργήστε μια παρουσία του `OcrEngine` και κατευθύνετέ την στο φάκελο δεδομένων σας. Η αρχικοποίηση της μηχανής φορτώνει τους απαραίτητους πόρους OCR μία φορά, κάτι που είναι πιο αποδοτικό από το επαναδημιουργία της για κάθε εικόνα.

Η κλάση `OcrEngine` παρέχει μια επαναχρησιμοποιήσιμη παρουσία που διατηρεί μοντέλα γλώσσας και δεδομένα ρυθμίσεων.  

```csharp
var engine = new OcrEngine();
engine.ImagePath = @"C:\Images";
```

> **Definition anchor:** `RecognitionSettings` περιέχει προαιρετικές παραμέτρους όπως γλώσσα, ανάλυση και όρια μνήμης που ρυθμίζουν λεπτομερώς τη διαδικασία OCR.

## Βήμα 2: φόρτωση εικόνας και επιλογή Detect Areas Mode

Φορτώστε την εικόνα-στόχο και καθορίστε τη στρατηγική ανίχνευσης που ταιριάζει στο σενάριό σας. Το enum `DetectAreasMode` παρέχει τις τρεις επιλογές που περιγράφηκαν παραπάνω.

Το enum `DetectAreasMode` καθορίζει ποια στρατηγική ανίχνευσης (PHOTO, DOCUMENT, COMBINE) θα χρησιμοποιήσει η μηχανή.  

```csharp
engine.Image = @"C:\Images\table.png";
engine.Settings.DetectAreasMode = DetectAreasMode.PHOTO; // change as needed
```

## Βήμα 3: ανάκτηση και εμφάνιση του αναγνωρισμένου κειμένου

Μετά την ολοκλήρωση του OCR, μπορείτε να αποκτήσετε πρόσβαση στο εξαγόμενο κείμενο μέσω της ιδιότητας `Text`. Το αποτέλεσμα είναι μια συμβολοσειρά απλού κειμένου που μπορείτε να αποθηκεύσετε, να εμφανίσετε ή να ενσωματώσετε σε επόμενες διαδικασίες.

Η ιδιότητα `Text` επιστρέφει το αναγνωρισμένο αποτέλεσμα απλού κειμένου από τη μηχανή OCR.  

```csharp
engine.Recognize();
string result = engine.Text;
Console.WriteLine(result);
```

## Συχνά προβλήματα και λύσεις

| Πρόβλημα | Αιτία | Διόρθωση |
|-------|--------|-----|
| **Blank output** | Λάθος `DetectAreasMode` για τον τύπο της εικόνας | Αλλάξτε σε `DOCUMENT` ή `COMBINE` ανάλογα με τη διάταξη |
| **Garbage characters** | Εικόνα χαμηλής ανάλυσης | Παρέχετε πηγή υψηλότερης ανάλυσης ή προεπεξεργαστείτε με ενίσχυση εικόνας |
| **Timeouts on large files** | Ανεπαρκής μνήμη | Χρησιμοποιήστε `RecognitionSettings` για περιορισμό μεγέθους περιοχής ή επεξεργαστείτε τις σελίδες σε τμήματα |

## Συχνές ερωτήσεις

**Q: Είναι το Aspose.OCR για .NET κατάλληλο για εφαρμογές μεγάλης κλίμακας;**  
A: Ναι, έχει σχεδιαστεί για να διαχειρίζεται υψηλού όγκου εργασίες OCR με βελτιστοποιημένη απόδοση και χαμηλή κατανάλωση μνήμης.

**Q: Μπορώ να χρησιμοποιήσω το Aspose.OCR για .NET για αναγνώριση χειρόγραφου κειμένου;**  
A: Η βιβλιοθήκη εστιάζει σε τυπωμένο κείμενο· η αναγνώριση χειρόγραφου μπορεί να απαιτεί εξειδικευμένη μηχανή.

**Q: Ποιες μορφές εικόνας υποστηρίζονται;**  
A: Κοινές μορφές όπως PNG, JPEG, BMP και TIFF υποστηρίζονται πλήρως, συνολικά πάνω από 30 τύπους εισόδου.

**Q: Πώς μπορώ να λάβω τεχνική υποστήριξη;**  
A: Επισκεφθείτε το [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) για να θέσετε ερωτήσεις και να αλληλεπιδράσετε με την κοινότητα.

**Q: Υπάρχει διαθέσιμη δωρεάν δοκιμαστική άδεια;**  
A: Ναι, μπορείτε να εξερευνήσετε τις δυνατότητες με μια [δωρεάν δοκιμαστική άδεια](https://releases.aspose.com/).

## Καλύτερες πρακτικές για μεγιστοποίηση της ακρίβειας OCR

1. **Pre‑process images** – Εφαρμόστε διόρθωση κλίσης, ενίσχυση αντίθεσης και μείωση θορύβου πριν την επεξεργασία.  
2. **Choose the correct mode** – Χρησιμοποιήστε `PHOTO` για πυκνούς πίνακες, `DOCUMENT` για κείμενο πολλαπλών στηλών, και `COMBINE` όταν εμφανίζονται και τα δύο.  
3. **Set language explicitly** – Ορίζοντας τη γλώσσα (π.χ., `engine.Settings.Language = Language.English`) βελτιώνει την αναγνώριση χαρακτήρων.  
4. **Limit region size** – Για πολύ μεγάλες σαρώσεις, επεξεργαστείτε μία σελίδα ή περιοχή τη φορά ώστε η χρήση μνήμης να παραμένει ελεγχόμενη.  
5. **Validate output** – Εφαρμόστε απλούς ελέγχους λογικής (π.χ., αναμενόμενος αριθμός στηλών) για να εντοπίζετε λανθασμένες αναγνώσεις νωρίς.

## Συμπέρασμα

Με την εξοικείωση με το **ocr document mode** και τις επιλογές Detect Areas Mode, μπορείτε να ρυθμίσετε το Aspose.OCR για .NET ώστε να **βελτιώσετε την ακρίβεια OCR** κατά την εξαγωγή κειμένου πινάκων και άλλων δομημένων δεδομένων. Ενσωματώστε αυτές τις τεχνικές στις εφαρμογές σας για αυτοματοποίηση εισαγωγής δεδομένων, επεξεργασία τιμολογίων ή οποιοδήποτε σενάριο όπου η μετατροπή εικόνων σε αναζητήσιμο κείμενο είναι κρίσιμη. Στη συνέχεια, εξερευνήστε τις δυνατότητες ανίχνευσης γλώσσας και προσαρμοσμένων λεξικών της βιβλιοθήκης για ακόμη μεγαλύτερη ακρίβεια.

---

**Last Updated:** 2026-08-07  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< blocks/products/products-backtop-button >}}

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "table.png", new RecognitionSettings
{
    // Choose the Detect Areas Mode
    DetectAreasMode = DetectAreasMode.PHOTO
    // Other options: NONE, DOCUMENT, COMBINE
});
```

```csharp
// Display the recognized text
Console.WriteLine(result.RecognitionText);

Console.WriteLine("OCRDetectAreasMode executed successfully");
```

## Σχετικά Μαθήματα

- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/net/ocr-optimization/prepare-rectangles/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/net/text-recognition/recognize-table/)
- [Improve OCR Accuracy with Spell Checking in Images](/ocr/net/ocr-optimization/result-correction-with-spell-checking/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}