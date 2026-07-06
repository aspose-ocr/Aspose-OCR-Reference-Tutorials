---
category: general
date: 2026-02-13
description: Πώς να χρησιμοποιήσετε OCR σε C# για να εξάγετε κείμενο από εικόνα, να
  αναγνωρίσετε κείμενο από φωτογραφία ή JPG και να εκτελέσετε OCR σε εικόνα χωρίς
  internet.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from photo
- recognize text from jpg
- run OCR on image
language: el
og_description: Πώς να χρησιμοποιήσετε OCR σε C# για να εξάγετε κείμενο από εικόνα,
  να αναγνωρίσετε κείμενο από φωτογραφία και να εκτελέσετε OCR σε εικόνα με ένα πλήρες,
  εκτελέσιμο παράδειγμα.
og_title: Πώς να χρησιμοποιήσετε OCR σε C# – Εξαγωγή κειμένου από εικόνα
tags:
- OCR
- C#
- Image Processing
title: Πώς να χρησιμοποιήσετε OCR σε C# – Εξαγωγή κειμένου από εικόνα και αναγνώριση
  κειμένου από φωτογραφία
url: /el/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-and-recognize-te/
---

"Πώς να Χρησιμοποιήσετε OCR σε C# – Εξαγωγή Κειμένου από Εικόνα και Αναγνώριση Κειμένου από Φωτογραφία"

Proceed.

Now translate paragraphs.

Will keep **how to use OCR** etc.

Let's produce.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε OCR σε C# – Εξαγωγή Κειμένου από Εικόνα και Αναγνώριση Κειμένου από Φωτογραφία

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε OCR** για να εξάγετε λέξεις από ένα στιγμιότυπο οθόνης, μια σαρωμένη απόδειξη ή μια τυχαία φωτογραφία που τραβήξατε με το τηλέφωνό σας; Δεν είστε οι μόνοι. Σε πολλές πραγματικές εφαρμογές πρέπει να μετατρέπουμε εικόνες σε αναζητήσιμο κείμενο, και το να το κάνουμε τοπικά — χωρίς μια ασταθή σύνδεση στο διαδίκτυο — μπορεί να φαίνεται σαν γρίφος.

Γι' αυτό αυτός ο οδηγός σας δείχνει βήμα‑βήμα πώς να **εξάγετε κείμενο από αρχεία εικόνας** χρησιμοποιώντας μια μηχανή OCR σε C#, και καλύπτει επίσης πώς να **αναγνωρίσετε κείμενο από φωτογραφία**, **αναγνωρίσετε κείμενο από JPG**, και **να τρέξετε OCR σε εικόνα** που βρίσκεται απευθείας στον δίσκο σας. Στο τέλος θα έχετε ένα πλήρες πρόγραμμα, έτοιμο για αντιγραφή‑επικόλληση, που λειτουργεί αμέσως.

## Τι Θα Μάθετε

- Πώς να ρυθμίσετε μια μηχανή OCR για Απλοποιημένα Κινέζικα (ή οποιαδήποτε γλώσσα προσθέσετε).  
- Τον ακριβή κώδικα που απαιτείται για **φόρτωση πόρων** από τοπικό φάκελο — χωρίς κλήσεις δικτύου.  
- Πώς να **αναγνωρίσετε κείμενο από φωτογραφία** σε αρχεία όπως JPEG, PNG ή BMP.  
- Συμβουλές για την αντιμετώπιση κοινών περιπτώσεων, όπως ελλιπή αρχεία μοντέλου ή μη υποστηριζόμενες μορφές εικόνας.  
- Ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να ενσωματώσετε στο Visual Studio και να δείτε τα αποτελέσματα αμέσως.

### Προαπαιτούμενα

