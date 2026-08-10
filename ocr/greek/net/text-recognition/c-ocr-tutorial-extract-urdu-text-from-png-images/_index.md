---
category: general
date: 2026-03-21
description: 'c# OCR tutorial: Μάθετε πώς να εξάγετε κείμενο Urdu από εικόνα PNG χρησιμοποιώντας
  OCR σε C#. Περιλαμβάνονται κώδικας βήμα‑βήμα, ρύθμιση γλώσσας και πρακτικές συμβουλές.'
draft: false
keywords:
- c# ocr tutorial
- extract urdu text
- recognize text image
- how to extract urdu
- ocr from png file
language: el
og_description: 'c# OCR tutorial: Μάθετε πώς να εξάγετε κείμενο Urdu από εικόνα PNG
  χρησιμοποιώντας OCR σε C#. Πλήρης οδηγός με κώδικα και συμβουλές.'
og_title: c# OCR οδηγός – Εξαγωγή κειμένου Urdu από εικόνες PNG
tags:
- OCR
- C#
- Urdu
- Image Processing
title: c# OCR tutorial – Εξαγωγή κειμένου Urdu από εικόνες PNG
url: /el/net/text-recognition/c-ocr-tutorial-extract-urdu-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Εξαγωγή κειμένου Urdu από εικόνες PNG

Χρειάστηκε ποτέ ένα **c# ocr tutorial** που πραγματικά εξάγει κείμενο Urdu από ένα αρχείο PNG; Δεν είστε μόνοι. Σε πολλά έργα—επεξεργασία τιμολογίων, αρχειοθέτηση εγγράφων ή ακόμη και ένα γρήγορο εργαλείο μετάφρασης—θα φτάσετε στο σημείο όπου πρέπει να αναγνωρίσετε δεδομένα κειμένου από εικόνα, και η γλώσσα έχει σημασία.  

Σε αυτόν τον οδηγό θα περάσουμε βήμα προς βήμα από μια πλήρη, έτοιμη προς εκτέλεση λύση που εξάγει κείμενο Urdu από PNG χρησιμοποιώντας μια μηχανή OCR. Θα δείτε γιατί υπάρχει κάθε γραμμή, πώς να διαχειριστείτε τα ελλιπή πακέτα γλώσσας και τι να κάνετε αν η εικόνα δεν είναι τέλεια. Στο τέλος θα είστε αρκετά σίγουροι για να προσαρμόσετε τον κώδικα σε άλλες γλώσσες ή τύπους αρχείων.

## Τι θα μάθετε

- Πώς να εγκαταστήσετε μια βιβλιοθήκη C# OCR (χωρίς κρυφή μαγεία)  
- Τα ακριβή βήματα για **extract urdu text** από αρχείο PNG  
- Γιατί η ρύθμιση της γλώσσας σε Urdu είναι σημαντική και πώς η μηχανή κατεβάζει αυτόματα τα ελλιπή δεδομένα  
- Τρόποι επαλήθευσης του αποτελέσματος και αντιμετώπισης κοινών προβλημάτων  

Δεν απαιτούνται εξωτερικοί σύνδεσμοι τεκμηρίωσης—όλα όσα χρειάζεστε είναι εδώ.

## Προαπαιτούμενα (Τι χρειάζεστε πριν ξεκινήσετε)

