---
category: general
date: 2026-01-07
description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να αναγνωρίζετε κείμενο από φωτογραφία, να βελτιώσετε την ακρίβεια του OCR,
  να φορτώσετε εικόνα για OCR και να ορίσετε τη γλώσσα του OCR.
draft: false
keywords:
- extract text from image
- recognize text from photo
- improve ocr accuracy
- load image for ocr
- set ocr language
language: el
og_description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR. Αυτός ο
  οδηγός δείχνει πώς να αναγνωρίζετε κείμενο από φωτογραφία, να βελτιώσετε την ακρίβεια
  του OCR, να φορτώσετε εικόνα για OCR και να ορίσετε τη γλώσσα του OCR.
og_title: Εξαγωγή κειμένου από εικόνα με Aspose OCR – Οδηγός C#
tags:
- Aspose OCR
- C#
- Image Processing
title: Εξαγωγή κειμένου από εικόνα με Aspose OCR – Πλήρης οδηγός C#
url: /el/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα – Πλήρης Υλοποίηση C# με Aspose OCR

Έχετε χρειαστεί ποτέ να **εξάγετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα σας δώσει αξιόπιστα αποτελέσματα; Δεν είστε μόνοι. Σε πολλές πραγματικές εφαρμογές — σαρωτές αποδείξεων, επαληθευτές ταυτοτήτων ή απλώς ένα γρήγορο εργαλείο σημειώσεων — η **αναγνώριση κειμένου από φωτογραφία** είναι απαραίτητη λειτουργία.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει πώς να **φορτώσετε εικόνα για OCR**, να ρυθμίσετε τη μηχανή ώστε **να ορίσετε τη γλώσσα OCR**, και να εφαρμόσετε μερικά κόλπα προεπεξεργασίας για **βελτίωση της ακρίβειας του OCR**. Στο τέλος θα έχετε ένα μοναδικό αρχείο C# που εκτυπώνει το εξαγόμενο κείμενο στην κονσόλα, και θα καταλάβετε γιατί κάθε ρύθμιση έχει σημασία.

> **Συμβουλή:** Ο κώδικας λειτουργεί με Aspose.OCR ≥ 23.5, .NET 6+ και σε οποιοδήποτε περιβάλλον Windows, Linux ή macOS που μπορεί να τρέξει .NET Core.

## Προαπαιτούμενα

- .NET 6 SDK (ή νεότερο) εγκατεστημένο  
- Visual Studio 2022, VS Code ή οποιοσδήποτε επεξεργαστής προτιμάτε  
- Πακέτο NuGet `Aspose.OCR` (εγκατάσταση μέσω `dotnet add package Aspose.OCR`)  
- Ένα αρχείο εικόνας (JPEG/PNG) που περιέχει καθαρό τυπωμένο ή πληκτρολογημένο κείμενο  

Αν έχετε όλα αυτά, ας ξεκινήσουμε.

![παράδειγμα εξαγωγής κειμένου από εικόνα](/images/ocr-example.png "εξαγωγή κειμένου από εικόνα – έξοδος Aspose OCR")

## Βήμα 1: Δημιουργία και Αποδέσμευση του OCR Engine – Πυρήνας «Extract Text from Image»

Το πρώτο που χρειάζεστε είναι μια παρουσία του `OcrEngine`. Η τοποθέτησή του μέσα σε μπλοκ `using` εγγυάται τη σωστή αποδέσμευση των εγγενών πόρων.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