- .NET 6.0 ή νεότερο (το API που χρησιμοποιείται στο παράδειγμα στοχεύει στο .NET Standard 2.0, οπότε λειτουργούν και παλαιότερες εκδόσεις).  
- Βασική εξοικείωση με C# και Visual Studio (ή οποιοδήποτε IDE προτιμάτε).  
- Η βιβλιοθήκη OCR που χρησιμοποιείτε (το απόσπασμα υποθέτει μια φανταστική κλάση `OcrEngine` που έρχεται με μοντέλα γλώσσας).  
- Ένας φάκελος που περιέχει τα απαιτούμενα αρχεία μοντέλου γλώσσας — σκεφτείτε το ως το “εγκέφαλο” που η μηχανή χρησιμοποιεί για να διαβάσει κινέζικα χαρακτήρες.

> **Συμβουλή επαγγελματία:** Αν δεν έχετε ακόμη τα αρχεία μοντέλου για τα κινέζικα, κατεβάστε τα μία φορά από τον ιστότοπο του προμηθευτή και τοποθετήστε τα σε φάκελο όπως `C:\OcrResources`. Η μηχανή δεν θα χρειαστεί ποτέ ξανά σύνδεση στο διαδίκτυο.

---

![Διάγραμμα που δείχνει τη διαδικασία OCR σε μια φωτογραφία](path/to/ocr-diagram.png "Διάγραμμα που δείχνει τη διαδικασία OCR σε μια φωτογραφία")

## Πώς να Χρησιμοποιήσετε OCR: Ρύθμιση της Μηχανής

Το πρώτο που χρειάζεστε είναι μια παρουσία της μηχανής OCR, ρυθμισμένη για τη γλώσσα που σας ενδιαφέρει. Σε αυτόν τον οδηγό στοχεύουμε στα **Απλοποιημένα Κινέζικα**, αλλά η αλλαγή του `OcrLanguage.ChineseSimplified` σε `OcrLanguage.English` (ή οποιαδήποτε άλλη τιμή enum) είναι απλώς μια γραμμή κώδικα.

```csharp
using System;
using YourOcrLibrary;   // Replace with the actual namespace of your OCR SDK

// Step 1: Create and configure the OCR engine for Simplified Chinese
var ocrEngine = new OcrEngine
{
    // Primary keyword appears here naturally
    Language = OcrLanguage.ChineseSimplified,

    // Point to a folder that already contains the Chinese model files
    ResourceFolder = @"C:\OcrResources"
};
```

**Γιατί είναι σημαντικό:**  
Η ιδιότητα `Language` λέει στη μηχανή ποιο σύνολο χαρακτήρων να περιμένει. Το `ResourceFolder` είναι το φάκελο όπου η μηχανή ψάχνει για τα βάρη του νευρωνικού δικτύου και τα λεξικά γλώσσας — σκεφτείτε το ως τη μνήμη του εγκεφάλου. Αν το δείξετε σε λάθος φάκελο, η μηχανή θα πετάξει `FileNotFoundException` και θα κολλήσετε.

## Εξαγωγή Κειμένου από Εικόνα – Φόρτωση Πόρων

Πριν η μηχανή μπορέσει να διαβάσει οτιδήποτε, πρέπει να φορτώσετε τα αρχεία μοντέλου στη μνήμη. Αυτό το βήμα είναι **καίριο** επειδή αποφεύγει κλήση δικτύου κάθε φορά που επεξεργάζεστε μια εικόνα.

```csharp
// Step 2: Load the language resources from the specified folder (no internet required)
try
{
    ocrEngine.LoadResources();
    Console.WriteLine("Resources loaded successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to load OCR resources: {ex.Message}");
    // In a real app you might fallback to a default language or abort gracefully
}
```

**Τι μπορεί να πάει στραβά;**  
Αν η διαδρομή του φακέλου είναι λανθασμένη ή τα αρχεία είναι κατεστραμμένα, το `LoadResources()` θα εγείρει εξαίρεση. Το μπλοκ `try/catch` παραπάνω δείχνει ευγενική διαχείριση σφαλμάτων — κάτι που συχνά χρειάζεται στην παραγωγή.

