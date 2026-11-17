---
category: general
date: 2026-03-13
description: Εξαγωγή κειμένου από εικόνα με χρήση του Aspose OCR σε C#. Μάθετε πώς
  να φορτώνετε εικόνα για OCR, να εκτελείτε OCR στην εικόνα και να εξάγετε κυριλλικό
  κείμενο με σαφή βήμα‑βήμα κώδικα.
draft: false
keywords:
- extract text from image
- load image for ocr
- run ocr on image
- extract cyrillic text
- recognize cyrillic text
language: el
og_description: Εξαγωγή κειμένου από εικόνα σε C# χρησιμοποιώντας το Aspose OCR. Αυτό
  το σεμινάριο δείχνει πώς να φορτώσετε μια εικόνα για OCR, να εκτελέσετε OCR στην
  εικόνα και να εξάγετε κυριλλικό κείμενο αποδοτικά.
og_title: Εξαγωγή κειμένου από εικόνα με Aspose OCR – Οδηγός C#
tags:
- Aspose OCR
- C#
- Image Processing
title: Εξαγωγή κειμένου από εικόνα με το Aspose OCR – Οδηγός προγραμματισμού C#
url: /el/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Προγραμματισμού C#

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα διαχειριστεί τους κυριλλικούς χαρακτήρες χωρίς προβλήματα; Δεν είστε μόνοι. Σε πολλά έργα—σάρωση τιμολογίων, επαλήθευση διαβατηρίου ή γρήγορη λήψη σημειώσεων—η αξιόπιστη εξαγωγή κειμένου από μια φωτογραφία είναι απαραίτητη.  

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από το **φόρτωμα εικόνας για OCR**, τη ρύθμιση του Aspose OCR, το **run OCR on image**, και τέλος την **εξαγωγή κυριλλικού κειμένου** με λίγες γραμμές C#. Στο τέλος θα έχετε ένα έτοιμο κομμάτι κώδικα που εκτυπώνει το αναγνωρισμένο κείμενο στην κονσόλα.

## Τι Θα Μάθετε

- Πώς να εγκαταστήσετε και να αναφέρετε το πακέτο NuGet Aspose OCR.  
- Ο σωστός τρόπος να δείξετε τη μηχανή στα πόρους των πακέτων γλώσσας.  
- Γιατί η επιλογή του `Language.Cyrillic` είναι σημαντική για μη λατινικά σενάρια.  
- Συνηθισμένα προβλήματα (απουσία πόρων, μη υποστηριζόμενες μορφές εικόνας) και πώς να τα αποφύγετε.  
- Ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

Δεν απαιτείται προηγούμενη εμπειρία OCR, αλλά μια βασική εξοικείωση με C# και Visual Studio θα κάνει τη διαδικασία πιο ομαλή.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

