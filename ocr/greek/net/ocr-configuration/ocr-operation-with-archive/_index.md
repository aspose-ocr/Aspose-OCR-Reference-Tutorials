---
date: 2026-08-17
description: Μάθετε πώς να εξάγετε κείμενο χρησιμοποιώντας OCR από αρχεία ZIP με το
  Aspose.OCR για .NET. Ρύθμιση βήμα προς βήμα, κώδικας και αντιμετώπιση προβλημάτων
  για τη μετατροπή εικόνων μέσα σε ένα zip σε αναζητήσιμο κείμενο.
keywords:
- extract text using ocr
- extract text from zip
- Aspose OCR .NET
lastmod: 2026-08-17
linktitle: Πώς να εξάγετε κείμενο χρησιμοποιώντας OCR από αρχεία ZIP με το Aspose.OCR
  για .NET
og_description: Εξαγωγή κειμένου χρησιμοποιώντας OCR από αρχεία ZIP με το Aspose.OCR
  για .NET. Ακολουθήστε αυτό το πλήρες οδηγό για να διαβάσετε εικόνες μέσα σε ένα
  zip και να λάβετε αναζητήσιμο κείμενο.
og_image_alt: Screenshot of Aspose.OCR extracting text from images inside a ZIP file
og_title: Εξαγωγή κειμένου χρησιμοποιώντας OCR από αρχεία ZIP – Οδηγός Aspose.OCR
  .NET
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Learn how to extract text using OCR from ZIP archives with Aspose.OCR
    for .NET. Step‑by‑step setup, code, and troubleshooting for converting images
    inside a zip to searchable text.
  headline: How to extract text using OCR from ZIP archives with Aspose.OCR for .NET
  type: TechArticle
- questions:
  - answer: Yes, a free trial is available for evaluation, but a licensed version
      is required for production deployments.
    question: Can I use Aspose.OCR for .NET without a license?
  - answer: '`RecognizeMultipleImages` works with standard ZIP files only. For encrypted
      archives, extract the images with a third‑party ZIP library first, then feed
      the image array to the OCR engine.'
    question: Does the library support password‑protected ZIP archives?
  - answer: Enable `RecognitionSettings.EnableHandwritingRecognition` and set a higher
      DPI (e.g., 300) to give the engine more pixel data to work with.
    question: How can I improve accuracy for handwritten notes?
  - answer: Each `RecognitionResult` includes a `Confidence` property (0‑100 %). You
      can log or filter results based on this score.
    question: Is there a way to obtain confidence scores for each line of text?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- extract text using ocr
- Aspose OCR
- zip archive processing
- .NET OCR tutorial
title: Πώς να εξάγετε κείμενο χρησιμοποιώντας OCR από αρχεία ZIP με το Aspose.OCR
  για .NET
url: /el/net/ocr-configuration/ocr-operation-with-archive/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εξάγετε κείμενο χρησιμοποιώντας OCR από αρχεία ZIP με Aspose.OCR για .NET

Σε αυτό το **tutorial** θα ανακαλύψετε **πώς να εξάγετε κείμενο χρησιμοποιώντας OCR από αρχεία ZIP** με Aspose.OCR για .NET. Είτε χρειάζεστε να μετατρέψετε σαρωμένες εικόνες σε αναζητήσιμες συμβολοσειρές, να δημιουργήσετε μια παγκόσμια διαδικασία εισαγωγής εικόνων, είτε να δημιουργήσετε μια αναζητήσιμη αποθήκη εγγράφων, τα παρακάτω βήματα καλύπτουν τα πάντα—από την εγκατάσταση της βιβλιοθήκης μέχρι την εκτύπωση του αναγνωρισμένου κειμένου για κάθε εικόνα μέσα σε ένα αρχείο ZIP.

## Εισαγωγή

Η Οπτική Αναγνώριση Χαρακτήρων (OCR) μετατρέπει εικόνες raster σε επεξεργάσιμο, αναζητήσιμο κείμενο. Όταν αυτές οι εικόνες είναι συσκευασμένες σε αρχείο ZIP, η επεξεργασία κάθε εικόνας ξεχωριστά γίνεται κουραστική. Η μέθοδος `RecognizeMultipleImages` του Aspose.OCR σας επιτρέπει να τροφοδοτήσετε ολόκληρο το αρχείο στην μηχανή, εξάγοντας αυτόματα κάθε εικόνα και επιστρέφοντας το κείμενό της σε μία κλήση. Αυτή η προσέγγιση εξοικονομεί χρόνο I/O, μειώνει τη χρήση μνήμης και κλιμακώνεται σε εκατοντάδες εικόνες ανά αρχείο.