/// <summary>
/// Demonstrates how to extract text from image using Aspose OCR.
/// </summary>
class Program
{
    static void Main()
    {
        // Step 1 – Initialize the OCR engine (the heart of the process)
        using (var ocrEngine = new OcrEngine())
        {
            // The rest of the workflow lives inside this block.
```

**Γιατί είναι σημαντικό:** Το `OcrEngine` κρατά μη διαχειριζόμενη μνήμη για τις εγγενείς DLL του OCR. Η άμεση αποδέσμευσή του αποτρέπει διαρροές μνήμης, ειδικά όταν επεξεργάζεστε πολλές εικόνες σε παρτίδα.

## Βήμα 2: Ορισμός Ρυθμίσεων Αναγνώρισης – Βελτίωση της Ακρίβειας του OCR

Στη συνέχεια δημιουργούμε ένα αντικείμενο `RecognitionSettings`. Εδώ **ορίζουμε τη γλώσσα OCR** και προσθέτουμε φίλτρα προεπεξεργασίας που συχνά κάνουν τη διαφορά μεταξύ ακατάστατου κειμένου και καθαρού αποτελέσματος.

```csharp
            // Step 2 – Configure recognition settings
            var recognitionSettings = new RecognitionSettings
            {
                // Set the language to English; other languages are available via Language enum.
                Language = Language.English,

                // PreprocessFilters help the engine deal with real‑world photo issues.
                PreprocessFilters = new[]
                {
                    PreprocessFilter.Deskew,          // Corrects slight rotation
                    PreprocessFilter.Denoise,         // Reduces grainy noise
                    PreprocessFilter.ContrastEnhance // Boosts text visibility
                }
            };
```

**Γιατί αυτά τα φίλτρα;**  
- **Deskew** διορθώνει το κοινό πρόβλημα μιας φωτογραφίας που τραβήχτηκε με το τηλέφωνο και είναι ελαφρώς κεκλιμένη.  
- **Denoise** αφαιρεί σπαστάκια που μπορούν να ερμηνευτούν ως χαρακτήρες.  
- **ContrastEnhance** κάνει το αχνό μελάνι πιο εμφανές, κάτι ουσιώδες για **βελτίωση της ακρίβειας του OCR**.

## Βήμα 3: Φόρτωση της Εικόνας – Φόρτωση Εικόνας για OCR Αποτελεσματικά

Η Aspose παρέχει τη μέθοδο `ImageStream.FromFile` για γρήγορη φόρτωση. Μπορείτε επίσης να τροφοδοτήσετε ένα `MemoryStream` αν η εικόνα προέρχεται από αίτημα web ή βάση δεδομένων.

```csharp
            // Step 3 – Load the image you want to analyze
            var imagePath = @"YOUR_DIRECTORY/phone_photo.jpg";
            var imageStream = ImageStream.FromFile(imagePath);
```

**Κοινό λάθος:** Η χρήση διαδρομής με μπροστιγές κάθετες (forward slashes) στα Windows λειτουργεί, αλλά η χρήση του `Path.Combine` είναι πιο ασφαλής για έργα πολλαπλών πλατφορμών.

## Βήμα 4: Εκτέλεση Αναγνώρισης – Αναγνώριση Κειμένου από Φωτογραφία

Τώρα καλούμε το `Recognize`, περνώντας τόσο το ρεύμα εικόνας όσο και τις ρυθμίσεις μας. Η μέθοδος επιστρέφει μια απλή συμβολοσειρά με το εξαγόμενο κείμενο.

```csharp
            // Step 4 – Run OCR and capture the result
            string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);
```

Αν η εικόνα περιέχει πολλαπλά τμήματα κειμένου, η Aspose τα συνενώνει με αλλαγές γραμμής, διατηρώντας όσο το δυνατόν καλύτερα την αρχική διάταξη.

## Βήμα 5: Εξαγωγή Αποτελέσματος – Επαλήθευση Εξαγωγής

Τέλος, γράψτε το αποτέλεσμα στην κονσόλα. Σε μια πραγματική εφαρμογή μπορεί να το αποθηκεύσετε σε βάση δεδομένων, να το στείλετε σε άλλη υπηρεσία ή να το εμφανίσετε σε UI.

```csharp
            // Step 5 – Show the extracted text
            Console.WriteLine("=== Extracted Text Start ===");
            Console.WriteLine(recognizedText);
            Console.WriteLine("=== Extracted Text End ===");
        } // End of using block – OcrEngine disposed
    }
}
```

### Αναμενόμενη Εξαγωγή στην Κονσόλα

```
=== Extracted Text Start ===
This is a sample receipt.
Total: $23.45
Thank you for shopping!
=== Extracted Text End ===
```

Αν δείτε ακατάστατους χαρακτήρες, ελέγξτε ξανά ότι η εικόνα είναι καθαρή, ότι η γλώσσα ταιριάζει με το κείμενο, και ότι τα φίλτρα προεπεξεργασίας είναι κατάλληλα.

## Βήμα 6: Προαιρετικές Ρυθμίσεις – Λεπτομερής Βελτιστοποίηση για Ακραίες Περιπτώσεις

### α. Αλλαγή Γλωσσών

```csharp
recognitionSettings.Language = Language.Spanish; // For Spanish receipts
```

### β. Προσθήκη Προσαρμοσμένων Φίλτρων

Η Aspose προσφέρει επίσης `PreprocessFilter.Sharpen` ή `PreprocessFilter.Binarize`. Πειραματιστείτε με αυτά όταν το προεπιλεγμένο τρίο δεν είναι αρκετό.

### γ. Διαχείριση Μεγάλων Εικόνων

Για πολύ υψηλής ανάλυσης φωτογραφίες, μειώστε πρώτα το μέγεθος ώστε η χρήση μνήμης να παραμείνει χαμηλή:

```csharp
var resizedStream = ImageProcessor.Resize(imageStream, 1024, 768);
string text = ocrEngine.Recognize(resizedStream, recognitionSettings);
```

## Συχνές Ερωτήσεις

**Ε: Λειτουργεί αυτό με χειρόγραφα σημειώματα;**  
Α: Το Aspose OCR είναι βελτιστοποιημένο για τυπωμένο κείμενο. Η αναγνώριση χειρόγραφου απαιτεί διαφορετική μηχανή (π.χ. Aspose.OCR for Handwriting ή μοντέλο μηχανικής μάθησης).

**Ε: Μπορώ να επεξεργαστώ πολλές εικόνες σε βρόχο;**  
Α: Σίγουρα. Απλώς μετακινήστε το μπλοκ `using (var ocrEngine = new OcrEngine())` έξω από το βρόχο και επαναχρησιμοποιήστε τη μηχανή για καλύτερη απόδοση.

**Ε: Τι γίνεται αν η εικόνα είναι σελίδα PDF;**  
Α: Μετατρέψτε πρώτα τη σελίδα PDF σε εικόνα (η Aspose.PDF μπορεί να αποδώσει σελίδες ως PNG/JPEG), έπειτα δώστε την στο OCR engine.

## Ανακεφαλαίωση – Τι Καταφέραμε

- **Εξάγαμε κείμενο από εικόνα** χρησιμοποιώντας ένα ενιαίο, αυτόνομο πρόγραμμα C#.  
- Δείξαμε πώς να **αναγνωρίζουμε κείμενο από φωτογραφία** με προεπεξεργασία που **βελτιώνει την ακρίβεια του OCR**.  
- Επιδείξαμε τον σωστό τρόπο **φόρτωσης εικόνας για OCR** και **ορισμού γλώσσας OCR** για πολυγλωσσικά σενάρια.  

## Επόμενα Βήματα & Σχετικά Θέματα

- **Επεξεργασία παρτίδας:** Συνδυάστε αυτό το απόσπασμα με `Directory.GetFiles` για OCR ολόκληρου φακέλου.  
- **Μετα-επεξεργασία:** Χρησιμοποιήστε κανονικές εκφράσεις για καθαρισμό ημερομηνιών, ποσών ή αριθμών ταυτοποίησης μετά την εξαγωγή.  
- **Ενσωματώσεις:** Στείλτε το εξαγόμενο κείμενο στο Azure Cognitive Search ή Elastic για αναζητήσιμα έγγραφα.  

Πειραματιστείτε με διαφορετικούς συνδυασμούς φίλτρων, γλώσσες και πηγές εικόνας. Το βασικό μοτίβο παραμένει το ίδιο: δημιουργήστε τη μηχανή, ρυθμίστε τις παραμέτρους, φορτώστε την εικόνα, αναγνωρίστε και εξάγετε. Καλή προγραμματιστική δουλειά!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}