---
date: 2026-07-23
description: Μάθετε πώς να εξάγετε κείμενο από εικόνες χρησιμοποιώντας το Aspose.OCR
  για .NET, επιτρέποντας την αναγνώριση εικόνων OCR με βάση τους φακέλους.
keywords:
- extract text from images
- convert images to text
- ocr multiple images
lastmod: 2026-07-23
linktitle: OCROperation με φάκελο στην αναγνώριση εικόνων OCR
og_description: Εξάγετε κείμενο από εικόνες με το Aspose.OCR για .NET. Μάθετε για
  OCR με βάση φακέλους, επεξεργασία παρτίδας και βέλτιστες πρακτικές σε C# σε λίγα
  μόνο βήματα.
og_image_alt: Guide showing C# code extracting text from image files using Aspose.OCR
og_title: Εξαγωγή κειμένου από εικόνες χρησιμοποιώντας λειτουργία OCR σε φακέλους
  – Οδηγός Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how to extract text from images using Aspose.OCR for .NET, enabling
    folder‑based OCR image recognition.
  headline: Extract Text from Images Using OCR Operation on Folders
  type: TechArticle
- description: Learn how to extract text from images using Aspose.OCR for .NET, enabling
    folder‑based OCR image recognition.
  name: Extract Text from Images Using OCR Operation on Folders
  steps:
  - name: Set Document Directory
    text: Define the folder that holds the images you want to process. > **Pro tip:**
      Use an absolute path or `Path.Combine` to avoid path‑separator issues on different
      OSes.
  - name: Initialize Aspose.OCR
    text: Create an instance of the OCR engine.
  - name: Specify Image Path
    text: Point the API to the specific sub‑folder that contains your image files.
      > **Why this matters:** The `RecognizeMultipleImages` method expects a folder
      path, not a single file.
  - name: Recognize Images
    text: Run OCR on every image inside the folder. You can customize `RecognitionSettings`
      if you need language hints or specific preprocessing. `RecognitionResult` contains
      the extracted text and confidence information for a processed image.
  - name: Print Results
    text: Iterate through the returned `RecognitionResult` array and output the extracted
      text. > **Common pitfall:** Forgetting to check `result.Length` can cause an
      `IndexOutOfRangeException` when the folder is empty. Always validate the folder
      content first.
  - name: Completion Message
    text: Signal successful execution.
  type: HowTo