## Αναγνώριση Κειμένου από Φωτογραφία – Εκτέλεση του OCR

Τώρα το διασκεδαστικό κομμάτι: τροφοδοτήστε ένα αρχείο εικόνας στη μηχανή και λάβετε το αναγνωρισμένο κείμενο. Αυτό είναι η καρδιά των σεναρίων **run OCR on image**, είτε η εικόνα είναι JPEG, PNG ή ακόμα και BMP.

```csharp
// Step 3: Recognize text from an image file
string imagePath = @"C:\OcrResources\photo.jpg";

try
{
    var recognitionResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(recognitionResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
}
```

Η μέθοδος `RecognizeImage` επιστρέφει ένα `RecognitionResult` (ή ό,τι όνομα δίνει το SDK σας) που συνήθως περιέχει:

- `Text` – η απλή μεταγραφή κειμένου.  
- `Confidence` – ένας αριθμητικός δείκτης που υποδεικνύει πόσο σίγουρη είναι η μηχανή για κάθε γραμμή.  
- `BoundingBoxes` – προαιρετικές συντεταγμένες για το πού βρίσκεται κάθε λέξη στην εικόνα.

**Γιατί μπορεί να σας ενδιαφέρει η αξιοπιστία:**  
Αν χτίζετε ένα εργαλείο αυτοματοποίησης εισαγωγής δεδομένων, μπορείτε να θέσετε ένα όριο (π.χ. 0.85) και να ζητήσετε από τον χρήστη επιβεβαίωση για γραμμές χαμηλής αξιοπιστίας. Αυτό βελτιώνει δραστικά τη συνολική ακρίβεια.

## Αναγνώριση Κειμένου από JPG – Διαχείριση Διαφορετικών Μορφών

Πολλοί προγραμματιστές υποθέτουν ότι το OCR λειτουργεί μόνο με PNG, αλλά οι σύγχρονες μηχανές διαχειρίζονται **αρχεία JPG** εξίσου καλά. Το μόνο πρόβλημα είναι ότι η συμπίεση JPEG μπορεί να εισάγει θόρυβο που μπερδεύει το μοντέλο.

```csharp
// Bonus: Recognize text from a JPG with optional preprocessing
string jpgPath = @"C:\OcrResources\scanned_doc.jpg";

// Optional: use a simple image‑preprocess step to improve accuracy
var preprocessed = ImageHelper.DenoiseAndDeskew(jpgPath); // pseudo‑method
var result = ocrEngine.RecognizeImage(preprocessed);
Console.WriteLine($"Detected text ({result.Confidence:P0} confidence):");
Console.WriteLine(result.Text);
```

Αν δεν έχετε βοηθητική συνάρτηση `DenoiseAndDeskew`, πολλές βιβλιοθήκες (π.χ. OpenCvSharp) παρέχουν αυτές τις λειτουργίες. Το κύριο συμπέρασμα είναι: **run OCR on image** αρχεία μετά από μια μικρή καθαριότητα αν προέρχονται από σαρωτή ή κάμερα τηλεφώνου.

## Run OCR on Image – Συμβουλές, Ακραίες Περιπτώσεις και Καλές Πρακτικές

### 1. Διαχείριση Μνήμης
Η φόρτωση μεγάλων μοντέλων γλώσσας μπορεί να καταναλώσει εκατοντάδες megabytes. Αποδεσμεύστε τη μηχανή όταν τελειώσετε:

```csharp
ocrEngine.Dispose(); // or using statement if the SDK implements IDisposable
```

### 2. Επεξεργασία σε Παρτίδες
Αν χρειάζεται να επεξεργαστείτε δεκάδες φωτογραφίες, φορτώστε τους πόρους μία φορά, μετά κάντε βρόχο:

```csharp
string[] files = Directory.GetFiles(@"C:\BatchPhotos", "*.jpg");
foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), res.Text);
}
```