## Γρήγορες απαντήσεις
- **Τι καλύπτει αυτό το tutorial;** Εξαγωγή κειμένου χρησιμοποιώντας OCR από αρχεία ZIP με Aspose.OCR για .NET.  
- **Ποια κύρια λέξη-κλειδί στοχεύεται;** *extract text using ocr*.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση· απαιτείται εμπορική άδεια για παραγωγή.  
- **Ποιες εκδόσεις .NET υποστηρίζονται;** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Μπορώ να προσαρμόσω τις ρυθμίσεις αναγνώρισης;** Ναι—χρησιμοποιήστε `RecognitionSettings` για να ρυθμίσετε την ακρίβεια για διαφορετικές γλώσσες ή ποιότητες εικόνας.

## Τι είναι το OCR και γιατί να το χρησιμοποιήσετε σε αρχεία ZIP;

Το OCR (Optical Character Recognition) είναι η τεχνολογία που διαβάζει τυπωμένους ή χειρόγραφους χαρακτήρες από αρχεία εικόνας και τους επιστρέφει ως κείμενο Unicode. Η άμεση εφαρμογή του OCR σε ένα αρχείο ZIP εξαλείφει την ανάγκη ξεχωριστού βήματος εξαγωγής, επιτρέποντάς σας να επεξεργαστείτε δεκάδες ή εκατοντάδες εικόνες με μία κλήση API.

## Προαπαιτούμενα

- Visual Studio 2019 ή νεότερο (ή οποιοδήποτε IDE συμβατό με .NET).  
- .NET Framework 4.5 + ή .NET Core 3.1 + εγκατεστημένο.  
- Πρόσβαση στη βιβλιοθήκη Aspose.OCR για .NET (σύνδεσμος λήψης παρακάτω).  
- Έγκυρη άδεια Aspose.OCR για παραγωγική χρήση (διαθέσιμη δοκιμαστική έκδοση).

## Εισαγωγή ονομάτων χώρων

Το namespace `Aspose.OCR` παρέχει τον πυρήνα της μηχανής OCR, ενώ τα `System.IO` και `System.IO.Compression` διαχειρίζονται λειτουργίες συστήματος αρχείων και ZIP.

