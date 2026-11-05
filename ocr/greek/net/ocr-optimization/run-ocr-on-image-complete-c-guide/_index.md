---
category: general
date: 2026-05-28
description: Εκτελέστε OCR σε εικόνα χρησιμοποιώντας C# για να διαβάσετε κείμενο από
  την εικόνα και να εξάγετε γρήγορα το κείμενο από την απόδειξη. Μάθετε τις επιλογές
  GPU και τις τεχνικές φόρτωσης.
draft: false
keywords:
- run ocr on image
- read text from image
- extract text from receipt
- load image for ocr
language: el
og_description: Εκτελέστε OCR σε εικόνα με C#. Αυτό το σεμινάριο σας δείχνει πώς να
  διαβάζετε κείμενο από εικόνα, να εξάγετε κείμενο από απόδειξη και να βελτιστοποιήσετε
  τη χρήση της GPU.
og_title: Εκτέλεση OCR σε εικόνα – Πλήρης οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Run OCR on image using C# to read text from image and extract text
    from receipt fast. Learn GPU options and loading techniques.
  headline: Run OCR on Image – Complete C# Guide
  type: TechArticle
- description: Run OCR on image using C# to read text from image and extract text
    from receipt fast. Learn GPU options and loading techniques.
  name: Run OCR on Image – Complete C# Guide
  steps:
  - name: '**Batch processing:** Re‑use a single `OcrEngine` instance for a batch
      of images; it caches language models and reduces latency.'
    text: '**Batch processing:** Re‑use a single `OcrEngine` instance for a batch
      of images; it caches language models and reduces latency.'
  - name: '**Pre‑filtering:** Apply a simple grayscale conversion and contrast boost
      before handing the image to the engine—many libraries expose a `Preprocess`
      method.'
    text: '**Pre‑filtering:** Apply a simple grayscale conversion and contrast boost
      before handing the image to the engine—many libraries expose a `Preprocess`
      method.'
  - name: '**Error logging:** Capture `ocrEngine.LastError` (if available) after each
      `Recognize()` call to diagnose failures without crashing your service.'
    text: '**Error logging:** Capture `ocrEngine.LastError` (if available) after each
      `Recognize()` call to diagnose failures without crashing your service.'
  - name: '**Thread safety:** Most OCR engines are **not** thread‑safe. If you need
      parallelism, create a separate engine per thread or use a concurrency queue.'
    text: '**Thread safety:** Most OCR engines are **not** thread‑safe. If you need
      parallelism, create a separate engine per thread or use a concurrency queue.'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Computer Vision
title: Εκτέλεση OCR σε εικόνα – Πλήρης οδηγός C#
url: /el/net/ocr-optimization/run-ocr-on-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε εικόνα – Πλήρης οδηγός C#

Έχετε ποτέ χρειαστεί να **εκτελέσετε OCR σε εικόνα** αρχεία αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι· πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν προσπαθούν για πρώτη φορά να διαβάσουν κείμενο από δεδομένα εικόνας. Τα καλά νέα είναι ότι με μερικές γραμμές C# μπορείτε να εξάγετε κείμενο από σκανάρισμα αποδείξεων, PDF ή οποιαδήποτε εικόνα. Σε αυτόν τον οδηγό θα περάσουμε από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει επίσης πώς να **φορτώσετε εικόνα για OCR**, να αξιοποιήσετε την επιτάχυνση GPU και να περιορίσετε με ασφάλεια τη χρήση μνήμης.

Με το τέλος αυτού του tutorial θα μπορείτε να:

* Αρχικοποίηση μηχανής OCR σε C#  
* **Φορτώστε εικόνα για OCR** από δίσκο ή ροή  
* **Διαβάστε κείμενο από εικόνα** με προαιρετική υποστήριξη GPU  
* **Εξάγετε κείμενο από απόδειξη** και εμφανίστε το στην κονσόλα  

Δεν απαιτούνται εξωτερικές υπηρεσίες—μόνο μια τοπική βιβλιοθήκη και ένα δείγμα εικόνας απόδειξης.

---

## Τι θα χρειαστείτε

| Προαπαιτούμενο | Αιτία |
|----------------|-------|
| .NET 6.0 SDK or later | Σύγχρονο runtime, υποστηρίζει τις τελευταίες δυνατότητες της γλώσσας |
| Μια βιβλιοθήκη OCR που εκθέτει μια κλάση `OcrEngine` (π.χ., IronOCR, Tesseract .NET wrapper) | Παρέχει τις μεθόδους `Configuration` και `Recognize` που χρησιμοποιούνται παρακάτω |
| A CUDA‑enabled GPU (optional) | Ενεργοποιεί τη σημαία `EnableGpu` για ταχύτερη επεξεργασία |
| A sample receipt image (`receipt.jpg`) | Δείχνει το βήμα **εξαγωγής κειμένου από απόδειξη** |
| Any C# IDE (Visual Studio, Rider, VS Code) | Για γρήγορη μεταγλώττιση και αποσφαλμάτωση |