### 3. Σενάρια Πολλαπλών Γλωσσών
Μπορείτε να αλλάζετε γλώσσες εν κινήσει επανα‑αναθέτοντας το `ocrEngine.Language` και καλώντας ξανά το `LoadResources()`. Προσέξτε όμως τον επιπλέον χρόνο φόρτωσης.

### 4. Διαχείριση Κενών Αποτελεσμάτων
Μερικές φορές η μηχανή επιστρέφει κενή συμβολοσειρά. Αυτό συνήθως σημαίνει ότι η εικόνα είναι πολύ θολή ή το χρώμα του κειμένου αναμειγνύεται με το φόντο. Έλεγχος σε μία γραμμή:

```csharp
if (string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text detected – consider increasing image contrast.");
}
```

### 5. Θέματα Ασφάλειας
Ποτέ μην τροφοδοτείτε αρχεία που ανέβηκαν από χρήστες απευθείας στη μηχανή OCR χωρίς επικύρωση. Τουλάχιστον, ελέγξτε την επέκταση και το μέγεθος του αρχείου, και σκεφτείτε να κάνετε σάρωση για κακόβουλο λογισμικό.

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω υπάρχει ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε σε ένα νέο έργο Console App. Δείχνει **πώς να χρησιμοποιήσετε OCR**, **εξαγωγή κειμένου από εικόνα**, **αναγνώριση κειμένου από φωτογραφία**, **αναγνώριση κειμένου από JPG**, και **run OCR on image** — όλα μαζί.

```csharp
// File: Program.cs
using System;
using System.IO;
using YourOcrLibrary; // Replace with actual namespace

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // ------------------------------
            // 1️⃣ Configure the OCR engine
            // ------------------------------
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified,
                ResourceFolder = @"C:\OcrResources"
            };

            // Load language resources (no internet needed)
            try
            {
                ocrEngine.LoadResources();
                Console.WriteLine("Resources loaded.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Failed to load resources: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Recognize text from a photo (JPG in this case)
            // -------------------------------------------------
            string imagePath = @"C:\OcrResources\photo.jpg";

            if (!File.Exists(imagePath))
            {
                Console.Error.WriteLine($"Image not found: {imagePath}");
                return;
            }

            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("\n=== OCR Output ===");
                Console.WriteLine(result.Text);
                Console.WriteLine($"\nConfidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"OCR error: {ex.Message}");
            }

            // Clean up
            ocrEngine.Dispose();
        }
    }
}
```

**Αναμενόμενη έξοδος (παράδειγμα):**

```
Resources loaded.

=== OCR Output ===
中华人民共和国
北京
2026年02月13日

Confidence: 92.45%
```

Το πραγματικό κείμενο σας θα διαφέρει ανάλογα με το περιεχόμενο της εικόνας, αλλά θα πρέπει να δείτε ένα μπλοκ χαρακτήρων Unicode να εκτυπώνεται στην κονσόλα μαζί με ένα ποσοστό αξιοπιστίας.

---

## Συμπέρασμα

Διασχίσαμε **πώς να χρησιμοποιήσετε OCR** σε C# από την αρχή μέχρι το τέλος — ρυθμίζοντας τη μηχανή, φορτώνοντας πόρους γλώσσας, και τελικά **αναγνωρίζοντας κείμενο από φωτογραφία** ή **JPG** χωρίς ποτέ να χρειαστεί σύνδεση στο διαδίκτυο. Ακολουθώντας τα παραπάνω βήματα μπορείτε να **εξάγετε κείμενο από εικόνα**, **να τρέξετε OCR σε εικόνα** και να αντιμετωπίσετε τα πιο συνηθισμένα εμπόδια που συναντούν οι αρχάριοι.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να τροφοδοτήσετε τη μηχανή με μια σελίδα PDF μετατρεπόμενη σε εικόνα, ή πειραματιστείτε με ένα διαφορετικό πακέτο γλώσσας για να δείτε πώς αλλάζουν οι βαθμολογίες αξιοπιστίας. Μπορείτε

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}