Η κλάση `Aspose.OCR` είναι το αντικείμενο υψηλότερου επιπέδου του Aspose.OCR που αντιπροσωπεύει τη μηχανή OCR και εκθέτει μεθόδους όπως `RecognizeMultipleImages`.  
```csharp
using Aspose.OCR;
using System.IO;
using System.IO.Compression;
```
```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Λήψη και εγκατάσταση Aspose.OCR για .NET

Κατεβάστε το πιο πρόσφατο πακέτο από τη σελίδα κυκλοφοριών **[Σελίδα κυκλοφοριών Aspose OCR .NET](https://releases.aspose.com/ocr/net/)** και ακολουθήστε τα τυπικά βήματα εγκατάστασης μέσω NuGet ή χειροκίνητα.

## Απόκτηση άδειας

Αποκτήστε άδεια από τη **[σελίδα αγοράς](https://purchase.aspose.com/buy)** ή δοκιμάστε τη **[δωρεάν δοκιμή](https://releases.aspose.com/)**. Τοποθετήστε το αρχείο άδειας στη ρίζα του έργου σας και φορτώστε το κατά την εκτέλεση όπως περιγράφεται στην τεκμηρίωση του Aspose.

## Βήμα 1: ρυθμίστε τον φάκελο εγγράφων σας

Ξεκινήστε αρχικοποιώντας τη διαδρομή προς το φάκελο που περιέχει το αρχείο ZIP που θέλετε να επεξεργαστείτε. Η χρήση του `Path.Combine` εγγυάται το σωστό διαχωριστικό καταλόγου σε Windows, Linux και macOS.

```csharp
string basePath = Path.Combine(Environment.CurrentDirectory, "Data");
string zipPath   = Path.Combine(basePath, "ImagesArchive.zip");
```
```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";
// ExEnd:1
```

> **Συμβουλή:** Αποθηκεύστε μεγάλα αρχεία ZIP εκτός του φακέλου του έργου και αναφερθείτε σε αυτά με απόλυτη διαδρομή για να αποφύγετε τυχαία προσθήκη στον έλεγχο πηγής.

## Βήμα 2: αρχικοποίηση Aspose.OCR

Δημιουργήστε μια παρουσία της μηχανής OCR. Η κλάση `AsposeOcr` είναι το σημείο εισόδου για όλες τις λειτουργίες αναγνώρισης και πρέπει να δημιουργηθεί πριν κληθούν οποιεσδήποτε μέθοδοι OCR.

```csharp
AsposeOcr ocrEngine = new AsposeOcr();
```
```csharp
// ExStart:3
AsposeOcr api = new AsposeOcr();
// ExEnd:3
```

## Βήμα 3: καθορίστε τη διαδρομή του αρχείου ZIP

Ορίστε τη πλήρη διαδρομή του συστήματος αρχείων προς το αρχείο σας. Η διαδρομή πρέπει να δείχνει σε ένα έγκυρο αρχείο `.zip`; διαφορετικά η μηχανή θα εγείρει `FileNotFoundException`.

```csharp
string archivePath = zipPath;   // already built in Step 1
```
```csharp
// ExStart:4
string fullPath = dataDir + "OCR.zip";
// ExEnd:4
```

## Βήμα 4: αναγνώριση εικόνων μέσα στο ZIP

Εκτελέστε OCR στο αρχείο χρησιμοποιώντας τις προεπιλεγμένες ρυθμίσεις ή ένα προσαρμοσμένο αντικείμενο `RecognitionSettings`. Αυτή η ενιαία κλήση εξάγει κάθε εικόνα από το ZIP και επιστρέφει μια συλλογή αντικειμένων `RecognitionResult`.

Η κλάση `RecognitionResult` αντιπροσωπεύει το αποτέλεσμα OCR για μία εικόνα, περιλαμβάνοντας το εξαγόμενο κείμενο, το σκορ εμπιστοσύνης και τον δείκτη εικόνας μέσα στο αρχείο.  
```csharp
RecognitionSettings settings = new RecognitionSettings
{
    Language = Language.English,
    Dpi = 300,
    EnableHandwritingRecognition = false
};

