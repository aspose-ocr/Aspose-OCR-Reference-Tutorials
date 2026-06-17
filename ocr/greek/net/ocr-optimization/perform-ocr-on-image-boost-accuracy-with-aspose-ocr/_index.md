---
category: general
date: 2026-03-15
description: Εκτελέστε OCR σε εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε πώς
  να προεπεξεργάζεστε την εικόνα πριν το OCR για να βελτιώσετε την ακρίβεια του OCR
  και να αναγνωρίζετε κείμενο από την εικόνα αποδοτικά.
draft: false
keywords:
- perform OCR on image
- recognize text from image
- improve OCR accuracy
- preprocess image before OCR
language: el
og_description: Εκτελέστε OCR σε εικόνα με το Aspose OCR. Αυτός ο οδηγός δείχνει πώς
  να προεπεξεργαστείτε την εικόνα πριν το OCR, να βελτιώσετε την ακρίβεια του OCR
  και να αναγνωρίσετε κείμενο από την εικόνα σε C#.
og_title: Εκτελέστε OCR σε εικόνα – Αυξήστε την ακρίβεια με το Aspose OCR
tags:
- C#
- Aspose OCR
- Image Processing
title: Εκτελέστε OCR σε εικόνα – Αυξήστε την ακρίβεια με το Aspose OCR
url: /el/net/ocr-optimization/perform-ocr-on-image-boost-accuracy-with-aspose-ocr/
---

are not actual code blocks but placeholders. They should stay as is.

Also there are block shortcodes at top and bottom.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε Εικόνα – Βελτιώστε την Ακρίβεια με το Aspose OCR

Έχετε ποτέ χρειαστεί να **εκτελέσετε OCR σε αρχεία εικόνας** αλλά έχετε συνεχώς λησμονημένα αποτελέσματα; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα, μια θορυβώδης, κεκλιμένη σάρωση μπορεί να αποπροσανατολίσει ακόμη και τις καλύτερες μηχανές OCR, αφήνοντάς σας με κείμενο που μοιάζει με κάτι που πληκτρολόγησε μια γάτα που περπατά πάνω από το πληκτρολόγιο.

Το θέμα είναι το εξής: η ακατέργαστη εικόνα είναι μόνο το ήμισυ του αγώνα. Με το **προεπεξεργασία εικόνας πριν το OCR**, μπορείτε να **βελτιώσετε δραματικά την ακρίβεια του OCR** και τελικά να **αναγνωρίσετε κείμενο από εικόνα** αξιόπιστα. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο προς εκτέλεση παράδειγμα C# που δείχνει ακριβώς πώς να το κάνετε αυτό με το Aspose.OCR.

Θα καλύψουμε:

* Εγκατάσταση του πακέτου NuGet Aspose.OCR.  
* Δημιουργία μιας αλυσίδας προεπεξεργασίας (απλοποίηση κλίσης, αποθόρυβο, ενίσχυση αντίθεσης, δυαδικοποίηση).  
* Εκτέλεση της μηχανής OCR και εκτύπωση του αναγνωρισμένου κειμένου.  

Καμία περιττή πληροφορία, χωρίς «δείτε τα έγγραφα αργότερα» συντομεύσεις — μόνο μια αυτόνομη λύση που μπορείτε να ενσωματώσετε σε μια εφαρμογή κονσόλας αμέσως.

---

## Τι Θα Χρειαστείτε

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

* **.NET 6+** (ή .NET Framework 4.6.2+).  
* Ένα πρόσφατο πακέτο **Aspose.OCR** NuGet (v23.10 ή νεότερο).  
* Ένα αρχείο εικόνας που είναι λίγο ακατάστατο — σκεφτείτε κεκλιμένη, θορυβώδη, χαμηλής αντίθεσης.  
* Visual Studio, VS Code ή οποιοδήποτε IDE προτιμάτε.

Αυτό είναι όλο. Αν λείπει το πακέτο NuGet, τρέξτε:

```bash
dotnet add package Aspose.OCR
```

Τώρα ας βάλουμε τα χέρια μας στη δουλειά.

---

## ## Εκτέλεση OCR σε Εικόνα – Ρύθμιση της Μηχανής

Το πρώτο βήμα είναι η δημιουργία ενός αντικειμένου `OcrEngine`. Αυτό το αντικείμενο είναι η καρδιά του Aspose OCR· περιέχει τις ρυθμίσεις, τις αλυσίδες και τη λογική αναγνώρισης.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System.Drawing;          // For Image class
using System;                  // For Console