1. **.NET 6.0** ή νεότερο εγκατεστημένο (ο κώδικας λειτουργεί σε .NET Core και .NET Framework).  
2. **Visual Studio 2022** (ή οποιονδήποτε επεξεργαστή που υποστηρίζει C#).  
3. Το **Aspose.OCR** πακέτο NuGet. Εγκαταστήστε το μέσω του Package Manager Console:  

   ```powershell
   Install-Package Aspose.OCR
   ```

4. Έναν φάκελο που περιέχει τα OCR language packs (διαθέσιμα για λήψη από τον ιστότοπο της Aspose).  
5. Ένα αρχείο εικόνας (`cyrillic.png` στο παράδειγμα) που περιέχει κυριλλικό κείμενο που θέλετε να διαβάσετε.

> **Pro tip:** Κρατήστε το φάκελο των language‑pack δίπλα στον φάκελο `bin` του έργου σας· απλοποιεί τη διαχείριση διαδρομών.

## Step 1 – Load Image for OCR

Το πρώτο που πρέπει να κάνετε είναι να δώσετε στη μηχανή ένα bitmap για επεξεργασία. Το Aspose OCR δέχεται ένα `ImageStream`, το οποίο μπορεί να δημιουργηθεί απευθείας από διαδρομή αρχείου.

```csharp
using Aspose.OCR;

// Step 1: Load the image you want to process
string imagePath = @"YOUR_DIRECTORY\cyrillic.png";
ImageStream image = ImageStream.FromFile(imagePath);
```

*Γιατί είναι σημαντικό:* Η προημεροληπτική φόρτωση της εικόνας σας επιτρέπει να ελέγξετε ότι το αρχείο υπάρχει και είναι σε υποστηριζόμενη μορφή (PNG, JPEG, BMP, κ.λπ.). Αν λείπει το αρχείο, η κλήση `FromFile` θα ρίξει μια σαφή εξαίρεση, αποφεύγοντας ασαφείς σφάλματα OCR αργότερα.

## Step 2 – Set Up OCR Engine and Resources

Στη συνέχεια, δημιουργήστε την μηχανή OCR και δείξτε της το φάκελο που περιέχει τα language packs. Χωρίς τους σωστούς πόρους η μηχανή δεν θα ξέρει πώς να ερμηνεύσει τα κυριλλικά γλύφους.

```csharp
// Step 2: Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Tell Aspose where the language resources live
string resourcesPath = @"YOUR_DIRECTORY\OcrResources";
ocrEngine.SetResourcesPath(resourcesPath);
```

*Γιατί είναι σημαντικό:* Η μέθοδος `SetResourcesPath` είναι η γέφυρα μεταξύ του κώδικά σας και των αρχείων δεδομένων που περιέχουν τα σχήματα χαρακτήρων για κάθε υποστηριζόμενη γλώσσα. Η παράλειψη αυτού του βήματος συνήθως οδηγεί σε ακατανόητη έξοδο ή σε `ResourceNotFoundException`.

## Step 3 – Choose Language and **Run OCR on Image**

Τώρα επιλέγουμε τη γλώσσα που αναμένουμε. Επειδή το παράδειγμα αφορά κυριλλικό, ορίζουμε `Language.Cyrillic`. Αν χρειάζεται να υποστηρίξετε πολλαπλά σενάρια, μπορείτε να τα συνδυάσετε με τελεστή bitwise OR (`|`).

```csharp
// Step 3: Select the language you want to recognize
ocrEngine.Language = Language.Cyrillic;

// Assign the previously loaded image to the engine
ocrEngine.Image = image;

// Finally, perform the recognition
ocrEngine.Recognize();
```

*Γιατί είναι σημαντικό:* Η καθορισμένη γλώσσα περιορίζει το χώρο αναζήτησης του αλγορίθμου OCR, βελτιώνοντας δραστικά την ταχύτητα και την ακρίβεια. Όταν **run OCR on image** με τη σωστή σημαία γλώσσας, θα δείτε πολύ λιγότερα λάθη αναγνώρισης.

## Step 4 – Retrieve and Use the Extracted Cyrillic Text

Αφού ολοκληρωθεί η αναγνώριση, η μηχανή αποθηκεύει το αποτέλεσμα στην ιδιότητα `Text`. Μπορείτε τώρα να το εμφανίσετε, να το γράψετε σε αρχείο ή να το περάσετε σε άλλο σύστημα.

```csharp
// Step 4: Output the recognized text
string recognizedText = ocrEngine.Text;
Console.WriteLine("=== Extracted Cyrillic Text ===");
Console.WriteLine(recognizedText);
```

Τυπική έξοδος κονσόλας μοιάζει με:

```
=== Extracted Cyrillic Text ===
Привет, мир! Это тестовое изображение.
```

Αν η έξοδος περιέχει ανεπιθύμητα σύμβολα, ελέγξτε ξανά ότι τα language packs ταιριάζουν με την έκδοση του Aspose OCR που έχετε εγκαταστήσει.

## Full Working Example – All Steps Combined

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα νέο έργο κονσόλας. Αντικαταστήστε το `YOUR_DIRECTORY` με τις πραγματικές διαδρομές του υπολογιστή σας.

```csharp
using System;
using Aspose.OCR;

namespace ExtractCyrillicDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the image you want to process
            string imagePath = @"YOUR_DIRECTORY\cyrillic.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // 2️⃣ Initialize OCR engine and point to language resources
            OcrEngine ocrEngine = new OcrEngine();
            string resourcesPath = @"YOUR_DIRECTORY\OcrResources";
            ocrEngine.SetResourcesPath(resourcesPath);

            // 3️⃣ Choose Cyrillic language and run OCR on image
            ocrEngine.Language = Language.Cyrillic;
            ocrEngine.Image = image;
            ocrEngine.Recognize();

            // 4️⃣ Extract and display the text
            string result = ocrEngine.Text;
            Console.WriteLine("=== Extracted Cyrillic Text ===");
            Console.WriteLine(result);
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Η εκτέλεση του προγράμματος θα πρέπει να εκτυπώσει το ακριβές κείμενο που εμφανίζεται στο `cyrillic.png`. Αν η εικόνα περιέχει τη φράση “Привет, мир!”, θα δείτε αυτή τη γραμμή στην κονσόλα χωρίς επιπλέον σύμβολα.

## Edge Cases & Troubleshooting

| Κατάσταση | Τι να Ελέγξετε | Προτεινόμενη Διόρθωση |
|-----------|---------------|------------------------|
| **Απουσία πακέτων γλώσσας** | Δείχνει το `resourcesPath` σε φάκελο που περιέχει αρχεία `.dat`; | Κατεβάστε ξανά τα πακέτα από το Aspose και τοποθετήστε τα στον καθορισμένο φάκελο. |
| **Μη υποστηριζόμενη μορφή εικόνας** | Η εικόνα είναι PNG, JPEG, BMP ή TIFF; | Μετατρέψτε την εικόνα σε μία από τις υποστηριζόμενες μορφές πριν καλέσετε το `FromFile`. |
| **Αχρείοι χαρακτήρες στην έξοδο** | Ορίσατε σωστά το `ocrEngine.Language`; | Χρησιμοποιήστε `Language.Cyrillic` (ή συνδυάστε σημαίες για πολλαπλές γλώσσες). |
| **Καθυστέρηση απόδοσης σε μεγάλες εικόνες** | Ανάλυση εικόνας > 3000 px; | Μειώστε την ανάλυση της εικόνας σε λογικό μέγεθος (π.χ., πλάτος 1024 px) πριν το OCR. |

## Related Topics You Might Explore Next

- **Εξαγωγή κειμένου από εικόνα** σε PDF χρησιμοποιώντας Aspose PDF + OCR.  
- **Φόρτωση εικόνας για OCR** από `Stream` (χρήσιμο όταν οι εικόνες προέρχονται από web API).  
- Χρήση του **run OCR on image** σε παράλληλη εκτέλεση για επιτάχυνση της επεξεργασίας παρτίδας.  
- **Εξαγωγή κυριλλικού κειμένου** από χειρόγραφες σημειώσεις με τη λειτουργία χειρόγραφου του Aspose OCR.  
- Ενσωμάτωση του αποτελέσματος με **recognize cyrillic text** σε βάση δεδομένων για ευρετηρίαση αναζήτησης.

## Conclusion

Μόλις δείξαμε πώς να **εξάγετε κείμενο από εικόνα** με το Aspose OCR, καλύπτοντας όλα από τη φόρτωση της εικόνας μέχρι την εκτύπωση των αναγνωρισμένων κυριλλικών χαρακτήρων. Το σύντομο, αυτόνομο πρόγραμμα δείχνει τον ελάχιστο κώδικα που χρειάζεστε, ενώ ο πίνακας αντιμετώπισης προβλημάτων σας προστατεύει από τα πιο κοινά εμπόδια.  

Δοκιμάστε το με τις δικές σας στιγμιότυπες, αντικαταστήστε το language pack με Αραβικά ή Κινέζικα, και δείτε πώς το ίδιο μοτίβο λειτουργεί παγκοσμίως. Καλό προγραμματισμό, και εύχομαι τα αποτελέσματα OCR σας να είναι πάντα kristall‑clear! 

![Extract text from image example](extract-text-from-image.png "Extract text from image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}