RecognitionResult[] results = ocrEngine.RecognizeMultipleImages(archivePath, settings);
```
```csharp
// ExStart:5
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
   //default or custom settings
});
// ExEnd:5
```

> Μπορείτε να προσαρμόσετε το `RecognitionSettings` για να βελτιώσετε την ακρίβεια για συγκεκριμένες γλώσσες, να αυξήσετε το DPI για σαρώσεις υψηλότερης ανάλυσης ή να ενεργοποιήσετε την αναγνώριση χειρόγραφου όταν χρειάζεται.

## Βήμα 5: εκτύπωση του εξαγόμενου κειμένου

Διατρέξτε τον πίνακα `RecognitionResult` και εμφανίστε το κείμενο για κάθε εικόνα. Η ιδιότητα `Confidence` (0‑100) σας επιτρέπει να φιλτράρετε αναγνώσεις χαμηλής ποιότητας.

```csharp
for (int i = 0; i < results.Length; i++)
{
    Console.WriteLine($"Image {i + 1}:");
    Console.WriteLine(results[i].Text);
    Console.WriteLine($"Confidence: {results[i].Confidence}%");
    Console.WriteLine(new string('-', 40));
}
```
```csharp
// ExStart:6
for (int i = 0; i < result.Length; i++)
{
	 Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
// ExEnd:6
```

Η κονσόλα τώρα εμφανίζει κάθε δείκτη εικόνας ακολουθούμενο από τη αναγνωρισμένη συμβολοσειρά, εξάγοντας αποτελεσματικά **κείμενο χρησιμοποιώντας OCR από zip** και μετατρέποντας μια συλλογή εικόνων σε αναζητήσιμο περιεχόμενο.

## Γιατί αυτή η προσέγγιση έχει σημασία

Η επεξεργασία εικόνων απευθείας από αρχείο ZIP μειώνει τις λειτουργίες I/O έως και 60 % σε σύγκριση με την προεξαγωγή αρχείων, και η μηχανή OCR μπορεί να διαχειριστεί αρχεία που περιέχουν **έως 500 εικόνες** σε μία κλήση χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη. Αυτή η δυνατότητα παρτίδας καθιστά τη λύση ιδανική για μεγάλης κλίμακας έργα ψηφιοποίησης, αυτοματοποιημένες γραμμές επεξεργασίας τιμολογίων και οποιοδήποτε σενάριο όπου χρειάζεται να μετατρέψετε μαζικές συλλογές εικόνων σε αναζητήσιμο κείμενο.

## Συχνά προβλήματα & αντιμετώπιση

| Πρόβλημα | Αιτία | Λύση |
|----------|-------|------|
| Δεν επιστράφηκε κείμενο | Ποιότητα εικόνας πολύ χαμηλή | Προεπεξεργασία εικόνων (δυαδικοποίηση, ενίσχυση αντίθεσης) ή αύξηση του `RecognitionSettings.Dpi` σε 300‑600 |
| Εξαίρεση κατά την ανάγνωση ZIP | Μη έγκυρη διαδρομή αρχείου ή έλλειψη δικαιωμάτων ανάγνωσης | Επαληθεύστε ότι το `archivePath` δείχνει σε υπάρχον αρχείο `.zip` και ότι η διαδικασία έχει πρόσβαση στο σύστημα αρχείων |
| Η άδεια δεν εφαρμόστηκε | Απουσία αρχείου άδειας ή το `SetLicense` δεν κλήθηκε έγκαιρα | Καλέστε `new License().SetLicense("Aspose.OCR.lic");` πριν δημιουργήσετε την παρουσία `AsposeOcr` |

## Συχνές ερωτήσεις

**Q: Μπορώ να χρησιμοποιήσω το Aspose.OCR για .NET χωρίς άδεια;**  
A: Ναι, υπάρχει δωρεάν δοκιμή για αξιολόγηση, αλλά απαιτείται έκδοση με άδεια για παραγωγικές εγκαταστάσεις.

**Q: Η βιβλιοθήκη υποστηρίζει αρχεία ZIP με κωδικό πρόσβασης;**  
A: `RecognizeMultipleImages` λειτουργεί μόνο με τυπικά αρχεία ZIP. Για κρυπτογραφημένα αρχεία, εξάγετε πρώτα τις εικόνες με βιβλιοθήκη ZIP τρίτου μέρους, έπειτα τροφοδοτήστε τον πίνακα εικόνων στη μηχανή OCR.

**Q: Πώς μπορώ να βελτιώσω την ακρίβεια για χειρόγραφες σημειώσεις;**  
A: Ενεργοποιήστε `RecognitionSettings.EnableHandwritingRecognition` και ορίστε υψηλότερο DPI (π.χ., 300) για να δώσετε στη μηχανή περισσότερα δεδομένα pixel.

**Q: Υπάρχει τρόπος να λάβετε σκορ εμπιστοσύνης για κάθε γραμμή κειμένου;**  
A: Κάθε `RecognitionResult` περιλαμβάνει την ιδιότητα `Confidence` (0‑100 %). Μπορείτε να καταγράψετε ή να φιλτράρετε τα αποτελέσματα βάσει αυτού του σκορ.

## Πρόσθετοι πόροι

- **Φόρουμ Aspose.OCR:** Για υποστήριξη κοινότητας και προχωρημένα σενάρια, επισκεφθείτε το [Φόρουμ Aspose.OCR](https://forum.aspose.com/c/ocr/16).  
- **Προσωρινή άδεια:** Εάν χρειάζεστε κλειδί αξιολόγησης βραχυπρόθεσμης διάρκειας, ζητήστε μια [προσωρινή άδεια](https://purchase.aspose.com/temporary-license/).  
- **Επίσημη τεκμηρίωση:** Μείνετε ενημερωμένοι για τις τελευταίες αλλαγές API εξετάζοντας την [τεκμηρίωση](https://reference.aspose.com/ocr/net/).

---

**Τελευταία ενημέρωση:** 2026-08-17  
**Δοκιμή με:** Aspose.OCR 24.11 for .NET  
**Συγγραφέας:** Aspose

## Σχετικά μαθήματα

- [Εξαγωγή κειμένου από εικόνες χρησιμοποιώντας λειτουργία OCR σε φακέλους](/ocr/net/ocr-configuration/ocr-operation-with-folder/)
- [Πώς να επεξεργαστείτε εικόνες OCR σε παρτίδες με λίστα στο Aspose.OCR για .NET](/ocr/net/ocr-configuration/ocr-operation-with-list/)
- [Εξαγωγή κειμένου από εικόνες – Ρυθμίσεις OCR με Aspose.OCR](/ocr/net/ocr-settings/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}