- questions:
  - answer: Yes, Aspose.OCR for .NET is a commercial product. For licensing information,
      visit [here](https://purchase.aspose.com/buy).
    question: Can I use Aspose.OCR for .NET in commercial projects?
  - answer: Yes, you can explore a free trial [here](https://releases.aspose.com/).
    question: Is there a free trial available?
  - answer: The documentation is available [here](https://reference.aspose.com/ocr/net/).
    question: Where can I find the documentation?
  - answer: Temporary licenses can be obtained [here](https://purchase.aspose.com/temporary-license/).
    question: How can I obtain a temporary license for evaluation?
  - answer: Visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) for community
      support.
    question: Need support or have questions?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- extract text from images
- Aspose.OCR
- C# OCR library
title: Εξαγωγή κειμένου από εικόνες χρησιμοποιώντας λειτουργία OCR σε φακέλους
url: /el/net/ocr-configuration/ocr-operation-with-folder/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνες Χρησιμοποιώντας Λειτουργία OCR σε Φακέλους

## Εισαγωγή

Καλώς ήρθατε στον κόσμο της Οπτικής Αναγνώρισης Χαρακτήρων (OCR) με **Aspose.OCR for .NET**! Εάν χρειάζεστε να **εξάγετε κείμενο από εικόνες** μαζικά—π.χ. ολόκληρο φάκελο σαρωμένων εγγράφων—αυτό το σεμινάριο σας καθοδηγεί μέσα από μια πρακτική, πραγματική λύση. Θα καλύψουμε τα πάντα, από τη ρύθμιση του έργου μέχρι την εκτύπωση του αναγνωρισμένου κειμένου, ώστε να ενσωματώσετε γρήγορα το OCR βάσει φακέλου στις εφαρμογές σας C#. Στο τέλος, θα δείτε επίσης πώς αυτή η προσέγγιση σας επιτρέπει να **μετατρέψετε εικόνες σε κείμενο**, **εξάγετε κείμενο από σαρωμένα έγγραφα**, και **διαβάζετε κείμενο εικόνας σε C#** με λίγες μόνο γραμμές κώδικα.

## Γρήγορες Απαντήσεις
- **Τι διδάσκει αυτό το σεμινάριο;** Πώς να εξάγετε κείμενο από εικόνες που αποθηκεύονται σε φάκελο χρησιμοποιώντας το Aspose.OCR.  
- **Ποια γλώσσα & πλατφόρμα;** C# με .NET (Framework ή .NET Core).  
- **Κύρια προαπαιτούμενα;** Η βιβλιοθήκη Aspose.OCR for .NET – κατεβάστε την [εδώ](https://releases.aspose.com/ocr/net/).  
- **Πόσα αποσπάσματα κώδικα;** Επτά σύντομα placeholders που απεικονίζουν κάθε βήμα.  
- **Μπορώ να μετατρέψω εικόνες σε κείμενο;** Απόλυτα—αυτό το παράδειγμα δείχνει τη μετατροπή από άκρο σε άκρο.

## Τι είναι η «εξαγωγή κειμένου από εικόνες»;
Η εξαγωγή κειμένου από εικόνες χρησιμοποιεί OCR για να μετατρέπει χαρακτήρες σε φωτογραφίες, PDF ή σαρώσεις σε επεξεργάσιμες, αναζητήσιμες αλφαριθμητικές ακολουθίες. Το Aspose.OCR παρέχει μια ισχυρή μηχανή που υποστηρίζει πολλαπλές μορφές εικόνας και γλώσσες. Αυτή η τεχνολογία επιτρέπει στους προγραμματιστές να μετατρέπουν οπτικό περιεχόμενο σε κείμενο αναγνώσιμο από μηχανές, διευκολύνοντας τη δεικτοποίηση, την αναζήτηση και τις ροές εξαγωγής δεδομένων σε ένα ευρύ φάσμα εφαρμογών.

## Γιατί να χρησιμοποιήσετε το Aspose.OCR για OCR βάσει φακέλου;
Φορτώστε ολόκληρο το φάκελο σας με μία μόνο κλήση API και αφήστε το Aspose.OCR να διαχειριστεί την ανίχνευση γλώσσας, την ανάλυση διάταξης και την επεξεργασία παρτίδων. Η μηχανή υποστηρίζει **πάνω από 70 μορφές εικόνας** (συμπεριλαμβανομένων PNG, JPEG, TIFF, BMP και WebP) και μπορεί να επεξεργαστεί αρχεία έως **2 GB** χωρίς να φορτώνει ολόκληρο το έγγραφο στη μνήμη, παρέχοντας αποτελέσματα υψηλής ακρίβειας για **πάνω από 30 γλώσσες**.

## Συνηθισμένες Περιπτώσεις Χρήσης
- Ψηφιοποίηση μιας βιβλιοθήκης σαρωμένων τιμολογίων ή αποδείξεων.  
- Μετατροπή αρχειοθετημένων αρχείων PNG/JPEG σε αναζητήσιμο κείμενο για δεικτοποίηση.  
- Αυτοματοποίηση εισαγωγής δεδομένων διαβάζοντας κείμενο από εικόνες ετικετών προϊόντων.  
- Δημιουργία λειτουργίας αναζήτησης εγγράφων που χρειάζεται να **εξάγει κείμενο από σαρωμένα έγγραφα** σε πραγματικό χρόνο.

## Προαπαιτούμενα

- Βασική εξοικείωση με C# και ανάπτυξη .NET.  
- Visual Studio (οποιαδήποτε πρόσφατη έκδοση).  
- **Βιβλιοθήκη Aspose.OCR for .NET** – κατεβάστε την [εδώ](https://releases.aspose.com/ocr/net/).  
- Κατανόηση των εννοιών OCR (προαιρετικό αλλά χρήσιμο).

## Εισαγωγή Ονομάτων Χώρων

Προσθέστε τις απαιτούμενες οδηγίες `using` στην αρχή του αρχείου C# ώστε ο μεταγλωττιστής να γνωρίζει πού βρίσκονται οι κλάσεις OCR.

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Πώς να εξάγετε κείμενο από εικόνες χρησιμοποιώντας OCR σε φακέλους;

Φορτώστε τη διαδρομή του φακέλου, δημιουργήστε μια παρουσία του μηχανήματος OCR, καλέστε τη μέθοδο `RecognizeMultipleImages` και επαναλάβετε τα αποτελέσματα για να εκτυπώσετε το κείμενο κάθε σελίδας. Αυτή η ροή από άκρο σε άκρο εκτελείται σε λιγότερο από ένα δευτερόλεπτο για μια τυπική παρτίδα 20 εικόνων σε σύγχρονο σταθμό εργασίας.

Η μέθοδος `RecognizeMultipleImages` επεξεργάζεται όλα τα υποστηριζόμενα αρχεία εικόνας σε έναν κατάλογο και επιστρέφει έναν πίνακα αντικειμένων `RecognitionResult`.  
`RecognitionSettings` σας επιτρέπει να καθορίσετε γλώσσα, προεπεξεργασία και άλλες επιλογές OCR.

### Οδηγός Βήμα‑Βήμα

### Βήμα 1: Ορισμός Καταλόγου Εγγράφου
Ορίστε το φάκελο που περιέχει τις εικόνες που θέλετε να επεξεργαστείτε.

```csharp
// ExStart:1   
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

> **Συμβουλή:** Χρησιμοποιήστε απόλυτη διαδρομή ή `Path.Combine` για να αποφύγετε προβλήματα διαχωριστών διαδρομής σε διαφορετικά λειτουργικά συστήματα.

### Βήμα 2: Αρχικοποίηση Aspose.OCR
Δημιουργήστε μια παρουσία του μηχανήματος OCR.

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Βήμα 3: Καθορισμός Διαδρομής Εικόνας
Κατευθύνετε το API στον συγκεκριμένο υποφάκελο που περιέχει τα αρχεία εικόνας.

```csharp
// Image Path
string fullPath = dataDir + "OCR";
```

> **Γιατί είναι σημαντικό:** Η μέθοδος `RecognizeMultipleImages` αναμένει μια διαδρομή φακέλου, όχι ένα μεμονωμένο αρχείο.

### Βήμα 4: Αναγνώριση Εικόνων
Εκτελέστε OCR σε κάθε εικόνα μέσα στο φάκελο. Μπορείτε να προσαρμόσετε το `RecognitionSettings` εάν χρειάζεστε υποδείξεις γλώσσας ή συγκεκριμένη προεπεξεργασία.

```csharp
// Recognize image           
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
    //default or custom
});
```

`RecognitionResult` περιέχει το εξαγόμενο κείμενο και πληροφορίες εμπιστοσύνης για μια επεξεργασμένη εικόνα.  

### Βήμα 5: Εκτύπωση Αποτελεσμάτων
Περιηγηθείτε στον επιστρεφόμενο πίνακα `RecognitionResult` και εμφανίστε το εξαγόμενο κείμενο.

```csharp
// Print result
for (int i = 0; i < result.Length; i++)
{
    Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
```

> **Κοινό λάθος:** Η παράλειψη ελέγχου του `result.Length` μπορεί να προκαλέσει `IndexOutOfRangeException` όταν ο φάκελος είναι κενός. Πάντα να επικυρώνετε το περιεχόμενο του φακέλου πρώτα.

### Βήμα 6: Μήνυμα Ολοκλήρωσης
Σήμα επιτυχούς εκτέλεσης.

```csharp
// ExEnd:1
Console.WriteLine("OCROperationWithFolder executed successfully");
```

## Συμβουλές και Καλές Πρακτικές

- **Μέγεθος παρτίδας:** Εάν επεξεργάζεστε χιλιάδες αρχεία, χωρίστε το φάκελο σε μικρότερες παρτίδες (π.χ. τμήματα 500 εικόνων) για να διατηρήσετε τη χρήση μνήμης προβλέψιμη.  
- **Υποδείξεις γλώσσας:** Η παροχή του σωστού κωδικού γλώσσας στο `RecognitionSettings` βελτιώνει δραστικά την ακρίβεια, ειδικά για μη λατινικά αλφάβητα.  
- **Ασύγχρονη επεξεργασία:** Τυλίξτε την κλήση OCR σε `Task.Run` ή χρησιμοποιήστε async/await για να διατηρήσετε τα νήματα UI ανταποκρινόμενα.  
- **Επικύρωση αρχείων:** Πριν καλέσετε το `RecognizeMultipleImages`, φιλτράρετε τον κατάλογο για υποστηριζόμενες επεκτάσεις (`.png`, `.jpg`, `.jpeg`, `.tif`, `.tiff`).  
- **Παρακολούθηση απόδοσης:** Χρησιμοποιήστε `Stopwatch` για να καταγράψετε τον χρόνο που διανύθηκε ανά παρτίδα· σε τυπική CPU 4 πυρήνων θα δείτε ~0.8 s ανά 100 εικόνες.

## Συνηθισμένα Προβλήματα & Λύσεις

| Πρόβλημα | Αιτία | Διόρθωση |
|----------|-------|----------|
| Δεν επιστρέφεται έξοδος | Λάθος ή κενή διαδρομή φακέλου | Επαληθεύστε ότι το `fullPath` δείχνει στον σωστό κατάλογο και περιέχει υποστηριζόμενες μορφές εικόνας (PNG, JPEG, TIFF). |
| Κατεστραμμένοι χαρακτήρες | Λανθασμένες ρυθμίσεις γλώσσας | Περάστε ένα ρυθμισμένο `RecognitionSettings` με `Language` ορισμένο στον κατάλληλο κωδικό ISO. |
| Καθυστέρηση απόδοσης με πολλές εικόνες | Επεξεργασία διαδοχικά στο νήμα UI | Εκτελέστε OCR σε νήμα παρασκηνίου ή χρησιμοποιήστε async μοτίβα για να διατηρήσετε το UI ανταποκρινόμενο. |

## Συχνές Ερωτήσεις

**Ε: Μπορώ να χρησιμοποιήσω το Aspose.OCR for .NET σε εμπορικά έργα;**  
Α: Ναι, το Aspose.OCR for .NET είναι εμπορικό προϊόν. Για πληροφορίες αδειοδότησης, επισκεφθείτε [εδώ](https://purchase.aspose.com/buy).

**Ε: Υπάρχει διαθέσιμη δωρεάν δοκιμή;**  
Α: Ναι, μπορείτε να δοκιμάσετε δωρεάν [εδώ](https://releases.aspose.com/).

**Ε: Πού μπορώ να βρω την τεκμηρίωση;**  
Α: Η τεκμηρίωση είναι διαθέσιμη [εδώ](https://reference.aspose.com/ocr/net/).

**Ε: Πώς μπορώ να αποκτήσω προσωρινή άδεια για αξιολόγηση;**  
Α: Προσωρινές άδειες μπορούν να ληφθούν [εδώ](https://purchase.aspose.com/temporary-license/).

**Ε: Χρειάζεστε υποστήριξη ή έχετε ερωτήσεις;**  
Α: Επισκεφθείτε το [φόρουμ Aspose.OCR](https://forum.aspose.com/c/ocr/16) για υποστήριξη της κοινότητας.

---

**Τελευταία Ενημέρωση:** 2026-07-23  
**Δοκιμή με:** Aspose.OCR 24.11 for .NET  
**Συγγραφέας:** Aspose

## Σχετικές Οδηγίες

- [Πώς να Εκτελέσετε OCR σε Παρτίδες Εικόνων με Λίστα στο Aspose.OCR for .NET](/ocr/net/ocr-configuration/ocr-operation-with-list/)
- [Πώς να Εξάγετε Κείμενο από Αρχεία ZIP Χρησιμοποιώντας το Aspose.OCR for .NET](/ocr/net/ocr-configuration/ocr-operation-with-archive/)
- [Εξαγωγή Κειμένου από Εικόνες – Ρυθμίσεις OCR με Aspose.OCR](/ocr/net/ocr-settings/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< blocks/products/products-backtop-button >}}

{{< /blocks/products/pf/main-wrap-class >}}