| Απαίτηση | Γιατί είναι σημαντικό |
|-------------|----------------|
| .NET 6.0+ (or .NET Core 3.1) | Σύγχρονα API και υποστήριξη async |
| Visual Studio 2022 (or VS Code with C# extension) | IDE με IntelliSense κάνει τον κώδικα πιο σαφή |
| An OCR library that exposes `OcrEngine` (e.g., **Microsoft.Windows.SDK.Contracts** or a third‑party NuGet) | Παρέχει τις μεθόδους `Language.Urdu` και `Recognize` |
| A PNG image containing Urdu text (e.g., `urdu_invoice.png`) | Η πηγή για τη λειτουργία **recognize text image** |

Αν δεν έχετε ακόμη πακέτο OCR, εκτελέστε αυτή τη μία γραμμή στην Κονσόλα Διαχειριστή Πακέτων:

```powershell
Install-Package Microsoft.Windows.SDK.Contracts
```

> **Pro tip:** Το SDK αυτόματα κατεβάζει τα δεδομένα γλώσσας στην πρώτη χρήση, οπότε δεν χρειάζεται να κατεβάσετε χειροκίνητα τα πακέτα γλώσσας Urdu.

## Βήμα 1: Εγκατάσταση και Αναφορά της βιβλιοθήκης OCR

Πριν μπορέσουμε να δημιουργήσουμε μια μηχανή, το έργο πρέπει να αναφέρει το πακέτο OCR. Προσθέστε τις ακόλουθες οδηγίες `using` στην αρχή του αρχείου σας:

```csharp
using System;
using Windows.Media.Ocr;          // Core OCR classes
using Windows.Graphics.Imaging;   // For loading PNG files
using Windows.Storage;            // File handling helpers
```

Αυτά τα namespaces μας δίνουν πρόσβαση στα `OcrEngine`, `Language` και τα εργαλεία φόρτωσης εικόνας. Αν χρησιμοποιείτε διαφορετική βιβλιοθήκη, ψάξτε για αντίστοιχα namespaces.

## Βήμα 2: Δημιουργία ενός παραδείγματος OCR Engine  

Τώρα δημιουργούμε πραγματικά τη μηχανή. Σκεφτείτε τη μηχανή ως τον εγκέφαλο που θα ερμηνεύει τα μοτίβα εικονοστοιχείων ως χαρακτήρες.

```csharp
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));
if (ocrEngine == null)
{
    Console.WriteLine("Failed to create OCR engine for Urdu. Check your language pack.");
    return;
}
```

**Γιατί είναι σημαντικό:** Η `TryCreateFromLanguage` επιστρέφει `null` εάν τα δεδομένα γλώσσας δεν είναι διαθέσιμα, δίνοντάς μας την ευκαιρία να αποτύχουμε γρήγορα αντί να καταρρεύσουμε αργότερα.

## Βήμα 3: Φόρτωση της εικόνας PNG  

Η μηχανή OCR λειτουργεί με αντικείμενα `SoftwareBitmap`, όχι με ακατέργαστες διαδρομές αρχείων. Ο παρακάτω βοηθός φορτώνει ένα PNG από το δίσκο και το μετατρέπει στη απαιτούμενη μορφή.

```csharp
// Step 3: Load the PNG image into a SoftwareBitmap
async Task<SoftwareBitmap> LoadImageAsync(string path)
{
    StorageFile file = await StorageFile.GetFileFromPathAsync(path);
    using var stream = await file.OpenReadAsync();
    var decoder = await BitmapDecoder.CreateAsync(stream);
    // Convert to Gray8 for best OCR accuracy
    return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
}
```

**Περίπτωση άκρης:** Εάν το PNG είναι έγχρωμο, η μετατροπή σε αποχρώσεις του γκρι (`Gray8`) συχνά βελτιώνει την αναγνώριση, ειδικά για γραφές όπως το Urdu που έχουν ευαίσθητες διακριτικές σημάνσεις.

## Βήμα 4: Αναγνώριση κειμένου από την εικόνα  

Αυτή είναι η καρδιά του **c# ocr tutorial**—ζητώντας από τη μηχανή να διαβάσει την εικόνα.

```csharp
// Step 4: Perform OCR on the loaded bitmap
async Task<string> RecognizeUrduAsync(string imagePath)
{
    SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
    OcrResult result = await ocrEngine.RecognizeAsync(bitmap);
    return result.Text;
}
```

Η ιδιότητα `OcrResult.Text` περιέχει τη ακατέργαστη συμβολοσειρά Unicode. Επειδή ορίσαμε τη γλώσσα σε Urdu νωρίτερα, η μηχανή εφαρμόζει τους σωστούς κανόνες γραφής.

## Βήμα 5: Έξοδος και επαλήθευση του εξαγόμενου κειμένου  

Τέλος, εκτυπώνουμε το αποτέλεσμα στην κονσόλα. Σε μια πραγματική εφαρμογή μπορεί να το αποθηκεύσετε σε βάση δεδομένων ή να το στείλετε σε υπηρεσία μετάφρασης.

```csharp
// Step 5: Run the OCR and display the result
static async Task Main(string[] args)
{
    string imageFile = @"C:\Images\urdu_invoice.png"; // adjust path as needed
    string extracted = await RecognizeUrduAsync(imageFile);
    Console.WriteLine("=== Extracted Urdu Text ===");
    Console.WriteLine(extracted);
}
```

**Τι να περιμένετε:** Εάν η εικόνα είναι καθαρή, θα δείτε κάτι όπως:

```
=== Extracted Urdu Text ===
بل نمبر: 12345
تاریخ: 21/03/2026
کل رقم: 5,000 روپے
```

Αν το αποτέλεσμα φαίνεται χαραγμένο, ελέγξτε την ποιότητα της εικόνας (αντίθεση, θόρυβος) και σκεφτείτε προεπεξεργασία (π.χ., δυαδικοποίηση).

## Πώς να εξάγετε κείμενο Urdu από αρχείο PNG – Συνηθισμένα προβλήματα  

1. **Low contrast** – Το OCR δυσκολεύεται όταν τα χρώματα του προσκηνίου και του φόντου είναι παρόμοια. Χρησιμοποιήστε εργαλεία επεξεργασίας εικόνας για να αυξήσετε την αντίθεση πριν εκτελέσετε τον κώδικα.  
2. **Incorrect DPI** – Η σάρωση σε 300 dpi ή περισσότερο παρέχει στη μηχανή περισσότερες λεπτομέρειες για επεξεργασία.  
3. **Missing language pack** – Η πρώτη κλήση στη `TryCreateFromLanguage` μπορεί να προκαλέσει λήψη· βεβαιωθείτε ότι ο υπολογιστής σας έχει πρόσβαση στο internet.  

Η αντιμετώπιση αυτών των ζητημάτων βελτιώνει δραστικά το ποσοστό επιτυχίας του **recognize text image**.

## Recognize Text Image: Επέκταση σε άλλες μορφές  

Αν και αυτό το tutorial εστιάζει στο PNG, η ίδια ροή εργασίας λειτουργεί για JPEG, BMP ή TIFF—απλώς αλλάξτε την επέκταση του αρχείου και βεβαιωθείτε ότι ο αποκωδικοποιητής το υποστηρίζει. Η βασική γραμμή παραμένει `await ocrEngine.RecognizeAsync(bitmap);`.

## Συμβουλές για OCR από αρχείο PNG – Απόδοση και κλιμάκωση  

- **Batch processing:** Φορτώστε πολλές εικόνες σε μια λίστα και εκτελέστε `Task.WhenAll` για να παραλληλοποιήσετε την αναγνώριση.  
- **Caching the engine:** Δημιουργήστε ένα μόνο παράδειγμα `OcrEngine` και επαναχρησιμοποιήστε το σε κλήσεις· η επαναλαμβανόμενη δημιουργία προσθέτει επιπλέον φόρτο.  
- **Memory management:** Αποδεσμεύστε τα αντικείμενα `SoftwareBitmap` μετά τη χρήση (`bitmap.Dispose()`) για να διατηρήσετε τη διαδικασία ελαφριά.  

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι ολόκληρο το πρόγραμμα που μπορείτε να μεταγλωττίσετε και να εκτελέσετε. Περιλαμβάνει όλες τις δηλώσεις using, τη διαχείριση async και ελέγχους σφαλμάτων.

```csharp
// Full C# OCR tutorial – Extract Urdu text from a PNG file
using System;
using System.Threading.Tasks;
using Windows.Media.Ocr;
using Windows.Graphics.Imaging;
using Windows.Storage;

class Program
{
    // Initialize the OCR engine for Urdu
    private static OcrEngine _ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));

    static async Task Main(string[] args)
    {
        if (_ocrEngine == null)
        {
            Console.WriteLine("Urdu language pack not available. Ensure internet connectivity for automatic download.");
            return;
        }

        string imagePath = @"C:\Images\urdu_invoice.png"; // <-- change to your image location
        string text = await RecognizeUrduAsync(imagePath);
        Console.WriteLine("=== Extracted Urdu Text ===");
        Console.WriteLine(text);
    }

    // Load PNG and convert to grayscale bitmap
    private static async Task<SoftwareBitmap> LoadImageAsync(string path)
    {
        StorageFile file = await StorageFile.GetFileFromPathAsync(path);
        using var stream = await file.OpenReadAsync();
        var decoder = await BitmapDecoder.CreateAsync(stream);
        return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
    }

    // Perform OCR and return the recognized text
    private static async Task<string> RecognizeUrduAsync(string imagePath)
    {
        SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
        OcrResult result = await _ocrEngine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

**Expected output:** Η κονσόλα εκτυπώνει τους ακριβείς χαρακτήρες Urdu που βρέθηκαν στην εικόνα, διατηρώντας τη σειρά από δεξιά προς αριστερά.

## Συμπέρασμα  

Μόλις ολοκληρώσατε ένα **c# ocr tutorial** που δείχνει πώς να **extract urdu text** από PNG, να ρυθμίσετε τη γλώσσα και να χειριστείτε το αποτέλεσμα με ασφάλεια. Τα βήματα—εγκατάσταση της βιβλιοθήκης, δημιουργία της μηχανής, φόρτωση της εικόνας, αναγνώριση κειμένου και έξοδος—σχηματίζουν ένα επαναχρησιμοποιήσιμο πρότυπο που μπορείτε να εφαρμόσετε σε οποιαδήποτε γραφή ή τύπο αρχείου.  

Στη συνέχεια, σκεφτείτε να πειραματιστείτε με **recognize text image** σε PDF πολλαπλών σελίδων (μετατρέψτε κάθε σελίδα σε PNG πρώτα) ή να ενσωματώσετε ένα API μετάφρασης για να μετατρέψετε το εξαγόμενο Urdu αυτόματα σε Αγγλικά. Ο ουρανός είναι το όριο μόλις κυριαρχήσετε αυτή τη βασική ροή εργασίας.

Καλό κώδικα, και εύχομαι τα αποτελέσματα OCR σας να είναι κρυστάλλινα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}