// Step 1: Instantiate the OCR engine
var ocrEngine = new OcrEngine();
```

> **Γιατί είναι σημαντικό:**  
> Η δημιουργία της μηχανής σας δίνει ένα καθαρό ξεκίνημα. Μπορείτε αργότερα να αλλάξετε τις ρυθμίσεις (γλώσσα, λειτουργία αναγνώρισης κ.λπ.) χωρίς να αγγίξετε το υπόλοιπο κώδικα.

---

## ## Προεπεξεργασία Εικόνας Πριν το OCR – Δημιουργία της Αλυσίδας

Οι ακατέργαστες σάρωσες σπάνια είναι τέλειες. Μια καλή αλυσίδα προεπεξεργασίας μπορεί να **βελτιώσει την ακρίβεια του OCR** έως και 30 % σε ορισμένες περιπτώσεις. Παρακάτω ενώνουμε τέσσερα φίλτρα:

| Φίλτρο | Τι κάνει | Τυπικές τιμές |
|--------|----------|---------------|
| `DeskewFilter` | Ανιχνεύει και διορθώνει την περιστροφή | `Angle = 0.0` (αυτόματη ανίχνευση) |
| `DenoiseFilter` | Αφαιρεί σπασίματα & κόκκο | `Strength = 70` (από 100) |
| `ContrastBoostFilter` | Κάνει το σκοτεινό κείμενο πιο εμφανές | `Strength = 40` |
| `BinarizationFilter` | Μετατρέπει την εικόνα σε καθαρό ασπρόμαυρο | `Threshold = 128` |

```csharp
// Step 2: Create a preprocessing pipeline
var preprocessingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { Angle = 0.0 })               // auto‑detect skew angle
    .Add(new DenoiseFilter { Strength = 70 })           // reduce noise
    .Add(new ContrastBoostFilter { Strength = 40 })     // enhance contrast
    .Add(new BinarizationFilter { Threshold = 128 });   // convert to B/W

// Attach the pipeline to the OCR engine
ocrEngine.Configuration.PreProcessing = preprocessingPipeline;
```

> **Συμβουλή επαγγελματία:** Αν οι πηγές εικόνας είναι ήδη καθαρές, μπορείτε να παραλείψετε το `DenoiseFilter` ή να μειώσετε το `Strength`. Η υπερβολική φιλτράρισμα μπορεί μερικές φορές να διαγράψει αδύνατους χαρακτήρες.

---

## ## Φόρτωση της Εικόνας – Πού Βρίσκετε το Αρχείο Σας

Τώρα δείχνουμε στη μηχανή την εικόνα που θέλουμε να διαβάσουμε. Η μέθοδος `Image.FromFile` λειτουργεί με οποιαδήποτε μορφή υποστηρίζεται από το System.Drawing (JPEG, PNG, BMP κ.λπ.).

```csharp
// Step 3: Load the image you want to recognize
var inputImagePath = @"C:\Images\skewed_noisy.jpg";   // change to your path
var inputImage = Image.FromFile(inputImagePath);
```

> **Περίπτωση άκρης:** Αν η διαδρομή του αρχείου περιέχει κενά ή χαρακτήρες Unicode, τυλίξτε την σε αλφαριθμητικό ακριβούς μορφής (`@"..."`) όπως φαίνεται παραπάνω. Επίσης, πάντα διαχειριστείτε το `FileNotFoundException` σε κώδικα παραγωγής.

---

## ## Αναγνώριση Κειμένου από Εικόνα – Εκτέλεση της Μηχανής OCR

Με τη μηχανή ρυθμισμένη και την εικόνα φορτωμένη, η πραγματική αναγνώριση είναι μια μόνο γραμμή. Το αποτέλεσμα περιέχει το εξαγόμενο κείμενο μαζί με μετρικές εμπιστοσύνης που μπορείτε να εξετάσετε αργότερα.

```csharp
// Step 4: Perform OCR and get the result
var ocrResult = ocrEngine.Recognize(inputImage);

// Display the recognized text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

Όταν τρέξετε το πρόγραμμα, θα πρέπει να δείτε κάτι σαν:

```
=== OCR Output ===
Invoice #12345
Date: 03/12/2026
Total: $1,250.00
```

Αν το αποτέλεσμα φαίνεται λανθασμένο, ρυθμίστε τις δυνάμεις της αλυσίδας ή πειραματιστείτε με διαφορετική τιμή `Threshold`. Μικρές προσαρμογές συχνά κάνουν μεγάλη διαφορά.

---

## ## Συνηθισμένα Πιθανά Σφάλματα & Πώς να Τα Διορθώσετε

1. **Το αποτέλεσμα είναι κενό ή κυρίως ακαταλαβίστικο**  
   *Ελέγξτε την αλυσίδα.* Πολύ επιθετικός αποθόρυβος μπορεί να διαγράψει λεπτές γραμμές. Μειώστε το `Strength` ή σχολιάστε προσωρινά το φίλτρο.

2. **Η κλίση δεν διορθώνεται**  
   Το `DeskewFilter` λειτουργεί καλύτερα σε έγγραφα όπου η βάση του κειμένου είναι περίπου οριζόντια. Αν η εικόνα είναι περιστραμμένη περισσότερο από 15°, ίσως χρειαστεί να την προ‑στρέψετε χειροκίνητα χρησιμοποιώντας `RotateFlip`.

3. **Μη‑λατινικοί χαρακτήρες δεν αναγνωρίζονται**  
   Από προεπιλογή το Aspose OCR χρησιμοποιεί αγγλικά μοντέλα γλώσσας. Ορίστε `ocrEngine.Configuration.Language` στον κατάλληλο κωδικό ISO (π.χ., `"fr"` για γαλλικά) πριν καλέσετε το `Recognize`.