Αν δεν έχετε GPU, ο κώδικας θα επιστρέψει απλώς σε λειτουργία CPU—χωρίς πρόβλημα.

![Παράδειγμα εξόδου OCR σε εικόνα](https://example.com/ocr-output.png "OCR σε εικόνα – δείγμα εξόδου κονσόλας")

*Κείμενο εναλλακτικής περιγραφής: Παράδειγμα εξόδου OCR σε εικόνα που εμφανίζει το αναγνωρισμένο κείμενο της απόδειξης.*

---

## Βήμα 1: Εκτέλεση OCR σε εικόνα – Ρύθμιση της μηχανής

Πρώτα απ' όλα: δημιουργήστε μια παρουσία της μηχανής OCR. Αυτό το αντικείμενο είναι η καρδιά της διαδικασίας· διατηρεί όλες τις λεπτομέρειες ρυθμίσεων και εκτελεί το βαρέως βάρους έργο.

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

*Γιατί είναι σημαντικό:* Η κλάση `OcrEngine` ενσωματώνει τη φυσική μηχανή OCR (Tesseract, IronOCR, κ.λπ.). Η δημιουργία μιας μόνο στιγμής και η επαναχρησιμοποίησή της σε πολλαπλές εικόνες μειώνει το κόστος και σας δίνει ένα κεντρικό σημείο για προσαρμογή ρυθμίσεων.

---

## Βήμα 2: Φόρτωση εικόνας για OCR

Πριν η μηχανή μπορέσει να διαβάσει οτιδήποτε, πρέπει να της τροφοδοτήσετε μια εικόνα. Η ιδιότητα `Image` της βιβλιοθήκης αναμένει μια ροή ή μια διαδρομή αρχείου, ανάλογα με την υλοποίηση.

```csharp
// Step 2: Load the image to be processed
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

*Συμβουλή:* Αν διαχειρίζεστε μεταφορτώσεις χρηστών, τυλίξτε αυτό σε `try/catch` και επικυρώστε πρώτα τον τύπο αρχείου. Μορφές που δεν υποστηρίζονται θα ρίξουν εξαίρεση που μπορεί να αντιμετωπιστεί με χάρη.

---

## Βήμα 3: Ενεργοποίηση επιτάχυνσης GPU (Προαιρετικό)

Αν το σύστημά σας διαθέτει συμβατό runtime CUDA ή OpenCL, η ενεργοποίηση της λειτουργίας GPU μπορεί να μειώσει δευτερόλεπτα από κάθε πέρασμα αναγνώρισης.

```csharp
// Step 3: Enable GPU acceleration (requires CUDA/OpenCL runtime)
ocrEngine.Configuration.EnableGpu = true;
```

*Pro tip:* Δεν όλα τα GPU είναι ίσα. Σε παλαιότερες κάρτες μπορεί να παρατηρήσετε μικρή καθυστέρηση λόγω του φορτίου των οδηγών. Δοκιμάστε και τις δύο διαδρομές (`EnableGpu = true/false`) για να δείτε τι λειτουργεί καλύτερα στο υλικό σας.

---

## Βήμα 4: Περιορισμός χρήσης μνήμης GPU (Προαιρετικό)

Μερικές φορές δεν θέλετε η διαδικασία OCR να καταναλώνει όλη τη μνήμη του GPU, ειδικά όταν μοιράζεστε το GPU με άλλες εργασίες όπως inference βαθιάς μάθησης.

```csharp
// Step 4: (Optional) Limit the amount of GPU memory the engine can use (in MB)
ocrEngine.Configuration.GpuMemoryLimit = 1024; // 1 GB limit
```

*Πότε να το χρησιμοποιήσετε:* Αν τρέχετε μια υπηρεσία web που επεξεργάζεται πολλές εικόνες ταυτόχρονα, ο περιορισμός μνήμης αποτρέπει καταρρίψεις λόγω έλλειψης μνήμης.

---

## Βήμα 5: Αναγνώριση κειμένου και ανάγνωση κειμένου από εικόνα

Τώρα η μηχανή είναι έτοιμη να κάνει τη δουλειά της. Η κλήση `Recognize()` εκτελεί την αλυσίδα OCR και επιστρέφει το εξαγόμενο κείμενο.

```csharp
// Step 5: Perform OCR and retrieve the recognized text
string recognizedText = ocrEngine.Recognize();
```

*Γιατί είναι το κεντρικό:* Αυτή η μοναδική γραμμή κρύβει μια αλυσίδα προεπεξεργασίας (δυαδικοποίηση, ευθυγράμμιση) και την πραγματική ταξινόμηση χαρακτήρων. Το επιστρεφόμενο `recognizedText` είναι απλό Unicode, έτοιμο για περαιτέρω επεξεργασία.

---

## Βήμα 6: Εξαγωγή κειμένου από απόδειξη – Έξοδος

Τέλος, γράψτε το αποτέλεσμα στην κονσόλα ή αποθηκεύστε το όπου χρειάζεστε. Για μια απόδειξη, μπορείτε αργότερα να αναλύσετε τις γραμμές, τα σύνολα ή τις ημερομηνίες.

```csharp
// Step 6: Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

**Αναμενόμενη έξοδος κονσόλας (προσαρμοσμένη για συντομία):**

```
=== OCR Result ===
Store Name
123 Main St.
Date: 04/27/2026
Item   Qty   Price
Apple   2    1.20
Bread   1    2.50
Total          3.70
Thank you!
```

Αν το OCR δυσκολεύεται με συγκεκριμένη διάταξη απόδειξης, σκεφτείτε να προσαρμόσετε τις επιλογές προεπεξεργασίας (π.χ., `ocrEngine.Configuration.Deskew = true`) ή να τροφοδοτήσετε εικόνα υψηλότερης ανάλυσης.

---

## Συνηθισμένες περιπτώσεις άκρων & πώς να τις αντιμετωπίσετε

| Κατάσταση | Προτεινόμενη Διόρθωση |
|-----------|------------------------|
| **Null image** – `ocrEngine.Image` is `null` | Επικυρώστε τη διαδρομή αρχείου πριν την ανάθεση· ρίξτε ένα σαφές `ArgumentException` εάν λείπει. |
| **GPU not available** – `EnableGpu = true` throws `PlatformNotSupportedException` | Τυλίξτε την κλήση ενεργοποίησης GPU σε `try/catch` και επιστρέψτε σε λειτουργία CPU. |
| **Large receipts ( > 10 MB )** cause memory pressure | Χρησιμοποιήστε `GpuMemoryLimit` ή επεξεργαστείτε την εικόνα σε πλακίδια (`ocrEngine.Configuration.TileSize`). |
| **Incorrect language detection** – output contains gibberish | Ορίστε `ocrEngine.Configuration.Language = "eng"` (ή τον κατάλληλο κωδικό ISO) για να επιβάλετε την Αγγλική. |

---

## Επαγγελματικές συμβουλές για OCR έτοιμο για παραγωγή

1. **Επεξεργασία σε παρτίδες:** Επαναχρησιμοποιήστε μια μοναδική παρουσία `OcrEngine` για μια παρτίδα εικόνων· αποθηκεύει στην κρυφή μνήμη τα μοντέλα γλώσσας και μειώνει την καθυστέρηση.  
2. **Προφίλτρινγκ:** Εφαρμόστε μια απλή μετατροπή σε κλίμακα του γκρι και ενίσχυση αντίθεσης πριν παραδώσετε την εικόνα στη μηχανή—πολλές βιβλιοθήκες εκθέτουν μέθοδο `Preprocess`.  
3. **Καταγραφή σφαλμάτων:** Συλλέξτε το `ocrEngine.LastError` (αν υπάρχει) μετά από κάθε κλήση `Recognize()` για διάγνωση αποτυχιών χωρίς να καταρρεύσει η υπηρεσία σας.  
4. **Ασφάλεια νήματος:** Οι περισσότερες μηχανές OCR **δεν** είναι ασφαλείς για πολλαπλά νήματα. Αν χρειάζεστε παραλληλισμό, δημιουργήστε ξεχωριστή μηχανή ανά νήμα ή χρησιμοποιήστε ουρά σύγκλισης.

---

## Συμπέρασμα

Μόλις περάσαμε από μια πλήρη ροή εργασίας **εκτέλεσης OCR σε εικόνα** σε C#. Ξεκινώντας από τη δημιουργία της μηχανής, **φορτώνοντας εικόνα για OCR**, ενεργοποιώντας την επιτάχυνση GPU και τελικά **εξάγοντας κείμενο από απόδειξη**, έχετε τώρα μια σταθερή βάση για να χτίσετε πιο σύνθετες γραμμές επεξεργασίας εγγράφων.

Τα επόμενα βήματα μπορεί να περιλαμβάνουν:

* Ανάλυση του κειμένου της απόδειξης σε δομημένο JSON (χρησιμοποιώντας regex ή βιβλιοθήκη φυσικής γλώσσας) – ιδανικό για αυτοματοποίηση **ανάγνωσης κειμένου από εικόνα**.  
* Ενσωμάτωση του βήματος OCR σε API ASP .NET Core ώστε οι χρήστες να μπορούν να ανεβάζουν αποδείξεις μέσω HTTP.  
* Πειραματισμός με διαφορετικά OCR back‑ends (Tesseract vs. εμπορικά SDK) για σύγκριση ακρίβειας.

Δοκιμάστε το με διάφορες διατάξεις αποδείξεων, ρυθμίστε τις παραμέτρους και θα δείτε πόσο γρήγορα μπορείτε να μετατρέψετε μια θολή φωτογραφία σε χρήσιμα δεδομένα. Καλή προγραμματιστική, και οι εικόνες σας να είναι πάντα καθαρές!

## Σχετικά Μαθήματα

- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Εξαγωγή κειμένου από εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)
- [Πώς να εξάγετε κείμενο από εικόνα προετοιμάζοντας ορθογώνια στο OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}