```csharp
ocrEngine.Configuration.Language = "fr";   // for French text
```

4. **Η απόδοση είναι αργή**  
   Αν επεξεργάζεστε εκατοντάδες σελίδες, επαναχρησιμοποιήστε ένα μόνο αντικείμενο `OcrEngine` και αντικαταστήστε μόνο το αντικείμενο `Image` σε κάθε βρόχο. Η δημιουργία νέας μηχανής κάθε φορά προσθέτει περιττό φόρτο.

---

## ## Οπτικό Αποτέλεσμα – Πώς Φαίνεται η Προεπεξεργασμένη Εικόνα

Παρακάτω υπάρχει μια γρήγορη εικονογράφηση πριν‑και‑μετά (το πραγματικό σας αποτέλεσμα μπορεί να διαφέρει).

![Perform OCR on Image result](https://example.com/ocr-before-after.png "Perform OCR on Image – preprocessed vs original")

*Alt text:* “Perform OCR on Image – σύγκριση αρχικής θορυβώδους σάρωσης και προεπεξεργασμένης έκδοσης έτοιμης για OCR”.

---

## ## Συμπλήρωση: Πλήρες Παράδειγμα Λειτουργίας

Αντιγράψτε ολόκληρο το παρακάτω απόσπασμα σε ένα νέο έργο κονσόλας (`dotnet new console`) και πατήστε **F5**. Θα μεταγλωττιστεί, θα τρέξει και θα εκτυπώσει το αναγνωρισμένο κείμενο στην κονσόλα.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System.Drawing;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build a preprocessing pipeline (improve OCR accuracy)
        var preprocessingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { Angle = 0.0 })               // auto‑detect skew angle
            .Add(new DenoiseFilter { Strength = 70 })           // reduce noise
            .Add(new ContrastBoostFilter { Strength = 40 })     // enhance contrast
            .Add(new BinarizationFilter { Threshold = 128 });   // convert to B/W

        ocrEngine.Configuration.PreProcessing = preprocessingPipeline;

        // 3️⃣ Load the image you want to read
        var imagePath = @"YOUR_DIRECTORY\skewed_noisy.jpg";   // ← update this path
        var inputImage = Image.FromFile(imagePath);

        // 4️⃣ Run OCR – recognize text from image
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Show the result
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Η κονσόλα εκτυπώνει την απλή κειμενική έκδοση ό,τι υπήρχε στην εικόνα — είτε είναι τιμολόγιο, σάρωση διαβατηρίου ή χειρόγραφη σημείωση.

---

## ## Επόμενα Βήματα – Περαιτέρω Εξέλιξη

* **Επεξεργασία παρτίδας:** Τυλίξτε την κλήση αναγνώρισης μέσα σε βρόχο `foreach` για να διαχειριστείτε έναν φάκελο εικόνων.  
* **Πακέτα γλώσσας:** Εγκαταστήστε πρόσθετα δεδομένα γλώσσας από το Aspose για **αναγνώριση κειμένου από εικόνα** στα Ισπανικά, Γερμανικά, Κινέζικα κ.λπ.  
* **Προσαρμοσμένη μεταεπεξεργασία:** Χρησιμοποιήστε κανονικές εκφράσεις για να εξάγετε ημερομηνίες, ποσά ή αριθμούς ταυτοποίησης από το OCR string.  
* **Εναλλακτικές βιβλιοθήκες:** Συγκρίνετε τα αποτελέσματα με το Tesseract ή το Microsoft Azure Computer Vision για να δείτε πώς το **προεπεξεργασία εικόνας πριν το OCR** συγκρίνεται μεταξύ πλατφορμών.

---

## ## Συμπέρασμα

Δείξαμε πώς να **εκτελέσετε OCR σε αρχεία εικόνας** χρησιμοποιώντας το Aspose OCR, να χτίσουμε μια έξυπνη αλυσίδα προεπεξεργασίας, και να δούμε ότι το **προεπεξεργασία εικόνας πριν το OCR** μπορεί να **βελτιώσει δραματικά την ακρίβεια του OCR**. Ακολουθώντας τα παραπάνω βήματα μπορείτε πλέον να **αναγνωρίζετε κείμενο από εικόνα** αξιόπιστα σε οποιαδήποτε εφαρμογή C# — χωρίς να παλεύετε πια με ακατάληπτο κείμενο.

Μη διστάσετε να πειραματιστείτε με τις δυνάμεις των φίλτρων, να δοκιμάσετε διαφορετικές μορφές εικόνας ή να ενσωματώσετε αυτόν τον κώδικα σε μια μεγαλύτερη υπηρεσία επεξεργασίας εγγράφων. Ο ουρανός είναι το όριο μόλις η αλυσίδα OCR είναι σταθερή.

Έχετε ερωτήσεις ή ένα ενδιαφέρον σενάριο χρήσης; Αφήστε ένα σχόλιο παρακάτω, και καλή κωδικοποίηση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}